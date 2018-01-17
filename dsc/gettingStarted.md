---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Ismerkedés a PowerShell-Célállapotkonfiguráció"
ms.openlocfilehash: 856528f1e52eafa8b2c93b825a60376a0d64cab2
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="getting-started-with-powershell-desired-state-configuration"></a><span data-ttu-id="457a9-103">Ismerkedés a PowerShell-Célállapotkonfiguráció</span><span class="sxs-lookup"><span data-stu-id="457a9-103">Getting Started with PowerShell Desired State Configuration</span></span> #

<span data-ttu-id="457a9-104">Ez az útmutató ismerteti, hogyan elindítja a PowerShell célállapot-konfiguráció dokumentumok létrehozása és alkalmazása a gépeken.</span><span class="sxs-lookup"><span data-stu-id="457a9-104">This guide describes how to begin creating PowerShell Desired State Configuration documents and apply them to machines.</span></span> <span data-ttu-id="457a9-105">Funkciók, a PowerShell parancsmagok és a modulok alapszintű ismeretét feltételezi.</span><span class="sxs-lookup"><span data-stu-id="457a9-105">It assumes basic familiarity with PowerShell cmdlets, modules, and functions.</span></span> 


## <a name="create-a-configuration"></a><span data-ttu-id="457a9-106">Konfiguráció létrehozása</span><span class="sxs-lookup"><span data-stu-id="457a9-106">Create a Configuration</span></span> ##

