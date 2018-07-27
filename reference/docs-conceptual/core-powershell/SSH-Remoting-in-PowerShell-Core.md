
# <a name="powershell-remoting-over-ssh"></a>PowerShell távoli eljáráshívás SSH-n keresztül

## <a name="overview"></a>Áttekintés

PowerShell távoli eljáráshívás általában winrm funkciót használ a kapcsolat egyeztetési és adatátvitel. SSH a távoli eljáráshívás megvalósítási lett választva, mert már Linux és Windows platformokon elérhető, és lehetővé teszi, hogy igaz többplatformos PowerShell távoli eljáráshívás. Azonban a Rendszerfelügyeleti webszolgáltatások is biztosít egy robusztus üzemeltetési modell PowerShell távoli munkamenetek, amelyek ezt a megvalósítást még nem teszi. És ez azt jelenti, hogy PowerShell távoli végpont-konfiguráció és a JEA (Just Enough Administration) még nem támogatott a végrehajtása során.

PowerShell SSH távelérés lehetővé teszi egyszerű PowerShell-munkamenet távelérés Windows és Linux gép között. Ez történik, egy PowerShell-folyamat a célgépen, mint egy SSH-alrendszer üzemeltető létrehozásával. Végül ez fog módosítható, hasonlóan ahhoz, hogy támogatja a végpont-konfiguráció és a JEA WinRM működése általános üzemeltetési modell.

A `New-PSSession`, `Enter-PSSession` és `Invoke-Command` parancsmagok most már rendelkezik egy új paraméter megkönnyítése érdekében a távoli eljáráshívás új kapcsolat beállítása

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

Az új paraméterkészlet valószínűleg változni fognak, de egyelőre lehetővé teszi, hogy hozzon létre SSH PSSessions, hogy kommunikáljanak a parancssorból, vagy a parancsok és szkriptek invoke. A HostName paraméter adja meg a célgépen, és adja meg a felhasználónevet a felhasználónévvel. Amikor interaktívan futtatja a parancsmagok a PowerShell-parancssorból, a rendszer kéri, a jelszót. De lehetősége is van az SSH-kulcsos hitelesítést, és adja meg a titkos kulcsfájl elérési útja a KeyFilePath paraméterrel.

## <a name="general-setup-information"></a>Általános beállítási adatok

SSH szükség minden gépen telepíthető. Telepítenie kell a mindkét-ügyfelet (`ssh.exe`) és a kiszolgáló (`sshd.exe`), hogy a távoli eljáráshívás irányuló és onnan a gépek kísérletezhet. A Windows, telepítenie kell [a Githubról történő Win32-OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/releases).
A Linux rendszerre, telepítenie kell a platformjának megfelelő (így sshd-kiszolgálót) SSH. A legújabb PowerShell-build vagy a csomag kellene a távoli eljáráshívás SSH szolgáltatás a githubból is kell.
A távoli gépen egy PowerShell-folyamat létrehozásához használt SSH alrendszerek és az SSH-kiszolgálót kell konfigurálni, amely. Szüksége lesz továbbá jelszóalapú hitelesítés, illetve opcionálisan kulcs alapú hitelesítés engedélyezéséhez.

## <a name="setup-on-windows-machine"></a>Windows-gépen beállítása

1. Telepítse a legújabb verzióját, [a Windows PowerShell Core]

   - Is megadhatja, hogy a távoli eljáráshívás SSH-támogatás, ha megnézzük a paraméterkészletek számára `New-PSSession`

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. A legújabb [Win32 OpenSSH] build telepítése [telepítés] utasításai a githubról
3. A helyen, amelyre telepítve van a Win32-OpenSSH sshd_config fájlban szerkesztése

   - Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > Az OpenSSH a Windows, amely megakadályozza, hogy a tárolóhelyek alrendszer végrehajtható elérési utak használata programhiba van.
     > Lásd: [további információt a problémát a Githubban](https://github.com/PowerShell/Win32-OpenSSH/issues/784).

     Az egyik megoldás, a Powershell telepítési könyvtárát, amely nem tartalmaz szóközöket szimbolikus létrehozásához:

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6.0.0"
     ```

     és a alrendszer írja be:

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - Igény szerint a kulcs alapú hitelesítés engedélyezése

     ```
     PubkeyAuthentication yes
     ```

4. Indítsa újra az sshd szolgáltatást

   ```powershell
   Restart-Service sshd
   ```

5. Az OpenSSH helyéül az elérési út Env változó az elérési út hozzáadása

   - Ez a témakörgyűjtemény legyen `C:\Program Files\OpenSSH\`
   - Ez lehetővé teszi a ssh.exe találhatók

## <a name="setup-on-linux-ubuntu-1404-machine"></a>Telepítés Linux (Ubuntu 14.04) gépen

1. Telepítse a legújabb [a PowerShell Core for Linux] build a Githubról
2. Telepítése [Ubuntu SSH] igény szerint

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

## <a name="setup-on-macos-machine"></a>A MacOS rendszerű gépén beállítása

1. Telepítse a legújabb [PowerShell Core for MacOS keretrendszert]-build

   - Győződjön meg arról, hogy SSH-távelérés engedélyezve van az alábbi lépéseket:
     - Nyissa meg `System Preferences`
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

## <a name="powershell-remoting-example"></a>Távoli eljáráshívás a PowerShell-példa

A legegyszerűbb módon távelérésének lehetővé tétele, hogy csak egyetlen gépen történő kipróbálására. Itt I hoz létre vissza ugyanarra a gépre a távoli munkamenetet egy Linux-be. Figyelje meg, hogy egy parancssorból a PowerShell-parancsmagok használom, így láthatjuk, hogy SSH ellenőrzése a gazdaszámítógépen, valamint a jelszót utasításokat kéri az utasításokat. Egy Windows gépre van működik a távoli eljáráshívás biztosításához és a gépek a gazdagép neve egyszerűen módosításával közötti majd távoli ugyanezt teheti meg.

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
 Id Name            ComputerName    ComputerType    State         ConfigurationName     Availability
 -- ----            ------------    ------------    -----         -----------------     ------------
  1 SSH1            UbuntuVM1       RemoteMachine   Opened        DefaultShell             Available
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

A sudo parancs nem működik a távoli munkamenetet Linux rendszerű gépen.

## <a name="see-also"></a>Lásd még:

[A Windows PowerShell Core](../setup/installing-powershell-core-on-windows.md#msi)

[A PowerShell Core linuxhoz](../setup/installing-powershell-core-on-linux.md#ubuntu-1404)

[MacOS-hez a PowerShell Core](../setup/installing-powershell-core-on-macos.md)

[A Win32-OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/releases)

[telepítés](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

[Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html)