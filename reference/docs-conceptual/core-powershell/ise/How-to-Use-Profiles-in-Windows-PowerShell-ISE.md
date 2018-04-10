---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Profilok használata a Windows PowerShell ISE-ben
ms.assetid: 0219626a-6da5-4acc-b630-d058e8b29cc6
ms.openlocfilehash: 8789d6283457f790fdea27657abb2612304e10a1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="how-to-use-profiles-in-windows-powershell-ise"></a><span data-ttu-id="a533d-103">Profilok használata a Windows PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="a533d-103">How to Use Profiles in Windows PowerShell ISE</span></span>

<span data-ttu-id="a533d-104">Ez a témakör ismerteti, hogyan használható a profilok a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE).</span><span class="sxs-lookup"><span data-stu-id="a533d-104">This topic explains how to use Profiles in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="a533d-105">Javasoljuk, hogy ez a szakasz a feladatok elvégzése előtt tekintse át [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles), vagy a konzol ablaktáblájában típusa, `Get-Help about_Profiles` nyomja le az ENTER **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a533d-105">We recommend that before performing the tasks in this section, you review [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles), or in the Console Pane, type, `Get-Help about_Profiles` and press **ENTER**.</span></span>

<span data-ttu-id="a533d-106">A profil egy Windows PowerShell ISE-parancsfájlt, amely automatikusan fut egy új munkamenet indításakor.</span><span class="sxs-lookup"><span data-stu-id="a533d-106">A profile is a Windows PowerShell ISE script that runs automatically when you start a new session.</span></span>  <span data-ttu-id="a533d-107">Hozzon létre egy vagy több Windows PowerShell-profilokat a Windows PowerShell ISE, és segítségükkel adja hozzá a Windows PowerShell vagy a Windows PowerShell ISE környezet konfigurálása a, változók, aliasok, Funkciók, és a színt és használt betűtípus előkészítése használni kívánt elérhető beállítások.</span><span class="sxs-lookup"><span data-stu-id="a533d-107">You can create one or more Windows PowerShell profiles for Windows PowerShell ISE and use them to add the configure the Windows PowerShell or Windows PowerShell ISE environment, preparing it for your use, with variables, aliases, functions, and color and font preferences that you want available.</span></span> <span data-ttu-id="a533d-108">Profil minden Windows PowerShell ISE-munkamenetet, amely elindítja hatással van.</span><span class="sxs-lookup"><span data-stu-id="a533d-108">A profile affects every Windows PowerShell ISE session that you start.</span></span>

