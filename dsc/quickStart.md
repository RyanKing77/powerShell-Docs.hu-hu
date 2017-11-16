---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Szükségeskonfiguráció-State Configuration – első lépések"
ms.openlocfilehash: 295a78f3fd85464239d51d7be0defa04d2344689
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/13/2017
---
> <span data-ttu-id="0e20a-103">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="0e20a-103">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

# <a name="desired-state-configuration-quick-start"></a><span data-ttu-id="0e20a-104">Szükségeskonfiguráció-State Configuration – első lépések</span><span class="sxs-lookup"><span data-stu-id="0e20a-104">Desired State Configuration Quick Start</span></span>

<span data-ttu-id="0e20a-105">Ebben a gyakorlatban végigvezeti a létrehozásával és alkalmazásával a kívánt állapot konfigurációs szolgáltatása (DSC) konfigurációs kezdetétől a végéig.</span><span class="sxs-lookup"><span data-stu-id="0e20a-105">This exercise walks through creating and applying a Desired State Configuration (DSC) configuration from start to finish.</span></span>
<span data-ttu-id="0e20a-106">A példában használjuk biztosítja, hogy a kiszolgáló rendelkezik-e a `Web-Server` (IIS) engedélyezve van, és egy egyszerű "Hello, World" webhely tartalmának megtalálható-e a `intepub\wwwroot` mappában található a kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="0e20a-106">The example we'll use ensures that a server has the `Web-Server` (IIS) feature enabled, and that the content for a simple "Hello World" website is present in the `intepub\wwwroot` directory of that server.</span></span>

