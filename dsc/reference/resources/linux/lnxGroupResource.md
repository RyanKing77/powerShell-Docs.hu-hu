---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxGroup erőforrás
ms.openlocfilehash: c61b6ab4a8c56d085b5297dcfc7582187d54f946
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688342"
---
# <a name="dsc-for-linux-nxgroup-resource"></a><span data-ttu-id="3e345-103">DSC, a Linux nxGroup erőforrás</span><span class="sxs-lookup"><span data-stu-id="3e345-103">DSC for Linux nxGroup Resource</span></span>

<span data-ttu-id="3e345-104">A **nxGroup** erőforrás a PowerShell Desired State Configuration (DSC) Linux csomópont helyi csoportok kezeléséhez mechanizmust biztosít.</span><span class="sxs-lookup"><span data-stu-id="3e345-104">The **nxGroup** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="3e345-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="3e345-105">Syntax</span></span>

```
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Ensure = <string> { Absent | Present } ]
    [ Members = <string[]> ]
    [ MembersToInclude = <string[]> ]
    [ MembersToExclude = <string[]> ]
    [ DependsOn = <string[]> ]
}
```

## <a name="properties"></a><span data-ttu-id="3e345-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="3e345-106">Properties</span></span>

|  <span data-ttu-id="3e345-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="3e345-107">Property</span></span> |  <span data-ttu-id="3e345-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="3e345-108">Description</span></span> |
|---|---|
| <span data-ttu-id="3e345-109">Csoportnév</span><span class="sxs-lookup"><span data-stu-id="3e345-109">GroupName</span></span>| <span data-ttu-id="3e345-110">Megadja a csoport, amelyhez szeretne biztosítani egy adott állapot nevét.</span><span class="sxs-lookup"><span data-stu-id="3e345-110">Specifies the name of the group for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="3e345-111">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="3e345-111">Ensure</span></span>| <span data-ttu-id="3e345-112">Ellenőrizze, hogy létezik-e a csoport határozza meg.</span><span class="sxs-lookup"><span data-stu-id="3e345-112">Determines whether to check if the group exists.</span></span> <span data-ttu-id="3e345-113">Ezzel a tulajdonsággal, "E" annak érdekében, hogy a csoport létezik.</span><span class="sxs-lookup"><span data-stu-id="3e345-113">Set this property to "Present" to ensure the group exists.</span></span> <span data-ttu-id="3e345-114">Állítsa a "Hiányzó" annak érdekében, hogy a csoport nem létezik.</span><span class="sxs-lookup"><span data-stu-id="3e345-114">Set it to "Absent" to ensure the group does not exist.</span></span> <span data-ttu-id="3e345-115">Az alapértelmezett érték: "E".</span><span class="sxs-lookup"><span data-stu-id="3e345-115">The default value is "Present".</span></span>|
| <span data-ttu-id="3e345-116">Tagok</span><span class="sxs-lookup"><span data-stu-id="3e345-116">Members</span></span>| <span data-ttu-id="3e345-117">Adja meg a csoportot alkotó a tagokat.</span><span class="sxs-lookup"><span data-stu-id="3e345-117">Specifies the members that form the group.</span></span>|
| <span data-ttu-id="3e345-118">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="3e345-118">MembersToInclude</span></span>| <span data-ttu-id="3e345-119">Megadja, hogy a felhasználók, akik szeretne biztosítani a csoport tagjai.</span><span class="sxs-lookup"><span data-stu-id="3e345-119">Specifies the users who you want to ensure are members of the group.</span></span>|
| <span data-ttu-id="3e345-120">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="3e345-120">MembersToExclude</span></span>| <span data-ttu-id="3e345-121">Megadja, hogy a felhasználók, akik azt szeretné, amelyek nem a csoport tagjai.</span><span class="sxs-lookup"><span data-stu-id="3e345-121">Specifies the users who you want to ensure are not members of the group.</span></span>|
| <span data-ttu-id="3e345-122">PreferredGroupID</span><span class="sxs-lookup"><span data-stu-id="3e345-122">PreferredGroupID</span></span>| <span data-ttu-id="3e345-123">Lehetséges, ha beállítja a csoport azonosítója a megadott érték.</span><span class="sxs-lookup"><span data-stu-id="3e345-123">Sets the group id to the provided value if possible.</span></span> <span data-ttu-id="3e345-124">Ha a csoportazonosító jelenleg használatban van, használja a következő rendelkezésre álló csoport azonosítója.</span><span class="sxs-lookup"><span data-stu-id="3e345-124">If the group id is currently in use, the next available group id is used.</span></span>|
| <span data-ttu-id="3e345-125">DependsOn</span><span class="sxs-lookup"><span data-stu-id="3e345-125">DependsOn</span></span> | <span data-ttu-id="3e345-126">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="3e345-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="3e345-127">Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = '[ResourceType]ResourceName'`.</span><span class="sxs-lookup"><span data-stu-id="3e345-127">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = '[ResourceType]ResourceName'`.</span></span>|

## <a name="example"></a><span data-ttu-id="3e345-128">Példa</span><span class="sxs-lookup"><span data-stu-id="3e345-128">Example</span></span>

<span data-ttu-id="3e345-129">Az alábbi példa biztosítja, hogy a felhasználó monuser létezik, és a "DBusers" csoport tagja.</span><span class="sxs-lookup"><span data-stu-id="3e345-129">The following example ensures that the user 'monuser' exists and is a member of the group 'DBusers'.</span></span>

```powershell
Import-DSCResource -Module nx

Node $node {
    nxUser UserExample {
       UserName = 'monuser'
       Description = 'Monitoring user'
       Password = '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
       Ensure = 'Present'
       HomeDirectory = '/home/monuser'
    }

    nxGroup GroupExample {
       GroupName = 'DBusers'
       Ensure = 'Present'
       MembersToInclude = 'monuser'
       DependsOn = '[nxUser]UserExample'
    }
}
```