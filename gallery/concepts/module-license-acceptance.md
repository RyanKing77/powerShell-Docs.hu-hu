---
ms.date: 06/09/2017
schema: 2.0.0
keywords: PowerShell
title: Licencfeltételek elfogadását igénylő modulok
ms.openlocfilehash: 369e32d5278a2e1bf1d3f2ae67f670c524b9f878
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687530"
---
# <a name="modules-requiring-license-acceptance"></a>Licencfeltételek elfogadását igénylő modulok

## <a name="synopsis"></a>SYNOPSIS

Néhány modul közzétevők jogi részlegek számára szükséges, hogy ügyfeleink kell explicit módon fogadnia a licencfeltételeket PowerShell-galériából a modul telepítése előtt. Ha egy felhasználó telepíti, frissíti, vagy közvetlenül vagy egy másik csomagnak függőségként a PowerShellGet,-modul menti, és a modulnak szüksége van arra, hogy egy licencet a felhasználó, a felhasználó jeleznie kell, akkor el kell fogadnia a licencfeltételeket, vagy a művelet sikertelen lesz.

## <a name="publish-requirements-for-modules"></a>Modulok követelményei közzététele

Modulok, amelyeket a felhasználók licenc elfogadására szeretne az alábbi követelményeknek kell teljesíteni:

- Moduljegyzék PSData szakaszában tartalmaznia kell RequireLicenseAcceptance = $True.
- A modul license.txt fájlt a gyökérkönyvtárban tartalmaznia kell.
- Moduljegyzék licenc URI-t kell tartalmaznia.
- A modul a PowerShellGet formátum 2.0-s verziójával és újabb közzé kell tenni.

## <a name="impact-on-installsaveupdate-module"></a>Telepítés/Save/Update-Module gyakorolt hatás

- Telepítés/Save/frissítési parancsmagok támogatni fogja az új paraméter, amely fog viselkedni, mintha a felhasználói licenc látott – AcceptLicense.
- Ha nincs megadva a – AcceptLicense RequiredLicenseAcceptance értéke igaz, a felhasználó lesz látható a license.txt, és a rendszer: &quot;Elfogadja ezeket a licencfeltételeket (Yes/No/YesToAll/NoToAll)&quot;.
  - Ha elfogadja a licencfeltételeket
    - **Save-Module:** lesznek másolva a modul a felhasználó&#39;s rendszer
    - **Install-Module:** lesznek másolva a modul a felhasználó&#39;s rendszer a megfelelő mappába (hatókör alapján)
    - **Frissítés-modul:** a modul frissülni fog.
  - Ha nem fogadta el a licencet a rendszer.
    - Művelet megszakad.
    - Minden parancsmag rákeres arról, hogy egy licenc elfogadása szükséges metaadatokat (requireLicenseAcceptance és adatformátum-verzió)
    - Ha ügyfél formátumú verziója régebbi, mint 2,0., a művelet sikertelen, és kérje meg a felhasználó frissítheti az ügyfelet.
    - Ha a modul úgy lett közzétéve, 2.0-s verziónál régebbi formátumban-verzióval rendelkező, requireLicenseAcceptance jelző figyelmen kívül.

## <a name="module-dependencies"></a>A modul függőségek

- Telepítés/Save/frissítése során szükség lesz a művelet, ha egy függő modul (valami mást attól függ, a modul) van szüksége a licencfeltételek elfogadását, majd a licenc elfogadása viselkedése (feljebb).
- Ha a modul verzió telepítését a rendszer a helyi katalógus már fel van sorolva, hogy lenne szülőkönyvtár a licenc.
- Telepítés/Save/frissítés művelet során egy függő modul licencre van szüksége, és a licencfeltételek elfogadását nem történik meg, ha a művelet meghiúsul, és kövesse a normál folyamatok a csomag telepítése/save/frissítése nem sikerült.

## <a name="impact-on--force"></a>A - Force gyakorolt hatás

Adjon meg `–Force` nem elegendő az, hogy fogadja el a licencet. `–AcceptLicense` engedély telepítéséhez szükség. Ha `–Force` van megadva, RequiredLicenseAcceptance értéke igaz, és `–AcceptLicense` nincs megadva, a művelet sikertelen lesz.

## <a name="examples"></a>EXAMPLES

