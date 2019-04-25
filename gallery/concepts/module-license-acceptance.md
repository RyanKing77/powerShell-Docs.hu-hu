---
ms.date: 06/09/2017
schema: 2.0.0
keywords: PowerShell
title: Licencfeltételek elfogadását igénylő modulok
ms.openlocfilehash: 369e32d5278a2e1bf1d3f2ae67f670c524b9f878
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62075222"
---
# <a name="modules-requiring-license-acceptance"></a><span data-ttu-id="a6aae-103">Licencfeltételek elfogadását igénylő modulok</span><span class="sxs-lookup"><span data-stu-id="a6aae-103">Modules Requiring License Acceptance</span></span>

## <a name="synopsis"></a><span data-ttu-id="a6aae-104">SYNOPSIS</span><span class="sxs-lookup"><span data-stu-id="a6aae-104">SYNOPSIS</span></span>

<span data-ttu-id="a6aae-105">Néhány modul közzétevők jogi részlegek számára szükséges, hogy ügyfeleink kell explicit módon fogadnia a licencfeltételeket PowerShell-galériából a modul telepítése előtt.</span><span class="sxs-lookup"><span data-stu-id="a6aae-105">Legal departments for some module publishers require that customers must explicitly accept the license before installing their module from PowerShell Gallery.</span></span> <span data-ttu-id="a6aae-106">Ha egy felhasználó telepíti, frissíti, vagy közvetlenül vagy egy másik csomagnak függőségként a PowerShellGet,-modul menti, és a modulnak szüksége van arra, hogy egy licencet a felhasználó, a felhasználó jeleznie kell, akkor el kell fogadnia a licencfeltételeket, vagy a művelet sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="a6aae-106">If a user installs, updates, or saves a module using PowerShellGet, whether directly or as a dependency for another package, and that module requires the user to agree to a license, the user must indicate they accept the license or the operation fails.</span></span>

## <a name="publish-requirements-for-modules"></a><span data-ttu-id="a6aae-107">Modulok követelményei közzététele</span><span class="sxs-lookup"><span data-stu-id="a6aae-107">Publish Requirements for Modules</span></span>

<span data-ttu-id="a6aae-108">Modulok, amelyeket a felhasználók licenc elfogadására szeretne az alábbi követelményeknek kell teljesíteni:</span><span class="sxs-lookup"><span data-stu-id="a6aae-108">Modules that would like to require users to accept license should fulfill following requirements:</span></span>

- <span data-ttu-id="a6aae-109">Moduljegyzék PSData szakaszában tartalmaznia kell RequireLicenseAcceptance = $True.</span><span class="sxs-lookup"><span data-stu-id="a6aae-109">PSData section of module manifest should include RequireLicenseAcceptance = $True.</span></span>
- <span data-ttu-id="a6aae-110">A modul license.txt fájlt a gyökérkönyvtárban tartalmaznia kell.</span><span class="sxs-lookup"><span data-stu-id="a6aae-110">Module should contain license.txt file in root directory.</span></span>
- <span data-ttu-id="a6aae-111">Moduljegyzék licenc URI-t kell tartalmaznia.</span><span class="sxs-lookup"><span data-stu-id="a6aae-111">Module manifest should contain License Uri.</span></span>
- <span data-ttu-id="a6aae-112">A modul a PowerShellGet formátum 2.0-s verziójával és újabb közzé kell tenni.</span><span class="sxs-lookup"><span data-stu-id="a6aae-112">Module should be published with PowerShellGet Format Version 2.0 and above.</span></span>

## <a name="impact-on-installsaveupdate-module"></a><span data-ttu-id="a6aae-113">Telepítés/Save/Update-Module gyakorolt hatás</span><span class="sxs-lookup"><span data-stu-id="a6aae-113">Impact on Install/Save/Update-Module</span></span>

