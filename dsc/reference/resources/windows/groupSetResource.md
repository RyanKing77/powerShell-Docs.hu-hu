---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
description: Lehetővé teszi a célcsomóponton helyi csoportok kezelése.
title: DSC GroupSet erőforrás
ms.openlocfilehash: afe4c4d33ac5620c411481e93d76a1f90c26deb9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684926"
---
# <a name="dsc-groupset-resource"></a><span data-ttu-id="d0472-104">DSC GroupSet erőforrás</span><span class="sxs-lookup"><span data-stu-id="d0472-104">DSC GroupSet Resource</span></span>

> <span data-ttu-id="d0472-105">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d0472-105">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="d0472-106">A **GroupSet** erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton helyi csoportok kezelése.</span><span class="sxs-lookup"><span data-stu-id="d0472-106">The **GroupSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on the target node.</span></span> <span data-ttu-id="d0472-107">Ez az erőforrás egy [összetett erőforrás](../../../resources/authoringResourceComposite.md) , amely meghívja a [erőforrás csoport](groupResource.md) minden egyes megadott csoport számára a `GroupName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="d0472-107">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [Group resource](groupResource.md) for each group specified in the `GroupName` parameter.</span></span>

<span data-ttu-id="d0472-108">Akkor használja ezt az erőforrást, ha hozzáadása és/vagy távolítsa el a több csoport tagjai ugyanazt a listát, egynél több csoport eltávolítása, vagy adja hozzá ugyanazt a listát egynél több csoport tagjai.</span><span class="sxs-lookup"><span data-stu-id="d0472-108">Use this resource when you want to add and/or remove the same list of members to more than one group, remove more than one group, or add more than one group with the same list of members.</span></span>

## <a name="syntax"></a><span data-ttu-id="d0472-109">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d0472-109">Syntax</span></span>

