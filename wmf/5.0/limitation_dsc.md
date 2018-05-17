---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 76aa4a372602d78e013b2138eb6409304a4dfb76
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="desired-state-configuration-dsc-known-issues-and-limitations"></a>Célállapot-konfiguráció (DSC) ismert problémák és korlátozások

<a name="breaking-change-certificates-used-to-encryptdecrypt-passwords-in-dsc-configurations-may-not-work-after-installing-wmf-50-rtm"></a>Megtörje módosítása: A DSC-konfigurációk jelszavak titkosításához/visszafejtéséhez használt tanúsítványok nem feltétlenül WMF 5.0 RTM telepítése után
--------------------------------------------------------------------------------------------------------------------------------

A WMF 4.0-s és a WMF 5.0 Preview kiadásokban DSC nem teszik lehetővé a jelszavak a konfigurációban kell lennie a length több mint 121 karaktereket. A DSC rövid jelszavak használatát, akkor is, ha a hosszú és erős jelszót volt szükség volt kényszerítése. A legfrissebb módosítás lehetővé teszi, hogy a DSC-konfiguráció tetszőleges hosszúságú jelszót.

**Megoldás:** hozza létre újból a tanúsítványt, amelynek adattitkosítás vagy kulcs rejtjelezése kulcs használatát, és a dokumentum titkosítási kibővített kulcshasználat (1.3.6.1.4.1.311.80.1). A TechNet cikknek <https://technet.microsoft.com/library/dn807171.aspx> további részleteket tartalmaz.


<a name="dsc-cmdlets-may-fail-after-installing-wmf-50-rtm"></a>A DSC-parancsmagok sikertelenek lehetnek a WMF 5.0 RTM telepítése után
------------------------------------------------------------------------------------
Start-DscConfiguration és egyéb DSC-parancsmagokkal meghiúsulhat, miután telepítette a WMF 5.0 RTM-re a következő hiba miatt:
```powershell
    LCM failed to retrieve the property PendingJobStep from the object of class dscInternalCache .
    + CategoryInfo : ObjectNotFound: (root/Microsoft/...gurationManager:String) [], CimException
    + FullyQualifiedErrorId : MI RESULT 6
    + PSComputerName : localhost
```

**Megoldás:** DSCEngineCache.mof törlése a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):

```powershell
Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof
```


<a name="dsc-cmdlets-may-not-work-if-wmf-50-rtm-is-installed-on-top-of-wmf-50-production-preview"></a>A DSC-parancsmagok előfordulhat, hogy nem működik, ha a WMF 5.0 RTM WMF 5.0 éles előzetes funkciók mellett kártevőészlelést telepítve van
------------------------------------------------------
**Megoldás:** a következő parancsot egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):
```powershell
    mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof
```


<a name="lcm-can-go-into-an-unstable-state-while-using-get-dscconfiguration-in-debugmode"></a>LCM is kísérhet instabil állapotban DebugMode a Get-DscConfiguration használata során
-------------------------------------------------------------------------------

Ha LCM DebugMode, állítsa le a Get-DscConfiguration feldolgozását a CTRL + C billentyűkombináció lenyomásával okozhat a go LCM instabil állapotban ilyen be, hogy a DSC-parancsmagok többsége nem fognak működni.

**Megoldás:** nem CTRL + C billentyűkombináció Get-DscConfiguration parancsmag hibakeresés során.


<a name="stop-dscconfiguration-may-hang-in-debugmode"></a>A DebugMode STOP-DscConfiguration lefagyhat
------------------------------------------------------------------------------------------------------------------------
Ha LCM DebugMode, Stop-DscConfiguration leállhat a Get-DscConfiguration által elindított egy műveletet leállítására tett kísérlet közben

**Megoldás:** Befejezés szakaszban leírt módon történő Get-DscConfiguration indította a műveletet a hibakeresés "[hibakeresés DSC erőforrások](https://msdn.microsoft.com/powershell/dsc/debugresource)".


<a name="no-verbose-error-messages-are-shown-in-debugmode"></a>Részletes hibaüzenetek nem jelennek meg DebugMode
-----------------------------------------------------------------------------------
Ha LCM DebugMode, a részletes hibaüzeneteket a DSC-források jelennek meg.

**Megoldás:** letiltása *DebugMode* részletes üzenetek a erőforrás megtekintéséhez


<a name="invoke-dscresource-operations-cannot-be-retrieved-by-get-dscconfigurationstatus-cmdlet"></a>Invoke-DscResource műveletek nem sikerült beolvasni a Get-DscConfigurationStatus parancsmaggal
--------------------------------------------------------------------------------------
Után közvetlenül a bármilyen olyan erőforrás módszerek meghívására Invoke-DscResource parancsmag használatával, a rekordok ilyen művelet nem sikerült beolvasni a Get-DscConfigurationStatus egy későbbi időpontban.