- <span data-ttu-id="a6aae-114">Telepítés/Save/frissítési parancsmagok támogatni fogja az új paraméter, amely fog viselkedni, mintha a felhasználói licenc látott – AcceptLicense.</span><span class="sxs-lookup"><span data-stu-id="a6aae-114">Install/Save/Update cmdlets will support a new parameter –AcceptLicense that will behave as though the user saw the license.</span></span>
- <span data-ttu-id="a6aae-115">Ha nincs megadva a – AcceptLicense RequiredLicenseAcceptance értéke igaz, a felhasználó lesz látható a license.txt, és a rendszer: &quot;Elfogadja ezeket a licencfeltételeket (Yes/No/YesToAll/NoToAll)&quot;.</span><span class="sxs-lookup"><span data-stu-id="a6aae-115">If RequiredLicenseAcceptance is True and –AcceptLicense is not specified, the user will be shown the license.txt, and prompted with: &quot;Do you accept these license terms (Yes/No/YesToAll/NoToAll)&quot;.</span></span>
  - <span data-ttu-id="a6aae-116">Ha elfogadja a licencfeltételeket</span><span class="sxs-lookup"><span data-stu-id="a6aae-116">If the license is accepted</span></span>
    - <span data-ttu-id="a6aae-117">**Save-Module:** lesznek másolva a modul a felhasználó&#39;s rendszer</span><span class="sxs-lookup"><span data-stu-id="a6aae-117">**Save-Module:** the module will be copied to the user&#39;s system</span></span>
    - <span data-ttu-id="a6aae-118">**Install-Module:** lesznek másolva a modul a felhasználó&#39;s rendszer a megfelelő mappába (hatókör alapján)</span><span class="sxs-lookup"><span data-stu-id="a6aae-118">**Install-Module:** the module will be copied to the user&#39;s system to the proper folder (based on scope)</span></span>
    - <span data-ttu-id="a6aae-119">**Frissítés-modul:** a modul frissülni fog.</span><span class="sxs-lookup"><span data-stu-id="a6aae-119">**Update-Module:** the module will be updated.</span></span>
  - <span data-ttu-id="a6aae-120">Ha nem fogadta el a licencet a rendszer.</span><span class="sxs-lookup"><span data-stu-id="a6aae-120">If the license is declined.</span></span>
    - <span data-ttu-id="a6aae-121">Művelet megszakad.</span><span class="sxs-lookup"><span data-stu-id="a6aae-121">Operation will be cancelled.</span></span>
    - <span data-ttu-id="a6aae-122">Minden parancsmag rákeres arról, hogy egy licenc elfogadása szükséges metaadatokat (requireLicenseAcceptance és adatformátum-verzió)</span><span class="sxs-lookup"><span data-stu-id="a6aae-122">All cmdlets will check for the metadata(requireLicenseAcceptance and Format Version) that says a license acceptance is required</span></span>
    - <span data-ttu-id="a6aae-123">Ha ügyfél formátumú verziója régebbi, mint 2,0., a művelet sikertelen, és kérje meg a felhasználó frissítheti az ügyfelet.</span><span class="sxs-lookup"><span data-stu-id="a6aae-123">If format version of client is older than 2.0, operation will fail and ask the user to update the client.</span></span>
    - <span data-ttu-id="a6aae-124">Ha a modul úgy lett közzétéve, 2.0-s verziónál régebbi formátumban-verzióval rendelkező, requireLicenseAcceptance jelző figyelmen kívül.</span><span class="sxs-lookup"><span data-stu-id="a6aae-124">If module was published with format version older than 2.0, requireLicenseAcceptance flag will be ignored.</span></span>

## <a name="module-dependencies"></a><span data-ttu-id="a6aae-125">A modul függőségek</span><span class="sxs-lookup"><span data-stu-id="a6aae-125">Module Dependencies</span></span>

