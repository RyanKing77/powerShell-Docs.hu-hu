---
title: PowerShell távoli eljáráshívás SSH-n keresztül
description: Távoli eljáráshívás a PowerShell Core SSH-val
ms.date: 08/06/2018
ms.openlocfilehash: 27a8fc5623796a270a2ea67aa550c9a0998e766b
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587499"
---
# <a name="powershell-remoting-over-ssh"></a><span data-ttu-id="f5faf-103">PowerShell távoli eljáráshívás SSH-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f5faf-103">PowerShell Remoting Over SSH</span></span>

## <a name="overview"></a><span data-ttu-id="f5faf-104">Áttekintés</span><span class="sxs-lookup"><span data-stu-id="f5faf-104">Overview</span></span>

<span data-ttu-id="f5faf-105">PowerShell távoli eljáráshívás általában winrm funkciót használ a kapcsolat egyeztetési és adatátvitel.</span><span class="sxs-lookup"><span data-stu-id="f5faf-105">PowerShell remoting normally uses WinRM for connection negotiation and data transport.</span></span> <span data-ttu-id="f5faf-106">SSH a távoli eljáráshívás megvalósítási lett választva, mert már Linux és Windows platformokon elérhető, és lehetővé teszi, hogy igaz többplatformos PowerShell távoli eljáráshívás.</span><span class="sxs-lookup"><span data-stu-id="f5faf-106">SSH was chosen for this remoting implementation since it is now available for both Linux and Windows platforms and allows true multiplatform PowerShell remoting.</span></span> <span data-ttu-id="f5faf-107">Azonban a Rendszerfelügyeleti webszolgáltatások is biztosít egy robusztus üzemeltetési modell PowerShell távoli munkamenetek, amelyek ezt a megvalósítást még nem teszi.</span><span class="sxs-lookup"><span data-stu-id="f5faf-107">However, WinRM also provides a robust hosting model for PowerShell remote sessions which this implementation does not yet do.</span></span> <span data-ttu-id="f5faf-108">És ez azt jelenti, hogy PowerShell távoli végpont-konfiguráció és a JEA (Just Enough Administration) még nem támogatott a végrehajtása során.</span><span class="sxs-lookup"><span data-stu-id="f5faf-108">And this means that PowerShell remote endpoint configuration and JEA (Just Enough Administration) is not yet supported in this implementation.</span></span>

<span data-ttu-id="f5faf-109">PowerShell SSH távelérés lehetővé teszi egyszerű PowerShell-munkamenet távelérés Windows és Linux gép között.</span><span class="sxs-lookup"><span data-stu-id="f5faf-109">PowerShell SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines.</span></span> <span data-ttu-id="f5faf-110">Ez történik, egy PowerShell-folyamat a célgépen, mint egy SSH-alrendszer üzemeltető létrehozásával.</span><span class="sxs-lookup"><span data-stu-id="f5faf-110">This is done by creating a PowerShell hosting process on the target machine as an SSH subsystem.</span></span> <span data-ttu-id="f5faf-111">Végül ez fog módosítható, hasonlóan ahhoz, hogy támogatja a végpont-konfiguráció és a JEA WinRM működése általános üzemeltetési modell.</span><span class="sxs-lookup"><span data-stu-id="f5faf-111">Eventually this will be changed to a more general hosting model similar to how WinRM works in order to support endpoint configuration and JEA.</span></span>

<span data-ttu-id="f5faf-112">A `New-PSSession`, `Enter-PSSession` és `Invoke-Command` parancsmagok most már rendelkezik egy új paraméter megkönnyítése érdekében a távoli eljáráshívás új kapcsolat beállítása</span><span class="sxs-lookup"><span data-stu-id="f5faf-112">The `New-PSSession`, `Enter-PSSession` and `Invoke-Command` cmdlets now have a new parameter set to facilitate this new remoting connection</span></span>

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

