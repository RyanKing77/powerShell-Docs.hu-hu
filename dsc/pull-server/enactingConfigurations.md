---
ms.date: 10/16/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációk életbe léptetése
ms.openlocfilehash: 2a40f2055dda78cc0cb6cb05a5e14dce48be9d00
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079933"
---
# <a name="enacting-configurations"></a><span data-ttu-id="e4a6b-103">Konfigurációk életbe léptetése</span><span class="sxs-lookup"><span data-stu-id="e4a6b-103">Enacting configurations</span></span>

><span data-ttu-id="e4a6b-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="e4a6b-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="e4a6b-105">A PowerShell Desired State Configuration (DSC) konfigurációk kihirdeti két módja van: leküldéses és lekéréses módot.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-105">There are two ways to enact PowerShell Desired State Configuration (DSC) configurations: push mode and pull mode.</span></span>

## <a name="push-mode"></a><span data-ttu-id="e4a6b-106">Leküldéses módban</span><span class="sxs-lookup"><span data-stu-id="e4a6b-106">Push mode</span></span>

<span data-ttu-id="e4a6b-107">![Leküldéses módban](../images/pushModel.png "leküldés üzemmód működése")</span><span class="sxs-lookup"><span data-stu-id="e4a6b-107">![Push mode](../images/pushModel.png "How push mode works")</span></span>

<span data-ttu-id="e4a6b-108">Leküldéses módban a felhasználó aktívan alkalmazása egy konfigurációs egy célcsomóponttal meghívásával hivatkozik a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-108">Push mode refers to a user actively applying a configuration to a target node by calling the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span>

<span data-ttu-id="e4a6b-109">Miután létrehozta és fordításáról, akkor is kihirdeti, leküldéses módban meghívásával a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) beállítást, a parancsmag a - Path paraméterrel, a parancsmagot, amely a konfigurációs MOF elérési útját.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-109">After creating and compiling a configuration, you can enact it in push mode by calling the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet, setting the -Path parameter of the cmdlet to the path where the configuration MOF is located.</span></span>
<span data-ttu-id="e4a6b-110">Például, ha a konfigurációs MOF a következő helyen található `C:\DSC\Configurations\localhost.mof`, a következő paranccsal a helyi számítógépen szeretné alkalmazni: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span><span class="sxs-lookup"><span data-stu-id="e4a6b-110">For example, if the configuration MOF is located at `C:\DSC\Configurations\localhost.mof`, you would apply it to the local machine with the following command: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span></span>

> <span data-ttu-id="e4a6b-111">__Megjegyzés:__: Alapértelmezés szerint DSC háttérfeladatként futtatja a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-111">__Note__: By default, DSC runs a configuration as a background job.</span></span> <span data-ttu-id="e4a6b-112">A konfiguráció interaktívan, hívja meg a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) az a __-várjon__ paraméter.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-112">To run the configuration interactively, call the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) with the __-Wait__ parameter.</span></span>

## <a name="pull-mode"></a><span data-ttu-id="e4a6b-113">Lekérési mód</span><span class="sxs-lookup"><span data-stu-id="e4a6b-113">Pull mode</span></span>

<span data-ttu-id="e4a6b-114">![Lekérési mód](../images/pullModel.png "lekéréses üzemmód működése")</span><span class="sxs-lookup"><span data-stu-id="e4a6b-114">![Pull Mode](../images/pullModel.png "How pull mode works")</span></span>

