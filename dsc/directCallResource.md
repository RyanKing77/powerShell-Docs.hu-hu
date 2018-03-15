---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Közvetlenül a DSC-erőforrás metódusok meghívása"
ms.openlocfilehash: 68344d1be5c41e5ce4660e0a62019fa0a52c2541
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="calling-dsc-resource-methods-directly"></a><span data-ttu-id="80ee5-103">Közvetlenül a DSC-erőforrás metódusok meghívása</span><span class="sxs-lookup"><span data-stu-id="80ee5-103">Calling DSC resource methods directly</span></span>

><span data-ttu-id="80ee5-104">Vonatkozik: A Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="80ee5-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="80ee5-105">Használhatja a [Invoke-DscResource](https://technet.microsoft.com/library/mt517869.aspx) parancsmagot hívja közvetlenül a funkciók vagy DSC erőforrás módszerek (a **Get-TargetResource**, **Set-TargetResource**, és  **Test-TargetResource** funkciók MOF-alapú erőforrás, vagy a **beolvasása**, **beállítása**, és **teszt** osztály-alapú erőforrás módszerek).</span><span class="sxs-lookup"><span data-stu-id="80ee5-105">You can use the [Invoke-DscResource](https://technet.microsoft.com/library/mt517869.aspx) cmdlet to directly call the functions or methods of a DSC resource (The **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions of a MOF-based resource, or the **Get**, **Set**, and **Test** methods of a class-based resource).</span></span> <span data-ttu-id="80ee5-106">Ez használható DSC erőforrások használni kívánt harmadik felek által vagy hasznos eszközként erőforrások fejlesztése során.</span><span class="sxs-lookup"><span data-stu-id="80ee5-106">This can be used by third-parties that want to use DSC resources, or as a helpful tool while developing resources.</span></span> 

<span data-ttu-id="80ee5-107">Ez a parancsmag jellemzően metakonfigurációját tulajdonsággal együtt `refreshMode = 'Disabled'`, függetlenül attól, hogy mi is használható, de **refreshMode** értékre van állítva.</span><span class="sxs-lookup"><span data-stu-id="80ee5-107">This cmdlet is typically used in combination with a metaconfiguration property `refreshMode = 'Disabled'`, but it can be used no matter what **refreshMode** is set to.</span></span>

<span data-ttu-id="80ee5-108">Ha előhívja a **Invoke-DscResource** parancsmaggal, megadhatja mely metódus vagy függvény használatával a **metódus** paraméter.</span><span class="sxs-lookup"><span data-stu-id="80ee5-108">When calling the **Invoke-DscResource** cmdlet, you specify which method or function to call by using the **Method** parameter.</span></span> <span data-ttu-id="80ee5-109">Az erőforrás tulajdonságait úgy, hogy egy kivonattáblát értékeként adja meg a **tulajdonság** paraméter.</span><span class="sxs-lookup"><span data-stu-id="80ee5-109">You specify the properties of the resource by passing a hashtable as the value of the **Property** parameter.</span></span>

<span data-ttu-id="80ee5-110">A következő példák-k közvetlen hívásakor erőforrás módszerek:</span><span class="sxs-lookup"><span data-stu-id="80ee5-110">The following are examples of directly calling resource methods:</span></span>

## <a name="ensure-a-file-is-present"></a><span data-ttu-id="80ee5-111">Győződjön meg arról, egy fájl jelen</span><span class="sxs-lookup"><span data-stu-id="80ee5-111">Ensure a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a><span data-ttu-id="80ee5-112">Tesztelje, hogy a fájl megtalálható-e</span><span class="sxs-lookup"><span data-stu-id="80ee5-112">Test that a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a><span data-ttu-id="80ee5-113">A fájl tartalmának beolvasása</span><span class="sxs-lookup"><span data-stu-id="80ee5-113">Get the contents of file</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

><span data-ttu-id="80ee5-114">**Megjegyzés:** közvetlen összetett erőforrás metódusok meghívása nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="80ee5-114">**Note:** Directly calling composite resource methods is not supported.</span></span> <span data-ttu-id="80ee5-115">Ehelyett hívása az alapul szolgáló erőforrások, az összetett erőforrás alkotó módszerek.</span><span class="sxs-lookup"><span data-stu-id="80ee5-115">Instead, call the methods of the underlying resources that make up the composite resource.</span></span>

## <a name="see-also"></a><span data-ttu-id="80ee5-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="80ee5-116">See Also</span></span>
- [<span data-ttu-id="80ee5-117">Egyéni DSC-erőforrás MOF írása</span><span class="sxs-lookup"><span data-stu-id="80ee5-117">Writing a custom DSC resource with MOF</span></span>](authoringResourceMOF.md) 
- [<span data-ttu-id="80ee5-118">A PowerShell osztályok egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="80ee5-118">Writing a custom DSC resource with PowerShell classes</span></span>](authoringResourceClass.md)
- [<span data-ttu-id="80ee5-119"> DSC-erőforrások hibakeresése</span><span class="sxs-lookup"><span data-stu-id="80ee5-119">Debugging DSC resources</span></span>](debugResource.md)

