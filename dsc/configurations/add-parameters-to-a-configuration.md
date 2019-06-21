---
ms.date: 12/12/2018
keywords: DSC, powershell, erőforrás, katalógus, beállítása
title: Paraméterek hozzáadása konfigurációkhoz
ms.openlocfilehash: 514bb4cf82b7adbe4cd3d3e34d5464f574cb2206
ms.sourcegitcommit: f60fa420bdc81db174e6168d3aeb11371e483162
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/20/2019
ms.locfileid: "67301515"
---
# <a name="add-parameters-to-a-configuration"></a><span data-ttu-id="597c1-103">Paraméterek hozzáadása konfigurációkhoz</span><span class="sxs-lookup"><span data-stu-id="597c1-103">Add Parameters to a Configuration</span></span>

<span data-ttu-id="597c1-104">Funkciók, például [konfigurációk](configurations.md) , hogy a felhasználói bemenet alapján több dinamikus konfigurációk rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="597c1-104">Like Functions, [Configurations](configurations.md) can be parameterized to allow more dynamic configurations based on user input.</span></span> <span data-ttu-id="597c1-105">A lépések hasonlóak leírt [függvényeket paraméterekkel](/powershell/module/microsoft.powershell.core/about/about_functions).</span><span class="sxs-lookup"><span data-stu-id="597c1-105">The steps are similar to those described in [Functions with Parameters](/powershell/module/microsoft.powershell.core/about/about_functions).</span></span>

<span data-ttu-id="597c1-106">Ebben a példában a "Nyomtatásisor-kezelő" szolgáltatás "Fut" konfigurál alapkonfiguráció kezdődik.</span><span class="sxs-lookup"><span data-stu-id="597c1-106">This example starts with a basic Configuration that configures the "Spooler" service to be "Running".</span></span>

```powershell
Configuration TestConfig
{
    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node localhost
    {
        Service 'Spooler'
        {
            Name = 'Spooler'
            State = 'Running'
        }
    }
}
```

## <a name="built-in-configuration-parameters"></a><span data-ttu-id="597c1-107">Beépített konfigurációs paraméterei</span><span class="sxs-lookup"><span data-stu-id="597c1-107">Built-in Configuration parameters</span></span>

<span data-ttu-id="597c1-108">Egy függvény eltérően azonban a [CmdletBinding](/powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute) attribútum nincs funkciókkal bővíti a.</span><span class="sxs-lookup"><span data-stu-id="597c1-108">Unlike a Function though, the [CmdletBinding](/powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute) attribute adds no functionality.</span></span> <span data-ttu-id="597c1-109">Mellett [általános paraméterek](/powershell/module/microsoft.powershell.core/about/about_commonparameters), konfigurációk is használhatja az alábbi paraméterek, beépített anélkül, hogy definiálja azokat.</span><span class="sxs-lookup"><span data-stu-id="597c1-109">In addition to [Common Parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters), Configurations can also use the following built in parameters, without requiring you to define them.</span></span>

|<span data-ttu-id="597c1-110">Paraméter</span><span class="sxs-lookup"><span data-stu-id="597c1-110">Parameter</span></span>  |<span data-ttu-id="597c1-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="597c1-111">Description</span></span>  |
|---------|---------|
|`-InstanceName`|<span data-ttu-id="597c1-112">Határozza meg [összetett konfigurációk](compositeconfigs.md)</span><span class="sxs-lookup"><span data-stu-id="597c1-112">Used in defining [Composite Configurations](compositeconfigs.md)</span></span>|
|`-DependsOn`|<span data-ttu-id="597c1-113">Határozza meg [összetett konfigurációk](compositeconfigs.md)</span><span class="sxs-lookup"><span data-stu-id="597c1-113">Used in defining [Composite Configurations](compositeconfigs.md)</span></span>|
|`-PSDSCRunAsCredential`|<span data-ttu-id="597c1-114">Határozza meg [összetett konfigurációk](compositeconfigs.md)</span><span class="sxs-lookup"><span data-stu-id="597c1-114">Used in defining [Composite Configurations](compositeconfigs.md)</span></span>|
|`-ConfigurationData`|<span data-ttu-id="597c1-115">Amelyen a strukturált [konfigurációs adatok](configData.md) a konfigurációban való használat.</span><span class="sxs-lookup"><span data-stu-id="597c1-115">Used to pass in structured [Configuration Data](configData.md) for use in the Configuration.</span></span>|
|`-OutputPath`|<span data-ttu-id="597c1-116">Hol adható meg a "\<computername\>.mof" fájl le lesz fordítva</span><span class="sxs-lookup"><span data-stu-id="597c1-116">Used to specify where your "\<computername\>.mof" file will be compiled</span></span>|

