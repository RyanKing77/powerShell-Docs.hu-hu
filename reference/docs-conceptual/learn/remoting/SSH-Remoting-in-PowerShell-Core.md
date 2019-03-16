---
title: PowerShell távoli eljáráshívás SSH-n keresztül
description: Távoli eljáráshívás a PowerShell Core SSH-val
ms.date: 08/14/2018
ms.openlocfilehash: 1d7bcb69c7e784bf745cb5c2633106ea53f6226a
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58056532"
---
# <a name="powershell-remoting-over-ssh"></a>PowerShell távoli eljáráshívás SSH-n keresztül

## <a name="overview"></a>Áttekintés

PowerShell távoli eljáráshívás általában winrm funkciót használ a kapcsolat egyeztetési és adatátvitel. Az SSH Linux és Windows platformokon elérhető, és lehetővé teszi a valódi többplatformos PowerShell távoli eljáráshívás.

A Rendszerfelügyeleti webszolgáltatások egy robusztus üzemeltetési modellt biztosít a távoli PowerShell-munkamenetet. Távoli eljáráshívás SSH-alapú jelenleg nem támogatja a távoli végpont-konfiguráció és a JEA (Just Enough Administration).

Az SSH a távelérés lehetővé teszi egyszerű PowerShell-munkamenet távelérés Windows és Linux gép között. SSH távoli eljáráshívás hoz létre, mint egy SSH-alrendszer egy PowerShell gazdafolyamat a célgépen.
Végül hoznunk egy általános üzemeltetési modell, a Rendszerfelügyeleti webszolgáltatások, a végpont-konfiguráció és a JEA hasonló lesz.

A `New-PSSession`, `Enter-PSSession`, és `Invoke-Command` parancsmagok most már támogatja az új távelérési kapcsolat új paramétert.

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

Hozzon létre egy távoli munkamenetet, adja meg a célszámítógépen a `HostName` paramétert, és adja meg a felhasználónevet, `UserName`. Amikor interaktívan futtatja a parancsmagok, kéri a jelszót. Emellett, a titkos kulcsfájl használata SSH kulcsos hitelesítést a `KeyFilePath` paraméter.

## <a name="general-setup-information"></a>Általános beállítási adatok

SSH minden gépen telepítve kell lennie. Mindkét az SSH-ügyfél telepítése (`ssh.exe`) és a kiszolgáló (`sshd.exe`) segítségével távoli, és onnan a gépek. Az OpenSSH for Windows már rendelkezésre álló, a Windows 10-es build 1809 és a Windows Server 2019. További információkért lásd: [OpenSSH for Windows](/windows-server/administration/openssh/openssh_overview). A Linux telepítse az SSH (beleértve sshd-kiszolgálót) a platformjának megfelelő. Emellett telepítenie kell a PowerShell Core a Githubról, a távoli eljáráshívás SSH szolgáltatás beolvasása. Az SSH-kiszolgálót úgy kell konfigurálni, egy SSH-alrendszer üzemeltetéséhez a távoli gépen egy PowerShell-folyamat létrehozásához. Emellett konfigurálnia kell jelszó engedélyezése vagy kulcs alapú hitelesítés.

## <a name="set-up-on-windows-machine"></a>Windows-gépen beállítása