- <span data-ttu-id="a6aae-126">Telepítés/Save/frissítése során szükség lesz a művelet, ha egy függő modul (valami mást attól függ, a modul) van szüksége a licencfeltételek elfogadását, majd a licenc elfogadása viselkedése (feljebb).</span><span class="sxs-lookup"><span data-stu-id="a6aae-126">During Install/Save/Update operation, if a dependent module(something else depends on the module) requires license acceptance, then the license acceptance behavior (above) will be required.</span></span>
- <span data-ttu-id="a6aae-127">Ha a modul verzió telepítését a rendszer a helyi katalógus már fel van sorolva, hogy lenne szülőkönyvtár a licenc.</span><span class="sxs-lookup"><span data-stu-id="a6aae-127">If the module version is already listed in the local catalog as being installed on the system, we would bypass the license checking.</span></span>
- <span data-ttu-id="a6aae-128">Telepítés/Save/frissítés művelet során egy függő modul licencre van szüksége, és a licencfeltételek elfogadását nem történik meg, ha a művelet meghiúsul, és kövesse a normál folyamatok a csomag telepítése/save/frissítése nem sikerült.</span><span class="sxs-lookup"><span data-stu-id="a6aae-128">During Install/Save/Update operation, if a dependent module requires a license, and the license acceptance does not occur, the operation will fail and follow normal processes for the package failed to install/save/update.</span></span>

## <a name="impact-on--force"></a><span data-ttu-id="a6aae-129">A - Force gyakorolt hatás</span><span class="sxs-lookup"><span data-stu-id="a6aae-129">Impact on -Force</span></span>

<span data-ttu-id="a6aae-130">Adjon meg `–Force` nem elegendő az, hogy fogadja el a licencet.</span><span class="sxs-lookup"><span data-stu-id="a6aae-130">Specifying `–Force` is NOT sufficient to accept a license.</span></span> <span data-ttu-id="a6aae-131">`–AcceptLicense` engedély telepítéséhez szükség.</span><span class="sxs-lookup"><span data-stu-id="a6aae-131">`–AcceptLicense` is required for permission to install.</span></span> <span data-ttu-id="a6aae-132">Ha `–Force` van megadva, RequiredLicenseAcceptance értéke igaz, és `–AcceptLicense` nincs megadva, a művelet sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="a6aae-132">If `–Force` is specified, RequiredLicenseAcceptance is True, and `–AcceptLicense` is NOT specified, the operation will fail.</span></span>

## <a name="examples"></a><span data-ttu-id="a6aae-133">EXAMPLES</span><span class="sxs-lookup"><span data-stu-id="a6aae-133">EXAMPLES</span></span>

### <a name="example-1-update-module-manifest-to-require-license-acceptance"></a><span data-ttu-id="a6aae-134">1. példa: Licencfeltételek elfogadásának kérése az Alkalmazásjegyzéket az modul frissítése</span><span class="sxs-lookup"><span data-stu-id="a6aae-134">Example 1: Update Module Manifest to require license acceptance</span></span>

```powershell
Update-ModuleManifest -Path C:\modulemanifest.psd1 -RequireLicenseAcceptance -PrivateData @{
    PSData = @{
        # Flag to indicate whether the module requires explicit user acceptance
        RequireLicenseAcceptance = $true
    } # End of PSData hashtable

 } # End of PrivateData hashtable
```

<span data-ttu-id="a6aae-135">Ez a parancs frissíti a jegyzékfájlt, és a RequireLicenseAcceptance jelzőt igaz értékre állítja.</span><span class="sxs-lookup"><span data-stu-id="a6aae-135">This command updates the manifest file and sets the RequireLicenseAcceptance flag to true.</span></span>

### <a name="example-2-install-module-requiring-license-acceptance"></a><span data-ttu-id="a6aae-136">2. példa: Licencfeltételek elfogadását igénylő modul telepítése</span><span class="sxs-lookup"><span data-stu-id="a6aae-136">Example 2: Install Module requiring license acceptance</span></span>

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance
```

```output
License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

