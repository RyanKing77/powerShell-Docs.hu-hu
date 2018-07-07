---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxFileLine erőforrás
ms.openlocfilehash: f2a989dd3a6746948e09ba94e279c02be8ebe2de
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893297"
---
# <a name="dsc-for-linux-nxfileline-resource"></a><span data-ttu-id="6d8c6-103">DSC, a Linux nxFileLine erőforrás</span><span class="sxs-lookup"><span data-stu-id="6d8c6-103">DSC for Linux nxFileLine Resource</span></span>

<span data-ttu-id="6d8c6-104">A **nxFileLine** erőforrás a PowerShell Desired State Configuration (DSC) használatával kezelheti egy konfigurációs fájl egy Linux-csomóponton belül sorok mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-104">The **nxFileLine** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to to manage lines within a configuration file on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="6d8c6-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6d8c6-105">Syntax</span></span>

```
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="6d8c6-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="6d8c6-106">Properties</span></span>

|  <span data-ttu-id="6d8c6-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="6d8c6-107">Property</span></span> |  <span data-ttu-id="6d8c6-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="6d8c6-108">Description</span></span> |
|---|---|
| <span data-ttu-id="6d8c6-109">Fájl elérési útja</span><span class="sxs-lookup"><span data-stu-id="6d8c6-109">FilePath</span></span>| <span data-ttu-id="6d8c6-110">A fájl teljes elérési útja a célcsomóponton lévő sorok kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-110">The full path to the file to manage lines in on the target node.</span></span>|
| <span data-ttu-id="6d8c6-111">ContainsLine</span><span class="sxs-lookup"><span data-stu-id="6d8c6-111">ContainsLine</span></span>| <span data-ttu-id="6d8c6-112">Győződjön meg arról, hogy egy sort a fájl létezik.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-112">A line to ensure exists in the file.</span></span> <span data-ttu-id="6d8c6-113">Ezt a sort a fájl is bővül, ha nem létezik a fájlban.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-113">This line will be appended to the file if it does not exist in the file.</span></span> <span data-ttu-id="6d8c6-114">**ContainsLine** kötelező, de egy üres karakterláncra állítható (`ContainsLine = ""`) Ha már nincs szükség.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-114">**ContainsLine** is mandatory, but can be set to an empty string (`ContainsLine = ""`) if it is not needed.</span></span>|
| <span data-ttu-id="6d8c6-115">DoesNotContainPattern</span><span class="sxs-lookup"><span data-stu-id="6d8c6-115">DoesNotContainPattern</span></span>| <span data-ttu-id="6d8c6-116">A sorokat, amelyek a fájl nem létezhet Reguláriskifejezés-mintának.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-116">A regular expression pattern for lines that should not exist in the file.</span></span> <span data-ttu-id="6d8c6-117">Olyan sort, amely létezik a fájlban a reguláris kifejezésnek megfelelő a sort a fájl törlődik.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-117">For any lines that exist in the file that match this regular expression, the line will be removed from the file.</span></span>|
| <span data-ttu-id="6d8c6-118">DependsOn</span><span class="sxs-lookup"><span data-stu-id="6d8c6-118">DependsOn</span></span> | <span data-ttu-id="6d8c6-119">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-119">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="6d8c6-120">Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-120">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="6d8c6-121">Példa</span><span class="sxs-lookup"><span data-stu-id="6d8c6-121">Example</span></span>

<span data-ttu-id="6d8c6-122">Ebben a példában használatát mutatja be a **nxFileLine** erőforrás konfigurálása az `/etc/sudoers` fájl, biztosítva, hogy a felhasználó: monuser nem requiretty van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="6d8c6-122">This example demonstrates using the **nxFileLine** resource to configure the `/etc/sudoers` file, ensuring that the user: monuser is configured to not requiretty.</span></span>

```powershell
Import-DscResource -Module nx

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
}
```