---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: psgallery_deploy_to_azure_automation
ms.openlocfilehash: 8da4eabead6a419dc0c01c74335c06bf8be25d0c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
<a name="deploy-to-azure-automation"></a>Üzembe helyezés az Azure Automation szolgáltatásban
===========================

Azure Automation gomb elem részleteit megjelenítő oldalon a telepítés telepíti az Azure Automation a PowerShell-galériából elemet.

![Telepítse az Azure Automation gomb](Images/DeployToAzureAutomationButton.png)

Amikor a felhasználó kattint, átirányítja az Azure felügyeleti portálra, ahol bejelentkezik az Azure-fiók hitelesítő adataival.
Ha a cikk függőségeket tartalmaz, a függőségek telepíti az Azure Automation is.

Figyelmeztetés: Ha elem és a verzió már szerepel az Automation-fiók, a PowerShell-galériából újra telepítése felülírja az elemet az Automation-fiókban.

Ha egy modult telepít, akkor jelenik meg az Azure Automation modulok szakaszában.  Ha egy parancsfájlt, megjelenik az Azure Automation Runbookjai szakasza.

Azure Automation gombra a telepítés az elem metaadatok AzureAutomationNotSupported címke hozzáadásával lehet letiltani.

Azure Automation kapcsolatos további tudnivalókért tekintse meg az Azure Automation-webhely [Azure Automation-webhely](http://azure.microsoft.com/services/automation/).