### <a name="example-1-update-module-manifest-to-require-license-acceptance"></a>1. példa: Licencfeltételek elfogadásának kérése az Alkalmazásjegyzéket az modul frissítése

```powershell
Update-ModuleManifest -Path C:\modulemanifest.psd1 -RequireLicenseAcceptance -PrivateData @{
    PSData = @{
        # Flag to indicate whether the module requires explicit user acceptance
        RequireLicenseAcceptance = $true
    } # End of PSData hashtable

 } # End of PrivateData hashtable
```

Ez a parancs frissíti a jegyzékfájlt, és a RequireLicenseAcceptance jelzőt igaz értékre állítja.

### <a name="example-2-install-module-requiring-license-acceptance"></a>2. példa: Licencfeltételek elfogadását igénylő modul telepítése

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

Ez a parancs megjeleníti a licenc license.txt fájlból, és kéri a felhasználót, fogadja el a licencfeltételeket.

### <a name="example-3-install-module-requiring-license-acceptance-with--acceptlicense"></a>3. példa: A - AcceptLicense licencfeltételek elfogadását igénylő modul telepítése

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

A modul telepítve van minden licenc elfogadására kérése nélkül.

### <a name="example-4-install-module-requiring-license-acceptance-with--force"></a>4. példa: A - Force licencfeltételek elfogadását igénylő modul telepítése

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

### <a name="example-5-install-module-with-dependencies-requiring-license-acceptance"></a>5. példa: Licencfeltételek elfogadását igénylő függőségekkel modul telepítése

A modul "ModuleWithDependency" modul "ModuleRequireLicenseAcceptance" függ. Licenc fogadja el a rendszer kéri.

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

### <a name="example-6-install-module-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>6. példa: Licencfeltételek elfogadásának és - AcceptLicense függőségekkel modul telepítése

A modul "ModuleWithDependency" modul "ModuleRequireLicenseAcceptance" függ. Fogadja el a licenc - AcceptLicense van megadva, az nem kéri a felhasználótól.

```powershell
Install-Module -Name ModuleWithDependency -AcceptLicense
```

### <a name="example-7-install-module-requiring-license-acceptance-on-a-client-older-than-psgetformatversion-20"></a>7. példa: A régebbi, mint PSGetFormatVersion 2.0-s ügyfél licencfeltételek elfogadását igénylő modul telepítése

```powershell
Install-Module -Name ModuleRequireLicenseAcceptance
```

```output
WARNING: The specified module 'ModuleRequireLicenseAcceptance' with PowerShellGetFormatVersion '2.0' is not supported by the current version of PowerShellGet. Get the latest version of the PowerShellGet module to install this module, 'ModuleRequireLicenseAcceptance'.
```

### <a name="example-8-save-module-requiring-license-acceptance"></a>8. példa: Licencfeltételek elfogadását igénylő modul mentése

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

Ez a parancs megjeleníti a licenc license.txt fájlból, és kéri a felhasználót, fogadja el a licencfeltételeket.

### <a name="example-9-save-module-requiring-license-acceptance-with--acceptlicense"></a>9. példa: A modul - AcceptLicense a licencfeltételek elfogadását igénylő mentése

```powershell
Save-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense -Path C:\Saved
```

A modul a rendszer minden licenc elfogadására kérdés nélkül menti.

### <a name="example-10-update-module-requiring-license-acceptance"></a>10. példa: Licencfeltételek elfogadását igénylő modulok frissítésére

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

Ez a parancs megjeleníti a licenc license.txt fájlból, és kéri a felhasználót, fogadja el a licencfeltételeket.

### <a name="example-11-update-module-requiring-license-acceptance-with--acceptlicense"></a>11. példa: A - AcceptLicense licencfeltételek elfogadását igénylő modulok frissítésére

```powershell
Update-Module -Name ModuleRequireLicenseAcceptance -AcceptLicense
```

A modul frissül minden licenc elfogadására kérése nélkül.

## <a name="more-details"></a>További részletek

[Licencfeltételek elfogadásának megkövetelése a parancsfájlokhoz](./script-license-acceptance.md)

[A PowerShell-Galériabeli licencfeltételek elfogadását támogatásra van szüksége](../how-to/working-with-packages/packages-that-require-license-acceptance.md)

[Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez](../how-to/working-with-packages/deploy-to-azure-automation.md)