1. Telepítse a legújabb verzióját, [a Windows PowerShell Core](../../install/installing-powershell-core-on-windows.md#msi)

   - Is megadhatja, hogy a távoli eljáráshívás SSH-támogatás, ha megnézzük a paraméterkészletek számára `New-PSSession`

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. Telepítse a legújabb Win32-OpenSSH. A telepítési utasításokért lásd: [telepítési az OpenSSH](/windows-server/administration/openssh/openssh_install_firstuse).
3. Szerkessze a `sshd_config` helyen található fájl `$env:ProgramData\ssh`.

   - Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > Az OpenSSH a Windows, amely megakadályozza, hogy a tárolóhelyek alrendszer végrehajtható elérési utak használata programhiba van. További információkért lásd: [a GitHub-problémát](https://github.com/PowerShell/Win32-OpenSSH/issues/784).

     Az egyik megoldás, a PowerShell telepítési könyvtárát, amely nem rendelkezik a tárolóhelyek szimbolikus létrehozásához:

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6"
     ```

     és a alrendszer írja be:

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - Igény szerint a kulcs alapú hitelesítés engedélyezése

     ```
     PubkeyAuthentication yes
     ```

4. Indítsa újra az sshd szolgáltatást

   ```powershell
   Restart-Service sshd
   ```

5. Adja hozzá az elérési útját a Path környezeti változóba OpenSSH helyéül. Például: `C:\Program Files\OpenSSH\`. Ez a bejegyzés lehetővé teszi a ssh.exe is meg lehet találni.

## <a name="set-up-on-linux-ubuntu-1404-machine"></a>Állítsa be a Linux (Ubuntu 14.04) gépen

1. Telepítse a legújabb [PowerShell Core for Linux](../../install/installing-powershell-core-on-linux.md#ubuntu-1404) létrehozása a Githubról
2. Telepítés [Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html) igény szerint

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. Az sshd_config fájlban a következő helyen /etc/ssh szerkesztése

   - Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés

   ```
   PasswordAuthentication yes
   ```

   - PowerShell alrendszer bejegyzés hozzáadása

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - Igény szerint a kulcs alapú hitelesítés engedélyezése

   ```
   PubkeyAuthentication yes
   ```

4. Indítsa újra az sshd szolgáltatást

   ```bash
   sudo service sshd restart
   ```

## <a name="set-up-on-macos-machine"></a>Állítsa be a MacOS rendszerű gépén

1. Telepítse a legújabb [MacOS-hez a PowerShell Core](../../install/installing-powershell-core-on-macos.md) összeállítása

   - Győződjön meg arról, hogy SSH-távelérés engedélyezve van az alábbi lépéseket:
     - Nyissa meg a `System Preferences`
     - Kattintson a `Sharing`
     - Ellenőrizze `Remote Login` – a következő: `Remote Login: On`
     - Megfelelő felhasználók férhessenek hozzá

2. Szerkessze a `sshd_config` helyen található fájl `/private/etc/ssh/sshd_config`

   - Használja kedvenc szerkesztőjében, vagy

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés

     ```
     PasswordAuthentication yes
     ```

   - PowerShell alrendszer bejegyzés hozzáadása

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - Igény szerint a kulcs alapú hitelesítés engedélyezése

     ```
     PubkeyAuthentication yes
     ```

3. Indítsa újra az sshd szolgáltatást

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="authentication"></a>Hitelesítés

PowerShell távoli eljáráshívás ssh-n keresztül az SSH-ügyfél és az SSH-szolgáltatást között a hitelesítési csere támaszkodik, és nem valósítja meg a hitelesítési sémát magát.
Ez azt jelenti, hogy többek között a multi-factor authentication szolgáltatáshoz beállított hitelesítési sémát az SSH és PowerShell függetlenül történik.
Például konfigurálhatja a nyilvános kulcsos hitelesítés, valamint az egyszeri jelszó megkövetelése a fokozott biztonság az SSH-szolgáltatást.
A multi-factor authentication konfigurálása az ebben a dokumentációban hatókörén kívül számára.
Hogyan kell megfelelően multi-factor authentication konfigurálásához, és a PowerShell-en kívül működik, a PowerShell-táveléréssel használata előtt az SSH számára dokumentációban tájékozódhat.

## <a name="powershell-remoting-example"></a>Távoli eljáráshívás a PowerShell-példa

A legegyszerűbb módon távelérésének lehetővé tétele, hogy egyetlen gépen kipróbálására. Ebben a példában létrehozunk egy távoli munkamenetet vissza ugyanaz a Linux rendszerű gép. PowerShell-parancsmagok interaktív módon, így láthatjuk, kérni fogja az SSH kéri ellenőrzése a gazdaszámítógépen, és a jelszót kérő üzenet használjuk. Megteheti ugyanezt egy Windows-gépen annak érdekében, hogy működik a távoli eljáráshívás. Aztán távoli állomásnév módosításával gépek között.

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
Linux TestUser-UbuntuVM1 4.2.0-42-generic 49~14.04.1-Ubuntu SMP Wed Jun 29 20:22:11 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

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

A sudo parancs nem működik a távoli munkamenet Linux rendszerű gépen.

## <a name="see-also"></a>Lásd még:

[A Windows PowerShell Core](../../install/installing-powershell-core-on-windows.md#msi)

[A PowerShell Core linuxhoz](../../install/installing-powershell-core-on-linux.md#ubuntu-1404)

[MacOS-hez a PowerShell Core](../../install/installing-powershell-core-on-macos.md)

[A Windows OpenSSH](/windows-server/administration/openssh/openssh_overview)

[Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html)
