---
ms.date: 12/12/2018
keywords: DSC, PowerShell, konfigurálás, beállítás
title: Get-test-set
ms.openlocfilehash: 68738107cd4a222a13dd4afa158f0370953158ad
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215429"
---
# <a name="get-test-set"></a><span data-ttu-id="a8033-103">Get-test-set</span><span class="sxs-lookup"><span data-stu-id="a8033-103">Get-Test-Set</span></span>

><span data-ttu-id="a8033-104">Érvényes: Windows PowerShell 4,0, Windows PowerShell 5,0</span><span class="sxs-lookup"><span data-stu-id="a8033-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

![Get, Test és Set](../media/get-test-set.png)

<span data-ttu-id="a8033-106">A PowerShell kívánt állapotának konfigurálása **Get**, **test**és **set** folyamat körül történik.</span><span class="sxs-lookup"><span data-stu-id="a8033-106">PowerShell Desired State Configuration is constructed around a **Get**, **Test**, and **Set** process.</span></span> <span data-ttu-id="a8033-107">A DSC- [erőforrások](resources.md) mindegyike metódust tartalmaz az egyes műveletek végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="a8033-107">DSC [resources](resources.md) each contains methods to complete each of these operations.</span></span> <span data-ttu-id="a8033-108">Egy [konfigurációban](../configurations/configurations.md)az erőforrás-blokkokat úgy definiálhatja, hogy kitöltse azokat a kulcsokat, amelyek egy erőforrás **Get**, **test**és **set** metódusának paraméterei lesznek.</span><span class="sxs-lookup"><span data-stu-id="a8033-108">In a [Configuration](../configurations/configurations.md), you define resource blocks to fill in keys that become parameters for a resource's **Get**, **Test**, and **Set** methods.</span></span>

<span data-ttu-id="a8033-109">Ez a **szolgáltatás** -erőforrás blokk szintaxisa.</span><span class="sxs-lookup"><span data-stu-id="a8033-109">This is the syntax for a **Service** resource block.</span></span> <span data-ttu-id="a8033-110">A **szolgáltatási** erőforrás konfigurálja a Windows-szolgáltatásokat.</span><span class="sxs-lookup"><span data-stu-id="a8033-110">The **Service** resource configures Windows services.</span></span>

```syntax
Service [String] #ResourceName
{
    Name = [string]
    [BuiltInAccount = [string]{ LocalService | LocalSystem | NetworkService }]
    [Credential = [PSCredential]]
    [Dependencies = [string[]]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [DisplayName = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Path = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [StartupType = [string]{ Automatic | Disabled | Manual }]
    [State = [string]{ Running | Stopped }]
}
```

<span data-ttu-id="a8033-111">A **szolgáltatási** erőforrás **Get**, **test**és **set** metódusának paraméter-blokkokkal kell elfogadnia ezeket az értékeket.</span><span class="sxs-lookup"><span data-stu-id="a8033-111">The **Get**, **Test**, and **Set** methods of the **Service** resource will have parameter blocks that accept these values.</span></span>

```powershell
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [System.String]
        $Name,

        [System.String]
        [ValidateSet("Automatic", "Manual", "Disabled")]
        $StartupType,

        [System.String]
        [ValidateSet("LocalSystem", "LocalService", "NetworkService")]
        $BuiltInAccount,

        [System.Management.Automation.PSCredential]
        [ValidateNotNull()]
        $Credential,

        [System.String]
        [ValidateSet("Running", "Stopped")]
        $State="Running",

        [System.String]
        [ValidateNotNullOrEmpty()]
        $DisplayName,

        [System.String]
        [ValidateNotNullOrEmpty()]
        $Description,

        [System.String]
        [ValidateNotNullOrEmpty()]
        $Path,

        [System.String[]]
        [ValidateNotNullOrEmpty()]
        $Dependencies,

        [System.String]
        [ValidateSet("Present", "Absent")]
        $Ensure="Present"
    )
```

