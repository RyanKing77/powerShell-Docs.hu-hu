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
# <a name="generate-powershell-cmdlets-based-on-odata-endpoint"></a><span data-ttu-id="2e18f-102">PowerShell-parancsmagok létrehozása OData-végpont alapján</span><span class="sxs-lookup"><span data-stu-id="2e18f-102">Generate PowerShell Cmdlets based on OData Endpoint</span></span>

## <a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint"></a><span data-ttu-id="2e18f-103">Az OData-végpont alapján Windows PowerShell-parancsmagok létrehozása</span><span class="sxs-lookup"><span data-stu-id="2e18f-103">Generate Windows PowerShell cmdlets based on an OData endpoint</span></span>

<span data-ttu-id="2e18f-104">**Exportálás – ODataEndpointProxy** -parancsmag, amely létrehoz egy Windows PowerShell-parancsmagok a megadott OData-végpont által elérhetővé tett funkciók alapján.</span><span class="sxs-lookup"><span data-stu-id="2e18f-104">**Export-ODataEndpointProxy** is a cmdlet that generates a set of Windows PowerShell cmdlets based on the functionality exposed by a given OData endpoint.</span></span>

<span data-ttu-id="2e18f-105">Az alábbi példa bemutatja, hogyan használhatja az új parancsmag:</span><span class="sxs-lookup"><span data-stu-id="2e18f-105">The following example shows how to use this new cmdlet:</span></span>

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

<span data-ttu-id="2e18f-106">Továbbra is vannak fejlesztést, így ezt a funkciót, beleértve többek között, a fő használati eseteit részei:</span><span class="sxs-lookup"><span data-stu-id="2e18f-106">There are still parts of key use cases in development for this functionality, including, but not limited to:</span></span>
-   <span data-ttu-id="2e18f-107">Társítások</span><span class="sxs-lookup"><span data-stu-id="2e18f-107">Associations</span></span>
-   <span data-ttu-id="2e18f-108">Streamek átadása</span><span class="sxs-lookup"><span data-stu-id="2e18f-108">Passing streams</span></span>

## <a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint-with-odatautils"></a><span data-ttu-id="2e18f-109">Az OData-végpont az ODataUtils alapján Windows PowerShell-parancsmagok létrehozása</span><span class="sxs-lookup"><span data-stu-id="2e18f-109">Generate Windows PowerShell cmdlets based on an OData endpoint with ODataUtils</span></span>

<span data-ttu-id="2e18f-110">A ODataUtils modul lehetővé teszi, hogy a Windows PowerShell-parancsmagjait REST-végpontokat, amelyek támogatják az OData generációja.</span><span class="sxs-lookup"><span data-stu-id="2e18f-110">The ODataUtils module allows generation of Windows PowerShell cmdlets from REST endpoints that support OData.</span></span> <span data-ttu-id="2e18f-111">A következő növekményes fejlesztéseket a Microsoft.PowerShell.ODataUtils Windows PowerShell-modul találhatók.</span><span class="sxs-lookup"><span data-stu-id="2e18f-111">The following incremental enhancements are in the Microsoft.PowerShell.ODataUtils Windows PowerShell module.</span></span>
-   <span data-ttu-id="2e18f-112">Csatorna ügyféloldali, kiszolgálóoldali végpontról további információt.</span><span class="sxs-lookup"><span data-stu-id="2e18f-112">Channel additional information from server-side endpoint to client side.</span></span>
-   <span data-ttu-id="2e18f-113">Ügyféloldali lapozási támogatása</span><span class="sxs-lookup"><span data-stu-id="2e18f-113">Client-side paging support</span></span>
-   <span data-ttu-id="2e18f-114">Kiszolgálóoldali szűrés használatával a – Select paraméter</span><span class="sxs-lookup"><span data-stu-id="2e18f-114">Server-side filtering by using the -Select parameter</span></span>
-   <span data-ttu-id="2e18f-115">Webalkalmazás-kérelemfejlécek támogatása</span><span class="sxs-lookup"><span data-stu-id="2e18f-115">Support for web request headers</span></span>

