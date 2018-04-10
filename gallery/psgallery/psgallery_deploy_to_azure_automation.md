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
<a name="deploy-to-azure-automation"></a><span data-ttu-id="7758f-103">Üzembe helyezés az Azure Automation szolgáltatásban</span><span class="sxs-lookup"><span data-stu-id="7758f-103">Deploy to Azure Automation</span></span>
===========================

<span data-ttu-id="7758f-104">Azure Automation gomb elem részleteit megjelenítő oldalon a telepítés telepíti az Azure Automation a PowerShell-galériából elemet.</span><span class="sxs-lookup"><span data-stu-id="7758f-104">The Deploy to Azure Automation button on the item details page will deploy the item from the PowerShell Gallery to Azure Automation.</span></span>

![Telepítse az Azure Automation gomb](Images/DeployToAzureAutomationButton.png)

<span data-ttu-id="7758f-106">Amikor a felhasználó kattint, átirányítja az Azure felügyeleti portálra, ahol bejelentkezik az Azure-fiók hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="7758f-106">When clicked, it will redirect you to the Azure Management Portal, where you sign in using your Azure account credentials.</span></span>
<span data-ttu-id="7758f-107">Ha a cikk függőségeket tartalmaz, a függőségek telepíti az Azure Automation is.</span><span class="sxs-lookup"><span data-stu-id="7758f-107">If the item includes dependencies, all the dependencies will be deployed to Azure Automation as well.</span></span>

<span data-ttu-id="7758f-108">Figyelmeztetés: Ha elem és a verzió már szerepel az Automation-fiók, a PowerShell-galériából újra telepítése felülírja az elemet az Automation-fiókban.</span><span class="sxs-lookup"><span data-stu-id="7758f-108">WARNING:  If the same item and version already exist in your Automation account, deploying it again from the PowerShell Gallery will overwrite the item in your Automation account.</span></span>

<span data-ttu-id="7758f-109">Ha egy modult telepít, akkor jelenik meg az Azure Automation modulok szakaszában.</span><span class="sxs-lookup"><span data-stu-id="7758f-109">If you deploy a module, it will appear in the Modules section of Azure Automation.</span></span>  <span data-ttu-id="7758f-110">Ha egy parancsfájlt, megjelenik az Azure Automation Runbookjai szakasza.</span><span class="sxs-lookup"><span data-stu-id="7758f-110">If you deploy a script, it will appear in the Runbooks section of Azure Automation.</span></span>

<span data-ttu-id="7758f-111">Azure Automation gombra a telepítés az elem metaadatok AzureAutomationNotSupported címke hozzáadásával lehet letiltani.</span><span class="sxs-lookup"><span data-stu-id="7758f-111">The Deploy to Azure Automation button can be disabled by adding the AzureAutomationNotSupported tag to the item metadata.</span></span>

<span data-ttu-id="7758f-112">Azure Automation kapcsolatos további tudnivalókért tekintse meg az Azure Automation-webhely [Azure Automation-webhely](http://azure.microsoft.com/services/automation/).</span><span class="sxs-lookup"><span data-stu-id="7758f-112">To learn more about Azure Automation, see the Azure Automation website [Azure Automation website](http://azure.microsoft.com/services/automation/).</span></span>