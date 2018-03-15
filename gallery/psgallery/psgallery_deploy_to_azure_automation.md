---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, a powershell, a parancsmag, a psgallery"
title: psgallery_deploy_to_azure_automation
ms.openlocfilehash: 223acbcc2f6cd4f15e1ee55d3f2f68df851cd902
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
<a name="deploy-to-azure-automation"></a>Azure Automation szolgáltatásbeli telepítése
===========================

Azure Automation gomb elem részleteit megjelenítő oldalon a telepítés telepíti az Azure Automation a PowerShell-galériából elemet.

![Telepítse az Azure Automation gomb](Images/DeployToAzureAutomationButton.png)

Amikor a felhasználó kattint, átirányítja az Azure felügyeleti portálra, ahol bejelentkezik az Azure-fiók hitelesítő adataival.
Ha a cikk függőségeket tartalmaz, a függőségek telepíti az Azure Automation is.

Figyelmeztetés: Ha elem és a verzió már szerepel az Automation-fiók, a PowerShell-galériából újra telepítése felülírja az elemet az Automation-fiókban.

Ha egy modult telepít, akkor jelenik meg az Azure Automation modulok szakaszában.  Ha egy parancsfájlt, megjelenik az Azure Automation Runbookjai szakasza.

Azure Automation gombra a telepítés az elem metaadatok AzureAutomationNotSupported címke hozzáadásával lehet letiltani.

Azure Automation kapcsolatos további tudnivalókért tekintse meg az Azure Automation-webhely [Azure Automation-webhely](http://azure.microsoft.com/services/automation/).

