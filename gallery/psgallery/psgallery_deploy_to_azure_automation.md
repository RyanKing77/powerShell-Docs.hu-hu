---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, a powershell, a parancsmag, a psgallery"
title: psgallery_deploy_to_azure_automation
ms.openlocfilehash: 91f48fb43d7fb099e34ce5d3b3b632e3cb119d64
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
<a name="deploy-to-azure-automation"></a><span data-ttu-id="778f0-103">Azure Automation szolgáltatásbeli telepítése</span><span class="sxs-lookup"><span data-stu-id="778f0-103">Deploy to Azure Automation</span></span>
===========================

<span data-ttu-id="778f0-104">Azure Automation gomb elem részleteit megjelenítő oldalon a telepítés telepíti az Azure Automation a PowerShell-galériából elemet.</span><span class="sxs-lookup"><span data-stu-id="778f0-104">The Deploy to Azure Automation button on the item details page will deploy the item from the PowerShell Gallery to Azure Automation.</span></span>

![Telepítse az Azure Automation gomb](Images/DeployToAzureAutomationButton.png)

<span data-ttu-id="778f0-106">Amikor a felhasználó kattint, átirányítja az Azure felügyeleti portálra, ahol bejelentkezik az Azure-fiók hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="778f0-106">When clicked, it will redirect you to the Azure Management Portal, where you sign in using your Azure account credentials.</span></span>
<span data-ttu-id="778f0-107">Ha a cikk függőségeket tartalmaz, a függőségek telepíti az Azure Automation is.</span><span class="sxs-lookup"><span data-stu-id="778f0-107">If the item includes dependencies, all the dependencies will be deployed to Azure Automation as well.</span></span>

<span data-ttu-id="778f0-108">Figyelmeztetés: Ha elem és a verzió már szerepel az Automation-fiók, a PowerShell-galériából újra telepítése felülírja az elemet az Automation-fiókban.</span><span class="sxs-lookup"><span data-stu-id="778f0-108">WARNING:  If the same item and version already exist in your Automation account, deploying it again from the PowerShell Gallery will overwrite the item in your Automation account.</span></span>

<span data-ttu-id="778f0-109">Ha egy modult telepít, akkor jelenik meg az Azure Automation modulok szakaszában.</span><span class="sxs-lookup"><span data-stu-id="778f0-109">If you deploy a module, it will appear in the Modules section of Azure Automation.</span></span>  <span data-ttu-id="778f0-110">Ha egy parancsfájlt, megjelenik az Azure Automation Runbookjai szakasza.</span><span class="sxs-lookup"><span data-stu-id="778f0-110">If you deploy a script, it will appear in the Runbooks section of Azure Automation.</span></span>

<span data-ttu-id="778f0-111">Azure Automation gombra a telepítés az elem metaadatok AzureAutomationNotSupported címke hozzáadásával lehet letiltani.</span><span class="sxs-lookup"><span data-stu-id="778f0-111">The Deploy to Azure Automation button can be disabled by adding the AzureAutomationNotSupported tag to the item metadata.</span></span>

<span data-ttu-id="778f0-112">Azure Automation kapcsolatos további tudnivalókért tekintse meg az Azure Automation-webhely [Azure Automation-webhely](http://azure.microsoft.com/en-us/services/automation/).</span><span class="sxs-lookup"><span data-stu-id="778f0-112">To learn more about Azure Automation, see the Azure Automation website [Azure Automation website](http://azure.microsoft.com/en-us/services/automation/).</span></span>