<span data-ttu-id="0e20a-107">A DSC-ből és annak működéséről áttekintését lásd: [kívánt állapot konfigurációs áttekintése döntéshozók](decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="0e20a-107">For an overview of what DSC is and how it works, see [Desired State Configuration Overview for Decision Makers](decisionMaker.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="0e20a-108">Követelmények</span><span class="sxs-lookup"><span data-stu-id="0e20a-108">Requirements</span></span>

<span data-ttu-id="0e20a-109">A példa futtatásához, szüksége lesz egy Windows Server 2012 vagy újabb és PowerShell 4.0-s vagy újabb rendszert futtató számítógép.</span><span class="sxs-lookup"><span data-stu-id="0e20a-109">To run this example, you will need a computer running Windows Server 2012 or later and PowerShell 4.0 or later.</span></span>

## <a name="write-and-place-the-indexhtm-file"></a><span data-ttu-id="0e20a-110">Írása, és helyezze a index.HTML fájlt</span><span class="sxs-lookup"><span data-stu-id="0e20a-110">Write and place the index.htm file</span></span>

<span data-ttu-id="0e20a-111">Először létrehozunk fogjuk használni, a webhely tartalmát a HTML-fájlba.</span><span class="sxs-lookup"><span data-stu-id="0e20a-111">First, we'll create the HTML file that we will use as the website content.</span></span>

<span data-ttu-id="0e20a-112">A legfelső szintű mappában hozza létre a `test`.</span><span class="sxs-lookup"><span data-stu-id="0e20a-112">In your root folder, create a folder named `test`.</span></span>

<span data-ttu-id="0e20a-113">Egy szövegszerkesztőben írja be a következőket:</span><span class="sxs-lookup"><span data-stu-id="0e20a-113">In a text editor, type the following text:</span></span>

```html
<head></head>
<body>
<p>Hello World!</p>
</body>
```

<span data-ttu-id="0e20a-114">Mentse ezt `index.htm` a a `test` korábban létrehozott mappába.</span><span class="sxs-lookup"><span data-stu-id="0e20a-114">Save this as `index.htm` in the `test` folder you created earlier.</span></span> 

## <a name="write-the-configuration"></a><span data-ttu-id="0e20a-115">A konfiguráció írásakor</span><span class="sxs-lookup"><span data-stu-id="0e20a-115">Write the configuration</span></span>

<span data-ttu-id="0e20a-116">A [DSC-konfiguráció](configurations.md) különleges PowerShell függvény, amely meghatározza, hogyan szeretné konfigurálni egy vagy több cél számítógépek (csomópontok).</span><span class="sxs-lookup"><span data-stu-id="0e20a-116">A [DSC configuration](configurations.md) is a special PowerShell function that defines how you want to configure one or more target computers (nodes).</span></span>

<span data-ttu-id="0e20a-117">A PowerShell ISE írja be a következőt:</span><span class="sxs-lookup"><span data-stu-id="0e20a-117">In the PowerShell ISE, type the following:</span></span>

```powershell
Configuration WebsiteTest {

    # Import the module that contains the resources we're using.
    Import-DscResource -ModuleName PsDesiredStateConfiguration

    # The Node statement specifies which targets this configuration will be applied to.
    Node 'localhost' {

        # The first resource block ensures that the Web-Server (IIS) feature is enabled.
        WindowsFeature WebServer {
            Ensure = "Present"
            Name   = "Web-Server"
        }

        # The second resource block ensures that the website content copied to the website root folder.
        File WebsiteContent {
            Ensure = 'Present'
            SourcePath = 'c:\test\index.htm'
            DestinationPath = 'c:\inetpub\wwwroot'
        }
    }
}
```

<span data-ttu-id="0e20a-118">Mentse a fájlt `WebsiteTest.ps1`.</span><span class="sxs-lookup"><span data-stu-id="0e20a-118">Save the file as `WebsiteTest.ps1`.</span></span>

<span data-ttu-id="0e20a-119">Láthatja, hogy úgy tűnik, a kulcsszó azonban kiegészül a PowerShell függvény **konfigurációs** a függvény neve előtt használt.</span><span class="sxs-lookup"><span data-stu-id="0e20a-119">You can see that it looks like a PowerShell function, with the addition of the keyword **Configuration** used before the name of the function.</span></span>

<span data-ttu-id="0e20a-120">A **csomópont** blokk megadja a célcsomópont konfigurálását, ebben az esetben `localhost`.</span><span class="sxs-lookup"><span data-stu-id="0e20a-120">The **Node** block specifies the target node to be configured, in this case `localhost`.</span></span>

<span data-ttu-id="0e20a-121">A konfigurációs meghívja a két [erőforrások](resources.md), [WindowsFeature](windowsFeatureResource.md) és [fájl](fileResource.md).</span><span class="sxs-lookup"><span data-stu-id="0e20a-121">The configuration calls two [resources](resources.md), [WindowsFeature](windowsFeatureResource.md) and [File](fileResource.md).</span></span>
<span data-ttu-id="0e20a-122">Erőforrások munkájuk a annak biztosítására, hogy, hogy a célcsomópont a konfiguráció által meghatározott állapotban van.</span><span class="sxs-lookup"><span data-stu-id="0e20a-122">Resources do the work of ensuring that the target node is in the state defined by the configuration.</span></span>

## <a name="compile-the-configuration"></a><span data-ttu-id="0e20a-123">A konfiguráció-fordítási</span><span class="sxs-lookup"><span data-stu-id="0e20a-123">Compile the configuration</span></span>

<span data-ttu-id="0e20a-124">A DSC-konfiguráció egy csomópont alkalmazandó azt kell először fordítható MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="0e20a-124">For a DSC configuration to be applied to a node, it must first be compiled into a MOF file.</span></span>
<span data-ttu-id="0e20a-125">Ehhez futtassa a konfiguráció, például egy olyan függvényt.</span><span class="sxs-lookup"><span data-stu-id="0e20a-125">To do this, you run the configuration like a function.</span></span>
<span data-ttu-id="0e20a-126">PowerShell-konzolban navigáljon a ugyanabba a mappába, ahová menteni szeretné a konfigurációt, és futtassa az alábbi parancsokat a MOF-fájlba konfiguráció-fordítási:</span><span class="sxs-lookup"><span data-stu-id="0e20a-126">In a PowerShell console, navigate to the same folder where you saved your configuration and run the following commands to compile the configuration into a MOF file:</span></span>

```powershell
. .\WebsiteTest.ps1
WebsiteTest
```

<span data-ttu-id="0e20a-127">Ezt követően a következő az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="0e20a-127">This generates the following output:</span></span>

```
Directory: C:\ConfigurationTest\WebsiteTest


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

<span data-ttu-id="0e20a-128">Az első sor elérhetővé teszi a konfigurációs függvény a konzolon.</span><span class="sxs-lookup"><span data-stu-id="0e20a-128">The first line makes the configuration function available in the console.</span></span>
<span data-ttu-id="0e20a-129">A második sor fut, a konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="0e20a-129">The second line runs the configuration.</span></span>
<span data-ttu-id="0e20a-130">Az eredménye, hogy egy új mappát nevű `WebsiteTest` megegyezik az aktuális mappában jön létre.</span><span class="sxs-lookup"><span data-stu-id="0e20a-130">The result is that a new folder, named `WebsiteTest` is created as a subfolder of the current folder.</span></span>
<span data-ttu-id="0e20a-131">A `WebsiteTest` mappa tartalmaz egy nevű fájlt `localhost.mof`.</span><span class="sxs-lookup"><span data-stu-id="0e20a-131">The `WebsiteTest` folder contains a file named `localhost.mof`.</span></span>
<span data-ttu-id="0e20a-132">Ezt a fájlt, majd a célcsomópont alkalmazhatja.</span><span class="sxs-lookup"><span data-stu-id="0e20a-132">It is this file that can then be applied to the target node.</span></span>

## <a name="apply-the-configuration"></a><span data-ttu-id="0e20a-133">A konfiguráció alkalmazásához</span><span class="sxs-lookup"><span data-stu-id="0e20a-133">Apply the configuration</span></span>

<span data-ttu-id="0e20a-134">Most, hogy a lefordított MOF, alkalmazhat a konfiguráció célcsomóponton (ebben az esetben, a helyi számítógép) meghívásával a [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="0e20a-134">Now that you have the compiled MOF, you can apply the configuration to the target node (in this case, the local computer) by calling the [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration) cmdlet.</span></span>

<span data-ttu-id="0e20a-135">A `Start-DscConfiguration` parancsmag közli a [helyi Configuration Manager (LCM)](metaConfig.md), vagyis a DSC-ből, a beállítások-motor.</span><span class="sxs-lookup"><span data-stu-id="0e20a-135">The `Start-DscConfiguration` cmdlet tells the [Local Configuration Manager (LCM)](metaConfig.md), which is the engine of DSC, to apply the configuration.</span></span>
<span data-ttu-id="0e20a-136">A LCM e történt a DSC-erőforrások, a beállítások a munkáját.</span><span class="sxs-lookup"><span data-stu-id="0e20a-136">The LCM does the work of calling the DSC resources to apply the configuration.</span></span>

<span data-ttu-id="0e20a-137">PowerShell-konzolban navigáljon a ugyanabba a mappába, ahová menteni szeretné a konfigurációt, és futtassa a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="0e20a-137">In a PowerShell console, navigate to the same folder where you saved your configuration and run the following command:</span></span>

```powershell
Start-DscConfiguration .\WebsiteTest
```

## <a name="test-the-configuration"></a><span data-ttu-id="0e20a-138">Tesztelje a konfigurációt</span><span class="sxs-lookup"><span data-stu-id="0e20a-138">Test the configuration</span></span>

<span data-ttu-id="0e20a-139">Hívása a [Get-DscConfigurationStatus](/reference/5.1/PSDesiredStateConfiguration/Get-DscConfigurationStatus) parancsmag használatával ellenőrizheti, hogy a konfiguráció sikeres volt.</span><span class="sxs-lookup"><span data-stu-id="0e20a-139">You can call the [Get-DscConfigurationStatus](/reference/5.1/PSDesiredStateConfiguration/Get-DscConfigurationStatus) cmdlet to see whether the configuration succeeded.</span></span> 

<span data-ttu-id="0e20a-140">Is tesztelheti az eredmények közvetlenül, ebben az esetben tallózással `http://localhost/` egy webböngészőben.</span><span class="sxs-lookup"><span data-stu-id="0e20a-140">You can also test the results directly, in this case by browsing to `http://localhost/` in a web browser.</span></span>
<span data-ttu-id="0e20a-141">Ez a példa első lépéseként meg kell jelennie a létrehozott "Hello World" HTML-lapon.</span><span class="sxs-lookup"><span data-stu-id="0e20a-141">You should see the "Hello World" HTML page you created as the first step in this example.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e20a-142">További lépések</span><span class="sxs-lookup"><span data-stu-id="0e20a-142">Next steps</span></span>

- <span data-ttu-id="0e20a-143">További információk a DSC-konfigurációk [a DSC-konfigurációk](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="0e20a-143">Find out more about DSC configurations at [DSC configurations](configurations.md).</span></span>
- <span data-ttu-id="0e20a-144">Milyen DSC erőforrások elérhetők, és egyéni DSC erőforrások létrehozása [DSC erőforrások](resources.md).</span><span class="sxs-lookup"><span data-stu-id="0e20a-144">See what DSC resources are available, and how to create custom DSC resources at [DSC resources](resources.md).</span></span>
- <span data-ttu-id="0e20a-145">A DSC-konfigurációk és az erőforrások megkeresése a [PowerShell-galériában](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="0e20a-145">Find DSC configurations and resources in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>