> [!NOTE]
> <span data-ttu-id="a533d-109">A Windows PowerShell végrehajtási házirend határozza meg, hogy parancsfájlok futtatásához, és egy profil betöltése.</span><span class="sxs-lookup"><span data-stu-id="a533d-109">The Windows PowerShell execution policy determines whether you can run scripts and load a profile.</span></span> <span data-ttu-id="a533d-110">Az alapértelmezett végrehajtási házirendet "Korlátozott," Megakadályozza, hogy az összes parancsfájl futtatását, beleértve a profilok.</span><span class="sxs-lookup"><span data-stu-id="a533d-110">The default execution policy, “Restricted,” prevents all scripts from running, including profiles.</span></span> <span data-ttu-id="a533d-111">Ha a "Korlátozott" házirendet használja, a profil nem tölthető be.</span><span class="sxs-lookup"><span data-stu-id="a533d-111">If you use the “Restricted” policy, the profile cannot load.</span></span> <span data-ttu-id="a533d-112">Végrehajtási házirenddel kapcsolatos további információkért lásd: [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span><span class="sxs-lookup"><span data-stu-id="a533d-112">For more information about execution policy, see [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span></span>

## <a name="selecting-a-profile-to-use-in-the-windows-powershell-ise"></a><span data-ttu-id="a533d-113">A Windows PowerShell ISE használandó profil kiválasztása</span><span class="sxs-lookup"><span data-stu-id="a533d-113">Selecting a profile to use in the Windows PowerShell ISE</span></span>

<span data-ttu-id="a533d-114">A Windows PowerShell ISE profilok támogatja az aktuális felhasználó és az összes felhasználóra.</span><span class="sxs-lookup"><span data-stu-id="a533d-114">Windows PowerShell ISE supports profiles for the current user and all users.</span></span> <span data-ttu-id="a533d-115">A Windows PowerShell-profilok, amelyek érvényesek az összes gazdagép is támogatja.</span><span class="sxs-lookup"><span data-stu-id="a533d-115">It also supports the Windows PowerShell profiles that apply to all hosts.</span></span>

<span data-ttu-id="a533d-116">A profil, amelyekkel Ön miként használja a Windows PowerShell és a Windows PowerShell ISE határozza meg.</span><span class="sxs-lookup"><span data-stu-id="a533d-116">The profile that you use is determined by how you use Windows PowerShell and Windows PowerShell ISE.</span></span>

- <span data-ttu-id="a533d-117">Ha csak a Windows PowerShell ISE használatával futtassa a Windows Powershellt, majd a elemek mentése az ISE-specifikus profilokhoz, például a Windows PowerShell ISE- vagy Windows PowerShell ISE AllUsersCurrentHost profil a CurrentUserCurrentHost egyikében.</span><span class="sxs-lookup"><span data-stu-id="a533d-117">If you use only Windows PowerShell ISE to run Windows PowerShell, then save all your items in one of the ISE-specific profiles, such as the CurrentUserCurrentHost profile for Windows PowerShell ISE or the AllUsersCurrentHost profile for Windows PowerShell ISE.</span></span>

- <span data-ttu-id="a533d-118">Ha több gazdagépre programok segítségével futtassa a Windows PowerShell, a Funkciók, az aliasokat, a változók és a parancsok mentse egy minden gazdagépre programok, például a CurrentUserAllHosts érintő vagy a AllUsersAllHosts profilt, és ISE-specifikus szolgáltatások, például a Mentés szín- és betűtípus testreszabási Windows PowerShell ISE- vagy AllUsersCurrentHost profil CurrentUserCurrentHost profiljában Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="a533d-118">If you use multiple host programs to run Windows PowerShell, save your functions, aliases, variables, and commands in a profile that affects all host programs, such as the CurrentUserAllHosts or the AllUsersAllHosts profile, and save ISE-specific features, like color and font customization in the CurrentUserCurrentHost profile for Windows PowerShell ISE profile or the AllUsersCurrentHost profile for Windows PowerShell ISE.</span></span>

<span data-ttu-id="a533d-119">A következőkben létrehozott és használt Windows PowerShell ISE profilok.</span><span class="sxs-lookup"><span data-stu-id="a533d-119">The following are profiles that can be created and used in Windows PowerShell ISE.</span></span> <span data-ttu-id="a533d-120">Az egyes profilok menti a saját konkrét elérési utat.</span><span class="sxs-lookup"><span data-stu-id="a533d-120">Each profile is saved to its own specific path.</span></span>

| <span data-ttu-id="a533d-121">Profil típusa</span><span class="sxs-lookup"><span data-stu-id="a533d-121">Profile Type</span></span> | <span data-ttu-id="a533d-122">Profil elérési útja</span><span class="sxs-lookup"><span data-stu-id="a533d-122">Profile Path</span></span> |
| --- | --- |
| <span data-ttu-id="a533d-123">**Aktuális felhasználó, a PowerShell ISE**</span><span class="sxs-lookup"><span data-stu-id="a533d-123">**Current user, PowerShell ISE**</span></span>| <span data-ttu-id="a533d-124">`$PROFILE.CurrentUserCurrentHost`, vagy `$PROFILE`</span><span class="sxs-lookup"><span data-stu-id="a533d-124">`$PROFILE.CurrentUserCurrentHost`, or `$PROFILE`</span></span> |
| <span data-ttu-id="a533d-125">**Minden felhasználó, a PowerShell ISE**</span><span class="sxs-lookup"><span data-stu-id="a533d-125">**All users, PowerShell ISE**</span></span>| `$PROFILE.AllUsersCurrentHost` |
| <span data-ttu-id="a533d-126">**Aktuális felhasználó, minden gazdagép**</span><span class="sxs-lookup"><span data-stu-id="a533d-126">**Current user, All hosts**</span></span>| `$PROFILE.CurrentUserAllHosts` |
| <span data-ttu-id="a533d-127">**Minden felhasználó, minden gazdagép**</span><span class="sxs-lookup"><span data-stu-id="a533d-127">**All users, All hosts**</span></span> | `$PROFILE.AllUsersAllHosts` |

## <a name="to-create-a-new-profile"></a><span data-ttu-id="a533d-128">Új profil létrehozásához</span><span class="sxs-lookup"><span data-stu-id="a533d-128">To create a new profile</span></span>

<span data-ttu-id="a533d-129">Hozzon létre egy új "Current user, a Windows PowerShell ISE" a profil, futtassa a parancsot:</span><span class="sxs-lookup"><span data-stu-id="a533d-129">To create a new “Current user, Windows PowerShell ISE” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE ))
{ New-Item -Type File -Path $PROFILE -Force }
```

<span data-ttu-id="a533d-130">Hozzon létre egy új "Minden felhasználó, a Windows PowerShell ISE" profil, futtassa a parancsot:</span><span class="sxs-lookup"><span data-stu-id="a533d-130">To create a new “All users, Windows PowerShell ISE” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersCurrentHost))
{ New-Item -Type File -Path $PROFILE.AllUsersCurrentHost -Force }
```

