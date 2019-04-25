---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-Group erőforrás
ms.openlocfilehash: 123e09b54a923af942a15f80fa7291c555b4235f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62077347"
---
# <a name="dsc-group-resource"></a><span data-ttu-id="6b410-103">DSC-Group erőforrás</span><span class="sxs-lookup"><span data-stu-id="6b410-103">DSC Group Resource</span></span>

> <span data-ttu-id="6b410-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6b410-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="6b410-105">A csoport erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton helyi csoportok kezelése.</span><span class="sxs-lookup"><span data-stu-id="6b410-105">The Group resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="6b410-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6b410-106">Syntax</span></span>

```
Group [string] #ResourceName
{
    GroupName          = [string]
    [ Credential       = [PSCredential] ]
    [ Description      = [string[]] ]
    [ Ensure           = [string] { Absent | Present }  ]
    [ Members          = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ MembersToInclude = [string[]] ]
    [ DependsOn        = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="6b410-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="6b410-107">Properties</span></span>

|  <span data-ttu-id="6b410-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="6b410-108">Property</span></span>  |  <span data-ttu-id="6b410-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="6b410-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="6b410-110">Csoportnév</span><span class="sxs-lookup"><span data-stu-id="6b410-110">GroupName</span></span>| <span data-ttu-id="6b410-111">A csoport, amelyhez szeretne biztosítani egy adott állapot neve.</span><span class="sxs-lookup"><span data-stu-id="6b410-111">The name of the group for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="6b410-112">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="6b410-112">Credential</span></span>| <span data-ttu-id="6b410-113">A távoli erőforrások eléréséhez szükséges hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="6b410-113">The credentials required to access remote resources.</span></span> <span data-ttu-id="6b410-114">**Megjegyzés:**: Ennek a fióknak rendelkeznie kell a megfelelő Active Directory-engedélyek minden nem helyi fiók hozzáadása a csoporthoz; Ellenkező esetben hiba lép fel, a konfiguráció célcsomóponton való végrehajtásakor.</span><span class="sxs-lookup"><span data-stu-id="6b410-114">**Note**: This account must have the appropriate Active Directory permissions to add all non-local accounts to the group; otherwise, an error occurs when the configuration is executed on the target node.</span></span>
| <span data-ttu-id="6b410-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="6b410-115">Description</span></span>| <span data-ttu-id="6b410-116">A csoport leírása.</span><span class="sxs-lookup"><span data-stu-id="6b410-116">The description of the group.</span></span>|
| <span data-ttu-id="6b410-117">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="6b410-117">Ensure</span></span>| <span data-ttu-id="6b410-118">Azt jelzi, hogy létezik-e a csoportnak.</span><span class="sxs-lookup"><span data-stu-id="6b410-118">Indicates if the group exists.</span></span> <span data-ttu-id="6b410-119">Állítsa be ezt a tulajdonságot a "Hiányzó" annak érdekében, hogy a csoport nem létezik.</span><span class="sxs-lookup"><span data-stu-id="6b410-119">Set this property to "Absent" to ensure that the group does not exist.</span></span> <span data-ttu-id="6b410-120">Beállítása a "Nyújtjuk" (az alapértelmezett érték) biztosítja, hogy a csoport létezik.</span><span class="sxs-lookup"><span data-stu-id="6b410-120">Setting it to "Present" (the default value) ensures that the group exists.</span></span>|
| <span data-ttu-id="6b410-121">Tagok</span><span class="sxs-lookup"><span data-stu-id="6b410-121">Members</span></span>| <span data-ttu-id="6b410-122">Ez a tulajdonság használatával az aktuális csoport tagságának cserélje le a meghatározott tagokat.</span><span class="sxs-lookup"><span data-stu-id="6b410-122">Use this property to replace the current group membership with the specified members.</span></span> <span data-ttu-id="6b410-123">Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="6b410-123">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="6b410-124">Ezzel a tulajdonsággal konfigurációban, ha nem használja a **MembersToExclude** vagy **MembersToInclude** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="6b410-124">If you set this property in a configuration, do not use either the **MembersToExclude** or **MembersToInclude** property.</span></span> <span data-ttu-id="6b410-125">Ezzel létrejön egy hiba.</span><span class="sxs-lookup"><span data-stu-id="6b410-125">Doing so generates an error.</span></span>|
| <span data-ttu-id="6b410-126">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="6b410-126">MembersToExclude</span></span>| <span data-ttu-id="6b410-127">Ez a tulajdonság használatával a meglévő tagság a csoport tagjainak eltávolítását.</span><span class="sxs-lookup"><span data-stu-id="6b410-127">Use this property to remove members from the existing membership of the group.</span></span> <span data-ttu-id="6b410-128">Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="6b410-128">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="6b410-129">Ha ezzel a tulajdonsággal konfigurációban, ne használja a **tagok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="6b410-129">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="6b410-130">Ezzel létrejön egy hiba.</span><span class="sxs-lookup"><span data-stu-id="6b410-130">Doing so generates an error.</span></span>|
| <span data-ttu-id="6b410-131">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="6b410-131">MembersToInclude</span></span>| <span data-ttu-id="6b410-132">Ez a tulajdonság használatával tagok hozzáadása a meglévő tagság a csoport.</span><span class="sxs-lookup"><span data-stu-id="6b410-132">Use this property to add members to the existing membership of the group.</span></span> <span data-ttu-id="6b410-133">Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="6b410-133">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="6b410-134">Ha ezzel a tulajdonsággal konfigurációban, ne használja a **tagok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="6b410-134">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="6b410-135">Így generál hibát.</span><span class="sxs-lookup"><span data-stu-id="6b410-135">Doing so will generate an error.</span></span>|
| <span data-ttu-id="6b410-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="6b410-136">DependsOn</span></span> | <span data-ttu-id="6b410-137">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="6b410-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="6b410-138">Például, ha az erőforrás-konfiguráció azonosítója parancsfájl-blokk futtatni kívánt első az __ResourceName__ és a típusa __ResourceType__, esetén ez a tulajdonság használatával "DependsOn"[a = Erőforrástípus] ResourceName"s".</span><span class="sxs-lookup"><span data-stu-id="6b410-138">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|

## <a name="example-1"></a><span data-ttu-id="6b410-139">1. példa</span><span class="sxs-lookup"><span data-stu-id="6b410-139">Example 1</span></span>

<span data-ttu-id="6b410-140">Az alábbi példa bemutatja, hogyan annak érdekében, hogy hiányzik egy "TestGroup" nevű csoportot.</span><span class="sxs-lookup"><span data-stu-id="6b410-140">The following example shows how to ensure that a group called "TestGroup" is absent.</span></span>

```powershell
Group GroupExample
{
    # This removes TestGroup, if present
    # To create a new group, set Ensure to "Present“
    Ensure = "Absent"
    GroupName = "TestGroup"
}
```

## <a name="example-2"></a><span data-ttu-id="6b410-141">2. példa</span><span class="sxs-lookup"><span data-stu-id="6b410-141">Example 2</span></span>

<span data-ttu-id="6b410-142">Az alábbi példa bemutatja, hogyan egy Active Directory-felhasználó hozzáadása a helyi Rendszergazdák csoport már használata pscredential adattá a helyi rendszergazdai fiók több gép labor build részeként.</span><span class="sxs-lookup"><span data-stu-id="6b410-142">The following example shows how to add an Active Directory User to the local administrators group as part of a Multi-Machine Lab build where you are already using a PSCredential for the Local Administrator account.</span></span>
<span data-ttu-id="6b410-143">Mivel ez után is használja a tartományi rendszergazdai fiók (előléptetését), majd egy rövid tartományi hitelesítő adatok a meglévő PSCredential konvertálni kell.</span><span class="sxs-lookup"><span data-stu-id="6b410-143">As this is also used for the Domain Admin Account (after Domain promotion), we then need to convert this existing PSCredential to a Domain Friendly credential.</span></span>
<span data-ttu-id="6b410-144">Ezután azt is hozzáadhat egy tartományi felhasználót a helyi Rendszergazdák csoport azon a tagkiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="6b410-144">Then we can add a Domain User to the Local Administrators Group on the Member server.</span></span>

```powershell
@{
    AllNodes = @(
        @{
            NodeName = '*';
            DomainName = 'SubTest.contoso.com';
         }
        @{
            NodeName = 'Box2';
            AdminAccount = 'Admin-Dave_Alexanderson'
        }
    )
}

