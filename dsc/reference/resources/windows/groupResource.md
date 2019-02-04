---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-Group erőforrás
ms.openlocfilehash: 9894150f6f749fc23efd4ce2b155b18788557d1d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687509"
---
# <a name="dsc-group-resource"></a><span data-ttu-id="1736c-103">DSC-Group erőforrás</span><span class="sxs-lookup"><span data-stu-id="1736c-103">DSC Group Resource</span></span>

> <span data-ttu-id="1736c-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1736c-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="1736c-105">A csoport erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton helyi csoportok kezelése.</span><span class="sxs-lookup"><span data-stu-id="1736c-105">The Group resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="1736c-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="1736c-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="1736c-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="1736c-107">Properties</span></span>

|  <span data-ttu-id="1736c-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="1736c-108">Property</span></span>  |  <span data-ttu-id="1736c-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="1736c-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="1736c-110">Csoportnév</span><span class="sxs-lookup"><span data-stu-id="1736c-110">GroupName</span></span>| <span data-ttu-id="1736c-111">A csoport, amelyhez szeretne biztosítani egy adott állapot neve.</span><span class="sxs-lookup"><span data-stu-id="1736c-111">The name of the group for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="1736c-112">Hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="1736c-112">Credential</span></span>| <span data-ttu-id="1736c-113">A távoli erőforrások eléréséhez szükséges hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="1736c-113">The credentials required to access remote resources.</span></span> <span data-ttu-id="1736c-114">**Megjegyzés:**: Ennek a fióknak rendelkeznie kell a megfelelő Active Directory-engedélyek minden nem helyi fiók hozzáadása a csoporthoz; Ellenkező esetben hiba lép fel, a konfiguráció célcsomóponton való végrehajtásakor.</span><span class="sxs-lookup"><span data-stu-id="1736c-114">**Note**: This account must have the appropriate Active Directory permissions to add all non-local accounts to the group; otherwise, an error occurs when the configuration is executed on the target node.</span></span>
| <span data-ttu-id="1736c-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="1736c-115">Description</span></span>| <span data-ttu-id="1736c-116">A csoport leírása.</span><span class="sxs-lookup"><span data-stu-id="1736c-116">The description of the group.</span></span>|
| <span data-ttu-id="1736c-117">Győződjön meg, hogy</span><span class="sxs-lookup"><span data-stu-id="1736c-117">Ensure</span></span>| <span data-ttu-id="1736c-118">Azt jelzi, hogy létezik-e a csoportnak.</span><span class="sxs-lookup"><span data-stu-id="1736c-118">Indicates if the group exists.</span></span> <span data-ttu-id="1736c-119">Állítsa be ezt a tulajdonságot a "Hiányzó" annak érdekében, hogy a csoport nem létezik.</span><span class="sxs-lookup"><span data-stu-id="1736c-119">Set this property to "Absent" to ensure that the group does not exist.</span></span> <span data-ttu-id="1736c-120">Beállítása a "Nyújtjuk" (az alapértelmezett érték) biztosítja, hogy a csoport létezik.</span><span class="sxs-lookup"><span data-stu-id="1736c-120">Setting it to "Present" (the default value) ensures that the group exists.</span></span>|
| <span data-ttu-id="1736c-121">Tagok</span><span class="sxs-lookup"><span data-stu-id="1736c-121">Members</span></span>| <span data-ttu-id="1736c-122">Ez a tulajdonság használatával az aktuális csoport tagságának cserélje le a meghatározott tagokat.</span><span class="sxs-lookup"><span data-stu-id="1736c-122">Use this property to replace the current group membership with the specified members.</span></span> <span data-ttu-id="1736c-123">Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="1736c-123">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="1736c-124">Ezzel a tulajdonsággal konfigurációban, ha nem használja a **MembersToExclude** vagy **MembersToInclude** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="1736c-124">If you set this property in a configuration, do not use either the **MembersToExclude** or **MembersToInclude** property.</span></span> <span data-ttu-id="1736c-125">Ezzel létrejön egy hiba.</span><span class="sxs-lookup"><span data-stu-id="1736c-125">Doing so generates an error.</span></span>|
| <span data-ttu-id="1736c-126">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="1736c-126">MembersToExclude</span></span>| <span data-ttu-id="1736c-127">Ez a tulajdonság használatával a meglévő tagság a csoport tagjainak eltávolítását.</span><span class="sxs-lookup"><span data-stu-id="1736c-127">Use this property to remove members from the existing membership of the group.</span></span> <span data-ttu-id="1736c-128">Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="1736c-128">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="1736c-129">Ha ezzel a tulajdonsággal konfigurációban, ne használja a **tagok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="1736c-129">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="1736c-130">Ezzel létrejön egy hiba.</span><span class="sxs-lookup"><span data-stu-id="1736c-130">Doing so generates an error.</span></span>|
| <span data-ttu-id="1736c-131">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="1736c-131">MembersToInclude</span></span>| <span data-ttu-id="1736c-132">Ez a tulajdonság használatával tagok hozzáadása a meglévő tagság a csoport.</span><span class="sxs-lookup"><span data-stu-id="1736c-132">Use this property to add members to the existing membership of the group.</span></span> <span data-ttu-id="1736c-133">Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="1736c-133">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="1736c-134">Ha ezzel a tulajdonsággal konfigurációban, ne használja a **tagok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="1736c-134">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="1736c-135">Így generál hibát.</span><span class="sxs-lookup"><span data-stu-id="1736c-135">Doing so will generate an error.</span></span>|
| <span data-ttu-id="1736c-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="1736c-136">DependsOn</span></span> | <span data-ttu-id="1736c-137">Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="1736c-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="1736c-138">Például, ha az erőforrás-konfiguráció azonosítója parancsfájl-blokk futtatni kívánt első az __ResourceName__ és a típusa __ResourceType__, esetén ez a tulajdonság használatával "DependsOn"[a = Erőforrástípus] ResourceName"s".</span><span class="sxs-lookup"><span data-stu-id="1736c-138">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|

