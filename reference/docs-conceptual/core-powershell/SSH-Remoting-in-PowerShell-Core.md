# <a name="powershell-remoting-over-ssh"></a>PowerShell távoli eljáráshívás SSH-n keresztül

## <a name="overview"></a>Áttekintés

PowerShell távvezérlése általában használ Rendszerfelügyeleti webszolgáltatások kapcsolat egyeztetéshez, és az adatok átvitel.
SSH a távoli eljáráshívás megvalósításával lett választva, mert Linux és a Windows platformokhoz érhető el, és lehetővé teszi, hogy igaz többplatformos PowerShell távoli eljáráshívás.
Azonban a Rendszerfelügyeleti webszolgáltatások is biztosít egy robusztus üzemeltetési modell PowerShell távoli munkamenetek, amelyek ebben az implementációban még nem.
És ez azt jelenti, hogy PowerShell távoli végpont-konfiguráció és a JEA (csak elég felügyeleti) jelenleg nem támogatott ebben az implementációban.

PowerShell SSH távoli eljáráshívás lehetővé teszi alapszintű PowerShell-munkamenet távelérés Windows és Linux rendszerű számítógép között.
Ez a folyamat a célszámítógépen, egy SSH-alrendszer üzemeltető PowerShell létrehozásával történik.
Végül ez módosulnak hasonlóak a Rendszerfelügyeleti webszolgáltatások működése érdekében támogatja a végpont-konfiguráció és a JEA általánosabb üzemeltetési modellre.

A New-PSSession, Enter-PSSession és Invoke-Command-parancsmagok most már rendelkezik egy új paraméter lehetővé teszi a távoli eljáráshívás új kapcsolat beállítása

```powershell
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

Az új paraméterkészletet alakítanak valószínűleg változik, de most hozhat létre SSH PSSession, hogy a parancssorból kezelésére, és meghívni parancsaiban és parancsfájljaiban.
Adja meg a célszámítógépen az állomásnév paraméterrel, és adjon meg a felhasználónevet használva.
A parancsmag párbeszédes formában történő futtatásakor a PowerShell-parancssorból kéri a jelszót.
De lehetősége is van SSH hitelesítés használatára, majd adjon meg egy titkos kulcsot tartalmazó fájlt elérési utat a KeyFilePath paraméterrel.

## <a name="general-setup-information"></a>Általános telepítési információk

Az SSH egy minden gépen kell telepíteni.
Telepíteni kell (ssh.exe) ügyfélen és kiszolgálón (sshd.exe) is, hogy a gépek és a távelérés kísérletezhet.
A Windows rendszer telepítendő [Win32 OpenSSH a Githubról](https://github.com/PowerShell/Win32-OpenSSH/releases).
Linux kell telepíteni kell a platform (többek között a következőket sshd kiszolgáló) SSH.
Konfigurálnia kell a legutóbbi PowerShell build vagy a csomag a Githubból, hogy az SSH távvezérlési funkció.
SSH-alrendszereket használatos PowerShell folyamatot a távoli számítógépen, és az SSH-kiszolgálót kell konfigurálni, hogy.
Továbbá szüksége lesz jelszóalapú hitelesítés, illetve opcionálisan kulcs alapú hitelesítés engedélyezéséhez.

## <a name="setup-on-windows-machine"></a>A telepítő a Windows-gépen

1. Telepítse a legújabb verzióját [a Windows PowerShell központ]
    - Állapítható meg, ha az SSH-távelérésének jobb támogatása megnézzük a paraméter állandóként állítja be a New-PSSession

    ```powershell
    PS> Get-Command New-PSSession -syntax
    New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
    ```

1. Telepítse a legújabb [Win32 OpenSSH] GitHub használatával felépíteni a [telepítési] utasításokat
1. A Win32 OpenSSH telepítési helyére sshd_config fájl szerkesztése
    - Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van

    ```
    PasswordAuthentication yes
    ```

    - PowerShell alrendszer bejegyzés hozzáadása, cseréje `c:/program files/powershell/6.0.0/pwsh.exe` a helyes elérési útját a használni kívánt verzióra

    ```
    Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
    ```
    
    > [!NOTE]
    Hogy programhiba van a protokoll OpenSSH for Windows, amely megakadályozza, hogy a tárolóhelyek alrendszer végrehajtható elérési utak használata.
    Lásd: [további információt a Githubon probléma](https://github.com/PowerShell/Win32-OpenSSH/issues/784).
    
    Egy megoldás létrehozása a Powershell telepítési könyvtárába, amely nem tartalmaz szóközöket egy symlink:
    
    ```powershell
    mklink /D c:\pwsh "C:\Program Files\PowerShell\6.0.0"
    ```

    és alrendszerben írja be:
 
    ```
    Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
    ```

    - Opcionálisan a hitelesítés engedélyezése

    ```
    PubkeyAuthentication yes
    ```

1. Indítsa újra a sshd szolgáltatást

    ```powershell
    Restart-Service sshd
    ```

1. Az elérési utat, ahol OpenSSH van telepítve az elérési út Env változó hozzáadása
    - Ez a témakörgyűjtemény legyen `C:\Program Files\OpenSSH\`
    - Ez lehetővé teszi a keresett ssh.exe

## <a name="setup-on-linux-ubuntu-1404-machine"></a>Linux (Ubuntu 14.04) gépen beállítása

1. Telepítse a legújabb [PowerShell Core Linux] a Githubról összeállítása
1. Telepítés [Ubuntu SSH] igény szerint

    ```bash
    sudo apt install openssh-client
    sudo apt install openssh-server
    ```

1. A sshd_config fájlban a következő helyen /etc/ssh szerkesztése
    - Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van

    ```
    PasswordAuthentication yes
    ```

    - PowerShell alrendszer bejegyzés hozzáadása

    ```
    Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
    ```

    - Opcionálisan a hitelesítés engedélyezése

    ```
    PubkeyAuthentication yes
    ```

1. Indítsa újra a sshd szolgáltatást

    ```bash
    sudo service sshd restart
    ```

## <a name="setup-on-macos-machine"></a>MacOS gépen beállítása

1. Telepítse a legújabb [MacOS a PowerShell Core] összeállítása
    - Ellenőrizze, hogy engedélyezve van a SSH távelérése az alábbiak szerint:
      - Nyissa meg a `System Preferences`
      - Kattintson a `Sharing`
      - Ellenőrizze `Remote Login` -üzenetnek kell megjelennie `Remote Login: On`
      - Megfelelő felhasználók hozzáférésének engedélyezése
1. Szerkessze a `sshd_config` fájl a következő helyen: `/private/etc/ssh/sshd_config`
    - A kedvenc szerkesztővel vagy

    ```bash
    sudo nano /private/etc/ssh/sshd_config
    ```

    - Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van

    ```
    PasswordAuthentication yes
    ```

    - PowerShell alrendszer bejegyzés hozzáadása

    ```
    Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
    ```

    - Opcionálisan a hitelesítés engedélyezése

    ```
    PubkeyAuthentication yes
    ```

1. Indítsa újra a sshd szolgáltatást

    ```bash
    sudo launchctl stop com.openssh.sshd
    sudo launchctl start com.openssh.sshd
    ```

## <a name="powershell-remoting-example"></a>PowerShell távoli eljáráshívás – példa

A távoli eljáráshívás teszteléséhez legkönnyebben csak egyetlen gépen próbálja.
Itt I hoz létre egy távoli munkamenet az azonos gépre egy Linux-be.
Figyelje meg, hogy PowerShell-parancsmagok egy parancs parancssori futtatásával használom, így azt kéri az SSH ellenőrzése a gazdaszámítógépen, valamint a kért azonosítóadatok kéri.
Ezt megteheti ugyanezt egy Windows számítógép távoli eljáráshívási hiba működik-e, és ezután távoli gép állomásneve egyszerűen módosításával közötti.

```powershell
#
# Linux to Linux
#
PS /home/TestUser> $session = New-PSSession -HostName UbuntuVM1 -UserName TestUser
The authenticity of host 'UbuntuVM1 (9.129.17.107)' cannot be established.
ECDSA key fingerprint is SHA256:2kCbnhT2dUE6WCGgVJ8Hyfu1z2wE4lifaJXLO7QJy0Y.
Are you sure you want to continue connecting (yes/no)?
TestUser@UbuntuVM1s password:

