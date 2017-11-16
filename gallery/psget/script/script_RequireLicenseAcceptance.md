---
ms.date: 2017-06-09
schema: 2.0.0
keywords: PowerShell
title: RequireLicenseAcceptanceScript
ms.openlocfilehash: 7092fb2e63b9e2b1eca59cd418317631bff8b172
ms.sourcegitcommit: cd66d4f49ea762a31887af2c72d087b219ddbe10
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/11/2017
---
# <a name="requiring-license-acceptance-for-scripts"></a>Licenc elfogadása igénylő parancsfájlok

Licenc elfogadása parancsfájlok nem támogatott. Azonban a forgatókönyvet, ahol egy parancsfájl attól függ, a modul, amely licencszerződés elfogadását igényli támogatott.

Parancsfájl commands(Install-Script/Save-Script/Update-Script) támogatja az új paramétert, amely úgy viselkedik, mintha a felhasználói látta a licenc - AcceptLicense. Ha nincs megadva a - AcceptLicense; a felhasználó kéri, hogy elfogadja a licencfeltételeket és a függő modul license.txt megjelenítendő.

## <a name="examples"></a>PÉLDÁK

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a>1. példa: Telepítési parancsfájl licenc elfogadása igénylő függőségekkel rendelkező
Parancsfájl "ScriptRequireLicenseAcceptance" modul "ModuleRequireLicenseAcceptance" függ. Licenc elfogadása felhasználótól.
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance

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

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>2. példa: Telepítési parancsfájl licenc elfogadása és - AcceptLicense függőségekkel rendelkező
Parancsfájl "ScriptRequireLicenseAcceptance" modul "ModuleRequireLicenseAcceptance" függ. Nem felhasználótól fogadnia a licencfeltételeket, mert - AcceptLicense sincs megadva.
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a>További részletekért
### <a name="require-license-acceptance-support-for-modulesmodulerequirelicenseacceptancemd"></a>[Licenc elfogadása támogatásra van szüksége a modulok](../module/RequireLicenseAcceptance.md)

### <a name="require-license-acceptance-support-on-powershellgallerypsgallerypsgalleryrequireslicenseacceptancemd"></a>[A PowerShellGallery licenc elfogadása támogatásra van szüksége](../../psgallery/psgallery_requires_license_acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationpsgallerypsgallerydeploytoazureautomationrequirelicenseacceptancemd"></a>[Licenc elfogadására van szükség az Azure Automation szolgáltatásbeli központi telepítése](../../psgallery/psgallery_deploy_to_azure_automation_requireLicenseAcceptance.md)
