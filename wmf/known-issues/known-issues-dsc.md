---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: Desired State Configuration (DSC) ismert problémák és korlátozások
ms.openlocfilehash: 6faf24795d14a93f265943029d9f6f1388f32263
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856195"
---
# <a name="desired-state-configuration-dsc-known-issues-and-limitations"></a>Desired State Configuration (DSC) ismert problémák és korlátozások

## <a name="breaking-change-certificates-used-to-encryptdecrypt-passwords-in-dsc-configurations-may-not-work-after-installing-wmf-50-rtm"></a>Kompatibilitástörő változás: A DSC-konfigurációk jelszavak titkosítási/visszafejtési tanúsítványokat nem működnek a WMF 5.0 RTM-re telepítése után

A WMF 4.0-s és WMF 5.0-s előzetes kiadások DSC nem teszik lehetővé a jelszavak hosszát, a konfiguráció a több mint 121 karakter. DSC rövid jelszavak használatát, akkor is, ha a hosszú és erős jelszót volt szükség volt kényszerítése. Ez használhatatlanná tévő változás lehetővé teszi, hogy a jelszavakat a DSC-konfiguráció tetszőleges hosszúságú lehet.

**Megoldás:** Hozza létre újra a tanúsítványt, az adattitkosítás vagy a fő titkosítási kulcs használati és dokumentum titkosítási kibővített kulcshasználat (1.3.6.1.4.1.311.80.1). További információkért lásd: [Protect-CmsMessage](/powershell/module/Microsoft.PowerShell.Security/Protect-CmsMessage).

## <a name="dsc-cmdlets-may-fail-after-installing-wmf-50-rtm"></a>A WMF 5.0 RTM-re telepítése után sikertelen lehet a DSC-parancsmagok

`Start-DscConfiguration` és egyéb DSC-parancsmagok meghiúsulhat a következő hiba miatt a WMF 5.0 RTM-re telepítése után:

```Output
LCM failed to retrieve the property PendingJobStep from the object of class dscInternalCache .
+ CategoryInfo : ObjectNotFound: (root/Microsoft/...gurationManager:String) [], CimException
+ FullyQualifiedErrorId : MI RESULT 6
+ PSComputerName : localhost
```

**Megoldás:** DSCEngineCache.mof törölje a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):

```powershell
Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof
```

## <a name="dsc-cmdlets-may-not-work-if-wmf-50-rtm-is-installed-on-top-of-wmf-50-production-preview"></a>DSC-parancsmagok előfordulhat, hogy nem működik, ha a WMF 5.0 RTM-re épülő WMF 5.0 éles előzetes verzió van telepítve

**Megoldás:** Futtassa a következő parancsot egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):

```powershell
mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof
```

## <a name="lcm-can-go-into-an-unstable-state-while-using-get-dscconfiguration-in-debugmode"></a>Az LCM lépjen nem stabil állapotba kerülnek DebugMode Get-DscConfiguration használatával

Ha LCM DebugMode, nyomja le a CTRL + C billentyűkombinációval feldolgozásának leállítása `Get-DscConfiguration` okozhat a go LCM nem stabil állapotba kerülnek az ilyen a DSC-parancsmagok többsége nem fog működni.

**Megoldás:** Hibakeresés közben nem CTRL + C billentyűkombináció `Get-DscConfiguration` parancsmagot.

## <a name="stop-dscconfiguration-may-not-respond-in-debugmode"></a>STOP-DscConfiguration nem válaszol a DebugMode

Az LCM DebugMode, ha `Stop-DscConfiguration` által indított művelet megszakítására tett kísérlet során nem válaszol `Get-DscConfiguration`

**Megoldás:** A hibakeresési lépések: a művelet befejezéséhez `Get-DscConfiguration` leírt módon [hibakeresés DSC-erőforrások](/powershell/dsc/troubleshooting/debugResource).

## <a name="no-verbose-error-messages-are-shown-in-debugmode"></a>Részletes hibaüzenetek nem jelennek meg DebugMode

Ha LCM **DebugMode**, nem a részletes hibaüzenet jelenik meg a DSC-erőforrásokat.

**Megoldás:** Tiltsa le **DebugMode** erőforrásból részletes üzenetek megtekintéséhez

## <a name="invoke-dscresource-operations-cannot-be-retrieved-by-get-dscconfigurationstatus-cmdlet"></a>Invoke-DscResource műveletek nem lehet beolvasni a Get-DscConfigurationStatus parancsmag

Forgatókönyv használata útán `Invoke-DscResource` parancsmagot, hogy közvetlenül a minden erőforrás metódusok, a rekordokat az ilyen művelet meghívása nem sikerült beolvasni a keresztül `Get-DscConfigurationStatus`.

