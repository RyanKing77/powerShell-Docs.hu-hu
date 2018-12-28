---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Rövid útmutató – a DSC-s webhely létrehozása
ms.openlocfilehash: c62e2d8af46bf74c4dd13069ddff6cc39763a209
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404144"
---
> <span data-ttu-id="baac2-103">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="baac2-103">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

# <a name="quickstart---create-a-website-with-dsc"></a><span data-ttu-id="baac2-104">Rövid útmutató – a DSC-s webhely létrehozása</span><span class="sxs-lookup"><span data-stu-id="baac2-104">Quickstart - Create a website with DSC</span></span>

<span data-ttu-id="baac2-105">Ebben a gyakorlatban létrehozásával és alkalmazásával a Desired State Configuration (DSC) konfigurációs elejétől a végéig ismerteti.</span><span class="sxs-lookup"><span data-stu-id="baac2-105">This exercise walks through creating and applying a Desired State Configuration (DSC) configuration from start to finish.</span></span>
<span data-ttu-id="baac2-106">A példában használunk biztosítja, hogy a kiszolgáló rendelkezik-e a `Web-Server` (IIS) szolgáltatás engedélyezve van, és egy egyszerű "Hello World" webhely tartalmának szerepel a `intepub\wwwroot` könyvtárat, az adott kiszolgáló.</span><span class="sxs-lookup"><span data-stu-id="baac2-106">The example we'll use ensures that a server has the `Web-Server` (IIS) feature enabled, and that the content for a simple "Hello World" website is present in the `intepub\wwwroot` directory of that server.</span></span>

