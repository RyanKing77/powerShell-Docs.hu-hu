---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Ismerkedés a Desired State Configuration (DSC) rétegen a Linux rendszeren
ms.openlocfilehash: 69f087434455aae8e97ea07c79c52e493412d134
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686599"
---
# <a name="get-started-with-desired-state-configuration-dsc-for-linux"></a>Ismerkedés a Desired State Configuration (DSC) rétegen a Linux rendszeren

Ez a témakör ismerteti, hogyan kezdheti el a PowerShell Desired State Configuration (DSC) használatával Linux rendszeren. DSC kapcsolatos általános információkért lásd: [Ismerkedés a Windows PowerShell Desired State Configuration](../overview/overview.md).

## <a name="supported-linux-operation-system-versions"></a>Támogatott Linux-művelet rendszerekről

A következő Linux operációsrendszer-verziók Linuxhoz készült DSC támogatottak.

- CentOS 5, 6 és 7 (x86/x64)
- Debian GNU/Linux 6, 7, 8 (x86/x64)
- Oracle Linux 5, 6 és 7 (x86/x64)
- Red Hat Enterprise Linux Server 5, 6 és 7 (x86/x64)
- SUSE Linux Enterprise Server 10, 11, 12 (x86/x64)
- Ubuntu Server 12.04 LTS, 14.04 LTS és 16.04 LTS (x86/x64)

A következő táblázat ismerteti a szükséges csomag függőségeit a DSC Linux rendszeren.

|  Szükséges csomag |  Leírás |  Minimális verziója |
|---|---|---|
| glibc| GNU könyvtár| 2…4 – 31.30|
| python| Python| 2.4 – 3.4|
| omiserver| Nyílt kezelési infrastruktúra| 1.0.8.1|
| openssl| OpenSSL-függvénytárak| 0.9.8-as vagy 1.0|
| ctypes| Python CTypes könyvtár| Meg kell egyeznie a Python-verzió|
| libcurl| a cURL http-klienskódtár| 7.15.1|

## <a name="installing-dsc-for-linux"></a>Linuxhoz készült DSC telepítése

Telepítenie kell a [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) Linuxhoz készült DSC telepítése előtt.

### <a name="installing-omi"></a>OMI telepítése

