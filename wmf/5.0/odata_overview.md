---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 1153738fdf6f926d5d819bbf91450408dcb17f71
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794491"
---
# <a name="generate-powershell-cmdlets-based-on-odata-endpoint"></a>PowerShell-parancsmagok létrehozása OData-végpont alapján

## <a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint"></a>Az OData-végpont alapján Windows PowerShell-parancsmagok létrehozása

**Exportálás – ODataEndpointProxy** -parancsmag, amely létrehoz egy Windows PowerShell-parancsmagok a megadott OData-végpont által elérhetővé tett funkciók alapján.

Az alábbi példa bemutatja, hogyan használhatja az új parancsmag:

```powershell
Export-ODataEndpointProxy -Uri 'http://services.odata.org/v3/(S(snyobsk1hhutkb2yulwldgf1))/odata/odata.svc' -OutputModule C:\Users\user\Generated.psd1

ipmo 'C:\Users\user\Generated.psd1'
# Cmdlets are created based on the following heuristics
# New-<EntityType> -<Key> [-<Other Attributes>]
#
# Get-<EntityType> [-<Key> -Top –Skip –Filter -OrderBy]
# # If there is a complex key, the keys will actually be -<Key1> -<Key2>…
# # Note this rule applies to any other instances of the key
#
# Set-<EntityType> -<Key> [-<Other Attributes>]
#
# Remove-<EntityType> -<Key>
#
# Invoke-<EntityType><Action> [-<Key> -<Other Parameters>]
#
#
# Cmdlets from associations (Note: Get and Remove get additional parameter sets)
# Get-<EntityType> -<AssociatedEntity>
# New-<EntityType> -<AssociatedEntity> -<Key>
# Remove-<EntityType> -<AssociatedEntity> -<Key>
#
#
# Note: Every cmdlet has the –ConnectionURI parameter for explicitly setting the URI of the endpoint. This normally uses the same address that you gave the Export-ODataEndpointProxy cmdlet, but can be overridden in this fashion for the sake of similar endpoints.
#
```

Továbbra is vannak fejlesztést, így ezt a funkciót, beleértve többek között, a fő használati eseteit részei:
-   Társítások
-   Streamek átadása

## <a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint-with-odatautils"></a>Az OData-végpont az ODataUtils alapján Windows PowerShell-parancsmagok létrehozása

A ODataUtils modul lehetővé teszi, hogy a Windows PowerShell-parancsmagjait REST-végpontokat, amelyek támogatják az OData generációja. A következő növekményes fejlesztéseket a Microsoft.PowerShell.ODataUtils Windows PowerShell-modul találhatók.
-   Csatorna ügyféloldali, kiszolgálóoldali végpontról további információt.
-   Ügyféloldali lapozási támogatása
-   Kiszolgálóoldali szűrés használatával a – Select paraméter
-   Webalkalmazás-kérelemfejlécek támogatása

A webalkalmazásproxy-parancsmagok az Export-ODataEndPointProxy parancsmag által létrehozott további információkkal (nem szerepel a a ügyféloldali proxy létrehozása során használt $metadata) a kiszolgálóról ügyféloldali OData-végpont (egy új Windows Information Stream A PowerShell 5.0-s szolgáltatás). Íme egy példa adatok beszerzése.

```powershell
Import-Module Microsoft.PowerShell.ODataUtils -Force
$generatedProxyModuleDir = Join-Path -Path $env:SystemDrive -ChildPath 'ODataDemoProxy'
$uri = "http://services.odata.org/V3/(S(fhleiief23wrm5a5nhf542q5))/OData/OData.svc/"
Export-ODataEndpointProxy -Uri $uri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -AllowClobber
Import-Module $generatedProxyModuleDir -Force

# In the below command, we are retrieving top 1 product.
# By specifying -IncludeTotalResponseCount parameter,
# we are getting the total count of all the Product records
# available on the server side. This information
# is surfaced on the client side through the Information stream.
$product = Get-Product -Top 1 -AllowUnsecureConnection -AllowAdditionalData -IncludeTotalResponseCount -InformationVariable infoStream
# The Information stream contains the additional
# information sent from the server side.
$additionalInfo = $infoStream.GetEnumerator() | % MessageData
# 'Odata.Count' indicates the total product records
# available on the server side Odata endpoint.
$additionalInfo['odata.count']
```

A rekordok érheti el a kiszolgálói oldalon kötegekben, a ügyféloldali lapozási támogatási használatával. Ez akkor hasznos, ha be kell szereznie egy nagy mennyiségű adatot a kiszolgálóról a hálózaton keresztül.

```powershell
$skipCount = 0
$batchSize = 3
# Client-Side Paging Support: The records from the server side
# are retrieved in batches of $batchSize
while($skipCount -le $additionalInfo['odata.count'])
{
Get-Product -AllowUnsecureConnection -AllowAdditionalData -Top $batchSize -Skip $skipCount
$skipCount += $batchSize
}
```

A létrehozott webalkalmazásproxy-parancsmagok támogatják a – Select paramétert, amely használható egy szűrőt a csak a rekord tulajdonságokat, amelyeket az ügyfélnek kell. Ez csökkenti a hálózaton keresztül továbbított adatok mennyisége, mivel a szűrés a kiszolgálói oldalon történik.

```powershell
# In the below example only the Name property of the
# Product record is retrieved from the server side.
Get-Product -Top 2 -AllowUnsecureConnection -AllowAdditionalData -Select Name
```

Az Export-ODataEndpointProxy parancsmagot, és az általa létrehozott webalkalmazásproxy-parancsmagok mostantól támogatják a fejlécek paraméter (egy kivonattáblát értékeket adjon meg), amelyet használhat a channel minden további információt a kiszolgálóoldali OData-végpont által várt. A következő példában a szolgáltatásokhoz, amelyek egy előfizetési kulcsot hitelesítéshez sebességhez fejlécek keresztül egy előfizetési kulcsot is channel.

```powershell
# As an example, in the below command 'XXXX' is the authentication used by the
# Export-ODataEndpointProxy cmdlet to interact with the server-side
# OData endpoint accessed through $endPointUri.

Export-ODataEndpointProxy -Uri $endPointUri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -Headers @{'subscription-key'='XXXX'}
```
