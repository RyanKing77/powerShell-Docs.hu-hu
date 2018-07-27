---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC hibaelhárítása
ms.openlocfilehash: 93a2f3728968882f78d4c050238d226b71c11ca5
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268194"
---
# <a name="troubleshooting-dsc"></a>A DSC hibaelhárítása

_A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0_

Ez a témakör ismerteti azokat a módszereket a DSC elhárításához, ha problémák merülnek fel.

## <a name="winrm-dependency"></a>A WinRM-függőség

Windows PowerShell Desired State Configuration (DSC) attól függ, hogy a Rendszerfelügyeleti webszolgáltatások. A Rendszerfelügyeleti webszolgáltatások a Windows Server 2008 R2 és Windows 7 alapértelmezés szerint nincs engedélyezve. Futtatás `Set-WSManQuickConfig`, egy Windows PowerShell az emelt szintű ahhoz, hogy a WinRM-munkamenetben.

## <a name="using-get-dscconfigurationstatus"></a>Get-DscConfigurationStatus használatával

A [Get-DscConfigurationStatus](https://technet.microsoft.com/library/mt517868.aspx) parancsmag konfigurációs állapotára vonatkozó információkat olvas be egy célcsomóponttal. Egy gazdag objektumot ad vissza, amely tartalmazza-e a konfigurációs Futtatás sikeres volt-e magas szintű információkat. Meg is tárja az objektum felderítését, például futtassa a konfiguráció részleteit:

- Az összes erőforrást, amely nem sikerült
- Bármely erőforrás kért újraindítás
- Meta-konfigurációs beállítások konfigurációs időpontjában futtatása
- Etc.

A következő paraméterkészletet adja vissza a legutóbbi konfiguráció futtatása állapotinformációit:

```
Get-DscConfigurationStatus [-CimSession <CimSession[]>]
                           [-ThrottleLimit <int>]
                           [-AsJob]
                           [<CommonParameters>]
```
A következő paraméterkészletet az összes korábbi konfigurációs futtatások állapotának adatait adja vissza:

```
Get-DscConfigurationStatus -All
                           [-CimSession <CimSession[]>]
                           [-ThrottleLimit <int>]
                           [-AsJob]
                           [<CommonParameters>]
```

## <a name="example"></a>Példa

```powershell
PS C:\> $Status = Get-DscConfigurationStatus

PS C:\> $Status

Status         StartDate                Type            Mode    RebootRequested        NumberOfResources
------        ---------                ----            ----    ---------------        -----------------
Failure        11/24/2015  3:44:56     Consistency        Push    True                36

PS C:\> $Status.ResourcesNotInDesiredState

ConfigurationName     :    MyService
DependsOn             :
ModuleName            :    PSDesiredStateConfiguration
ModuleVersion         :    1.1
PsDscRunAsCredential  :
ResourceID            :    [File]ServiceDll
SourceInfo            :    c:\git\CustomerService\Configs\MyCustomService.ps1::5::34::File
DurationInSeconds     :    0.19
Error                 :    SourcePath must be accessible for current configuration. The related file/directory is:
                           \\Server93\Shared\contosoApp.dll. The related ResourceID is [File]ServiceDll
FinalState            :
InDesiredState        :    False
InitialState          :
InstanceName          :    ServiceDll
RebootRequested       :    False
ReosurceName          :    File
StartDate             :    11/24/2015  3:44:56
PSComputerName        :
```

## <a name="my-script-wont-run-using-dsc-logs-to-diagnose-script-errors"></a>A parancsfájl futtatásának megakadályozása: DSC használatával naplózza a parancsprogram-hibák diagnosztizálása

Minden Windows szoftverek, például DSC rögzíti a hibák és események [naplók](https://msdn.microsoft.com/library/windows/desktop/aa363632.aspx) tekinthetnek meg az a [Eseménynapló](http://windows.microsoft.com/windows/what-information-event-logs-event-viewer).
Ezek a naplók vizsgálata segítségével megtudhatja, miért nem sikerült egy adott művelet, és hogyan hibája megakadályozza a jövőben. Konfigurációs parancsfájlok írása lehet megkülönböztetni, ezért a követési hibákat egyszerűbb, Szerző, a konfiguráció a DSC elemzési eseménynaplójában az előrehaladását úgy követheti nyomon a DSC-Log erőforrás használatával.

## <a name="where-are-dsc-event-logs"></a>Hol találhatók a DSC-eseménynaplók?

Az Eseménynapló DSC események szerepelnek: **alkalmazások és szolgáltatások Logs/Microsoft/Windows/Desired State Configuration**

A megfelelő PowerShell-parancsmag [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx), tekintse meg az eseménynaplókat, is futtathatók:

```
PS C:\> Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"

   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
11/17/2014 10:27:23 PM        4102 Information      Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
```

A fentiek DSC tartozó elsődleges naplófájl neve: **Microsoft -> Windows -> DSC** (a Windows más napló neve nem jelennek itt kivonatosan). Az elsődleges név a rendszer hozzáfűzi a csatorna neve hozhat létre a naplófájl teljes neve. A DSC motor elsősorban három típusú naplók írja: [Operational, elemzési és hibakeresési naplók](https://technet.microsoft.com/library/cc722404.aspx). Mivel az elemzési és hibakeresési naplók alapértelmezés szerint ki van kapcsolva, engedélyezze a őket az eseménynaplóban. Ehhez nyissa meg az eseménynaplót a Windows PowerShellben; Show-Eseménynapló beírásával vagy kattintson a **Start** gombra, majd **Vezérlőpult**, kattintson a **felügyeleti eszközök**, és kattintson a **Eseménynapló**.
Az a **nézet** az eseménynaplóban menüjében kattintson **elemzési és hibakeresési naplók megjelenítése**. A naplófájl neve az elemzési csatorna **elemzési Microsoft-Windows-Dsc**, és a hibakeresési csatorna **Microsoft-Windows-Dsc/Debug**. Is használhatja a [wevtutil](https://technet.microsoft.com/library/cc732848.aspx) segédprogram a naplók engedélyezéséhez az alábbi példában látható módon.

```powershell
wevtutil.exe set-log "Microsoft-Windows-Dsc/Analytic" /q:true /e:true
```

## <a name="what-do-dsc-logs-contain"></a>Mi a DSC-naplók tartalmaznak?

DSC-naplók alatt a három naplózási csatornák, az üzenet fontossága alapján vannak osztva. A DSC a műveleti napló az összes hibaüzenet tartalmazza, és a probléma meghatározásához használható. Az elemzési naplóját nagyobb mennyiségű esemény rendelkezik, és azonosíthatja, ahol a hiba lépett fel. Ez a csatorna is tartalmaz részletes üzenetek a (ha van). A hibakeresési napló tartalmazza, amelyek segítségével jobban megértheti, hogy a hiba történt a naplók. DSC-eseményüzenetek struktúrája úgy, hogy minden eseményüzenet kezdődik, amely egyedileg jelöli egy DSC művelet Feladatazonosítót. Az alábbi példa próbál meg az első esemény a műveleti napló DSC bejelentkezett szerezze be az üzenetet.

```powershell
PS C:\> $AllDscOpEvents = Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
PS C:\> $FirstOperationalEvent = $AllDscOpEvents[0]
PS C:\> $FirstOperationalEvent.Message
Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} :
Consistency engine was run successfully.
```

DSC-események egy adott struktúra, amely lehetővé teszi a felhasználó az egyik DSC-feladat eseményeket naplózza. A struktúra a következőképpen történik:

```
Job ID : <Guid>
<Event Message>
```

## <a name="gathering-events-from-a-single-dsc-operation"></a>DSC egyetlen műveletben eseményeinek gyűjtése

DSC-eseménynaplók DSC különféle műveletek által előállított eseményeket tartalmaz. Azonban általában fogja fontos szempont a részletes csak egy adott műveletet. Minden DSC-naplók csoportosíthatók a feladat azonosító tulajdonság, amely minden DSC művelet esetében egyedi legyen. A feladat azonosítója első tulajdonság értékét minden DSC-esemény jelenik meg. A következő lépések azt ismertetik, hogyan gyűlnek szerkezetben vannak csoportosítva tömb összes eseményt.

```powershell
<##########################################################################
 Step 1 : Enable analytic and debug DSC channels (Operational channel is enabled by default)
###########################################################################>

wevtutil.exe set-log "Microsoft-Windows-Dsc/Analytic" /q:true /e:true
wevtutil.exe set-log "Microsoft-Windows-Dsc/Debug" /q:True /e:true

<##########################################################################
 Step 2 : Perform the required DSC operation (Below is an example, you could run any DSC operation instead)
###########################################################################>

Get-DscLocalConfigurationManager

<##########################################################################
Step 3 : Collect all DSC Logs, from the Analytic, Debug and Operational channels
###########################################################################>

$DscEvents=[System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Operational") `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Analytic" -Oldest) `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Debug" -Oldest)


<##########################################################################
 Step 4 : Group all logs based on the job ID
###########################################################################>
$SeparateDscOperations = $DscEvents | Group {$_.Properties[0].value}
```

Itt, a változó `$SeparateDscOperations` tartalmazza a naplók a feladat-azonosítók szerint csoportosítva. A változó egyes tömbelemeken különböző DSC művelet, engedélyezi a hozzáférést a naplók további információ a naplózott eseményeket egy csoportját jelöli.

```
PS C:\> $SeparateDscOperations

Count Name                      Group
----- ----                      -----
   48 {1A776B6A-5BAC-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
   40 {E557E999-5BA8-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....

PS C:\> $SeparateDscOperations[0].Group

   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/2/2013 3:47:29 PM          4115 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4198 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4114 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4102 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4176 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...
```

Az adatok a változóban kibonthatja `$SeparateDscOperations` használatával [Where-Object](https://technet.microsoft.com/library/ee177028.aspx). Öt forgatókönyvek, amelyben érdemes DSC hibaelhárítási adatokat nyerhet ki a következők:

### <a name="1-operations-failures"></a>1: sikertelen műveletek

Az összes esemény rendelkezik [súlyossági szintek](https://msdn.microsoft.com/library/dd996917(v=vs.85)). Ezek az információk segítségével azonosíthatja a hibaesemények:

```
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.LevelDisplayName -contains "Error"}

Count Name                      Group
----- ----                      -----
   38 {5BCA8BE7-5BB6-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
```

### <a name="2-details-of-operations-run-in-the-last-half-hour"></a>2: a műveletek részletei futtassa az elmúlt fél órában

`TimeCreated`, minden Windows esemény-tulajdonságra állapotok a az esemény létrehozásának ideje. Ennek a tulajdonságnak egy adott dátum/idő objektum összehasonlítása az összes esemény szűrésére használható:

```powershell
PS C:\> $DateLatest = (Get-Date).AddMinutes(-30)
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.TimeCreated -gt $DateLatest}

Count Name                      Group
----- ----                      -----
    1 {6CEC5B09-5BB0-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord}
```

### <a name="3-messages-from-the-latest-operation"></a>3: a legutóbbi művelet üzeneteit

A legutóbbi művelet tárolja az első index a tömb csoport `$SeparateDscOperations`.
A csoport üzenetek 0. index lekérdezése a legutóbbi műveletet üzenetek adja vissza:

```powershell
PS C:\> $SeparateDscOperations[0].Group.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} :
Running consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} :
Configuration is sent from computer NULL by user sid S-1-5-18.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} :
Displaying messages from built-in DSC resources:
 WMI channel 1
 ResourceID:
 Message : [INCH-VM]:                            [] Starting consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} :
