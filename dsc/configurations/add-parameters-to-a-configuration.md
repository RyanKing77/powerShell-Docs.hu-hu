---
ms.date: 12/12/2018
keywords: DSC, PowerShell, erőforrás, katalógus, beállítás
title: Paraméterek hozzáadása konfigurációkhoz
ms.openlocfilehash: 72e6c15593d11ed39d7fe8ea79f794089f410cf8
ms.sourcegitcommit: d1ba596f9e0d4df9565601a70687a126d535c917
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/05/2019
ms.locfileid: "70386317"
---
# <a name="add-parameters-to-a-configuration"></a><span data-ttu-id="881ad-103">Paraméterek hozzáadása konfigurációkhoz</span><span class="sxs-lookup"><span data-stu-id="881ad-103">Add Parameters to a Configuration</span></span>

<span data-ttu-id="881ad-104">A függvényekhez hasonlóan a [konfigurációk](configurations.md) paraméterei is lehetővé teszik, hogy a felhasználók bevitele alapján több dinamikus konfigurációt engedélyezzen.</span><span class="sxs-lookup"><span data-stu-id="881ad-104">Like Functions, [Configurations](configurations.md) can be parameterized to allow more dynamic configurations based on user input.</span></span> <span data-ttu-id="881ad-105">A lépések hasonlóak a [függvények paraméterrel](/powershell/module/microsoft.powershell.core/about/about_functions)ismertetett műveletekhez.</span><span class="sxs-lookup"><span data-stu-id="881ad-105">The steps are similar to those described in [Functions with Parameters](/powershell/module/microsoft.powershell.core/about/about_functions).</span></span>

<span data-ttu-id="881ad-106">Ez a példa egy alapszintű konfigurációval kezdődik, amely úgy konfigurálja a "sorkezelő" szolgáltatást, hogy "fut".</span><span class="sxs-lookup"><span data-stu-id="881ad-106">This example starts with a basic Configuration that configures the "Spooler" service to be "Running".</span></span>

