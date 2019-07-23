---
ms.date: 12/12/2018
keywords: DSC, PowerShell, konfigurálás, szolgáltatás, beállítás
title: Konfiguráció írása, fordítása és alkalmazása
ms.openlocfilehash: 8bcd55518b0409b9a4b02ca95f027a0a77eb5300
ms.sourcegitcommit: 118eb294d5a84a772e6449d42a9d9324e18ef6b9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/22/2019
ms.locfileid: "68372177"
---
> <span data-ttu-id="1428c-103">Érvényes: Windows PowerShell 4,0, Windows PowerShell 5,0</span><span class="sxs-lookup"><span data-stu-id="1428c-103">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

# <a name="write-compile-and-apply-a-configuration"></a><span data-ttu-id="1428c-104">Konfiguráció írása, fordítása és alkalmazása</span><span class="sxs-lookup"><span data-stu-id="1428c-104">Write, Compile, and Apply a Configuration</span></span>

<span data-ttu-id="1428c-105">Ez a gyakorlat végigvezeti a kívánt állapot-konfiguráció (DSC) konfigurációjának a kezdéstől a befejezésig történő létrehozásán és alkalmazásán.</span><span class="sxs-lookup"><span data-stu-id="1428c-105">This exercise walks through creating and applying a Desired State Configuration (DSC) configuration from start to finish.</span></span>
<span data-ttu-id="1428c-106">Az alábbi példában megtudhatja, hogyan írhat és alkalmazhat egy nagyon egyszerű konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="1428c-106">In the following example, you will learn how to write and apply a very simple Configuration.</span></span> <span data-ttu-id="1428c-107">A konfiguráció biztosítja, hogy a "HelloWorld. txt" fájl létezik a helyi gépen.</span><span class="sxs-lookup"><span data-stu-id="1428c-107">The Configuration will ensure a "HelloWorld.txt" file exists on your local machine.</span></span> <span data-ttu-id="1428c-108">Ha törli a fájlt, a DSC a következő frissítésekor újra létrehozza azt.</span><span class="sxs-lookup"><span data-stu-id="1428c-108">If you delete the file, DSC will recreate it the next time it updates.</span></span>

