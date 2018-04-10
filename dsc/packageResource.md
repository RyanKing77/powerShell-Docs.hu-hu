---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-csomag erőforrás
ms.openlocfilehash: cfa9d53d5ea588b0ec97e5503302a451caa09e03
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-package-resource"></a><span data-ttu-id="7f2f0-103">A DSC-csomag erőforrás</span><span class="sxs-lookup"><span data-stu-id="7f2f0-103">DSC Package Resource</span></span>

> <span data-ttu-id="7f2f0-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="7f2f0-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="7f2f0-105">A **csomag** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) telepítéséhez vagy eltávolításához csomagok, például a setup.exe és a Windows Installer-csomagokat a egy célcsomóponttal mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-105">The **Package** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to install or uninstall packages, such as Windows Installer and setup.exe packages, on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="7f2f0-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7f2f0-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="7f2f0-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="7f2f0-107">Properties</span></span>
|  <span data-ttu-id="7f2f0-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="7f2f0-108">Property</span></span>  |  <span data-ttu-id="7f2f0-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="7f2f0-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="7f2f0-110">Név</span><span class="sxs-lookup"><span data-stu-id="7f2f0-110">Name</span></span>| <span data-ttu-id="7f2f0-111">Azt jelzi, amelyekhez egy adott állapot biztosításához a csomag nevét.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-111">Indicates the name of the package for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="7f2f0-112">Elérési út</span><span class="sxs-lookup"><span data-stu-id="7f2f0-112">Path</span></span>| <span data-ttu-id="7f2f0-113">Azt jelzi, hogy az elérési utat, amelyen a csomag található.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-113">Indicates the path where the package resides.</span></span>|
| <span data-ttu-id="7f2f0-114">Termékazonosító</span><span class="sxs-lookup"><span data-stu-id="7f2f0-114">ProductId</span></span>| <span data-ttu-id="7f2f0-115">Azt jelzi, hogy a termék azonosítója, amely egyedileg azonosítja a csomagot.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-115">Indicates the product ID that uniquely identifies the package.</span></span>|
| <span data-ttu-id="7f2f0-116">Argumentumok</span><span class="sxs-lookup"><span data-stu-id="7f2f0-116">Arguments</span></span>| <span data-ttu-id="7f2f0-117">Az átadott csomag pontosan megegyezik a megadott argumentumok karakterlánc sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-117">Lists a string of arguments that will be passed to the package exactly as provided.</span></span>|
| <span data-ttu-id="7f2f0-118">hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="7f2f0-118">Credential</span></span>| <span data-ttu-id="7f2f0-119">A csomag hozzáférést biztosít a távoli adatforráson.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-119">Provides access to the package on a remote source.</span></span> <span data-ttu-id="7f2f0-120">Ez a tulajdonság nem használható a csomag telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-120">This property is not used to install the package.</span></span> <span data-ttu-id="7f2f0-121">A csomag mindig telepítve van a helyi rendszeren.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-121">The package is always installed on the local system.</span></span>|
| <span data-ttu-id="7f2f0-122">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="7f2f0-122">Ensure</span></span>| <span data-ttu-id="7f2f0-123">Azt jelzi, ha a csomag telepítve van-e.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-123">Indicates if the package is installed.</span></span> <span data-ttu-id="7f2f0-124">Állítsa be ezt a tulajdonságot "Hiányzik", győződjön meg arról, a csomag nincs telepítve (vagy a csomag eltávolítása, ha telepítve van).</span><span class="sxs-lookup"><span data-stu-id="7f2f0-124">Set this property to "Absent" to ensure the package is not installed (or uninstall the package if it is installed).</span></span> <span data-ttu-id="7f2f0-125">Állítsa be azt, hogy "" (az alapértelmezett érték) annak érdekében, hogy a csomag telepítve van.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-125">Set it to "Present" (the default value) to ensure the package is installed.</span></span>|
| <span data-ttu-id="7f2f0-126">LogPath</span><span class="sxs-lookup"><span data-stu-id="7f2f0-126">LogPath</span></span>| <span data-ttu-id="7f2f0-127">Azt jelzi, hogy a teljes elérési útja, ha azt szeretné, hogy a szolgáltatót, amelyet telepíteni, vagy távolítsa el a csomagot naplófájlt.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-127">Indicates the full path where you want the provider to save a log file to install or uninstall the package.</span></span>|
| <span data-ttu-id="7f2f0-128">dependsOn</span><span class="sxs-lookup"><span data-stu-id="7f2f0-128">DependsOn</span></span> | <span data-ttu-id="7f2f0-129">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-129">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="7f2f0-130">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az **ResourceName** és annak típusa **ResourceType**, szintaxisa a következő e tulajdonság használatával "DependsOn ="[ A ResourceType] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="7f2f0-130">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|
| <span data-ttu-id="7f2f0-131">Visszatérési kód:</span><span class="sxs-lookup"><span data-stu-id="7f2f0-131">ReturnCode</span></span>| <span data-ttu-id="7f2f0-132">Azt jelzi, hogy a várt visszatérési kód.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-132">Indicates the expected return code.</span></span> <span data-ttu-id="7f2f0-133">Ha a tényleges visszatérési kód nem egyezik a várt érték megadva itt, a konfigurációs hibát adnak vissza.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-133">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>|

## <a name="example"></a><span data-ttu-id="7f2f0-134">Példa</span><span class="sxs-lookup"><span data-stu-id="7f2f0-134">Example</span></span>

<span data-ttu-id="7f2f0-135">Ez a példa futtatja a .msi telepítő, amely a megadott elérési úton található, és nem a megadott termékkulcs azonosítója.</span><span class="sxs-lookup"><span data-stu-id="7f2f0-135">This example runs the .msi installer that is located at the specified path and has the specified product ID.</span></span>

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