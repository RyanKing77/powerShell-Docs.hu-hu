---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: Üzembe helyezés az Azure Automation szolgáltatásban
ms.openlocfilehash: dc382b1cf3ceaa787f54c555d01e6bd9ba70e680
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084900"
---
# <a name="deploy-to-azure-automation"></a><span data-ttu-id="fcc51-103">Üzembe helyezés az Azure Automation szolgáltatásban</span><span class="sxs-lookup"><span data-stu-id="fcc51-103">Deploy to Azure Automation</span></span>

<span data-ttu-id="fcc51-104">Üzembe helyezés az Azure Automation gombra a csomag részletei lapon fog üzembe helyezni az Azure Automation PowerShell-galériából történő csomagot.</span><span class="sxs-lookup"><span data-stu-id="fcc51-104">The Deploy to Azure Automation button on the package details page will deploy the package from the PowerShell Gallery to Azure Automation.</span></span>

![Helyezze üzembe az Azure Automation gomb](../../Images/DeployToAzureAutomationButton.png)

<span data-ttu-id="fcc51-106">Amikor kattint, átirányítja az Azure felügyeleti portálon, ha bejelentkezik az Azure-fiókja hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="fcc51-106">When clicked, it will redirect you to the Azure Management Portal, where you sign in using your Azure account credentials.</span></span>
<span data-ttu-id="fcc51-107">Ha a csomag tartalmazza a függőségeket, összes függőséget telepíti az Azure Automationhöz is.</span><span class="sxs-lookup"><span data-stu-id="fcc51-107">If the package includes dependencies, all the dependencies will be deployed to Azure Automation as well.</span></span>

> [!WARNING]
> <span data-ttu-id="fcc51-108">Ha csomag és a verzió az Automation-fiók már létezik, ismét üzembe helyezné a PowerShell-galériából, azzal felülírja a csomag az Automation-fiókban.</span><span class="sxs-lookup"><span data-stu-id="fcc51-108">If the same package and version already exist in your Automation account, deploying it again from the PowerShell Gallery will overwrite the package in your Automation account.</span></span>

<span data-ttu-id="fcc51-109">Ha egy modul telepít, meg fog jelenni az Azure Automation modulok szakaszában.</span><span class="sxs-lookup"><span data-stu-id="fcc51-109">If you deploy a module, it will appear in the Modules section of Azure Automation.</span></span>  <span data-ttu-id="fcc51-110">Ha a parancsfájl telepíti, meg fog jelenni az Azure Automation Runbookok szakaszában.</span><span class="sxs-lookup"><span data-stu-id="fcc51-110">If you deploy a script, it will appear in the Runbooks section of Azure Automation.</span></span>

<span data-ttu-id="fcc51-111">Üzembe helyezés az Azure Automation gomb a AzureAutomationNotSupported címkét ad hozzá a metaadatcsomagok letiltható.</span><span class="sxs-lookup"><span data-stu-id="fcc51-111">The Deploy to Azure Automation button can be disabled by adding the AzureAutomationNotSupported tag to the package metadata.</span></span>

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a><span data-ttu-id="fcc51-112">Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez</span><span class="sxs-lookup"><span data-stu-id="fcc51-112">Require License Acceptance on Deploy to Azure Automation</span></span>

<span data-ttu-id="fcc51-113">Ha a modul helyezésüket az Azure Automation licencfeltételek elfogadását igényli, a portál felhasználói Felületét jeleníti meg a egy jogi nyilatkozat üzenettel "Ez a modul licencfeltételek elfogadását igényli.</span><span class="sxs-lookup"><span data-stu-id="fcc51-113">If the module being deployed to Azure Automation requires license acceptance, portal UI will show a disclaimer saying 'This module requires license acceptance.</span></span> <span data-ttu-id="fcc51-114">Az OK gombra kattintva elfogadja licencfeltételeket. "</span><span class="sxs-lookup"><span data-stu-id="fcc51-114">By clicking OK, you are accepting license terms.'</span></span>

![Helyezze üzembe az Azure Automation licencfeltételek elfogadását igényli](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a><span data-ttu-id="fcc51-116">További részletek</span><span class="sxs-lookup"><span data-stu-id="fcc51-116">More details</span></span>

- [<span data-ttu-id="fcc51-117">A PowerShellGet licencfeltételek elfogadásának megkövetelése</span><span class="sxs-lookup"><span data-stu-id="fcc51-117">Require License Acceptance in PowerShellGet</span></span>](../../concepts/module-license-acceptance.md)
- [<span data-ttu-id="fcc51-118">A PowerShell-galériában licencfeltételek elfogadásának megkövetelése</span><span class="sxs-lookup"><span data-stu-id="fcc51-118">Require License Acceptance in PowerShell Gallery</span></span>](packages-that-require-license-acceptance.md)
- [<span data-ttu-id="fcc51-119">Azure Automation-webhelyen</span><span class="sxs-lookup"><span data-stu-id="fcc51-119">Azure Automation website</span></span>](http://azure.microsoft.com/services/automation/)
