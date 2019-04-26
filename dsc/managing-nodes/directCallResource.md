---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-erőforrások metódusainak közvetlen hívása
ms.openlocfilehash: cf237f638593706e5959e2bcc0d851b0e55baf0e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079625"
---
# <a name="calling-dsc-resource-methods-directly"></a><span data-ttu-id="b230c-103">DSC-erőforrások metódusainak közvetlen hívása</span><span class="sxs-lookup"><span data-stu-id="b230c-103">Calling DSC resource methods directly</span></span>

><span data-ttu-id="b230c-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b230c-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="b230c-105">Használhatja a [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource) parancsmag, amellyel közvetlenül hívja az a funkciók vagy DSC-erőforrás módszerek (a **Get-TargetResource**, **Set-TargetResource**, és  **Test-TargetResource** funkciók MOF-alapú erőforrás, vagy a **első**, **beállítása**, és **teszt** módszer egy adott osztály-alapú erőforrás).</span><span class="sxs-lookup"><span data-stu-id="b230c-105">You can use the [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource) cmdlet to directly call the functions or methods of a DSC resource (The **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions of a MOF-based resource, or the **Get**, **Set**, and **Test** methods of a class-based resource).</span></span>
<span data-ttu-id="b230c-106">Ez használható szeretné használni a DSC-erőforrások harmadik felek, akár egy hasznos eszköz erőforrások fejlesztése során.</span><span class="sxs-lookup"><span data-stu-id="b230c-106">This can be used by third-parties that want to use DSC resources, or as a helpful tool while developing resources.</span></span>

<span data-ttu-id="b230c-107">Ez a parancsmag jellemzően a metaconfiguration tulajdonsággal együtt `refreshMode = 'Disabled'`, függetlenül attól, hogy mi is használható, de **refreshMode** értékre van állítva.</span><span class="sxs-lookup"><span data-stu-id="b230c-107">This cmdlet is typically used in combination with a metaconfiguration property `refreshMode = 'Disabled'`, but it can be used no matter what **refreshMode** is set to.</span></span>

<span data-ttu-id="b230c-108">Hívásakor a **Invoke-DscResource** parancsmaggal, megadhatja mely metódus vagy függvény használatával a **metódus** paraméter.</span><span class="sxs-lookup"><span data-stu-id="b230c-108">When calling the **Invoke-DscResource** cmdlet, you specify which method or function to call by using the **Method** parameter.</span></span> <span data-ttu-id="b230c-109">Az erőforrás tulajdonságainak egy kivonattáblát átadásával értékeként adja meg a **tulajdonság** paraméter.</span><span class="sxs-lookup"><span data-stu-id="b230c-109">You specify the properties of the resource by passing a hashtable as the value of the **Property** parameter.</span></span>

<span data-ttu-id="b230c-110">Az alábbi példák-erőforrások metódusainak közvetlen hívása:</span><span class="sxs-lookup"><span data-stu-id="b230c-110">The following are examples of directly calling resource methods:</span></span>

## <a name="ensure-a-file-is-present"></a><span data-ttu-id="b230c-111">Győződjön meg, hogy egy fájl jelen</span><span class="sxs-lookup"><span data-stu-id="b230c-111">Ensure a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Set -Property @{
                            DestinationPath = "$env:SystemDrive\\DirectAccess.txt";
                            Contents = 'This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="test-that-a-file-is-present"></a><span data-ttu-id="b230c-112">Tesztelje, hogy egy fájl jelen</span><span class="sxs-lookup"><span data-stu-id="b230c-112">Test that a file is present</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Test -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result | fl
```

## <a name="get-the-contents-of-file"></a><span data-ttu-id="b230c-113">Fájl tartalmának beolvasása</span><span class="sxs-lookup"><span data-stu-id="b230c-113">Get the contents of file</span></span>

```powershell
$result = Invoke-DscResource -Name File -Method Get -Property @{
                            DestinationPath="$env:SystemDrive\\DirectAccess.txt";
                            Contents='This file is create by Invoke-DscResource'} -Verbose
$result.ItemValue | fl
```

><span data-ttu-id="b230c-114">**Megjegyzés:** Összetett erőforrások metódusainak közvetlen hívása nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="b230c-114">**Note:** Directly calling composite resource methods is not supported.</span></span> <span data-ttu-id="b230c-115">Ehelyett hívja meg a mögöttes erőforrások, az összetett erőforrás alkotó módszereket.</span><span class="sxs-lookup"><span data-stu-id="b230c-115">Instead, call the methods of the underlying resources that make up the composite resource.</span></span>

## <a name="see-also"></a><span data-ttu-id="b230c-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b230c-116">See Also</span></span>
- [<span data-ttu-id="b230c-117">MOF-egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="b230c-117">Writing a custom DSC resource with MOF</span></span>](../resources/authoringResourceMOF.md)
- [<span data-ttu-id="b230c-118">A PowerShell-osztályok egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="b230c-118">Writing a custom DSC resource with PowerShell classes</span></span>](../resources/authoringResourceClass.md)
- [<span data-ttu-id="b230c-119"> DSC-erőforrások hibakeresése</span><span class="sxs-lookup"><span data-stu-id="b230c-119">Debugging DSC resources</span></span>](../troubleshooting/debugResource.md)