$domain = $node.DomainName.split('.')[0]
$DCredential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList ("$domain\$($credential.Username)", $Credential.Password)

Group AddADUserToLocalAdminGroup {
    GroupName='Administrators'
    Ensure= 'Present'
    MembersToInclude= "$domain\$($Node.AdminAccount)"
    Credential = $dCredential
    PsDscRunAsCredential = $DCredential
}
```

## <a name="example-3"></a><span data-ttu-id="6b410-145">3. példa</span><span class="sxs-lookup"><span data-stu-id="6b410-145">Example 3</span></span>

<span data-ttu-id="6b410-146">Az alábbi példa bemutatja, hogyan kell egy helyi csoport TigerTeamAdmins biztosítása, a kiszolgálón az TigerTeamSource.Contoso.Com nem tartalmaz egy adott tartományi fiókot, Contoso\JerryG.</span><span class="sxs-lookup"><span data-stu-id="6b410-146">The following example shows how to ensure a local group, TigerTeamAdmins, on the server TigerTeamSource.Contoso.Com does not contain a particular domain account, Contoso\JerryG.</span></span>

```powershell
Configuration SecureTigerTeamSource {
  Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

  Node TigerTeamSource.Contoso.Com {
    Group TigerTeamAdmins {
       GroupName        = 'TigerTeamAdmins'
       Ensure           = 'Present'
       MembersToExclude = "Contoso\JerryG"
    }
  }
}
```