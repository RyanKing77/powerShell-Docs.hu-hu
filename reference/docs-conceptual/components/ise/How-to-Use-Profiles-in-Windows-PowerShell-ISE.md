---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Profilok használata a Windows PowerShell ISE-ben
ms.assetid: 0219626a-6da5-4acc-b630-d058e8b29cc6
ms.openlocfilehash: b319aa089c2a4a7008acd9850f15342dac70aee2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057533"
---
# <a name="how-to-use-profiles-in-windows-powershell-ise"></a><span data-ttu-id="e00fb-103">Profilok használata a Windows PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="e00fb-103">How to Use Profiles in Windows PowerShell ISE</span></span>

<span data-ttu-id="e00fb-104">Ez a témakör ismerteti a profilok használata a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE).</span><span class="sxs-lookup"><span data-stu-id="e00fb-104">This topic explains how to use Profiles in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="e00fb-105">Azt javasoljuk, hogy ebben a szakaszban található feladatok végrehajtása, előtt tekintse át [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles), vagy írja be, a konzol ablaktáblában `Get-Help about_Profiles` nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="e00fb-105">We recommend that before performing the tasks in this section, you review [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles), or in the Console Pane, type, `Get-Help about_Profiles` and press **ENTER**.</span></span>

<span data-ttu-id="e00fb-106">A profil a Windows PowerShell ISE parancsfájl, amely akkor fut automatikusan, amikor új munkamenet indításához.</span><span class="sxs-lookup"><span data-stu-id="e00fb-106">A profile is a Windows PowerShell ISE script that runs automatically when you start a new session.</span></span>  <span data-ttu-id="e00fb-107">Egy vagy több Windows PowerShell-profilok létrehozása a Windows PowerShell ISE-ben, és ezek segítségével a konfigurálása a Windows PowerShell vagy a Windows PowerShell ISE környezetben hozzáadása használatát, a változók, aliasok, Funkciók, és a szín és betűtípus előkészítése rendelkezésre álló kívánt beállításai.</span><span class="sxs-lookup"><span data-stu-id="e00fb-107">You can create one or more Windows PowerShell profiles for Windows PowerShell ISE and use them to add the configure the Windows PowerShell or Windows PowerShell ISE environment, preparing it for your use, with variables, aliases, functions, and color and font preferences that you want available.</span></span> <span data-ttu-id="e00fb-108">A profil hatással van minden Windows PowerShell ISE-munkamenetet, amely a megkezdése.</span><span class="sxs-lookup"><span data-stu-id="e00fb-108">A profile affects every Windows PowerShell ISE session that you start.</span></span>

