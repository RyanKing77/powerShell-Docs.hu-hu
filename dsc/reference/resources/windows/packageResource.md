---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-Package erőforrás
ms.openlocfilehash: 9285df71a303c9a53dd50d450272575a64e962e7
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048263"
---
# <a name="dsc-package-resource"></a><span data-ttu-id="827fb-103">DSC-Package erőforrás</span><span class="sxs-lookup"><span data-stu-id="827fb-103">DSC Package Resource</span></span>

<span data-ttu-id="827fb-104">_A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0_</span><span class="sxs-lookup"><span data-stu-id="827fb-104">_Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0_</span></span>

<span data-ttu-id="827fb-105">A **csomag** erőforrás a Windows PowerShell Desired State Configuration (DSC) telepítéséhez vagy eltávolításához a csomagok, például a setup.exe és a Windows Installer csomagokat, a cél csomópont mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="827fb-105">The **Package** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall packages, such as Windows Installer and setup.exe packages, on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="827fb-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="827fb-106">Syntax</span></span>

```
Package [string] #ResourceName
{
    Name = [string]
    Path = [string]
    ProductId = [string]
    [ Arguments = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ ReturnCode = [UInt32[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="827fb-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="827fb-107">Properties</span></span>

| <span data-ttu-id="827fb-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="827fb-108">Property</span></span> | <span data-ttu-id="827fb-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="827fb-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="827fb-110">Név</span><span class="sxs-lookup"><span data-stu-id="827fb-110">Name</span></span>| <span data-ttu-id="827fb-111">Azt jelzi, hogy a csomag, amelyhez szeretne biztosítani egy adott állapot neve.</span><span class="sxs-lookup"><span data-stu-id="827fb-111">Indicates the name of the package for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="827fb-112">Elérési út</span><span class="sxs-lookup"><span data-stu-id="827fb-112">Path</span></span>| <span data-ttu-id="827fb-113">Azt jelzi, hogy az elérési utat, ahol a csomag található.</span><span class="sxs-lookup"><span data-stu-id="827fb-113">Indicates the path where the package resides.</span></span>|
| <span data-ttu-id="827fb-114">Termékazonosító</span><span class="sxs-lookup"><span data-stu-id="827fb-114">ProductId</span></span>| <span data-ttu-id="827fb-115">Azt jelzi, hogy a termék azonosítója, amely egyedileg azonosítja a csomagot.</span><span class="sxs-lookup"><span data-stu-id="827fb-115">Indicates the product ID that uniquely identifies the package.</span></span>|
| <span data-ttu-id="827fb-116">Argumentumok</span><span class="sxs-lookup"><span data-stu-id="827fb-116">Arguments</span></span>| <span data-ttu-id="827fb-117">Felsorolja egy karakterlánc, amely a rendszer átad a csomag pontosan a megadott argumentumok.</span><span class="sxs-lookup"><span data-stu-id="827fb-117">Lists a string of arguments that will be passed to the package exactly as provided.</span></span>|
| <span data-ttu-id="827fb-118">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="827fb-118">Credential</span></span>| <span data-ttu-id="827fb-119">A csomag hozzáférést biztosít a távoli forrás.</span><span class="sxs-lookup"><span data-stu-id="827fb-119">Provides access to the package on a remote source.</span></span> <span data-ttu-id="827fb-120">Ez a tulajdonság nem használatos a csomag telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="827fb-120">This property is not used to install the package.</span></span> <span data-ttu-id="827fb-121">A csomag mindig telepítve van a helyi rendszeren.</span><span class="sxs-lookup"><span data-stu-id="827fb-121">The package is always installed on the local system.</span></span>|
| <span data-ttu-id="827fb-122">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="827fb-122">Ensure</span></span>| <span data-ttu-id="827fb-123">Azt jelzi, hogy telepítve van-e a csomag.</span><span class="sxs-lookup"><span data-stu-id="827fb-123">Indicates if the package is installed.</span></span> <span data-ttu-id="827fb-124">Állítsa be ezt a tulajdonságot a "Hiányzó", győződjön meg arról, a csomag nincs telepítve (vagy távolítsa el a csomagot, ha telepítve van).</span><span class="sxs-lookup"><span data-stu-id="827fb-124">Set this property to "Absent" to ensure the package is not installed (or uninstall the package if it is installed).</span></span> <span data-ttu-id="827fb-125">Állítsa be azt, hogy "" (az alapértelmezett érték) annak érdekében, hogy a csomag telepítése.</span><span class="sxs-lookup"><span data-stu-id="827fb-125">Set it to "Present" (the default value) to ensure the package is installed.</span></span>|
| <span data-ttu-id="827fb-126">LogPath</span><span class="sxs-lookup"><span data-stu-id="827fb-126">LogPath</span></span>| <span data-ttu-id="827fb-127">Azt jelzi, hogy a teljes elérési útja, ahol azt szeretné, hogy a szolgáltató telepítéséhez, vagy távolítsa el a csomagot a naplófájl mentéséhez.</span><span class="sxs-lookup"><span data-stu-id="827fb-127">Indicates the full path where you want the provider to save a log file to install or uninstall the package.</span></span>|
| <span data-ttu-id="827fb-128">DependsOn</span><span class="sxs-lookup"><span data-stu-id="827fb-128">DependsOn</span></span> | <span data-ttu-id="827fb-129">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="827fb-129">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="827fb-130">Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="827fb-130">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="827fb-131">Visszatérési kód:</span><span class="sxs-lookup"><span data-stu-id="827fb-131">ReturnCode</span></span>| <span data-ttu-id="827fb-132">Azt jelzi, hogy a várt visszatérési kódot.</span><span class="sxs-lookup"><span data-stu-id="827fb-132">Indicates the expected return code.</span></span> <span data-ttu-id="827fb-133">Ha a tényleges visszatérési kód nem egyezik a várt értéknek. Itt, elérhető, a konfigurációs hibát adnak vissza.</span><span class="sxs-lookup"><span data-stu-id="827fb-133">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>|

## <a name="example"></a><span data-ttu-id="827fb-134">Példa</span><span class="sxs-lookup"><span data-stu-id="827fb-134">Example</span></span>

<span data-ttu-id="827fb-135">Ebben a példában futtatja a .msi-telepítőt, a megadott elérési úton található, és a megadott termék azonosítója.</span><span class="sxs-lookup"><span data-stu-id="827fb-135">This example runs the .msi installer that is located at the specified path and has the specified product ID.</span></span>

```powershell
Configuration PackageTest
{
    Package PackageExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Path        = "$Env:SystemDrive\TestFolder\TestProject.msi"
        Name        = "TestPackage"
        ProductId   = "ACDDCDAF-80C6-41E6-A1B9-8ABD8A05027E"
    }
}
```