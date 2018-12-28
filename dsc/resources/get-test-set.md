---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Get-teszt – Set
ms.openlocfilehash: e46710954679bf20f4536c6efbcbd4dafd9e629e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404240"
---
# <a name="get-test-set"></a><span data-ttu-id="1f858-103">Get-teszt – Set</span><span class="sxs-lookup"><span data-stu-id="1f858-103">Get-Test-Set</span></span>

><span data-ttu-id="1f858-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1f858-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

![GET, tesztelési, és állítsa be](/media/get-test-set.png)

<span data-ttu-id="1f858-106">PowerShell Desired State Configuration körül jön létre egy **első**, **teszt**, és **beállítása** folyamat.</span><span class="sxs-lookup"><span data-stu-id="1f858-106">PowerShell Desired State Configuration is constructed around a **Get**, **Test**, and **Set** process.</span></span> <span data-ttu-id="1f858-107">DSC [erőforrások](resources.md) minden tartalmaz módszerek mindkét művelet végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="1f858-107">DSC [resources](resources.md) each contains methods to complete each of these operations.</span></span> <span data-ttu-id="1f858-108">Az egy [konfigurációs](../configurations/configurations.md), meg kell adni, amely egy erőforrás paraméterek válnak kulcsok erőforrás blokkok határoz meg **első**, **teszt**, és **beállítása** metódusok.</span><span class="sxs-lookup"><span data-stu-id="1f858-108">In a [Configuration](../configurations/configurations.md), you define resource blocks to fill in keys that become parameters for a resource's **Get**, **Test**, and **Set** methods.</span></span>

<span data-ttu-id="1f858-109">Ez szintaxisa látható egy **szolgáltatás** erőforrás letiltása.</span><span class="sxs-lookup"><span data-stu-id="1f858-109">This is the syntax for a **Service** resource block.</span></span> <span data-ttu-id="1f858-110">A **szolgáltatás** erőforrás konfigurálja a Windows-szolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="1f858-110">The **Service** resource configures Windows services.</span></span>

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

<span data-ttu-id="1f858-111">A **első**, **teszt**, és **beállítása** módszerek a **szolgáltatás** erőforrás lesz paraméter blokkolja, hogy fogadja el ezeket az értékeket.</span><span class="sxs-lookup"><span data-stu-id="1f858-111">The **Get**, **Test**, and **Set** methods of the **Service** resource will have parameter blocks that accept these values.</span></span>

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
> <span data-ttu-id="1f858-112">A nyelv és az erőforrás meghatározásához használt módszer határozza meg, hogyan a **első**, **teszt**, és **beállítása** módszerek meg lesznek határozva.</span><span class="sxs-lookup"><span data-stu-id="1f858-112">The language and method used to define the resource determines how the **Get**, **Test**, and **Set** methods will be defined.</span></span>

<span data-ttu-id="1f858-113">Mivel a **szolgáltatás** erőforrás csak rendelkezik egy szükséges kulcs (`Name`), amely egy **szolgáltatás** blokk erőforrás egyszerű a megoldás lehet:</span><span class="sxs-lookup"><span data-stu-id="1f858-113">Because the **Service** resource only has one required key (`Name`), a **Service** block resource could be as simple as this:</span></span>

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

<span data-ttu-id="1f858-114">Ha a fenti konfiguráció fordítása, egy kulcsot a megadott értékek a ".mof" fájl, amelyet vannak tárolva.</span><span class="sxs-lookup"><span data-stu-id="1f858-114">When you compile the Configuration above, the values you specify for a key are stored in the ".mof" file that is generated.</span></span> <span data-ttu-id="1f858-115">További információkért lásd: [MOF](/windows/desktop/wmisdk/managed-object-format--mof-).</span><span class="sxs-lookup"><span data-stu-id="1f858-115">For more information, see [MOF](/windows/desktop/wmisdk/managed-object-format--mof-).</span></span>

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

<span data-ttu-id="1f858-116">Alkalmazásakor a [helyi Configuration Manager](../managing-nodes/metaConfig.md) olvassa el az értéket "Nyomtatásisor-kezelő" a ".mof" fájlból, majd adja azt át a `-Name` paraméterében a **első**, **teszt**, és **beállítása** módszerek "MyService" példányának a **szolgáltatás** erőforrás.</span><span class="sxs-lookup"><span data-stu-id="1f858-116">When applied, the [Local Configuration Manager](../managing-nodes/metaConfig.md) will read the value "Spooler" from the ".mof" file, and pass it to the `-Name` parameter of the **Get**, **Test**, and **Set** methods for the "MyService" instance of the **Service** resource.</span></span>

## <a name="get"></a><span data-ttu-id="1f858-117">Lekérés</span><span class="sxs-lookup"><span data-stu-id="1f858-117">Get</span></span>

