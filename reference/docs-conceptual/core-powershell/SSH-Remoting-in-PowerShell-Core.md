# <a name="powershell-remoting-over-ssh"></a><span data-ttu-id="37b31-101">PowerShell távoli eljáráshívás SSH-n keresztül</span><span class="sxs-lookup"><span data-stu-id="37b31-101">PowerShell Remoting Over SSH</span></span>

## <a name="overview"></a><span data-ttu-id="37b31-102">Áttekintés</span><span class="sxs-lookup"><span data-stu-id="37b31-102">Overview</span></span>

<span data-ttu-id="37b31-103">PowerShell távvezérlése általában használ Rendszerfelügyeleti webszolgáltatások kapcsolat egyeztetéshez, és az adatok átvitel.</span><span class="sxs-lookup"><span data-stu-id="37b31-103">PowerShell remoting normally uses WinRM for connection negotiation and data transport.</span></span>
<span data-ttu-id="37b31-104">SSH a távoli eljáráshívás megvalósításával lett választva, mert Linux és a Windows platformokhoz érhető el, és lehetővé teszi, hogy igaz többplatformos PowerShell távoli eljáráshívás.</span><span class="sxs-lookup"><span data-stu-id="37b31-104">SSH was chosen for this remoting implementation since it is now available for both Linux and Windows platforms and allows true multiplatform PowerShell remoting.</span></span>
<span data-ttu-id="37b31-105">Azonban a Rendszerfelügyeleti webszolgáltatások is biztosít egy robusztus üzemeltetési modell PowerShell távoli munkamenetek, amelyek ebben az implementációban még nem.</span><span class="sxs-lookup"><span data-stu-id="37b31-105">However, WinRM also provides a robust hosting model for PowerShell remote sessions which this implementation does not yet do.</span></span>
<span data-ttu-id="37b31-106">És ez azt jelenti, hogy PowerShell távoli végpont-konfiguráció és a JEA (csak elég felügyeleti) jelenleg nem támogatott ebben az implementációban.</span><span class="sxs-lookup"><span data-stu-id="37b31-106">And this means that PowerShell remote endpoint configuration and JEA (Just Enough Administration) is not yet supported in this implementation.</span></span>

<span data-ttu-id="37b31-107">PowerShell SSH távoli eljáráshívás lehetővé teszi alapszintű PowerShell-munkamenet távelérés Windows és Linux rendszerű számítógép között.</span><span class="sxs-lookup"><span data-stu-id="37b31-107">PowerShell SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines.</span></span>
<span data-ttu-id="37b31-108">Ez a folyamat a célszámítógépen, egy SSH-alrendszer üzemeltető PowerShell létrehozásával történik.</span><span class="sxs-lookup"><span data-stu-id="37b31-108">This is done by creating a PowerShell hosting process on the target machine as an SSH subsystem.</span></span>
<span data-ttu-id="37b31-109">Végül ez módosulnak hasonlóak a Rendszerfelügyeleti webszolgáltatások működése érdekében támogatja a végpont-konfiguráció és a JEA általánosabb üzemeltetési modellre.</span><span class="sxs-lookup"><span data-stu-id="37b31-109">Eventually this will be changed to a more general hosting model similar to how WinRM works in order to support endpoint configuration and JEA.</span></span>

<span data-ttu-id="37b31-110">A New-PSSession, Enter-PSSession és Invoke-Command-parancsmagok most már rendelkezik egy új paraméter lehetővé teszi a távoli eljáráshívás új kapcsolat beállítása</span><span class="sxs-lookup"><span data-stu-id="37b31-110">The New-PSSession, Enter-PSSession and Invoke-Command cmdlets now have a new parameter set to facilitate this new remoting connection</span></span>

