
# <a name="powershell-remoting-over-ssh"></a><span data-ttu-id="b593c-101">PowerShell távoli eljáráshívás SSH-n keresztül</span><span class="sxs-lookup"><span data-stu-id="b593c-101">PowerShell Remoting Over SSH</span></span>

## <a name="overview"></a><span data-ttu-id="b593c-102">Áttekintés</span><span class="sxs-lookup"><span data-stu-id="b593c-102">Overview</span></span>

<span data-ttu-id="b593c-103">PowerShell távoli eljáráshívás általában winrm funkciót használ a kapcsolat egyeztetési és adatátvitel.</span><span class="sxs-lookup"><span data-stu-id="b593c-103">PowerShell remoting normally uses WinRM for connection negotiation and data transport.</span></span>
<span data-ttu-id="b593c-104">SSH a távoli eljáráshívás megvalósítási lett választva, mert már Linux és Windows platformokon elérhető, és lehetővé teszi, hogy igaz többplatformos PowerShell távoli eljáráshívás.</span><span class="sxs-lookup"><span data-stu-id="b593c-104">SSH was chosen for this remoting implementation since it is now available for both Linux and Windows platforms and allows true multiplatform PowerShell remoting.</span></span>
<span data-ttu-id="b593c-105">Azonban a Rendszerfelügyeleti webszolgáltatások is biztosít egy robusztus üzemeltetési modell PowerShell távoli munkamenetek, amelyek ezt a megvalósítást még nem teszi.</span><span class="sxs-lookup"><span data-stu-id="b593c-105">However, WinRM also provides a robust hosting model for PowerShell remote sessions which this implementation does not yet do.</span></span>
<span data-ttu-id="b593c-106">És ez azt jelenti, hogy PowerShell távoli végpont-konfiguráció és a JEA (Just Enough Administration) még nem támogatott a végrehajtása során.</span><span class="sxs-lookup"><span data-stu-id="b593c-106">And this means that PowerShell remote endpoint configuration and JEA (Just Enough Administration) is not yet supported in this implementation.</span></span>

<span data-ttu-id="b593c-107">PowerShell SSH távelérés lehetővé teszi egyszerű PowerShell-munkamenet távelérés Windows és Linux gép között.</span><span class="sxs-lookup"><span data-stu-id="b593c-107">PowerShell SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines.</span></span>
<span data-ttu-id="b593c-108">Ez történik, egy PowerShell-folyamat a célgépen, mint egy SSH-alrendszer üzemeltető létrehozásával.</span><span class="sxs-lookup"><span data-stu-id="b593c-108">This is done by creating a PowerShell hosting process on the target machine as an SSH subsystem.</span></span>
<span data-ttu-id="b593c-109">Végül ez fog módosítható, hasonlóan ahhoz, hogy támogatja a végpont-konfiguráció és a JEA WinRM működése általános üzemeltetési modell.</span><span class="sxs-lookup"><span data-stu-id="b593c-109">Eventually this will be changed to a more general hosting model similar to how WinRM works in order to support endpoint configuration and JEA.</span></span>

<span data-ttu-id="b593c-110">A `New-PSSession`, `Enter-PSSession` és `Invoke-Command` parancsmagok most már rendelkezik egy új paraméter megkönnyítése érdekében a távoli eljáráshívás új kapcsolat beállítása</span><span class="sxs-lookup"><span data-stu-id="b593c-110">The `New-PSSession`, `Enter-PSSession` and `Invoke-Command` cmdlets now have a new parameter set to facilitate this new remoting connection</span></span>

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

<span data-ttu-id="b593c-111">Az új paraméterkészlet valószínűleg változni fognak, de egyelőre lehetővé teszi, hogy hozzon létre SSH PSSessions, hogy kommunikáljanak a parancssorból, vagy a parancsok és szkriptek invoke.</span><span class="sxs-lookup"><span data-stu-id="b593c-111">This new parameter set will likely change but for now allows you to create SSH PSSessions that you can interact with from the command line or invoke commands and scripts on.</span></span>
<span data-ttu-id="b593c-112">A HostName paraméter adja meg a célgépen, és adja meg a felhasználónevet a felhasználónévvel.</span><span class="sxs-lookup"><span data-stu-id="b593c-112">You specify the target machine with the HostName parameter and provide the user name with UserName.</span></span>
<span data-ttu-id="b593c-113">Amikor interaktívan futtatja a parancsmagok a PowerShell-parancssorból, a rendszer kéri, a jelszót.</span><span class="sxs-lookup"><span data-stu-id="b593c-113">When running the cmdlets interactively at the PowerShell command line you will be prompted for a password.</span></span>
<span data-ttu-id="b593c-114">De lehetősége is van az SSH-kulcsos hitelesítést, és adja meg a titkos kulcsfájl elérési útja a KeyFilePath paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="b593c-114">But you also have the option to use SSH key authentication and provide a private key file path with the KeyFilePath parameter.</span></span>

