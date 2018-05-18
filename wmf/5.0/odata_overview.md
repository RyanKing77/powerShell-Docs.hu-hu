---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 01d4989711c22db20431876c52740afb350caad0
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="generate-powershell-cmdlets-based-on-odata-endpoint"></a><span data-ttu-id="bdf31-102">PowerShell-parancsmagok létrehozása OData-végpont alapján</span><span class="sxs-lookup"><span data-stu-id="bdf31-102">Generate PowerShell Cmdlets based on OData Endpoint</span></span>
<a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint"></a><span data-ttu-id="bdf31-103">Windows PowerShell-parancsmagok alapján egy OData-végpont létrehozása</span><span class="sxs-lookup"><span data-stu-id="bdf31-103">Generate Windows PowerShell cmdlets based on an OData endpoint</span></span>
--------------------------------------------------------------

<span data-ttu-id="bdf31-104">**Export-ODataEndpointProxy** parancsmag létrehoz egy Windows PowerShell-parancsmagok által megadott OData-végpont funkciókon alapulnak.</span><span class="sxs-lookup"><span data-stu-id="bdf31-104">**Export-ODataEndpointProxy** is a cmdlet that generates a set of Windows PowerShell cmdlets based on the functionality exposed by a given OData endpoint.</span></span>

<span data-ttu-id="bdf31-105">A következő példa bemutatja, hogyan használja a következő új parancsmagot:</span><span class="sxs-lookup"><span data-stu-id="bdf31-105">The following example shows how to use this new cmdlet:</span></span>

<span data-ttu-id="bdf31-106">\# Az Export-ODataEndpointProxy alapvető használati eset</span><span class="sxs-lookup"><span data-stu-id="bdf31-106">\# Basic use case of Export-ODataEndpointProxy</span></span>

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

<span data-ttu-id="bdf31-107">Még vannak főbb használati esetek fejlesztési erre a funkcióra, de nem kizárólagosan beleértve a részei:</span><span class="sxs-lookup"><span data-stu-id="bdf31-107">There are still parts of key use cases in development for this functionality, including, but not limited to:</span></span>
-   <span data-ttu-id="bdf31-108">Társítások</span><span class="sxs-lookup"><span data-stu-id="bdf31-108">Associations</span></span>
-   <span data-ttu-id="bdf31-109">Sikeres adatfolyamok</span><span class="sxs-lookup"><span data-stu-id="bdf31-109">Passing streams</span></span>

<a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint-with-odatautils"></a><span data-ttu-id="bdf31-110">Windows PowerShell-parancsmagok egy OData-végpont a ODataUtils alapján készítése</span><span class="sxs-lookup"><span data-stu-id="bdf31-110">Generate Windows PowerShell cmdlets based on an OData endpoint with ODataUtils</span></span>
------------------------------------------------------------------------------
<span data-ttu-id="bdf31-111">A ODataUtils modul lehetővé teszi, hogy a Windows PowerShell-parancsmagok az OData-t támogató REST-végpontok előállítását.</span><span class="sxs-lookup"><span data-stu-id="bdf31-111">The ODataUtils module allows generation of Windows PowerShell cmdlets from REST endpoints that support OData.</span></span> <span data-ttu-id="bdf31-112">A következő növekményes fejlesztéseket Microsoft.PowerShell.ODataUtils Windows PowerShell-modul szerepelnek.</span><span class="sxs-lookup"><span data-stu-id="bdf31-112">The following incremental enhancements are in the Microsoft.PowerShell.ODataUtils Windows PowerShell module.</span></span>
-   <span data-ttu-id="bdf31-113">További információ a kiszolgálóoldali végpont az ügyféloldali csatorna.</span><span class="sxs-lookup"><span data-stu-id="bdf31-113">Channel additional information from server-side endpoint to client side.</span></span>
-   <span data-ttu-id="bdf31-114">Ügyféloldali lapozás támogatása</span><span class="sxs-lookup"><span data-stu-id="bdf31-114">Client-side paging support</span></span>
-   <span data-ttu-id="bdf31-115">Kiszolgálóoldali szűrés használatával a – Select paraméter</span><span class="sxs-lookup"><span data-stu-id="bdf31-115">Server-side filtering by using the -Select parameter</span></span>
-   <span data-ttu-id="bdf31-116">Webes kérelemfejléc támogatása</span><span class="sxs-lookup"><span data-stu-id="bdf31-116">Support for web request headers</span></span>

