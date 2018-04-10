---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Linux nxGroup erőforrás DSC
ms.openlocfilehash: 750b7c38a38fb8a7781585a3a7776f832ee62495
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-for-linux-nxgroup-resource"></a><span data-ttu-id="7bb6a-103">A Linux nxGroup erőforrás DSC</span><span class="sxs-lookup"><span data-stu-id="7bb6a-103">DSC for Linux nxGroup Resource</span></span>

<span data-ttu-id="7bb6a-104">A **nxGroup** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) lehetővé teszi egy Linux-csomóponton helyi csoportok kezelése.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-104">The **nxGroup** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="7bb6a-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7bb6a-105">Syntax</span></span>

```powershell
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Members = <string[]> ]
    [ MebersToInclude = <string[]>]
    [ MembersToExclude = <string[]> ]
    [ DependsOn = <string[]> ]
}

```

## <a name="properties"></a><span data-ttu-id="7bb6a-106">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="7bb6a-106">Properties</span></span>

|  <span data-ttu-id="7bb6a-107">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="7bb6a-107">Property</span></span> |  <span data-ttu-id="7bb6a-108">Leírás</span><span class="sxs-lookup"><span data-stu-id="7bb6a-108">Description</span></span> |
|---|---|
| <span data-ttu-id="7bb6a-109">Csoportnév</span><span class="sxs-lookup"><span data-stu-id="7bb6a-109">GroupName</span></span>| <span data-ttu-id="7bb6a-110">Adja meg a legyen egy adott állapot biztosításához a csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-110">Specifies the name of the group for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="7bb6a-111">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="7bb6a-111">Ensure</span></span>| <span data-ttu-id="7bb6a-112">Meghatározza, hogy ellenőrizze, hogy a csoport létezik-e.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-112">Determines whether to check if the group exists.</span></span> <span data-ttu-id="7bb6a-113">Állítsa be ezt a tulajdonságot "Elérhető" annak érdekében, hogy a csoport létezik.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-113">Set this property to "Present" to ensure the group exists.</span></span> <span data-ttu-id="7bb6a-114">Állítsa az értékét "Hiányzik", annak érdekében, hogy a csoport nem létezik.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-114">Set it to "Absent" to ensure the group does not exist.</span></span> <span data-ttu-id="7bb6a-115">Az alapértelmezett érték: "Elérhető".</span><span class="sxs-lookup"><span data-stu-id="7bb6a-115">The default value is "Present".</span></span>|
| <span data-ttu-id="7bb6a-116">Tagok</span><span class="sxs-lookup"><span data-stu-id="7bb6a-116">Members</span></span>| <span data-ttu-id="7bb6a-117">Adja meg a csoportot alkotó tagok.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-117">Specifies the members that form the group.</span></span>|
| <span data-ttu-id="7bb6a-118">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="7bb6a-118">MembersToInclude</span></span>| <span data-ttu-id="7bb6a-119">Adja meg a felhasználókat, akik számára biztosítani szeretné a csoport tagjai.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-119">Specifies the users who you want to ensure are members of the group.</span></span>|
| <span data-ttu-id="7bb6a-120">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="7bb6a-120">MembersToExclude</span></span>| <span data-ttu-id="7bb6a-121">Meghatározza, hogy a felhasználók számára szeretné biztosítani nem a csoport tagjai.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-121">Specifies the users who you want to ensure are not members of the group.</span></span>|
| <span data-ttu-id="7bb6a-122">PreferredGroupID</span><span class="sxs-lookup"><span data-stu-id="7bb6a-122">PreferredGroupID</span></span>| <span data-ttu-id="7bb6a-123">Ha lehetséges beállítja a csoport azonosítója a megadott értékre.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-123">Sets the group id to the provided value if possible.</span></span> <span data-ttu-id="7bb6a-124">Ha a csoport azonosító jelenleg használatban van, a következő rendelkezésre álló csoport azonosítót használja.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-124">If the group id is currently in use, the next available group id is used.</span></span>|
| <span data-ttu-id="7bb6a-125">dependsOn</span><span class="sxs-lookup"><span data-stu-id="7bb6a-125">DependsOn</span></span> | <span data-ttu-id="7bb6a-126">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="7bb6a-127">Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-127">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="7bb6a-128">Példa</span><span class="sxs-lookup"><span data-stu-id="7bb6a-128">Example</span></span>

<span data-ttu-id="7bb6a-129">Az alábbi példa biztosítja, hogy a felhasználó "monuser" létezik, és a "DBusers" csoport tagja.</span><span class="sxs-lookup"><span data-stu-id="7bb6a-129">The following example ensures that the user “monuser” exists and is a member of the group "DBusers".</span></span>

```
Import-DSCResource -Module nx

Node $node {

nxUser UserExample{
   UserName = "monuser"
   Description = "Monitoring user"
   Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
   Ensure = "Present"
   HomeDirectory = "/home/monuser"
}

nxGroup GroupExample{
   GroupName = "DBusers"
   Ensure = "Present"
   MembersToInclude = "monuser"
   DependsOn = "[nxUser]UserExample"
}
}
```