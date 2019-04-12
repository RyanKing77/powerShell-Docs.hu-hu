---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfiguráció, a szolgáltatás, a telepítő
title: Konfiguráció írása, fordítása és alkalmazása
ms.openlocfilehash: 947308efa165543571801c88a922daf44fa88be0
ms.sourcegitcommit: 3f6002e7109373eda31cc65fc84d2600447cb7e9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/11/2019
ms.locfileid: "59506818"
---
> <span data-ttu-id="1f233-103">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1f233-103">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

# <a name="write-compile-and-apply-a-configuration"></a><span data-ttu-id="1f233-104">Konfiguráció írása, fordítása és alkalmazása</span><span class="sxs-lookup"><span data-stu-id="1f233-104">Write, Compile, and Apply a Configuration</span></span>

<span data-ttu-id="1f233-105">Ebben a gyakorlatban létrehozásával és alkalmazásával a Desired State Configuration (DSC) konfigurációs elejétől a végéig ismerteti.</span><span class="sxs-lookup"><span data-stu-id="1f233-105">This exercise walks through creating and applying a Desired State Configuration (DSC) configuration from start to finish.</span></span>
<span data-ttu-id="1f233-106">A következő példában, megtudhatja, hogyan írhat, és a egy nagyon egyszerű konfiguráció alkalmazása.</span><span class="sxs-lookup"><span data-stu-id="1f233-106">In the following example, you will learn how to write and apply a very simple Configuration.</span></span> <span data-ttu-id="1f233-107">A konfiguráció biztosítja, hogy a "HelloWorld.txt" fájl létezik a helyi gépen.</span><span class="sxs-lookup"><span data-stu-id="1f233-107">The Configuration will ensure a "HelloWorld.txt" file exists on your local machine.</span></span> <span data-ttu-id="1f233-108">Ha a fájl törléséhez DSC létrehozza azt a következő alkalommal, amikor frissíti.</span><span class="sxs-lookup"><span data-stu-id="1f233-108">If you delete the file, DSC will recreate it the next time it updates.</span></span>

