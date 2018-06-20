---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A kívánt állapot konfigurációs szolgáltatása (DSC) első lépései Linux rendszeren
ms.openlocfilehash: 0534cede979eb2917adb608dba622539fe4bdc45
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189431"
---
# <a name="get-started-with-desired-state-configuration-dsc-for-linux"></a>A kívánt állapot konfigurációs szolgáltatása (DSC) első lépései Linux rendszeren

Ez a témakör ismerteti, hogyan Linux PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) az első lépéseiben. A DSC kapcsolatos általános információkért lásd: [Ismerkedés a Windows PowerShell célállapot-konfiguráció](overview.md).

## <a name="supported-linux-operation-system-versions"></a>Támogatott Linux művelet-verziók

A következő Linux operációsrendszer-verziók DSC Linux támogatottak.
- CentOS 5, 6 és 7 (x86/x64)
- Debian GNU/Linux 6, 7, 8 (x86/x64)
- Oracle Linux 5, 6, 7 (x86/x64)
- Red Hat Enterprise Linux Server 5, 6, 7 (x86/x64)
- SUSE Linux Enterprise Server 10, 11, 12 (x86/x64)
- Ubuntu Server 12.04 LTS, 14.04 LTS és 16.04 LTS (x86/x64)

A következő táblázat ismerteti a szükséges csomagfüggőségek Linux a DSC-ből.

|  Szükséges csomag |  Leírás |  Minimális verzió |
|---|---|---|
| Glibc| GNU könyvtár| 2... 4 – 31.30|
| Python| Python| 2.4 – 3.4|
| omiserver| Nyílt kezelési infrastruktúra| 1.0.8.1|
| Openssl| OpenSSL-függvénytárak| 0.9.8-as vagy 1.0|
| ctypes| Python CTypes könyvtár| Meg kell egyeznie a Python-verzió|
| libcurl| cURL http ügyféloldali kódtár| 7.15.1|

## <a name="installing-dsc-for-linux"></a>A Linux DSC telepítése

Telepítenie kell a [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) Linux DSC telepítése előtt.

### <a name="installing-omi"></a>OMI telepítése

Állapotkonfiguráció szükséges Linux ír elő az Open Management Infrastructure (OMI) CIM-kiszolgáló, 1.0.8.1 verzió vagy újabb. OMI tölthető le: az Open Group: [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi).

OMI telepítéséhez telepítse a csomagot, amely megfelel a Linux rendszer (.rpm vagy .deb) és a OpenSSL-verzió (ssl_098 vagy ssl_100) és az architektúra (x64/x86). RPM csomagok CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server és Oracle Linux alkalmasak. DEB-csomagokat a Debian GNU/Linux és Ubuntu Server alkalmasak. A ssl_098 csomagok megfelelőek OpenSSL telepítve, miközben az OpenSSL 1.0 telepítve olyan számítógépek a ssl_100 csomagok 0.9.8-as rendelkező számítógépek.

> **Megjegyzés:**: a parancs futtatásával határozza meg a telepített OpenSSL-verzió, `openssl version`.

A következő paranccsal telepíthető OMI CentOS 7 x64 rendszeren.

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### <a name="installing-dsc"></a>A DSC telepítése

Linux DSC érhető el a letöltési [Itt](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/latest).

A DSC telepítéséhez telepítse a csomagot, amely megfelel a Linux rendszer (.rpm vagy .deb) és a OpenSSL-verzió (ssl_098 vagy ssl_100) és az architektúra (x64/x86). RPM csomagok CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server és Oracle Linux alkalmasak. DEB-csomagokat a Debian GNU/Linux és Ubuntu Server alkalmasak. A ssl_098 csomagok megfelelőek OpenSSL telepítve, miközben az OpenSSL 1.0 telepítve olyan számítógépek a ssl_100 csomagok 0.9.8-as rendelkező számítógépek.

> **Megjegyzés:**: annak meghatározásához, a telepített OpenSSL-verzió, a parancs openssl verzióját futtatják.

A következő paranccsal telepíthető DSC CentOS 7 x64 rendszeren.

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`


## <a name="using-dsc-for-linux"></a>A DSC használata Linux rendszeren

Az alábbi szakaszok ismertetik, hogyan hozhat létre és futtathat a DSC-konfigurációk a Linux rendszerű számítógépeken.

### <a name="creating-a-configuration-mof-document"></a>Konfigurációs MOF dokumentumok létrehozása

A Windows PowerShell-konfiguráció kulcsszó létrehozásához használt Linux rendszerű számítógépek konfigurációját hasonlóan a Windows rendszerű számítógépeken. A következő lépések azt mutatják be, a Windows PowerShell használatával Linux számítógép konfigurációs dokumentum létrehozása.

1. A nx modul importálása. Nx Windows PowerShell-modul tartalmaz az a séma beépített erőforrások DSC Linux, és telepítve legyen a helyi számítógépen, és importálja a konfigurációban.

    -A nx modul telepítése, másolja a nx modulkönyvtárat vagy `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` vagy `$PSHOME\Modules`. A nx modul tartalmazza a DSC Linux-telepítési csomag (MSI). A nx moduljának a konfiguráció importálásához használja a __Import-DSCResource__ parancs:

```powershell
Configuration ExampleConfiguration{

    Import-DSCResource -Module nx

}
```
2. A konfiguráció és a konfigurációs dokumentum létrehozása:

```powershell
Configuration ExampleConfiguration{

    Import-DscResource -Module nx

    Node  "linuxhost.contoso.com"{
    nxFile ExampleFile {

        DestinationPath = "/tmp/example"
        Contents = "hello world `n"
        Ensure = "Present"
        Type = "File"
    }

    }
}
ExampleConfiguration -OutputPath:"C:\temp"
```

### <a name="push-the-configuration-to-the-linux-computer"></a>A konfigurációs leküldése a Linux rendszerű számítógép

Konfigurációs dokumentumok (MOF-fájlok) a Linux rendszerű számítógépen történő továbbíthatja a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag. Ahhoz, hogy ez a parancsmag, valamint a [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx), vagy [teszt-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) parancsmagok távolról a Linux-számítógép segítségével kell egy CIMSession. A [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) parancsmag segítségével hozzon létre egy CIMSession Linux rendszerű számítógép.

A következő kód bemutatja, hogyan hozzon létre egy CIMSession DSC Linux.

```powershell
$Node = "ostc-dsc-01"
$Credential = Get-Credential -UserName:"root" -Message:"Enter Password:"