> [!NOTE]
> <span data-ttu-id="e00fb-109">A Windows PowerShell végrehajtási házirend határozza meg, hogy parancsfájlok futtatásához, és egy profil betöltése.</span><span class="sxs-lookup"><span data-stu-id="e00fb-109">The Windows PowerShell execution policy determines whether you can run scripts and load a profile.</span></span> <span data-ttu-id="e00fb-110">Az alapértelmezett végrehajtási házirendet "Tiltott" Megakadályozza, hogy az összes parancsfájl futtatását, beleértve a profilok.</span><span class="sxs-lookup"><span data-stu-id="e00fb-110">The default execution policy, “Restricted,” prevents all scripts from running, including profiles.</span></span> <span data-ttu-id="e00fb-111">Ha a "Tiltott" szabályzatot használja, akkor a profil nem tölthető be.</span><span class="sxs-lookup"><span data-stu-id="e00fb-111">If you use the “Restricted” policy, the profile cannot load.</span></span> <span data-ttu-id="e00fb-112">További információ a végrehajtási házirend: [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span><span class="sxs-lookup"><span data-stu-id="e00fb-112">For more information about execution policy, see [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span></span>

## <a name="selecting-a-profile-to-use-in-the-windows-powershell-ise"></a><span data-ttu-id="e00fb-113">A Windows PowerShell ISE-ben használandó profil kiválasztása</span><span class="sxs-lookup"><span data-stu-id="e00fb-113">Selecting a profile to use in the Windows PowerShell ISE</span></span>

<span data-ttu-id="e00fb-114">Windows PowerShell ISE-ben támogatja a profilok az aktuális felhasználó és minden felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="e00fb-114">Windows PowerShell ISE supports profiles for the current user and all users.</span></span> <span data-ttu-id="e00fb-115">Ezen kívül a Windows PowerShell-profilok, amelyek a alkalmazni a minden gazdagép támogatja.</span><span class="sxs-lookup"><span data-stu-id="e00fb-115">It also supports the Windows PowerShell profiles that apply to all hosts.</span></span>

<span data-ttu-id="e00fb-116">A profilt, amelyet használhat Windows PowerShell és a Windows PowerShell ISE-ben használatáról határozza meg.</span><span class="sxs-lookup"><span data-stu-id="e00fb-116">The profile that you use is determined by how you use Windows PowerShell and Windows PowerShell ISE.</span></span>

- <span data-ttu-id="e00fb-117">Ha csak a Windows PowerShell ISE használatával futtassa a Windows Powershellt, majd mentse összes elemet az ISE-specifikus profilok, például a Windows PowerShell ISE- vagy Windows PowerShell ISE AllUsersCurrentHost profil a CurrentUserCurrentHost egyikében.</span><span class="sxs-lookup"><span data-stu-id="e00fb-117">If you use only Windows PowerShell ISE to run Windows PowerShell, then save all your items in one of the ISE-specific profiles, such as the CurrentUserCurrentHost profile for Windows PowerShell ISE or the AllUsersCurrentHost profile for Windows PowerShell ISE.</span></span>

- <span data-ttu-id="e00fb-118">Ha több gazdagép program használatával futtassa a Windows Powershellt, a functions, aliasok, változók és parancsok mentse a profilt, amely hatással van az összes gazdagép-programok, például a CurrentUserAllHosts vagy AllUsersAllHosts profilban, és mentse az ISE-specifikus szolgáltatásokat, például a szín- és betűtípus testreszabása a Windows PowerShell ISE-ben vagy a AllUsersCurrentHost profilt CurrentUserCurrentHost profilját a Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="e00fb-118">If you use multiple host programs to run Windows PowerShell, save your functions, aliases, variables, and commands in a profile that affects all host programs, such as the CurrentUserAllHosts or the AllUsersAllHosts profile, and save ISE-specific features, like color and font customization in the CurrentUserCurrentHost profile for Windows PowerShell ISE profile or the AllUsersCurrentHost profile for Windows PowerShell ISE.</span></span>

<span data-ttu-id="e00fb-119">Az alábbiakban a profilok létrehozott és használt Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="e00fb-119">The following are profiles that can be created and used in Windows PowerShell ISE.</span></span> <span data-ttu-id="e00fb-120">Az egyes profilok menti a saját egyedi elérési útja.</span><span class="sxs-lookup"><span data-stu-id="e00fb-120">Each profile is saved to its own specific path.</span></span>

| <span data-ttu-id="e00fb-121">Profil típusa</span><span class="sxs-lookup"><span data-stu-id="e00fb-121">Profile Type</span></span> | <span data-ttu-id="e00fb-122">Profil elérési útja</span><span class="sxs-lookup"><span data-stu-id="e00fb-122">Profile Path</span></span> |
| --- | --- |
| <span data-ttu-id="e00fb-123">**Aktuális felhasználó, a PowerShell ISE-ben**</span><span class="sxs-lookup"><span data-stu-id="e00fb-123">**Current user, PowerShell ISE**</span></span>| <span data-ttu-id="e00fb-124">`$PROFILE.CurrentUserCurrentHost`, vagy `$PROFILE`</span><span class="sxs-lookup"><span data-stu-id="e00fb-124">`$PROFILE.CurrentUserCurrentHost`, or `$PROFILE`</span></span> |
| <span data-ttu-id="e00fb-125">**Minden felhasználó, a PowerShell ISE-ben**</span><span class="sxs-lookup"><span data-stu-id="e00fb-125">**All users, PowerShell ISE**</span></span>| `$PROFILE.AllUsersCurrentHost` |
| <span data-ttu-id="e00fb-126">**Aktuális felhasználó, minden gazdagép**</span><span class="sxs-lookup"><span data-stu-id="e00fb-126">**Current user, All hosts**</span></span>| `$PROFILE.CurrentUserAllHosts` |
| <span data-ttu-id="e00fb-127">**Minden felhasználó, minden gazdagép**</span><span class="sxs-lookup"><span data-stu-id="e00fb-127">**All users, All hosts**</span></span> | `$PROFILE.AllUsersAllHosts` |

## <a name="to-create-a-new-profile"></a><span data-ttu-id="e00fb-128">Új profil létrehozása</span><span class="sxs-lookup"><span data-stu-id="e00fb-128">To create a new profile</span></span>

<span data-ttu-id="e00fb-129">Hozzon létre egy új "aktuális felhasználó Windows PowerShell ISE-ben" a profil, futtassa a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="e00fb-129">To create a new “Current user, Windows PowerShell ISE” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE ))
{ New-Item -Type File -Path $PROFILE -Force }
```

<span data-ttu-id="e00fb-130">Hozzon létre egy új "Minden felhasználó, Windows PowerShell ISE-ben" profil, futtassa a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="e00fb-130">To create a new “All users, Windows PowerShell ISE” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersCurrentHost))
{ New-Item -Type File -Path $PROFILE.AllUsersCurrentHost -Force }
```