**Megoldás:** Nincs.

## <a name="get-dscconfigurationstatus-returns-pull-cycle-operations-as-type-consistency"></a>Get-DscConfigurationStatus értéket ad vissza lekéréses ciklus műveletek típusként **konzisztencia**

Ha egy csomópont értéke LEKÉRÉSES frissítési mód, egyes lekéréses műveletek elvégzése `Get-DscConfigurationStatus` parancsmag-jelentések, a művelet típusa **konzisztencia** helyett *kezdeti*

**Megoldás:** Nincs.

## <a name="invoke-dscresource-cmdlet-does-not-return-message-in-the-order-they-were-produced"></a>Invoke-DscResource parancsmag nem ad vissza üzenet állították sorrendben

A `Invoke-DscResource` a parancsmag nem ad részletes, figyelmeztetés, és hibaüzenetek LCM vagy a DSC-erőforrás állították a sorrendben.

**Megoldás:** Nincs.

## <a name="dsc-resources-cannot-be-debugged-easily-when-used-with-invoke-dscresource"></a>DSC-erőforrások hibakeresése nem végezhető el egyszerűen Invoke-DscResource együtt használva

Az LCM hibakeresési módban való futtatáskor `Invoke-DscResource` parancsmag nem ad hibakeresési csatlakozni futási térben kapcsolatos információkat. További információkért lásd: [hibakeresés DSC-erőforrások](/powershell/dsc/troubleshooting/debugResource).

**Megoldás:** Fedezze fel, és csatolja a futási térben parancsmagokkal `Get-PSHostProcessInfo`, `Enter-PSHostProcess` , `Get-Runspace` és `Debug-Runspace` hibakeresése a DSC-erőforrás.

```powershell
# Find all the processes hosting PowerShell
Get-PSHostProcessInfo

ProcessName    ProcessId AppDomainName
-----------    --------- -------------
powershell          3932 DefaultAppDomain
powershell_ise      2304 DefaultAppDomain
WmiPrvSE            3396 DscPsPluginWkr_AppDomain

# Enter the process that is hosting DSC engine (WMI process with DscPsPluginWkr_Appdomain)
Enter-PSHostProcess -Id 3396 -AppDomainName DscPsPluginWkr_AppDomain

# Find all the available rusnspaces in that process
Get-Runspace

Id Name       ComputerName Type  State  Availability
-- ----       ------------ ----  -----  ------------
 2 Runspace2  localhost    Local Opened InBreakpoint
 5 RemoteHost localhost    Local Opened Busy

# Debug the runspace that is in **InBreakpoint** availability state
Debug-Runspace -Id 2
```

## <a name="various-partial-configuration-documents-for-same-node-cannot-have-identical-resource-names"></a>Ugyanazon a csomóponton különböző részleges konfigurációs dokumentumok azonos erőforrás neve nem lehet.

Azonos nevek erőforrások OK, amely egyetlen csomópont időszakaik legyenek több részleges konfigurációk, futásidejű hiba.

**Megoldás:** Akkor is ugyanazokat az erőforrásokat a különböző neveket használ a különböző részleges konfigurációk.

## <a name="start-dscconfiguration-useexisting-does-not-work-with--credential"></a>Start-DscConfiguration – UseExisting nem működik – a hitelesítő adatok

Használata esetén `Start-DscConfiguration` a **UseExisting** paramétert, a **Credential** paraméter figyelmen kívül hagyja. DSC használ alapértelmezett folyamatidentitás folytatja a műveletet. Ez hibát okoz, ha más hitelesítő adatokat távoli csomóponton folytatja van szükség.

**Megoldás:** CIM-munkamenet távoli DSC műveletek:

```powershell
$session = New-CimSession -ComputerName $node -Credential $credential
Start-DscConfiguration -UseExisting -CimSession $session
```

## <a name="ipv6-addresses-as-node-names-in-dsc-configurations"></a>A DSC-konfigurációkat csomópont nevét, az IPv6-címek

DSC-konfigurációs szkripteket a csomópont nevét, az IPv6-címek nem támogatottak ebben a kiadásban.

**Megoldás:** Nincs.

## <a name="debugging-of-class-based-dsc-resources"></a>A hibakeresés `Class-Based` DSC-erőforrások

Osztályalapú DSC-erőforrások hibakeresése ebben a kiadásban nem támogatott.

**Megoldás:** Nincs.

## <a name="variables-and-functions-defined-in-script-scope-in-dsc-class-based-resource-are-not-preserved-across-multiple-calls-to-a-dsc-resource"></a>Változók és a DSC osztály-alapú erőforrás $script hatókörében meghatározott függvényeket nem maradnak meg több alkalommal hívnia egy DSC-erőforrás között

