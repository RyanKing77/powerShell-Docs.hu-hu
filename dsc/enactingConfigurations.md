---
ms.date: 2017-10-16
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Életbe konfigurációk"
ms.openlocfilehash: 4285dbe04c9745ec2a859e479848da2881c18de0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="enacting-configurations"></a><span data-ttu-id="70963-103">Életbe konfigurációk</span><span class="sxs-lookup"><span data-stu-id="70963-103">Enacting configurations</span></span>

><span data-ttu-id="70963-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="70963-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="70963-105">PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) konfigurációk kihirdeti két módja van: leküldéses és lekéréses módot.</span><span class="sxs-lookup"><span data-stu-id="70963-105">There are two ways to enact PowerShell Desired State Configuration (DSC) configurations: push mode and pull mode.</span></span>

## <a name="push-mode"></a><span data-ttu-id="70963-106">Leküldéses mód</span><span class="sxs-lookup"><span data-stu-id="70963-106">Push mode</span></span>

<span data-ttu-id="70963-107">![Leküldéses módot](images/pushModel.png "leküldés üzemmód működése")</span><span class="sxs-lookup"><span data-stu-id="70963-107">![Push mode](images/pushModel.png "How push mode works")</span></span>

<span data-ttu-id="70963-108">Leküldéses módban a felhasználó aktívan alkalmazása egy konfigurációs egy célcsomóponttal meghívásával hivatkozik a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="70963-108">Push mode refers to a user actively applying a configuration to a target node by calling the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet.</span></span>

<span data-ttu-id="70963-109">Miután létrehozta, és a konfiguráció fordítása, akkor is kihirdeti azt leküldéses módban meghívásával a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) beállítása, a parancsmag a - Path paramétert a konfigurációs MOF elérési útját a parancsmag.</span><span class="sxs-lookup"><span data-stu-id="70963-109">After creating and compiling a configuration, you can enact it in push mode by calling the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, setting the -Path parameter of the cmdlet to the path where the configuration MOF is located.</span></span>
<span data-ttu-id="70963-110">Például, ha a konfiguráció MOF itt található: `C:\DSC\Configurations\localhost.mof`, volna vonatkoznak a helyi gép a következő paranccsal:`Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span><span class="sxs-lookup"><span data-stu-id="70963-110">For example, if the configuration MOF is located at `C:\DSC\Configurations\localhost.mof`, you would apply it to the local machine with the following command: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`</span></span>

> <span data-ttu-id="70963-111">__Megjegyzés:__: DSC alapértelmezés szerint egy konfigurációs fut háttérfeladatként.</span><span class="sxs-lookup"><span data-stu-id="70963-111">__Note__: By default, DSC runs a configuration as a background job.</span></span> <span data-ttu-id="70963-112">Interaktív módon futtassa a konfigurációt, hívja meg a [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) rendelkező a __-Várjon, amíg__ paraméter.</span><span class="sxs-lookup"><span data-stu-id="70963-112">To run the configuration interactively, call the [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) with the __-Wait__ parameter.</span></span>

## <a name="pull-mode"></a><span data-ttu-id="70963-113">Lekéréses mód</span><span class="sxs-lookup"><span data-stu-id="70963-113">Pull mode</span></span>

<span data-ttu-id="70963-114">![Lekéréses mód](images/pullModel.png "lekéréses üzemmód működése")</span><span class="sxs-lookup"><span data-stu-id="70963-114">![Pull Mode](images/pullModel.png "How pull mode works")</span></span>