<span data-ttu-id="e00fb-131">Egy új "aktuális felhasználó összes tároló" profil létrehozásához a következő parancs futtatásával:</span><span class="sxs-lookup"><span data-stu-id="e00fb-131">To create a new “Current user, All Hosts” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.CurrentUserAllHosts))
{ New-Item -Type File -Path $PROFILE.CurrentUserAllHosts -Force }
```

<span data-ttu-id="e00fb-132">"Minden felhasználó az összes tároló" új profil létrehozásához, írja be:</span><span class="sxs-lookup"><span data-stu-id="e00fb-132">To create a new “All users, All Hosts” profile, type:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersAllHosts))
{ New-Item -Type File -Path $PROFILE.AllUsersAllHosts -Force }
```

## <a name="to-edit-a-profile"></a><span data-ttu-id="e00fb-133">Profil szerkesztése</span><span class="sxs-lookup"><span data-stu-id="e00fb-133">To edit a profile</span></span>

1. <span data-ttu-id="e00fb-134">Nyissa meg a profil, futtassa a parancsot psedit a változót, amely meghatározza a szerkeszteni kívánt profilt.</span><span class="sxs-lookup"><span data-stu-id="e00fb-134">To open the profile, run the command psedit with the variable that specifies the profile you want to edit.</span></span> <span data-ttu-id="e00fb-135">Nyissa meg az "aktuális felhasználó, Windows PowerShell ISE-ben" például írja be a profil: `psEdit $PROFILE`</span><span class="sxs-lookup"><span data-stu-id="e00fb-135">For example, to open the “Current user, Windows PowerShell ISE” profile, type: `psEdit $PROFILE`</span></span>

2. <span data-ttu-id="e00fb-136">A profil kívánt elemeket.</span><span class="sxs-lookup"><span data-stu-id="e00fb-136">Add some items to your profile.</span></span> <span data-ttu-id="e00fb-137">Az alábbiakban néhány példa a kezdéshez:</span><span class="sxs-lookup"><span data-stu-id="e00fb-137">The following are a few examples to get you started:</span></span>

   - <span data-ttu-id="e00fb-138">A konzol ablaktáblájában, a fájl profiltípust kék alapértelmezett hátterének színét módosítani: `$psISE.Options.OutputPaneBackground = 'blue'` .</span><span class="sxs-lookup"><span data-stu-id="e00fb-138">To change the default background color of the Console Pane to blue, in the profile file type: `$psISE.Options.OutputPaneBackground = 'blue'` .</span></span> <span data-ttu-id="e00fb-139">A $psISE változó kapcsolatos további információkért lásd: [Windows PowerShell ISE objektummodell-hivatkozás](object-model/The-ISE-Object-Model-Hierarchy.md).</span><span class="sxs-lookup"><span data-stu-id="e00fb-139">For more information about the $psISE variable, see [Windows PowerShell ISE Object Model Reference](object-model/The-ISE-Object-Model-Hierarchy.md).</span></span>

   - <span data-ttu-id="e00fb-140">Betűméret megváltoztatása 20-ra, a profil fájlt be a következőt: `$psISE.Options.FontSize =20`</span><span class="sxs-lookup"><span data-stu-id="e00fb-140">To change font size to 20, in the profile file type: `$psISE.Options.FontSize =20`</span></span>

3. <span data-ttu-id="e00fb-141">A profil fájlt, a menteni a **fájl** menüben kattintson a **mentése**.</span><span class="sxs-lookup"><span data-stu-id="e00fb-141">To save your profile file, on the **File** menu, click **Save**.</span></span> <span data-ttu-id="e00fb-142">A Windows PowerShell ISE-ben következő megnyitásakor a testre szabást érvényesek.</span><span class="sxs-lookup"><span data-stu-id="e00fb-142">Next time you open the Windows PowerShell ISE, your customizations are applied.</span></span>

## <a name="see-also"></a><span data-ttu-id="e00fb-143">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e00fb-143">See Also</span></span>

- [<span data-ttu-id="e00fb-144">about_Profiles</span><span class="sxs-lookup"><span data-stu-id="e00fb-144">about_Profiles</span></span>](/powershell/module/microsoft.powershell.core/about/about_profiles)
- [<span data-ttu-id="e00fb-145">A Windows PowerShell ISE bemutatása</span><span class="sxs-lookup"><span data-stu-id="e00fb-145">Introducing the Windows PowerShell ISE</span></span>](Introducing-the-Windows-PowerShell-ISE.md)