## <a name="example-1"></a><span data-ttu-id="1736c-139">1. példa</span><span class="sxs-lookup"><span data-stu-id="1736c-139">Example 1</span></span>

<span data-ttu-id="1736c-140">Az alábbi példa bemutatja, hogyan annak érdekében, hogy hiányzik egy "TestGroup" nevű csoportot.</span><span class="sxs-lookup"><span data-stu-id="1736c-140">The following example shows how to ensure that a group called "TestGroup" is absent.</span></span>

```powershell
Group GroupExample
{
    # This removes TestGroup, if present
    # To create a new group, set Ensure to "Present“
    Ensure = "Absent"
    GroupName = "TestGroup"
}
```

## <a name="example-2"></a><span data-ttu-id="1736c-141">2. példa</span><span class="sxs-lookup"><span data-stu-id="1736c-141">Example 2</span></span>

<span data-ttu-id="1736c-142">Az alábbi példa bemutatja, hogyan egy Active Directory-felhasználó hozzáadása a helyi Rendszergazdák csoport egy több gép labor hozhat létre, ha már használ egy PSCredential a helyi rendszergazdai fiók részeként.</span><span class="sxs-lookup"><span data-stu-id="1736c-142">The following example shows how to add an Active Directory User to the local administrators group as part of a Multi-Machine Lab build where you are already using a PSCredential for the Local Adminstrator account.</span></span>
<span data-ttu-id="1736c-143">Mivel ez után is használja a tartományi rendszergazdai fiók (előléptetését), majd egy rövid tartományi hitelesítő adatok a meglévő PSCredential konvertálni kell.</span><span class="sxs-lookup"><span data-stu-id="1736c-143">As this is also used for the Domain Admin Account (after Domain promotion), we then need to convert this existing PSCredential to a Domain Friendly credential.</span></span>
<span data-ttu-id="1736c-144">Ezután azt is hozzáadhat egy tartományi felhasználót a helyi Rendszergazdák csoport azon a tagkiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="1736c-144">Then we can add a Domain User to the Local Administrators Group on the Member server.</span></span>

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

## <a name="example-3"></a><span data-ttu-id="1736c-145">3. példa</span><span class="sxs-lookup"><span data-stu-id="1736c-145">Example 3</span></span>

<span data-ttu-id="1736c-146">Az alábbi példa bemutatja, hogyan kell egy helyi csoport TigerTeamAdmins biztosítása, a kiszolgálón az TigerTeamSource.Contoso.Com nem tartalmaz egy adott tartományi fiókot, Contoso\JerryG.</span><span class="sxs-lookup"><span data-stu-id="1736c-146">The following example shows how to ensure a local group, TigerTeamAdmins, on the server TigerTeamSource.Contoso.Com does not contain a particular domain account, Contoso\JerryG.</span></span>

```powershell
Configuration SecureTigerTeamSrouce {
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