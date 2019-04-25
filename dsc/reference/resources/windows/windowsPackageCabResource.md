---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WindowsPackageCab Resource
ms.openlocfilehash: 035944e7ca5c7469250c48a19b79f2f2d5d38e9a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076939"
---
# <a name="dsc-windowspackagecab-resource"></a><span data-ttu-id="27d40-103">DSC WindowsPackageCab Resource</span><span class="sxs-lookup"><span data-stu-id="27d40-103">DSC WindowsPackageCab Resource</span></span>

> <span data-ttu-id="27d40-104">A következőkre vonatkozik: Windows PowerShell 5.1-es és újabb verziók</span><span class="sxs-lookup"><span data-stu-id="27d40-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="27d40-105">A **WindowsPackageCab** erőforrás a Windows PowerShell Desired State Configuration (DSC) telepítéséhez vagy eltávolításához Windows kabinetfájl (.cab) csomagokat egy célcsomóponttal a mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="27d40-105">The **WindowsPackageCab** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall Windows cabinet (.cab) packages on a target node.</span></span>

<span data-ttu-id="27d40-106">A célcsomópont rendelkeznie kell a DISM PowerShell-modul telepítve van.</span><span class="sxs-lookup"><span data-stu-id="27d40-106">The target node must have the DISM PowerShell module installed.</span></span> <span data-ttu-id="27d40-107">További információ: [a Windows PowerShell használata a DISM](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/use-dism-in-windows-powershell-s14).</span><span class="sxs-lookup"><span data-stu-id="27d40-107">For information, see [Use DISM in Windows PowerShell](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/use-dism-in-windows-powershell-s14).</span></span>


## <a name="syntax"></a><span data-ttu-id="27d40-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="27d40-108">Syntax</span></span>

```
{
    Name = [string]
    Ensure = [string] { Absent | Present }
    SourcePath = [string]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="27d40-109">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="27d40-109">Properties</span></span>

|  <span data-ttu-id="27d40-110">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="27d40-110">Property</span></span>  |  <span data-ttu-id="27d40-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="27d40-111">Description</span></span>   |
|---|---|
| <span data-ttu-id="27d40-112">Név</span><span class="sxs-lookup"><span data-stu-id="27d40-112">Name</span></span>| <span data-ttu-id="27d40-113">Azt jelzi, a csomag nevét, a szeretne biztosítani adott állapotú.</span><span class="sxs-lookup"><span data-stu-id="27d40-113">Indicates the name of the package for you want to ensure a specific state.</span></span>|
| <span data-ttu-id="27d40-114">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="27d40-114">Ensure</span></span>| <span data-ttu-id="27d40-115">Azt jelzi, hogy telepítve van-e a csomag.</span><span class="sxs-lookup"><span data-stu-id="27d40-115">Indicates if the package is installed.</span></span> <span data-ttu-id="27d40-116">Állítsa be ezt a tulajdonságot a "Hiányzó", győződjön meg arról, a csomag nincs telepítve (vagy távolítsa el a csomagot, ha telepítve van).</span><span class="sxs-lookup"><span data-stu-id="27d40-116">Set this property to "Absent" to ensure the package is not installed (or uninstall the package if it is installed).</span></span> <span data-ttu-id="27d40-117">Állítsa be azt, hogy "" (az alapértelmezett érték) annak érdekében, hogy a csomag telepítése.</span><span class="sxs-lookup"><span data-stu-id="27d40-117">Set it to "Present" (the default value) to ensure the package is installed.</span></span>|
| <span data-ttu-id="27d40-118">Elérési út</span><span class="sxs-lookup"><span data-stu-id="27d40-118">Path</span></span>| <span data-ttu-id="27d40-119">Azt jelzi, hogy az elérési utat, ahol a csomag található.</span><span class="sxs-lookup"><span data-stu-id="27d40-119">Indicates the path where the package resides.</span></span>|
| <span data-ttu-id="27d40-120">LogPath</span><span class="sxs-lookup"><span data-stu-id="27d40-120">LogPath</span></span>| <span data-ttu-id="27d40-121">Azt jelzi, hogy a teljes elérési útja, ahol azt szeretné, hogy a szolgáltató telepítéséhez, vagy távolítsa el a csomagot a naplófájl mentéséhez.</span><span class="sxs-lookup"><span data-stu-id="27d40-121">Indicates the full path where you want the provider to save a log file to install or uninstall the package.</span></span>|
| <span data-ttu-id="27d40-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="27d40-122">DependsOn</span></span> | <span data-ttu-id="27d40-123">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="27d40-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="27d40-124">Például, ha az erőforrás-konfiguráció azonosítója parancsfájl-blokk futtatni kívánt első az **ResourceName** és a típusa **ResourceType**, esetén ez a tulajdonság használatával "DependsOn"[a = Erőforrástípus] ResourceName"s".</span><span class="sxs-lookup"><span data-stu-id="27d40-124">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|

## <a name="example"></a><span data-ttu-id="27d40-125">Példa</span><span class="sxs-lookup"><span data-stu-id="27d40-125">Example</span></span>

<span data-ttu-id="27d40-126">Az alábbi példa konfiguráció szükséges bemeneti paramétereket, és biztosítja, hogy a .cab-fájl által meghatározott a `$Name` paraméter van telepítve.</span><span class="sxs-lookup"><span data-stu-id="27d40-126">The following example configuration takes input parameters, and ensures that the .cab file specified by the `$Name` parameter is installed.</span></span>

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