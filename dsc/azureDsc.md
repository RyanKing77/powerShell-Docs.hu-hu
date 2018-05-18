---
ms.date: 03/15/2018
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC használata a Microsoft Azure-ban
ms.openlocfilehash: d35488c3f66895e930eaa84360f3d3ec9d74e9c7
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="using-dsc-on-microsoft-azure"></a><span data-ttu-id="24e4a-103">A DSC használata a Microsoft Azure-ban</span><span class="sxs-lookup"><span data-stu-id="24e4a-103">Using DSC on Microsoft Azure</span></span>

<span data-ttu-id="24e4a-104">A Microsoft Azure használatával támogatott a kívánt állapot konfigurációs szolgáltatása (DSC) a [Azure célállapot-konfiguráció bővítmény kezelő](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview) és a [Azure Automation DSC](/azure/automation/automation-dsc-overview).</span><span class="sxs-lookup"><span data-stu-id="24e4a-104">Desired State Configuration (DSC) is supported in Microsoft Azure through the [Azure Desired State Configuration extension handler](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview) and through [Azure Automation DSC](/azure/automation/automation-dsc-overview).</span></span>

## <a name="azure-desired-state-configuration-extension-handler"></a><span data-ttu-id="24e4a-105">Azure kívánt állapot konfigurációs kiterjesztés kezelője</span><span class="sxs-lookup"><span data-stu-id="24e4a-105">Azure Desired State Configuration extension handler</span></span>

<span data-ttu-id="24e4a-106">Az Azure DSC-bővítmény lehetővé teszi, hogy a kezelni kívánt DSC Microsoft Azure-ban üzemeltetett virtuális gépeket.</span><span class="sxs-lookup"><span data-stu-id="24e4a-106">The Azure DSC extension allows VMs hosted in Microsoft Azure to be managed with DSC.</span></span>
<span data-ttu-id="24e4a-107">További tudnivalók az alábbi témakörökben találhatók:</span><span class="sxs-lookup"><span data-stu-id="24e4a-107">For more information, see the following topics:</span></span>

- [<span data-ttu-id="24e4a-108">Azure kívánt állapot konfigurációs kiterjesztés kezelője</span><span class="sxs-lookup"><span data-stu-id="24e4a-108">Azure Desired State Configuration extension handler</span></span>](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-overview)
- [<span data-ttu-id="24e4a-109">Windows VMSS és célállapot-konfiguráció Azure Resource Manager-sablonok</span><span class="sxs-lookup"><span data-stu-id="24e4a-109">Windows VMSS and Desired State Configuration with Azure Resource Manager templates</span></span>](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-template)
- [<span data-ttu-id="24e4a-110">Hitelesítő adatok átadni a Azure DSC-kiterjesztés kezelője</span><span class="sxs-lookup"><span data-stu-id="24e4a-110">Passing credentials to the Azure DSC extension handler</span></span>](/azure/virtual-machines/virtual-machines-windows-extensions-dsc-credentials)
- [<span data-ttu-id="24e4a-111">Azure kívánt állapot konfigurációs bővítmény előzmények</span><span class="sxs-lookup"><span data-stu-id="24e4a-111">Azure Desired State Configuration extension history</span></span>](azureDscexthistory.md)

## <a name="azure-automation-dsc"></a><span data-ttu-id="24e4a-112">Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="24e4a-112">Azure Automation DSC</span></span>

<span data-ttu-id="24e4a-113">A [Azure Automation szolgáltatás](https://azure.microsoft.com/services/automation/) kezelheti a DSC-konfigurációk, erőforrások és az Azure-ban felügyelt csomópontokat.</span><span class="sxs-lookup"><span data-stu-id="24e4a-113">The [Azure Automation service](https://azure.microsoft.com/services/automation/) allows you to manage DSC configurations, resources, and managed nodes from within Azure.</span></span> <span data-ttu-id="24e4a-114">További tudnivalók az alábbi témakörökben találhatók:</span><span class="sxs-lookup"><span data-stu-id="24e4a-114">For more information, see the following topics:</span></span>

- [<span data-ttu-id="24e4a-115">Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="24e4a-115">Azure Automation DSC</span></span>](/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="24e4a-116">Ismerkedés az Azure Automation DSC</span><span class="sxs-lookup"><span data-stu-id="24e4a-116">Getting started with Azure Automation DSC</span></span>](/azure/automation/automation-dsc-getting-started)
- [<span data-ttu-id="24e4a-117">Azure Automation DSC általi kezelésre bevezetési gépek</span><span class="sxs-lookup"><span data-stu-id="24e4a-117">Onboarding machines for management by Azure Automation DSC</span></span>](/azure/automation/automation-dsc-onboarding)