<span data-ttu-id="457a9-107">[**Konfigurációk** ](https://msdn.microsoft.com/en-us/powershell/dsc/configurations) környezet ismertető dokumentum.</span><span class="sxs-lookup"><span data-stu-id="457a9-107">[**Configurations**](https://msdn.microsoft.com/en-us/powershell/dsc/configurations) are documents that describe an environment.</span></span> <span data-ttu-id="457a9-108">Környezetek áll "**csomópontok**", amelyeket gyakran virtuális vagy fizikai gépek.</span><span class="sxs-lookup"><span data-stu-id="457a9-108">Environments consist of "**nodes**", which are commonly virtual or physical machines.</span></span> 

<span data-ttu-id="457a9-109">Az űrlap különböző konfigurációkat kerülhet.</span><span class="sxs-lookup"><span data-stu-id="457a9-109">Configurations can come in a variety of forms.</span></span> <span data-ttu-id="457a9-110">Az új konfiguráció létrehozásához legkönnyebben .ps1 (PowerShell-parancsfájl) fájl létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="457a9-110">The easiest way to create a new configuration is to create a .ps1 (PowerShell script) file.</span></span> <span data-ttu-id="457a9-111">Ehhez nyissa meg a választott szerkesztővel.</span><span class="sxs-lookup"><span data-stu-id="457a9-111">To do this, open your editor of choice.</span></span> <span data-ttu-id="457a9-112">A PowerShell ISE érdemes használni, mert DSC natív módon támogatja.</span><span class="sxs-lookup"><span data-stu-id="457a9-112">The PowerShell ISE is a good choice, since it understands DSC natively.</span></span> <span data-ttu-id="457a9-113">Mentse a PS1 a következőket:</span><span class="sxs-lookup"><span data-stu-id="457a9-113">Save the following as a PS1:</span></span>

```powershell
configuration MyFirstConfiguration
{
    Import-DscResource -Name WindowsFeature

    Node localhost
    {
        WindowsFeature IIS
        {
            Name = "IIS"

        }
        
    }

}
```
## <a name="parts-of-a-configuration"></a><span data-ttu-id="457a9-114">A konfiguráció részei</span><span class="sxs-lookup"><span data-stu-id="457a9-114">Parts of a Configuration</span></span> ##
<span data-ttu-id="457a9-115">**Konfigurációs** PowerShell 4.0-s hozzáadott kulcsszó.</span><span class="sxs-lookup"><span data-stu-id="457a9-115">**Configuration** is a keyword that has been added to PowerShell 4.0.</span></span> <span data-ttu-id="457a9-116">Azt jelzi, hogy olyan különleges célállapot-konfiguráció által használt PowerShell-függvény.</span><span class="sxs-lookup"><span data-stu-id="457a9-116">It signifies a special kind of PowerShell function used by Desired State Configuration.</span></span> <span data-ttu-id="457a9-117">Ebben a példában a függvény myFirstConfiguration neve.</span><span class="sxs-lookup"><span data-stu-id="457a9-117">In this example, the function is named myFirstConfiguration.</span></span> 

<span data-ttu-id="457a9-118">A következő sorban egy importálási utasítást, a modul importálása hasonlít.</span><span class="sxs-lookup"><span data-stu-id="457a9-118">The next line is an import statement, similar to importing a module.</span></span> <span data-ttu-id="457a9-119">Az tárgyalja később.</span><span class="sxs-lookup"><span data-stu-id="457a9-119">It will be discussed later on.</span></span>

<span data-ttu-id="457a9-120">"Csomópont" Ebben a konfigurációban fog működni a számítógép nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="457a9-120">"Node" defines the machine name this configuration will act on.</span></span> <span data-ttu-id="457a9-121">Bár ez a konfiguráció helyi szerkeszt, konfigurációk elérhetők a távoli csomópontokat, és konfigurálja őket.</span><span class="sxs-lookup"><span data-stu-id="457a9-121">Although this configuration is edited locally, configurations can reach out to remote nodes and configure them.</span></span> 

<span data-ttu-id="457a9-122">Csomópontok lehetnek a számítógép nevét vagy IP-címeket.</span><span class="sxs-lookup"><span data-stu-id="457a9-122">Nodes can be machine names or IP addresses.</span></span> <span data-ttu-id="457a9-123">Több csomópont lehet egy egyetlen konfigurációs dokumentumot.</span><span class="sxs-lookup"><span data-stu-id="457a9-123">You can have multiple nodes in a single configuration document.</span></span> <span data-ttu-id="457a9-124">Használatával [konfigurációs adatok](https://msdn.microsoft.com/en-us/powershell/dsc/configdata), ugyanaz a konfiguráció alkalmazása több csomópont is lehet.</span><span class="sxs-lookup"><span data-stu-id="457a9-124">Using [configuration data](https://msdn.microsoft.com/en-us/powershell/dsc/configdata), you can also have the same configuration apply to multiple nodes.</span></span> <span data-ttu-id="457a9-125">Ebben az esetben a csomópont nem "localhost" – ami azt jelenti, hogy a helyi számítógépen.</span><span class="sxs-lookup"><span data-stu-id="457a9-125">In this case, the node is "localhost" - which means the local computer.</span></span> 

<span data-ttu-id="457a9-126">A következő elem egy [ **erőforrás**](https://msdn.microsoft.com/en-us/powershell/dsc/resources).</span><span class="sxs-lookup"><span data-stu-id="457a9-126">The next item is a [**resource**](https://msdn.microsoft.com/en-us/powershell/dsc/resources).</span></span> <span data-ttu-id="457a9-127">Erőforrások konfigurációk építőelemei.</span><span class="sxs-lookup"><span data-stu-id="457a9-127">Resources are building blocks of configurations.</span></span> <span data-ttu-id="457a9-128">Minden erőforrás, amely meghatározza egy gép egyetlen aspektusa végrehajtási logikájának modul.</span><span class="sxs-lookup"><span data-stu-id="457a9-128">Each resource is a module that defines the implementation logic of a single aspect of a machine.</span></span> <span data-ttu-id="457a9-129">Megtekintheti minden erőforrás a számítógépen futó **Get-DscResource** a PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="457a9-129">You can view every resource on your machine by running **Get-DscResource** in PowerShell.</span></span> <span data-ttu-id="457a9-130">Erőforrások a helyi számítógépen jelen kell lennie, és konfigurációban való használat előtt importálni **Import-DscResource** Ez a konfiguráció a második sorban.</span><span class="sxs-lookup"><span data-stu-id="457a9-130">Resources must be present on the local machine and imported before they can be used in a configuration with **Import-DscResource** which is on the second line of this configuration.</span></span> 

<span data-ttu-id="457a9-131">**A konfiguráció életbe**</span><span class="sxs-lookup"><span data-stu-id="457a9-131">**Enacting a Configuration**</span></span>

<span data-ttu-id="457a9-132">A fenti parancsfájl menti, és futtassa, ha nincs kimenet gyűjtenek.</span><span class="sxs-lookup"><span data-stu-id="457a9-132">If the script above is saved and run, no output will be produced.</span></span> <span data-ttu-id="457a9-133">Ez a, mert a konfiguráció csak a következő függvényt, és a fenti parancsfájl a függvény definiálva van, de még nem futtatható.</span><span class="sxs-lookup"><span data-stu-id="457a9-133">This is because a configuration is just a function, and the script above has defined the function but not yet run it.</span></span> <span data-ttu-id="457a9-134">Miután a függvény definiálva van, a kell meghívni:</span><span class="sxs-lookup"><span data-stu-id="457a9-134">After the function is defined, it must be invoked:</span></span>
```powershell
myFirstConfiguration
```

<span data-ttu-id="457a9-135">Végrehajtásakor konfigurációs funkciók a konfiguráció ellenőrzése érvényes.</span><span class="sxs-lookup"><span data-stu-id="457a9-135">When executed, configuration functions validate the configuration is valid.</span></span> <span data-ttu-id="457a9-136">Nincsenek szintaktikai hibák rendelkeznie kell, és erőforrások rendelkeznie kell meghatározott összes kötelező paraméterek összes erőforrás végrehajtása előtt kell importálni.</span><span class="sxs-lookup"><span data-stu-id="457a9-136">It should have no syntax errors, resources should have all mandatory parameters defined, and all resources should be imported before execution.</span></span>

<span data-ttu-id="457a9-137">A konfigurációs végrehajtása, amennyiben azt egy mappát hoz létre a konfigurációs tartalmazó nevű egy **. MOF-fájlt** a konfiguráció minden csomópontján.</span><span class="sxs-lookup"><span data-stu-id="457a9-137">Once the configuration is executed, it creates a folder with the name of the configuration containing a **.MOF file** for every node in the configuration.</span></span> <span data-ttu-id="457a9-138">A. MOF-fájlt a hálózaton keresztül kommunikálnak a PowerShell DSC által használt szabványalapú felügyeleti formátumban.</span><span class="sxs-lookup"><span data-stu-id="457a9-138">The .MOF file is a standards-based management format which is used by PowerShell DSC to communicate over the network.</span></span>

<span data-ttu-id="457a9-139">A konfiguráció életbe léptetni:</span><span class="sxs-lookup"><span data-stu-id="457a9-139">To enact the configuration:</span></span>
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration
```
<span data-ttu-id="457a9-140">Ezzel létrehoz egy PowerShell feladat egészítse ki a konfigurációs csomópontjaihoz, és konfigurálja azokat.</span><span class="sxs-lookup"><span data-stu-id="457a9-140">This creates a PowerShell job that reaches out to the nodes in the configuration and configures them.</span></span> <span data-ttu-id="457a9-141">A feladat eredményének megtekintéséhez használja a-Wait.</span><span class="sxs-lookup"><span data-stu-id="457a9-141">To see the output of the job, use -Wait.</span></span> 
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration -Wait
```

