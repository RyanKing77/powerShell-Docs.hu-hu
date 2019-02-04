---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxPackage erőforrás
ms.openlocfilehash: 64bb89a95bd6cbaea4e74b8a9979de52428fef3f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685682"
---
# <a name="dsc-for-linux-nxpackage-resource"></a><span data-ttu-id="d709f-103">DSC, a Linux nxPackage erőforrás</span><span class="sxs-lookup"><span data-stu-id="d709f-103">DSC for Linux nxPackage Resource</span></span>

<span data-ttu-id="d709f-104">A **nxPackage** erőforrás a PowerShell Desired State Configuration (DSC) Linux csomóponton csomagok kezeléséhez mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="d709f-104">The **nxPackage** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage packages on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="d709f-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d709f-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="d709f-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="d709f-106">Properties</span></span>

|  <span data-ttu-id="d709f-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d709f-107">Property</span></span> |  <span data-ttu-id="d709f-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="d709f-108">Description</span></span> |
|---|---|
| <span data-ttu-id="d709f-109">Név</span><span class="sxs-lookup"><span data-stu-id="d709f-109">Name</span></span>| <span data-ttu-id="d709f-110">A csomag, amelyhez szeretne biztosítani egy adott állapot neve.</span><span class="sxs-lookup"><span data-stu-id="d709f-110">The name of the package for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="d709f-111">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="d709f-111">Ensure</span></span>| <span data-ttu-id="d709f-112">Ellenőrizze, hogy létezik-e a csomag határozza meg.</span><span class="sxs-lookup"><span data-stu-id="d709f-112">Determines whether to check if the package exists.</span></span> <span data-ttu-id="d709f-113">Ezzel a tulajdonsággal, "E" annak érdekében, hogy a csomag létezik.</span><span class="sxs-lookup"><span data-stu-id="d709f-113">Set this property to "Present" to ensure the package exists.</span></span> <span data-ttu-id="d709f-114">Állítsa a "Hiányzó" annak érdekében, hogy a csomag nem létezik.</span><span class="sxs-lookup"><span data-stu-id="d709f-114">Set it to "Absent" to ensure the package does not exist.</span></span> <span data-ttu-id="d709f-115">Az alapértelmezett érték: "E".</span><span class="sxs-lookup"><span data-stu-id="d709f-115">The default value is "Present".</span></span>|
| <span data-ttu-id="d709f-116">PackageManager</span><span class="sxs-lookup"><span data-stu-id="d709f-116">PackageManager</span></span>| <span data-ttu-id="d709f-117">Támogatott értékei a következők: "yum", "apt" és "zypper".</span><span class="sxs-lookup"><span data-stu-id="d709f-117">Supported values are "yum", "apt", and "zypper".</span></span> <span data-ttu-id="d709f-118">Adja meg a csomagok telepítéséhez használni kívánt Csomagkezelő.</span><span class="sxs-lookup"><span data-stu-id="d709f-118">Specifies the package manager to use when installing packages.</span></span> <span data-ttu-id="d709f-119">Ha **FilePath** van megadva, a megadott elérési út lesz a csomag telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="d709f-119">If **FilePath** is specified, the provided path will be used to install the package.</span></span> <span data-ttu-id="d709f-120">Ellenkező esetben Csomagkezelő használható egy előre konfigurált adattárból a csomag telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="d709f-120">Otherwise, a Package Manager will be used to install the package from a pre-configured repository.</span></span> <span data-ttu-id="d709f-121">Ha sem **PackageManager** sem **FilePath** érhetők el, az alapértelmezett Csomagkezelő esetében a rendszer használható.</span><span class="sxs-lookup"><span data-stu-id="d709f-121">If neither **PackageManager** nor **FilePath** are provided, the default package manager for the system will be used.</span></span>|
| <span data-ttu-id="d709f-122">FilePath</span><span class="sxs-lookup"><span data-stu-id="d709f-122">FilePath</span></span>| <span data-ttu-id="d709f-123">A fájl elérési útja, ahol a csomag található</span><span class="sxs-lookup"><span data-stu-id="d709f-123">The file path where the package resides</span></span>|
| <span data-ttu-id="d709f-124">PackageGroup</span><span class="sxs-lookup"><span data-stu-id="d709f-124">PackageGroup</span></span>| <span data-ttu-id="d709f-125">Ha **$true**, a **neve** kell lennie egy csomag csoport nevére, a segítségével egy **PackageManager**.</span><span class="sxs-lookup"><span data-stu-id="d709f-125">If **$true**, the **Name** is expected to be the name of a package group for use with a **PackageManager**.</span></span> <span data-ttu-id="d709f-126">**PacakgeGroup** esetén nem érvényes biztosít egy **FilePath**.</span><span class="sxs-lookup"><span data-stu-id="d709f-126">**PacakgeGroup** is not valid when providing a **FilePath**.</span></span>|
| <span data-ttu-id="d709f-127">Argumentumok</span><span class="sxs-lookup"><span data-stu-id="d709f-127">Arguments</span></span>| <span data-ttu-id="d709f-128">Egy karakterlánc, amely a rendszer átad a csomag pontosan a megadott argumentumok.</span><span class="sxs-lookup"><span data-stu-id="d709f-128">A string of arguments that will be passed to the package exactly as provided.</span></span>|
| <span data-ttu-id="d709f-129">ReturnCode</span><span class="sxs-lookup"><span data-stu-id="d709f-129">ReturnCode</span></span>| <span data-ttu-id="d709f-130">A várt visszatérési kód.</span><span class="sxs-lookup"><span data-stu-id="d709f-130">The expected return code.</span></span> <span data-ttu-id="d709f-131">Ha a tényleges visszatérési kód nem egyezik a várt értéknek. Itt, elérhető, a konfigurációs hibát adnak vissza.</span><span class="sxs-lookup"><span data-stu-id="d709f-131">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>|
| <span data-ttu-id="d709f-132">DependsOn</span><span class="sxs-lookup"><span data-stu-id="d709f-132">DependsOn</span></span> | <span data-ttu-id="d709f-133">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="d709f-133">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d709f-134">Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="d709f-134">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="d709f-135">Példa</span><span class="sxs-lookup"><span data-stu-id="d709f-135">Example</span></span>

<span data-ttu-id="d709f-136">Az alábbi példa biztosítja, hogy a "httpd" nevű csomag telepítve van-e egy Linux rendszerű számítógépre, a "Yum" package manager használatával.</span><span class="sxs-lookup"><span data-stu-id="d709f-136">The following example ensures that the package named "httpd" is installed on a Linux computer, using the “Yum” package manager.</span></span>

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