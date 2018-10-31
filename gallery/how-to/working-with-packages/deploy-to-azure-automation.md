---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Üzembe helyezés az Azure Automation szolgáltatásban
ms.openlocfilehash: dc382b1cf3ceaa787f54c555d01e6bd9ba70e680
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004074"
---
# <a name="deploy-to-azure-automation"></a>Üzembe helyezés az Azure Automation szolgáltatásban

Üzembe helyezés az Azure Automation gombra a csomag részletei lapon fog üzembe helyezni az Azure Automation PowerShell-galériából történő csomagot.

![Helyezze üzembe az Azure Automation gomb](../../Images/DeployToAzureAutomationButton.png)

Amikor kattint, átirányítja az Azure felügyeleti portálon, ha bejelentkezik az Azure-fiókja hitelesítő adataival.
Ha a csomag tartalmazza a függőségeket, összes függőséget telepíti az Azure Automationhöz is.

> [!WARNING]
> Ha csomag és a verzió az Automation-fiók már létezik, ismét üzembe helyezné a PowerShell-galériából, azzal felülírja a csomag az Automation-fiókban.

Ha egy modul telepít, meg fog jelenni az Azure Automation modulok szakaszában.  Ha a parancsfájl telepíti, meg fog jelenni az Azure Automation Runbookok szakaszában.

Üzembe helyezés az Azure Automation gomb a AzureAutomationNotSupported címkét ad hozzá a metaadatcsomagok letiltható.

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a>Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez

Ha a modul helyezésüket az Azure Automation licencfeltételek elfogadását igényli, a portál felhasználói Felületét jeleníti meg a egy jogi nyilatkozat üzenettel "Ez a modul licencfeltételek elfogadását igényli. Az OK gombra kattintva elfogadja licencfeltételeket. "

![Helyezze üzembe az Azure Automation licencfeltételek elfogadását igényli](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a>További részletek

- [A PowerShellGet licencfeltételek elfogadásának megkövetelése](../../concepts/module-license-acceptance.md)
- [A PowerShell-galériában licencfeltételek elfogadásának megkövetelése](packages-that-require-license-acceptance.md)
- [Azure Automation-webhelyen](http://azure.microsoft.com/services/automation/)