<span data-ttu-id="bdf31-117">Az Export-ODataEndPointProxy parancsmag által létrehozott webalkalmazásproxy-parancsmagok további információkkal (nem szerepel a ügyféloldali proxy létrehozása során használt $metadata) a kiszolgáló oldalán OData-végpont az információk adatfolyamon (egy új Windows PowerShell 5.0 szolgáltatáshoz).</span><span class="sxs-lookup"><span data-stu-id="bdf31-117">The proxy cmdlets generated by the Export-ODataEndPointProxy cmdlet provide additional information (not mentioned in the $metadata used during the client-side proxy generation) from the server side OData endpoint on the Information stream (a new Windows PowerShell 5.0 feature).</span></span> <span data-ttu-id="bdf31-118">Itt található példa bemutatja, hogyan ezt az információt lekérni.</span><span class="sxs-lookup"><span data-stu-id="bdf31-118">Here is an example of how to get that information.</span></span>
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

<span data-ttu-id="bdf31-119">A kiszolgáló oldalán kötegekben az a rekordok ügyféloldali lapozás támogatása használatával kérheti le.</span><span class="sxs-lookup"><span data-stu-id="bdf31-119">You can get the records from the server side in batches by using client-side paging support.</span></span> <span data-ttu-id="bdf31-120">Ez akkor hasznos, ha ha előbb telepítik azokra a nagy mennyiségű adatot a kiszolgálóról a hálózaton keresztül.</span><span class="sxs-lookup"><span data-stu-id="bdf31-120">This is useful when you must get a large amount of data from the server over the network.</span></span>
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

<span data-ttu-id="bdf31-121">A létrehozott webalkalmazásproxy-parancsmagok támogatja a – Select paraméter, amely használható szűrőként a csak a rekord tulajdonságokat, amelyeket az ügyfélnek.</span><span class="sxs-lookup"><span data-stu-id="bdf31-121">The generated proxy cmdlets support the –Select parameter which you can use as a filter to receive only the record properties that the client needs.</span></span> <span data-ttu-id="bdf31-122">Ez csökkenti a hálózaton keresztül továbbított adatmennyiséget, mert a kiszolgáló oldalán a szűrés történik.</span><span class="sxs-lookup"><span data-stu-id="bdf31-122">This reduces the amount of data that is transferred over the network, because the filtering occurs on the server side.</span></span>
```powershell
# In the below example only the Name property of the
# Product record is retrieved from the server side.
Get-Product -Top 2 -AllowUnsecureConnection -AllowAdditionalData -Select Name
```

<span data-ttu-id="bdf31-123">Az Export-ODataEndpointProxy parancsmag és az általa létrehozott webalkalmazásproxy-parancsmagok mostantól támogatja a fejlécek paraméter (ellátási értékeinek egy kivonattáblát), amely azokat az adatokat a kiszolgálóoldali OData-végpont által várt csatorna segítségével.</span><span class="sxs-lookup"><span data-stu-id="bdf31-123">The Export-ODataEndpointProxy cmdlet, and the proxy cmdlets generated by it, now support the Headers parameter (supply values as a hash table), which you can use to channel any additional information that is expected by the server-side OData endpoint.</span></span> <span data-ttu-id="bdf31-124">A következő példában egy előfizetés kulcs egy előfizetés kulcs hitelesítéshez számított szolgáltatások fejlécek keresztül is csatorna.</span><span class="sxs-lookup"><span data-stu-id="bdf31-124">In the following example, you can channel a Subscription key through Headers for services that are expecting a Subscription key for authentication.</span></span>
```powershell
# As an example, in the below command 'XXXX' is the authentication used by the
# Export-ODataEndpointProxy cmdlet to interact with the server-side
# OData endpoint accessed through $endPointUri.

Export-ODataEndpointProxy -Uri $endPointUri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -Headers @{'subscription-key'='XXXX'}
```