> [!NOTE]
> <span data-ttu-id="a8033-112">Az erőforrás definiálásához használt nyelv és metódus határozza meg a **Get**, a **test**és a **set** metódusok meghatározásának módját.</span><span class="sxs-lookup"><span data-stu-id="a8033-112">The language and method used to define the resource determines how the **Get**, **Test**, and **Set** methods will be defined.</span></span>

<span data-ttu-id="a8033-113">Mivel a **szolgáltatási** erőforrásnak csak egy kötelező kulcsa (`Name`) van, a **szolgáltatási** blokk erőforrásai a következőképpen lehetnek egyszerűek:</span><span class="sxs-lookup"><span data-stu-id="a8033-113">Because the **Service** resource only has one required key (`Name`), a **Service** block resource could be as simple as this:</span></span>

```powershell
Configuration TestConfig
{
    Import-DSCResource -Name Service
    Node localhost
    {
        Service "MyService"
        {
            Name = "Spooler"
        }
    }
}
```

<span data-ttu-id="a8033-114">A fenti konfiguráció fordításakor a rendszer a kulcshoz megadott értékeket a generált ". MOF" fájlban tárolja.</span><span class="sxs-lookup"><span data-stu-id="a8033-114">When you compile the Configuration above, the values you specify for a key are stored in the ".mof" file that is generated.</span></span> <span data-ttu-id="a8033-115">További információ: [MOF](/windows/desktop/wmisdk/managed-object-format--mof-).</span><span class="sxs-lookup"><span data-stu-id="a8033-115">For more information, see [MOF](/windows/desktop/wmisdk/managed-object-format--mof-).</span></span>

```
instance of MSFT_ServiceResource as $MSFT_ServiceResource1ref
{
SourceInfo = "::5::1::Service";
 ModuleName = "PsDesiredStateConfiguration";
 ResourceID = "[Service]MyService";
 Name = "Spooler";

ModuleVersion = "1.0";

 ConfigurationName = "Test";

};
```

<span data-ttu-id="a8033-116">Alkalmazása esetén a [helyi Configuration Manager](../managing-nodes/metaConfig.md) (LCD ChipOnGlas) a ". `-Name` MOF" fájlból olvassa be a "sorkezelő" értéket, és átadja a **Get**, **test**és **set** metódusok paraméterének a következőhöz: "MyService"  **Szolgáltatási** erőforrás.</span><span class="sxs-lookup"><span data-stu-id="a8033-116">When applied, the [Local Configuration Manager](../managing-nodes/metaConfig.md) (LCM) will read the value "Spooler" from the ".mof" file, and pass it to the `-Name` parameter of the **Get**, **Test**, and **Set** methods for the "MyService" instance of the **Service** resource.</span></span>

## <a name="get"></a><span data-ttu-id="a8033-117">Lekérés</span><span class="sxs-lookup"><span data-stu-id="a8033-117">Get</span></span>

<span data-ttu-id="a8033-118">Egy erőforrás **Get** metódusa lekéri az erőforrás állapotát, ahogy azt a célként megadott csomóponton konfigurálták.</span><span class="sxs-lookup"><span data-stu-id="a8033-118">The **Get** method of a resource, retrieves the state of the resource as it is configured on the target Node.</span></span> <span data-ttu-id="a8033-119">Ezt az állapotot [szórótábla](/powershell/module/microsoft.powershell.core/about/about_hash_tables)adja vissza.</span><span class="sxs-lookup"><span data-stu-id="a8033-119">This state is returned as a [hashtable](/powershell/module/microsoft.powershell.core/about/about_hash_tables).</span></span> <span data-ttu-id="a8033-120">A **szórótábla** kulcsai lesznek a konfigurálható értékek vagy paraméterek, amelyeket az erőforrás elfogad.</span><span class="sxs-lookup"><span data-stu-id="a8033-120">The keys of the **hashtable** will be the configurable values, or parameters, the resource accepts.</span></span>

