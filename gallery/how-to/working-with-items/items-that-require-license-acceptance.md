---
ms.date: 06/12/2017
contributor: Farehar
ms.topic: conceptual
keywords: gyűjtemény, powershell, psgallery
title: Licenc elfogadására van szükség
ms.openlocfilehash: 76f16e848e1cd660e062bf8569fb914b32f14934
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="require-license-acceptance"></a><span data-ttu-id="fe591-103">Licenc elfogadására van szükség</span><span class="sxs-lookup"><span data-stu-id="fe591-103">Require license acceptance</span></span>

<span data-ttu-id="fe591-104">Szükséges elem részleteit megjelenítő oldalon modulok licencszerződés elfogadására van szükség, a licenc elfogadása szöveg jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="fe591-104">Require License Acceptance text shows up on item details page for modules that require license acceptance.</span></span> <span data-ttu-id="fe591-105">Modul licenc a "Nézet License.txt" hivatkozásra kattintva tekintheti meg.</span><span class="sxs-lookup"><span data-stu-id="fe591-105">License for module can be viewed by clicking on 'View License.txt' link.</span></span>

![Licenc elfogadására van szükség](../../Images/RequireLicenseAcceptance.png)

<span data-ttu-id="fe591-107">Fogadja el a licencfeltételeket, telepítésekor, mentése vagy frissítése a modul PowerShellGet keresztül, vagy az Azure Automation telepítésekor a felhasználók felszólítást kapnak.</span><span class="sxs-lookup"><span data-stu-id="fe591-107">Users will be prompted to accept the license when installing, saving or updating the module through PowerShellGet or when deploying to Azure Automation.</span></span>

## <a name="require-license-acceptance-on-deploy-to-azure-automation"></a><span data-ttu-id="fe591-108">Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez</span><span class="sxs-lookup"><span data-stu-id="fe591-108">Require License Acceptance on Deploy to Azure Automation</span></span>

<span data-ttu-id="fe591-109">Ha az Azure Automation telepített modul licencszerződés elfogadását igényli, portál felhasználói felületének jelennek meg a jogi nyilatkozat bármelyiket "Ez a modul licencszerződés elfogadását igényli.</span><span class="sxs-lookup"><span data-stu-id="fe591-109">If the module being deployed to Azure Automation requires license acceptance, portal UI will show a disclaimer saying 'This module requires license acceptance.</span></span> <span data-ttu-id="fe591-110">Az OK gombra kattintva elfogadja licencfeltételek. "</span><span class="sxs-lookup"><span data-stu-id="fe591-110">By clicking OK, you are accepting license terms.'</span></span>

![Telepítse az Azure Automation licencszerződés elfogadását igényli](../../Images/DeployToAzureAutomationRequireLicenseAcceptanceDisclaimer.png)

## <a name="more-details"></a><span data-ttu-id="fe591-112">További részletekért</span><span class="sxs-lookup"><span data-stu-id="fe591-112">More details</span></span>

<span data-ttu-id="fe591-113">[A PowerShellGet licencszerződés elfogadására van szükség](../../concepts/module-license-acceptance.md)
[Azure Automation-webhely](/azure/automation)</span><span class="sxs-lookup"><span data-stu-id="fe591-113">[Require License Acceptance in PowerShellGet](../../concepts/module-license-acceptance.md)
[Azure Automation website](/azure/automation)</span></span>