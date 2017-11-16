---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-csoport erőforrás"
ms.openlocfilehash: 6fb6c5f9593687d7204ff31fddd9bca978ed2707
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-group-resource"></a><span data-ttu-id="215ae-103">A DSC-csoport erőforrás</span><span class="sxs-lookup"><span data-stu-id="215ae-103">DSC Group Resource</span></span>

> <span data-ttu-id="215ae-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="215ae-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="215ae-105">A csoport erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton helyi csoportok kezelése.</span><span class="sxs-lookup"><span data-stu-id="215ae-105">The Group resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="215ae-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="215ae-106">Syntax</span></span>
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

## <a name="properties"></a><span data-ttu-id="215ae-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="215ae-107">Properties</span></span>

|  <span data-ttu-id="215ae-108">Tulajdonság</span><span class="sxs-lookup"><span data-stu-id="215ae-108">Property</span></span>  |  <span data-ttu-id="215ae-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="215ae-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="215ae-110">Csoportnév</span><span class="sxs-lookup"><span data-stu-id="215ae-110">GroupName</span></span>| <span data-ttu-id="215ae-111">A csoport, amelyekhez egy adott állapot biztosításához neve.</span><span class="sxs-lookup"><span data-stu-id="215ae-111">The name of the group for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="215ae-112">hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="215ae-112">Credential</span></span>| <span data-ttu-id="215ae-113">A távoli erőforrások eléréséhez szükséges hitelesítő adatokat.</span><span class="sxs-lookup"><span data-stu-id="215ae-113">The credentials required to access remote resources.</span></span> <span data-ttu-id="215ae-114">**Megjegyzés:**: ennek a fióknak rendelkeznie kell a megfelelő Active Directory-engedélyek minden nem helyi fiók hozzáadása a csoporthoz,, hiba történik a konfiguráció célcsomóponton való végrehajtásakor.</span><span class="sxs-lookup"><span data-stu-id="215ae-114">**Note**: This account must have the appropriate Active Directory permissions to add all non-local accounts to the group; otherwise, an error occurs when the configuration is executed on the target node.</span></span>  
| <span data-ttu-id="215ae-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="215ae-115">Description</span></span>| <span data-ttu-id="215ae-116">A csoport leírását.</span><span class="sxs-lookup"><span data-stu-id="215ae-116">The description of the group.</span></span>| 
| <span data-ttu-id="215ae-117">Győződjön meg arról</span><span class="sxs-lookup"><span data-stu-id="215ae-117">Ensure</span></span>| <span data-ttu-id="215ae-118">Azt jelzi, hogy a csoport létezik-e.</span><span class="sxs-lookup"><span data-stu-id="215ae-118">Indicates if the group exists.</span></span> <span data-ttu-id="215ae-119">Állítsa be ezt a tulajdonságot "Hiányzik", annak érdekében, hogy a csoport nem létezik.</span><span class="sxs-lookup"><span data-stu-id="215ae-119">Set this property to "Absent" to ensure that the group does not exist.</span></span> <span data-ttu-id="215ae-120">Azt, hogy "" (az alapértelmezett érték) beállítást biztosítja, hogy a csoport létezik.</span><span class="sxs-lookup"><span data-stu-id="215ae-120">Setting it to "Present" (the default value) ensures that the group exists.</span></span>| 
| <span data-ttu-id="215ae-121">Tagok</span><span class="sxs-lookup"><span data-stu-id="215ae-121">Members</span></span>| <span data-ttu-id="215ae-122">Ez a tulajdonság használatával az aktuális csoporttagság cserélje le a megadott tagot.</span><span class="sxs-lookup"><span data-stu-id="215ae-122">Use this property to replace the current group membership with the specified members.</span></span> <span data-ttu-id="215ae-123">Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="215ae-123">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="215ae-124">Ha ez a tulajdonság konfigurációban, nem használja a **MembersToExclude** vagy **MembersToInclude** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="215ae-124">If you set this property in a configuration, do not use either the **MembersToExclude** or **MembersToInclude** property.</span></span> <span data-ttu-id="215ae-125">Ennek során hibát generál.</span><span class="sxs-lookup"><span data-stu-id="215ae-125">Doing so generates an error.</span></span>| 
| <span data-ttu-id="215ae-126">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="215ae-126">MembersToExclude</span></span>| <span data-ttu-id="215ae-127">Ez a tulajdonság használatával az eddigi tagságot a csoport tagjainak eltávolítását.</span><span class="sxs-lookup"><span data-stu-id="215ae-127">Use this property to remove members from the existing membership of the group.</span></span> <span data-ttu-id="215ae-128">Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="215ae-128">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="215ae-129">Ha ez a tulajdonság konfigurációban, ne használja a **tagok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="215ae-129">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="215ae-130">Ennek során hibát generál.</span><span class="sxs-lookup"><span data-stu-id="215ae-130">Doing so generates an error.</span></span>| 
| <span data-ttu-id="215ae-131">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="215ae-131">MembersToInclude</span></span>| <span data-ttu-id="215ae-132">Ez a tulajdonság használatával tagok hozzáadása a meglévő csoport tagságát.</span><span class="sxs-lookup"><span data-stu-id="215ae-132">Use this property to add members to the existing membership of the group.</span></span> <span data-ttu-id="215ae-133">Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*.</span><span class="sxs-lookup"><span data-stu-id="215ae-133">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="215ae-134">Ha ez a tulajdonság konfigurációban, ne használja a **tagok** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="215ae-134">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="215ae-135">Ennek során hibát adnak.</span><span class="sxs-lookup"><span data-stu-id="215ae-135">Doing so will generate an error.</span></span>| 
| <span data-ttu-id="215ae-136">dependsOn</span><span class="sxs-lookup"><span data-stu-id="215ae-136">DependsOn</span></span> | <span data-ttu-id="215ae-137">Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="215ae-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="215ae-138">Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, szintaxisa a következő e tulajdonság használatával "DependsOn ="[ A ResourceType] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="215ae-138">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`\`.</span></span>| 

