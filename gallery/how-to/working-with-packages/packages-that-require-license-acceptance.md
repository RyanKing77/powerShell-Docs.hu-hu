---
ms.date: 06/12/2017
contributor: Farehar
keywords: katalógus, a powershell, a psgallery
title: Licencfeltételek elfogadásának megkövetelése
ms.openlocfilehash: eaed248895d14bd455d2d8d3c2222d8848eeccae
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004086"
---
# <a name="require-license-acceptance"></a><span data-ttu-id="4185a-103">Licencfeltételek elfogadásának megkövetelése</span><span class="sxs-lookup"><span data-stu-id="4185a-103">Require license acceptance</span></span>

<span data-ttu-id="4185a-104">Szükséges a licencfeltételek elfogadását szöveg megjelenik-e a licencfeltételek elfogadását igénylő modulok elem részleteit megjelenítő oldalon.</span><span class="sxs-lookup"><span data-stu-id="4185a-104">Require License Acceptance text shows up on item details page for modules that require license acceptance.</span></span> <span data-ttu-id="4185a-105">Licenc modul "Nézet License.txt" hivatkozásra kattintva tekinthet meg.</span><span class="sxs-lookup"><span data-stu-id="4185a-105">License for module can be viewed by clicking on 'View License.txt' link.</span></span>

![Licencfeltételek elfogadásának megkövetelése](../../Images/RequireLicenseAcceptance.png)

<span data-ttu-id="4185a-107">Telepítésekor, mentés vagy a modul a PowerShellGet vagy frissítése az Azure Automationhöz üzembe helyezésekor elfogadásához kéri a felhasználótól.</span><span class="sxs-lookup"><span data-stu-id="4185a-107">Users will be prompted to accept the license when installing, saving or updating the module through PowerShellGet or when deploying to Azure Automation.</span></span>

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a><span data-ttu-id="4185a-108">Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez</span><span class="sxs-lookup"><span data-stu-id="4185a-108">Require License Acceptance on Deploy to Azure Automation</span></span>

<span data-ttu-id="4185a-109">Ha a modul helyezésüket az Azure Automation licencfeltételek elfogadását igényli, a portál felhasználói Felületét jeleníti meg a egy jogi nyilatkozat üzenettel "Ez a modul licencfeltételek elfogadását igényli.</span><span class="sxs-lookup"><span data-stu-id="4185a-109">If the module being deployed to Azure Automation requires license acceptance, portal UI will show a disclaimer saying 'This module requires license acceptance.</span></span> <span data-ttu-id="4185a-110">Az OK gombra kattintva elfogadja licencfeltételeket. "</span><span class="sxs-lookup"><span data-stu-id="4185a-110">By clicking OK, you are accepting license terms.'</span></span>

![Helyezze üzembe az Azure Automation licencfeltételek elfogadását igényli](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a><span data-ttu-id="4185a-112">További részletek</span><span class="sxs-lookup"><span data-stu-id="4185a-112">More details</span></span>

<span data-ttu-id="4185a-113">[A PowerShellGet licencfeltételek elfogadásának kérése az](../../concepts/module-license-acceptance.md)
[Azure Automation-webhely](/azure/automation)</span><span class="sxs-lookup"><span data-stu-id="4185a-113">[Require License Acceptance in PowerShellGet](../../concepts/module-license-acceptance.md)
[Azure Automation website](/azure/automation)</span></span>