#Ignore SSL certificate validation
#$opt = New-CimSessionOption -UseSsl:$true -SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true

#Options for a trusted SSL certificate
$opt = New-CimSessionOption -UseSsl:$true
$Sess=New-CimSession -Credential:$credential -ComputerName:$Node -Port:5986 -Authentication:basic -SessionOption:$opt -OperationTimeoutSec:90
```

> **Megjegyzés:**:
* Az "Push" módban a felhasználó hitelesítő adatainak a gyökér szintű felhasználó a Linux rendszerű számítógépen kell lennie.
* A Linux, a New-CimSession együtt kell használni a – UseSSL paraméter $true DSC csak SSL/TLS kapcsolatok támogatottak.
* Az SSL-tanúsítvány által használt OMI (DSC) a fájlban megadott: `/opt/omi/etc/omiserver.conf` a tulajdonságokkal: pemfile és keyfile.
Ha ez a tanúsítvány nem megbízható által a Windows-számítógép, amely futtatja a [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) parancsmagot, ha szeretné, figyelmen kívül hagyja a CIMSession beállításokkal tanúsítvány érvényesítése: `-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`

A következő parancsot a DSC-konfiguráció leküldése a Linux-csomópont.

`Start-DscConfiguration -Path:"C:\temp" -CimSession:$Sess -Wait -Verbose`

### <a name="distribute-the-configuration-with-a-pull-server"></a>A lekérési kiszolgálójával a konfiguráció terjesztése

Konfigurációk is terjeszthetők a Linux-számítógép lekéréses kiszolgálóval, csakúgy, mint a Windows rendszerű számítógépeken. A lekérési kiszolgálójával használatával útmutatóért lásd: [Windows PowerShell kívánt állapot konfigurációs lekéréses kiszolgálók](pullServer.md). További információért és Linux számítógépeket használ egy lekéréses-kiszolgálóval kapcsolatos korlátozások tekintse meg a kibocsátási megjegyzéseket a célállapot-konfiguráció Linux.

### <a name="working-with-configurations-locally"></a>Helyileg konfigurációk használata

Linux DSC tartalmaz a helyi Linux számítógép-konfiguráció használható parancsfájlokat. Ezek a parancsfájlok keresse meg `/opt/microsoft/dsc/Scripts` és adja meg a következőket:
* GetDscConfiguration.py

 A jelenlegi konfiguráció a számítógépen alkalmazott adja vissza. Hasonló a Windows PowerShell-parancsmag Get-DscConfiguration parancsmagnak.

`# sudo ./GetDscConfiguration.py`

* GetDscLocalConfigurationManager.py

 Visszaadja a jelenlegi metaadat-konfiguráció alkalmazni a számítógépen. A parancsmag hasonló [Get-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx) parancsmag.

`# sudo ./GetDscLocalConfigurationManager.py`

* InstallModule.py

 Egy egyéni DSC erőforrás modult telepít. A modul megosztott objektumtár tartalmazó .zip fájl és a séma MOF-fájlok elérési útja van szükség.

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

* RemoveModule.py

 Eltávolít egy egyéni DSC erőforrás modult. Eltávolítja a modul neve igényel.

`# sudo ./RemoveModule.py cnx_Resource`

* StartDscLocalConfigurationManager.py

 A számítógép érvényes konfigurációs MOF-fájlt. Hasonló a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag. A konfiguráció alkalmazásához MOF elérési igényel.

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

* SetDscLocalConfigurationManager.py

 A számítógép érvényes Meta konfigurációs MOF-fájlt. Hasonló a [Set-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx) parancsmag. Elérési útját a Meta konfigurációs MOF alkalmazásához szükséges.

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## <a name="powershell-desired-state-configuration-for-linux-log-files"></a>PowerShell kívánt állapot konfigurációs Linux-naplófájlok

A következő naplófájlokba Linux üzenetek DSC jön létre.

|Naplófájl|Könyvtár|Leírás|
|---|---|---|
|omiserver.log|/var/OPT/OMI/log|Az OMI a CIM-kiszolgáló működésével kapcsolatos üzeneteket.|
|DSC.log|/var/OPT/OMI/log|A helyi Configuration Manager (LCM) és a DSC erőforrás műveletek működésével kapcsolatos üzeneteket.|