Displaying messages from built-in DSC resources:
 WMI channel 1
 ResourceID:
 Message : [INCH-VM]:                            [] Consistency check completed.
```

### <a name="4-error-messages-logged-for-recent-failed-operations"></a>4: legutóbbi sikertelen műveletek a naplóba hibaüzenetek

`$SeparateDscOperations[0].Group` a legutóbbi művelet események egy meghatározott készletének tartalmazza. Futtassa a `Where-Object` parancsmag, amellyel az események szűréséhez állítsa szintű megjelenített név alapján. Az eredmények tárolása az `$myFailedEvent` változó, amely lehet további minél az eseményüzenet beolvasásához:

```powershell
PS C:\> $myFailedEvent = ($SeparateDscOperations[0].Group | Where-Object {$_.LevelDisplayName -eq "Error"})

PS C:\> $myFailedEvent.Message

Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} :
DSC Engine Error :
 Error Message Current configuration does not exist. Execute Start-DscConfiguration command with -Path pa
rameter to specify a configuration file and create a current configuration first.
Error Code : 1
```

### <a name="5-all-events-generated-for-a-particular-job-id"></a>5: összes eseményt hoz létre egy adott feladat.

`$SeparateDscOperations` egy tömb, csoportok, amelyek mindegyike rendelkezik-e a neve megegyezik a feladat egyedi azonosítója. Futtassa a `Where-Object` parancsmagot, kibonthatja a ezeket a csoportokat az eseményeket, amelyek egy adott feladat azonosítója:

```powershell
PS C:\> ($SeparateDscOperations | Where-Object {$_.Name -eq $jobX} ).Group

   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