<span data-ttu-id="70963-115">Lekéréses módban lekéréses ügyfél lekérni a kívánt állapot konfigurációját egy távoli lekéréses szolgáltatásból van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="70963-115">In pull mode, pull clients are configured to get their desired state configurations from a remote pull service.</span></span>
<span data-ttu-id="70963-116">Hasonlóképpen, a lekéréses szolgáltatás állomás a DSC szolgáltatás beállítása és konfigurációkat és a lekéréses ügyfelek által igényelt erőforrás van kiépítve.</span><span class="sxs-lookup"><span data-stu-id="70963-116">Likewise, the pull service has been set up to host the DSC service, and has been provisioned with the configurations and resources that are required by the pull clients.</span></span>
<span data-ttu-id="70963-117">Mindegyik lekéréses ügyfél rendelkezik-e egy ütemezett eseményre, hogy a csomópont konfigurálása rendszeres megfelelőségi ellenőrzést végez.</span><span class="sxs-lookup"><span data-stu-id="70963-117">Each of the pull clients has a scheduled event that performs a periodic compliance check on the configuration of the node.</span></span>
<span data-ttu-id="70963-118">Az esemény akkor váltódik ki az első alkalommal, amikor a helyi Configuration Manager (LCM) az lekéréses ügyfélen egy kérést küld a lekéréses szolgáltatás a LCM a megadott konfiguráció lekérése.</span><span class="sxs-lookup"><span data-stu-id="70963-118">When the event is triggered the first time, the Local Configuration Manager (LCM) on the pull client makes a request to the pull service to get the configuration specified in the LCM.</span></span>
<span data-ttu-id="70963-119">Ha ez a konfiguráció lekéréses szolgáltatás létezik, és adja át, kezdeti érvényességi ellenőrzéseket, a konfiguráció az lekéréses ügyfélnek, amelyen, majd végrehajtja a rendszer által a LCM le.</span><span class="sxs-lookup"><span data-stu-id="70963-119">If that configuration exists on the pull service, and it passes initial validation checks, the configuration is downloaded to the pull client, where it is then executed by the LCM.</span></span>

<span data-ttu-id="70963-120">A LCM ellenőrzi, hogy az ügyfél által meghatározott rendszeres időközönként a konfiguráció megfelel a **ConfigurationModeFrequencyMins** a LCM tulajdonsága.</span><span class="sxs-lookup"><span data-stu-id="70963-120">The LCM checks that the client is in compliance with the configuration at regular intervals specified by the **ConfigurationModeFrequencyMins** property of the LCM.</span></span>
<span data-ttu-id="70963-121">A LCM lekéréses szolgáltatás frissített konfiguráció által meghatározott rendszeres időközönként ellenőrzi a **RefreshModeFrequency** a LCM tulajdonsága.</span><span class="sxs-lookup"><span data-stu-id="70963-121">The LCM checks for updated configurations on the pull service at regular intervals specified by the **RefreshModeFrequency** property of the LCM.</span></span>
<span data-ttu-id="70963-122">A LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md).</span><span class="sxs-lookup"><span data-stu-id="70963-122">For information about configuring the LCM, see [Configuring the Local Configuration Manager](metaConfig.md).</span></span>

<span data-ttu-id="70963-123">Az ajánlott megoldás egy lekéréses szolgáltatást tartalmazó a DSC felhőszolgáltatás [Azure Automation](https://azure.microsoft.com/en-us/services/automation/).</span><span class="sxs-lookup"><span data-stu-id="70963-123">The recommended solution for hosting a Pull Service, is the DSC cloud service, [Azure Automation](https://azure.microsoft.com/en-us/services/automation/).</span></span>
<span data-ttu-id="70963-124">Ez üzemeltetett megoldás grafikus felügyeleti, a jelentéskészítés és a központi felügyeletet biztosít.</span><span class="sxs-lookup"><span data-stu-id="70963-124">This is hosted solution provides graphical management, reporting, and centralized administration.</span></span>

<span data-ttu-id="70963-125">Egy lekéréses szolgáltatás a Windows Server beállításával kapcsolatos további információkért lásd: [DSC lekérési webkiszolgáló beállítása](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="70963-125">For more information on setting up a Pull Service on Windows Server, see [Setting up a DSC web pull server](pullServer.md).</span></span>
<span data-ttu-id="70963-126">Ismerje meg, azonban, hogy ez a megvalósítás csak korlátozott szolgáltatásokat, és szükséges az egyes "elvégezhető saját kezűleg" integráció.</span><span class="sxs-lookup"><span data-stu-id="70963-126">Understand however, that this implementation has limited features and does require some "do it yourself" integration.</span></span>

<span data-ttu-id="70963-127">Az alábbi témakörök ismertetik lekéréses szolgáltatás és az ügyfelek:</span><span class="sxs-lookup"><span data-stu-id="70963-127">The following topics explain pull service and clients:</span></span>

- [<span data-ttu-id="70963-128">Azure Automation DSC – áttekintés</span><span class="sxs-lookup"><span data-stu-id="70963-128">Azure Automation DSC Overview</span></span>](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="70963-129">Az SMB-lekérési kiszolgálójával beállítása</span><span class="sxs-lookup"><span data-stu-id="70963-129">Setting up an SMB pull server</span></span>](pullServerSMB.md)
- [<span data-ttu-id="70963-130">A lekéréses ügyfél konfigurálása</span><span class="sxs-lookup"><span data-stu-id="70963-130">Configuring a pull client</span></span>](pullClientConfigID.md)
