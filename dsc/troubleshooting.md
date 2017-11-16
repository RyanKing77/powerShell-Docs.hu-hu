---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Hibaelhárítási DSC"
ms.openlocfilehash: 9b1266b9c8923474005760ef78b05d570efdde37
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="troubleshooting-dsc"></a>Hibaelhárítási DSC

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

Ez a témakör ismerteti azokat a módszereket DSC elhárításához, amikor probléma merül fel.

## <a name="winrm-dependency"></a>A WinRM-függőség

Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) attól függ, hogy a Rendszerfelügyeleti webszolgáltatások. Rendszerfelügyeleti webszolgáltatások a Windows Server 2008 R2 és Windows 7 alapértelmezés szerint nincs engedélyezve. Futtatás ```Set-WSManQuickConfig```, egy Windows PowerShell az emelt szintű ahhoz, hogy a WinRM-munkamenetben.

## <a name="using-get-dscconfigurationstatus"></a>Get-DscConfigurationStatus használatával

A [Get-DscConfigurationStatus](https://technet.microsoft.com/en-us/library/mt517868.aspx) parancsmag konfiguráció állapota információ lekérése a cél-csomópont. Gazdag objektumot ad vissza, amely tartalmazza-e a konfiguráció futtatása sikeres volt-e magas szintű információkat. Akkor is elmerülne a rendszer a objektumba felderítéséhez futtassa, mint a konfigurációs adatait:

* Az erőforrásokat, melyeknél nem sikerült
* Minden erőforrás újraindítást kérő
* Futtassa a konfigurációs időpontjában meta-konfigurációs beállítások
* stb.

A következő paraméterhalmaz adja vissza az utolsó futtatása konfigurációra vonatkozó információk:

```powershell
Get-DscConfigurationStatus  [-CimSession <CimSession[]>] 
                            [-ThrottleLimit <int>] 
                            [-AsJob] 
                            [<CommonParameters>]
```
A következő paraméterhalmaz adja vissza az összes korábbi konfigurációs futás esetén:

```powershell
Get-DscConfigurationStatus  -All 
                            [-CimSession <CimSession[]>] 
                            [-ThrottleLimit <int>] 
                            [-AsJob] 
                            [<CommonParameters>]
```

## <a name="example"></a>Példa

```powershell
PS C:\> $Status = Get-DscConfigurationStatus 

PS C:\> $Status

Status      StartDate               Type            Mode    RebootRequested     NumberOfResources
------      ---------               ----            ----    ---------------     -----------------
Failure     11/24/2015  3:44:56     Consistency     Push    True                36

PS C:\> $Status.ResourcesNotInDesiredState

ConfigurationName       :   MyService
DependsOn               :   
ModuleName              :   PSDesiredStateConfiguration
ModuleVersion           :   1.1
PsDscRunAsCredential    :   
ResourceID              :   [File]ServiceDll
SourceInfo              :   c:\git\CustomerService\Configs\MyCustomService.ps1::5::34::File
DurationInSeconds       :   0.19
Error                   :   SourcePath must be accessible for current configuration. The related file/directory is:
                            \\Server93\Shared\contosoApp.dll. The related ResourceID is [File]ServiceDll
FinalState              :   
InDesiredState          :   False
InitialState            :   
InstanceName            :   ServiceDll
RebootRequested         :   False
ReosurceName            :   File
StartDate               :   11/24/2015  3:44:56
PSComputerName          :
```

## <a name="my-script-wont-run-using-dsc-logs-to-diagnose-script-errors"></a>A parancsprogram nem futott: parancsfájl hibáinak diagnosztizálásához naplózza a DSC használata

Minden Windows szoftverek, például DSC rögzíti hibák és események [naplók](https://msdn.microsoft.com/library/windows/desktop/aa363632.aspx) , hogy megtekinthetők a [Eseménynapló](http://windows.microsoft.com/windows/what-information-event-logs-event-viewer). Ezek a naplók vizsgálata azt segítenek megérteni miért egy adott művelethez nem sikerült, és a jövőben megakadályozása hiba. Konfigurációs parancsfájlok írása megkapni, hogy követési hibák könnyíti meg Szerző, a konfiguráció a DSC elemzési eseménynaplóban az előrehaladását úgy követheti nyomon a DSC-napló erőforrás segítségével.

## <a name="where-are-dsc-event-logs"></a>Hol találhatók a DSC-eseménynaplók?

Az Eseménynapló DSC események szerepelnek: **alkalmazások és szolgáltatások Logs/Microsoft/Windows/kívánt állapot konfigurációs**

A megfelelő PowerShell-parancsmag [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx), is futtatható tekintse át az eseménynaplókat:

```
PS C:\> Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message                                                                                                  
-----------                     -- ---------------- -------                                                                                                  
11/17/2014 10:27:23 PM        4102 Information      Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} : 
```

A fentiek van-e DSC elsődleges napló neve **Microsoft -> Windows -> DSC** (a Windows egyéb napló nevek nem itt látható kivonatosan mutatja). Az elsődleges neve van hozzáfűzve csatornát létrehozni a teljes nevét. A DSC-motor ír főként a naplók három típusa: [működési, elemzési és hibakeresési naplók](https://technet.microsoft.com/library/cc722404.aspx). Mivel az elemzési és hibakeresési naplók alapértelmezés szerint ki van kapcsolva, engedélyezze a őket az eseménynaplóban. Ehhez nyissa meg az eseménynaplót az eseménynaplóban megjelenítése írja be a Windows PowerShell; vagy kattintson a **Start** gombra, majd **Vezérlőpult**, kattintson a **felügyeleti eszközök**, és kattintson a **Eseménynapló**. Az a **nézet** az eseménynaplóban, menüjében kattintson **elemzési és hibakeresési naplók megjelenítése**. A naplófájl neve a analytic channel bejegyzést **elemzési Microsoft-Windows-Dsc**, és a hibakeresési csatorna **Microsoft-Windows-Dsc/Debug**. Is használhatja a [wevtutil](https://technet.microsoft.com/library/cc732848.aspx) segédprogram a naplók engedélyezéséhez az alábbi példában látható módon.

```powershell
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
```

## <a name="what-do-dsc-logs-contain"></a>A DSC-naplók tartalmazzák

A DSC-naplók keresztül a három naplózási csatornák, az üzenet fontosságát alapján vannak osztva. A DSC műveleti napló az összes hibaüzenet tartalmazza, és a probléma azonosításához használható. Az elemzési naplóját nagyobb mennyiségű esemény rendelkezik, és azonosíthatja, ahol egy vagy több hiba történt. Ez a csatorna a részletes üzenetek is tartalmaz, (ha van ilyen). A hibakeresési napló tartalmazza a naplófájlokat, amelyek azt segítenek megérteni, hogyan a hibák fordultak elő. A DSC-eseményüzenetek felépítése úgy, hogy minden üzenet egy DSC művelet egyedileg jelölő feladatazonosítóval kezdődik. Az alábbi példa megkísérli az üzenet kérése az első esemény naplózása működési DSC naplóba.

```powershell
PS C:\> $AllDscOpEvents = Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
PS C:\> $FirstOperationalEvent = $AllDscOpEvents[0]
PS C:\> $FirstOperationalEvent.Message
Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} : 
Consistency engine was run successfully. 
```

Egy adott struktúra, amely lehetővé teszi a felhasználó az összegyűjtött eseményeket egy DSC feladatból DSC események naplózása. A struktúra a következőképpen történik:

**Feladat azonosítója:<Guid>**
**<Event Message>**

## <a name="gathering-events-from-a-single-dsc-operation"></a>Egy DSC művelettel eseményeinek gyűjtése

A DSC-eseménynaplók különböző DSC műveletei által előállított eseményeket tartalmaz. Azonban általában lesz a részletességgel aggódik egy adott művelet. Összes DSC napló csoportosíthatók az egyedi minden DSC művelethez feladat-azonosító tulajdonsággal. Minden DSC események első tulajdonság értéke jelenik meg a Feladatazonosítót. Az alábbi lépések ismertetik időtartamok csoportosított tömb struktúrában összes esemény megjelenítése.

```powershell
<##########################################################################
 Step 1 : Enable analytic and debug DSC channels (Operational channel is enabled by default)
###########################################################################>
 
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
wevtutil.exe set-log “Microsoft-Windows-Dsc/Debug” /q:True /e:true
 
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

Itt, a változó `$SeparateDscOperations` tartalmazza a naplók a feladat-azonosítók szerint csoportosítva. A változó minden tömbelem másik DSC műveletet, amely hozzáférést biztosít a naplókat további információt által naplózott eseményeket csoportja.

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

Az adatok a változóban kibonthatja `$SeparateDscOperations` használatával [Where-Object](https://technet.microsoft.com/library/ee177028.aspx). Az alábbiakban öt forgatókönyvek, amelyekben érdemes DSC hibaelhárítási adatokat nyerhet ki:

### <a name="1-operations-failures"></a>1: műveletek hibák

Minden eseményhez [súlyossági szintek](https://msdn.microsoft.com/library/dd996917(v=vs.85)). Ezek az információk segítségével azonosíthatja a hibaesemények:

```
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.LevelDisplayName -contains "Error"}
Count Name                      Group                                                                     
----- ----                      -----                                                                     
   38 {5BCA8BE7-5BB6-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
```

### <a name="2-details-of-operations-run-in-the-last-half-hour"></a>2: műveletek részleteit futtassa az utolsó fél óra

`TimeCreated`, minden Windows-esemény tulajdonsága jelzi, amikor az esemény létrejött. Ezt a tulajdonságot, egy adott dátum/idő objektummal összehasonlításával összes esemény szűrésére használható:

```powershell
PS C:\> $DateLatest = (Get-Date).AddMinutes(-30)
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.TimeCreated -gt $DateLatest}
Count Name                      Group                                                                     
----- ----                      -----                                                                     
    1 {6CEC5B09-5BB0-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord}   
```

### <a name="3-messages-from-the-latest-operation"></a>3: a legutóbbi művelet üzenetek

A legutóbbi művelet tárolja az első index a tömb csoport `$SeparateDscOperations`. A csoport üzenetek 0. index lekérdezése adja vissza a legutóbbi művelet üzenetek:

```powershelll
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

### <a name="4-error-messages-logged-for-recent-failed-operations"></a>4: legutóbbi meghiúsult műveletek a naplóba hibaüzenetek

`$SeparateDscOperations[0].Group`a legutóbbi művelet eseményeket tartalmaz. Futtassa a `Where-Object` parancsmag használatával az események szűréséhez szintű megjelenítendő neve alapján. Eredmények tárolódnak a `$myFailedEvent` változó, amely lehet további minél esemény üzenet:

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

`$SeparateDscOperations`egy tömb csoportok, amelyek mindegyikének a neve megegyezik a feladat egyedi azonosítója. Futtassa a `Where-Object` parancsmag is kibonthat egy ezeket a csoportokat az eseményeket, amelyek egy adott feladat azonosítója:

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

## <a name="using-xdscdiagnostics-to-analyze-dsc-logs"></a>Naplók segítségével xDscDiagnostics DSC elemzése

**xDscDiagnostics** egy PowerShell-modul, amely számos funkcióval segíti a számítógépre a DSC-hibák elemzése áll. Ezek a funkciók segítségével azonosítja az összes helyi események az elmúlt DSC műveletek vagy DSC események távoli számítógépeken (az érvényes hitelesítő adatok). Itt a DSC-művelet kifejezés egy egyetlen egyedi DSC végrehajtási a kezdetektől végéhez meghatározásához. Például `Test-DscConfiguration` egy külön DSC művelet lenne. Hasonlóképpen, minden más parancsmag DSC (például `Get-DscConfiguration`, `Start-DscConfiguration`stb) minden azonosítható DSC külön műveletként. A függvények van arra a [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics). Súgó áll rendelkezésre futtatásával `Get-Help <cmdlet name>`.

### <a name="getting-details-of-dsc-operations"></a>A DSC-műveletek-információk lekérdezése 

A `Get-xDscOperation` funkció lehetővé teszi, hogy az eredmények, amelyek egy vagy több számítógépen futnak a DSC-műveletek található, és visszahelyezi a minden egyes DSC művelet által létrehozott olyan objektum, amely az események gyűjteményét tartalmazza. Például a következő kimenet három parancsot futtatná. Az átadott, és két, a másik nem. Ezekkel az eredményekkel foglalja össze a kimenetét `Get-xDscOperation`.

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation

ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents            
------------   ---------- -----------           ------   -----                                 ---------            
SRV1   1          6/23/2016 9:37:52 AM  Failure  9701aadf-395e-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   2          6/23/2016 9:36:54 AM  Failure  7e8e2d6e-395c-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   3          6/23/2016 9:36:54 AM  Success  af72c6aa-3960-11e6-9165-00155d390509  {@{Message=Operati...

```

Megadhatja, amelyet csak a legutóbbi művelet használatával a `Newest` paraméter:

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

### <a name="getting-details-of-dsc-events"></a>A DSC-események adatainak lekérdezése

A `Trace-xDscOperation` parancsmag visszaad egy objektumot tartalmazó események, az esemény típusok gyűjteményét, és az üzenet kimeneti jön létre egy adott DSC-műveletből. Általában, amikor talált hiba használó műveletek `Get-xDscOperation`, szeretné nyomon követni Ez a művelet, ha szeretné tudni, amely az események hibáját okozta.

Használja a `SequenceID` paraméter használatával beolvassa az eseményeket egy adott művelet egy adott számítógépen. Például, ha megad egy `SequenceID` a 9-es, `Trace-xDscOperaion` a nyomkövetési lekérése a DSC művelet, amely a legutóbbi művelet 9 volt:

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

Adja át a **GUID** adott DSC művelethez hozzárendelt (amelyet a `Get-xDscOperation` cmldet) az esemény részleteinek lekérése DSC művelet:

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

Vegye figyelembe a következőket, azóta `Trace-xDscOperation` események összesíti az elemző, a Debug és műveleti naplói, akkor arra fogja kérni, hogy ezek a naplók engedélyezése a fent leírt módon.

Alternatív megoldásként adatokat gyűjthet a események kimenete mentésével `Trace-xDscOperation` egy változóba. A következő parancsok segítségével egy DSC művelethez tartozó összes esemény megjelenítése.

```powershell
PS C:\DiagnosticsTest> $Trace = Trace-xDscOperation -SequenceID 4

PS C:\DiagnosticsTest> $Trace.Event
```

Megjelenik az azonos a `Get-WinEvent` parancsmag, például az alábbi kimenetben:

```powershell
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

Ideális esetben először használja `Get-xDscOperation` listázásához, az elmúlt néhány DSC konfigurációs a gépeken futtatja. Ezt követően ellenőrizheti bármely (a SequenceID vagy JobID használatával) egyetlen művelettel rendelkező `Trace-xDscOperation` felderítésére, mi ugyanúgy a háttérben.

### <a name="getting-events-for-a-remote-computer"></a>Egy távoli számítógépen eseményeinek beolvasása

Használja a `ComputerName` paramétere a `Trace-xDscOperation` parancsmagot, hogy megkapja az esemény részleteit egy távoli számítógépen. Ezt megteheti, hogy kell hozzon létre egy tűzfalszabályt a távfelügyelet engedélyezéséhez a távoli számítógépen:

```powershell
New-NetFirewallRule -Name "Service RemoteAdmin" -DisplayName "Remote" -Action Allow
```
A hívás adhat meg, hogy a számítógép most `Trace-xDscOperation`:

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

## <a name="my-resources-wont-update-how-to-reset-the-cache"></a>Az erőforrások nem frissíti: a gyorsítótár visszaállítása

A DSC-motor valósul meg egy PowerShell-modul hatékonyságát célokra erőforrások gyorsítótárazza. Azonban ez problémát okozhat erőforrás szerzői és egyidejűleg tesztelése, mert DSC betölti a gyorsítótárazott verzió, a folyamat újraindításáig. Csak az újabb verzió betöltése DSC végrehajtásához, explicit módon leállítani a folyamatot a DSC-motor.

Hasonlóképpen, ha futtatja `Start-DscConfiguration`, után, és egyéni erőforrás módosításának a módosítás lehet, hogy nem hajthatók végre, vagy, amíg a számítógép újraindítása után. Ennek az az oka DSC futtatja a WMI-szolgáltató gazdafolyamat (WmiPrvSE), és általában több példánya van WmiPrvSE fut egyszerre. Újraindításakor, a gazdagép folyamatot, és a gyorsítótár nincs bejelölve.

Sikeres hasznosítsa újra a konfigurációt, és anélkül a gyorsítótárat kiürítheti, állítsa le és indítsa újra a gazdagép-folyamat. Ezt megteheti / példány alapon, amelynek során a folyamat azonosítására, állítsa le és indítsa újra. Másik lehetőségként használhatja `DebugMode`, ahogyan az alábbi töltse be újra a PowerShell DSC-erőforrás.

Azonosíthatja, melyik folyamat üzemelteti a DSC-motor, és állítsa le a / példány alapon, listázhatja a WmiPrvSE, amely üzemelteti a DSC-motor Folyamatazonosítója. Ezt követően frissítse a szolgáltatót, állítsa le a WmiPrvSE folyamatot az alábbi parancsok használatával, és futtassa **Start-DscConfiguration** újra.

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

A DSC helyi Configuration Manager (LCM) használatára konfigurálhatja `DebugMode` mindig törölje a gyorsítótár, a gazdagép-folyamat újraindításakor. Ha beállítása **igaz**, azt eredményezi, hogy a motor mindig töltse be újra a PowerShell DSC-erőforrás. Miután a ír, az erőforrás, állíthatja vissza a **hamis** és a motor visszaállítja a modulok gyorsítótárazásának működése.

Az alábbiakban látható egy bemutató megjelenítendő hogyan `DebugMode` automatikusan is frissítheti a gyorsítótárban. Először az alapértelmezett konfiguráció vizsgáljuk meg:

```
PS C:\> Get-DscLocalConfigurationManager
 
 
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

Láthatja, hogy `DebugMode` értéke **hamis**.

Beállítása a `DebugMode` bemutató, használja a következő PowerShell-erőforrás:

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

Most, szerzői egy konfigurációval, a fenti erőforrás neve `TestProviderDebugMode`:

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

Látni fogja, hogy a fájl tartalmát: "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" van **1**.

Most frissítse a szolgáltatót kódot használja a következő parancsfájlt:

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

Ezt a parancsfájlt hoz létre egy véletlenszerű számot, és ennek megfelelően frissíti a szolgáltató kódot. A `DebugMode` értéke HAMIS, a fájl tartalmát "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**" soha nem módosulnak.

Most, `DebugMode` való **igaz** konfigurációs parancsfájlban:

```powershell
LocalConfigurationManager
{
    DebugMode = $true
} 
```

Ha a fenti szkript újra futtatja, látni fogja, hogy a fájl tartalma különböző minden alkalommal. (Futtatása `Get-DscConfiguration` , hogy). Az alábbiakban oka két további fut (a eredmény lehetnek a parancsfájl futtatásakor):

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
* [A DSC-napló erőforrás](logResource.md)

### <a name="concepts"></a>Fogalmak
* [Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása](authoringResource.md)

### <a name="other-resources"></a>Egyéb források
* [A Windows PowerShell célállapot-konfiguráló parancsmagok](https://technet.microsoft.com/en-us/library/dn521624(v=wps.630).aspx)

