---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxFileLine erőforrás
ms.openlocfilehash: 6a91db25638b09659adfabcec78f91bcb2e69dd9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684968"
---
# <a name="dsc-for-linux-nxfileline-resource"></a><span data-ttu-id="5f28f-103">DSC, a Linux nxFileLine erőforrás</span><span class="sxs-lookup"><span data-stu-id="5f28f-103">DSC for Linux nxFileLine Resource</span></span>

<span data-ttu-id="5f28f-104">A **nxFileLine** erőforrás a PowerShell Desired State Configuration (DSC) kezelése konfigurációs fájl egy Linux-csomóponton belül sorok mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="5f28f-104">The **nxFileLine** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage lines within a configuration file on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="5f28f-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5f28f-105">Syntax</span></span>

```
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="5f28f-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="5f28f-106">Properties</span></span>

|  <span data-ttu-id="5f28f-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="5f28f-107">Property</span></span> |  <span data-ttu-id="5f28f-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="5f28f-108">Description</span></span> |
|---|---|
| <span data-ttu-id="5f28f-109">FilePath</span><span class="sxs-lookup"><span data-stu-id="5f28f-109">FilePath</span></span>| <span data-ttu-id="5f28f-110">A fájl teljes elérési útja a célcsomóponton lévő sorok kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="5f28f-110">The full path to the file to manage lines in on the target node.</span></span>|
| <span data-ttu-id="5f28f-111">ContainsLine</span><span class="sxs-lookup"><span data-stu-id="5f28f-111">ContainsLine</span></span>| <span data-ttu-id="5f28f-112">Győződjön meg arról, hogy egy sort a fájl létezik.</span><span class="sxs-lookup"><span data-stu-id="5f28f-112">A line to ensure exists in the file.</span></span> <span data-ttu-id="5f28f-113">Ezt a sort a fájl is bővül, ha nem létezik a fájlban.</span><span class="sxs-lookup"><span data-stu-id="5f28f-113">This line will be appended to the file if it does not exist in the file.</span></span> <span data-ttu-id="5f28f-114">**ContainsLine** kötelező, de egy üres karakterláncra állítható (`ContainsLine = ""`) Ha már nincs szükség.</span><span class="sxs-lookup"><span data-stu-id="5f28f-114">**ContainsLine** is mandatory, but can be set to an empty string (`ContainsLine = ""`) if it is not needed.</span></span>|
| <span data-ttu-id="5f28f-115">DoesNotContainPattern</span><span class="sxs-lookup"><span data-stu-id="5f28f-115">DoesNotContainPattern</span></span>| <span data-ttu-id="5f28f-116">A sorokat, amelyek a fájl nem létezhet Reguláriskifejezés-mintának.</span><span class="sxs-lookup"><span data-stu-id="5f28f-116">A regular expression pattern for lines that should not exist in the file.</span></span> <span data-ttu-id="5f28f-117">Olyan sort, amely létezik a fájlban a reguláris kifejezésnek megfelelő a sort a fájl törlődik.</span><span class="sxs-lookup"><span data-stu-id="5f28f-117">For any lines that exist in the file that match this regular expression, the line will be removed from the file.</span></span>|
| <span data-ttu-id="5f28f-118">DependsOn</span><span class="sxs-lookup"><span data-stu-id="5f28f-118">DependsOn</span></span> | <span data-ttu-id="5f28f-119">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="5f28f-119">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="5f28f-120">Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="5f28f-120">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="5f28f-121">Példa</span><span class="sxs-lookup"><span data-stu-id="5f28f-121">Example</span></span>

<span data-ttu-id="5f28f-122">Ebben a példában használatát mutatja be a **nxFileLine** erőforrás konfigurálása az `/etc/sudoers` fájl, biztosítva, hogy a felhasználó: monuser nem requiretty van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="5f28f-122">This example demonstrates using the **nxFileLine** resource to configure the `/etc/sudoers` file, ensuring that the user: monuser is configured to not requiretty.</span></span>

```powershell
Import-DscResource -Module nx

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
}
```