<span data-ttu-id="a533d-131">Hozzon létre egy új "aktuális felhasználó, az összes tároló" profilt, futtassa a parancsot:</span><span class="sxs-lookup"><span data-stu-id="a533d-131">To create a new “Current user, All Hosts” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.CurrentUserAllHosts))
{ New-Item -Type File -Path $PROFILE.CurrentUserAllHosts -Force }
```

<span data-ttu-id="a533d-132">"Minden felhasználó az összes tároló" új profil létrehozásához írja be:</span><span class="sxs-lookup"><span data-stu-id="a533d-132">To create a new “All users, All Hosts” profile, type:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersAllHosts))
{ New-Item -Type File -Path $PROFILE.AllUsersAllHosts -Force }
```

## <a name="to-edit-a-profile"></a><span data-ttu-id="a533d-133">A profil szerkesztése</span><span class="sxs-lookup"><span data-stu-id="a533d-133">To edit a profile</span></span>

1. <span data-ttu-id="a533d-134">Nyissa meg a profil, futtassa a parancs psedit a változó határozza meg a szerkeszteni kívánt profilt.</span><span class="sxs-lookup"><span data-stu-id="a533d-134">To open the profile, run the command psedit with the variable that specifies the profile you want to edit.</span></span> <span data-ttu-id="a533d-135">Ahhoz például, hogy nyissa meg a "Current user, a Windows PowerShell ISE" hivatkozásra, írja be: `psEdit $PROFILE`</span><span class="sxs-lookup"><span data-stu-id="a533d-135">For example, to open the “Current user, Windows PowerShell ISE” profile, type: `psEdit $PROFILE`</span></span>

2. <span data-ttu-id="a533d-136">Bizonyos elemek hozzáadása a profilhoz.</span><span class="sxs-lookup"><span data-stu-id="a533d-136">Add some items to your profile.</span></span> <span data-ttu-id="a533d-137">A következő példák néhány az első lépésekhez:</span><span class="sxs-lookup"><span data-stu-id="a533d-137">The following are a few examples to get you started:</span></span>

   - <span data-ttu-id="a533d-138">A konzol ablaktáblában kék profil fájltípus alapértelmezett háttérszíne módosítása: `$psISE.Options.OutputPaneBackground = 'blue'` .</span><span class="sxs-lookup"><span data-stu-id="a533d-138">To change the default background color of the Console Pane to blue, in the profile file type: `$psISE.Options.OutputPaneBackground = 'blue'` .</span></span> <span data-ttu-id="a533d-139">A $psISE változóval kapcsolatos további információkért lásd: [Windows PowerShell ISE objektumhivatkozás modell](The-ISE-Object-Model-Hierarchy.md).</span><span class="sxs-lookup"><span data-stu-id="a533d-139">For more information about the $psISE variable, see [Windows PowerShell ISE Object Model Reference](The-ISE-Object-Model-Hierarchy.md).</span></span>

   - <span data-ttu-id="a533d-140">Betűméret megváltoztatása 20, a profil fájlt be a következőt: `$psISE.Options.FontSize =20`</span><span class="sxs-lookup"><span data-stu-id="a533d-140">To change font size to 20, in the profile file type: `$psISE.Options.FontSize =20`</span></span>

3. <span data-ttu-id="a533d-141">A profil fájlt a menteni a **fájl** menüben kattintson a **mentése**.</span><span class="sxs-lookup"><span data-stu-id="a533d-141">To save your profile file, on the **File** menu, click **Save**.</span></span> <span data-ttu-id="a533d-142">A Windows PowerShell ISE következő megnyitásakor a testreszabások érvényesek.</span><span class="sxs-lookup"><span data-stu-id="a533d-142">Next time you open the Windows PowerShell ISE, your customizations are applied.</span></span>

## <a name="see-also"></a><span data-ttu-id="a533d-143">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a533d-143">See Also</span></span>

- [<span data-ttu-id="a533d-144">about_Profiles</span><span class="sxs-lookup"><span data-stu-id="a533d-144">about_Profiles</span></span>](/powershell/module/microsoft.powershell.core/about/about_profiles)
- [<span data-ttu-id="a533d-145">A Windows PowerShell ISE bemutatása</span><span class="sxs-lookup"><span data-stu-id="a533d-145">Introducing the Windows PowerShell ISE</span></span>](Introducing-the-Windows-PowerShell-ISE.md)