<span data-ttu-id="1428c-109">A DSC és annak működésének áttekintését lásd: [a fejlesztők számára a kívánt állapot konfigurációjának áttekintése](../overview/overview.md).</span><span class="sxs-lookup"><span data-stu-id="1428c-109">For an overview of what DSC is and how it works, see [Desired State Configuration Overview for Developers](../overview/overview.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="1428c-110">Követelmények</span><span class="sxs-lookup"><span data-stu-id="1428c-110">Requirements</span></span>

<span data-ttu-id="1428c-111">A példa futtatásához a PowerShell 4,0-es vagy újabb verzióját futtató számítógépre lesz szüksége.</span><span class="sxs-lookup"><span data-stu-id="1428c-111">To run this example, you will need a computer running PowerShell 4.0 or later.</span></span>

## <a name="write-the-configuration"></a><span data-ttu-id="1428c-112">A konfiguráció megírása</span><span class="sxs-lookup"><span data-stu-id="1428c-112">Write the configuration</span></span>

<span data-ttu-id="1428c-113">A DSC- [konfiguráció](configurations.md) egy speciális PowerShell-függvény, amely meghatározza, hogyan szeretné konfigurálni egy vagy több célszámítógépet (csomópontot).</span><span class="sxs-lookup"><span data-stu-id="1428c-113">A DSC [Configuration](configurations.md) is a special PowerShell function that defines how you want to configure one or more target computers (Nodes).</span></span>

<span data-ttu-id="1428c-114">A PowerShell ISE vagy más PowerShell-szerkesztőben írja be a következőt:</span><span class="sxs-lookup"><span data-stu-id="1428c-114">In the PowerShell ISE, or other PowerShell editor, type the following:</span></span>

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

> <span data-ttu-id="1428c-115">! Fontos olyan speciális forgatókönyvekben, ahol több modult kell importálni, hogy ugyanabban a konfigurációban több DSC-erőforrással is működjön, ügyeljen arra, hogy minden modult külön sorba helyezzen `Import-DscResource`a használatával.</span><span class="sxs-lookup"><span data-stu-id="1428c-115">!Important In more advanced scenarios where multiple modules need to be imported so you can work with many DSC Resources in the same configuration, make sure to put each module in a seperate line using `Import-DscResource`.</span></span>
> <span data-ttu-id="1428c-116">Ez könnyebben karbantartható a verziókövetés és a szükséges, ha a DSC-t az Azure-beli állapot konfigurációjában kell megtartani.</span><span class="sxs-lookup"><span data-stu-id="1428c-116">This is easier to maintain in source control and required when working with DSC in Azure State Configuration.</span></span>
>
> ```powershell
>  Configuration HelloWorld {
>
>   # Import the module that contains the File resource.
>   Import-DscResource -ModuleName PsDesiredStateConfiguration
>   Import-DscResource -ModuleName xWebAdministration
>
> ```

<span data-ttu-id="1428c-117">Mentse a fájlt "HelloWorld. ps1" néven.</span><span class="sxs-lookup"><span data-stu-id="1428c-117">Save the file as "HelloWorld.ps1".</span></span>

<span data-ttu-id="1428c-118">A konfiguráció definiálása hasonló a függvények definiálásához.</span><span class="sxs-lookup"><span data-stu-id="1428c-118">Defining a Configuration is like defining a Function.</span></span> <span data-ttu-id="1428c-119">A **csomópont** -blokk meghatározza a konfigurálni kívánt célként megadott csomópontot, ebben `localhost`az esetben.</span><span class="sxs-lookup"><span data-stu-id="1428c-119">The **Node** block specifies the target node to be configured, in this case `localhost`.</span></span>

<span data-ttu-id="1428c-120">A [konfiguráció egy](../resources/resources.md)erőforrást, az `File` erőforrást hívja meg.</span><span class="sxs-lookup"><span data-stu-id="1428c-120">The configuration calls one [resources](../resources/resources.md), the `File` resource.</span></span> <span data-ttu-id="1428c-121">Az erőforrások feladata annak biztosítása, hogy a cél csomópont a konfiguráció által meghatározott állapotban legyen.</span><span class="sxs-lookup"><span data-stu-id="1428c-121">Resources do the work of ensuring that the target node is in the state defined by the configuration.</span></span>

## <a name="compile-the-configuration"></a><span data-ttu-id="1428c-122">A konfiguráció fordítása</span><span class="sxs-lookup"><span data-stu-id="1428c-122">Compile the configuration</span></span>

<span data-ttu-id="1428c-123">Ahhoz, hogy egy DSC-konfigurációt egy csomóponton lehessen alkalmazni, először egy MOF-fájlba kell lefordítani.</span><span class="sxs-lookup"><span data-stu-id="1428c-123">For a DSC configuration to be applied to a node, it must first be compiled into a MOF file.</span></span>
<span data-ttu-id="1428c-124">A konfiguráció, például egy függvény futtatása lefordít egy ". MOF" fájlt a `Node` blokk által meghatározott összes csomóponthoz.</span><span class="sxs-lookup"><span data-stu-id="1428c-124">Running the configuration, like a function, will compile one ".mof" file for every Node defined by the `Node` block.</span></span>
<span data-ttu-id="1428c-125">A konfiguráció futtatásához a "HelloWorld. ps1" parancsfájlt az aktuális hatókörbe kell *leadnia* .</span><span class="sxs-lookup"><span data-stu-id="1428c-125">In order to run the configuration, you need to *dot source* your "HelloWorld.ps1" script into the current scope.</span></span>
<span data-ttu-id="1428c-126">További információ: [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts?view=powershell-6#script-scope-and-dot-sourcing).</span><span class="sxs-lookup"><span data-stu-id="1428c-126">For more information, see [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts?view=powershell-6#script-scope-and-dot-sourcing).</span></span>

<!-- markdownlint-disable MD038 -->
<span data-ttu-id="1428c-127">*Adja meg* a "HelloWorld. ps1" parancsfájlt úgy, hogy beírja azt az elérési utat, `. ` ahol a tárolta, a (pont, szóköz) után.</span><span class="sxs-lookup"><span data-stu-id="1428c-127">*Dot source* your "HelloWorld.ps1" script by typing in the path where you stored it, after the `. ` (dot, space).</span></span> <span data-ttu-id="1428c-128">Ezután futtathatja a konfigurációt úgy, hogy a függvényt hívja meg.</span><span class="sxs-lookup"><span data-stu-id="1428c-128">You may then, run your configuration by calling it like a Function.</span></span>
<!-- markdownlint-enable MD038 -->

```powershell
. C:\Scripts\HelloWorld.ps1
HelloWorld
```

<span data-ttu-id="1428c-129">Ez a következő kimenetet hozza létre:</span><span class="sxs-lookup"><span data-stu-id="1428c-129">This generates the following output:</span></span>

```output
Directory: C:\Scripts\HelloWorld


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

## <a name="apply-the-configuration"></a><span data-ttu-id="1428c-130">A konfiguráció alkalmazása</span><span class="sxs-lookup"><span data-stu-id="1428c-130">Apply the configuration</span></span>

<span data-ttu-id="1428c-131">Most, hogy már rendelkezik a lefordított MOF-vel, a konfigurációt alkalmazhatja a cél csomópontra (ebben az esetben a helyi számítógépre) a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmag meghívásával.</span><span class="sxs-lookup"><span data-stu-id="1428c-131">Now that you have the compiled MOF, you can apply the configuration to the target node (in this case, the local computer) by calling the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span>

<span data-ttu-id="1428c-132">A `Start-DscConfiguration` parancsmag a konfiguráció alkalmazásához megadja a [helyi Configuration Manager (LCD ChipOnGlas)](../managing-nodes/metaConfig.md), a DSC motorját.</span><span class="sxs-lookup"><span data-stu-id="1428c-132">The `Start-DscConfiguration` cmdlet tells the [Local Configuration Manager (LCM)](../managing-nodes/metaConfig.md), the engine of DSC, to apply the configuration.</span></span>
<span data-ttu-id="1428c-133">Az LCD-eszközök meghívja a DSC-erőforrásokat a konfiguráció alkalmazásához.</span><span class="sxs-lookup"><span data-stu-id="1428c-133">The LCM does the work of calling the DSC resources to apply the configuration.</span></span>

<span data-ttu-id="1428c-134">Az alábbi kód használatával hajtsa végre `Start-DSCConfiguration` a parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1428c-134">Use the code below to execute the `Start-DSCConfiguration` cmdlet.</span></span> <span data-ttu-id="1428c-135">Adja meg a könyvtár elérési útját, ahol a "localhost. MOF `-Path` " a paraméterre van tárolva.</span><span class="sxs-lookup"><span data-stu-id="1428c-135">Specify the directory path where your "localhost.mof" is stored to the `-Path` parameter.</span></span> <span data-ttu-id="1428c-136">A `Start-DSCConfiguration` parancsmag a "\<számítógépnév\>. MOF" fájlokhoz megadott könyvtárat vizsgálja.</span><span class="sxs-lookup"><span data-stu-id="1428c-136">The `Start-DSCConfiguration` cmdlet looks through the directory specified for any "\<computername\>.mof" files.</span></span> <span data-ttu-id="1428c-137">A `Start-DSCConfiguration` parancsmag megpróbálja alkalmazni az összes olyan ". MOF" fájlt, amely a fájlnévben ("localhost", "kiszolgalo01", "DC-02" stb.) megadott számítógépnévre hivatkozik.</span><span class="sxs-lookup"><span data-stu-id="1428c-137">The `Start-DSCConfiguration` cmdlet attempts to apply each ".mof" file it finds to the computername specified by the filename ("localhost", "server01", "dc-02", etc.).</span></span>

> [!NOTE]
> <span data-ttu-id="1428c-138">Ha a `-Wait` paraméter nincs megadva, `Start-DSCConfiguration` a létrehoz egy háttér-feladatot a művelet végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="1428c-138">If the `-Wait` parameter is not specified, `Start-DSCConfiguration` creates a background job to perform the operation.</span></span> <span data-ttu-id="1428c-139">A `-Verbose` paraméter megadásával megtekintheti a művelet **részletes** kimenetét.</span><span class="sxs-lookup"><span data-stu-id="1428c-139">Specifying the `-Verbose` parameter allows you to watch the **Verbose** output of the operation.</span></span> <span data-ttu-id="1428c-140">`-Wait`a és `-Verbose` a választható paraméterek is.</span><span class="sxs-lookup"><span data-stu-id="1428c-140">`-Wait`, and `-Verbose` are both optional parameters.</span></span>

```powershell
Start-DscConfiguration -Path C:\Scripts\HelloWorld -Verbose -Wait
```

## <a name="test-the-configuration"></a><span data-ttu-id="1428c-141">A konfiguráció tesztelése</span><span class="sxs-lookup"><span data-stu-id="1428c-141">Test the configuration</span></span>

<span data-ttu-id="1428c-142">A `Start-DSCConfiguration` parancsmag befejezését követően egy "HelloWorld. txt" fájlt kell látnia a megadott helyen.</span><span class="sxs-lookup"><span data-stu-id="1428c-142">Once the `Start-DSCConfiguration` cmdlet is complete, you should see a "HelloWorld.txt" file in the location you specified.</span></span> <span data-ttu-id="1428c-143">A tartalmat a [Get-Content](/powershell/module/microsoft.powershell.management/get-content) parancsmaggal ellenőrizheti.</span><span class="sxs-lookup"><span data-stu-id="1428c-143">You can verify the contents with the [Get-Content](/powershell/module/microsoft.powershell.management/get-content) cmdlet.</span></span>

<span data-ttu-id="1428c-144">Tesztelheti az *aktuális* állapotot a [test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)használatával is.</span><span class="sxs-lookup"><span data-stu-id="1428c-144">You can also *test* the current status using [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration).</span></span>

<span data-ttu-id="1428c-145">Ha a csomópont jelenleg megfelel az alkalmazott konfigurációnak, a kimenetnek "true" értékűnek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="1428c-145">The output should be "True" if the Node is currently compliant with the applied Configuration.</span></span>

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

## <a name="re-applying-the-configuration"></a><span data-ttu-id="1428c-146">A konfiguráció újbóli alkalmazása</span><span class="sxs-lookup"><span data-stu-id="1428c-146">Re-applying the configuration</span></span>

<span data-ttu-id="1428c-147">A konfiguráció ismételt alkalmazásának megtekintéséhez eltávolíthatja a konfiguráció által létrehozott szövegfájlt.</span><span class="sxs-lookup"><span data-stu-id="1428c-147">To see your configuration get applied again, you can remove the text file created by your Configuration.</span></span> <span data-ttu-id="1428c-148">A használja `Start-DSCConfiguration` a parancsmagot a `-UseExisting` paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="1428c-148">The use the `Start-DSCConfiguration` cmdlet with the `-UseExisting` parameter.</span></span> <span data-ttu-id="1428c-149">A `-UseExisting` paraméter `Start-DSCConfiguration` arra utasítja, hogy újra alkalmazza a "current. MOF" fájlt, amely a legutóbb sikeresen alkalmazott konfigurációt jelképezi.</span><span class="sxs-lookup"><span data-stu-id="1428c-149">The `-UseExisting` parameter instructs `Start-DSCConfiguration` to re-apply the "current.mof" file, which represents the most recently successfully applied configuration.</span></span>

```powershell
Remove-Item -Path C:\Temp\HelloWorld.txt
```

## <a name="next-steps"></a><span data-ttu-id="1428c-150">További lépések</span><span class="sxs-lookup"><span data-stu-id="1428c-150">Next steps</span></span>

- <span data-ttu-id="1428c-151">Tudjon meg többet a DSC-konfigurációkról a [DSC](configurations.md)-konfigurációknál.</span><span class="sxs-lookup"><span data-stu-id="1428c-151">Find out more about DSC configurations at [DSC configurations](configurations.md).</span></span>
- <span data-ttu-id="1428c-152">Ismerje meg, hogy milyen DSC-erőforrások érhetők el, és hogyan hozhat létre egyéni DSC-erőforrásokat a [DSC](../resources/resources.md)-erőforrásokon.</span><span class="sxs-lookup"><span data-stu-id="1428c-152">See what DSC resources are available, and how to create custom DSC resources at [DSC resources](../resources/resources.md).</span></span>
- <span data-ttu-id="1428c-153">Keresse meg a DSC-konfigurációkat és-erőforrásokat a [PowerShell-Galéria](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="1428c-153">Find DSC configurations and resources in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>