<span data-ttu-id="a6aae-137">Ez a parancs megjeleníti a licenc license.txt fájlból, és kéri a felhasználót, fogadja el a licencfeltételeket.</span><span class="sxs-lookup"><span data-stu-id="a6aae-137">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-3-install-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="a6aae-138">3. példa: A - AcceptLicense licencfeltételek elfogadását igénylő modul telepítése</span><span class="sxs-lookup"><span data-stu-id="a6aae-138">Example 3: Install Module requiring license acceptance with -AcceptLicense</span></span>

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

<span data-ttu-id="a6aae-139">A modul telepítve van minden licenc elfogadására kérése nélkül.</span><span class="sxs-lookup"><span data-stu-id="a6aae-139">Module is installed without any prompt to accept license.</span></span>

### <a name="example-4-install-module-requiring-license-acceptance-with--force"></a><span data-ttu-id="a6aae-140">4. példa: A - Force licencfeltételek elfogadását igénylő modul telepítése</span><span class="sxs-lookup"><span data-stu-id="a6aae-140">Example 4: Install Module requiring license acceptance with -Force</span></span>

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance -Force
```

```output
PackageManagement\Install-Package : License Acceptance is required for module 'ModuleRequireLicenseAcceptance'. Please specify '-AcceptLicense' to perform this operation.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.1.3.3\PSModule.psm1:1837 char:21
+ ...          $null = PackageManagement\Install-Package @PSBoundParameters
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (Microsoft.Power....InstallPackage:InstallPackage) [Install-Package], E
   xception
    + FullyQualifiedErrorId : ForceAcceptLicense,Install-PackageUtility,Microsoft.PowerShell.PackageManagement.Cmdlets
   .InstallPackage
```

### <a name="example-5-install-module-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="a6aae-141">5. példa: Licencfeltételek elfogadását igénylő függőségekkel modul telepítése</span><span class="sxs-lookup"><span data-stu-id="a6aae-141">Example 5: Install Module with dependencies requiring license acceptance</span></span>

<span data-ttu-id="a6aae-142">A modul "ModuleWithDependency" modul "ModuleRequireLicenseAcceptance" függ.</span><span class="sxs-lookup"><span data-stu-id="a6aae-142">Module 'ModuleWithDependency' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="a6aae-143">Licenc fogadja el a rendszer kéri.</span><span class="sxs-lookup"><span data-stu-id="a6aae-143">User is prompted to Accept License.</span></span>

```powershell
Install-Module -Name ModuleWithDependency
```

```output
License Acceptance
MIT License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

### <a name="example-6-install-module-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="a6aae-144">6. példa: Licencfeltételek elfogadásának és - AcceptLicense függőségekkel modul telepítése</span><span class="sxs-lookup"><span data-stu-id="a6aae-144">Example 6: Install Module with dependencies requiring license acceptance and -AcceptLicense</span></span>

<span data-ttu-id="a6aae-145">A modul "ModuleWithDependency" modul "ModuleRequireLicenseAcceptance" függ.</span><span class="sxs-lookup"><span data-stu-id="a6aae-145">Module 'ModuleWithDependency' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="a6aae-146">Fogadja el a licenc - AcceptLicense van megadva, az nem kéri a felhasználótól.</span><span class="sxs-lookup"><span data-stu-id="a6aae-146">User is not prompted to accept license as -AcceptLicense is specified.</span></span>

```powershell
Install-Module -Name ModuleWithDependency -AcceptLicense
```

