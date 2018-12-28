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
# <a name="get-test-set"></a>Get-teszt – Set

>Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

![GET, tesztelési, és állítsa be](/media/get-test-set.png)

PowerShell Desired State Configuration körül jön létre egy **első**, **teszt**, és **beállítása** folyamat. DSC [erőforrások](resources.md) minden tartalmaz módszerek mindkét művelet végrehajtásához. Az egy [konfigurációs](../configurations/configurations.md), meg kell adni, amely egy erőforrás paraméterek válnak kulcsok erőforrás blokkok határoz meg **első**, **teszt**, és **beállítása** metódusok.

Ez szintaxisa látható egy **szolgáltatás** erőforrás letiltása. A **szolgáltatás** erőforrás konfigurálja a Windows-szolgáltatások.

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

A **első**, **teszt**, és **beállítása** módszerek a **szolgáltatás** erőforrás lesz paraméter blokkolja, hogy fogadja el ezeket az értékeket.

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
> A nyelv és az erőforrás meghatározásához használt módszer határozza meg, hogyan a **első**, **teszt**, és **beállítása** módszerek meg lesznek határozva.

Mivel a **szolgáltatás** erőforrás csak rendelkezik egy szükséges kulcs (`Name`), amely egy **szolgáltatás** blokk erőforrás egyszerű a megoldás lehet:

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

Ha a fenti konfiguráció fordítása, egy kulcsot a megadott értékek a ".mof" fájl, amelyet vannak tárolva. További információkért lásd: [MOF](/windows/desktop/wmisdk/managed-object-format--mof-).

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

Alkalmazásakor a [helyi Configuration Manager](../managing-nodes/metaConfig.md) olvassa el az értéket "Nyomtatásisor-kezelő" a ".mof" fájlból, majd adja azt át a `-Name` paraméterében a **első**, **teszt**, és **beállítása** módszerek "MyService" példányának a **szolgáltatás** erőforrás.

## <a name="get"></a>Lekérés

A **első** módszer egy adott erőforrás az erőforrás állapotát kérdezi le, a cél csomópont konfigurálva van. Ebben az állapotban adja vissza egy [kivonattábla](/powershell/module/microsoft.powershell.core/about/about_hash_tables). A kulcsait a **kivonattábla** lesz a konfigurálható értékeket, vagy a paraméterek, az erőforrás fogad el.

A **első** metódus közvetlenül leképezve a [Get-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/get-dscconfiguration) parancsmagot. Meghívásakor `Get-DSCConfiguration`, az LCM fut a **első** metódus az egyes erőforrások jelenleg alkalmazott konfigurációjában. Az LCM paraméterekként minden kapcsolódó erőforrás-példányra ".mof" fájljában tárolt kulcs értékeit használja.

Ez a minta kimenete egy **szolgáltatás** erőforrás, amely konfigurálja a "Nyomtatásisor-kezelő" szolgáltatást.

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

A kimenet mutatja a jelenlegi érték tulajdonságok szerint konfigurálható a **szolgáltatás** erőforrás.

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

A **teszt** módszer egy adott erőforrás meghatározza, hogy a célcsomópont jelenleg felelnek meg az erőforrás *kívánt állapot*. A **teszt** metódus visszatért `$True` vagy `$False` , csak adja meg, hogy a csomópont megfelelő.
Meghívásakor [a Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration), a LCM meghívja a **teszt** metódus az egyes erőforrások jelenleg alkalmazott konfigurációjában. Az LCM paraméterekként minden kapcsolódó erőforrás-példányra ".mof" fájljában tárolt kulcs értékeit használja.

Ha az eredmény minden egyes erőforrás **teszt** van `$False`, `Test-DSCConfiguration` adja vissza `$False` jelzi, hogy a csomópont esetében ez nem engedélyezett. Ha az összes erőforrás **teszt** módszerek is szolgálnak `$True`, `Test-DSCConfiguration` adja vissza `$True` azt jelzi, hogy a csomópont megfelelő.

```powershell
Test-DSCConfiguration
```

```output
True
```

A PowerShell 5.0-, kezdve a `-Detailed` paraméter hozzá lett adva. Adjon meg `-Detailed` hatására `Test-DSCConfiguration` visszaadandó eredmények megfelelő és nem megfelelő erőforrások gyűjteményei tartalmazó objektumot.

```powershell
Test-DSCConfiguration -Detailed
```

```output
PSComputerName  ResourcesInDesiredState        ResourcesNotInDesiredState     InDesiredState
--------------  -----------------------        --------------------------     --------------
localhost       {[Service]Spooler}                                            True
```

További információkért lásd: [a Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)

## <a name="set"></a>Beállítás

A **beállítása** módszer egy adott erőforrás próbál kényszerítheti a csomópont az erőforrás megfelelő *kívánt állapot*. A **beállítása** módszer helyezni **idempotens**, ami azt jelenti, hogy **beállítása** lehet több példányban, és mindig elérhető ugyanaz az eredmény hiba nélkül.  Futtatásakor [Start-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Start-DSCConfiguration), az egyes erőforrások a jelenleg alkalmazott konfiguráció LCM váltás. Az LCM kérdezi le a kulcs értékeit az aktuális erőforrás-példány a ".mof" fájlból, és használja ezeket a paraméterek a **teszt** metódust. Ha a **teszt** metódus visszatért `$True`, a csomópont nem felelnek meg az aktuális erőforrás és a **beállítása** metódus a rendszer kihagyta. Ha a **teszt** adja vissza `$False`, a csomópont nem megfelelő.  Az LCM továbbítja az erőforrás példány kulcsérték paraméterként az erőforrás **beállítása** módot, a csomópont megfelelőségi való visszaállítása.

Adja meg a `-Verbose` és `-Wait` paraméterek állapotát megtekintheti a `Start-DSCConfiguration` parancsmag. Ebben a példában a csomópont már megfelelő. A `Verbose` kimeneti azt jelzi, hogy a **beállítása** metódus ki lett hagyva.

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

- [Az Azure Automation DSC – áttekintés](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
- [Az SMB-lekérési kiszolgálójának beállítása](../pull-server/pullServerSMB.md)
- [Lekérési ügyfél beállítása](../pull-server/pullClientConfigID.md)
