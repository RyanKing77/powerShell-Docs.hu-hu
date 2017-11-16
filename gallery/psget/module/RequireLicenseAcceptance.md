---
ms.date: 2017-06-09
schema: 2.0.0
keywords: PowerShell
title: RequireLicenseAcceptance
ms.openlocfilehash: 260ccc1ee52d09a640e88203c5644f20f9723d6f
ms.sourcegitcommit: cd66d4f49ea762a31887af2c72d087b219ddbe10
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/11/2017
---
# <a name="modules-requiring-license-acceptance"></a>Licenc elfogadása igénylő modulok

## <a name="synopsis"></a>ÖSSZEGZÉST
Az egyes modul közzétevők jogi részlegek szükséges, hogy az ügyfelek kell explicit módon fogadnia a licencfeltételeket a modul PowerShell-galériából telepítése előtt. Ha a felhasználó telepíti, frissítéseket, vagy egy modul segítségével PowerShellGet, közvetlenül vagy egy másik elem függőségei menti, és a modult a felhasználónak kell vállalja, hogy a licenc, a felhasználó jeleznie kell, a licenc elfogadja őket, vagy a művelet sikertelen lesz.

## <a name="publish-requirements-for-modules"></a>Modulok követelményei közzététele

Modulok, amelyeket szeretne felhasználótól megkövetelje-licenc szükséges következő követelményeknek kell teljesítéséhez:
    
- Moduljegyzék PSData szakasza tartalmaznia kell RequireLicenseAcceptance = $True.
- Modul gyökérkönyvtárában license.txt fájl tartalmazza.
- Moduljegyzék licenc Uri kell tartalmaznia.
- A modul PowerShellGet formátum 2.0-s verziójával és a fenti közzé kell tenni.

## <a name="impact-on-installsaveupdate-module"></a>Telepítés/Save/frissítés-modul gyakorolt hatás

- Telepítés/Save/frissítési parancsmagok fogja támogatni egy új paraméter, amely fog viselkedni, mintha a felhasználói licenc látott – AcceptLicense.
- Ha RequiredLicenseAcceptance tulajdonság igaz értékű, és – AcceptLicense nincs megadva, a felhasználó a license.txt, és megjelenítendő jelenik meg: &quot;elfogadja ezeket a licencfeltételeket (Yes/No/YesToAll/NoToAll)&quot;.
  - Ha elfogadja a licencfeltételeket
    - **Mentés-modul:** a modul a program a felhasználó &#39; s rendszer
    - **Install-modul:** a modul a program a felhasználó &#39; s rendszer a megfelelő mappába (hatókör alapján)
    - **Frissítés-modul:** a modul frissülni fog.
  - Ha a rendszer elutasította, a licenc. 
    - A művelet megszakad.
- Az összes parancsmag rákeres a metaadatok (requireLicenseAcceptance és adatformátum-verzió), amely szerint a licencszerződés elfogadását szükség
  - Formátum az ügyfél verziója régebbi, mint 2,0, a művelet sikertelen, és kérje meg, hogy frissítse az ügyfelet.
  - Ha a modul lett közzétéve, hogy a régebbi, mint a 2.0-s verziójú adatformátum, requireLicenseAcceptance jelző figyelmen kívül hagyja.

    
 ## <a name="module-dependencies"></a>A modul függőségek
- Telepítés/Save/frissítése közben. a művelet, ha egy függő modul (valami mással függ a modul) igényel licenc elfogadása, akkor a licenc elfogadása viselkedését (fent) lesz szükség.
- A modul verzió már szerepel a helyi katalógus telepítését a rendszer, ha azt szeretné szülőkönyvtár a licenc.
- Install-mentés-vagy frissítési művelet során egy függő modul licencre van szükség, és a licencszerződés elfogadását nem történik meg, ha a művelet meghiúsul, és hajtsa végre a szokásos folyamatok nem sikerült telepíteni vagy Mentés vagy frissíteni a cikkhez.

 ## <a name="impact-on--force"></a>A - Force gyakorolt hatás

Megadásával – kényszerített nincs elegendő fogadnia a licencfeltételeket. – AcceptLicense jogosultsága a telepítéséhez szükség. Ha – Force meg van adva, RequiredLicenseAcceptance tulajdonság igaz értékű, és – AcceptLicense nincs megadva, a művelet sikertelen lesz.

## <a name="examples"></a>PÉLDÁK