<span data-ttu-id="baac2-107">DSC és működésének áttekintését lásd: [Desired State Configuration áttekintése döntéshozók számára](../overview/decisionMaker.md).</span><span class="sxs-lookup"><span data-stu-id="baac2-107">For an overview of what DSC is and how it works, see [Desired State Configuration Overview for Decision Makers](../overview/decisionMaker.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="baac2-108">Követelmények</span><span class="sxs-lookup"><span data-stu-id="baac2-108">Requirements</span></span>

<span data-ttu-id="baac2-109">Ez a példa futtatásához szüksége lesz egy Windows Server 2012 vagy újabb verzió és a PowerShell 4.0-s vagy újabb rendszert futtató számítógép.</span><span class="sxs-lookup"><span data-stu-id="baac2-109">To run this example, you will need a computer running Windows Server 2012 or later and PowerShell 4.0 or later.</span></span>

## <a name="write-and-place-the-indexhtm-file"></a><span data-ttu-id="baac2-110">Írhat, és helyezze a index.HTML fájlt</span><span class="sxs-lookup"><span data-stu-id="baac2-110">Write and place the index.htm file</span></span>

<span data-ttu-id="baac2-111">Először a HTML-fájl, amely a webhely tartalmát, ezzel hozunk létre.</span><span class="sxs-lookup"><span data-stu-id="baac2-111">First, we'll create the HTML file that we will use as the website content.</span></span>

<span data-ttu-id="baac2-112">A legfelső szintű mappában hozza létre a `test`.</span><span class="sxs-lookup"><span data-stu-id="baac2-112">In your root folder, create a folder named `test`.</span></span>

<span data-ttu-id="baac2-113">Egy szövegszerkesztőben írja be a következőket:</span><span class="sxs-lookup"><span data-stu-id="baac2-113">In a text editor, type the following text:</span></span>

```html
<head></head>
<body>
<p>Hello World!</p>
</body>
```

<span data-ttu-id="baac2-114">Mentse ezt `index.htm` a a `test` korábban létrehozott mappába.</span><span class="sxs-lookup"><span data-stu-id="baac2-114">Save this as `index.htm` in the `test` folder you created earlier.</span></span>

## <a name="write-the-configuration"></a><span data-ttu-id="baac2-115">A konfiguráció írása</span><span class="sxs-lookup"><span data-stu-id="baac2-115">Write the configuration</span></span>

<span data-ttu-id="baac2-116">A [DSC-konfiguráció](../configurations/configurations.md) egy külön PowerShell-függvény, amely meghatározza, hogyan szeretné konfigurálni egy vagy több cél számítógépek (csomópontok).</span><span class="sxs-lookup"><span data-stu-id="baac2-116">A [DSC configuration](../configurations/configurations.md) is a special PowerShell function that defines how you want to configure one or more target computers (nodes).</span></span>

<span data-ttu-id="baac2-117">A PowerShell ISE-ben írja be a következőt:</span><span class="sxs-lookup"><span data-stu-id="baac2-117">In the PowerShell ISE, type the following:</span></span>

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

<span data-ttu-id="baac2-118">Mentse a fájlt az `WebsiteTest.ps1`.</span><span class="sxs-lookup"><span data-stu-id="baac2-118">Save the file as `WebsiteTest.ps1`.</span></span>

<span data-ttu-id="baac2-119">Láthatja, hogy hasonlóan néz ki egy PowerShell-függvény, a kulcsszó azonban kiegészül **konfigurációs** előtt a függvény nevét használja.</span><span class="sxs-lookup"><span data-stu-id="baac2-119">You can see that it looks like a PowerShell function, with the addition of the keyword **Configuration** used before the name of the function.</span></span>

<span data-ttu-id="baac2-120">A **csomópont** letiltása, adja meg a célcsomópont konfigurálását, ebben az esetben `localhost`.</span><span class="sxs-lookup"><span data-stu-id="baac2-120">The **Node** block specifies the target node to be configured, in this case `localhost`.</span></span>

<span data-ttu-id="baac2-121">A konfiguráció meghívja a két [erőforrások](../resources/resources.md), **WindowsFeature** és **fájl**.</span><span class="sxs-lookup"><span data-stu-id="baac2-121">The configuration calls two [resources](../resources/resources.md), **WindowsFeature** and **File**.</span></span>
<span data-ttu-id="baac2-122">Erőforrások teheti meg, hiszen a munkát, a célcsomópont a konfiguráció által meghatározott állapotban van.</span><span class="sxs-lookup"><span data-stu-id="baac2-122">Resources do the work of ensuring that the target node is in the state defined by the configuration.</span></span>

## <a name="compile-the-configuration"></a><span data-ttu-id="baac2-123">A konfiguráció fordítása</span><span class="sxs-lookup"><span data-stu-id="baac2-123">Compile the configuration</span></span>

<span data-ttu-id="baac2-124">DSC csomópont alkalmazandó konfiguráció azt először kell összeállítani egy MOF-fájlba.</span><span class="sxs-lookup"><span data-stu-id="baac2-124">For a DSC configuration to be applied to a node, it must first be compiled into a MOF file.</span></span>
<span data-ttu-id="baac2-125">Ehhez futtassa a konfiguráció, például egy függvényt.</span><span class="sxs-lookup"><span data-stu-id="baac2-125">To do this, you run the configuration like a function.</span></span>
<span data-ttu-id="baac2-126">A PowerShell-konzolt ugyanabba a mappába, ahová mentette a konfiguráció keresse meg és futtassa a következő parancsokat egy MOF-fájlba konfiguráció fordítása:</span><span class="sxs-lookup"><span data-stu-id="baac2-126">In a PowerShell console, navigate to the same folder where you saved your configuration and run the following commands to compile the configuration into a MOF file:</span></span>

```powershell
. .\WebsiteTest.ps1
WebsiteTest
```

<span data-ttu-id="baac2-127">Ez létrehozza a következő kimenet:</span><span class="sxs-lookup"><span data-stu-id="baac2-127">This generates the following output:</span></span>

```
Directory: C:\ConfigurationTest\WebsiteTest


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

<span data-ttu-id="baac2-128">Az első sor elérhetővé teszi a konfigurációs funkció a konzolon.</span><span class="sxs-lookup"><span data-stu-id="baac2-128">The first line makes the configuration function available in the console.</span></span>
<span data-ttu-id="baac2-129">A második sor fut, a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="baac2-129">The second line runs the configuration.</span></span>
<span data-ttu-id="baac2-130">Az eredménye, hogy egy új mappát nevű `WebsiteTest` jön létre, az aktuális mappa egy almappájában.</span><span class="sxs-lookup"><span data-stu-id="baac2-130">The result is that a new folder, named `WebsiteTest` is created as a subfolder of the current folder.</span></span>
<span data-ttu-id="baac2-131">A `WebsiteTest` mappa tartalmaz egy fájlt `localhost.mof`.</span><span class="sxs-lookup"><span data-stu-id="baac2-131">The `WebsiteTest` folder contains a file named `localhost.mof`.</span></span>
<span data-ttu-id="baac2-132">Ezt a fájlt, majd alkalmazható a cél csomópontra.</span><span class="sxs-lookup"><span data-stu-id="baac2-132">It is this file that can then be applied to the target node.</span></span>

## <a name="apply-the-configuration"></a><span data-ttu-id="baac2-133">A konfiguráció alkalmazásához</span><span class="sxs-lookup"><span data-stu-id="baac2-133">Apply the configuration</span></span>

<span data-ttu-id="baac2-134">Most, hogy a lefordított MOF, alkalmazhat a konfigurációt a célcsomópont (ebben az esetben az a helyi számítógép) meghívásával a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="baac2-134">Now that you have the compiled MOF, you can apply the configuration to the target node (in this case, the local computer) by calling the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span>

<span data-ttu-id="baac2-135">A `Start-DscConfiguration` arra utasítja a parancsmag a [helyi Configuration Manager (LCM) Konfigurálása](../managing-nodes/metaConfig.md), azaz a a alkalmazni a konfigurációt a DSC motor.</span><span class="sxs-lookup"><span data-stu-id="baac2-135">The `Start-DscConfiguration` cmdlet tells the [Local Configuration Manager (LCM)](../managing-nodes/metaConfig.md), which is the engine of DSC, to apply the configuration.</span></span>
<span data-ttu-id="baac2-136">Az LCM Konfigurálása a alkalmazni a konfigurációt a DSC-erőforrások hívása működik.</span><span class="sxs-lookup"><span data-stu-id="baac2-136">The LCM does the work of calling the DSC resources to apply the configuration.</span></span>

<span data-ttu-id="baac2-137">Az a PowerShell-konzolt keresse meg ugyanabba a mappába, ahová mentette a konfigurációt, és futtassa a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="baac2-137">In a PowerShell console, navigate to the same folder where you saved your configuration and run the following command:</span></span>

```powershell
Start-DscConfiguration .\WebsiteTest
```

## <a name="test-the-configuration"></a><span data-ttu-id="baac2-138">A konfiguráció tesztelése</span><span class="sxs-lookup"><span data-stu-id="baac2-138">Test the configuration</span></span>

<span data-ttu-id="baac2-139">Hívása a [Get-DscConfigurationStatus](/powershell/module/psdesiredstateconfiguration/get-dscconfigurationstatus) parancsmaggal ellenőrizheti, hogy sikerült-e a konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="baac2-139">You can call the [Get-DscConfigurationStatus](/powershell/module/psdesiredstateconfiguration/get-dscconfigurationstatus) cmdlet to see whether the configuration succeeded.</span></span>

<span data-ttu-id="baac2-140">Is tesztelheti az eredményeket közvetlenül, ebben az esetben megkeresve `http://localhost/` egy webböngészőben.</span><span class="sxs-lookup"><span data-stu-id="baac2-140">You can also test the results directly, in this case by browsing to `http://localhost/` in a web browser.</span></span>
<span data-ttu-id="baac2-141">Ez a példa első lépéseként kell megjelennie a "Hello World" HTML-lap hozott létre.</span><span class="sxs-lookup"><span data-stu-id="baac2-141">You should see the "Hello World" HTML page you created as the first step in this example.</span></span>

## <a name="next-steps"></a><span data-ttu-id="baac2-142">További lépések</span><span class="sxs-lookup"><span data-stu-id="baac2-142">Next steps</span></span>

- <span data-ttu-id="baac2-143">További információk a DSC-konfigurációk [DSC-konfigurációk](../configurations/configurations.md).</span><span class="sxs-lookup"><span data-stu-id="baac2-143">Find out more about DSC configurations at [DSC configurations](../configurations/configurations.md).</span></span>
- <span data-ttu-id="baac2-144">Megtudhatja, milyen DSC-erőforrás áll rendelkezésre, és hogyan hozhat létre egyéni DSC-erőforrásokat, [DSC-erőforrások](../resources/resources.md).</span><span class="sxs-lookup"><span data-stu-id="baac2-144">See what DSC resources are available, and how to create custom DSC resources at [DSC resources](../resources/resources.md).</span></span>
- <span data-ttu-id="baac2-145">DSC-konfigurációkat és erőforrásokat a [PowerShell-galériából](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="baac2-145">Find DSC configurations and resources in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
