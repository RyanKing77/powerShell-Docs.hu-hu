---
ms.date: 06/09/2017
schema: 2.0.0
keywords: PowerShell
title: Licencfeltételek elfogadását igénylő parancsprogramok
ms.openlocfilehash: e7101eb6a480dd87965b7b9be9d49583042b603f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084674"
---
# <a name="requiring-license-acceptance-for-scripts"></a>Licencfeltételek elfogadását igénylő parancsprogramok

Licencfeltételek elfogadásának parancsfájlok nem támogatott. Azonban a forgatókönyvet, ahol a parancsfájl attól függ, a licencfeltételek elfogadását igénylő moduljára támogatott.

Parancsfájl commands(Install-Script/Save-Script/Update-Script) támogatásához új paraméter, amely viselkedik, mintha a felhasználó látott a licenc - AcceptLicense. Ha nincs megadva - AcceptLicense; a felhasználó a licenc elfogadására kéri a rendszer és a függő modul license.txt megjelenítendő.

## <a name="examples"></a>EXAMPLES

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a>1. példa: Licencfeltételek elfogadását igénylő függőségekkel parancsfájl telepítése

Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'. Licenc fogadja el a rendszer kéri.

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

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a>2. példa: Licencfeltételek elfogadásának és - AcceptLicense függőségekkel parancsfájl telepítése

Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'. Fogadja el a licenc - AcceptLicense van megadva, az nem kéri a felhasználótól.

```PowerShell
PS> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a>További részletek

- [Licencfeltételek elfogadásának támogatást igénylő modulok](module-license-acceptance.md)
- [A PowerShell-Galériabeli licencfeltételek elfogadását támogatásra van szüksége](../how-to/working-with-packages/packages-that-require-license-acceptance.md)
- [Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez](../how-to/working-with-packages/deploy-to-azure-automation.md)