12/2/2013 4:33:24 PM          4102 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
12/2/2013 4:33:24 PM          4168 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
12/2/2013 4:33:24 PM          4146 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
12/2/2013 4:33:24 PM          4120 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...
```

## <a name="using-xdscdiagnostics-to-analyze-dsc-logs"></a>Naplók elemzéséhez a DSC xDscDiagnostics segítségével

**xDscDiagnostics** egy PowerShell-modul, amely számos funkciót, amely segíthet a gépen a DSC hibák elemzése áll. Ezek a függvények is segít azonosítani az elmúlt DSC műveletek összes helyi esemény vagy a távoli számítógépeken lévő DSC események (érvénytelen hitelesítő adatok). Az előfizetési időszak DSC művelet itt, az egy egyetlen egyedi DSC végrehajtása a kezdetektől a teljes körű meghatározására szolgál. Ha például `Test-DscConfiguration` lenne egy külön DSC művelet. Ehhez hasonlóan más parancsmagjáról DSC (például `Get-DscConfiguration`, `Start-DscConfiguration`használatához és így tovább) minden azonosítható külön DSC műveletként. A függvények vannak írva [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics). Súgó áll rendelkezésre a futó `Get-Help <cmdlet name>`.

### <a name="getting-details-of-dsc-operations"></a>DSC-műveletek részleteinek beolvasása közben

A `Get-xDscOperation` funkció lehetővé teszi a keresse meg az eredményeket a DSC-műveletek, amelyek egy vagy több számítógépen futnak, és adja vissza minden egyes DSC művelet által létrehozott olyan objektum, amely az események gyűjteményét tartalmazza. Például az alábbi kimenet három parancs futtatná. Az elsőt átadva, és a másik két nem sikerült. Ezekkel az eredményekkel foglalja össze a kimenetét `Get-xDscOperation`.

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation

ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents
------------   ---------- -----------           ------   -----                                 ---------
SRV1   1          6/23/2016 9:37:52 AM  Failure  9701aadf-395e-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   2          6/23/2016 9:36:54 AM  Failure  7e8e2d6e-395c-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   3          6/23/2016 9:36:54 AM  Success  af72c6aa-3960-11e6-9165-00155d390509  {@{Message=Operati...
```