Több egymást követő hívások `Start-DSCConfiguration` sikertelen lesz, ha definiálva függvények vagy a konfiguráció használ változók rendelkező osztályalapú erőforrásoknál `$script` hatókör.

**Megoldás:** Adjon meg a változók és a functions a DSC-erőforrás osztály. Nem `$script` változók a functions hatókörét.

## <a name="dsc-resource-debugging-when-a-resource-is-using-psdscrunascredential"></a>Ha egy erőforrás PSDscRunAsCredential hibakeresés DSC erőforrás

DSC-erőforrás hibakeresés erőforrás használatakor a **PSDscRunAsCredential** tulajdonság a konfiguráció nem támogatott ebben a kiadásban.

**Megoldás:** Nincs.

## <a name="psdscrunascredential-is-not-supported-for-dsc-composite-resources"></a>PsDscRunAsCredential összetett DSC-erőforrások esetén nem támogatott

**Megoldás:** Hitelesítő adat tulajdonság akkor használható, ha elérhető. Példa ServiceSet és WindowsFeatureSet

## <a name="get-dscresource--syntax-does-not-reflect-psdscrunascredential-correctly"></a>Get-DscResource-szintaxist nem tükrözi a PsDscRunAsCredential megfelelően

A **szintaxis** paraméter nem tükrözi a **PsDscRunAsCredential** megfelelően Ha erőforrás jelöli meg, kötelező vagy nem támogatja ezt.

**Megoldás:** Nincs. Azonban ISE-ben konfigurációs szerzői tükrözi metaadat kapcsolatos **PsDscRunAsCredential** tulajdonságot, amikor az IntelliSense segítségével.

## <a name="windowsoptionalfeature-is-not-available-in-windows-7"></a>WindowsOptionalFeature nem érhető el a Windows 7

A **WindowsOptionalFeature** DSC-erőforrás nem érhető el a Windows 7. Ezt az erőforrást igényel a DISM modul, és a DISM-parancsmagok érhetők el a Windows 8 és újabb verzióiban a Windows operációs rendszer indítása.

## <a name="for-class-based-dsc-resources-import-dscresource--moduleversion-may-not-work-as-expected"></a>Osztályalapú DSC-erőforrások az Import-DscResource - ModuleVersion esetleg nem működnek megfelelően

Ha a fordítás csomópont osztályalapú DSC erőforrás modulok, több verzió `Import-DscResource -ModuleVersion` ne foglalkozzon megadott verzióját és sémafordítási hiba történt a következő eredményez.

```Output
ImportClassResourcesFromModule : Exception calling "ImportClassResourcesFromModule" with "3" argument(s):
 "Keyword 'MyTestResource' already defined in the configuration."
At C:\Windows\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:2035 char:35
+ ... rcesFound = ImportClassResourcesFromModule -Module $mod -Resources $r ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [ImportClassResourcesFromModule], MethodInvocationException
    + FullyQualifiedErrorId : PSInvalidOperationException,ImportClassResourcesFromModule
```

**Megoldás:** Importálja a szükséges verzióra definiálásával a **ModuleSpecification** az objektum a **ModuleName** paraméterrel **RequiredVersion** kulcs van megadva a következőképpen:

```powershell
Import-DscResource -ModuleName @{ModuleName='MyModuleName';RequiredVersion='1.2'}
```

## <a name="some-dsc-resources-like-registry-resource-may-start-to-take-a-long-time-to-process-the-request"></a>Előfordulhat, hogy egyes DSC-erőforrások, például beállításjegyzék erőforrás időbe telik a kérelem feldolgozása megkezdődött.

**1. megoldás:** Hozzon létre egy ütemezett feladat, rendszeres időközönként megtisztítja a következő mappát.

```powershell
$env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis
```

**2. megoldás:** A DSC-konfiguráció karbantartása módosítsa a *CommandAnalysis* végén található a konfigurációs mappát.

```powershell
Configuration $configName
{

   # User Data
    Registry SetRegisteredOwner
    {
        Ensure = 'Present'
        Force = $True
        Key = $Node.RegisteredKey
        ValueName = $Node.RegisteredOwnerValue
        ValueType = 'String'
        ValueData = $Node.RegisteredOwnerData
    }
    #
    # Script to delete the config
    #
    script DeleteCommandAnalysisCache
    {
        DependsOn = "[Registry]SetRegisteredOwner"
        getscript = "@{}"
        testscript = 'Remove-Item -Path $env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis -Force -Recurse -ErrorAction SilentlyContinue -ErrorVariable ev | out-null;$true'
        setscript = '$true'
    }
}
```
