---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A Windows PowerShell célállapot-konfiguráló áttekintése"
ms.openlocfilehash: 154a3c78a9bf2a029577ca6862f333b6bfe69878
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="windows-powershell-desired-state-configuration-overview"></a><span data-ttu-id="f02ec-103">A Windows PowerShell célállapot-konfiguráló áttekintése</span><span class="sxs-lookup"><span data-stu-id="f02ec-103">Windows PowerShell Desired State Configuration Overview</span></span> 

> <span data-ttu-id="f02ec-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f02ec-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="f02ec-105">A DSC-ből egy olyan felügyeleti platformot, amely lehetővé teszi az informatikai kezelését PowerShell és a fejlesztői infrastruktúra és kód-konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="f02ec-105">DSC is a management platform in PowerShell that enables you to manage your IT and development infrastructure with configuration as code.</span></span>

- <span data-ttu-id="f02ec-106">Az üzleti előnyei a DSC áttekintését lásd: [kívánt állapot konfigurációs áttekintése döntéshozók](decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="f02ec-106">For an overview of the business benefits of using DSC, see [Desired State Configuration Overview for Decision Makers](decisionMaker.md).</span></span>
- <span data-ttu-id="f02ec-107">A mérnöki előnyei a DSC áttekintését lásd: [kívánt állapot konfigurációs áttekintése mérnökök](DscForEngineers.md).</span><span class="sxs-lookup"><span data-stu-id="f02ec-107">For an overview of the engineering benefits of using DSC, see [Desired State Configuration Overview for Engineers](DscForEngineers.md).</span></span>
- <span data-ttu-id="f02ec-108">A DSC gyorsan használatának megkezdéséhez tekintse meg [DSC gyors üzembe helyezési](quickStart.md).</span><span class="sxs-lookup"><span data-stu-id="f02ec-108">To start using DSC quickly, see [DSC quick start](quickStart.md).</span></span>

## <a name="key-concepts"></a><span data-ttu-id="f02ec-109">Alapfogalmak</span><span class="sxs-lookup"><span data-stu-id="f02ec-109">Key Concepts</span></span>

<span data-ttu-id="f02ec-110">A DSC-ből a egy konfigurációs, telepítési és felügyeleti rendszerek használt deklaratív platformja.</span><span class="sxs-lookup"><span data-stu-id="f02ec-110">DSC is a declarative platform used for configuration, deployment, and management of systems.</span></span> <span data-ttu-id="f02ec-111">Azt a három elsődleges összetevőből áll:</span><span class="sxs-lookup"><span data-stu-id="f02ec-111">It consists of three primary components:</span></span>

- <span data-ttu-id="f02ec-112">[Konfigurációk](configurations.md) deklaratív PowerShell parancsfájlok, amely határozza meg, és erőforrások példányainak konfigurálásához.</span><span class="sxs-lookup"><span data-stu-id="f02ec-112">[Configurations](configurations.md) are declarative PowerShell scripts which define and configure instances of resources.</span></span>
    <span data-ttu-id="f02ec-113">A konfiguráció, DSC (és az erőforrásokat, a konfiguráció által meghívott) lesz, egyszerűen "tenni,", győződjön meg arról, hogy létezik-e a rendszer a konfiguráció leírva állapotban.</span><span class="sxs-lookup"><span data-stu-id="f02ec-113">Upon running the configuration, DSC (and the resources being called by the configuration) will simply “make it so”, ensuring that the system exists in the state laid out by the configuration.</span></span> 
    <span data-ttu-id="f02ec-114">A DSC-konfigurációk megtalálhatók az idempotent: a helyi Configuration Manager (LCM) továbbra is győződjön meg arról, hogy gépek konfigurálva vannak-e bármilyen állapot, a konfiguráció a deklarál.</span><span class="sxs-lookup"><span data-stu-id="f02ec-114">DSC configurations are also idempotent: the Local Configuration Manager (LCM) will continue to ensure that machines are configured in whatever state the configuration declares.</span></span>
- <span data-ttu-id="f02ec-115">[Erőforrások](resources.md) DSC "legyen," részét képezik.</span><span class="sxs-lookup"><span data-stu-id="f02ec-115">[Resources](resources.md) are the "make it so" part of DSC.</span></span> <span data-ttu-id="f02ec-116">A put és a cél konfiguráció ne a megadott állapot kódot tartalmaznak.</span><span class="sxs-lookup"><span data-stu-id="f02ec-116">They contain the code that put and keep the target of a configuration in the specified state.</span></span> 
    <span data-ttu-id="f02ec-117">Erőforrások PowerShell-modulok találhatók, és csak írható modell valamilyen általános egy fájl vagy a Windows-folyamat vagy egy IIS-kiszolgálón vagy egy Azure-beli virtuális gép legpontosabb.</span><span class="sxs-lookup"><span data-stu-id="f02ec-117">Resources reside in PowerShell modules and can be written to model something as generic as a file or a Windows process, or as specific as an IIS server or a VM running in Azure.</span></span>
- <span data-ttu-id="f02ec-118">A [helyi Configuration Manager (LCM)](metaConfig.md) a motor, amely DSC elősegíti a konfigurációk és erőforrások közötti kapcsolat.</span><span class="sxs-lookup"><span data-stu-id="f02ec-118">The [Local Configuration Manager (LCM)](metaConfig.md) is the engine by which DSC facilitates the interaction between resources and configurations.</span></span> 
    <span data-ttu-id="f02ec-119">A LCM rendszeresen lekérdezi a rendszer az erőforrások által megvalósított folyamata segítségével győződjön meg arról, hogy megőrződjön-e a konfiguráció által meghatározott állapotot.</span><span class="sxs-lookup"><span data-stu-id="f02ec-119">The LCM regularly polls the system using the control flow implemented by resources to ensure that the state defined by a configuration is maintained.</span></span> 
    <span data-ttu-id="f02ec-120">Állapotát a rendszer esetén a LCM teszi a kód hívásainak erőforrások ahhoz "," konfigurációjának megfelelően.</span><span class="sxs-lookup"><span data-stu-id="f02ec-120">If the system is out of state, the LCM makes calls to the code in resources to “make it so” according to the configuration.</span></span> 

## <a name="see-also"></a><span data-ttu-id="f02ec-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f02ec-121">See Also</span></span>

- [<span data-ttu-id="f02ec-122">A DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="f02ec-122">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="f02ec-123">A DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="f02ec-123">DSC Resources</span></span>](resources.md)
- [<span data-ttu-id="f02ec-124">A helyi Configuration Manager konfigurálása</span><span class="sxs-lookup"><span data-stu-id="f02ec-124">Configuring The Local Configuration Manager</span></span>](metaConfig.md)