<span data-ttu-id="e4a6b-115">Lekérési mód lekéréses ügyfelek szolgáltatásból való beolvasására a kívánt állapotban konfigurációját egy távoli lekéréses vannak konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-115">In pull mode, pull clients are configured to get their desired state configurations from a remote pull service.</span></span>
<span data-ttu-id="e4a6b-116">Hasonlóképpen a lekéréses szolgáltatás be lett állítva a gazdagépen a DSC szolgáltatás, és kiépítette a konfigurációk és a pull-ügyfelek által igényelt forrásokat.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-116">Likewise, the pull service has been set up to host the DSC service, and has been provisioned with the configurations and resources that are required by the pull clients.</span></span>
<span data-ttu-id="e4a6b-117">A pull-ügyfelek mindegyike rendelkezik, amely a rendszeres megfelelőségét ellenőrzi a konfigurációt a csomópont, ütemezett esemény.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-117">Each of the pull clients has a scheduled event that performs a periodic compliance check on the configuration of the node.</span></span>
<span data-ttu-id="e4a6b-118">Az esemény első alkalommal aktiválódik, ha a helyi Configuration Manager (LCM) Konfigurálása a leküldéses ügyfél kérést küld a lekéréses szolgáltatásával a szükséges az LCM Konfigurálása a megadott konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-118">When the event is triggered the first time, the Local Configuration Manager (LCM) on the pull client makes a request to the pull service to get the configuration specified in the LCM.</span></span>
<span data-ttu-id="e4a6b-119">Ez a konfiguráció a lekéréses szolgáltatás létezik, és átadja a kezdeti érvényesség-ellenőrzések, a konfigurációs van letölti a lekérési ügyfél, ahol majd következő(k) az LCM Konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-119">If that configuration exists on the pull service, and it passes initial validation checks, the configuration is downloaded to the pull client, where it is then executed by the LCM.</span></span>

<span data-ttu-id="e4a6b-120">Az LCM ellenőrzi, hogy az ügyfél által megadott rendszeres időközönként a konfiguráció megfelel a **ConfigurationModeFrequencyMins** az LCM tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-120">The LCM checks that the client is in compliance with the configuration at regular intervals specified by the **ConfigurationModeFrequencyMins** property of the LCM.</span></span>
<span data-ttu-id="e4a6b-121">Az LCM Konfigurálása a lekérési szolgáltatást a frissített konfiguráció által meghatározott időközönként ellenőrzi a **RefreshModeFrequency** az LCM tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-121">The LCM checks for updated configurations on the pull service at regular intervals specified by the **RefreshModeFrequency** property of the LCM.</span></span>
<span data-ttu-id="e4a6b-122">Az LCM konfigurálásával kapcsolatos további információkért lásd: [a Local Configuration Manager](../managing-nodes/metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="e4a6b-122">For information about configuring the LCM, see [Configuring the Local Configuration Manager](../managing-nodes/metaConfig.md).</span></span>

<span data-ttu-id="e4a6b-123">Az ajánlott megoldás egy lekéréses szolgáltatás üzemeltetéséhez a DSC-felhőszolgáltatás, [Azure Automation](https://azure.microsoft.com/services/automation/).</span><span class="sxs-lookup"><span data-stu-id="e4a6b-123">The recommended solution for hosting a Pull Service, is the DSC cloud service, [Azure Automation](https://azure.microsoft.com/services/automation/).</span></span>
<span data-ttu-id="e4a6b-124">Ez üzemeltetett megoldás a grafikus felügyeleti, a jelentéseket és a központi felügyeletet biztosít.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-124">This is hosted solution provides graphical management, reporting, and centralized administration.</span></span>

<span data-ttu-id="e4a6b-125">A Windows Server lekéréses szolgáltatás beállításának további információkért lásd: [DSC lekérési kiszolgáló beállítása](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="e4a6b-125">For more information on setting up a Pull Service on Windows Server, see [Setting up a DSC web pull server](pullServer.md).</span></span>
<span data-ttu-id="e4a6b-126">Azonban, ismerje meg, hogy ez a megvalósítás csak korlátozott funkciókat, és néhány "mindezt saját maga" integrációt igényelnek.</span><span class="sxs-lookup"><span data-stu-id="e4a6b-126">Understand however, that this implementation has limited features and does require some "do it yourself" integration.</span></span>

<span data-ttu-id="e4a6b-127">Az alábbi témakörök ismertetik a lekérési szolgáltatást és az ügyfelek számára:</span><span class="sxs-lookup"><span data-stu-id="e4a6b-127">The following topics explain pull service and clients:</span></span>

- [<span data-ttu-id="e4a6b-128">Az Azure Automation DSC – áttekintés</span><span class="sxs-lookup"><span data-stu-id="e4a6b-128">Azure Automation DSC Overview</span></span>](https://docs.microsoft.com/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="e4a6b-129">Az SMB-lekérési kiszolgálójának beállítása</span><span class="sxs-lookup"><span data-stu-id="e4a6b-129">Setting up an SMB pull server</span></span>](pullServerSMB.md)
- [<span data-ttu-id="e4a6b-130">Lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="e4a6b-130">Configuring a pull client</span></span>](pullClientConfigID.md)
