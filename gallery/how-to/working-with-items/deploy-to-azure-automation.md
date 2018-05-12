---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: Üzembe helyezés az Azure Automation szolgáltatásban
ms.openlocfilehash: 1efdc289228d3a6962302d12ccf44143ce63a806
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="deploy-to-azure-automation"></a>Üzembe helyezés az Azure Automation szolgáltatásban

Azure Automation gomb elem részleteit megjelenítő oldalon a telepítés telepíti az Azure Automation a PowerShell-galériából elemet.

![Telepítse az Azure Automation gomb](../../Images/DeployToAzureAutomationButton.png)

Amikor a felhasználó kattint, átirányítja az Azure felügyeleti portálra, ahol bejelentkezik az Azure-fiók hitelesítő adataival.
Ha a cikk függőségeket tartalmaz, a függőségek telepíti az Azure Automation is.

> [!WARNING]
> Elem és a verzió már szerepel az Automation-fiók, ha telepítené újra a PowerShell-galériából felülírja az elemet az Automation-fiókban.

Ha egy modult telepít, akkor jelenik meg az Azure Automation modulok szakaszában.  Ha egy parancsfájlt, megjelenik az Azure Automation Runbookjai szakasza.

Azure Automation gombra a telepítés az elem metaadatok AzureAutomationNotSupported címke hozzáadásával lehet letiltani.

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a>Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez

Ha az Azure Automation telepített modul licencszerződés elfogadását igényli, portál felhasználói felületének jelennek meg a jogi nyilatkozat bármelyiket "Ez a modul licencszerződés elfogadását igényli. Az OK gombra kattintva elfogadja licencfeltételek. "

![Telepítse az Azure Automation licencszerződés elfogadását igényli](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a>További részletekért

- [A PowerShellGet licencszerződés elfogadására van szükség](../../concepts/module-license-acceptance.md)
- [A PowerShell-galériában licencszerződés elfogadására van szükség](items-that-require-license-acceptance.md)
- [Azure Automation-webhelyen](http://azure.microsoft.com/services/automation/)