## <a name="adding-your-own-parameters-to-configurations"></a><span data-ttu-id="597c1-117">Konfigurációk a saját paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="597c1-117">Adding your own parameters to Configurations</span></span>

<span data-ttu-id="597c1-118">A beépített paraméterek mellett is adhat a saját paraméterek a konfigurációk.</span><span class="sxs-lookup"><span data-stu-id="597c1-118">In addition to the built-in parameters, you can also add your own parameters to your Configurations.</span></span> <span data-ttu-id="597c1-119">A paraméterblokkban közvetlenül a konfigurációs nyilatkozat, csakúgy, mint egy függvény belülre irányul.</span><span class="sxs-lookup"><span data-stu-id="597c1-119">The parameter block goes directly inside the Configuration declaration, just like a Function.</span></span> <span data-ttu-id="597c1-120">Egy konfigurációs paraméter blokk kívül bármely kell **csomópont** nyilatkozatok, és minden újabb *importálása* utasításokat.</span><span class="sxs-lookup"><span data-stu-id="597c1-120">A Configuration parameter block should be outside any **Node** declarations, and above any *import* statements.</span></span> <span data-ttu-id="597c1-121">Paraméterek hozzáadásával a konfigurációk megbízhatóbb és dinamikus teheti meg.</span><span class="sxs-lookup"><span data-stu-id="597c1-121">By adding parameters, you can make your Configurations more robust and dynamic.</span></span>

```powershell
Configuration TestConfig
{
    param
    (

    )
```

### <a name="add-a-computername-parameter"></a><span data-ttu-id="597c1-122">ComputerName paraméter hozzáadása</span><span class="sxs-lookup"><span data-stu-id="597c1-122">Add a ComputerName parameter</span></span>

<span data-ttu-id="597c1-123">Az első paraméter lehetséges, hogy egy `-Computername` paramétert, így bármely dinamikusan állíthat össze egy ".mof" fájl `-Computername` adja át a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="597c1-123">The first parameter you might add is a `-Computername` parameter so you can dynamically compile a ".mof" file for any `-Computername` you pass to your configuration.</span></span> <span data-ttu-id="597c1-124">Funkciók, például megadhat egy alapértelmezett értéket, abban az esetben, ha a felhasználó nem felel meg egy értéket `-ComputerName`</span><span class="sxs-lookup"><span data-stu-id="597c1-124">Like Functions, you can also define a default value, in case the user does not pass in a value for `-ComputerName`</span></span>

```powershell
param
(
    [String]
    $ComputerName="localhost"
)
```

<span data-ttu-id="597c1-125">Belül a konfigurációját, majd megadhatja a `-ComputerName` paraméter a csomópont blokk meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="597c1-125">Within your configuration, you can then specify your `-ComputerName` parameter when defining your Node block.</span></span>

```powershell
Node $ComputerName
{

}
```

### <a name="calling-your-configuration-with-parameters"></a><span data-ttu-id="597c1-126">A konfiguráció paraméterekkel hívása</span><span class="sxs-lookup"><span data-stu-id="597c1-126">Calling your Configuration with parameters</span></span>

<span data-ttu-id="597c1-127">Miután hozzáadta a paraméterek a konfigurációt, ugyanúgy, mint egy parancsmaggal használhatja őket.</span><span class="sxs-lookup"><span data-stu-id="597c1-127">After you have added parameters to your Configuration, you can use them just like you would with a cmdlet.</span></span>

```powershell
TestConfig -ComputerName "server01"
```

### <a name="compiling-multiple-mof-files"></a><span data-ttu-id="597c1-128">Több .mof fájl fordítása</span><span class="sxs-lookup"><span data-stu-id="597c1-128">Compiling multiple .mof files</span></span>

<span data-ttu-id="597c1-129">A csomópont blokk is fogadhat számítógépnevek vesszővel tagolt listája, és minden ".mof" fájlokat hoz létre.</span><span class="sxs-lookup"><span data-stu-id="597c1-129">The Node block can also accept a comma-separated list of computer names and will generate ".mof" files for each.</span></span> <span data-ttu-id="597c1-130">Az összes számítógép átadott ".mof" fájlok létrehozásához az alábbi példa futtatása a `-ComputerName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="597c1-130">You can run the following example to generate ".mof" files for all of the computers passed to the `-ComputerName` parameter.</span></span>

```powershell
Configuration TestConfig
{
    param
    (
        [String]
        $ComputerName="localhost"
    )

    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node $ComputerName
    {
        Service 'Spooler'
        {
            Name = 'Spooler'
            State = 'Running'
        }
    }
}

