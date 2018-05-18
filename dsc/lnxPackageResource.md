---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Linux nxPackage erőforrás DSC
ms.openlocfilehash: 64bb89a95bd6cbaea4e74b8a9979de52428fef3f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-for-linux-nxpackage-resource"></a><span data-ttu-id="f9efa-103">A Linux nxPackage erőforrás DSC</span><span class="sxs-lookup"><span data-stu-id="f9efa-103">DSC for Linux nxPackage Resource</span></span>

<span data-ttu-id="f9efa-104">A **nxPackage** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) lehetővé teszi a csomagok egy Linux-csomóponton felügyeletéhez.</span><span class="sxs-lookup"><span data-stu-id="f9efa-104">The **nxPackage** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage packages on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="f9efa-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="f9efa-105">Syntax</span></span>

```
nxPackage <string> #ResourceName
{
    Name = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ PackageManager = <string> { Yum | Apt | Zypper } ]
    [ PackageGroup = <bool>]
    [ Arguments = <string> ]
    [ ReturnCode = <uint32> ]
    [ LogPath = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="f9efa-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="f9efa-106">Properties</span></span>

|  <span data-ttu-id="f9efa-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="f9efa-107">Property</span></span> |  <span data-ttu-id="f9efa-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="f9efa-108">Description</span></span> |
|---|---|
| <span data-ttu-id="f9efa-109">Név</span><span class="sxs-lookup"><span data-stu-id="f9efa-109">Name</span></span>| <span data-ttu-id="f9efa-110">A csomag, amelyekhez egy adott állapot biztosításához neve.</span><span class="sxs-lookup"><span data-stu-id="f9efa-110">The name of the package for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="f9efa-111">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="f9efa-111">Ensure</span></span>| <span data-ttu-id="f9efa-112">Meghatározza, hogy ellenőrizze, hogy a csomag létezik-e.</span><span class="sxs-lookup"><span data-stu-id="f9efa-112">Determines whether to check if the package exists.</span></span> <span data-ttu-id="f9efa-113">Állítsa be ezt a tulajdonságot "Elérhető" annak érdekében, hogy a csomag létezik-e.</span><span class="sxs-lookup"><span data-stu-id="f9efa-113">Set this property to "Present" to ensure the package exists.</span></span> <span data-ttu-id="f9efa-114">Állítsa az értékét "Hiányzik", annak érdekében, hogy a csomag nem létezik.</span><span class="sxs-lookup"><span data-stu-id="f9efa-114">Set it to "Absent" to ensure the package does not exist.</span></span> <span data-ttu-id="f9efa-115">Az alapértelmezett érték: "Elérhető".</span><span class="sxs-lookup"><span data-stu-id="f9efa-115">The default value is "Present".</span></span>|
| <span data-ttu-id="f9efa-116">PackageManager</span><span class="sxs-lookup"><span data-stu-id="f9efa-116">PackageManager</span></span>| <span data-ttu-id="f9efa-117">Támogatott értékei a "yum", "apt" és "zypper".</span><span class="sxs-lookup"><span data-stu-id="f9efa-117">Supported values are "yum", "apt", and "zypper".</span></span> <span data-ttu-id="f9efa-118">Adja meg a package manager csomagok telepítése során használja.</span><span class="sxs-lookup"><span data-stu-id="f9efa-118">Specifies the package manager to use when installing packages.</span></span> <span data-ttu-id="f9efa-119">Ha **FilePath** van megadva, a megadott elérési út fogja használni a csomag telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="f9efa-119">If **FilePath** is specified, the provided path will be used to install the package.</span></span> <span data-ttu-id="f9efa-120">Ellenkező esetben a Csomagkezelő használható előre konfigurált tárházból a csomag telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="f9efa-120">Otherwise, a Package Manager will be used to install the package from a pre-configured repository.</span></span> <span data-ttu-id="f9efa-121">Ha sem **PackageManager** sem **FilePath** biztosított, az alapértelmezett Csomagkezelőt a rendszer lesz használható.</span><span class="sxs-lookup"><span data-stu-id="f9efa-121">If neither **PackageManager** nor **FilePath** are provided, the default package manager for the system will be used.</span></span>|
| <span data-ttu-id="f9efa-122">fájl elérési útja</span><span class="sxs-lookup"><span data-stu-id="f9efa-122">FilePath</span></span>| <span data-ttu-id="f9efa-123">A fájl elérési útját, ahol a csomag található</span><span class="sxs-lookup"><span data-stu-id="f9efa-123">The file path where the package resides</span></span>|
| <span data-ttu-id="f9efa-124">PackageGroup</span><span class="sxs-lookup"><span data-stu-id="f9efa-124">PackageGroup</span></span>| <span data-ttu-id="f9efa-125">Ha **$true**, a **neve** kellene lennie a használathoz egy csomag csoport nevét a **PackageManager**.</span><span class="sxs-lookup"><span data-stu-id="f9efa-125">If **$true**, the **Name** is expected to be the name of a package group for use with a **PackageManager**.</span></span> <span data-ttu-id="f9efa-126">**PacakgeGroup** érvénytelen nyújtásakor a **FilePath**.</span><span class="sxs-lookup"><span data-stu-id="f9efa-126">**PacakgeGroup** is not valid when providing a **FilePath**.</span></span>|
| <span data-ttu-id="f9efa-127">Argumentumok</span><span class="sxs-lookup"><span data-stu-id="f9efa-127">Arguments</span></span>| <span data-ttu-id="f9efa-128">Az átadott csomag pontosan megegyezik a megadott argumentumok karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="f9efa-128">A string of arguments that will be passed to the package exactly as provided.</span></span>|
| <span data-ttu-id="f9efa-129">Visszatérési kód:</span><span class="sxs-lookup"><span data-stu-id="f9efa-129">ReturnCode</span></span>| <span data-ttu-id="f9efa-130">A várt visszatérési kód.</span><span class="sxs-lookup"><span data-stu-id="f9efa-130">The expected return code.</span></span> <span data-ttu-id="f9efa-131">Ha a tényleges visszatérési kód nem egyezik a várt érték megadva itt, a konfigurációs hibát adnak vissza.</span><span class="sxs-lookup"><span data-stu-id="f9efa-131">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>|
| <span data-ttu-id="f9efa-132">dependsOn</span><span class="sxs-lookup"><span data-stu-id="f9efa-132">DependsOn</span></span> | <span data-ttu-id="f9efa-133">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="f9efa-133">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="f9efa-134">Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="f9efa-134">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="f9efa-135">Példa</span><span class="sxs-lookup"><span data-stu-id="f9efa-135">Example</span></span>

<span data-ttu-id="f9efa-136">Az alábbi példa biztosítja, hogy a "httpd" nevű csomaghoz: telepítve van egy Linux-számítógép, a "Yum" package manager használatával.</span><span class="sxs-lookup"><span data-stu-id="f9efa-136">The following example ensures that the package named "httpd" is installed on a Linux computer, using the “Yum” package manager.</span></span>

```
Import-DSCResource -Module nx

Node $node {
nxPackage httpd
{
    Name = "httpd"
    Ensure = "Present"
    PackageManager = "Yum"
}
}
```