## <a name="example-1"></a><span data-ttu-id="215ae-139">1. példa</span><span class="sxs-lookup"><span data-stu-id="215ae-139">Example 1</span></span>

<span data-ttu-id="215ae-140">A következő példa bemutatja, hogyan annak érdekében, hogy hiányzik-e a "TestGroup" nevű csoport.</span><span class="sxs-lookup"><span data-stu-id="215ae-140">The following example shows how to ensure that a group called "TestGroup" is absent.</span></span> 

```powershell
Group GroupExample
{
    # This removes TestGroup, if present
    # To create a new group, set Ensure to "Present“
    Ensure = "Absent"
    GroupName = "TestGroup"
}
```
## <a name="example-2"></a><span data-ttu-id="215ae-141">2. példa</span><span class="sxs-lookup"><span data-stu-id="215ae-141">Example 2</span></span>
<span data-ttu-id="215ae-142">A következő példa bemutatja, hogyan egy Active Directory-felhasználó hozzáadása a helyi rendszergazdák csoportjának, ha már használja egy PSCredential a helyi Adminsztrátori fiók Többszámítógépes labor build részeként.</span><span class="sxs-lookup"><span data-stu-id="215ae-142">The following example shows how to add an Active Directory User to the local administrators group as part of a Multi-Machine Lab build where you are already using a PSCredential for the Local Adminstrator account.</span></span> <span data-ttu-id="215ae-143">Ez után is használja a tartományi rendszergazda fiók (előléptetését), majd a meglévő PSCredential átalakítása használandó lehetővé teszi, hogy a tartományi felhasználók hozzáadása a helyi Rendszergazdák csoport azon a tagkiszolgálón rövid tartományi hitelesítő adatokat kell.</span><span class="sxs-lookup"><span data-stu-id="215ae-143">As this is also used for the Domain Admin Account (after Domain promotion) we then need to convert this existing PSCredential to a Domain Friendly credential to enable us to add a Domain User to the Local Administrators Group on the Member server.</span></span>

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

Group AddADUserToLocalAdminGroup
        {
            GroupName='Administrators'   
            Ensure= 'Present'             
            MembersToInclude= "$domain\$($Node.AdminAccount)"
            Credential = $dCredential    
            PsDscRunAsCredential = $DCredential
        }
```

## <a name="example-3"></a><span data-ttu-id="215ae-144">3. példa</span><span class="sxs-lookup"><span data-stu-id="215ae-144">Example 3</span></span>
<span data-ttu-id="215ae-145">A következő példa bemutatja, hogyan egy helyi csoport, TigerTeamAdmins biztosításához, a kiszolgálón az TigerTeamSource.Contoso.Com nem tartalmaz egy adott tartományi fiókot, Contoso\JerryG.</span><span class="sxs-lookup"><span data-stu-id="215ae-145">The following example shows how to ensure a local group, TigerTeamAdmins, on the server TigerTeamSource.Contoso.Com does not contain a particular domain account, Contoso\JerryG.</span></span>  

```powershell

Configuration SecureTigerTeamSrouce 
{
  Import-DscResource -ModuleName 'PSDesiredStateConfiguration'
  
  Node TigerTeamSource.Contoso.Com {
  Group TigerTeamAdmins
    {
       GroupName        = 'TigerTeamAdmins'   
       Ensure           = 'Absent'             
       MembersToInclude = "Contoso\JerryG"
    }
  }
}
```

