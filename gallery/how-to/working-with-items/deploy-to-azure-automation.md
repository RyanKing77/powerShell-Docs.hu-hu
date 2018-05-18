---
ms.date: 06/12/2017
contributor: JKeithB
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: Üzembe helyezés az Azure Automation szolgáltatásban
ms.openlocfilehash: ced67809387a85e089259edf6b091d68e58ba6a7
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="deploy-to-azure-automation"></a><span data-ttu-id="66146-103">Üzembe helyezés az Azure Automation szolgáltatásban</span><span class="sxs-lookup"><span data-stu-id="66146-103">Deploy to Azure Automation</span></span>

<span data-ttu-id="66146-104">Azure Automation gomb elem részleteit megjelenítő oldalon a telepítés telepíti az Azure Automation a PowerShell-galériából elemet.</span><span class="sxs-lookup"><span data-stu-id="66146-104">The Deploy to Azure Automation button on the item details page will deploy the item from the PowerShell Gallery to Azure Automation.</span></span>

![Telepítse az Azure Automation gomb](../../Images/DeployToAzureAutomationButton.png)

<span data-ttu-id="66146-106">Amikor a felhasználó kattint, átirányítja az Azure felügyeleti portálra, ahol bejelentkezik az Azure-fiók hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="66146-106">When clicked, it will redirect you to the Azure Management Portal, where you sign in using your Azure account credentials.</span></span>
<span data-ttu-id="66146-107">Ha a cikk függőségeket tartalmaz, a függőségek telepíti az Azure Automation is.</span><span class="sxs-lookup"><span data-stu-id="66146-107">If the item includes dependencies, all the dependencies will be deployed to Azure Automation as well.</span></span>

> [!WARNING]
> <span data-ttu-id="66146-108">Elem és a verzió már szerepel az Automation-fiók, ha telepítené újra a PowerShell-galériából felülírja az elemet az Automation-fiókban.</span><span class="sxs-lookup"><span data-stu-id="66146-108">If the same item and version already exist in your Automation account, deploying it again from the PowerShell Gallery will overwrite the item in your Automation account.</span></span>

<span data-ttu-id="66146-109">Ha egy modult telepít, akkor jelenik meg az Azure Automation modulok szakaszában.</span><span class="sxs-lookup"><span data-stu-id="66146-109">If you deploy a module, it will appear in the Modules section of Azure Automation.</span></span>  <span data-ttu-id="66146-110">Ha egy parancsfájlt, megjelenik az Azure Automation Runbookjai szakasza.</span><span class="sxs-lookup"><span data-stu-id="66146-110">If you deploy a script, it will appear in the Runbooks section of Azure Automation.</span></span>

<span data-ttu-id="66146-111">Azure Automation gombra a telepítés az elem metaadatok AzureAutomationNotSupported címke hozzáadásával lehet letiltani.</span><span class="sxs-lookup"><span data-stu-id="66146-111">The Deploy to Azure Automation button can be disabled by adding the AzureAutomationNotSupported tag to the item metadata.</span></span>

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a><span data-ttu-id="66146-112">Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez</span><span class="sxs-lookup"><span data-stu-id="66146-112">Require License Acceptance on Deploy to Azure Automation</span></span>

<span data-ttu-id="66146-113">Ha az Azure Automation telepített modul licencszerződés elfogadását igényli, portál felhasználói felületének jelennek meg a jogi nyilatkozat bármelyiket "Ez a modul licencszerződés elfogadását igényli.</span><span class="sxs-lookup"><span data-stu-id="66146-113">If the module being deployed to Azure Automation requires license acceptance, portal UI will show a disclaimer saying 'This module requires license acceptance.</span></span> <span data-ttu-id="66146-114">Az OK gombra kattintva elfogadja licencfeltételek. "</span><span class="sxs-lookup"><span data-stu-id="66146-114">By clicking OK, you are accepting license terms.'</span></span>

![Telepítse az Azure Automation licencszerződés elfogadását igényli](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a><span data-ttu-id="66146-116">További részletekért</span><span class="sxs-lookup"><span data-stu-id="66146-116">More details</span></span>

- [<span data-ttu-id="66146-117">A PowerShellGet licencszerződés elfogadására van szükség</span><span class="sxs-lookup"><span data-stu-id="66146-117">Require License Acceptance in PowerShellGet</span></span>](../../concepts/module-license-acceptance.md)
- [<span data-ttu-id="66146-118">A PowerShell-galériában licencszerződés elfogadására van szükség</span><span class="sxs-lookup"><span data-stu-id="66146-118">Require License Acceptance in PowerShell Gallery</span></span>](items-that-require-license-acceptance.md)
- [<span data-ttu-id="66146-119">Azure Automation-webhelyen</span><span class="sxs-lookup"><span data-stu-id="66146-119">Azure Automation website</span></span>](http://azure.microsoft.com/services/automation/)