```powershell
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

<span data-ttu-id="37b31-111">Az új paraméterkészletet alakítanak valószínűleg változik, de most hozhat létre SSH PSSession, hogy a parancssorból kezelésére, és meghívni parancsaiban és parancsfájljaiban.</span><span class="sxs-lookup"><span data-stu-id="37b31-111">This new parameter set will likely change but for now allows you to create SSH PSSessions that you can interact with from the command line or invoke commands and scripts on.</span></span>
<span data-ttu-id="37b31-112">Adja meg a célszámítógépen az állomásnév paraméterrel, és adjon meg a felhasználónevet használva.</span><span class="sxs-lookup"><span data-stu-id="37b31-112">You specify the target machine with the HostName parameter and provide the user name with UserName.</span></span>
<span data-ttu-id="37b31-113">A parancsmag párbeszédes formában történő futtatásakor a PowerShell-parancssorból kéri a jelszót.</span><span class="sxs-lookup"><span data-stu-id="37b31-113">When running the cmdlets interactively at the PowerShell command line you will be prompted for a password.</span></span>
<span data-ttu-id="37b31-114">De lehetősége is van SSH hitelesítés használatára, majd adjon meg egy titkos kulcsot tartalmazó fájlt elérési utat a KeyFilePath paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="37b31-114">But you also have the option to use SSH key authentication and provide a private key file path with the KeyFilePath parameter.</span></span>

## <a name="general-setup-information"></a><span data-ttu-id="37b31-115">Általános telepítési információk</span><span class="sxs-lookup"><span data-stu-id="37b31-115">General setup information</span></span>

<span data-ttu-id="37b31-116">Az SSH egy minden gépen kell telepíteni.</span><span class="sxs-lookup"><span data-stu-id="37b31-116">SSH is required to be installed on all machines.</span></span>
<span data-ttu-id="37b31-117">Telepíteni kell (ssh.exe) ügyfélen és kiszolgálón (sshd.exe) is, hogy a gépek és a távelérés kísérletezhet.</span><span class="sxs-lookup"><span data-stu-id="37b31-117">You should install both client (ssh.exe) and server (sshd.exe) so that you can experiment with remoting to and from the machines.</span></span>
<span data-ttu-id="37b31-118">A Windows rendszer telepítendő [Win32 OpenSSH a Githubról](https://github.com/PowerShell/Win32-OpenSSH/releases).</span><span class="sxs-lookup"><span data-stu-id="37b31-118">For Windows you will need to install [Win32 OpenSSH from GitHub](https://github.com/PowerShell/Win32-OpenSSH/releases).</span></span>
<span data-ttu-id="37b31-119">Linux kell telepíteni kell a platform (többek között a következőket sshd kiszolgáló) SSH.</span><span class="sxs-lookup"><span data-stu-id="37b31-119">For Linux you will need to install SSH (including sshd server) appropriate to your platform.</span></span>
<span data-ttu-id="37b31-120">Konfigurálnia kell a legutóbbi PowerShell build vagy a csomag a Githubból, hogy az SSH távvezérlési funkció.</span><span class="sxs-lookup"><span data-stu-id="37b31-120">You will also need a recent PowerShell build or package from GitHub having the SSH remoting feature.</span></span>
<span data-ttu-id="37b31-121">SSH-alrendszereket használatos PowerShell folyamatot a távoli számítógépen, és az SSH-kiszolgálót kell konfigurálni, hogy.</span><span class="sxs-lookup"><span data-stu-id="37b31-121">SSH subsystems is used to establish a PowerShell process on the remote machine and the SSH server will need to be configured for that.</span></span>
<span data-ttu-id="37b31-122">Továbbá szüksége lesz jelszóalapú hitelesítés, illetve opcionálisan kulcs alapú hitelesítés engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="37b31-122">In addition you will need to enable password authentication and optionally key based authentication.</span></span>

## <a name="setup-on-windows-machine"></a><span data-ttu-id="37b31-123">A telepítő a Windows-gépen</span><span class="sxs-lookup"><span data-stu-id="37b31-123">Setup on Windows Machine</span></span>

1. <span data-ttu-id="37b31-124">[A Windows PowerShell-Core legújabb verziójának telepítéséhez] []</span><span class="sxs-lookup"><span data-stu-id="37b31-124">[Install the latest version of PowerShell Core for Windows][]</span></span>
    - <span data-ttu-id="37b31-125">Állapítható meg, ha az SSH-távelérésének jobb támogatása megnézzük a paraméter állandóként állítja be a New-PSSession</span><span class="sxs-lookup"><span data-stu-id="37b31-125">You can tell if it has the SSH remoting support by looking at the parameter sets for New-PSSession</span></span>
    ```powershell
    PS> Get-Command New-PSSession -syntax
    New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
    ```
1. <span data-ttu-id="37b31-126">Telepítse a legújabb [Win32 OpenSSH] GitHub használatával felépíteni a [telepítési] utasításokat</span><span class="sxs-lookup"><span data-stu-id="37b31-126">Install the latest [Win32 OpenSSH] build from GitHub using the [installation] instructions</span></span>
1. <span data-ttu-id="37b31-127">A Win32 OpenSSH telepítési helyére sshd_config fájl szerkesztése</span><span class="sxs-lookup"><span data-stu-id="37b31-127">Edit the sshd_config file at the location where you installed Win32 OpenSSH</span></span>
    - <span data-ttu-id="37b31-128">Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van</span><span class="sxs-lookup"><span data-stu-id="37b31-128">Make sure password authentication is enabled</span></span>
    ```none
    PasswordAuthentication yes
    ```
    - <span data-ttu-id="37b31-129">PowerShell alrendszer bejegyzés hozzáadása, cseréje `c:/program files/powershell/6.0.0/pwsh.exe` a helyes elérési útját a használni kívánt verzióra</span><span class="sxs-lookup"><span data-stu-id="37b31-129">Add a PowerShell subsystem entry, replace `c:/program files/powershell/6.0.0/pwsh.exe` with the correct path to the version you want to use</span></span>
    ```none
    Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
    ```
    - <span data-ttu-id="37b31-130">Opcionálisan a hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="37b31-130">Optionally enable key authentication</span></span>
    ```none
    PubkeyAuthentication yes
    ```
1. <span data-ttu-id="37b31-131">Indítsa újra a sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="37b31-131">Restart the sshd service</span></span>
    ```powershell
    Restart-Service sshd
    ```
1. <span data-ttu-id="37b31-132">Az elérési utat, ahol OpenSSH van telepítve az elérési út Env változó hozzáadása</span><span class="sxs-lookup"><span data-stu-id="37b31-132">Add the path where OpenSSH is installed to your Path Env Variable</span></span>
    - <span data-ttu-id="37b31-133">Ez a témakörgyűjtemény legyen `C:\Program Files\OpenSSH\`</span><span class="sxs-lookup"><span data-stu-id="37b31-133">This should be along the lines of `C:\Program Files\OpenSSH\`</span></span>
    - <span data-ttu-id="37b31-134">Ez lehetővé teszi a keresett ssh.exe</span><span class="sxs-lookup"><span data-stu-id="37b31-134">This allows for the ssh.exe to be found</span></span>

## <a name="setup-on-linux-ubuntu-1404-machine"></a><span data-ttu-id="37b31-135">Linux (Ubuntu 14.04) gépen beállítása</span><span class="sxs-lookup"><span data-stu-id="37b31-135">Setup on Linux (Ubuntu 14.04) Machine</span></span>

1. <span data-ttu-id="37b31-136">Telepítse a legújabb [Linux PowerShell] a Githubról összeállítása</span><span class="sxs-lookup"><span data-stu-id="37b31-136">Install the latest [PowerShell for Linux] build from GitHub</span></span>
1. <span data-ttu-id="37b31-137">Telepítés [Ubuntu SSH] igény szerint</span><span class="sxs-lookup"><span data-stu-id="37b31-137">Install [Ubuntu SSH] as needed</span></span>
    ```bash
    sudo apt install openssh-client
    sudo apt install openssh-server
    ```
1. <span data-ttu-id="37b31-138">A sshd_config fájlban a következő helyen /etc/ssh szerkesztése</span><span class="sxs-lookup"><span data-stu-id="37b31-138">Edit the sshd_config file at location /etc/ssh</span></span>
    - <span data-ttu-id="37b31-139">Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van</span><span class="sxs-lookup"><span data-stu-id="37b31-139">Make sure password authentication is enabled</span></span>
    ```none
    PasswordAuthentication yes
    ```
    - <span data-ttu-id="37b31-140">PowerShell alrendszer bejegyzés hozzáadása</span><span class="sxs-lookup"><span data-stu-id="37b31-140">Add a PowerShell subsystem entry</span></span>
    ```none
    Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
    ```
    - <span data-ttu-id="37b31-141">Opcionálisan a hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="37b31-141">Optionally enable key authentication</span></span>
    ```none
    PubkeyAuthentication yes
    ```
1. <span data-ttu-id="37b31-142">Indítsa újra a sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="37b31-142">Restart the sshd service</span></span>
    ```bash
    sudo service sshd restart
    ```

## <a name="setup-on-macos-machine"></a><span data-ttu-id="37b31-143">MacOS gépen beállítása</span><span class="sxs-lookup"><span data-stu-id="37b31-143">Setup on MacOS Machine</span></span>

1. <span data-ttu-id="37b31-144">Telepítse a legújabb [PowerShell MacOS] összeállítása</span><span class="sxs-lookup"><span data-stu-id="37b31-144">Install the latest [PowerShell for MacOS] build</span></span>
    - <span data-ttu-id="37b31-145">Ellenőrizze, hogy engedélyezve van a SSH távelérése az alábbiak szerint:</span><span class="sxs-lookup"><span data-stu-id="37b31-145">Make sure SSH Remoting is enabled by following these steps:</span></span>
      - <span data-ttu-id="37b31-146">Nyissa meg `System Preferences`</span><span class="sxs-lookup"><span data-stu-id="37b31-146">Open `System Preferences`</span></span>
      - <span data-ttu-id="37b31-147">Kattintson a `Sharing`</span><span class="sxs-lookup"><span data-stu-id="37b31-147">Click on `Sharing`</span></span>
      - <span data-ttu-id="37b31-148">Ellenőrizze `Remote Login` -üzenetnek kell megjelennie `Remote Login: On`</span><span class="sxs-lookup"><span data-stu-id="37b31-148">Check `Remote Login` - Should say `Remote Login: On`</span></span>
      - <span data-ttu-id="37b31-149">Megfelelő felhasználók hozzáférésének engedélyezése</span><span class="sxs-lookup"><span data-stu-id="37b31-149">Allow access to appropriate users</span></span>
1. <span data-ttu-id="37b31-150">Szerkessze a `sshd_config` fájl a következő helyen: `/private/etc/ssh/sshd_config`</span><span class="sxs-lookup"><span data-stu-id="37b31-150">Edit the `sshd_config` file at location `/private/etc/ssh/sshd_config`</span></span>
    - <span data-ttu-id="37b31-151">A kedvenc szerkesztővel vagy</span><span class="sxs-lookup"><span data-stu-id="37b31-151">Use your favorite editor or</span></span>
    ```bash
    sudo nano /private/etc/ssh/sshd_config
    ```
    - <span data-ttu-id="37b31-152">Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van</span><span class="sxs-lookup"><span data-stu-id="37b31-152">Make sure password authentication is enabled</span></span>
    ```none
    PasswordAuthentication yes
    ```
    - <span data-ttu-id="37b31-153">PowerShell alrendszer bejegyzés hozzáadása</span><span class="sxs-lookup"><span data-stu-id="37b31-153">Add a PowerShell subsystem entry</span></span>
    ```none
    Subsystem powershell /usr/local/bin/powershell -sshs -NoLogo -NoProfile
    ```
    - <span data-ttu-id="37b31-154">Opcionálisan a hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="37b31-154">Optionally enable key authentication</span></span>
    ```none
    PubkeyAuthentication yes
    ```
1. <span data-ttu-id="37b31-155">Indítsa újra a sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="37b31-155">Restart the sshd service</span></span>
    ```bash
    sudo launchctl stop com.openssh.sshd
    sudo launchctl start com.openssh.sshd
    ```

## <a name="powershell-remoting-example"></a><span data-ttu-id="37b31-156">PowerShell távoli eljáráshívás – példa</span><span class="sxs-lookup"><span data-stu-id="37b31-156">PowerShell Remoting Example</span></span>

<span data-ttu-id="37b31-157">A távoli eljáráshívás teszteléséhez legkönnyebben csak egyetlen gépen próbálja.</span><span class="sxs-lookup"><span data-stu-id="37b31-157">The easiest way to test remoting is to just try it on a single machine.</span></span>
<span data-ttu-id="37b31-158">Itt I hoz létre egy távoli munkamenet az azonos gépre egy Linux-be.</span><span class="sxs-lookup"><span data-stu-id="37b31-158">Here I will create a remote session back to the same machine on a Linux box.</span></span>
<span data-ttu-id="37b31-159">Figyelje meg, hogy PowerShell-parancsmagok egy parancs parancssori futtatásával használom, így azt kéri az SSH ellenőrzése a gazdaszámítógépen, valamint a kért azonosítóadatok kéri.</span><span class="sxs-lookup"><span data-stu-id="37b31-159">Notice that I am using PowerShell cmdlets from a command prompt so we see prompts from SSH asking to verify the host computer as well as password prompts.</span></span>
<span data-ttu-id="37b31-160">Ezt megteheti ugyanezt egy Windows számítógép távoli eljáráshívási hiba működik-e, és ezután távoli gép állomásneve egyszerűen módosításával közötti.</span><span class="sxs-lookup"><span data-stu-id="37b31-160">You can do the same thing on a Windows machine to ensure remoting is working there and then remote between machines by simply changing the host name.</span></span>

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

### <a name="known-issues"></a><span data-ttu-id="37b31-161">Ismert problémák</span><span class="sxs-lookup"><span data-stu-id="37b31-161">Known Issues</span></span>

1. <span data-ttu-id="37b31-162">sudo parancs nem működik a távoli munkamenet Linux-számítógép.</span><span class="sxs-lookup"><span data-stu-id="37b31-162">sudo command does not work in remote session to Linux machine.</span></span>

[PowerShell for Windows]: https://github.com/PowerShell/PowerShell/blob/master/docs/installation/windows.md#msi
[Win32 OpenSSH]: https://github.com/PowerShell/Win32-OpenSSH
[telepítési]: https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH
[installation]: https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH
[Linux PowerShell]: https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md#ubuntu-1404
[PowerShell for Linux]: https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md#ubuntu-1404
[Ubuntu SSH]: https://help.ubuntu.com/lts/serverguide/openssh-server.html
[PowerShell MacOS]: https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md#macos-1012
[PowerShell for MacOS]: https://github.com/PowerShell/PowerShell/blob/master/docs/installation/linux.md#macos-1012