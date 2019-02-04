---
ms.date: 06/12/2017
contributor: Farehar
keywords: katalógus, a powershell, a psgallery
title: Licencfeltételek elfogadásának megkövetelése
ms.openlocfilehash: eaed248895d14bd455d2d8d3c2222d8848eeccae
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684135"
---
# <a name="require-license-acceptance"></a><span data-ttu-id="22964-103">Licencfeltételek elfogadásának megkövetelése</span><span class="sxs-lookup"><span data-stu-id="22964-103">Require license acceptance</span></span>

<span data-ttu-id="22964-104">Szükséges a licencfeltételek elfogadását szöveg megjelenik-e a licencfeltételek elfogadását igénylő modulok elem részleteit megjelenítő oldalon.</span><span class="sxs-lookup"><span data-stu-id="22964-104">Require License Acceptance text shows up on item details page for modules that require license acceptance.</span></span> <span data-ttu-id="22964-105">Licenc modul "Nézet License.txt" hivatkozásra kattintva tekinthet meg.</span><span class="sxs-lookup"><span data-stu-id="22964-105">License for module can be viewed by clicking on 'View License.txt' link.</span></span>

![Require License Acceptance](../../Images/RequireLicenseAcceptance.png)

<span data-ttu-id="22964-107">Telepítésekor, mentés vagy a modul a PowerShellGet vagy frissítése az Azure Automationhöz üzembe helyezésekor elfogadásához kéri a felhasználótól.</span><span class="sxs-lookup"><span data-stu-id="22964-107">Users will be prompted to accept the license when installing, saving or updating the module through PowerShellGet or when deploying to Azure Automation.</span></span>

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a><span data-ttu-id="22964-108">Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez</span><span class="sxs-lookup"><span data-stu-id="22964-108">Require License Acceptance on Deploy to Azure Automation</span></span>

<span data-ttu-id="22964-109">Ha a modul helyezésüket az Azure Automation licencfeltételek elfogadását igényli, a portál felhasználói Felületét jeleníti meg a egy jogi nyilatkozat üzenettel "Ez a modul licencfeltételek elfogadását igényli.</span><span class="sxs-lookup"><span data-stu-id="22964-109">If the module being deployed to Azure Automation requires license acceptance, portal UI will show a disclaimer saying 'This module requires license acceptance.</span></span> <span data-ttu-id="22964-110">Az OK gombra kattintva elfogadja licencfeltételeket. "</span><span class="sxs-lookup"><span data-stu-id="22964-110">By clicking OK, you are accepting license terms.'</span></span>

![Helyezze üzembe az Azure Automation licencfeltételek elfogadását igényli](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a><span data-ttu-id="22964-112">További részletek</span><span class="sxs-lookup"><span data-stu-id="22964-112">More details</span></span>

<span data-ttu-id="22964-113">[A PowerShellGet licencfeltételek elfogadásának kérése az](../../concepts/module-license-acceptance.md)
[Azure Automation-webhely](/azure/automation)</span><span class="sxs-lookup"><span data-stu-id="22964-113">[Require License Acceptance in PowerShellGet](../../concepts/module-license-acceptance.md)
[Azure Automation website](/azure/automation)</span></span>