<span data-ttu-id="2e18f-116">A webalkalmazásproxy-parancsmagok az Export-ODataEndPointProxy parancsmag által létrehozott további információkkal (nem szerepel a a ügyféloldali proxy létrehozása során használt $metadata) a kiszolgálóról ügyféloldali OData-végpont (egy új Windows Information Stream A PowerShell 5.0-s szolgáltatás).</span><span class="sxs-lookup"><span data-stu-id="2e18f-116">The proxy cmdlets generated by the Export-ODataEndPointProxy cmdlet provide additional information (not mentioned in the $metadata used during the client-side proxy generation) from the server side OData endpoint on the Information stream (a new Windows PowerShell 5.0 feature).</span></span> <span data-ttu-id="2e18f-117">Íme egy példa adatok beszerzése.</span><span class="sxs-lookup"><span data-stu-id="2e18f-117">Here is an example of how to get that information.</span></span>

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

<span data-ttu-id="2e18f-118">A rekordok érheti el a kiszolgálói oldalon kötegekben, a ügyféloldali lapozási támogatási használatával.</span><span class="sxs-lookup"><span data-stu-id="2e18f-118">You can get the records from the server side in batches by using client-side paging support.</span></span> <span data-ttu-id="2e18f-119">Ez akkor hasznos, ha be kell szereznie egy nagy mennyiségű adatot a kiszolgálóról a hálózaton keresztül.</span><span class="sxs-lookup"><span data-stu-id="2e18f-119">This is useful when you must get a large amount of data from the server over the network.</span></span>

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

<span data-ttu-id="2e18f-120">A létrehozott webalkalmazásproxy-parancsmagok támogatják a – Select paramétert, amely használható egy szűrőt a csak a rekord tulajdonságokat, amelyeket az ügyfélnek kell.</span><span class="sxs-lookup"><span data-stu-id="2e18f-120">The generated proxy cmdlets support the –Select parameter which you can use as a filter to receive only the record properties that the client needs.</span></span> <span data-ttu-id="2e18f-121">Ez csökkenti a hálózaton keresztül továbbított adatok mennyisége, mivel a szűrés a kiszolgálói oldalon történik.</span><span class="sxs-lookup"><span data-stu-id="2e18f-121">This reduces the amount of data that is transferred over the network, because the filtering occurs on the server side.</span></span>

```powershell
# In the below example only the Name property of the
# Product record is retrieved from the server side.
Get-Product -Top 2 -AllowUnsecureConnection -AllowAdditionalData -Select Name
```

<span data-ttu-id="2e18f-122">Az Export-ODataEndpointProxy parancsmagot, és az általa létrehozott webalkalmazásproxy-parancsmagok mostantól támogatják a fejlécek paraméter (egy kivonattáblát értékeket adjon meg), amelyet használhat a channel minden további információt a kiszolgálóoldali OData-végpont által várt.</span><span class="sxs-lookup"><span data-stu-id="2e18f-122">The Export-ODataEndpointProxy cmdlet, and the proxy cmdlets generated by it, now support the Headers parameter (supply values as a hash table), which you can use to channel any additional information that is expected by the server-side OData endpoint.</span></span> <span data-ttu-id="2e18f-123">A következő példában a szolgáltatásokhoz, amelyek egy előfizetési kulcsot hitelesítéshez sebességhez fejlécek keresztül egy előfizetési kulcsot is channel.</span><span class="sxs-lookup"><span data-stu-id="2e18f-123">In the following example, you can channel a Subscription key through Headers for services that are expecting a Subscription key for authentication.</span></span>

```powershell
# As an example, in the below command 'XXXX' is the authentication used by the
# Export-ODataEndpointProxy cmdlet to interact with the server-side
# OData endpoint accessed through $endPointUri.

Export-ODataEndpointProxy -Uri $endPointUri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -Headers @{'subscription-key'='XXXX'}
```