<span data-ttu-id="f5faf-113">Az új paraméterkészlet valószínűleg változni fognak, de egyelőre lehetővé teszi, hogy hozzon létre SSH PSSessions, hogy kommunikáljanak a parancssorból, vagy a parancsok és szkriptek invoke.</span><span class="sxs-lookup"><span data-stu-id="f5faf-113">This new parameter set will likely change but for now allows you to create SSH PSSessions that you can interact with from the command line or invoke commands and scripts on.</span></span> <span data-ttu-id="f5faf-114">A HostName paraméter adja meg a célgépen, és adja meg a felhasználónevet a felhasználónévvel.</span><span class="sxs-lookup"><span data-stu-id="f5faf-114">You specify the target machine with the HostName parameter and provide the user name with UserName.</span></span> <span data-ttu-id="f5faf-115">Amikor interaktívan futtatja a parancsmagok a PowerShell-parancssorból, a rendszer kéri, a jelszót.</span><span class="sxs-lookup"><span data-stu-id="f5faf-115">When running the cmdlets interactively at the PowerShell command line you will be prompted for a password.</span></span> <span data-ttu-id="f5faf-116">De lehetősége is van az SSH-kulcsos hitelesítést, és adja meg a titkos kulcsfájl elérési útja a KeyFilePath paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="f5faf-116">But you also have the option to use SSH key authentication and provide a private key file path with the KeyFilePath parameter.</span></span>

## <a name="general-setup-information"></a><span data-ttu-id="f5faf-117">Általános beállítási adatok</span><span class="sxs-lookup"><span data-stu-id="f5faf-117">General setup information</span></span>

