---
ms.date: 06/09/2017
schema: 2.0.0
keywords: PowerShell
title: Licenc elfogadása igénylő parancsfájlok
ms.openlocfilehash: 6374c8c8536dd0c8f27580a5b8895b8db18424f9
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="requiring-license-acceptance-for-scripts"></a>Licenc elfogadása igénylő parancsfájlok

Licenc elfogadása parancsfájlok nem támogatott. Azonban a forgatókönyvet, ahol egy parancsfájl attól függ, a modul, amely licencszerződés elfogadását igényli támogatott.

Parancsfájl commands(Install-Script/Save-Script/Update-Script) támogatja az új paramétert, amely úgy viselkedik, mintha a felhasználói látta a licenc - AcceptLicense. Ha nincs megadva a - AcceptLicense; a felhasználó kéri, hogy elfogadja a licencfeltételeket és a függő modul license.txt megjelenítendő.

## <a name="examples"></a>PÉLDÁK

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a>1. példa: Telepítési parancsfájl licenc elfogadása igénylő függőségekkel rendelkező

Parancsfájl "ScriptRequireLicenseAcceptance" modul "ModuleRequireLicenseAcceptance" függ. Licenc elfogadása felhasználótól.

```PowerShell
PS> Install-Script -Name ScriptRequireLicenseAcceptance

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
PS> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a>További részletekért

- [Licenc elfogadása támogatásra van szüksége a modulok](module-license-acceptance.md)
- [A PowerShellGallery licenc elfogadása támogatásra van szüksége](../how-to/working-with-items/items-that-require-license-acceptance.md)
- [Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez](../how-to/working-with-items/deploy-to-azure-automation.md)