Azt is beállíthatja, hogy eredményeket össze szeretné csak a legutóbbi műveletek használatával a `Newest` paramétert:

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation -Newest 5
ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents
------------   ---------- -----------           ------   -----                                 ---------
SRV1   1          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   2          6/23/2016 4:36:54 PM  Success  5c06402b-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   3          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   4          6/23/2016 4:36:54 PM  Success  5c06402a-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   5          6/23/2016 4:36:51 PM  Success                                        {@{Message=; TimeC...
```

### <a name="getting-details-of-dsc-events"></a>DSC-esemény részleteinek beolvasása közben

A `Trace-xDscOperation` parancsmag események, az esemény típusok gyűjteményét tartalmazó objektumot ad vissza, és az üzenet kimeneti egy adott DSC műveletből létrehozott. Általában amikor talált hiba segítségével műveletek `Get-xDscOperation`, meg kellene nyomon követése a működést, és ismerje meg, amely az események hibáját okozta.

Használja a `SequenceID` paramétert az események beolvasása egy adott számítógép egy adott művelethez.
Például, ha megad egy `SequenceID` , 9, `Trace-xDscOperaion` a DSC-műveletet, amely az utolsó művelet 9 volt a nyomkövetési adatok lekérése:

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -SequenceID 9

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Running consistency engine.
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM The local configuration manager is updating the PSModulePath to WindowsPowerShell\Modules;C:\Prog...
SRV1   OPERATIONAL  6/24/2016 10:51:53 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer.
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Consistency engine was run successfully.
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Job runs under the following LCM setting. ...
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Operation Consistency Check or Pull completed successfully.
```

Adja át a **GUID** egy adott DSC művelethez hozzárendelt (által visszaadott a `Get-xDscOperation` cmldet), az esemény részleteinek beolvasása a DSC-művelethez:

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -JobID 9e0bfb6b-3a3a-11e6-9165-00155d390509

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Starting consistency engine.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Current.mof.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCServiceFeature]
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with resource name [WindowsFeature]DSC...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCServiceFeature]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCServiceFeature] True in 0.3130 sec...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCServiceFeature]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCPullServer]
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with resource name [xDSCWebService]P...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCPullServer]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Ensure
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Port
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Physical Path ...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check State
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Get Full Path for We...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCPullServer] True in 0.0160 seconds.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCPullServer]
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Consistency check completed.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
```

Vegye figyelembe, hogy, mivel `Trace-xDscOperation` események összesíti az elemzési, a Debug és műveleti naplók, akkor arra fogja kérni, hogy ezek a naplók engedélyezése a fent leírtak szerint.

Azt is megteheti, adatokat gyűjthet az események kimenete mentésével `Trace-xDscOperation` egy változóba. A következő parancsokat használhatja egy DSC művelethez tartozó összes esemény megjelenítéséhez.

```powershell
PS C:\DiagnosticsTest> $Trace = Trace-xDscOperation -SequenceID 4