PS /home/TestUser> $session

 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            UbuntuVM1       RemoteMachine   Opened        DefaultShell             Available

PS /home/TestUser> Enter-PSSession $session

[UbuntuVM1]: PS /home/TestUser> uname -a
Linux TestUser-UbuntuVM1 4.2.0-42-generic 49~14.04.1-Ubuntu SMP Wed Jun 29 20:22:11 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux

[UbuntuVM1]: PS /home/TestUser> Exit-PSSession

PS /home/TestUser> Invoke-Command $session -ScriptBlock { Get-Process powershell }

Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName                    PSComputerName
-------  ------    -----      -----     ------     --  -- -----------                    --------------
      0       0        0         19       3.23  10635 635 powershell                     UbuntuVM1
      0       0        0         21       4.92  11033 017 powershell                     UbuntuVM1
      0       0        0         20       3.07  11076 076 powershell                     UbuntuVM1


#
# Linux to Windows
#
PS /home/TestUser> Enter-PSSession -HostName WinVM1 -UserName PTestName
PTestName@WinVM1s password:

[WinVM1]: PS C:\Users\PTestName\Documents> cmd /c ver

Microsoft Windows [Version 10.0.10586]

[WinVM1]: PS C:\Users\PTestName\Documents>

#
# Windows to Windows
#
C:\Users\PSUser\Documents>pwsh.exe
PowerShell
Copyright (c) Microsoft Corporation. All rights reserved.

PS C:\Users\PSUser\Documents> $session = New-PSSession -HostName WinVM2 -UserName PSRemoteUser
The authenticity of host 'WinVM2 (10.13.37.3)' can't be established.
ECDSA key fingerprint is SHA256:kSU6slAROyQVMEynVIXAdxSiZpwDBigpAF/TXjjWjmw.
Are you sure you want to continue connecting (yes/no)?
Warning: Permanently added 'WinVM2,10.13.37.3' (ECDSA) to the list of known hosts.
PSRemoteUser@WinVM2's password:
PS C:\Users\PSUser\Documents> $session

 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            WinVM2          RemoteMachine   Opened        DefaultShell             Available


PS C:\Users\PSUser\Documents> Enter-PSSession -Session $session
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

1. sudo parancs nem működik a távoli munkamenet Linux-számítógép.

[A Windows PowerShell központ]: ../setup/installing-powershell-core-on-windows.md#msi
[PowerShell Core Linux]: ../setup/installing-powershell-core-on-linux.md#ubuntu-1404
[MacOS a PowerShell Core]: ../setup/installing-powershell-core-on-macos.md
[Win32 OpenSSH]: https://github.com/PowerShell/Win32-OpenSSH/releases
[telepítési]: https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH
[Ubuntu SSH]: https://help.ubuntu.com/lts/serverguide/openssh-server.html
