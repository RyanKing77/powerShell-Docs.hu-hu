---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC WindowsPackageCab erőforrás
ms.openlocfilehash: af45956c1fe8cffa1d7fd779847eded9e3f6b51e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowspackagecab-resource"></a><span data-ttu-id="624c0-103">A DSC WindowsPackageCab erőforrás</span><span class="sxs-lookup"><span data-stu-id="624c0-103">DSC WindowsPackageCab Resource</span></span>

> <span data-ttu-id="624c0-104">Vonatkozik: A Windows PowerShell 5.1-es és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="624c0-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="624c0-105">A **WindowsPackageCab** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) telepítéséhez vagy eltávolításához Windows kabinetfájl (.cab) csomagok egy célcsomóponttal mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="624c0-105">The **WindowsPackageCab** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Windows cabinet (.cab) packages on a target node.</span></span>

<span data-ttu-id="624c0-106">A célként megadott csomópont nem rendelkezhet a DISM PowerShell-modul telepítve.</span><span class="sxs-lookup"><span data-stu-id="624c0-106">The target node must have the DISM PowerShell module installed.</span></span> <span data-ttu-id="624c0-107">További információ: [a Windows PowerShell használata a DISM](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/use-dism-in-windows-powershell-s14).</span><span class="sxs-lookup"><span data-stu-id="624c0-107">For information, see [Use DISM in Windows PowerShell](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/use-dism-in-windows-powershell-s14).</span></span>


## <a name="syntax"></a><span data-ttu-id="624c0-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="624c0-108">Syntax</span></span>

```
{
    Name = [string]
    Ensure = [string] { Absent | Present }
    SourcePath = [string]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="624c0-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="624c0-109">Properties</span></span>

|  <span data-ttu-id="624c0-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="624c0-110">Property</span></span>  |  <span data-ttu-id="624c0-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="624c0-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="624c0-112">Név</span><span class="sxs-lookup"><span data-stu-id="624c0-112">Name</span></span>| <span data-ttu-id="624c0-113">A csomag nevét jelöli, a szeretne biztosítani adott állapotú.</span><span class="sxs-lookup"><span data-stu-id="624c0-113">Indicates the name of the package for you want to ensure a specific state.</span></span>|
| <span data-ttu-id="624c0-114">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="624c0-114">Ensure</span></span>| <span data-ttu-id="624c0-115">Azt jelzi, ha a csomag telepítve van-e.</span><span class="sxs-lookup"><span data-stu-id="624c0-115">Indicates if the package is installed.</span></span> <span data-ttu-id="624c0-116">Állítsa be ezt a tulajdonságot "Hiányzik", győződjön meg arról, a csomag nincs telepítve (vagy a csomag eltávolítása, ha telepítve van).</span><span class="sxs-lookup"><span data-stu-id="624c0-116">Set this property to "Absent" to ensure the package is not installed (or uninstall the package if it is installed).</span></span> <span data-ttu-id="624c0-117">Állítsa be azt, hogy "" (az alapértelmezett érték) annak érdekében, hogy a csomag telepítve van.</span><span class="sxs-lookup"><span data-stu-id="624c0-117">Set it to "Present" (the default value) to ensure the package is installed.</span></span>|
| <span data-ttu-id="624c0-118">Elérési út</span><span class="sxs-lookup"><span data-stu-id="624c0-118">Path</span></span>| <span data-ttu-id="624c0-119">Azt jelzi, hogy az elérési utat, amelyen a csomag található.</span><span class="sxs-lookup"><span data-stu-id="624c0-119">Indicates the path where the package resides.</span></span>|
| <span data-ttu-id="624c0-120">LogPath</span><span class="sxs-lookup"><span data-stu-id="624c0-120">LogPath</span></span>| <span data-ttu-id="624c0-121">Azt jelzi, hogy a teljes elérési útja, ha azt szeretné, hogy a szolgáltatót, amelyet telepíteni, vagy távolítsa el a csomagot naplófájlt.</span><span class="sxs-lookup"><span data-stu-id="624c0-121">Indicates the full path where you want the provider to save a log file to install or uninstall the package.</span></span>|
| <span data-ttu-id="624c0-122">dependsOn</span><span class="sxs-lookup"><span data-stu-id="624c0-122">DependsOn</span></span> | <span data-ttu-id="624c0-123">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="624c0-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="624c0-124">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az **ResourceName** és annak típusa **ResourceType**, szintaxisa a következő e tulajdonság használatával "DependsOn ="[ A ResourceType] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="624c0-124">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|

## <a name="example"></a><span data-ttu-id="624c0-125">Példa</span><span class="sxs-lookup"><span data-stu-id="624c0-125">Example</span></span>

<span data-ttu-id="624c0-126">A következő példa konfiguráció bemeneti paraméterek fogadja el, és biztosítja, hogy a kabinetfájl által megadott a `$Name` paraméter van telepítve.</span><span class="sxs-lookup"><span data-stu-id="624c0-126">The following example configuration takes input parameters, and ensures that the .cab file specified by the `$Name` parameter is installed.</span></span>

```powershell
Configuration Sample_WindowsPackageCab
{
    param
    (
        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $Name,

        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $SourcePath,

        [Parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $LogPath
    )

    Import-DscResource -ModuleName 'PSDscResources'

    WindowsPackageCab WindowsPackageCab1
    {
        Name = $Name
        Ensure = 'Present'
        SourcePath = $SourcePath
        LogPath = $LogPath
    }
}
```