**Megoldás:** nincs.


<a name="get-dscconfigurationstatus-returns-pull-cycle-operations-as-type-consistency"></a>Get-DscConfigurationStatus értéket ad vissza lekéréses ciklus műveletek típusként *konzisztencia*
---------------------------------------------------------------------------------
Ha egy csomópont értéke LEKÉRÉSES frissítési mód, minden egyes lekéréses műveletet hajtja végre, a Get-DscConfigurationStatus parancsmag jelent-e a művelet típusú, mint *konzisztencia* helyett *kezdeti*

**Megoldás:** nincs.

<a name="invoke-dscresource-cmdlet-does-not-return-message-in-the-order-they-were-produced"></a>Invoke-DscResource parancsmag nem ad vissza üzenet állították sorrendben
---------------------------------------------------------------------------------
Az Invoke-DscResource parancsmag nem ad vissza figyelmeztetést, a részletes és hibaüzeneteket LCM vagy a DSC-erőforrás állították sorrendben.

**Megoldás:** nincs.


<a name="dsc-resources-cannot-be-debugged-easily-when-used-with-invoke-dscresource"></a>A DSC-erőforrások nem indítja el egyszerűen Invoke-DscResource használata esetén
-----------------------------------------------------------------------
Ha az LCM hibakeresési módban fut. (lásd: [hibakeresés DSC erőforrások](https://msdn.microsoft.com/powershell/dsc/debugresource) további részletekért), Invoke-DscResource parancsmag nem ad futási térben csatlakoztatni a hibakeresési információ.
**Megoldás:** felderítése, és csatolja a parancsmagok használatával futási térben **Get-PSHostProcessInfo**, **Enter-PSHostProcess** , **Get-futási térben** és **Hibakeresési-futási térben** hibakeresése a DSC-erőforrás.

```powershell
# Find all the processes hosting PowerShell
Get-PSHostProcessInfo

ProcessName ProcessId AppDomainName
----------- --------- -------------
powershell 3932 DefaultAppDomain
powershell_ise 2304 DefaultAppDomain
WmiPrvSE 3396 DscPsPluginWkr_AppDomain

# Enter the process that is hosting DSC engine (WMI process with DscPsPluginWkr_Appdomain)
Enter-PSHostProcess -Id 3396 -AppDomainName DscPsPluginWkr_AppDomain

# Find all the available rusnspaces in that process
Get-Runspace

Id Name ComputerName Type State Availability
-- ---- ------------ ---- ----- ------------
2 Runspace2 localhost Local Opened InBreakpoint
5 RemoteHost localhost Local Opened Busy

# Debug the runspace that is in **InBreakpoint** availability state
Debug-Runspace -Id 2
```


<a name="various-partial-configuration-documents-for-same-node-cannot-have-identical-resource-names"></a>Azonos csomópont különböző részleges konfigurációs dokumentumok azonos erőforrás neve nem lehet.
------------------------------------------------------------------------------------------

Több részleges konfigurációkat egyetlen csomópont vannak telepítve, az erőforrások OK azonos nevű futásidejű hiba.

**Megoldás:** különböző részleges konfigurációk is ugyanazokat az erőforrásokat különböző neveket használja.


<a name="start-dscconfiguration-useexisting-does-not-work-with--credential"></a>Start-DscConfiguration – UseExisting nem működik a - Credential
------------------------------------------------------------------

– UseExisting paraméterrel, a Start-DscConfiguration használatakor az-Credential paraméter a rendszer figyelmen kívül hagyja. A DSC alapértelmezett folyamat identitást használja folytatja a műveletet. Ez hibát okoz, ha eltérő hitelesítő adatok a távoli csomóponton levő folytatáshoz van szükség.

**Megoldás:** használata CIM munkamenet távoli DSC műveletek:
```powershell
$session = New-CimSession -ComputerName $node -Credential $credential
Start-DscConfiguration -UseExisting -CimSession $session
```


<a name="ipv6-addresses-as-node-names-in-dsc-configurations"></a>IPv6-címek, a csomópont nevének a DSC-konfigurációk
--------------------------------------------------
IPv6-címek, a csomópont nevének a DSC konfigurációs parancsfájlokat ebben a kiadásban nem támogatottak.

**Megoldás:** nincs.


<a name="debugging-of-class-based-dsc-resources"></a>A DSC osztály-alapú erőforrások hibakeresés
--------------------------------------
A DSC-erőforrások osztály-alapú hibakeresés nem támogatott ebben a kiadásban.

**Megoldás:** nincs.


<a name="variables--functions-defined-in-script-scope-in-dsc-class-based-resource-are-not-preserved-across-multiple-calls-to-a-dsc-resource"></a>Változók & DSC osztály-alapú erőforrás $script hatókörben megadott függvények nem maradnak meg több hívások DSC-erőforrás között
-------------------------------------------------------------------------------------------------------------------------------------

Start-DSCConfiguration több egymást követő hívások sikertelen lesz, ha a configuration osztály-alapú erőforrás, változók vagy $script hatókörben megadott funkciók használ.

**Megoldás:** DSC erőforrásosztály magát a változók és a funkciók meghatározása. No $script hatókör változók vagy funkciók.


<a name="dsc-resource-debugging-when-a-resource-is-using-psdscrunascredential"></a>Ha egy erőforrás PSDscRunAsCredential hibakeresés DSC erőforrás
----------------------------------------------------------------------
A DSC erőforrás hibakeresési erőforrás használatakor a *PSDscRunAsCredential* tulajdonság a konfigurációban nincs suported ebben a kiadásban.

**Megoldás:** nincs.


<a name="psdscrunascredential-is-not-supported-for-dsc-composite-resources"></a>PsDscRunAsCredential DSC összetett erőforrások esetén nem támogatott
----------------------------------------------------------------

**Megoldás:** használata Credential tulajdonság, ha elérhető. Példa ServiceSet és WindowsFeatureSet


<a name="get-dscresource--syntax-does-not-reflect-psdscrunascredential-correctly"></a>*Get-DscResource-szintaxis* nem tükrözi a megfelelő PsDscRunAsCredential
-------------------------------------------------------------------------
Get-DscResource-szintaxis nem tükrözi PsDscRunAsCredential megfelelően erőforrás kötelezőként jelöli meg, vagy nem támogatja ezt.

**Megoldás:** nincs. Azonban ISE konfigurációs szerzői tükrözi PsDscRunAsCredential tulajdonságra vonatkozó metaadat IntelliSense használatakor.


<a name="windowsoptionalfeature-is-not-available-in-windows-7"></a>WindowsOptionalFeature nem érhető el a Windows 7
-----------------------------------------------------

A WindowsOptionalFeature DSC-erőforrás nem érhető el a Windows 7. Ehhez az erőforráshoz van szükség, a DISM-modulját, és a DISM-parancsmagok érhetők el a Windows 8 és újabb verziókban a Windows operációs rendszer elindítása.

<a name="for-class-based-dsc-resources-import-dscresource--moduleversion-may-not-work-as-expected"></a>Osztály-alapú DSC erőforrások importálás-DscResource - ModuleVersion előfordulhat, hogy nem működik megfelelően
------------------------------------------------------------------------------------------
Ha a fordítás fürtcsomópont egy osztály-alapú DSC erőforrásmodul, több verziójának `Import-DscResource -ModuleVersion` nem veszi a megadott verzióját, és annak az eredménye a következő fordítási hiba.

```
ImportClassResourcesFromModule : Exception calling "ImportClassResourcesFromModule" with "3" argument(s): "Keyword 'MyTestResource' already defined in the configuration."
At C:\Windows\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:2035 char:35
+ ... rcesFound = ImportClassResourcesFromModule -Module $mod -Resources $r ...
+                 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [ImportClassResourcesFromModule], MethodInvocationException
    + FullyQualifiedErrorId : PSInvalidOperationException,ImportClassResourcesFromModule
```

**Megoldás:** importálja a szükséges verziót megadásával a *ModuleSpecification* az objektum a `-ModuleName` a `RequiredVersion` kulcs van megadva az alábbiak szerint:
``` PowerShell
Import-DscResource -ModuleName @{ModuleName='MyModuleName';RequiredVersion='1.2'}
```

<a name="some-dsc-resources-like-registry-resource-may-start-to-take-a-long-time-to-process-the-request"></a>Néhány DSC-erőforrásokhoz, mint a beállításjegyzék erőforrás indítsa el a kérelem feldolgozása hosszú ideig tarthat.
--------------------------------------------------------------------------------------------------------------------------------

**Resolution1:** hozzon létre egy ütemezett feladat, amely a szükségtelenné vált a következő mappa rendszeres időközönként.
``` PowerShell
$env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis
```

**Resolution2:** karbantartása a DSC-konfiguráció módosítása a *CommandAnalysis* végén található a konfigurációs mappát.
``` PowerShell
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
        DependsOn="[Registry]SetRegisteredOwner"
        getscript="@{}"
        testscript = 'Remove-Item -Path $env:windir\system32\config\systemprofile\AppData\Local\Microsoft\Windows\PowerShell\CommandAnalysis -Force -Recurse -ErrorAction SilentlyContinue -ErrorVariable ev | out-null;$true'
        setscript = '$true'
    }
}
```