### <a name="example-7-install-module-requiring-license-acceptance-on-a-client-older-than-psgetformatversion-20"></a><span data-ttu-id="a6aae-147">7. példa: A régebbi, mint PSGetFormatVersion 2.0-s ügyfél licencfeltételek elfogadását igénylő modul telepítése</span><span class="sxs-lookup"><span data-stu-id="a6aae-147">Example 7: Install module requiring license acceptance on a client older than PSGetFormatVersion 2.0</span></span>

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance
```

```output
WARNING: The specified module 'ModuleRequireLicenseAcceptance' with PowerShellGetFormatVersion '2.0' is not supported by the current version of PowerShellGet. Get the latest version of the PowerShellGet module to install this module, 'ModuleRequireLicenseAcceptance'.
```

### <a name="example-8-save-module-requiring-license-acceptance"></a><span data-ttu-id="a6aae-148">8. példa: Licencfeltételek elfogadását igénylő modul mentése</span><span class="sxs-lookup"><span data-stu-id="a6aae-148">Example 8: Save Module requiring license acceptance</span></span>

```powershell
Save-Module -Name ModuleRequireLicenseAcceptance -Path C:\Saved
```

```output
License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

<span data-ttu-id="a6aae-149">Ez a parancs megjeleníti a licenc license.txt fájlból, és kéri a felhasználót, fogadja el a licencfeltételeket.</span><span class="sxs-lookup"><span data-stu-id="a6aae-149">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-9-save-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="a6aae-150">9. példa: A modul - AcceptLicense a licencfeltételek elfogadását igénylő mentése</span><span class="sxs-lookup"><span data-stu-id="a6aae-150">Example 9: Save Module requiring license acceptance with -AcceptLicense</span></span>

```powershell
Save-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense -Path C:\Saved
```

<span data-ttu-id="a6aae-151">A modul a rendszer minden licenc elfogadására kérdés nélkül menti.</span><span class="sxs-lookup"><span data-stu-id="a6aae-151">Module is saved without any prompt to accept license.</span></span>

### <a name="example-10-update-module-requiring-license-acceptance"></a><span data-ttu-id="a6aae-152">10. példa: Licencfeltételek elfogadását igénylő modulok frissítésére</span><span class="sxs-lookup"><span data-stu-id="a6aae-152">Example 10: Update Module requiring license acceptance</span></span>

```powershell
Update-Module -Name ModuleRequireLicenseAcceptance
```

```output
License Acceptance

License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

<span data-ttu-id="a6aae-153">Ez a parancs megjeleníti a licenc license.txt fájlból, és kéri a felhasználót, fogadja el a licencfeltételeket.</span><span class="sxs-lookup"><span data-stu-id="a6aae-153">This command shows the license from license.txt file and prompts the user to accept the license.</span></span>

### <a name="example-11-update-module-requiring-license-acceptance-with--acceptlicense"></a><span data-ttu-id="a6aae-154">11. példa: A - AcceptLicense licencfeltételek elfogadását igénylő modulok frissítésére</span><span class="sxs-lookup"><span data-stu-id="a6aae-154">Example 11: Update Module requiring license acceptance with -AcceptLicense</span></span>

```powershell
Update-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

<span data-ttu-id="a6aae-155">A modul frissül minden licenc elfogadására kérése nélkül.</span><span class="sxs-lookup"><span data-stu-id="a6aae-155">Module is updated without any prompt to accept license.</span></span>

## <a name="more-details"></a><span data-ttu-id="a6aae-156">További részletek</span><span class="sxs-lookup"><span data-stu-id="a6aae-156">More details</span></span>

[<span data-ttu-id="a6aae-157">Licencfeltételek elfogadásának megkövetelése a parancsfájlokhoz</span><span class="sxs-lookup"><span data-stu-id="a6aae-157">Require License Acceptance for Scripts</span></span>](./script-license-acceptance.md)

[<span data-ttu-id="a6aae-158">A PowerShell-Galériabeli licencfeltételek elfogadását támogatásra van szüksége</span><span class="sxs-lookup"><span data-stu-id="a6aae-158">Require License Acceptance support on PowerShellGallery</span></span>](../how-to/working-with-packages/packages-that-require-license-acceptance.md)

[<span data-ttu-id="a6aae-159">Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez</span><span class="sxs-lookup"><span data-stu-id="a6aae-159">Require License Acceptance on Deploy to Azure Automation</span></span>](../how-to/working-with-packages/deploy-to-azure-automation.md)