PS C:\DiagnosticsTest> $Trace.Event
```

Ez ugyanazokat az eredményeket, megjeleníti a `Get-WinEvent` parancsmagot, például az alábbi kimenetben:

```output
   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message
-----------                     -- ---------------- -------
6/23/2016 1:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 1:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 2:07:00 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 2:07:01 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 2:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 2:36:56 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 3:06:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 3:06:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 3:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 3:36:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 4:06:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 4:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 4:36:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 4:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 5:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 5:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 5:36:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 5:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 6:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 6:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 6:36:56 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 6:36:57 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 7:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 7:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 7:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
6/23/2016 7:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.
6/23/2016 8:06:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
```

Ideális esetben először használja `Get-xDscOperation` sorolja az elmúlt néhány DSC konfigurációs futtatja a gépeken. Ezt követően tekintse meg minden olyan (a saját SequenceID vagy JobID) egyetlen művelettel rendelkező `Trace-xDscOperation` felderítheti, milyen zavartalanul a háttérben.

### <a name="getting-events-for-a-remote-computer"></a>Események beolvasása egy távoli számítógépen

Használja a `ComputerName` paraméterében a `Trace-xDscOperation` -parancsmaggal beolvasható az esemény részleteinek a távoli számítógépen. Előtt ezt megteheti, hogy hozzon létre egy tűzfalszabályt a távfelügyelet engedélyezéséhez a távoli számítógépen:

```powershell
New-NetFirewallRule -Name "Service RemoteAdmin" -DisplayName "Remote" -Action Allow
```

Most már megadhatja, hogy a számítógép a hívása `Trace-xDscOperation`:

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -ComputerName SRV2 -Credential Get-Credential -SequenceID 5

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 f...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Starting consistency...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Curr...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature,...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCSer...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with re...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCP...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with ...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Consistency check co...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
```

## <a name="my-resources-wont-update-how-to-reset-the-cache"></a>Az erőforrások frissítése nem: a gyorsítótárának visszaállítása

A DSC motor megvalósítva, egy PowerShell-modul hatékonyság célokra erőforrások gyorsítótárazza.
Azonban ez problémákat okozhat szerzői erőforrás és egyidejű tesztelése, mert DSC betölti a gyorsítótárazott verziót, amíg a folyamat újraindítása során. Győződjön meg arról, az újabb verzió betöltése DSC csak úgy, hogy explicit módon kill a DSC motor tartalmazó folyamat.

Hasonlóképpen, ha futtatja `Start-DscConfiguration`, hozzáadásával és a egy egyéni erőforrás módosítása után a módosítás nem futhat, kivéve, ha vagy, amíg a számítógép újraindul. Ennek az az oka a DSC fut a WMI szolgáltató Gazdagépének folyamatánál (WmiPrvSE), és általában nincsenek WmiPrvSE fut egyszerre több példányát. Újraindítás, amikor a gazdagép-folyamat újraindítása, és a gyorsítótár nem lett kitörölve.

Sikeres újrahasznosítása a konfigurációt, és a gyorsítótár ürítése újraindítás nélkül, állítsa le és indítsa újra a gazdagép-folyamat. Ez a példány történik, amelyek segítségével azonosíthatja a folyamat, állítsa le és indítsa újra a elvégezhető. Vagy használhat `DebugMode`, ahogyan az alábbi betölti a PowerShell DSC-erőforrás is.