TestConfig -ComputerName "server01", "server02", "server03"
```

## <a name="advanced-parameters-in-configurations"></a><span data-ttu-id="597c1-131">Speciális paraméterek konfigurációk</span><span class="sxs-lookup"><span data-stu-id="597c1-131">Advanced parameters in Configurations</span></span>

<span data-ttu-id="597c1-132">Mellett egy `-ComputerName` paramétert, hozzáadhatja a szolgáltatás nevét és állapotát paramétereit.</span><span class="sxs-lookup"><span data-stu-id="597c1-132">In addition to a `-ComputerName` parameter, we can add parameters for the service name and state.</span></span> <span data-ttu-id="597c1-133">Az alábbi példa hozzáad egy paraméter blokkot, egy `-ServiceName` paramétert, és használja, ezzel dinamikusan definiálva a **szolgáltatás** erőforrás letiltása.</span><span class="sxs-lookup"><span data-stu-id="597c1-133">The following example adds a parameter block with a `-ServiceName` parameter and uses it to dynamically define the **Service** resource block.</span></span> <span data-ttu-id="597c1-134">Hozzáadja a `-State` paraméter, ezzel dinamikusan definiálva a **állapot** a a **szolgáltatás** erőforrás letiltása.</span><span class="sxs-lookup"><span data-stu-id="597c1-134">It also adds a `-State` parameter to dynamically define the **State** in the **Service** resource block.</span></span>

```powershell
Configuration TestConfig
{
    param
    (
        [String]
        $ServiceName,

        [String]
        $State,

        [String]
        $ComputerName="localhost"
    )

    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node $ComputerName
    {
        Service $ServiceName
        {
            Name = $ServiceName
            State = $State
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="597c1-135">Más advacned forgatókönyvekben, akkor előfordulhat, hogy célszerűbb, a dinamikus adatokat áthelyezni egy strukturált [konfigurációs adatok](configData.md).</span><span class="sxs-lookup"><span data-stu-id="597c1-135">In more advacned scenarios, it might make more sense to move your dynamic data into a structured [Configuration Data](configData.md).</span></span>

<span data-ttu-id="597c1-136">A példában most konfigurációs vesz igénybe egy dinamikus `$ServiceName`, de nincs megadva, ha fordítása hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="597c1-136">The example Configuration now takes a dynamic `$ServiceName`, but if one is not specified, compiling results in an error.</span></span> <span data-ttu-id="597c1-137">Hozzáadhat például ebben a példában egy alapértelmezett értéket.</span><span class="sxs-lookup"><span data-stu-id="597c1-137">You could add a default value like this example.</span></span>

```powershell
[String]
$ServiceName="Spooler"
```

<span data-ttu-id="597c1-138">Ebben a példányban, logikus további egyszerűen kényszerítik a felhasználót adjon meg egy értéket a `$ServiceName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="597c1-138">In this instance though, it makes more sense to simply force the user to specify a value for the `$ServiceName` parameter.</span></span> <span data-ttu-id="597c1-139">A `parameter` attribútum lehetővé teszi, hogy további ellenőrzési és a folyamat a konfigurációs paramétereket támogatja.</span><span class="sxs-lookup"><span data-stu-id="597c1-139">The `parameter` attribute allows you to add further validation and pipeline support to your Configuration's parameters.</span></span>

<span data-ttu-id="597c1-140">Bármely paraméterdeklarációhoz felett adja hozzá a `parameter` attribútum letiltása az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="597c1-140">Above any parameter declaration, add the `parameter` attribute block as in the example below.</span></span>

```powershell
[parameter()]
[String]
$ServiceName
```

<span data-ttu-id="597c1-141">A megadott argumentumok minden egyes `parameter` attribútum vezérlő aspektusainak paraméter van megadva.</span><span class="sxs-lookup"><span data-stu-id="597c1-141">You can specify arguments to each `parameter` attribute, to control aspects of the defined parameter.</span></span> <span data-ttu-id="597c1-142">A következő példa a `$ServiceName` egy **kötelező** paraméter.</span><span class="sxs-lookup"><span data-stu-id="597c1-142">The following example makes the `$ServiceName` a **Mandatory** parameter.</span></span>

```powershell
[parameter(Mandatory)]
[String]
$ServiceName
```

<span data-ttu-id="597c1-143">Az a `$State` paramétert, szeretnénk, hogy a felhasználó kívül előre meghatározott értékeket (például a futó, a Leállítva) a `ValidationSet*`attribútum megakadályozná, hogy a felhasználó kívül (például a futó, előre meghatározott értékeket adjanak meg Leállítva).</span><span class="sxs-lookup"><span data-stu-id="597c1-143">For the `$State` parameter, we would like to prevent the user from specifying values outside of a predefined set (like Running, Stopped) the `ValidationSet*`attribute would prevent the user from specifying values outside of a predefined set (like Running, Stopped).</span></span> <span data-ttu-id="597c1-144">Az alábbi példa hozzáadja a `ValidationSet` attribútumot a `$State` paraméter.</span><span class="sxs-lookup"><span data-stu-id="597c1-144">The following example adds the `ValidationSet` attribute to the `$State` parameter.</span></span> <span data-ttu-id="597c1-145">Mert szeretnénk, hogy nem a `$State` paraméter **kötelező**, hogy hozzá kell adnia egy alapértelmezett értéket.</span><span class="sxs-lookup"><span data-stu-id="597c1-145">Since we do not want to make the `$State` parameter **Mandatory**, we will need to add a default value for it.</span></span>

```powershell
[ValidateSet("Running", "Stopped")]
[String]
$State="Running"
```

> [!NOTE]
> <span data-ttu-id="597c1-146">Nem kell megadnia egy `parameter` attribútum használata esetén egy `validation` attribútum.</span><span class="sxs-lookup"><span data-stu-id="597c1-146">You do not need to specify a `parameter` attribute when using a `validation` attribute.</span></span>

<span data-ttu-id="597c1-147">További információ a `parameter` és az érvényesítési attribútumokat [about_Functions_Advanced_Parameters](/powershell/module/microsoft.powershell.core/about/about_Functions_Advanced_Parameters).</span><span class="sxs-lookup"><span data-stu-id="597c1-147">You can read more about the `parameter` and validation attributes in [about_Functions_Advanced_Parameters](/powershell/module/microsoft.powershell.core/about/about_Functions_Advanced_Parameters).</span></span>

## <a name="fully-parameterized-configuration"></a><span data-ttu-id="597c1-148">Teljes körűen paraméteres Configuration</span><span class="sxs-lookup"><span data-stu-id="597c1-148">Fully parameterized Configuration</span></span>

<span data-ttu-id="597c1-149">Ezzel kapunk egy paraméteres Configuration, amely a felhasználó adja meg egy `-InstanceName`, `-ServiceName`, és érvényesíti a `-State` paraméter.</span><span class="sxs-lookup"><span data-stu-id="597c1-149">We now have a parameterized Configuration that forces the user to specify an `-InstanceName`, `-ServiceName`, and validates the `-State` parameter.</span></span>

```powershell
Configuration TestConfig
{
    param
    (
        [parameter(Mandatory)]
        [String]
        $ServiceName,

        [ValidateSet("Running","Stopped")]
        [String]
        $State="Running",

        [String]
        $ComputerName="localhost",
    )

    # It is best practice to implicitly import any required resources or modules.
    Import-DSCResource -Module PSDesiredStateConfiguration

    Node localhost
    {
        Service $ServiceName
        {
            Name = $ServiceName
            State = $State
        }
    }
}
```

## <a name="see-also"></a><span data-ttu-id="597c1-150">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="597c1-150">See also</span></span>

- [<span data-ttu-id="597c1-151">DSC-konfigurációk súgót írni</span><span class="sxs-lookup"><span data-stu-id="597c1-151">Write help for DSC configurations</span></span>](configHelp.md)
- [<span data-ttu-id="597c1-152">A dinamikus konfigurációk</span><span class="sxs-lookup"><span data-stu-id="597c1-152">Dynamic Configurations</span></span>](flow-control-in-configurations.md)
- [<span data-ttu-id="597c1-153">Konfigurációs adatok használata a konfigurációk</span><span class="sxs-lookup"><span data-stu-id="597c1-153">Use Configuration Data in your Configurations</span></span>](configData.md)
- [<span data-ttu-id="597c1-154">Külön konfigurációs és környezeti adatok</span><span class="sxs-lookup"><span data-stu-id="597c1-154">Separate configuration and environment data</span></span>](separatingEnvData.md)