```
Group [string] #ResourceName
{
    GroupName = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ MembersToInclude = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="d0472-110">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="d0472-110">Properties</span></span>

|  <span data-ttu-id="d0472-111">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="d0472-111">Property</span></span>  |  <span data-ttu-id="d0472-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="d0472-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="d0472-113">Csoportnév</span><span class="sxs-lookup"><span data-stu-id="d0472-113">GroupName</span></span>| <span data-ttu-id="d0472-114">A csoportok, amelyhez szeretne biztosítani adott állapotú nevei.</span><span class="sxs-lookup"><span data-stu-id="d0472-114">The names of the groups for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="d0472-115">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="d0472-115">MembersToExclude</span></span>| <span data-ttu-id="d0472-116">Ez a tulajdonság használatával a meglévő tagság a csoportok tagjainak eltávolítását.</span><span class="sxs-lookup"><span data-stu-id="d0472-116">Use this property to remove members from the existing membership of the groups.</span></span> <span data-ttu-id="d0472-117">Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="d0472-117">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="d0472-118">Ha ezzel a tulajdonsággal konfigurációban, ne használja a **tagok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="d0472-118">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="d0472-119">Így generál hibát.</span><span class="sxs-lookup"><span data-stu-id="d0472-119">Doing so will generate an error.</span></span>|
| <span data-ttu-id="d0472-120">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="d0472-120">Credential</span></span>| <span data-ttu-id="d0472-121">A távoli erőforrások eléréséhez szükséges hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="d0472-121">The credentials required to access remote resources.</span></span> <span data-ttu-id="d0472-122">**Megjegyzés:**: Ennek a fióknak rendelkeznie kell a megfelelő Active Directory-engedélyek minden nem helyi fiók hozzáadása a csoporthoz; Ellenkező esetben a rendszer hibát fog jelezni.</span><span class="sxs-lookup"><span data-stu-id="d0472-122">**Note**: This account must have the appropriate Active Directory permissions to add all non-local accounts to the group; otherwise, an error will occur.</span></span>
| <span data-ttu-id="d0472-123">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="d0472-123">Ensure</span></span>| <span data-ttu-id="d0472-124">Azt jelzi, hogy a csoport létezik.</span><span class="sxs-lookup"><span data-stu-id="d0472-124">Indicates whether the groups exist.</span></span> <span data-ttu-id="d0472-125">Állítsa be ezt a tulajdonságot a "Hiányzó", győződjön meg arról, hogy a csoportok nem létezik.</span><span class="sxs-lookup"><span data-stu-id="d0472-125">Set this property to "Absent" to ensure that the groups do not exist.</span></span> <span data-ttu-id="d0472-126">Azt, hogy "" (az alapértelmezett érték) beállítás biztosítja, hogy létezik-e a csoportok.</span><span class="sxs-lookup"><span data-stu-id="d0472-126">Setting it to "Present" (the default value) ensures that the groups exist.</span></span>|
| <span data-ttu-id="d0472-127">Tagok</span><span class="sxs-lookup"><span data-stu-id="d0472-127">Members</span></span>| <span data-ttu-id="d0472-128">Ez a tulajdonság használatával az aktuális csoport tagságának cserélje le a meghatározott tagokat.</span><span class="sxs-lookup"><span data-stu-id="d0472-128">Use this property to replace the current group membership with the specified members.</span></span> <span data-ttu-id="d0472-129">Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="d0472-129">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="d0472-130">Ezzel a tulajdonsággal konfigurációban, ha nem használja a **MembersToExclude** vagy **MembersToInclude** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="d0472-130">If you set this property in a configuration, do not use either the **MembersToExclude** or **MembersToInclude** property.</span></span> <span data-ttu-id="d0472-131">Így generál hibát.</span><span class="sxs-lookup"><span data-stu-id="d0472-131">Doing so will generate an error.</span></span>|
| <span data-ttu-id="d0472-132">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="d0472-132">MembersToInclude</span></span>| <span data-ttu-id="d0472-133">Ez a tulajdonság használatával tagok hozzáadása a meglévő tagság a csoport.</span><span class="sxs-lookup"><span data-stu-id="d0472-133">Use this property to add members to the existing membership of the group.</span></span> <span data-ttu-id="d0472-134">Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="d0472-134">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="d0472-135">Ha ezzel a tulajdonsággal konfigurációban, ne használja a **tagok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="d0472-135">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="d0472-136">Így generál hibát.</span><span class="sxs-lookup"><span data-stu-id="d0472-136">Doing so will generate an error.</span></span>|
| <span data-ttu-id="d0472-137">DependsOn</span><span class="sxs-lookup"><span data-stu-id="d0472-137">DependsOn</span></span> | <span data-ttu-id="d0472-138">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="d0472-138">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="d0472-139">Például, ha az erőforrás-konfiguráció azonosítója parancsfájl-blokk futtatni kívánt első az __ResourceName__ és a típusa __ResourceType__, esetén ez a tulajdonság használatával "DependsOn"[a = Erőforrástípus] ResourceName"s".</span><span class="sxs-lookup"><span data-stu-id="d0472-139">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|

## <a name="example-1-ensuring-groups-are-present"></a><span data-ttu-id="d0472-140">1. példa: Biztosítása csoportok találhatók.</span><span class="sxs-lookup"><span data-stu-id="d0472-140">Example 1: Ensuring Groups are present</span></span>

<span data-ttu-id="d0472-141">Az alábbi példa bemutatja, hogyan győződjön meg arról, hogy telepítve-e két "myGroup" és "myOtherGroup" csoportot.</span><span class="sxs-lookup"><span data-stu-id="d0472-141">The following example shows how to ensure that two groups called "myGroup" and "myOtherGroup" are present.</span></span>

```powershell
configuration GroupSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {
        GroupSet GroupSetTest
        {
            GroupName        = @("myGroup", "myOtherGroup")
            Ensure           = "Present"
            MembersToInclude = @("contoso\alice", "contoso\bob")
            MembersToExclude = $("contoso\john")
            Credential       = Get-Credential
        }
    }
}
$cd = @{
    AllNodes = @(
        @{
            NodeName                    = 'localhost'
            PSDscAllowPlainTextPassword = $true
            PSDscAllowDomainUser        = $true
        }
    )
}

GroupSetTest -ConfigurationData $cd
```

> [!NOTE]
> <span data-ttu-id="d0472-142">Ebben a példában az egyszerűség kedvéért egy egyszerű szöveges hitelesítő adatokat használ.</span><span class="sxs-lookup"><span data-stu-id="d0472-142">This example uses plaintext credentials for simplicity.</span></span> <span data-ttu-id="d0472-143">A konfigurációs MOF-fájlban található hitelesítő adatainak titkosítása kapcsolatos információkért lásd: [a MOF-fájl biztonságossá tétele](../../../pull-server/secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="d0472-143">For information about how to encrypt credentials in the configuration MOF file, see [Securing the MOF File](../../../pull-server/secureMOF.md).</span></span>