Azonosíthatja a folyamatok a DSC motor üzemelteti, és állítsa le a példány, listázhatja a WmiPrvSE, amely a DSC motor Folyamatazonosítója. Ezután frissítse a szolgáltatót, állítsa le a WmiPrvSE folyamatot az alábbi parancsok használatával, és futtassa **Start-DscConfiguration** újra.

```powershell
###
### find the process that is hosting the DSC engine
###
$dscProcessID = Get-WmiObject msft_providers |
Where-Object {$_.provider -like 'dsccore'} |
Select-Object -ExpandProperty HostProcessIdentifier

###
### Stop the process
###
Get-Process -Id $dscProcessID | Stop-Process
```

## <a name="using-debugmode"></a>DebugMode használatával

A DSC helyi Configuration Manager (LCM) Konfigurálása használatára konfigurálhatja `DebugMode` mindig törölje a gyorsítótárban, a gazdagép-folyamat újraindításakor. Ha a beállítása **igaz**, azt eredményezi, hogy a motor, mindig töltse be újra a PowerShell DSC-erőforrás. Ha elkészült a-erőforrás írása állíthatja be, vissza **false (hamis)** és a motor visszaállítja a modulok gyorsítótárazásának működését.

Az alábbiakban a megjeleníthető bemutatója hogyan `DebugMode` automatikusan frissítheti a gyorsítótárban. Először is lássuk az alapértelmezett konfiguráció:

```powershell
PS C:\> Get-DscLocalConfigurationManager
```

```output
AllowModuleOverwrite           : False
CertificateID                  :
ConfigurationID                :
ConfigurationMode              : ApplyAndMonitor
ConfigurationModeFrequencyMins : 30
Credential                     :
DebugMode                      : False
DownloadManagerCustomData      :
DownloadManagerName            :
LocalConfigurationManagerState : Ready
RebootNodeIfNeeded             : False
RefreshFrequencyMins           : 15
RefreshMode                    : PUSH
PSComputerName                 :
```

Láthatja, hogy `DebugMode` értékre van állítva **hamis**.

Beállítása a `DebugMode` bemutató a következő PowerShell-erőforrásból:

```powershell
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    "1" | Out-File -PSPath "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return $false
}
```

Most hozhat létre egy konfigurációt a fenti erőforrás nevű `TestProviderDebugMode`:

```powershell
Configuration ConfigTestDebugMode
{
    Import-DscResource -Name TestProviderDebugMode
    Node localhost
    {
        TestProviderDebugMode test
        {
            onlyProperty = "blah"
        }
    }
}
ConfigTestDebugMode
```

Látni fogja, hogy a fájl tartalmát: `$env:SystemDrive\OutputFromTestProviderDebugMode.txt` van **1**.

Most frissítse a szolgáltatót kódot az alábbi parancsfájl használatával:

```powershell
$newResourceOutput = Get-Random -Minimum 5 -Maximum 30
$content = @"
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    "$newResourceOutput" | Out-File -PSPath C:\OutputFromTestProviderDebugMode.txt
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return `$false
}
"@ | Out-File -FilePath "C:\Program Files\WindowsPowerShell\Modules\MyPowerShellModules\DSCResources\TestProviderDebugMode\TestProviderDebugMode.psm1
```

Ez a szkript létrehoz egy véletlenszerű számot, és ennek megfelelően frissíti a szolgáltató kódot. A `DebugMode` hamis, a fájl tartalmát "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" soha nem módosulnak.

Most, `DebugMode` való **igaz** konfigurációs parancsfájlban:

```powershell
LocalConfigurationManager
{
    DebugMode = $true
}
```

Ha újra futtatja a fenti szkript, látni fogja, hogy a fájl tartalma eltér minden alkalommal. (Futtathatja `Get-DscConfiguration` , hogy). Az alábbi, két további futtatásoknál (a találatok eltérő lehet a parancsfájl futtatásakor) eredménye:

```powershell
PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)

onlyProperty                            PSComputerName
------------                            --------------
20                                      localhost

PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)

onlyProperty                            PSComputerName
------------                            --------------
14                                      localhost
```

## <a name="see-also"></a>Lásd még:

### <a name="reference"></a>Referencia

- [DSC-Log erőforrás](logResource.md)

### <a name="concepts"></a>Fogalmak

- [Egyéni Windows PowerShell Desired State Configuration erőforrások létrehozása](authoringResource.md)

### <a name="other-resources"></a>Egyéb források

- [Windows PowerShell Desired State Configuration parancsmagok](https://technet.microsoft.com/library/dn521624(v=wps.630).aspx)