Desired State Configuration for Linux számára az Open Management Infrastructure (OMI) CIM-kiszolgáló, 1.0.8.1 verzió vagy újabb. OMI letölthető az Open Group: [Nyissa meg a Management Infrastructure (OMI)](https://github.com/Microsoft/omi).

OMI telepítéséhez telepítse a csomagot, amely megfelelő a Linux rendszer (.rpm vagy .deb) és az OpenSSL-verzió (ssl_098 vagy ssl_100) és az architektúra (x64/x86). RPM-csomagot a CentOS, a Red Hat Enterprise Linux, a SUSE Linux Enterprise Server és az Oracle Linux alkalmasak. A Debian GNU/Linux és Ubuntu Server megfelelőek-DEB-csomag. A ssl_098 csomagok megfelelők OpenSSL 0.9.8-as telepítve van, miközben telepítve OpenSSL 1.0 megfelelő számítógépek a ssl_100 csomagok számítógépeken.

> [!NOTE]
> A telepített OpenSSL-verzió azonosításához futtassa a parancsot `openssl version`.

A következő paranccsal telepítse az OMI CentOS 7 x64 rendszerre.

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### <a name="installing-dsc"></a>DSC telepítése

Linuxhoz készült DSC érhető el letöltésre [Itt](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/tag/v1.1.1-294).

DSC telepítéséhez telepítse a csomagot, amely megfelelő a Linux rendszer (.rpm vagy .deb) és az OpenSSL-verzió (ssl_098 vagy ssl_100) és az architektúra (x64/x86). RPM-csomagot a CentOS, a Red Hat Enterprise Linux, a SUSE Linux Enterprise Server és az Oracle Linux alkalmasak. A Debian GNU/Linux és Ubuntu Server megfelelőek-DEB-csomag. A ssl_098 csomagok megfelelők OpenSSL 0.9.8-as telepítve van, miközben telepítve OpenSSL 1.0 megfelelő számítógépek a ssl_100 csomagok számítógépeken.

> [!NOTE]
> A telepített OpenSSL-verzió azonosításához futtassa a parancs openssl-verziót.

Futtassa a következő parancsot, DSC CentOS 7 x64 rendszer telepítése.

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`

## <a name="using-dsc-for-linux"></a>Linuxhoz készült DSC használatával

Az alábbi szakaszok azt ismertetik, hogyan hozhat létre és futtathat a DSC-konfigurációk Linux-számítógépeken.

### <a name="creating-a-configuration-mof-document"></a>A konfigurációs MOF-dokumentum létrehozása

A Windows PowerShell a konfigurációs kulcsszó a Linux rendszerű számítógépek esetében konfiguráció létrehozásához csakúgy, mint a Windows-számítógépek esetében használatos. A következő lépések írják le a konfigurációs dokumentum egy Windows PowerShell használatával egy Linux-számítógép létrehozása.

1. Az nx modul importálásához. Az nx Windows PowerShell-modul tartalmaz beépített erőforrások sémáját DSC Linux rendszeren, és telepítve legyen a helyi számítógépen, és importálja a konfigurációban.

   - Nx-modul telepítéséhez, másolni vagy nx modulkönyvtárat `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` vagy `$PSHOME\Modules`. Az nx-modul a DSC Linux-telepítési csomag tartalmazza. A konfigurációban az nx modul importálásához használja a `Import-DSCResource` parancsot:

   ```powershell
   Configuration ExampleConfiguration{

    Import-DSCResource -Module nx

   }
   ```

2. A konfiguráció meghatározása és a konfigurációs dokumentum létrehozása:

   ```powershell
   Configuration ExampleConfiguration
   {
        Import-DscResource -Module nx

        Node  "linuxhost.contoso.com"
        {
            nxFile ExampleFile 
            {
                DestinationPath = "/tmp/example"
                Contents = "hello world `n"
                Ensure = "Present"
                Type = "File"
            }
        }
   }

   ExampleConfiguration -OutputPath:"C:\temp"
   ```

### <a name="push-the-configuration-to-the-linux-computer"></a>A konfiguráció leküldése a Linux-számítógép

Konfigurációs dokumentumok (MOF-fájlok) a Linux rendszerű számítógépen történő lehet leküldeni a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot. Ez a parancsmag használatához az a [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration), vagy [a Test-DscConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration) parancsmagok távolról egy Linux rendszerű számítógépre kell használnia a CIMSession. A [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) parancsmag segítségével hozzon létre egy Linux rendszerű számítógép CIMSession.

A következő kód bemutatja a DSC-CIMSession létrehozása Linux rendszeren.

```powershell
$Node = "ostc-dsc-01"
$Credential = Get-Credential -UserName:"root" -Message:"Enter Password:"

#Ignore SSL certificate validation
#$opt = New-CimSessionOption -UseSsl:$true -SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true

#Options for a trusted SSL certificate
$opt = New-CimSessionOption -UseSsl:$true
$Sess=New-CimSession -Credential:$credential -ComputerName:$Node -Port:5986 -Authentication:basic -SessionOption:$opt -OperationTimeoutSec:90
```

> [!NOTE]
> "Push" mód a felhasználó hitelesítő adatait a gyökér szintű felhasználó a Linux rendszerű számítógépen kell lennie.
> Csak az SSL/TLS-kapcsolatok támogatottak DSC Linux rendszeren a `New-CimSession` – UseSSL paraméter $true értékűre kell használni.
> Az SSL-tanúsítvány által használt OMI (DSC) a fájlban megadott: `/opt/omi/etc/omiserver.conf` a tulajdonságokkal: pemfile és kulcsfájl.
> Ha ez a tanúsítvány nem megbízható által a Windows-számítógép, amely futtatja a [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) parancsmagot, ha szeretné, figyelmen kívül hagyja a tanúsítványok ellenőrzését a CIMSession beállításokkal: `-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`

A következő paranccsal küldje le a DSC-konfiguráció a Linux-csomópont.

`Start-DscConfiguration -Path:"C:\temp" -CimSession:$Sess -Wait -Verbose`

### <a name="distribute-the-configuration-with-a-pull-server"></a>A konfigurációt egy pull-kiszolgálóval

Konfigurációk lehetnek elosztva egy Linux-számítógép egy pull-kiszolgálóval, csakúgy, mint a Windows-számítógépek. Egy lekéréses kiszolgálót használ, tekintse át [Windows PowerShell Desired State Configuration lekéréses kiszolgálók](../pull-server/pullServer.md). További információt és Linux rendszerű számítógépek egy pull-kiszolgálóval kapcsolatos korlátozások: a kibocsátási megjegyzések a Desired State Configuration Linux rendszeren.

### <a name="working-with-configurations-locally"></a>Helyi konfigurációk használata

Linuxhoz készült DSC-szkriptek a helyi számítógépről Linux-konfigurációval is tartalmaz. Ezek a szkriptek keresse meg `/opt/microsoft/dsc/Scripts` és a következőket tartalmazzák:

- GetDscConfiguration.py

Visszaadja az aktuális konfigurációt alkalmazta a számítógépre. A Windows PowerShell-parancsmag hasonló `Get-DscConfiguration` parancsmagot.

`# sudo ./GetDscConfiguration.py`

- GetDscLocalConfigurationManager.py

Az aktuális meta-konfiguráció a számítógépen alkalmazott adja vissza. A parancsmag hasonló [Get-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) parancsmagot.

`# sudo ./GetDscLocalConfigurationManager.py`

- InstallModule.py

Egy egyéni DSC-resource modul telepítése. A modul megosztott objektumtár tartalmazó .zip fájl és a séma MOF-fájlok elérési útja szükséges.

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

- RemoveModule.py

Eltávolít egy egyéni DSC-erőforrás modult. A név egyben a modul eltávolítása szükséges.

`# sudo ./RemoveModule.py cnx_Resource`

- StartDscLocalConfigurationManager.py

A konfigurációs MOF-fájlt a számítógépre vonatkozik. Hasonló a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot. A konfiguráció alkalmazásához MOF elérési útja szükséges.

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

- SetDscLocalConfigurationManager.py

Meta konfigurációs MOF-fájlt a számítógépre vonatkozik. Hasonló a [Set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) parancsmagot. A alkalmazni Meta konfigurációs MOF elérési útja szükséges.

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## <a name="powershell-desired-state-configuration-for-linux-log-files"></a>PowerShell Desired State Configuration for Linux-naplófájlok

A következő naplófájlokat Linux üzenetek DSC jön létre.

|Naplófájl|Könyvtár|Leírás|
|---|---|---|
|**omiserver.log**|`/var/opt/omi/log`|Az OMI a CIM-kiszolgáló működésével kapcsolatos üzenetek.|
|**dsc.log**|`/var/opt/omi/log`|A helyi Configuration Manager (LCM) Konfigurálása és a DSC-erőforrás műveletek működésével kapcsolatos üzenetek.|