<span data-ttu-id="1f858-118">A **első** módszer egy adott erőforrás az erőforrás állapotát kérdezi le, a cél csomópont konfigurálva van.</span><span class="sxs-lookup"><span data-stu-id="1f858-118">The **Get** method of a resource, retrieves the state of the resource as it is configured on the target Node.</span></span> <span data-ttu-id="1f858-119">Ebben az állapotban adja vissza egy [kivonattábla](/powershell/module/microsoft.powershell.core/about/about_hash_tables).</span><span class="sxs-lookup"><span data-stu-id="1f858-119">This state is returned as a [hashtable](/powershell/module/microsoft.powershell.core/about/about_hash_tables).</span></span> <span data-ttu-id="1f858-120">A kulcsait a **kivonattábla** lesz a konfigurálható értékeket, vagy a paraméterek, az erőforrás fogad el.</span><span class="sxs-lookup"><span data-stu-id="1f858-120">The keys of the **hashtable** will be the configurable values, or parameters, the resource accepts.</span></span>

<span data-ttu-id="1f858-121">A **első** metódus közvetlenül leképezve a [Get-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1f858-121">The **Get** method maps directly to the [Get-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) cmdlet.</span></span> <span data-ttu-id="1f858-122">Meghívásakor `Get-DSCConfiguration`, az LCM fut a **első** metódus az egyes erőforrások jelenleg alkalmazott konfigurációjában.</span><span class="sxs-lookup"><span data-stu-id="1f858-122">When you call `Get-DSCConfiguration`, the LCM runs the **Get** method of each resource in the currently applied configuration.</span></span> <span data-ttu-id="1f858-123">Az LCM paraméterekként minden kapcsolódó erőforrás-példányra ".mof" fájljában tárolt kulcs értékeit használja.</span><span class="sxs-lookup"><span data-stu-id="1f858-123">The LCM uses the key values stored in the ".mof" file as parameters to each corresponding resource instance.</span></span>

<span data-ttu-id="1f858-124">Ez a minta kimenete egy **szolgáltatás** erőforrás, amely konfigurálja a "Nyomtatásisor-kezelő" szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="1f858-124">This is sample output from a **Service** resource that configures the "Spooler" service.</span></span>

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

<span data-ttu-id="1f858-125">A kimenet mutatja a jelenlegi érték tulajdonságok szerint konfigurálható a **szolgáltatás** erőforrás.</span><span class="sxs-lookup"><span data-stu-id="1f858-125">The output shows the current value properties configurable by the **Service** resource.</span></span>

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

## <a name="test"></a><span data-ttu-id="1f858-126">Teszt</span><span class="sxs-lookup"><span data-stu-id="1f858-126">Test</span></span>

<span data-ttu-id="1f858-127">A **teszt** módszer egy adott erőforrás meghatározza, hogy a célcsomópont jelenleg felelnek meg az erőforrás *kívánt állapot*.</span><span class="sxs-lookup"><span data-stu-id="1f858-127">The **Test** method of a resource determines if the target node is currently compliant with the resource's *desired state*.</span></span> <span data-ttu-id="1f858-128">A **teszt** metódus visszatért `$True` vagy `$False` , csak adja meg, hogy a csomópont megfelelő.</span><span class="sxs-lookup"><span data-stu-id="1f858-128">The **Test** method returns `$True` or `$False` only to indicate whether the Node is compliant.</span></span>
<span data-ttu-id="1f858-129">Meghívásakor [a Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration), a LCM meghívja a **teszt** metódus az egyes erőforrások jelenleg alkalmazott konfigurációjában.</span><span class="sxs-lookup"><span data-stu-id="1f858-129">When you call [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration), the LCM calls the **Test** method of each resource in the currently applied configuration.</span></span> <span data-ttu-id="1f858-130">Az LCM paraméterekként minden kapcsolódó erőforrás-példányra ".mof" fájljában tárolt kulcs értékeit használja.</span><span class="sxs-lookup"><span data-stu-id="1f858-130">The LCM uses the key values stored in the ".mof" file as parameters to each corresponding resource instance.</span></span>

<span data-ttu-id="1f858-131">Ha az eredmény minden egyes erőforrás **teszt** van `$False`, `Test-DSCConfiguration` adja vissza `$False` jelzi, hogy a csomópont esetében ez nem engedélyezett.</span><span class="sxs-lookup"><span data-stu-id="1f858-131">If the result of any individual resource's **Test** is `$False`, `Test-DSCConfiguration` returns `$False` indicating that the Node is not compliant.</span></span> <span data-ttu-id="1f858-132">Ha az összes erőforrás **teszt** módszerek is szolgálnak `$True`, `Test-DSCConfiguration` adja vissza `$True` azt jelzi, hogy a csomópont megfelelő.</span><span class="sxs-lookup"><span data-stu-id="1f858-132">If all resource's **Test** methods return `$True`, `Test-DSCConfiguration` returns `$True` to indicate that the Node is compliant.</span></span>

```powershell
Test-DSCConfiguration
```

```output
True
```

<span data-ttu-id="1f858-133">A PowerShell 5.0-, kezdve a `-Detailed` paraméter hozzá lett adva.</span><span class="sxs-lookup"><span data-stu-id="1f858-133">Beginning in PowerShell 5.0, the `-Detailed` parameter was added.</span></span> <span data-ttu-id="1f858-134">Adjon meg `-Detailed` hatására `Test-DSCConfiguration` visszaadandó eredmények megfelelő és nem megfelelő erőforrások gyűjteményei tartalmazó objektumot.</span><span class="sxs-lookup"><span data-stu-id="1f858-134">Specifying `-Detailed` causes `Test-DSCConfiguration` to return an object containing collections of results for compliant, and non-compliant resources.</span></span>

```powershell
Test-DSCConfiguration -Detailed
```

```output
PSComputerName  ResourcesInDesiredState        ResourcesNotInDesiredState     InDesiredState
--------------  -----------------------        --------------------------     --------------
localhost       {[Service]Spooler}                                            True
```

<span data-ttu-id="1f858-135">További információkért lásd: [a Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)</span><span class="sxs-lookup"><span data-stu-id="1f858-135">For more information, see [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)</span></span>

## <a name="set"></a><span data-ttu-id="1f858-136">Beállítás</span><span class="sxs-lookup"><span data-stu-id="1f858-136">Set</span></span>

<span data-ttu-id="1f858-137">A **beállítása** módszer egy adott erőforrás próbál kényszerítheti a csomópont az erőforrás megfelelő *kívánt állapot*.</span><span class="sxs-lookup"><span data-stu-id="1f858-137">The **Set** method of a resource attempts to force the Node to become compliant with the resource's *desired state*.</span></span> <span data-ttu-id="1f858-138">A **beállítása** módszer helyezni **idempotens**, ami azt jelenti, hogy **beállítása** lehet több példányban, és mindig elérhető ugyanaz az eredmény hiba nélkül.</span><span class="sxs-lookup"><span data-stu-id="1f858-138">The **Set** method is meant to be **idempotent**, which means that **Set** could be run multiple times and always get the same result without errors.</span></span>  <span data-ttu-id="1f858-139">Futtatásakor [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Start-DSCConfiguration), az egyes erőforrások a jelenleg alkalmazott konfiguráció LCM váltás.</span><span class="sxs-lookup"><span data-stu-id="1f858-139">When you run [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Start-DSCConfiguration), the LCM cycles through each resource in the currently applied configuration.</span></span> <span data-ttu-id="1f858-140">Az LCM kérdezi le a kulcs értékeit az aktuális erőforrás-példány a ".mof" fájlból, és használja ezeket a paraméterek a **teszt** metódust.</span><span class="sxs-lookup"><span data-stu-id="1f858-140">The LCM retrieves key values for the current resource instance from the ".mof" file and uses them as parameters for the **Test** method.</span></span> <span data-ttu-id="1f858-141">Ha a **teszt** metódus visszatért `$True`, a csomópont nem felelnek meg az aktuális erőforrás és a **beállítása** metódus a rendszer kihagyta.</span><span class="sxs-lookup"><span data-stu-id="1f858-141">If the **Test** method returns `$True`, the Node is compliant with the current resource, and the **Set** method is skipped.</span></span> <span data-ttu-id="1f858-142">Ha a **teszt** adja vissza `$False`, a csomópont nem megfelelő.</span><span class="sxs-lookup"><span data-stu-id="1f858-142">If the **Test** returns `$False`, the Node is non-compliant.</span></span>  <span data-ttu-id="1f858-143">Az LCM továbbítja az erőforrás példány kulcsérték paraméterként az erőforrás **beállítása** módot, a csomópont megfelelőségi való visszaállítása.</span><span class="sxs-lookup"><span data-stu-id="1f858-143">The LCM passes the resource instance's key values as parameters to the resource's **Set** method, restoring the Node to compliance.</span></span>

<span data-ttu-id="1f858-144">Adja meg a `-Verbose` és `-Wait` paraméterek állapotát megtekintheti a `Start-DSCConfiguration` parancsmag.</span><span class="sxs-lookup"><span data-stu-id="1f858-144">By specifying the `-Verbose` and `-Wait` parameters, you can watch the progress of the `Start-DSCConfiguration` cmdlet.</span></span> <span data-ttu-id="1f858-145">Ebben a példában a csomópont már megfelelő.</span><span class="sxs-lookup"><span data-stu-id="1f858-145">In this example, the Node is already compliant.</span></span> <span data-ttu-id="1f858-146">A `Verbose` kimeneti azt jelzi, hogy a **beállítása** metódus ki lett hagyva.</span><span class="sxs-lookup"><span data-stu-id="1f858-146">The `Verbose` output indicates that the **Set** method was skipped.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="1f858-147">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1f858-147">See also</span></span>

- [<span data-ttu-id="1f858-148">Az Azure Automation DSC – áttekintés</span><span class="sxs-lookup"><span data-stu-id="1f858-148">Azure Automation DSC Overview</span></span>](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
- [<span data-ttu-id="1f858-149">Az SMB-lekérési kiszolgálójának beállítása</span><span class="sxs-lookup"><span data-stu-id="1f858-149">Setting up an SMB pull server</span></span>](../pull-server/pullServerSMB.md)
- [<span data-ttu-id="1f858-150">Lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="1f858-150">Configuring a pull client</span></span>](../pull-server/pullClientConfigID.md)
