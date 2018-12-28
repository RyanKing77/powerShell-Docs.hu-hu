---
ms.date: 03/15/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC használata a Microsoft Azure-ban
ms.openlocfilehash: 54a317a415ff12c3d270897f414cba88716f0728
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404136"
---
# <a name="using-dsc-on-microsoft-azure"></a><span data-ttu-id="49933-103">A DSC használata a Microsoft Azure-ban</span><span class="sxs-lookup"><span data-stu-id="49933-103">Using DSC on Microsoft Azure</span></span>

<span data-ttu-id="49933-104">A Microsoft az Azure-ban támogatott Desired State Configuration (DSC) a [Azure Desired State Configuration bővítmény kezelő](/azure/virtual-machines/extensions/dsc-overview) és [Azure Automation DSC](/azure/automation/automation-dsc-overview).</span><span class="sxs-lookup"><span data-stu-id="49933-104">Desired State Configuration (DSC) is supported in Microsoft Azure through the [Azure Desired State Configuration extension handler](/azure/virtual-machines/extensions/dsc-overview) and through [Azure Automation DSC](/azure/automation/automation-dsc-overview).</span></span>

## <a name="azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="49933-105">Azure Desired State Configuration bővítmény kezelő</span><span class="sxs-lookup"><span data-stu-id="49933-105">Azure Desired State Configuration extension handler</span></span>

<span data-ttu-id="49933-106">Az Azure DSC bővítmény lehetővé teszi, hogy a DSC felügyelni a Microsoft Azure-ban üzemeltetett virtuális gépeket.</span><span class="sxs-lookup"><span data-stu-id="49933-106">The Azure DSC extension allows VMs hosted in Microsoft Azure to be managed with DSC.</span></span>
<span data-ttu-id="49933-107">További tudnivalók az alábbi témakörökben találhatók:</span><span class="sxs-lookup"><span data-stu-id="49933-107">For more information, see the following topics:</span></span>

- [<span data-ttu-id="49933-108">Azure Desired State Configuration bővítmény kezelő</span><span class="sxs-lookup"><span data-stu-id="49933-108">Azure Desired State Configuration extension handler</span></span>](/azure/virtual-machines/extensions/dsc-overview)
- [<span data-ttu-id="49933-109">Windows VMSS és az Azure Resource Manager-sablonok Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="49933-109">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>](/azure/virtual-machines/extensions/dsc-template)
- [<span data-ttu-id="49933-110">Hitelesítő adatok továbbítja az Azure DSC Bővítménykezelő</span><span class="sxs-lookup"><span data-stu-id="49933-110">Passing credentials to the Azure DSC extension handler</span></span>](/azure/virtual-machines/extensions/dsc-credentials)
- [<span data-ttu-id="49933-111">Azure Desired State Configuration bővítmény előzményei</span><span class="sxs-lookup"><span data-stu-id="49933-111">Azure Desired State Configuration extension history</span></span>](azureDscexthistory.md)

## <a name="azure-automation-dsc"></a><span data-ttu-id="49933-112">Az Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="49933-112">Azure Automation DSC</span></span>

<span data-ttu-id="49933-113">A [Azure Automation szolgáltatás](https://azure.microsoft.com/en-us/services/automation/) segítségével kezelheti a DSC-konfigurációk, erőforrások és a felügyelt csomópontok az Azure-ban.</span><span class="sxs-lookup"><span data-stu-id="49933-113">The [Azure Automation service](https://azure.microsoft.com/en-us/services/automation/) allows you to manage DSC configurations, resources, and managed nodes from within Azure.</span></span> <span data-ttu-id="49933-114">További tudnivalók az alábbi témakörökben találhatók:</span><span class="sxs-lookup"><span data-stu-id="49933-114">For more information, see the following topics:</span></span>

- [<span data-ttu-id="49933-115">Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="49933-115">Azure Automation DSC</span></span>](/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="49933-116">Azure Automation DSC – első lépések</span><span class="sxs-lookup"><span data-stu-id="49933-116">Getting started with Azure Automation DSC</span></span>](/azure/automation/automation-dsc-getting-started)
- [<span data-ttu-id="49933-117">Gépek előkészítése kezelésre, amelyet az Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="49933-117">Onboarding machines for management by Azure Automation DSC</span></span>](/azure/automation/automation-dsc-onboarding)