<span data-ttu-id="a8033-121">A **Get** metódus leképezi közvetlenül a [Get-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="a8033-121">The **Get** method maps directly to the [Get-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) cmdlet.</span></span> <span data-ttu-id="a8033-122">A hívásakor `Get-DSCConfiguration`az LCD a jelenleg alkalmazott konfigurációban futtatja az egyes erőforrások **Get** metódusát.</span><span class="sxs-lookup"><span data-stu-id="a8033-122">When you call `Get-DSCConfiguration`, the LCM runs the **Get** method of each resource in the currently applied configuration.</span></span> <span data-ttu-id="a8033-123">Az LCD ChipOnGlas a ". MOF" fájlban tárolt kulcs értékeket használja paraméterekként az összes kapcsolódó erőforrás-példányhoz.</span><span class="sxs-lookup"><span data-stu-id="a8033-123">The LCM uses the key values stored in the ".mof" file as parameters to each corresponding resource instance.</span></span>

<span data-ttu-id="a8033-124">Ez egy olyan **szolgáltatási** erőforrás mintája, amely a "sorkezelő" szolgáltatást konfigurálja.</span><span class="sxs-lookup"><span data-stu-id="a8033-124">This is sample output from a **Service** resource that configures the "Spooler" service.</span></span>

```output
ConfigurationName    : Test
DependsOn            :
ModuleName           : PsDesiredStateConfiguration
ModuleVersion        : 1.1
PsDscRunAsCredential :
ResourceId           : [Service]Spooler
SourceInfo           :
BuiltInAccount       : LocalSystem
Credential           :
Dependencies         : {RPCSS, http}
Description          : This service spools print jobs and handles interaction with the printer.  If you turn off
                       this service, you won’t be able to print or see your printers.
DisplayName          : Print Spooler
Ensure               :
Name                 : Spooler
Path                 : C:\WINDOWS\System32\spoolsv.exe
StartupType          : Automatic
State                : Running
Status               :
PSComputerName       :
CimClassName         : MSFT_ServiceResource
```

<span data-ttu-id="a8033-125">A kimenet a **szolgáltatási** erőforrás által konfigurálható aktuális érték tulajdonságokat jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="a8033-125">The output shows the current value properties configurable by the **Service** resource.</span></span>

```syntax
Service [String] #ResourceName
{
    Name = [string]
    [BuiltInAccount = [string]{ LocalService | LocalSystem | NetworkService }]
    [Credential = [PSCredential]]
    [Dependencies = [string[]]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [DisplayName = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Path = [string]]
    [PsDscRunAsCredential = [PSCredential]]
    [StartupType = [string]{ Automatic | Disabled | Manual }]
    [State = [string]{ Running | Stopped }]
}
```

## <a name="test"></a><span data-ttu-id="a8033-126">Teszt</span><span class="sxs-lookup"><span data-stu-id="a8033-126">Test</span></span>

<span data-ttu-id="a8033-127">Egy erőforrás **tesztelési** módszere határozza meg, hogy a cél csomópont jelenleg megfelel-e az erőforrás *kívánt állapotának*.</span><span class="sxs-lookup"><span data-stu-id="a8033-127">The **Test** method of a resource determines if the target node is currently compliant with the resource's *desired state*.</span></span> <span data-ttu-id="a8033-128">A **teszt** metódus `$True` visszaadja `$False` vagy csak azt jelzi, hogy a csomópont megfelelő-e.</span><span class="sxs-lookup"><span data-stu-id="a8033-128">The **Test** method returns `$True` or `$False` only to indicate whether the Node is compliant.</span></span>
<span data-ttu-id="a8033-129">A [test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)hívásakor az LCD ChipOnGlas a jelenleg alkalmazott konfigurációban meghívja az egyes erőforrások **tesztelési** módszerét.</span><span class="sxs-lookup"><span data-stu-id="a8033-129">When you call [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration), the LCM calls the **Test** method of each resource in the currently applied configuration.</span></span> <span data-ttu-id="a8033-130">Az LCD ChipOnGlas a ". MOF" fájlban tárolt kulcs értékeket használja paraméterekként az összes kapcsolódó erőforrás-példányhoz.</span><span class="sxs-lookup"><span data-stu-id="a8033-130">The LCM uses the key values stored in the ".mof" file as parameters to each corresponding resource instance.</span></span>

<span data-ttu-id="a8033-131">Ha egy adott erőforrás **tesztje** `$False`eredményét adja vissza, `Test-DSCConfiguration` a `$False` függvény azt jelzi, hogy a csomópont nem megfelelő.</span><span class="sxs-lookup"><span data-stu-id="a8033-131">If the result of any individual resource's **Test** is `$False`, `Test-DSCConfiguration` returns `$False` indicating that the Node is not compliant.</span></span> <span data-ttu-id="a8033-132">Ha az összes erőforrás **tesztelési** módszere `Test-DSCConfiguration` visszatér `$True` `$True`, a visszatérési érték azt jelzi, hogy a csomópont megfelelő.</span><span class="sxs-lookup"><span data-stu-id="a8033-132">If all resource's **Test** methods return `$True`, `Test-DSCConfiguration` returns `$True` to indicate that the Node is compliant.</span></span>

```powershell
Test-DSCConfiguration
```

```output
True
```

<span data-ttu-id="a8033-133">A PowerShell 5,0-től kezdve `-Detailed` a paraméter hozzá lett adva.</span><span class="sxs-lookup"><span data-stu-id="a8033-133">Beginning in PowerShell 5.0, the `-Detailed` parameter was added.</span></span> <span data-ttu-id="a8033-134">A megfelelő és `Test-DSCConfiguration` nem megfelelő erőforrások eredményeinek gyűjteményét tartalmazó objektum visszaadásának okai.`-Detailed`</span><span class="sxs-lookup"><span data-stu-id="a8033-134">Specifying `-Detailed` causes `Test-DSCConfiguration` to return an object containing collections of results for compliant, and non-compliant resources.</span></span>

```powershell
Test-DSCConfiguration -Detailed
```

```output
PSComputerName  ResourcesInDesiredState        ResourcesNotInDesiredState     InDesiredState
--------------  -----------------------        --------------------------     --------------
localhost       {[Service]Spooler}                                            True
```

<span data-ttu-id="a8033-135">További információ: [test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)</span><span class="sxs-lookup"><span data-stu-id="a8033-135">For more information, see [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)</span></span>

## <a name="set"></a><span data-ttu-id="a8033-136">Beállítás</span><span class="sxs-lookup"><span data-stu-id="a8033-136">Set</span></span>

<span data-ttu-id="a8033-137">Egy erőforrás **set** metódusa megkísérli kényszeríteni a csomópontot, hogy az megfeleljen az erőforrás *kívánt állapotának*.</span><span class="sxs-lookup"><span data-stu-id="a8033-137">The **Set** method of a resource attempts to force the Node to become compliant with the resource's *desired state*.</span></span> <span data-ttu-id="a8033-138">A **set** metódusnak **idempotens**kell lennie, ami azt jelenti, hogy a **készlet** többször is futhat, és hibák nélkül mindig ugyanazt az eredményt kapja.</span><span class="sxs-lookup"><span data-stu-id="a8033-138">The **Set** method is meant to be **idempotent**, which means that **Set** could be run multiple times and always get the same result without errors.</span></span>  <span data-ttu-id="a8033-139">A [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Start-DSCConfiguration)futtatásakor az LCD ChipOnGlas az aktuálisan alkalmazott konfigurációban lévő összes erőforráson keresztüli ciklust használ.</span><span class="sxs-lookup"><span data-stu-id="a8033-139">When you run [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Start-DSCConfiguration), the LCM cycles through each resource in the currently applied configuration.</span></span> <span data-ttu-id="a8033-140">Az LCD ChipOnGlas lekéri az aktuális erőforrás-példány kulcsának értékeit a ". MOF" fájlból, és paraméterként használja azokat a **tesztelési** módszerhez.</span><span class="sxs-lookup"><span data-stu-id="a8033-140">The LCM retrieves key values for the current resource instance from the ".mof" file and uses them as parameters for the **Test** method.</span></span> <span data-ttu-id="a8033-141">Ha a **teszt** metódus visszatér `$True`, a csomópont megfelel az aktuális erőforrásnak, és a **set** metódus ki lesz hagyva.</span><span class="sxs-lookup"><span data-stu-id="a8033-141">If the **Test** method returns `$True`, the Node is compliant with the current resource, and the **Set** method is skipped.</span></span> <span data-ttu-id="a8033-142">Ha a **teszt** eredménye `$False`, a csomópont nem megfelelő.</span><span class="sxs-lookup"><span data-stu-id="a8033-142">If the **Test** returns `$False`, the Node is non-compliant.</span></span>  <span data-ttu-id="a8033-143">Az LCD ChipOnGlas az erőforrás-példány kulcsának értékeit paraméterként adja át az erőforrás **beállított** metódusának, és a csomópontot a megfelelőségre állítja vissza.</span><span class="sxs-lookup"><span data-stu-id="a8033-143">The LCM passes the resource instance's key values as parameters to the resource's **Set** method, restoring the Node to compliance.</span></span>

<span data-ttu-id="a8033-144">A és `-Verbose` `-Wait` a paraméterek megadásával `Start-DSCConfiguration` megtekintheti a parancsmag előrehaladását.</span><span class="sxs-lookup"><span data-stu-id="a8033-144">By specifying the `-Verbose` and `-Wait` parameters, you can watch the progress of the `Start-DSCConfiguration` cmdlet.</span></span> <span data-ttu-id="a8033-145">Ebben a példában a csomópont már megfelelő.</span><span class="sxs-lookup"><span data-stu-id="a8033-145">In this example, the Node is already compliant.</span></span> <span data-ttu-id="a8033-146">A `Verbose` kimenet azt jelzi, hogy a **set** metódus ki lett hagyva.</span><span class="sxs-lookup"><span data-stu-id="a8033-146">The `Verbose` output indicates that the **Set** method was skipped.</span></span>

```
PS> Start-DSCConfiguration -Verbose -Wait -UseExisting

VERBOSE: Perform operation 'Invoke CimMethod' with following parameters, ''methodName' =
ApplyConfiguration,'className' = MSFT_DSCLocalConfigurationManager,'namespaceName' =
root/Microsoft/Windows/DesiredStateConfiguration'.
VERBOSE: An LCM method call arrived from computer SERVER01 with user sid
S-1-5-21-124525095-708259637-1543119021-1282804.
VERBOSE: [SERVER01]:                            [] Starting consistency engine.
VERBOSE: [SERVER01]:                            [] Checking consistency for current configuration.
VERBOSE: [SERVER01]:                            [DSCEngine] Importing the module
C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\DscResources\MSFT_ServiceResource\MSFT
_ServiceResource.psm1 in force mode.
VERBOSE: [SERVER01]: LCM:  [ Start  Resource ]  [[Service]Spooler]
VERBOSE: [SERVER01]: LCM:  [ Start  Test     ]  [[Service]Spooler]
VERBOSE: [SERVER01]:                            [[Service]Spooler] Importing the module MSFT_ServiceResource in
force mode.
VERBOSE: [SERVER01]: LCM:  [ End    Test     ]  [[Service]Spooler]  in 0.2540 seconds.
VERBOSE: [SERVER01]: LCM:  [ Skip   Set      ]  [[Service]Spooler]
VERBOSE: [SERVER01]: LCM:  [ End    Resource ]  [[Service]Spooler]
VERBOSE: [SERVER01]:                            [] Consistency check completed.
VERBOSE: Operation 'Invoke CimMethod' complete.
VERBOSE: Time taken for configuration job to complete is 1.379 seconds
```

## <a name="see-also"></a><span data-ttu-id="a8033-147">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a8033-147">See also</span></span>

- [<span data-ttu-id="a8033-148">Azure Automation DSC – áttekintés</span><span class="sxs-lookup"><span data-stu-id="a8033-148">Azure Automation DSC Overview</span></span>](https://docs.microsoft.com/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="a8033-149">SMB-lekérési kiszolgáló beállítása</span><span class="sxs-lookup"><span data-stu-id="a8033-149">Setting up an SMB pull server</span></span>](../pull-server/pullServerSMB.md)
- [<span data-ttu-id="a8033-150">Lekérési ügyfél konfigurálása</span><span class="sxs-lookup"><span data-stu-id="a8033-150">Configuring a pull client</span></span>](../pull-server/pullClientConfigID.md)