```powershell
Configuration TestConfig
{
    # It is best practice to explicitly import any required resources or modules.
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

## <a name="built-in-configuration-parameters"></a><span data-ttu-id="881ad-107">Beépített konfigurációs paraméterek</span><span class="sxs-lookup"><span data-stu-id="881ad-107">Built-in Configuration parameters</span></span>

<span data-ttu-id="881ad-108">A függvényektől eltérően a [CmdletBinding](/powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute) attribútum nem hoz létre funkciókat.</span><span class="sxs-lookup"><span data-stu-id="881ad-108">Unlike a Function though, the [CmdletBinding](/powershell/module/microsoft.powershell.core/about/about_functions_cmdletbindingattribute) attribute adds no functionality.</span></span> <span data-ttu-id="881ad-109">A [gyakori paraméterek](/powershell/module/microsoft.powershell.core/about/about_commonparameters)mellett a konfigurációk a következő beépített paramétereket is használhatják, anélkül, hogy meg kellene határozni őket.</span><span class="sxs-lookup"><span data-stu-id="881ad-109">In addition to [Common Parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters), Configurations can also use the following built in parameters, without requiring you to define them.</span></span>

|<span data-ttu-id="881ad-110">Paraméter</span><span class="sxs-lookup"><span data-stu-id="881ad-110">Parameter</span></span>  |<span data-ttu-id="881ad-111">Leírás</span><span class="sxs-lookup"><span data-stu-id="881ad-111">Description</span></span>  |
|---------|---------|
|`-InstanceName`|<span data-ttu-id="881ad-112">[Összetett konfigurációk](compositeconfigs.md) definiálásakor használatos</span><span class="sxs-lookup"><span data-stu-id="881ad-112">Used in defining [Composite Configurations](compositeconfigs.md)</span></span>|
|`-DependsOn`|<span data-ttu-id="881ad-113">[Összetett konfigurációk](compositeconfigs.md) definiálásakor használatos</span><span class="sxs-lookup"><span data-stu-id="881ad-113">Used in defining [Composite Configurations](compositeconfigs.md)</span></span>|
|`-PSDSCRunAsCredential`|<span data-ttu-id="881ad-114">[Összetett konfigurációk](compositeconfigs.md) definiálásakor használatos</span><span class="sxs-lookup"><span data-stu-id="881ad-114">Used in defining [Composite Configurations](compositeconfigs.md)</span></span>|
|`-ConfigurationData`|<span data-ttu-id="881ad-115">A konfigurációban használható strukturált [konfigurációs adatbevitelre](configData.md) szolgál.</span><span class="sxs-lookup"><span data-stu-id="881ad-115">Used to pass in structured [Configuration Data](configData.md) for use in the Configuration.</span></span>|
|`-OutputPath`|<span data-ttu-id="881ad-116">Annak megadására szolgál,\<hogy\>a "számítógépnév. MOF" fájl hol lesz lefordítva</span><span class="sxs-lookup"><span data-stu-id="881ad-116">Used to specify where your "\<computername\>.mof" file will be compiled</span></span>|

## <a name="adding-your-own-parameters-to-configurations"></a><span data-ttu-id="881ad-117">Saját paraméterek hozzáadása a konfigurációkhoz</span><span class="sxs-lookup"><span data-stu-id="881ad-117">Adding your own parameters to Configurations</span></span>

<span data-ttu-id="881ad-118">A beépített paraméterek mellett saját paramétereket is hozzáadhat a konfigurációkhoz.</span><span class="sxs-lookup"><span data-stu-id="881ad-118">In addition to the built-in parameters, you can also add your own parameters to your Configurations.</span></span> <span data-ttu-id="881ad-119">A Block paraméter közvetlenül a konfigurációs deklarációban található, ugyanúgy, mint a függvény.</span><span class="sxs-lookup"><span data-stu-id="881ad-119">The parameter block goes directly inside the Configuration declaration, just like a Function.</span></span> <span data-ttu-id="881ad-120">A konfigurációs paraméterek blokkjának a **csomópont** deklarációján kívül kell lennie, és minden *importálási* utasítás felett kell lennie.</span><span class="sxs-lookup"><span data-stu-id="881ad-120">A Configuration parameter block should be outside any **Node** declarations, and above any *import* statements.</span></span> <span data-ttu-id="881ad-121">Paraméterek hozzáadásával a konfigurációk robusztusabb és dinamikusak lehetnek.</span><span class="sxs-lookup"><span data-stu-id="881ad-121">By adding parameters, you can make your Configurations more robust and dynamic.</span></span>

```powershell
Configuration TestConfig
{
    param
    (

    )
```

### <a name="add-a-computername-parameter"></a><span data-ttu-id="881ad-122">Számítógépnév-paraméter hozzáadása</span><span class="sxs-lookup"><span data-stu-id="881ad-122">Add a ComputerName parameter</span></span>

<span data-ttu-id="881ad-123">Az első paraméter, amelyet hozzáadhat, egy `-Computername` paraméter, így dinamikusan lefordíthatja a ". MOF" fájlt `-Computername` a konfigurációba való átadáshoz.</span><span class="sxs-lookup"><span data-stu-id="881ad-123">The first parameter you might add is a `-Computername` parameter so you can dynamically compile a ".mof" file for any `-Computername` you pass to your configuration.</span></span> <span data-ttu-id="881ad-124">A függvényekhez hasonlóan megadhat egy alapértelmezett értéket is abban az esetben, ha a felhasználó nem ad át értéket a következőnek:`-ComputerName`</span><span class="sxs-lookup"><span data-stu-id="881ad-124">Like Functions, you can also define a default value, in case the user does not pass in a value for `-ComputerName`</span></span>

```powershell
param
(
    [String]
    $ComputerName="localhost"
)
```

<span data-ttu-id="881ad-125">A konfiguráción belül megadhatja a `-ComputerName` paramétert a csomópont-blokk definiálásakor.</span><span class="sxs-lookup"><span data-stu-id="881ad-125">Within your configuration, you can then specify your `-ComputerName` parameter when defining your Node block.</span></span>

```powershell
Node $ComputerName
{

}
```

### <a name="calling-your-configuration-with-parameters"></a><span data-ttu-id="881ad-126">A konfiguráció meghívása paraméterekkel</span><span class="sxs-lookup"><span data-stu-id="881ad-126">Calling your Configuration with parameters</span></span>

<span data-ttu-id="881ad-127">Miután hozzáadta a paramétereket a konfigurációhoz, azokat ugyanúgy használhatja, mint a parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="881ad-127">After you have added parameters to your Configuration, you can use them just like you would with a cmdlet.</span></span>

```powershell
TestConfig -ComputerName "server01"
```

### <a name="compiling-multiple-mof-files"></a><span data-ttu-id="881ad-128">Több. MOF fájl fordítása</span><span class="sxs-lookup"><span data-stu-id="881ad-128">Compiling multiple .mof files</span></span>

<span data-ttu-id="881ad-129">A csomópont-blokk is elfogadhatja a számítógépek neveinek vesszővel tagolt listáját, és mindegyikhez ". MOF" fájlokat fog készíteni.</span><span class="sxs-lookup"><span data-stu-id="881ad-129">The Node block can also accept a comma-separated list of computer names and will generate ".mof" files for each.</span></span> <span data-ttu-id="881ad-130">A következő példa futtatásával létrehozhat ". MOF" fájlokat a `-ComputerName` paraméternek átadott összes számítógép számára.</span><span class="sxs-lookup"><span data-stu-id="881ad-130">You can run the following example to generate ".mof" files for all of the computers passed to the `-ComputerName` parameter.</span></span>

```powershell
Configuration TestConfig
{
    param
    (
        [String]
        $ComputerName="localhost"
    )

    # It is best practice to explicitly import any required resources or modules.
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

## <a name="advanced-parameters-in-configurations"></a><span data-ttu-id="881ad-131">Speciális paraméterek a konfigurációkban</span><span class="sxs-lookup"><span data-stu-id="881ad-131">Advanced parameters in Configurations</span></span>

<span data-ttu-id="881ad-132">A `-ComputerName` paraméter mellett paramétereket is hozzáadhat a szolgáltatás nevéhez és állapotához.</span><span class="sxs-lookup"><span data-stu-id="881ad-132">In addition to a `-ComputerName` parameter, we can add parameters for the service name and state.</span></span> <span data-ttu-id="881ad-133">Az alábbi példa egy paraméterrel rendelkező `-ServiceName` paramétert ad hozzá, és a használatával dinamikusan meghatározza a **szolgáltatás** -erőforrás blokkot.</span><span class="sxs-lookup"><span data-stu-id="881ad-133">The following example adds a parameter block with a `-ServiceName` parameter and uses it to dynamically define the **Service** resource block.</span></span> <span data-ttu-id="881ad-134">Egy `-State` paraméter hozzáadásával dinamikusan definiálja az **állapotot** a **szolgáltatás** -erőforrás blokkban.</span><span class="sxs-lookup"><span data-stu-id="881ad-134">It also adds a `-State` parameter to dynamically define the **State** in the **Service** resource block.</span></span>

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

    # It is best practice to explicitly import any required resources or modules.
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
> <span data-ttu-id="881ad-135">További advacned forgatókönyvekben érdemes lehet a dinamikus adatok strukturált [konfigurációs adatokba](configData.md)való áthelyezésére.</span><span class="sxs-lookup"><span data-stu-id="881ad-135">In more advacned scenarios, it might make more sense to move your dynamic data into a structured [Configuration Data](configData.md).</span></span>

<span data-ttu-id="881ad-136">A példában a konfiguráció dinamikusan `$ServiceName`zajlik, de ha nincs megadva, a rendszer hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="881ad-136">The example Configuration now takes a dynamic `$ServiceName`, but if one is not specified, compiling results in an error.</span></span> <span data-ttu-id="881ad-137">Ehhez a példához hasonló alapértelmezett értéket adhat hozzá.</span><span class="sxs-lookup"><span data-stu-id="881ad-137">You could add a default value like this example.</span></span>

```powershell
[String]
$ServiceName="Spooler"
```

<span data-ttu-id="881ad-138">Ebben a példányban azonban több értelme van, hogy egyszerűen kényszerítse a felhasználót a `$ServiceName` paraméter értékének megadására.</span><span class="sxs-lookup"><span data-stu-id="881ad-138">In this instance though, it makes more sense to simply force the user to specify a value for the `$ServiceName` parameter.</span></span> <span data-ttu-id="881ad-139">Az `parameter` attribútum lehetővé teszi további érvényesítési és folyamat-támogatás hozzáadását a konfiguráció paramétereinek eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="881ad-139">The `parameter` attribute allows you to add further validation and pipeline support to your Configuration's parameters.</span></span>

<span data-ttu-id="881ad-140">A paraméterek deklarációja felett adja hozzá `parameter` az attribútum blokkot az alábbi példában látható módon.</span><span class="sxs-lookup"><span data-stu-id="881ad-140">Above any parameter declaration, add the `parameter` attribute block as in the example below.</span></span>

```powershell
[parameter()]
[String]
$ServiceName
```

<span data-ttu-id="881ad-141">Az egyes `parameter` attribútumokhoz argumentumokat adhat meg a definiált paraméter szempontjainak szabályozásához.</span><span class="sxs-lookup"><span data-stu-id="881ad-141">You can specify arguments to each `parameter` attribute, to control aspects of the defined parameter.</span></span> <span data-ttu-id="881ad-142">A következő példa a `$ServiceName` **kötelező** paramétert teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="881ad-142">The following example makes the `$ServiceName` a **Mandatory** parameter.</span></span>

```powershell
[parameter(Mandatory)]
[String]
$ServiceName
```

<span data-ttu-id="881ad-143">A paraméter esetében meg szeretnénk akadályozni, hogy a felhasználó az előre definiált készleten kívül (például a futó, leállított) értéket `ValidationSet*`adja meg. az attribútum megakadályozza, hogy a felhasználó egy előre definiált készleten kívüli értékeket határozzon meg (például a futtatást, `$State` Leállítva).</span><span class="sxs-lookup"><span data-stu-id="881ad-143">For the `$State` parameter, we would like to prevent the user from specifying values outside of a predefined set (like Running, Stopped) the `ValidationSet*`attribute would prevent the user from specifying values outside of a predefined set (like Running, Stopped).</span></span> <span data-ttu-id="881ad-144">A következő példa hozzáadja az `ValidationSet` attribútumot a `$State` paraméterhez.</span><span class="sxs-lookup"><span data-stu-id="881ad-144">The following example adds the `ValidationSet` attribute to the `$State` parameter.</span></span> <span data-ttu-id="881ad-145">Mivel a `$State` paramétert nem szeretnénk **kötelezővé**tenni, hozzá kell adnia egy alapértelmezett értéket.</span><span class="sxs-lookup"><span data-stu-id="881ad-145">Since we do not want to make the `$State` parameter **Mandatory**, we will need to add a default value for it.</span></span>

```powershell
[ValidateSet("Running", "Stopped")]
[String]
$State="Running"
```

> [!NOTE]
> <span data-ttu-id="881ad-146">Attribútum használatakor nem kell `parameter` attribútumot megadnia. `validation`</span><span class="sxs-lookup"><span data-stu-id="881ad-146">You do not need to specify a `parameter` attribute when using a `validation` attribute.</span></span>

<span data-ttu-id="881ad-147">További információt a [about_Functions_Advanced_Parameters](/powershell/module/microsoft.powershell.core/about/about_Functions_Advanced_Parameters)és az `parameter` érvényesítési attribútumokról a következő cikkekben olvashat:.</span><span class="sxs-lookup"><span data-stu-id="881ad-147">You can read more about the `parameter` and validation attributes in [about_Functions_Advanced_Parameters](/powershell/module/microsoft.powershell.core/about/about_Functions_Advanced_Parameters).</span></span>

## <a name="fully-parameterized-configuration"></a><span data-ttu-id="881ad-148">Teljes mértékben paraméteres konfiguráció</span><span class="sxs-lookup"><span data-stu-id="881ad-148">Fully parameterized Configuration</span></span>

<span data-ttu-id="881ad-149">Most már van egy paraméteres konfiguráció, amely arra kényszeríti a felhasználót `-InstanceName`, `-ServiceName`hogy határozzon meg egy, `-State` és érvényesíti a paramétert.</span><span class="sxs-lookup"><span data-stu-id="881ad-149">We now have a parameterized Configuration that forces the user to specify an `-InstanceName`, `-ServiceName`, and validates the `-State` parameter.</span></span>

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

    # It is best practice to explicitly import any required resources or modules.
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

## <a name="see-also"></a><span data-ttu-id="881ad-150">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="881ad-150">See also</span></span>

- [<span data-ttu-id="881ad-151">A DSC-konfigurációk írási súgója</span><span class="sxs-lookup"><span data-stu-id="881ad-151">Write help for DSC configurations</span></span>](configHelp.md)
- [<span data-ttu-id="881ad-152">Dinamikus konfigurációk</span><span class="sxs-lookup"><span data-stu-id="881ad-152">Dynamic Configurations</span></span>](flow-control-in-configurations.md)
- [<span data-ttu-id="881ad-153">Konfigurációs adatai használata a konfigurációkban</span><span class="sxs-lookup"><span data-stu-id="881ad-153">Use Configuration Data in your Configurations</span></span>](configData.md)
- [<span data-ttu-id="881ad-154">Különálló konfigurációs és környezeti adatértékek</span><span class="sxs-lookup"><span data-stu-id="881ad-154">Separate configuration and environment data</span></span>](separatingEnvData.md)
