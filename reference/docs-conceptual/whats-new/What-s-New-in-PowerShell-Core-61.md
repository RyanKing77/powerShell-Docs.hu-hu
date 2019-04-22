---
title: A PowerShell Core 6.1 újdonságai
description: Új szolgáltatásaival és módosításaival, amely a PowerShell Core 6.1
ms.date: 09/13/2018
ms.openlocfilehash: fe1e892d4a13a7758f5405867fdd7488c059f5cc
ms.sourcegitcommit: 17ce42f97e13e8b3286779dc3f583474b0357023
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59293316"
---
# <a name="whats-new-in-powershell-core-61"></a>A PowerShell Core 6.1 újdonságai

Alább néhány fontos új szolgáltatásokat és módosításokat vezettek be a PowerShell Core 6.1 egy kijelölt van.

Is **tonna** "unalmas szolgáltatáshasználatot", amelyek gyorsabb és stabilabb (és sok és számos hibajavítás) PowerShell!
Változások teljes listájához tekintse meg a [a Githubon változásnaplójában](https://github.com/PowerShell/PowerShell/blob/master/CHANGELOG.md).

És közben ki az alábbi néhány nevet nevezzük, Köszönjük, hogy [összes a közösségi közreműködők](https://github.com/PowerShell/PowerShell/graphs/contributors) , amely ebben a kiadásban lehetővé tenni.

## <a name="net-core-21"></a>.NET Core 2.1

Után, a .NET Core 2.1 átkerül PowerShell Core 6.1 [májusban, amely a](https://blogs.msdn.microsoft.com/dotnet/2018/05/30/announcing-net-core-2-1/), számos fejlesztéssel a Powershellbe, így többek között:

- teljesítménnyel kapcsolatos fejlesztések (lásd: [alábbi](#performance-improvements))
- Az Alpine Linux-támogatás (előzetes verzió)
- [Globális eszköz támogatott .NET](/dotnet/core/tools/global-tools) – hamarosan a PowerShell az elkövetkező
- [`Span<T>`](/dotnet/api/system.span-1?view=netcore-2.1)

## <a name="windows-compatibility-pack-for-net-core"></a>.NET Core for Windows kompatibilitási csomag

A Windows, a .NET-csapattal szállított a [Windows kompatibilitási csomag a .NET Core](https://blogs.msdn.microsoft.com/dotnet/2017/11/16/announcing-the-windows-compatibility-pack-for-net-core/), szerelvényeket, amelyek számos hozzáadása egy készletét vissza a .NET Core Windows API-k eltávolítása.

Lehetőségekkel bővült a Windows-kompatibilitási csomag PowerShell Core 6.1-es kiadásra, hogy bármilyen modulok vagy ezekkel az API-parancsprogramok is használhatók legyenek elérhetők.

A Windows-kompatibilitási csomag lehetővé teszi, hogy a PowerShell Core használata **több mint 1900 parancsmagok a Windows rendszerrel szállított 2018. október 10. és a Windows Server 2019**.

## <a name="support-for-application-whitelisting"></a>Az alkalmazások engedélyezési listáinak támogatása

PowerShell Core 6.1 rendelkezik a Windows PowerShell 5.1 támogatása paritásos [AppLocker](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/applocker/applocker-overview) és [Device Guard](https://docs.microsoft.com/windows/security/threat-protection/device-guard/introduction-to-device-guard-virtualization-based-security-and-windows-defender-application-control) alkalmazásengedélyezés bevezetését.
Az alkalmazások engedélyezési listáinak lehetővé teszi, hogy a szabályozhatja a melyik bináris fájlokat engedélyezett hajtható végre, a PowerShell-lel használt [korlátozott nyelvmód](https://blogs.msdn.microsoft.com/powershell/2017/11/02/powershell-constrained-language-mode/).

## <a name="performance-improvements"></a>Teljesítménnyel kapcsolatos fejlesztések

A PowerShell Core 6.0 végzett néhány jelentős teljesítménybeli fejlesztései.
PowerShell Core 6.1 továbbfejleszti bizonyos műveletek sebessége.

Ha például `Group-Object` 66 %-kal rendelkezik lett felgyorsul:

```powershell
Measure-Command { 1..100000 | % {Get-Random -Minimum 1 -Maximum 10000} | Group-Object }
```

|              | Windows PowerShell 5.1 | A PowerShell Core 6.0 | A PowerShell Core 6.1 |
|--------------|------------------------|---------------------|---------------------|
| Idő (mp)   | 25.178                 | 19.653              | 6.641               |
| Gyorsulás figyelhető meg (%) | N.a.                    | 21.9%               | 66.2%               |

Hasonlóképpen az alábbihoz hasonló rendezési forgatókönyvek javult több mint 15 %-kal:

```powershell
Measure-Command { 1..100000 | % {Get-Random -Minimum 1 -Maximum 10000} | Sort-Object }
```

|              | Windows PowerShell 5.1 | A PowerShell Core 6.0 | A PowerShell Core 6.1 |
|--------------|------------------------|---------------------|---------------------|
| Idő (mp)   | 12.170                 | 8.493               | 7.08                |
| Gyorsulás figyelhető meg (%) | N.a.                    | 30.2%               | 16.6%               |

`Import-Csv` azt is lett felgyorsul jelentősen regresszió után a Windows PowerShellben.
Az alábbi példa egy teszt CSV 26,616 sorok és oszlopok hat használja:

```powershell
Measure-Command {$a = Import-Csv foo.csv}
```

|              | Windows PowerShell 5.1 | A PowerShell Core 6.0 | A PowerShell Core 6.1    |
|--------------|------------------------|---------------------|------------------------|
| Idő (mp)   | 0.441                  | 1.069               | 0.268                  |
| Gyorsulás figyelhető meg (%) | N.a.                    | -142.4%             | 74.9 % (39.2 % WPS) |

Végül, a JSON-t átalakítás `PSObject` rendelkezik lett felgyorsul több mint 50 %-kal Windows PowerShell óta.
Az alábbi példa ~ 2 MB-os teszt JSON-fájlt használ:

```powershell
Measure-Command {Get-Content .\foo.json | ConvertFrom-Json}
```

|              | Windows PowerShell 5.1 | A PowerShell Core 6.0 | A PowerShell Core 6.1    |
|--------------|------------------------|---------------------|------------------------|
| Idő (mp)   | 0.259                  | 0.577               | 0.125                  |
| Gyorsulás figyelhető meg (%) | N.a.                    | -122.8%             | 78.3 % (51.7 % WPS) |

## <a name="check-system32-for-compatible-in-box-modules-on-windows"></a>Ellenőrizze `system32` a Windows kompatibilis beépített modulok

A Windows 10-es 1809 update és a Windows Server 2019 számos beépített kell megjelölni kompatibilis PowerShell Core a PowerShell-modulok frissítve.

PowerShell Core 6.1 indulásakor, automatikus módon kiegészül `$windir\System32` részeként a `PSModulePath` környezeti változót.
Azonban csak jelezzék modulok `Get-Module` és `Import-Module` ha annak `CompatiblePSEdition` kompatibilis van megjelölve `Core`.


```powershell
Get-Module -ListAvailable
```

> [!NOTE]
> Attól függően, hogy milyen szerepkörök és szolgáltatások telepítve vannak a különböző elérhető modulok jelenhet meg.

```Output
...
    Directory: C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules

ModuleType Version    Name                                PSEdition ExportedCommands
---------- -------    ----                                --------- ----------------
Manifest   2.0.1.0    Appx                                Core,Desk {Add-AppxPackage, Get-AppxPackage, Get-AppxPacka...
Manifest   1.0.0.0    BitLocker                           Core,Desk {Unlock-BitLocker, Suspend-BitLocker, Resume-Bit...
Manifest   1.0.0.0    DnsClient                           Core,Desk {Resolve-DnsName, Clear-DnsClientCache, Get-DnsC...
Manifest   1.0.0.0    HgsDiagnostics                      Core,Desk {New-HgsTraceTarget, Get-HgsTrace, Get-HgsTraceF...
Binary     2.0.0.0    Hyper-V                             Core,Desk {Add-VMAssignableDevice, Add-VMDvdDrive, Add-VMF...
Binary     1.1        Hyper-V                             Core,Desk {Add-VMDvdDrive, Add-VMFibreChannelHba, Add-VMHa...
Manifest   2.0.0.0    NetAdapter                          Core,Desk {Disable-NetAdapter, Disable-NetAdapterBinding, ...
Manifest   1.0.0.0    NetEventPacketCapture               Core,Desk {New-NetEventSession, Remove-NetEventSession, Ge...
Manifest   2.0.0.0    NetLbfo                             Core,Desk {Add-NetLbfoTeamMember, Add-NetLbfoTeamNic, Get-...
Manifest   1.0.0.0    NetNat                              Core,Desk {Get-NetNat, Get-NetNatExternalAddress, Get-NetN...
Manifest   2.0.0.0    NetQos                              Core,Desk {Get-NetQosPolicy, Set-NetQosPolicy, Remove-NetQ...
Manifest   2.0.0.0    NetSecurity                         Core,Desk {Get-DAPolicyChange, New-NetIPsecAuthProposal, N...
Manifest   1.0.0.0    NetSwitchTeam                       Core,Desk {New-NetSwitchTeam, Remove-NetSwitchTeam, Get-Ne...
Manifest   1.0.0.0    NetWNV                              Core,Desk {Get-NetVirtualizationProviderAddress, Get-NetVi...
Manifest   2.0.0.0    TrustedPlatformModule               Core,Desk {Get-Tpm, Initialize-Tpm, Clear-Tpm, Unblock-Tpm...
...
```

Minden modul használatával megjeleníthető a viselkedést felülírhatja a `-SkipEditionCheck` paraméter váltani.
Is elérhetővé tettünk egy `PSEdition` tulajdonság a táblázatos kimenetéhez.

```powershell
Get-Module Net* -ListAvailable -SkipEditionCheck
```

```Output
    Directory: C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules

ModuleType Version    Name                        PSEdition ExportedCommands
---------- -------    ----                        --------- ----------------
Manifest   2.0.0.0    NetAdapter                  Core,Desk {Disable-NetAdapter, Disable-NetAdapterBinding, ...
Manifest   1.0.0.0    NetConnection               Core,Desk {Get-NetConnectionProfile, Set-NetConnectionProf...
Manifest   1.0.0.0    NetDiagnostics              Desk      Get-NetView
Manifest   1.0.0.0    NetEventPacketCapture       Core,Desk {New-NetEventSession, Remove-NetEventSession, Ge...
Manifest   2.0.0.0    NetLbfo                     Core,Desk {Add-NetLbfoTeamMember, Add-NetLbfoTeamNic, Get-...
Manifest   1.0.0.0    NetNat                      Core,Desk {Get-NetNat, Get-NetNatExternalAddress, Get-NetN...
Manifest   2.0.0.0    NetQos                      Core,Desk {Get-NetQosPolicy, Set-NetQosPolicy, Remove-NetQ...
Manifest   2.0.0.0    NetSecurity                 Core,Desk {Get-DAPolicyChange, New-NetIPsecAuthProposal, N...
Manifest   1.0.0.0    NetSwitchTeam               Core,Desk {New-NetSwitchTeam, Remove-NetSwitchTeam, Get-Ne...
Manifest   1.0.0.0    NetTCPIP                    Core,Desk {Get-NetIPAddress, Get-NetIPInterface, Get-NetIP...
Manifest   1.0.0.0    NetWNV                      Core,Desk {Get-NetVirtualizationProviderAddress, Get-NetVi...
Manifest   1.0.0.0    NetworkConnectivityStatus   Core,Desk {Get-DAConnectionStatus, Get-NCSIPolicyConfigura...
Manifest   1.0.0.0    NetworkSwitchManager        Core,Desk {Disable-NetworkSwitchEthernetPort, Enable-Netwo...
Manifest   1.0.0.0    NetworkTransition           Core,Desk {Add-NetIPHttpsCertBinding, Disable-NetDnsTransi...
```

Ezzel a viselkedéssel kapcsolatos további információkért tekintse meg [PowerShell RFC0025](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0025-PSCore6-and-Windows-Modules.md).

## <a name="markdown-cmdlets-and-rendering"></a>Markdown-parancsmagok és megjelenítési szoftverek

Markdown a olvasható egyszerű szöveges dokumentumok létrehozásának alapszintű formázását, amely szabványos HTML be jeleníthetők meg.

Bizonyos parancsmagok tettünk elérhetővé, amelyek lehetővé teszik az átalakítás és a konzolon Markdown-dokumentumok 6.1 többek között:

- `ConvertFrom-Markdown`
- `Get-MarkdownOption`
- `Set-MarkdownOption`
- `Show-Markdown`

Ha például `Show-Markdown` megjelenítve egy Markdown-fájlt a konzolon:

![Show-Markdown-példa](./images/markdown_example.png)

Hogyan működnek a ezekkel a parancsmagokkal kapcsolatos további információkért tekintse meg [az RFC](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0025-Native-Markdown-Rendering.md).

## <a name="experimental-feature-flags"></a>Kísérleti funkció jelzők

Kísérleti funkció jelzők engedélyezése a felhasználók számára, kapcsolja be, amely még nem lett véglegesítése funkciókat.
Ezek kísérleti funkciók nem támogatottak, és előfordulhat, hogy hibák.

További információ ennek a funkciónak a [PowerShell RFC0029](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0029-Support-Experimental-Features.md).

## <a name="web-cmdlet-improvements"></a>Webes parancsmag fejlesztései

Köszönhetően [ @markekraus ](https://github.com/markekraus), egy teljes slew kapcsolatos fejlesztések történtek-e a webalkalmazás-parancsmagok: [`Invoke-WebRequest`](/powershell/module/microsoft.powershell.utility/invoke-webrequest)
és [ `Invoke-RestMethod` ](/powershell/module/microsoft.powershell.utility/invoke-restmethod).

- [Lekéréses kérelem #6109](https://github.com/PowerShell/PowerShell/pull/6109) -kódolási értéke UTF-8 az alapértelmezett `application-json` válaszok
- [Lekéréses kérelem #6018](https://github.com/PowerShell/PowerShell/pull/6018)  -  `-SkipHeaderValidation` , hogy a paraméter `Content-Type` fejlécek, amelyek nem szabványokkal kompatibilis
- [Lekéréses kérelem #5972](https://github.com/PowerShell/PowerShell/pull/5972)  -  `Form` paraméter támogatása egyszerűsített `multipart/form-data` támogatása
- [Lekéréses kérelem #6338](https://github.com/PowerShell/PowerShell/pull/6338) – megfelelő, a kis-és kapcsolat kulcsok kezelése
- [Lekéréses kérelem #6447](https://github.com/PowerShell/PowerShell/pull/6447) -hozzáadása `-Resume` paraméter webes parancsmagok esetében

## <a name="remoting-improvements"></a>Távoli eljáráshívás fejlesztései

### <a name="powershell-direct-for-containers-tries-to-use-powershell-core-first"></a>A tárolók a PowerShell Directet elsőként próbálja használni a PowerShell Core

[PowerShell Directet](/virtualization/hyper-v-on-windows/user-guide/powershell-direct) PowerShell és a egy Hyper-V virtuális gép vagy a tároló nincs hálózati kapcsolat vagy más távoli felügyeleti szolgáltatások összekapcsolhatók a Hyper-V szolgáltatása.

Múltbeli időpont a PowerShell Directet csatlakoztatva a tárolón a Beérkezett fájlok Windows PowerShell-példány használatával.
Most, PowerShell Direct először használatával próbál kapcsolódni az elérhető `pwsh.exe` a a `PATH` környezeti változót.
Ha `pwsh.exe` nem érhető el, PowerShell Direct visszavált használandó `powershell.exe`.

### <a name="enable-psremoting-now-creates-separate-remoting-endpoints-for-preview-versions"></a>`Enable-PSRemoting` ekkor létrehozza az előzetes verziókban külön távoli eljáráshívás végpontok

`Enable-PSRemoting` most létrehoz két távoli eljáráshívás munkamenet-konfigurációk:

- Egy a PowerShell főverziója. Például: `PowerShell.6`. Ezt a végpontot, amely képes lehet hivatkozni alverzió frissítések között, a "rendszerszintű" PowerShell 6-os munkamenet-konfiguráció
- Egy verzióspecifikus munkamenet-konfiguráció, például: `PowerShell.6.1.0`

Ez a viselkedés akkor hasznos, ha ugyanazon a gépen több PowerShell 6-os verzió telepítve, és elérhető legyen.

Továbbá PowerShell előzetes verziója mostantól igénybe a saját távoli eljáráshívás a munkamenet-konfigurációk futtatása után a `Enable-PSRemoting` parancsmagot:

```powershell
C:\WINDOWS\system32> Enable-PSRemoting
```

A kimeneti eltérő, ha még nem állított be a Rendszerfelügyeleti webszolgáltatások előtt lehet.

```Output
WinRM is already set up to receive requests on this computer.
WinRM is already set up for remote management on this computer.
```

Ezután láthatja, hogy külön PowerShell-munkamenet konfigurációk az előzetes verzióra, és stabil összeállítja a PowerShell 6-os, és minden egyes adott verziójához.

```powershell
Get-PSSessionConfiguration
```

```Output
Name          : PowerShell.6.2-preview.1
PSVersion     : 6.2
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : PowerShell.6-preview
PSVersion     : 6.2
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : powershell.6
PSVersion     : 6.1
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : powershell.6.1.0
PSVersion     : 6.1
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed
```

### <a name="userhostport-syntax-supported-for-ssh"></a>`user@host:port` az SSH-hoz támogatott szintaxis

SSH ügyfelek általában támogatja a kapcsolati karakterlánc a következő formátumban `user@host:port`.
Igény szerinti hozzáadásával SSH protokollt a PowerShell-táveléréssel lehetőségekkel bővült a kapcsolati karakterlánc-formátum támogatása:

`Enter-PSSession -HostName fooUser@ssh.contoso.com:2222`

## <a name="msi-option-to-add-explorer-shell-context-menu-on-windows"></a>MSI lehetőség a Windows Intéző rendszerhéj helyi menüjének hozzáadása

Köszönhetően [ @bergmeister ](https://github.com/bergmeister), engedélyezheti a Windows egy helyi menüjében. Most megnyithatja a PowerShell 6.1 a rendszerre telepített bármely mappából a Windows Explorerben:

![A PowerShell 6-os rendszerhéj helyi menü](./images/shell_context_menu.png)

## <a name="goodies"></a>Hasznos eszközök

### <a name="run-as-administrator-in-the-windows-shortcut-jump-list"></a>"Futtatás rendszergazdaként" a Windows helyi jump listában

Köszönhetően [ @bergmeister ](https://github.com/bergmeister), a PowerShell Core helyi jump listában mostantól tartalmazza a "Futtatás mint rendszergazda":

![Futtatás a PowerShell 6-os helyettesítő listában rendszergazdaként](./images/jumplist.png)

### <a name="cd---returns-to-previous-directory"></a>`cd -` adja vissza az előző könyvtár

```powershell
C:\Windows\System32> cd C:\
C:\> cd -
C:\Windows\System32>
```

Vagy a Linux rendszeren:

```ShellSession
PS /etc> cd /usr/bin
PS /usr/bin> cd -
PS /etc>
```

Ezenkívül `cd` és `cd --` módosítsa `$HOME`.

### `Test-Connection`

Köszönhetően [ @iSazonov ](https://github.com/iSazonov), a [ `Test-Connection` ](/powershell/module/microsoft.powershell.management/test-connection) parancsmag rendelkezik már a PowerShell Core.

### <a name="update-help-as-non-admin"></a>`Update-Help` a nem rendszergazda

Kérték `Update-Help` már nem kell rendszergazdaként kell futtatnia.
`Update-Help` Mostantól alapértelmezés szerint súgó, felhasználói hatókörbe tartozó mappába menti.

### <a name="new-methodsproperties-on-pscustomobject"></a>Új módszerek/tulajdonságai `PSCustomObject`

Köszönhetően [ @iSazonov ](https://github.com/iSazonov), új módszerek és a Tulajdonságok hozzáadtunk `PSCustomObject`.
`PSCustomObject` most már tartalmaz egy `Count` / `Length` tulajdonsága mint más objektumok.

```powershell
$PSCustomObject = [pscustomobject]@{foo = 1}

$PSCustomObject.Length
```

```Output
1
```

```powershell
$PSCustomObject.Count
```

```Output
1
```

Ezt a munkát is tartalmaz `ForEach` és `Where` módszereket, amelyek lehetővé teszik, hogy működjön, és szűrheti a `PSCustomObject` elemek:

```powershell
$PSCustomObject.ForEach({$_.foo + 1})
```

```Output
2
```

```powershell
$PSCustomObject.Where({$_.foo -gt 0})
```

```Output
foo
---
  1
```

### `Where-Object -Not`

Köszönhetően @SimonWahlin, tettünk elérhetővé a `-Not` paramétert `Where-Object`.
Egy objektum, a folyamat meglétét, tulajdonság vagy egy NULL értékű vagy üres tulajdonság értéke most már szűrheti.

Ez a parancs például minden olyan szolgáltatás, amely nincs definiálva a függő szolgáltatások adja vissza:

```powershell
Get-Service | Where-Object -Not DependentServices
```

### <a name="new-modulemanifest-creates-a-bom-less-utf-8-document"></a>`New-ModuleManifest` AJ nélküli UTF-8 dokumentum létrehozása

Adja meg az áthelyezés AJ nélküli UTF-8, a PowerShell 6.0-s, frissítettük a `New-ModuleManifest` parancsmaggal hozzon létre egy egyik UTF-16 helyett AJ nélküli UTF-8-dokumentumot.

### <a name="conversions-from-psmethod-to-delegate"></a>Átváltás a PSMethod delegálása

Köszönhetően [ @powercode ](https://github.com/powercode), mostantól támogatjuk a átalakítása egy `PSMethod` delegált be.
Ez lehetővé teszi, hogy többek között a megadásának `PSMethod` `[M]::DoubleStrLen` be delegált értékként `[M]::AggregateString`:

```powershell
class M {
    static [int] DoubleStrLen([string] $value) { return 2 * $value.Length }

    static [long] AggregateString([string[]] $values, [func[string, int]] $selector) {
        [long] $res = 0
        foreach($s in $values){
            $res += $selector.Invoke($s)
        }
        return $res
    }
}

[M]::AggregateString((gci).Name, [M]::DoubleStrLen)
```

További információ az ezt a módosítást, tekintse meg [PR #5287](https://github.com/PowerShell/PowerShell/pull/5287).

### <a name="standard-deviation-in-measure-object"></a>Szórás `Measure-Object`

Köszönhetően [ @CloudyDino ](https://github.com/CloudyDino), hozzáadtunk egy `StandardDeviation` tulajdonságot `Measure-Object`:

```powershell
Get-Process | Measure-Object -Property CPU -AllStats
```

```Output
Count             : 308
Average           : 31.3720576298701
Sum               : 9662.59375
Maximum           : 4416.046875
Minimum           :
StandardDeviation : 264.389544720926
Property          : CPU
```

### `GetPfxCertificate -Password`

Köszönhetően [ @maybe-hello-world ](https://github.com/maybe-hello-world), `Get-PfxCertificate` most már rendelkezik a `Password` paraméter, amely egy `SecureString`. Ez lehetővé teszi, hogy azt nem interaktív módon:

```powershell
$certFile = '\\server\share\pwd-protected.pfx'
$certPass = Read-Host -AsSecureString -Prompt 'Enter the password for certificate: '

$certThumbPrint = (Get-PfxCertificate -FilePath $certFile -Password $certPass ).ThumbPrint
```

### <a name="removal-of-the-more-function"></a>Eltávolítását a `more` függvény

A múltban PowerShell tartalmazza a szükséges a Windows nevű függvény `more` , hogy a burkolt be `more.com`.
Ez a függvény már el lett távolítva.

Emellett a `help` függvény módosítása, hogy `more.com` Windows vagy a rendszer alapértelmezett személyi hívó által megadott `$env:PAGER` nem Windows platformokon.

### <a name="cd-drivename-now-returns-users-to-the-current-working-directory-in-that-drive"></a>`cd DriveName:` most adja vissza a felhasználók a meghajtón található az aktuális munkakönyvtár

Korábban, a `Set-Location` vagy `cd` térjen vissza a felhasználók az alapértelmezett hely a meghajtó küldött PSDrive.

Köszönhetően [ @mcbobke ](https://github.com/mcbobke), felhasználók ekkor elküldi az utolsó ismert aktuális munkakönyvtár az adott munkamenethez.

### <a name="windows-powershell-type-accelerators"></a>Windows PowerShell-típus megoldásgyorsítók

A Windows PowerShellben amelyet hozzáadott a következő típusú megoldásgyorsítók könnyebb megfelelő adattípusukkal együtt működik:

- `[adsi]`: `System.DirectoryServices.DirectoryEntry`
- `[adsisearcher]`: `System.DirectoryServices.DirectorySearcher`
- `[wmi]`: `System.Management.ManagementObject`
- `[wmiclass]`: `System.Management.ManagementClass`
- `[wmisearcher]`: `System.Management.ManagementObjectSearcher`

A típus gyorsítók nem szereplő PowerShell 6-os, de a futó Windows PowerShell 6.1 lettek hozzáadva.

Ezek a típusok lehetnek hasznosak könnyedén hozhat létre, amely az AD és a WMI-objektumok.

Ha például lekérdezheti, ha az LDAP:

```powershell
[adsi]'LDAP://CN=FooUse,OU=People,DC=contoso,DC=com'
```

A következő példában egy Win32_OperatingSystem CIM-objektumot hoz létre:

```powershell
[wmi]"Win32_OperatingSystem=@"
```

```Output
SystemDirectory : C:\WINDOWS\system32
Organization    : Contoso IT
BuildNumber     : 18234
RegisteredUser  : Contoso Corp.
SerialNumber    : 12345-67890-ABCDE-F0123
Version         : 10.0.18234
```

Ebben a példában egy Win32_OperatingSystem osztály ManagementClass objektumot ad vissza.

```powershell
[wmiclass]"Win32_OperatingSystem"
```

```Output
   NameSpace: ROOT\cimv2

Name                                Methods              Properties
----                                -------              ----------
Win32_OperatingSystem               {Reboot, Shutdown... {BootDevice, BuildNumber, BuildType, Caption...}
```

### <a name="-lp-alias-for-all--literalpath-parameters"></a>`-lp` az összes alias `-LiteralPath` paraméterek

Köszönhetően [ @kvprasoon ](https://github.com/kvprasoon), hogy most már megvannak a paraméter-alias `-lp` minden a beépített PowerShell-parancsmagok, amelyek rendelkeznek egy `-LiteralPath` paraméter.

## <a name="breaking-changes"></a>Kompatibilitástörő változások

### <a name="msi-based-installation-paths-on-windows"></a>MSI-alapú telepítési elérési utak a Windows

A Windows az MSI-csomag most telepíti a következő elérési utat:

- `$env:ProgramFiles\PowerShell\6\` 6.x stabil telepítéséhez
- `$env:ProgramFiles\PowerShell\6-preview\` az előzetes verzió telepítésének 6.x

Ez a változás biztosítja, hogy a PowerShell Core, hogy a Microsoft Update frissíteni/szolgáltatója.

További információkért tekintse meg [PowerShell RFC0026](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0026-MSI-Installation-Path.md).

### <a name="telemetry-can-only-be-disabled-with-an-environment-variable"></a>Telemetria csak letiltható a környezeti változó

A PowerShell Core alapvető telemetriai adatokat küld a Microsoftnak, amikor indul el. Az operációs rendszer neve, az operációs rendszer verziójára és a PowerShell-verzió szerepel. Ezek az adatok jobb megértése érdekében a környezetekben, ahol a PowerShell szolgál, és lehetővé teszi számunkra, új funkciókkal és javításokkal rangsorolására tesz lehetővé.

Kapcsolnia ezt a telemetriát, állítsa be a környezeti változó `POWERSHELL_TELEMETRY_OPTOUT` való `true`, `yes`, vagy `1`. Már nem támogatjuk a fájl törlésének `DELETE_ME_TO_DISABLE_CONSOLEHOST_TELEMETRY` telemetria letiltása.

### <a name="disallowed-basic-auth-over-http-in-powershell-remoting-on-unix-platforms"></a>Alapszintű hitelesítés PowerShell-táveléréssel a HTTP-kapcsolaton keresztül a UNIX rendszerű platformokon nem engedélyezett

Letilthatja a nem titkosított forgalmat, a PowerShell-táveléréssel a UNIX rendszerű platformokon mostantól csak NTLM/egyeztetés vagy a HTTPS használatát.

További információ ezekről a változásokról, tekintse meg [probléma #6779](https://github.com/PowerShell/PowerShell/issues/6779).

### <a name="removed-visualbasic-as-a-supported-language-in-add-type"></a>Eltávolított `VisualBasic` egy támogatott nyelv az Add-Type

A múltban sikerült összeállíthatja a Visual Basic-kód használatával a `Add-Type` parancsmagot.
A Visual Basic a ritkán használt `Add-Type`. Ez a funkció PowerShell méretének csökkentésére eltávolítottuk.

### <a name="cleaned-up-uses-of-commandtypesworkflow-and-workflowinfocleaned"></a>Használati tisztítani `CommandTypes.Workflow` és `WorkflowInfoCleaned`

További információ ezekről a változásokról, tekintse meg [PR #6708](https://github.com/PowerShell/PowerShell/pull/6708).

### <a name="group-object-now-sorts-the-groups"></a>Csoportházirend-objektum most már a csoportok rendezése

A teljesítmény fokozása részeként `Group-Object` most adja vissza a csoportok rendezett listája.
Bár a sorrend nem támaszkodhat, sikerült bonthatók Ez a módosítás az első csoport egységben. Azt határozza meg, hogy a a teljesítmény fokozása érdemes a módosítás volt, mert folyamatban van a korábbi működése függ a hatását, alacsony.

Ezt a módosítást a további információkért lásd: [probléma #7409](https://github.com/PowerShell/PowerShell/issues/7409).