<span data-ttu-id="1f233-109">DSC és működésének áttekintését lásd: [Desired State Configuration áttekintése fejlesztők számára](../overview/overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f233-109">For an overview of what DSC is and how it works, see [Desired State Configuration Overview for Developers](../overview/overview.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="1f233-110">Követelmények</span><span class="sxs-lookup"><span data-stu-id="1f233-110">Requirements</span></span>

<span data-ttu-id="1f233-111">Ez a példa futtatásához szüksége lesz a futtató PowerShell 4.0-s vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="1f233-111">To run this example, you will need a computer running PowerShell 4.0 or later.</span></span>

## <a name="write-the-configuration"></a><span data-ttu-id="1f233-112">A konfiguráció írása</span><span class="sxs-lookup"><span data-stu-id="1f233-112">Write the configuration</span></span>

<span data-ttu-id="1f233-113">A DSC [konfigurációs](configurations.md) egy külön PowerShell-függvény, amely meghatározza, hogyan szeretné konfigurálni egy vagy több cél számítógépek (csomópontok).</span><span class="sxs-lookup"><span data-stu-id="1f233-113">A DSC [Configuration](configurations.md) is a special PowerShell function that defines how you want to configure one or more target computers (Nodes).</span></span>

<span data-ttu-id="1f233-114">A PowerShell ISE-ben, vagy más PowerShell-szerkesztő írja be a következőt:</span><span class="sxs-lookup"><span data-stu-id="1f233-114">In the PowerShell ISE, or other PowerShell editor, type the following:</span></span>

```powershell
Configuration HelloWorld {

    # Import the module that contains the File resource.
    Import-DscResource -ModuleName PsDesiredStateConfiguration

    # The Node statement specifies which targets to compile MOF files for, when this configuration is executed.
    Node 'localhost' {

        # The File resource can ensure the state of files, or copy them from a source to a destination with persistent updates.
        File HelloWorld {
            DestinationPath = "C:\Temp\HelloWorld.txt"
            Ensure = "Present"
            Contents   = "Hello World from DSC!"
        }
    }
}
```

<span data-ttu-id="1f233-115">Mentse a fájlt "HelloWorld.ps1".</span><span class="sxs-lookup"><span data-stu-id="1f233-115">Save the file as "HelloWorld.ps1".</span></span>

<span data-ttu-id="1f233-116">Konfiguráció definiálása olyan, mint egy függvény meghatározása.</span><span class="sxs-lookup"><span data-stu-id="1f233-116">Defining a Configuration is like defining a Function.</span></span> <span data-ttu-id="1f233-117">A **csomópont** letiltása, adja meg a célcsomópont konfigurálását, ebben az esetben `localhost`.</span><span class="sxs-lookup"><span data-stu-id="1f233-117">The **Node** block specifies the target node to be configured, in this case `localhost`.</span></span>

<span data-ttu-id="1f233-118">A konfiguráció meghívja az egyiket [erőforrások](../resources/resources.md), a `File` erőforrás.</span><span class="sxs-lookup"><span data-stu-id="1f233-118">The configuration calls one [resources](../resources/resources.md), the `File` resource.</span></span> <span data-ttu-id="1f233-119">Erőforrások teheti meg, hiszen a munkát, a célcsomópont a konfiguráció által meghatározott állapotban van.</span><span class="sxs-lookup"><span data-stu-id="1f233-119">Resources do the work of ensuring that the target node is in the state defined by the configuration.</span></span>

## <a name="compile-the-configuration"></a><span data-ttu-id="1f233-120">A konfiguráció fordítása</span><span class="sxs-lookup"><span data-stu-id="1f233-120">Compile the configuration</span></span>

<span data-ttu-id="1f233-121">DSC csomópont alkalmazandó konfiguráció azt először kell összeállítani egy MOF-fájlba.</span><span class="sxs-lookup"><span data-stu-id="1f233-121">For a DSC configuration to be applied to a node, it must first be compiled into a MOF file.</span></span>
<span data-ttu-id="1f233-122">A konfiguráció, például egy függvényt, futtató lefordítása fog egy ".mof" fájl által definiált minden csomópont esetében a `Node` letiltása.</span><span class="sxs-lookup"><span data-stu-id="1f233-122">Running the configuration, like a function, will compile one ".mof" file for every Node defined by the `Node` block.</span></span>
<span data-ttu-id="1f233-123">Futtassa a konfigurációt, kell *pont forrás* a "HelloWorld.ps1" parancsfájlt az aktuális hatókörben.</span><span class="sxs-lookup"><span data-stu-id="1f233-123">In order to run the configuration, you need to *dot source* your "HelloWorld.ps1" script into the current scope.</span></span>
<span data-ttu-id="1f233-124">További információkért lásd: [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts?view=powershell-6#script-scope-and-dot-sourcing).</span><span class="sxs-lookup"><span data-stu-id="1f233-124">For more information, see [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts?view=powershell-6#script-scope-and-dot-sourcing).</span></span>

<!-- markdownlint-disable MD038 -->
<span data-ttu-id="1f233-125">*Pont forrás* az elérési út helyétől, után írja be a "HelloWorld.ps1" parancsfájl a `. ` (pont, terület).</span><span class="sxs-lookup"><span data-stu-id="1f233-125">*Dot source* your "HelloWorld.ps1" script by typing in the path where you stored it, after the `. ` (dot, space).</span></span> <span data-ttu-id="1f233-126">A következő lehetőségekkel, majd futtassa a konfiguráció például függvény meghívásával.</span><span class="sxs-lookup"><span data-stu-id="1f233-126">You may then, run your configuration by calling it like a Function.</span></span>
<!-- markdownlint-enable MD038 -->

```powershell
. C:\Scripts\HelloWorld.ps1
HelloWorld
```

<span data-ttu-id="1f233-127">Ez létrehozza a következő kimenet:</span><span class="sxs-lookup"><span data-stu-id="1f233-127">This generates the following output:</span></span>

```output
Directory: C:\Scripts\HelloWorld


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

## <a name="apply-the-configuration"></a><span data-ttu-id="1f233-128">A konfiguráció alkalmazásához</span><span class="sxs-lookup"><span data-stu-id="1f233-128">Apply the configuration</span></span>

<span data-ttu-id="1f233-129">Most, hogy a lefordított MOF, alkalmazhat a konfigurációt a célcsomópont (ebben az esetben az a helyi számítógép) meghívásával a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1f233-129">Now that you have the compiled MOF, you can apply the configuration to the target node (in this case, the local computer) by calling the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span>

<span data-ttu-id="1f233-130">A `Start-DscConfiguration` arra utasítja a parancsmag a [helyi Configuration Manager (LCM) Konfigurálása](../managing-nodes/metaConfig.md), DSC, a alkalmazni a konfigurációt motorját.</span><span class="sxs-lookup"><span data-stu-id="1f233-130">The `Start-DscConfiguration` cmdlet tells the [Local Configuration Manager (LCM)](../managing-nodes/metaConfig.md), the engine of DSC, to apply the configuration.</span></span>
<span data-ttu-id="1f233-131">Az LCM Konfigurálása a alkalmazni a konfigurációt a DSC-erőforrások hívása működik.</span><span class="sxs-lookup"><span data-stu-id="1f233-131">The LCM does the work of calling the DSC resources to apply the configuration.</span></span>

<span data-ttu-id="1f233-132">Az alábbi kód használatával hajtsa végre a `Start-DSCConfiguration` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1f233-132">Use the code below to execute the `Start-DSCConfiguration` cmdlet.</span></span> <span data-ttu-id="1f233-133">Adja meg a könyvtár elérési útja a "localhost.mof" tárolódnak, a `-Path` paraméter.</span><span class="sxs-lookup"><span data-stu-id="1f233-133">Specify the directory path where your "localhost.mof" is stored to the `-Path` parameter.</span></span> <span data-ttu-id="1f233-134">A `Start-DSCConfiguration` parancsmag átvizsgálja a megadott "\<computername\>.mof" fájlokat.</span><span class="sxs-lookup"><span data-stu-id="1f233-134">The `Start-DSCConfiguration` cmdlet looks through the directory specified for any "\<computername\>.mof" files.</span></span> <span data-ttu-id="1f233-135">A `Start-DSCConfiguration` parancsmag megkísérli minden ".mof" fájlt megtalálta a alkalmazni a számítógépnév, a fájlnév ("localhost", "kiszolgalo01", "tartományvezérlő-02", stb.) által meghatározott.</span><span class="sxs-lookup"><span data-stu-id="1f233-135">The `Start-DSCConfiguration` cmdlet attempts to apply each ".mof" file it finds to the computername specified by the filename ("localhost", "server01", "dc-02", etc.).</span></span>

> [!NOTE]
> <span data-ttu-id="1f233-136">Ha a `-Wait` paraméter nincs megadva, `Start-DSCConfiguration` létrehoz egy háttérben futó feladatot, a művelet végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="1f233-136">If the `-Wait` parameter is not specified, `Start-DSCConfiguration` creates a background job to perform the operation.</span></span> <span data-ttu-id="1f233-137">Adja meg a `-Verbose` paraméter lehetővé teszi, hogy tekintse meg a **részletes** a művelet kimenetét.</span><span class="sxs-lookup"><span data-stu-id="1f233-137">Specifying the `-Verbose` parameter allows you to watch the **Verbose** output of the operation.</span></span> `-Wait`<span data-ttu-id="1f233-138">, és `-Verbose` mindkét opcionális paraméterek.</span><span class="sxs-lookup"><span data-stu-id="1f233-138">, and `-Verbose` are both optional parameters.</span></span>

```powershell
Start-DscConfiguration -Path C:\Scripts\HelloWorld -Verbose -Wait
```

## <a name="test-the-configuration"></a><span data-ttu-id="1f233-139">A konfiguráció tesztelése</span><span class="sxs-lookup"><span data-stu-id="1f233-139">Test the configuration</span></span>

<span data-ttu-id="1f233-140">Miután a `Start-DSCConfiguration` parancsmag befejeződött, megjelenik egy "HelloWorld.txt" fájlt a megadott helyen.</span><span class="sxs-lookup"><span data-stu-id="1f233-140">Once the `Start-DSCConfiguration` cmdlet is complete, you should see a "HelloWorld.txt" file in the location you specified.</span></span> <span data-ttu-id="1f233-141">A tartalmak ellenőrizheti a [Get-tartalom](/powershell/module/microsoft.powershell.management/get-content) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1f233-141">You can verify the contents with the [Get-Content](/powershell/module/microsoft.powershell.management/get-content) cmdlet.</span></span>

<span data-ttu-id="1f233-142">Emellett *tesztelése* az aktuális állapot használatával [a Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration).</span><span class="sxs-lookup"><span data-stu-id="1f233-142">You can also *test* the current status using [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration).</span></span>

<span data-ttu-id="1f233-143">A kimenet lehet "True", ha a csomópont jelenleg felel meg az alkalmazott konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="1f233-143">The output should be "True" if the Node is currently compliant with the applied Configuration.</span></span>

```powershell
Test-DSCConfiguration
```

```output
True
```

```powershell
Get-Content -Path C:\Temp\HelloWorld.txt
```

```output
Hello World from DSC!
```

## <a name="re-applying-the-configuration"></a><span data-ttu-id="1f233-144">A beállítások újbóli alkalmazásával</span><span class="sxs-lookup"><span data-stu-id="1f233-144">Re-applying the configuration</span></span>

<span data-ttu-id="1f233-145">A konfiguráció újra alkalmazva megtekintéséhez, eltávolíthatja a hozta létre a konfigurációs szövegfájlban.</span><span class="sxs-lookup"><span data-stu-id="1f233-145">To see your configuration get applied again, you can remove the text file created by your Configuration.</span></span> <span data-ttu-id="1f233-146">A használatát a `Start-DSCConfiguration` parancsmagot a `-UseExisting` paraméter.</span><span class="sxs-lookup"><span data-stu-id="1f233-146">The use the `Start-DSCConfiguration` cmdlet with the `-UseExisting` parameter.</span></span> <span data-ttu-id="1f233-147">A `-UseExisting` paraméter utasítja `Start-DSCConfiguration` újból a alkalmazni az "current.mof" fájlt, amely jelöli a legutóbb sikeresen alkalmazott konfigurációs.</span><span class="sxs-lookup"><span data-stu-id="1f233-147">The `-UseExisting` parameter instructs `Start-DSCConfiguration` to re-apply the "current.mof" file, which represents the most recently successfully applied configuration.</span></span>

```powershell
Remove-Item -Path C:\Temp\HelloWorld.txt
```

## <a name="next-steps"></a><span data-ttu-id="1f233-148">További lépések</span><span class="sxs-lookup"><span data-stu-id="1f233-148">Next steps</span></span>

- <span data-ttu-id="1f233-149">További információk a DSC-konfigurációk [DSC-konfigurációk](configurations.md).</span><span class="sxs-lookup"><span data-stu-id="1f233-149">Find out more about DSC configurations at [DSC configurations](configurations.md).</span></span>
- <span data-ttu-id="1f233-150">Megtudhatja, milyen DSC-erőforrás áll rendelkezésre, és hogyan hozhat létre egyéni DSC-erőforrásokat, [DSC-erőforrások](../resources/resources.md).</span><span class="sxs-lookup"><span data-stu-id="1f233-150">See what DSC resources are available, and how to create custom DSC resources at [DSC resources](../resources/resources.md).</span></span>
- <span data-ttu-id="1f233-151">DSC-konfigurációkat és erőforrásokat a [PowerShell-galériából](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="1f233-151">Find DSC configurations and resources in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
