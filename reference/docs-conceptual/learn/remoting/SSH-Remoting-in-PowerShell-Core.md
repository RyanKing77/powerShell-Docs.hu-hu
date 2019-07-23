---
title: PowerShell távoli eljáráshívás SSH-n keresztül
description: Távoli eljáráshívás a PowerShell Core-ban SSH használatával
ms.date: 08/14/2018
ms.openlocfilehash: d994a3888b9a372b803a65666634775a8905d63a
ms.sourcegitcommit: 118eb294d5a84a772e6449d42a9d9324e18ef6b9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/22/2019
ms.locfileid: "68372147"
---
# <a name="powershell-remoting-over-ssh"></a>PowerShell távoli eljáráshívás SSH-n keresztül

## <a name="overview"></a>Áttekintés

A PowerShell távelérés általában a WinRM szolgáltatást használja a kapcsolatok egyeztetéséhez és az adatátvitelhez. Az SSH mostantól elérhető Linux és Windows platformokon, és lehetővé teszi a valódi többplatformos PowerShell-távelérést.

A WinRM robusztus üzemeltetési modellt biztosít a PowerShell távoli munkameneteihez. Az SSH-alapú távelérés jelenleg nem támogatja a távoli végpont-konfigurációt és a JEA (elég felügyelet).

Az SSH távoli eljáráshívás lehetővé teszi a Windows és Linux rendszerű gépek közötti alapszintű PowerShell-munkamenetek elvégzését. Az SSH távelérés egy PowerShell-gazdagépet hoz létre a célszámítógépen SSH alrendszerként. Végül a WinRM-hez hasonló általános üzemeltetési modellt fogunk megvalósítani a végpont-konfiguráció és a JEA támogatásához.

A `New-PSSession`, `Enter-PSSession`a és`Invoke-Command` a parancsmagok mostantól új paraméterrel rendelkeznek az új távelérési kapcsolatok támogatásához.

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

Távoli munkamenet létrehozásához adja meg a cél gépet `HostName` a paraméterrel, és adja meg a felhasználónevet `UserName`a következővel:. A parancsmagok interaktív futtatásakor a rendszer jelszót kér. Az `KeyFilePath` SSH-kulcsos hitelesítést a paraméterrel rendelkező titkos kulcsfájl használatával is használhatja.

## <a name="general-setup-information"></a>Általános telepítési információk

Az SSH-t az összes gépen telepíteni kell. Telepítse az SSH-ügyfelet`ssh.exe`() és a`sshd.exe`kiszolgálót () is, hogy a gépekről és a számítógépekről is legyen távoli. A Windowshoz készült OpenSSH mostantól elérhető a Windows 10 Build 1809 és a Windows Server 2019 rendszerben. További információ: [OpenSSH for Windows](/windows-server/administration/openssh/openssh_overview). Linux esetén telepítse a platformnak megfelelő SSH-t (beleértve az sshd-kiszolgálót is). Telepítenie kell a PowerShell Core-t is a GitHubról az SSH távelérési szolgáltatásának beszerzéséhez. Az SSH-kiszolgálót úgy kell konfigurálni, hogy hozzon létre egy SSH-alrendszert a távoli gépen futó PowerShell-folyamat futtatásához. Emellett konfigurálnia kell a jelszó vagy a kulcs alapú hitelesítés engedélyezését is.

## <a name="set-up-on-windows-machine"></a>Beállítás Windows rendszerű gépen

