---
ms.date: 06/12/2017
contributor: Farehar
keywords: gyűjtemény, powershell, psgallery
title: Licenc elfogadására van szükség
ms.openlocfilehash: 69787cdb12aa47223072551c9b68fc046573f022
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="require-license-acceptance"></a><span data-ttu-id="cb57b-103">Licenc elfogadására van szükség</span><span class="sxs-lookup"><span data-stu-id="cb57b-103">Require license acceptance</span></span>

<span data-ttu-id="cb57b-104">Szükséges elem részleteit megjelenítő oldalon modulok licencszerződés elfogadására van szükség, a licenc elfogadása szöveg jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="cb57b-104">Require License Acceptance text shows up on item details page for modules that require license acceptance.</span></span> <span data-ttu-id="cb57b-105">Modul licenc a "Nézet License.txt" hivatkozásra kattintva tekintheti meg.</span><span class="sxs-lookup"><span data-stu-id="cb57b-105">License for module can be viewed by clicking on 'View License.txt' link.</span></span>

![Licenc elfogadására van szükség](../../Images/RequireLicenseAcceptance.png)

<span data-ttu-id="cb57b-107">Fogadja el a licencfeltételeket, telepítésekor, mentése vagy frissítése a modul PowerShellGet keresztül, vagy az Azure Automation telepítésekor a felhasználók felszólítást kapnak.</span><span class="sxs-lookup"><span data-stu-id="cb57b-107">Users will be prompted to accept the license when installing, saving or updating the module through PowerShellGet or when deploying to Azure Automation.</span></span>

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a><span data-ttu-id="cb57b-108">Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez</span><span class="sxs-lookup"><span data-stu-id="cb57b-108">Require License Acceptance on Deploy to Azure Automation</span></span>

<span data-ttu-id="cb57b-109">Ha az Azure Automation telepített modul licencszerződés elfogadását igényli, portál felhasználói felületének jelennek meg a jogi nyilatkozat bármelyiket "Ez a modul licencszerződés elfogadását igényli.</span><span class="sxs-lookup"><span data-stu-id="cb57b-109">If the module being deployed to Azure Automation requires license acceptance, portal UI will show a disclaimer saying 'This module requires license acceptance.</span></span> <span data-ttu-id="cb57b-110">Az OK gombra kattintva elfogadja licencfeltételek. "</span><span class="sxs-lookup"><span data-stu-id="cb57b-110">By clicking OK, you are accepting license terms.'</span></span>

![Telepítse az Azure Automation licencszerződés elfogadását igényli](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a><span data-ttu-id="cb57b-112">További részletekért</span><span class="sxs-lookup"><span data-stu-id="cb57b-112">More details</span></span>

<span data-ttu-id="cb57b-113">[A PowerShellGet licencszerződés elfogadására van szükség](../../concepts/module-license-acceptance.md)
[Azure Automation-webhely](/azure/automation)</span><span class="sxs-lookup"><span data-stu-id="cb57b-113">[Require License Acceptance in PowerShellGet](../../concepts/module-license-acceptance.md)
[Azure Automation website](/azure/automation)</span></span>