---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
description: Lehetővé teszi a célcsomóponton helyi csoportok kezelése.
title: A DSC GroupSet erőforrás
ms.openlocfilehash: 4f8fc21806fdb4eb06e0d915d5b6ca229357a210
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-groupset-resource"></a><span data-ttu-id="cf153-104">A DSC GroupSet erőforrás</span><span class="sxs-lookup"><span data-stu-id="cf153-104">DSC GroupSet Resource</span></span>

> <span data-ttu-id="cf153-105">Vonatkozik: Windows Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="cf153-105">Applies To: Windows Windows PowerShell 5.0</span></span>

<span data-ttu-id="cf153-106">A **GroupSet** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton helyi csoportok kezelése.</span><span class="sxs-lookup"><span data-stu-id="cf153-106">The **GroupSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on the target node.</span></span> <span data-ttu-id="cf153-107">Az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [erőforrás csoport](groupResource.md) minden egyes megadott csoport számára a `GroupName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="cf153-107">This resource is a [composite resource](authoringResourceComposite.md) that calls the [Group resource](groupResource.md) for each group specified in the `GroupName` parameter.</span></span>

<span data-ttu-id="cf153-108">Adja hozzá és/vagy távolítsa el a egynél több csoport tagjai ugyanazt a listát, egynél több csoport eltávolítása vagy vegyen fel egy tagok ugyanazt a listát egynél több csoportot használni ehhez az erőforráshoz.</span><span class="sxs-lookup"><span data-stu-id="cf153-108">Use this resource when you want to add and/or remove the same list of members to more than one group, remove more than one group, or add more than one group with the same list of members.</span></span>

##<a name="syntax"></a><span data-ttu-id="cf153-109">Szintaxis ##</span><span class="sxs-lookup"><span data-stu-id="cf153-109">Syntax##</span></span>
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

## <a name="properties"></a><span data-ttu-id="cf153-110">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="cf153-110">Properties</span></span>

|  <span data-ttu-id="cf153-111">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="cf153-111">Property</span></span>  |  <span data-ttu-id="cf153-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="cf153-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="cf153-113">Csoportnév</span><span class="sxs-lookup"><span data-stu-id="cf153-113">GroupName</span></span>| <span data-ttu-id="cf153-114">A csoportokat, amelyekhez egy adott állapot biztosításához nevei.</span><span class="sxs-lookup"><span data-stu-id="cf153-114">The names of the groups for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="cf153-115">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="cf153-115">MembersToExclude</span></span>| <span data-ttu-id="cf153-116">Ez a tulajdonság segítségével távolítsa el a meglévő a csoportok tagságának tagot.</span><span class="sxs-lookup"><span data-stu-id="cf153-116">Use this property to remove members from the existing membership of the groups.</span></span> <span data-ttu-id="cf153-117">Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="cf153-117">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="cf153-118">Ha ez a tulajdonság konfigurációban, ne használja a **tagok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="cf153-118">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="cf153-119">Ennek során hibát adnak.</span><span class="sxs-lookup"><span data-stu-id="cf153-119">Doing so will generate an error.</span></span>|
| <span data-ttu-id="cf153-120">hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="cf153-120">Credential</span></span>| <span data-ttu-id="cf153-121">A távoli erőforrások eléréséhez szükséges hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="cf153-121">The credentials required to access remote resources.</span></span> <span data-ttu-id="cf153-122">**Megjegyzés:**: ennek a fióknak rendelkeznie kell a megfelelő Active Directory-engedélyek minden nem helyi fiók hozzáadása a csoporthoz; ellenkező esetben hiba történik.</span><span class="sxs-lookup"><span data-stu-id="cf153-122">**Note**: This account must have the appropriate Active Directory permissions to add all non-local accounts to the group; otherwise, an error will occur.</span></span>
| <span data-ttu-id="cf153-123">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="cf153-123">Ensure</span></span>| <span data-ttu-id="cf153-124">Azt jelzi, hogy a csoportok is léteznek.</span><span class="sxs-lookup"><span data-stu-id="cf153-124">Indicates whether the groups exist.</span></span> <span data-ttu-id="cf153-125">Állítsa be ezt a tulajdonságot "Hiányzik", annak érdekében, hogy a csoportok nem léteznek.</span><span class="sxs-lookup"><span data-stu-id="cf153-125">Set this property to "Absent" to ensure that the groups do not exist.</span></span> <span data-ttu-id="cf153-126">Azt, hogy "" (az alapértelmezett érték) beállítást biztosítja, hogy a csoportok is léteznek.</span><span class="sxs-lookup"><span data-stu-id="cf153-126">Setting it to "Present" (the default value) ensures that the groups exist.</span></span>|
| <span data-ttu-id="cf153-127">Tagok</span><span class="sxs-lookup"><span data-stu-id="cf153-127">Members</span></span>| <span data-ttu-id="cf153-128">Ez a tulajdonság használatával az aktuális csoporttagság cserélje le a megadott tagot.</span><span class="sxs-lookup"><span data-stu-id="cf153-128">Use this property to replace the current group membership with the specified members.</span></span> <span data-ttu-id="cf153-129">Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="cf153-129">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="cf153-130">Ha ez a tulajdonság konfigurációban, nem használja a **MembersToExclude** vagy **MembersToInclude** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="cf153-130">If you set this property in a configuration, do not use either the **MembersToExclude** or **MembersToInclude** property.</span></span> <span data-ttu-id="cf153-131">Ennek során hibát adnak.</span><span class="sxs-lookup"><span data-stu-id="cf153-131">Doing so will generate an error.</span></span>|
| <span data-ttu-id="cf153-132">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="cf153-132">MembersToInclude</span></span>| <span data-ttu-id="cf153-133">Ez a tulajdonság használatával tagok hozzáadása a meglévő csoport tagságát.</span><span class="sxs-lookup"><span data-stu-id="cf153-133">Use this property to add members to the existing membership of the group.</span></span> <span data-ttu-id="cf153-134">Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="cf153-134">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="cf153-135">Ha ez a tulajdonság konfigurációban, ne használja a **tagok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="cf153-135">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="cf153-136">Ennek során hibát adnak.</span><span class="sxs-lookup"><span data-stu-id="cf153-136">Doing so will generate an error.</span></span>|
| <span data-ttu-id="cf153-137">dependsOn</span><span class="sxs-lookup"><span data-stu-id="cf153-137">DependsOn</span></span> | <span data-ttu-id="cf153-138">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="cf153-138">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="cf153-139">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, szintaxisa a következő e tulajdonság használatával "DependsOn ="[ A ResourceType] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="cf153-139">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|

## <a name="example-1"></a><span data-ttu-id="cf153-140">1. példa</span><span class="sxs-lookup"><span data-stu-id="cf153-140">Example 1</span></span>

<span data-ttu-id="cf153-141">A következő példa bemutatja, hogyan annak érdekében, hogy jelen-e "myGroup" és "myOtherGroup" két csoportot.</span><span class="sxs-lookup"><span data-stu-id="cf153-141">The following example shows how to ensure that two groups called "myGroup" and "myOtherGroup" are present.</span></span>

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

><span data-ttu-id="cf153-142">**Megjegyzés:** ebben a példában egyszerű szöveges hitelesítő adatokat használja az egyszerűség érdekében.</span><span class="sxs-lookup"><span data-stu-id="cf153-142">**Note:** This example uses plaintext credentials for simplicity.</span></span> <span data-ttu-id="cf153-143">A konfigurációs MOF-fájlt a hitelesítő adatok titkosításához kapcsolatos információkért lásd: [biztonságossá tétele a MOF-fájlt](secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="cf153-143">For information about how to encrypt credentials in the configuration MOF file, see [Securing the MOF File](secureMOF.md).</span></span>