## <a name="general-setup-information"></a><span data-ttu-id="b593c-115">Általános beállítási adatok</span><span class="sxs-lookup"><span data-stu-id="b593c-115">General setup information</span></span>

<span data-ttu-id="b593c-116">SSH szükség minden gépen telepíthető.</span><span class="sxs-lookup"><span data-stu-id="b593c-116">SSH is required to be installed on all machines.</span></span>
<span data-ttu-id="b593c-117">Telepítenie kell a mindkét-ügyfelet (`ssh.exe`) és a kiszolgáló (`sshd.exe`), hogy a távoli eljáráshívás irányuló és onnan a gépek kísérletezhet.</span><span class="sxs-lookup"><span data-stu-id="b593c-117">You should install both client (`ssh.exe`) and server (`sshd.exe`) so that you can experiment with remoting to and from the machines.</span></span>
<span data-ttu-id="b593c-118">A Windows, telepítenie kell [a Githubról történő Win32-OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/releases).</span><span class="sxs-lookup"><span data-stu-id="b593c-118">For Windows you will need to install [Win32 OpenSSH from GitHub](https://github.com/PowerShell/Win32-OpenSSH/releases).</span></span>
<span data-ttu-id="b593c-119">A Linux rendszerre, telepítenie kell a platformjának megfelelő (így sshd-kiszolgálót) SSH.</span><span class="sxs-lookup"><span data-stu-id="b593c-119">For Linux you will need to install SSH (including sshd server) appropriate to your platform.</span></span>
<span data-ttu-id="b593c-120">A legújabb PowerShell-build vagy a csomag kellene a távoli eljáráshívás SSH szolgáltatás a githubból is kell.</span><span class="sxs-lookup"><span data-stu-id="b593c-120">You will also need a recent PowerShell build or package from GitHub having the SSH remoting feature.</span></span>
<span data-ttu-id="b593c-121">A távoli gépen egy PowerShell-folyamat létrehozásához használt SSH alrendszerek és az SSH-kiszolgálót kell konfigurálni, amely.</span><span class="sxs-lookup"><span data-stu-id="b593c-121">SSH subsystems is used to establish a PowerShell process on the remote machine and the SSH server will need to be configured for that.</span></span>
<span data-ttu-id="b593c-122">Szüksége lesz továbbá jelszóalapú hitelesítés, illetve opcionálisan kulcs alapú hitelesítés engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="b593c-122">In addition you will need to enable password authentication and optionally key based authentication.</span></span>

## <a name="setup-on-windows-machine"></a><span data-ttu-id="b593c-123">Windows-gépen beállítása</span><span class="sxs-lookup"><span data-stu-id="b593c-123">Setup on Windows Machine</span></span>

1. <span data-ttu-id="b593c-124">Telepítse a legújabb verzióját, [a Windows PowerShell Core]</span><span class="sxs-lookup"><span data-stu-id="b593c-124">Install the latest version of [PowerShell Core for Windows]</span></span>
   - <span data-ttu-id="b593c-125">Is megadhatja, hogy a távoli eljáráshívás SSH-támogatás, ha megnézzük a paraméterkészletek számára `New-PSSession`</span><span class="sxs-lookup"><span data-stu-id="b593c-125">You can tell if it has the SSH remoting support by looking at the parameter sets for `New-PSSession`</span></span>

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. <span data-ttu-id="b593c-126">A legújabb [Win32 OpenSSH] build telepítése [telepítés] utasításai a githubról</span><span class="sxs-lookup"><span data-stu-id="b593c-126">Install the latest [Win32 OpenSSH] build from GitHub using the [installation] instructions</span></span>
3. <span data-ttu-id="b593c-127">A helyen, amelyre telepítve van a Win32-OpenSSH sshd_config fájlban szerkesztése</span><span class="sxs-lookup"><span data-stu-id="b593c-127">Edit the sshd_config file at the location where you installed Win32 OpenSSH</span></span>
   - <span data-ttu-id="b593c-128">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="b593c-128">Make sure password authentication is enabled</span></span>

   ```
   PasswordAuthentication yes
   ```

    ```
    Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
    ```

    > [!NOTE]
    <span data-ttu-id="b593c-129">Az OpenSSH a Windows, amely megakadályozza, hogy a tárolóhelyek alrendszer végrehajtható elérési utak használata programhiba van.</span><span class="sxs-lookup"><span data-stu-id="b593c-129">There is a bug in OpenSSH for Windows that prevents spaces from working in subsystem executable paths.</span></span>
    <span data-ttu-id="b593c-130">Lásd: [további információt a problémát a Githubban](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span><span class="sxs-lookup"><span data-stu-id="b593c-130">See [this issue on GitHub for more information](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span></span>

    <span data-ttu-id="b593c-131">Az egyik megoldás, a Powershell telepítési könyvtárát, amely nem tartalmaz szóközöket szimbolikus létrehozásához:</span><span class="sxs-lookup"><span data-stu-id="b593c-131">One solution is to create a symlink to the Powershell installation directory that does not contain spaces:</span></span>

    ```powershell
    mklink /D c:\pwsh "C:\Program Files\PowerShell\6.0.0"
    ```

    <span data-ttu-id="b593c-132">és a alrendszer írja be:</span><span class="sxs-lookup"><span data-stu-id="b593c-132">and then enter it in the subsystem:</span></span>

    ```
    Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
    ```

   ```
   Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
   ```

   - <span data-ttu-id="b593c-133">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="b593c-133">Optionally enable key authentication</span></span>

   ```
   PubkeyAuthentication yes
   ```

4. <span data-ttu-id="b593c-134">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="b593c-134">Restart the sshd service</span></span>

   ```powershell
   Restart-Service sshd
   ```

5. <span data-ttu-id="b593c-135">Az OpenSSH helyéül az elérési út Env változó az elérési út hozzáadása</span><span class="sxs-lookup"><span data-stu-id="b593c-135">Add the path where OpenSSH is installed to your Path Env Variable</span></span>
   - <span data-ttu-id="b593c-136">Ez a témakörgyűjtemény legyen `C:\Program Files\OpenSSH\`</span><span class="sxs-lookup"><span data-stu-id="b593c-136">This should be along the lines of `C:\Program Files\OpenSSH\`</span></span>
   - <span data-ttu-id="b593c-137">Ez lehetővé teszi a ssh.exe találhatók</span><span class="sxs-lookup"><span data-stu-id="b593c-137">This allows for the ssh.exe to be found</span></span>

## <a name="setup-on-linux-ubuntu-1404-machine"></a><span data-ttu-id="b593c-138">Telepítés Linux (Ubuntu 14.04) gépen</span><span class="sxs-lookup"><span data-stu-id="b593c-138">Setup on Linux (Ubuntu 14.04) Machine</span></span>

1. <span data-ttu-id="b593c-139">Telepítse a legújabb [a PowerShell Core for Linux] build a Githubról</span><span class="sxs-lookup"><span data-stu-id="b593c-139">Install the latest [PowerShell Core for Linux] build from GitHub</span></span>
2. <span data-ttu-id="b593c-140">Telepítése [Ubuntu SSH] igény szerint</span><span class="sxs-lookup"><span data-stu-id="b593c-140">Install [Ubuntu SSH] as needed</span></span>

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. <span data-ttu-id="b593c-141">Az sshd_config fájlban a következő helyen /etc/ssh szerkesztése</span><span class="sxs-lookup"><span data-stu-id="b593c-141">Edit the sshd_config file at location /etc/ssh</span></span>
   - <span data-ttu-id="b593c-142">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="b593c-142">Make sure password authentication is enabled</span></span>

   ```
   PasswordAuthentication yes
   ```

   - <span data-ttu-id="b593c-143">PowerShell alrendszer bejegyzés hozzáadása</span><span class="sxs-lookup"><span data-stu-id="b593c-143">Add a PowerShell subsystem entry</span></span>

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - <span data-ttu-id="b593c-144">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="b593c-144">Optionally enable key authentication</span></span>

   ```
   PubkeyAuthentication yes
   ```

4. <span data-ttu-id="b593c-145">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="b593c-145">Restart the sshd service</span></span>

   ```bash
   sudo service sshd restart
   ```

## <a name="setup-on-macos-machine"></a><span data-ttu-id="b593c-146">A MacOS rendszerű gépén beállítása</span><span class="sxs-lookup"><span data-stu-id="b593c-146">Setup on MacOS Machine</span></span>

1. <span data-ttu-id="b593c-147">Telepítse a legújabb [PowerShell Core for MacOS keretrendszert]-build</span><span class="sxs-lookup"><span data-stu-id="b593c-147">Install the latest [PowerShell Core for MacOS] build</span></span>
   - <span data-ttu-id="b593c-148">Győződjön meg arról, hogy SSH-távelérés engedélyezve van az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="b593c-148">Make sure SSH Remoting is enabled by following these steps:</span></span>
     - <span data-ttu-id="b593c-149">Nyissa meg `System Preferences`</span><span class="sxs-lookup"><span data-stu-id="b593c-149">Open `System Preferences`</span></span>
     - <span data-ttu-id="b593c-150">Kattintson a `Sharing`</span><span class="sxs-lookup"><span data-stu-id="b593c-150">Click on `Sharing`</span></span>
     - <span data-ttu-id="b593c-151">Ellenőrizze `Remote Login` – a következő: `Remote Login: On`</span><span class="sxs-lookup"><span data-stu-id="b593c-151">Check `Remote Login` - Should say `Remote Login: On`</span></span>
     - <span data-ttu-id="b593c-152">Megfelelő felhasználók férhessenek hozzá</span><span class="sxs-lookup"><span data-stu-id="b593c-152">Allow access to appropriate users</span></span>
2. <span data-ttu-id="b593c-153">Szerkessze a `sshd_config` helyen található fájl `/private/etc/ssh/sshd_config`</span><span class="sxs-lookup"><span data-stu-id="b593c-153">Edit the `sshd_config` file at location `/private/etc/ssh/sshd_config`</span></span>
   - <span data-ttu-id="b593c-154">Használja kedvenc szerkesztőjében, vagy</span><span class="sxs-lookup"><span data-stu-id="b593c-154">Use your favorite editor or</span></span>

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - <span data-ttu-id="b593c-155">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="b593c-155">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

   - <span data-ttu-id="b593c-156">PowerShell alrendszer bejegyzés hozzáadása</span><span class="sxs-lookup"><span data-stu-id="b593c-156">Add a PowerShell subsystem entry</span></span>

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="b593c-157">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="b593c-157">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

3. <span data-ttu-id="b593c-158">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="b593c-158">Restart the sshd service</span></span>

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="powershell-remoting-example"></a><span data-ttu-id="b593c-159">Távoli eljáráshívás a PowerShell-példa</span><span class="sxs-lookup"><span data-stu-id="b593c-159">PowerShell Remoting Example</span></span>

<span data-ttu-id="b593c-160">A legegyszerűbb módon távelérésének lehetővé tétele, hogy csak egyetlen gépen történő kipróbálására.</span><span class="sxs-lookup"><span data-stu-id="b593c-160">The easiest way to test remoting is to just try it on a single machine.</span></span>
<span data-ttu-id="b593c-161">Itt I hoz létre vissza ugyanarra a gépre a távoli munkamenetet egy Linux-be.</span><span class="sxs-lookup"><span data-stu-id="b593c-161">Here I will create a remote session back to the same machine on a Linux box.</span></span>
<span data-ttu-id="b593c-162">Figyelje meg, hogy egy parancssorból a PowerShell-parancsmagok használom, így láthatjuk, hogy SSH ellenőrzése a gazdaszámítógépen, valamint a jelszót utasításokat kéri az utasításokat.</span><span class="sxs-lookup"><span data-stu-id="b593c-162">Notice that I am using PowerShell cmdlets from a command prompt so we see prompts from SSH asking to verify the host computer as well as password prompts.</span></span>
<span data-ttu-id="b593c-163">Egy Windows gépre van működik a távoli eljáráshívás biztosításához és a gépek a gazdagép neve egyszerűen módosításával közötti majd távoli ugyanezt teheti meg.</span><span class="sxs-lookup"><span data-stu-id="b593c-163">You can do the same thing on a Windows machine to ensure remoting is working there and then remote between machines by simply changing the host name.</span></span>

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

### <a name="known-issues"></a><span data-ttu-id="b593c-164">Ismert problémák</span><span class="sxs-lookup"><span data-stu-id="b593c-164">Known Issues</span></span>

- <span data-ttu-id="b593c-165">sudo parancs nem működik a távoli munkamenetet Linux rendszerű gépen.</span><span class="sxs-lookup"><span data-stu-id="b593c-165">sudo command does not work in remote session to Linux machine.</span></span>

## <a name="see-also"></a><span data-ttu-id="b593c-166">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b593c-166">See Also</span></span>

[<span data-ttu-id="b593c-167">A Windows PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="b593c-167">PowerShell Core for Windows</span></span>](../setup/installing-powershell-core-on-windows.md#msi)

[<span data-ttu-id="b593c-168">A PowerShell Core linuxhoz</span><span class="sxs-lookup"><span data-stu-id="b593c-168">PowerShell Core for Linux</span></span>](../setup/installing-powershell-core-on-linux.md#ubuntu-1404)

[<span data-ttu-id="b593c-169">MacOS-hez a PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="b593c-169">PowerShell Core for MacOS</span></span>](../setup/installing-powershell-core-on-macos.md)

[<span data-ttu-id="b593c-170">A Win32-OpenSSH</span><span class="sxs-lookup"><span data-stu-id="b593c-170">Win32 OpenSSH</span></span>](https://github.com/PowerShell/Win32-OpenSSH/releases)

[<span data-ttu-id="b593c-171">telepítés</span><span class="sxs-lookup"><span data-stu-id="b593c-171">installation</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

[<span data-ttu-id="b593c-172">Ubuntu SSH</span><span class="sxs-lookup"><span data-stu-id="b593c-172">Ubuntu SSH</span></span>](https://help.ubuntu.com/lts/serverguide/openssh-server.html)