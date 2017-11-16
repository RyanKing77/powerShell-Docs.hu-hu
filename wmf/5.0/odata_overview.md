---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 11891587f59dc8a38e4ce267018160f7f9a28178
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="generate-powershell-cmdlets-based-on-odata-endpoint"></a>PowerShell-parancsmagok alapján OData-végpont létrehozása
<a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint"></a>Windows PowerShell-parancsmagok alapján egy OData-végpont létrehozása
--------------------------------------------------------------

**Export-ODataEndpointProxy** parancsmag létrehoz egy Windows PowerShell-parancsmagok által megadott OData-végpont funkciókon alapulnak.

A következő példa bemutatja, hogyan használja a következő új parancsmagot:

\#Az Export-ODataEndpointProxy alapvető használati eset

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

Még vannak főbb használati esetek fejlesztési erre a funkcióra, de nem kizárólagosan beleértve a részei:
-   Társítások
-   Sikeres adatfolyamok

<a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint-with-odatautils"></a>Windows PowerShell-parancsmagok egy OData-végpont a ODataUtils alapján készítése
------------------------------------------------------------------------------
A ODataUtils modul lehetővé teszi, hogy a Windows PowerShell-parancsmagok az OData-t támogató REST-végpontok előállítását. A következő növekményes fejlesztéseket Microsoft.PowerShell.ODataUtils Windows PowerShell-modul szerepelnek.
-   További információ a kiszolgálóoldali végpont az ügyféloldali csatorna.
-   Ügyféloldali lapozás támogatása
-   Kiszolgálóoldali szűrés használatával a – Select paraméter
-   Webes kérelemfejléc támogatása

Az Export-ODataEndPointProxy parancsmag által létrehozott webalkalmazásproxy-parancsmagok további információkkal (nem szerepel a ügyféloldali proxy létrehozása során használt $metadata) a kiszolgáló oldalán OData-végpont az információk adatfolyamon (egy új Windows PowerShell 5.0 szolgáltatáshoz). Itt található példa bemutatja, hogyan ezt az információt lekérni.
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

A kiszolgáló oldalán kötegekben az a rekordok ügyféloldali lapozás támogatása használatával kérheti le. Ez akkor hasznos, ha ha előbb telepítik azokra a nagy mennyiségű adatot a kiszolgálóról a hálózaton keresztül.
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

A létrehozott webalkalmazásproxy-parancsmagok támogatja a – Select paraméter, amely használható szűrőként a csak a rekord tulajdonságokat, amelyeket az ügyfélnek. Ez csökkenti a hálózaton keresztül továbbított adatmennyiséget, mert a kiszolgáló oldalán a szűrés történik.
```powershell
# In the below example only the Name property of the
# Product record is retrieved from the server side.
Get-Product -Top 2 -AllowUnsecureConnection -AllowAdditionalData -Select Name
```

Az Export-ODataEndpointProxy parancsmag és az általa létrehozott webalkalmazásproxy-parancsmagok mostantól támogatja a fejlécek paraméter (ellátási értékeinek egy kivonattáblát), amely azokat az adatokat a kiszolgálóoldali OData-végpont által várt csatorna segítségével. A következő példában egy előfizetés kulcs egy előfizetés kulcs hitelesítéshez számított szolgáltatások fejlécek keresztül is csatorna.
```powershell
# As an example, in the below command 'XXXX' is the authentication used by the
# Export-ODataEndpointProxy cmdlet to interact with the server-side
# OData endpoint accessed through $endPointUri.

Export-ODataEndpointProxy -Uri $endPointUri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -Headers @{'subscription-key'='XXXX'}
```

