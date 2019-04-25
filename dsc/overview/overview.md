---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Windows PowerShell Desired State Configuration áttekintése
ms.openlocfilehash: 3e4f0afa17ab60bfa98f1b86b9830462a7c8e1cf
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079971"
---
# <a name="windows-powershell-desired-state-configuration-overview"></a><span data-ttu-id="719fe-103">Windows PowerShell Desired State Configuration áttekintése</span><span class="sxs-lookup"><span data-stu-id="719fe-103">Windows PowerShell Desired State Configuration Overview</span></span>

> <span data-ttu-id="719fe-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="719fe-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="719fe-105">DSC egy felügyeleti platform, amely lehetővé teszi, hogy az informatikai RÉSZLEG felügyelete PowerShell és a fejlesztési infrastruktúra mint kód konfigurációval.</span><span class="sxs-lookup"><span data-stu-id="719fe-105">DSC is a management platform in PowerShell that enables you to manage your IT and development infrastructure with configuration as code.</span></span>

- <span data-ttu-id="719fe-106">Az üzleti előnyei DSC áttekintését lásd: [Desired State Configuration áttekintése döntéshozók számára](decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="719fe-106">For an overview of the business benefits of using DSC, see [Desired State Configuration Overview for Decision Makers](decisionMaker.md).</span></span>
- <span data-ttu-id="719fe-107">A mérnöki előnyei DSC áttekintését lásd: [Desired State Configuration áttekintése mérnökök számára](DscForEngineers.md).</span><span class="sxs-lookup"><span data-stu-id="719fe-107">For an overview of the engineering benefits of using DSC, see [Desired State Configuration Overview for Engineers](DscForEngineers.md).</span></span>
- <span data-ttu-id="719fe-108">DSC használatának gyors megkezdéséhez lásd [DSC gyors üzembe helyezési](../quickstarts/website-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="719fe-108">To start using DSC quickly, see [DSC quick start](../quickstarts/website-quickstart.md).</span></span>

## <a name="key-concepts"></a><span data-ttu-id="719fe-109">Fő fogalmak</span><span class="sxs-lookup"><span data-stu-id="719fe-109">Key Concepts</span></span>

<span data-ttu-id="719fe-110">DSC az deklaratív platform konfiguráció, telepítési és felügyeleti rendszerek használható.</span><span class="sxs-lookup"><span data-stu-id="719fe-110">DSC is a declarative platform used for configuration, deployment, and management of systems.</span></span> <span data-ttu-id="719fe-111">Három elsődleges összetevőből áll:</span><span class="sxs-lookup"><span data-stu-id="719fe-111">It consists of three primary components:</span></span>

- <span data-ttu-id="719fe-112">[Konfigurációk](../configurations/configurations.md) deklaratív PowerShell-szkriptek, amelyek meghatározása és konfigurálása erőforráspéldány.</span><span class="sxs-lookup"><span data-stu-id="719fe-112">[Configurations](../configurations/configurations.md) are declarative PowerShell scripts which define and configure instances of resources.</span></span>
    <span data-ttu-id="719fe-113">Futtatása a konfiguráció, DSC (és az erőforrások által a konfiguráció) lesz, egyszerűen csak "Győződjön meg arról, hogy így", annak biztosítása, hogy létezik-e a rendszer által a konfiguráció állapotban.</span><span class="sxs-lookup"><span data-stu-id="719fe-113">Upon running the configuration, DSC (and the resources being called by the configuration) will simply “make it so”, ensuring that the system exists in the state laid out by the configuration.</span></span>
    <span data-ttu-id="719fe-114">DSC-konfigurációk is idempotens: a helyi Configuration Manager (LCM) továbbra is győződjön meg arról, hogy a gépek megtörténik-e a függetlenül a konfigurációs állapot deklarálja.</span><span class="sxs-lookup"><span data-stu-id="719fe-114">DSC configurations are also idempotent: the Local Configuration Manager (LCM) will continue to ensure that machines are configured in whatever state the configuration declares.</span></span>
- <span data-ttu-id="719fe-115">[Erőforrások](../resources/resources.md) DSC "Győződjön meg arról, hogy így" részét képezik.</span><span class="sxs-lookup"><span data-stu-id="719fe-115">[Resources](../resources/resources.md) are the "make it so" part of DSC.</span></span> <span data-ttu-id="719fe-116">A put és a cél egy konfiguráció ne a megadott állapot kódját tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="719fe-116">They contain the code that put and keep the target of a configuration in the specified state.</span></span>
    <span data-ttu-id="719fe-117">Erőforrások PowerShell-modulok tartalmazhat, és írható, valamilyen általános egy fájl vagy egy Windows-folyamat vagy egy IIS-kiszolgáló vagy az Azure-ban futó virtuális gépek az adott modell.</span><span class="sxs-lookup"><span data-stu-id="719fe-117">Resources reside in PowerShell modules and can be written to model something as generic as a file or a Windows process, or as specific as an IIS server or a VM running in Azure.</span></span>
- <span data-ttu-id="719fe-118">A [helyi Configuration Manager (LCM) Konfigurálása](../managing-nodes/metaConfig.md) a motor, amellyel DSC elősegíti a közötti interakció erőforrásokat és konfigurációkat.</span><span class="sxs-lookup"><span data-stu-id="719fe-118">The [Local Configuration Manager (LCM)](../managing-nodes/metaConfig.md) is the engine by which DSC facilitates the interaction between resources and configurations.</span></span>
    <span data-ttu-id="719fe-119">Az LCM rendszeresen lekérdezi a rendszer az erőforrások által megvalósított vezérlési folyamatában segítségével győződjön meg arról, hogy megőrződjön-e a konfiguráció által meghatározott állapotot.</span><span class="sxs-lookup"><span data-stu-id="719fe-119">The LCM regularly polls the system using the control flow implemented by resources to ensure that the state defined by a configuration is maintained.</span></span>
    <span data-ttu-id="719fe-120">Ha a rendszer állapotát, a LCM teszi a kód meghívja "erőforrásaink, így" konfigurációjának megfelelően.</span><span class="sxs-lookup"><span data-stu-id="719fe-120">If the system is out of state, the LCM makes calls to the code in resources to “make it so” according to the configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="719fe-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="719fe-121">See Also</span></span>

- [<span data-ttu-id="719fe-122">DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="719fe-122">DSC Configurations</span></span>](../configurations/configurations.md)
- [<span data-ttu-id="719fe-123">DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="719fe-123">DSC Resources</span></span>](../resources/resources.md)
- [<span data-ttu-id="719fe-124">A helyi Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="719fe-124">Configuring The Local Configuration Manager</span></span>](../managing-nodes/metaConfig.md)