1. A [PowerShell Core for Windows](../../install/installing-powershell-core-on-windows.md#msi) legújabb verziójának telepítése

   - Megtudhatja, hogy rendelkezik-e az SSH távelérési támogatással a következő paraméterekkel:`New-PSSession`

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. Telepítse a legújabb Win32 OpenSSH-t. A telepítési utasításokért lásd: [az OpenSSH telepítése](/windows-server/administration/openssh/openssh_install_firstuse).
3. Szerkessze `sshd_config` a következő helyen `$env:ProgramData\ssh`található fájlt:.

   - Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > Hiba történt a Windows OpenSSH-ban, amely megakadályozza, hogy a szóközök nem működnek az alrendszer végrehajtható fájljainak elérési útjain. További információkért tekintse meg [ezt a GitHub-problémát](https://github.com/PowerShell/Win32-OpenSSH/issues/784).

     Az egyik megoldás egy olyan symlink létrehozása a PowerShell telepítési könyvtárához, amely nem rendelkezik szóközökkel:

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6"
     ```

     majd írja be az alrendszerbe:

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - Kulcsos hitelesítés opcionális engedélyezése

     ```
     PubkeyAuthentication yes
     ```

4. Az sshd szolgáltatás újraindítása

   ```powershell
   Restart-Service sshd
   ```

5. Adja meg az elérési utat, ahol az OpenSSH telepítve van a PATH környezeti változóba. Például: `C:\Program Files\OpenSSH\`. Ez a bejegyzés lehetővé teszi az SSH. exe megkeresését.

## <a name="set-up-on-linux-ubuntu-1604-machine"></a>Beállítás Linux (Ubuntu 16,04) rendszerű gépen

1. Telepítse a legújabb [PowerShell Core for Linux](../../install/installing-powershell-core-on-linux.md#ubuntu-1604) buildet a githubról
2. [Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html) telepítése igény szerint

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. A sshd_config-fájl szerkesztése a következő helyen:/etc/ssh

   - Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van

   ```
   PasswordAuthentication yes
   ```

   - PowerShell alrendszer bejegyzésének hozzáadása

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - Kulcsos hitelesítés opcionális engedélyezése

   ```
   PubkeyAuthentication yes
   ```

4. Az sshd szolgáltatás újraindítása

   ```bash
   sudo service sshd restart
   ```

## <a name="set-up-on-macos-machine"></a>Beállítás MacOS rendszerű gépen

1. A legújabb [PowerShell-mag telepítése MacOS](../../install/installing-powershell-core-on-macos.md) -buildhez

   - Győződjön meg arról, hogy az SSH távelérés engedélyezve van a következő lépések végrehajtásával:
     - Nyissa meg`System Preferences`
     - Kattintson a`Sharing`
     - Be `Remote Login` kell mondani`Remote Login: On`
     - A megfelelő felhasználók hozzáférésének engedélyezése

2. A fájl `sshd_config` szerkesztése a helyen`/private/etc/ssh/sshd_config`

   - Használja kedvenc szerkesztőjét vagy

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van

     ```
     PasswordAuthentication yes
     ```

   - PowerShell alrendszer bejegyzésének hozzáadása

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - Kulcsos hitelesítés opcionális engedélyezése

     ```
     PubkeyAuthentication yes
     ```

3. Az sshd szolgáltatás újraindítása

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="authentication"></a>Hitelesítés

A PowerShell távoli SSH-kapcsolaton keresztüli hitelesítése az SSH-ügyfél és az SSH-szolgáltatás közötti hitelesítési Exchange-re támaszkodik, és nem valósít meg saját hitelesítési sémákat. Ez azt jelenti, hogy minden konfigurált hitelesítési sémát, beleértve a többtényezős hitelesítést, az SSH és a PowerShelltől függetlenül kezeli. Beállíthatja például, hogy az SSH szolgáltatás nyilvános kulcsú hitelesítésre, valamint egy egyszeri jelszóra legyen szükség a további biztonság érdekében. A többtényezős hitelesítés konfigurációja kívül esik a dokumentáció hatókörén. A többtényezős hitelesítés helyes konfigurálásához és a PowerShellen kívüli működésének ellenőrzéséhez tekintse meg az SSH dokumentációját, mielőtt a PowerShell távelérési szolgáltatással próbálja használni.

## <a name="powershell-remoting-example"></a>PowerShell-távelérés – példa

A távelérés tesztelésének legegyszerűbb módja, ha egyetlen gépen próbálja ki. Ebben a példában egy távoli munkamenetet hozunk létre ugyanarra a Linux-gépre. A PowerShell-parancsmagokat interaktívan használjuk, ezért a rendszer kéri az SSH-t, hogy ellenőrizze a gazdaszámítógép ellenőrzését és a jelszó megadását. Ugyanezt megteheti a Windows rendszerű gépen is a távelérés működésének biztosításához. Ezután a gépek közötti távoli kapcsolat megváltoztatásával adja meg a gazdagép nevét.

```powershell
#
# Linux to Linux
#
$session = New-PSSession -HostName UbuntuVM1 -UserName TestUser
```

```output
The authenticity of host 'UbuntuVM1 (9.129.17.107)' cannot be established.
ECDSA key fingerprint is SHA256:2kCbnhT2dUE6WCGgVJ8Hyfu1z2wE4lifaJXLO7QJy0Y.
Are you sure you want to continue connecting (yes/no)?
TestUser@UbuntuVM1s password:
```

```powershell
$session
```

```output
 Id Name   ComputerName    ComputerType    State    ConfigurationName     Availability
 -- ----   ------------    ------------    -----    -----------------     ------------
  1 SSH1   UbuntuVM1       RemoteMachine   Opened   DefaultShell             Available
```

```powershell
Enter-PSSession $session
```

```output
[UbuntuVM1]: PS /home/TestUser> uname -a
Linux TestUser-UbuntuVM1 4.2.0-42-generic 49~16.04.1-Ubuntu SMP Wed Jun 29 20:22:11 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

[UbuntuVM1]: PS /home/TestUser> Exit-PSSession
```

```powershell
Invoke-Command $session -ScriptBlock { Get-Process powershell }
```

```output
Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName                    PSComputerName
-------  ------    -----      -----     ------     --  -- -----------                    --------------
      0       0        0         19       3.23  10635 635 powershell                     UbuntuVM1
      0       0        0         21       4.92  11033 017 powershell                     UbuntuVM1
      0       0        0         20       3.07  11076 076 powershell                     UbuntuVM1
```

```powershell
#
# Linux to Windows
#
Enter-PSSession -HostName WinVM1 -UserName PTestName
```

```output
PTestName@WinVM1s password:
```

```powershell
[WinVM1]: PS C:\Users\PTestName\Documents> cmd /c ver
```

```output
Microsoft Windows [Version 10.0.10586]
```

```powershell
#
# Windows to Windows
#
C:\Users\PSUser\Documents>pwsh.exe
```

```output
PowerShell
Copyright (c) Microsoft Corporation. All rights reserved.
```

```powershell
$session = New-PSSession -HostName WinVM2 -UserName PSRemoteUser
```

```output
The authenticity of host 'WinVM2 (10.13.37.3)' can't be established.
ECDSA key fingerprint is SHA256:kSU6slAROyQVMEynVIXAdxSiZpwDBigpAF/TXjjWjmw.
Are you sure you want to continue connecting (yes/no)?
Warning: Permanently added 'WinVM2,10.13.37.3' (ECDSA) to the list of known hosts.
PSRemoteUser@WinVM2's password:
```

```powershell
$session
```

```output
 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            WinVM2          RemoteMachine   Opened        DefaultShell             Available
```

```powershell
Enter-PSSession -Session $session
```

```output
[WinVM2]: PS C:\Users\PSRemoteUser\Documents> $PSVersionTable

Name                           Value
----                           -----
PSEdition                      Core
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
SerializationVersion           1.1.0.1
BuildVersion                   3.0.0.0
CLRVersion
PSVersion                      6.0.0-alpha
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
GitCommitId                    v6.0.0-alpha.17


[WinVM2]: PS C:\Users\PSRemoteUser\Documents>
```

### <a name="known-issues"></a>Ismert problémák

A sudo parancs nem működik a távoli munkamenetben a Linux rendszerű gépeken.

## <a name="see-also"></a>Lásd még:

[Windows PowerShell Core](../../install/installing-powershell-core-on-windows.md#msi)

[A Linux PowerShell-magja](../../install/installing-powershell-core-on-linux.md#ubuntu-1604)

[A MacOS-hez készült PowerShell Core](../../install/installing-powershell-core-on-macos.md)

[Windowsos OpenSSH](/windows-server/administration/openssh/openssh_overview)

[Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html)
