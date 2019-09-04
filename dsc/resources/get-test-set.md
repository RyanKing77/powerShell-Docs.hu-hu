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
# <a name="get-test-set"></a>Get-test-set

>Érvényes: Windows PowerShell 4,0, Windows PowerShell 5,0

![Get, Test és Set](../media/get-test-set.png)

A PowerShell kívánt állapotának konfigurálása **Get**, **test**és **set** folyamat körül történik. A DSC- [erőforrások](resources.md) mindegyike metódust tartalmaz az egyes műveletek végrehajtásához. Egy [konfigurációban](../configurations/configurations.md)az erőforrás-blokkokat úgy definiálhatja, hogy kitöltse azokat a kulcsokat, amelyek egy erőforrás **Get**, **test**és **set** metódusának paraméterei lesznek.

Ez a **szolgáltatás** -erőforrás blokk szintaxisa. A **szolgáltatási** erőforrás konfigurálja a Windows-szolgáltatásokat.

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

A **szolgáltatási** erőforrás **Get**, **test**és **set** metódusának paraméter-blokkokkal kell elfogadnia ezeket az értékeket.

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
> Az erőforrás definiálásához használt nyelv és metódus határozza meg a **Get**, a **test**és a **set** metódusok meghatározásának módját.

Mivel a **szolgáltatási** erőforrásnak csak egy kötelező kulcsa (`Name`) van, a **szolgáltatási** blokk erőforrásai a következőképpen lehetnek egyszerűek:

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

A fenti konfiguráció fordításakor a rendszer a kulcshoz megadott értékeket a generált ". MOF" fájlban tárolja. További információ: [MOF](/windows/desktop/wmisdk/managed-object-format--mof-).

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

Alkalmazása esetén a [helyi Configuration Manager](../managing-nodes/metaConfig.md) (LCD ChipOnGlas) a ". `-Name` MOF" fájlból olvassa be a "sorkezelő" értéket, és átadja a **Get**, **test**és **set** metódusok paraméterének a következőhöz: "MyService"  **Szolgáltatási** erőforrás.

## <a name="get"></a>Lekérés

Egy erőforrás **Get** metódusa lekéri az erőforrás állapotát, ahogy azt a célként megadott csomóponton konfigurálták. Ezt az állapotot [szórótábla](/powershell/module/microsoft.powershell.core/about/about_hash_tables)adja vissza. A **szórótábla** kulcsai lesznek a konfigurálható értékek vagy paraméterek, amelyeket az erőforrás elfogad.

A **Get** metódus leképezi közvetlenül a [Get-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) parancsmagot. A hívásakor `Get-DSCConfiguration`az LCD a jelenleg alkalmazott konfigurációban futtatja az egyes erőforrások **Get** metódusát. Az LCD ChipOnGlas a ". MOF" fájlban tárolt kulcs értékeket használja paraméterekként az összes kapcsolódó erőforrás-példányhoz.

Ez egy olyan **szolgáltatási** erőforrás mintája, amely a "sorkezelő" szolgáltatást konfigurálja.

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

A kimenet a **szolgáltatási** erőforrás által konfigurálható aktuális érték tulajdonságokat jeleníti meg.

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

## <a name="test"></a>Teszt

Egy erőforrás **tesztelési** módszere határozza meg, hogy a cél csomópont jelenleg megfelel-e az erőforrás *kívánt állapotának*. A **teszt** metódus `$True` visszaadja `$False` vagy csak azt jelzi, hogy a csomópont megfelelő-e.
A [test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)hívásakor az LCD ChipOnGlas a jelenleg alkalmazott konfigurációban meghívja az egyes erőforrások **tesztelési** módszerét. Az LCD ChipOnGlas a ". MOF" fájlban tárolt kulcs értékeket használja paraméterekként az összes kapcsolódó erőforrás-példányhoz.

Ha egy adott erőforrás **tesztje** `$False`eredményét adja vissza, `Test-DSCConfiguration` a `$False` függvény azt jelzi, hogy a csomópont nem megfelelő. Ha az összes erőforrás **tesztelési** módszere `Test-DSCConfiguration` visszatér `$True` `$True`, a visszatérési érték azt jelzi, hogy a csomópont megfelelő.

```powershell
Test-DSCConfiguration
```

```output
True
```

A PowerShell 5,0-től kezdve `-Detailed` a paraméter hozzá lett adva. A megfelelő és `Test-DSCConfiguration` nem megfelelő erőforrások eredményeinek gyűjteményét tartalmazó objektum visszaadásának okai.`-Detailed`

```powershell
Test-DSCConfiguration -Detailed
```

```output
PSComputerName  ResourcesInDesiredState        ResourcesNotInDesiredState     InDesiredState
--------------  -----------------------        --------------------------     --------------
localhost       {[Service]Spooler}                                            True
```

További információ: [test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)

## <a name="set"></a>Beállítás

Egy erőforrás **set** metódusa megkísérli kényszeríteni a csomópontot, hogy az megfeleljen az erőforrás *kívánt állapotának*. A **set** metódusnak **idempotens**kell lennie, ami azt jelenti, hogy a **készlet** többször is futhat, és hibák nélkül mindig ugyanazt az eredményt kapja.  A [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Start-DSCConfiguration)futtatásakor az LCD ChipOnGlas az aktuálisan alkalmazott konfigurációban lévő összes erőforráson keresztüli ciklust használ. Az LCD ChipOnGlas lekéri az aktuális erőforrás-példány kulcsának értékeit a ". MOF" fájlból, és paraméterként használja azokat a **tesztelési** módszerhez. Ha a **teszt** metódus visszatér `$True`, a csomópont megfelel az aktuális erőforrásnak, és a **set** metódus ki lesz hagyva. Ha a **teszt** eredménye `$False`, a csomópont nem megfelelő.  Az LCD ChipOnGlas az erőforrás-példány kulcsának értékeit paraméterként adja át az erőforrás **beállított** metódusának, és a csomópontot a megfelelőségre állítja vissza.

A és `-Verbose` `-Wait` a paraméterek megadásával `Start-DSCConfiguration` megtekintheti a parancsmag előrehaladását. Ebben a példában a csomópont már megfelelő. A `Verbose` kimenet azt jelzi, hogy a **set** metódus ki lett hagyva.

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

## <a name="see-also"></a>Lásd még:

- [Azure Automation DSC – áttekintés](https://docs.microsoft.com/azure/automation/automation-dsc-overview)
- [SMB-lekérési kiszolgáló beállítása](../pull-server/pullServerSMB.md)
- [Lekérési ügyfél konfigurálása](../pull-server/pullClientConfigID.md)