### <a name="example-1-update-module-manifest-to-require-license-acceptance"></a>1. példa: Frissítés modul Alkalmazásjegyzéket licencszerződés elfogadására van szükség
```PowerShell
PS C:\> Update-ModuleManifest -Path C:\modulemanifest.psd1 -RequireLicenseAcceptance

PrivateData = @{

    PSData = @{
        # Flag to indicate whether the module requires explicit user acceptance
        RequireLicenseAcceptance = $true
    } # End of PSData hashtable
    
 } # End of PrivateData hashtable
```
Ez a parancs frissíti a jegyzékfájlt és a RequireLicenseAcceptance jelző IGAZ értékűre állítja be.
### <a name="example-2-install-module-requiring-license-acceptance"></a>2. példa: Telepítés modul megkövetelését licenc elfogadása
```PowerShell
PS C:\> Install-Module -Name ModuleRequireLicenseAcceptance

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
Ez a parancs megjeleníti a licenc license.txt fájlból, és megkérdezi a felhasználót, hogy elfogadja a licencfeltételeket.

### <a name="example-3-install-module-requiring-license-acceptance-with--acceptlicense"></a>3. példa: Telepítés modul megkövetelését licenc elfogadása - AcceptLicense
```PowerShell
PS C:\> Install-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```
Bármely prompt licenc elfogadása nélkül a modul telepítve van.

### <a name="example-4-install-module-requiring-license-acceptance-with--force"></a>4. példa: Telepítés modul megkövetelését licenc elfogadás és a - Force
```PowerShell
PS C:\> Install-Module -Name ModuleRequireLicenseAcceptance -Force
PackageManagement\Install-Package : License Acceptance is required for module 'ModuleRequireLicenseAcceptance'. Please specify '-AcceptLicense' to perform this operation.
At C:\Program Files\WindowsPowerShell\Modules\PowerShellGet\1.1.3.3\PSModule.psm1:1837 char:21
+ ...          $null = PackageManagement\Install-Package @PSBoundParameters
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidArgument: (Microsoft.Power....InstallPackage:InstallPackage) [Install-Package], E
   xception
    + FullyQualifiedErrorId : ForceAcceptLicense,Install-PackageUtility,Microsoft.PowerShell.PackageManagement.Cmdlets
   .InstallPackage
```

### <a name="example-5-install-module-with-dependencies-requiring-license-acceptance"></a>5. példa: Telepítés modul licenc elfogadása igénylő függőségekkel rendelkező
A modul "ModuleWithDependency" modul "ModuleRequireLicenseAcceptance" függ. Licenc elfogadása felhasználótól.
```PowerShell
PS C:\> Install-Module -Name ModuleWithDependency

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

### <a name="example-6-install-module-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>6. példa: Telepítés modul licenc elfogadása és - AcceptLicense függőségekkel rendelkező
A modul "ModuleWithDependency" modul "ModuleRequireLicenseAcceptance" függ. Nem felhasználótól fogadnia a licencfeltételeket, mert - AcceptLicense sincs megadva.
```PowerShell
PS C:\>  Install-Module -Name ModuleWithDependency -AcceptLicense
```
### <a name="example-7-install-module-requiring-license-acceptance-on-a-client-older-than-psgetformatversion-20"></a>7. példa: Egy régebbi, mint PSGetFormatVersion 2.0 ügyfél licencszerződés elfogadására igénylő modul telepítése
```PowerShell
PS C:\windows\system32> Install-Module -Name ModuleRequireLicenseAcceptance

WARNING: The specified module 'ModuleRequireLicenseAcceptance' with PowerShellGetFormatVersion '2.0' is not supported by the current version of PowerShellGet. Get the latest version of the PowerShellGet module to install this module, 'ModuleRequireLicenseAcceptance'.

```
### <a name="example-8-save-module-requiring-license-acceptance"></a>8. példa: Mentés modul igénylő licenc elfogadása
```PowerShell
PS C:\> Save-Module -Name ModuleRequireLicenseAcceptance -Path C:\Saved

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
Ez a parancs megjeleníti a licenc license.txt fájlból, és megkérdezi a felhasználót, hogy elfogadja a licencfeltételeket.

### <a name="example-9-save-module-requiring-license-acceptance-with--acceptlicense"></a>9. példa: Mentés licenc elfogadás és - AcceptLicense igénylő modul
```PowerShell
PS C:\> Save-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense -Path C:\Saved
```
A modul bármely prompt licenc elfogadása nélkül menti a rendszer.

### <a name="example-10-update-module-requiring-license-acceptance"></a>10. példa: Frissítés modul megkövetelését licenc elfogadása
```PowerShell
PS C:\> Update-Module -Name ModuleRequireLicenseAcceptance

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
Ez a parancs megjeleníti a licenc license.txt fájlból, és megkérdezi a felhasználót, hogy elfogadja a licencfeltételeket.

### <a name="example-11-update-module-requiring-license-acceptance-with--acceptlicense"></a>11. példa: Frissítés modul megkövetelését licenc elfogadása - AcceptLicense
```PowerShell
PS C:\> Update-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```
Modul frissül bármely prompt licenc elfogadása nélkül.

## <a name="more-details"></a>További részletekért
### <a name="require-license-acceptance-for-scriptsscriptscriptrequirelicenseacceptancemd"></a>[Parancsfájlok licencszerződés elfogadására van szükség](../script/script_RequireLicenseAcceptance.md)

### <a name="require-license-acceptance-support-on-powershellgallerypsgallerypsgalleryrequireslicenseacceptancemd"></a>[A PowerShellGallery licenc elfogadása támogatásra van szüksége](../../psgallery/psgallery_requires_license_acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationpsgallerypsgallerydeploytoazureautomationrequirelicenseacceptancemd"></a>[Licenc elfogadására van szükség az Azure Automation szolgáltatásbeli központi telepítése](../../psgallery/psgallery_deploy_to_azure_automation_requireLicenseAcceptance.md)