<span data-ttu-id="f5faf-118">SSH szükség minden gépen telepíthető.</span><span class="sxs-lookup"><span data-stu-id="f5faf-118">SSH is required to be installed on all machines.</span></span> <span data-ttu-id="f5faf-119">Telepítenie kell a mindkét-ügyfelet (`ssh.exe`) és a kiszolgáló (`sshd.exe`), hogy a távoli eljáráshívás irányuló és onnan a gépek kísérletezhet.</span><span class="sxs-lookup"><span data-stu-id="f5faf-119">You should install both client (`ssh.exe`) and server (`sshd.exe`) so that you can experiment with remoting to and from the machines.</span></span> <span data-ttu-id="f5faf-120">A Windows, telepítenie kell [a Githubról történő Win32-OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/releases).</span><span class="sxs-lookup"><span data-stu-id="f5faf-120">For Windows you will need to install [Win32 OpenSSH from GitHub](https://github.com/PowerShell/Win32-OpenSSH/releases).</span></span>
<span data-ttu-id="f5faf-121">A Linux rendszerre, telepítenie kell a platformjának megfelelő (így sshd-kiszolgálót) SSH.</span><span class="sxs-lookup"><span data-stu-id="f5faf-121">For Linux you will need to install SSH (including sshd server) appropriate to your platform.</span></span> <span data-ttu-id="f5faf-122">A legújabb PowerShell-build vagy a csomag kellene a távoli eljáráshívás SSH szolgáltatás a githubból is kell.</span><span class="sxs-lookup"><span data-stu-id="f5faf-122">You will also need a recent PowerShell build or package from GitHub having the SSH remoting feature.</span></span>
<span data-ttu-id="f5faf-123">A távoli gépen egy PowerShell-folyamat létrehozásához használt SSH alrendszerek és az SSH-kiszolgálót kell konfigurálni, amely.</span><span class="sxs-lookup"><span data-stu-id="f5faf-123">SSH subsystems is used to establish a PowerShell process on the remote machine and the SSH server will need to be configured for that.</span></span> <span data-ttu-id="f5faf-124">Szüksége lesz továbbá jelszóalapú hitelesítés, illetve opcionálisan kulcs alapú hitelesítés engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="f5faf-124">In addition you will need to enable password authentication and optionally key based authentication.</span></span>

## <a name="setup-on-windows-machine"></a><span data-ttu-id="f5faf-125">Windows-gépen beállítása</span><span class="sxs-lookup"><span data-stu-id="f5faf-125">Setup on Windows Machine</span></span>

1. <span data-ttu-id="f5faf-126">Telepítse a legújabb verzióját, [a Windows PowerShell Core]</span><span class="sxs-lookup"><span data-stu-id="f5faf-126">Install the latest version of [PowerShell Core for Windows]</span></span>

   - <span data-ttu-id="f5faf-127">Is megadhatja, hogy a távoli eljáráshívás SSH-támogatás, ha megnézzük a paraméterkészletek számára `New-PSSession`</span><span class="sxs-lookup"><span data-stu-id="f5faf-127">You can tell if it has the SSH remoting support by looking at the parameter sets for `New-PSSession`</span></span>

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. <span data-ttu-id="f5faf-128">A legújabb [Win32 OpenSSH] build telepítése [telepítés] utasításai a githubról</span><span class="sxs-lookup"><span data-stu-id="f5faf-128">Install the latest [Win32 OpenSSH] build from GitHub using the [installation] instructions</span></span>
3. <span data-ttu-id="f5faf-129">A helyen, amelyre telepítve van a Win32-OpenSSH sshd_config fájlban szerkesztése</span><span class="sxs-lookup"><span data-stu-id="f5faf-129">Edit the sshd_config file at the location where you installed Win32 OpenSSH</span></span>

   - <span data-ttu-id="f5faf-130">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="f5faf-130">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > <span data-ttu-id="f5faf-131">Az OpenSSH a Windows, amely megakadályozza, hogy a tárolóhelyek alrendszer végrehajtható elérési utak használata programhiba van.</span><span class="sxs-lookup"><span data-stu-id="f5faf-131">There is a bug in OpenSSH for Windows that prevents spaces from working in subsystem executable paths.</span></span>
     > <span data-ttu-id="f5faf-132">Lásd: [további információt a problémát a Githubban](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span><span class="sxs-lookup"><span data-stu-id="f5faf-132">See [this issue on GitHub for more information](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span></span>

     <span data-ttu-id="f5faf-133">Az egyik megoldás, a Powershell telepítési könyvtárát, amely nem tartalmaz szóközöket szimbolikus létrehozásához:</span><span class="sxs-lookup"><span data-stu-id="f5faf-133">One solution is to create a symlink to the Powershell installation directory that does not contain spaces:</span></span>

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6.0.0"
     ```

     <span data-ttu-id="f5faf-134">és a alrendszer írja be:</span><span class="sxs-lookup"><span data-stu-id="f5faf-134">and then enter it in the subsystem:</span></span>

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6.0.0/pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="f5faf-135">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="f5faf-135">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

4. <span data-ttu-id="f5faf-136">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="f5faf-136">Restart the sshd service</span></span>

   ```powershell
   Restart-Service sshd
   ```

5. <span data-ttu-id="f5faf-137">Az OpenSSH helyéül az elérési út Env változó az elérési út hozzáadása</span><span class="sxs-lookup"><span data-stu-id="f5faf-137">Add the path where OpenSSH is installed to your Path Env Variable</span></span>

   - <span data-ttu-id="f5faf-138">Ez a témakörgyűjtemény legyen `C:\Program Files\OpenSSH\`</span><span class="sxs-lookup"><span data-stu-id="f5faf-138">This should be along the lines of `C:\Program Files\OpenSSH\`</span></span>
   - <span data-ttu-id="f5faf-139">Ez lehetővé teszi a ssh.exe találhatók</span><span class="sxs-lookup"><span data-stu-id="f5faf-139">This allows for the ssh.exe to be found</span></span>

## <a name="setup-on-linux-ubuntu-1404-machine"></a><span data-ttu-id="f5faf-140">Telepítés Linux (Ubuntu 14.04) gépen</span><span class="sxs-lookup"><span data-stu-id="f5faf-140">Setup on Linux (Ubuntu 14.04) Machine</span></span>

1. <span data-ttu-id="f5faf-141">Telepítse a legújabb [a PowerShell Core for Linux] build a Githubról</span><span class="sxs-lookup"><span data-stu-id="f5faf-141">Install the latest [PowerShell Core for Linux] build from GitHub</span></span>
2. <span data-ttu-id="f5faf-142">Telepítése [Ubuntu SSH] igény szerint</span><span class="sxs-lookup"><span data-stu-id="f5faf-142">Install [Ubuntu SSH] as needed</span></span>

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. <span data-ttu-id="f5faf-143">Az sshd_config fájlban a következő helyen /etc/ssh szerkesztése</span><span class="sxs-lookup"><span data-stu-id="f5faf-143">Edit the sshd_config file at location /etc/ssh</span></span>

   - <span data-ttu-id="f5faf-144">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="f5faf-144">Make sure password authentication is enabled</span></span>

   ```
   PasswordAuthentication yes
   ```

   - <span data-ttu-id="f5faf-145">PowerShell alrendszer bejegyzés hozzáadása</span><span class="sxs-lookup"><span data-stu-id="f5faf-145">Add a PowerShell subsystem entry</span></span>

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - <span data-ttu-id="f5faf-146">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="f5faf-146">Optionally enable key authentication</span></span>

   ```
   PubkeyAuthentication yes
   ```

4. <span data-ttu-id="f5faf-147">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="f5faf-147">Restart the sshd service</span></span>

   ```bash
   sudo service sshd restart
   ```

## <a name="setup-on-macos-machine"></a><span data-ttu-id="f5faf-148">A MacOS rendszerű gépén beállítása</span><span class="sxs-lookup"><span data-stu-id="f5faf-148">Setup on MacOS Machine</span></span>

1. <span data-ttu-id="f5faf-149">Telepítse a legújabb [PowerShell Core for MacOS keretrendszert]-build</span><span class="sxs-lookup"><span data-stu-id="f5faf-149">Install the latest [PowerShell Core for MacOS] build</span></span>

   - <span data-ttu-id="f5faf-150">Győződjön meg arról, hogy SSH-távelérés engedélyezve van az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="f5faf-150">Make sure SSH Remoting is enabled by following these steps:</span></span>
     - <span data-ttu-id="f5faf-151">Nyissa meg `System Preferences`</span><span class="sxs-lookup"><span data-stu-id="f5faf-151">Open `System Preferences`</span></span>
     - <span data-ttu-id="f5faf-152">Kattintson a `Sharing`</span><span class="sxs-lookup"><span data-stu-id="f5faf-152">Click on `Sharing`</span></span>
     - <span data-ttu-id="f5faf-153">Ellenőrizze `Remote Login` – a következő: `Remote Login: On`</span><span class="sxs-lookup"><span data-stu-id="f5faf-153">Check `Remote Login` - Should say `Remote Login: On`</span></span>
     - <span data-ttu-id="f5faf-154">Megfelelő felhasználók férhessenek hozzá</span><span class="sxs-lookup"><span data-stu-id="f5faf-154">Allow access to appropriate users</span></span>

2. <span data-ttu-id="f5faf-155">Szerkessze a `sshd_config` helyen található fájl `/private/etc/ssh/sshd_config`</span><span class="sxs-lookup"><span data-stu-id="f5faf-155">Edit the `sshd_config` file at location `/private/etc/ssh/sshd_config`</span></span>

   - <span data-ttu-id="f5faf-156">Használja kedvenc szerkesztőjében, vagy</span><span class="sxs-lookup"><span data-stu-id="f5faf-156">Use your favorite editor or</span></span>

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - <span data-ttu-id="f5faf-157">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="f5faf-157">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

   - <span data-ttu-id="f5faf-158">PowerShell alrendszer bejegyzés hozzáadása</span><span class="sxs-lookup"><span data-stu-id="f5faf-158">Add a PowerShell subsystem entry</span></span>

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="f5faf-159">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="f5faf-159">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

3. <span data-ttu-id="f5faf-160">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="f5faf-160">Restart the sshd service</span></span>

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="powershell-remoting-example"></a><span data-ttu-id="f5faf-161">Távoli eljáráshívás a PowerShell-példa</span><span class="sxs-lookup"><span data-stu-id="f5faf-161">PowerShell Remoting Example</span></span>

<span data-ttu-id="f5faf-162">A legegyszerűbb módon távelérésének lehetővé tétele, hogy csak egyetlen gépen történő kipróbálására.</span><span class="sxs-lookup"><span data-stu-id="f5faf-162">The easiest way to test remoting is to just try it on a single machine.</span></span> <span data-ttu-id="f5faf-163">Itt I hoz létre vissza ugyanarra a gépre a távoli munkamenetet egy Linux-be.</span><span class="sxs-lookup"><span data-stu-id="f5faf-163">Here I will create a remote session back to the same machine on a Linux box.</span></span> <span data-ttu-id="f5faf-164">Figyelje meg, hogy egy parancssorból a PowerShell-parancsmagok használom, így láthatjuk, hogy SSH ellenőrzése a gazdaszámítógépen, valamint a jelszót utasításokat kéri az utasításokat.</span><span class="sxs-lookup"><span data-stu-id="f5faf-164">Notice that I am using PowerShell cmdlets from a command prompt so we see prompts from SSH asking to verify the host computer as well as password prompts.</span></span> <span data-ttu-id="f5faf-165">Egy Windows gépre van működik a távoli eljáráshívás biztosításához és a gépek a gazdagép neve egyszerűen módosításával közötti majd távoli ugyanezt teheti meg.</span><span class="sxs-lookup"><span data-stu-id="f5faf-165">You can do the same thing on a Windows machine to ensure remoting is working there and then remote between machines by simply changing the host name.</span></span>

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

### <a name="known-issues"></a><span data-ttu-id="f5faf-166">Ismert problémák</span><span class="sxs-lookup"><span data-stu-id="f5faf-166">Known Issues</span></span>

<span data-ttu-id="f5faf-167">A sudo parancs nem működik a távoli munkamenetet Linux rendszerű gépen.</span><span class="sxs-lookup"><span data-stu-id="f5faf-167">The sudo command does not work in remote session to Linux machine.</span></span>

## <a name="see-also"></a><span data-ttu-id="f5faf-168">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f5faf-168">See Also</span></span>

[<span data-ttu-id="f5faf-169">A Windows PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="f5faf-169">PowerShell Core for Windows</span></span>](../setup/installing-powershell-core-on-windows.md#msi)

[<span data-ttu-id="f5faf-170">A PowerShell Core linuxhoz</span><span class="sxs-lookup"><span data-stu-id="f5faf-170">PowerShell Core for Linux</span></span>](../setup/installing-powershell-core-on-linux.md#ubuntu-1404)

[<span data-ttu-id="f5faf-171">MacOS-hez a PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="f5faf-171">PowerShell Core for MacOS</span></span>](../setup/installing-powershell-core-on-macos.md)

[<span data-ttu-id="f5faf-172">A Win32-OpenSSH</span><span class="sxs-lookup"><span data-stu-id="f5faf-172">Win32 OpenSSH</span></span>](https://github.com/PowerShell/Win32-OpenSSH/releases)

[<span data-ttu-id="f5faf-173">telepítés</span><span class="sxs-lookup"><span data-stu-id="f5faf-173">installation</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

[<span data-ttu-id="f5faf-174">Ubuntu SSH</span><span class="sxs-lookup"><span data-stu-id="f5faf-174">Ubuntu SSH</span></span>](https://help.ubuntu.com/lts/serverguide/openssh-server.html)