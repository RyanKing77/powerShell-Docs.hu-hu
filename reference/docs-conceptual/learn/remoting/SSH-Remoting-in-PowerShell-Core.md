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
# <a name="powershell-remoting-over-ssh"></a><span data-ttu-id="30526-103">PowerShell távoli eljáráshívás SSH-n keresztül</span><span class="sxs-lookup"><span data-stu-id="30526-103">PowerShell Remoting Over SSH</span></span>

## <a name="overview"></a><span data-ttu-id="30526-104">Áttekintés</span><span class="sxs-lookup"><span data-stu-id="30526-104">Overview</span></span>

<span data-ttu-id="30526-105">A PowerShell távelérés általában a WinRM szolgáltatást használja a kapcsolatok egyeztetéséhez és az adatátvitelhez.</span><span class="sxs-lookup"><span data-stu-id="30526-105">PowerShell remoting normally uses WinRM for connection negotiation and data transport.</span></span> <span data-ttu-id="30526-106">Az SSH mostantól elérhető Linux és Windows platformokon, és lehetővé teszi a valódi többplatformos PowerShell-távelérést.</span><span class="sxs-lookup"><span data-stu-id="30526-106">SSH is now available for Linux and Windows platforms and allows true multiplatform PowerShell remoting.</span></span>

<span data-ttu-id="30526-107">A WinRM robusztus üzemeltetési modellt biztosít a PowerShell távoli munkameneteihez.</span><span class="sxs-lookup"><span data-stu-id="30526-107">WinRM provides a robust hosting model for PowerShell remote sessions.</span></span> <span data-ttu-id="30526-108">Az SSH-alapú távelérés jelenleg nem támogatja a távoli végpont-konfigurációt és a JEA (elég felügyelet).</span><span class="sxs-lookup"><span data-stu-id="30526-108">SSH-based remoting doesn't currently support remote endpoint configuration and JEA (Just Enough Administration).</span></span>

<span data-ttu-id="30526-109">Az SSH távoli eljáráshívás lehetővé teszi a Windows és Linux rendszerű gépek közötti alapszintű PowerShell-munkamenetek elvégzését.</span><span class="sxs-lookup"><span data-stu-id="30526-109">SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines.</span></span> <span data-ttu-id="30526-110">Az SSH távelérés egy PowerShell-gazdagépet hoz létre a célszámítógépen SSH alrendszerként.</span><span class="sxs-lookup"><span data-stu-id="30526-110">SSH Remoting creates a PowerShell host process on the target machine as an SSH subsystem.</span></span> <span data-ttu-id="30526-111">Végül a WinRM-hez hasonló általános üzemeltetési modellt fogunk megvalósítani a végpont-konfiguráció és a JEA támogatásához.</span><span class="sxs-lookup"><span data-stu-id="30526-111">Eventually we'll implement a general hosting model, similar to WinRM, to support endpoint configuration and JEA.</span></span>

<span data-ttu-id="30526-112">A `New-PSSession`, `Enter-PSSession`a és`Invoke-Command` a parancsmagok mostantól új paraméterrel rendelkeznek az új távelérési kapcsolatok támogatásához.</span><span class="sxs-lookup"><span data-stu-id="30526-112">The `New-PSSession`, `Enter-PSSession`, and `Invoke-Command` cmdlets now have a new parameter set to support this new remoting connection.</span></span>

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

<span data-ttu-id="30526-113">Távoli munkamenet létrehozásához adja meg a cél gépet `HostName` a paraméterrel, és adja meg a felhasználónevet `UserName`a következővel:.</span><span class="sxs-lookup"><span data-stu-id="30526-113">To create a remote session, you specify the target machine with the `HostName` parameter and provide the user name with `UserName`.</span></span> <span data-ttu-id="30526-114">A parancsmagok interaktív futtatásakor a rendszer jelszót kér.</span><span class="sxs-lookup"><span data-stu-id="30526-114">When running the cmdlets interactively, you're prompted for a password.</span></span> <span data-ttu-id="30526-115">Az `KeyFilePath` SSH-kulcsos hitelesítést a paraméterrel rendelkező titkos kulcsfájl használatával is használhatja.</span><span class="sxs-lookup"><span data-stu-id="30526-115">You can also, use SSH key authentication using a private key file with the `KeyFilePath` parameter.</span></span>

## <a name="general-setup-information"></a><span data-ttu-id="30526-116">Általános telepítési információk</span><span class="sxs-lookup"><span data-stu-id="30526-116">General setup information</span></span>

<span data-ttu-id="30526-117">Az SSH-t az összes gépen telepíteni kell.</span><span class="sxs-lookup"><span data-stu-id="30526-117">SSH must be installed on all machines.</span></span> <span data-ttu-id="30526-118">Telepítse az SSH-ügyfelet`ssh.exe`() és a`sshd.exe`kiszolgálót () is, hogy a gépekről és a számítógépekről is legyen távoli.</span><span class="sxs-lookup"><span data-stu-id="30526-118">Install both the SSH client (`ssh.exe`) and server (`sshd.exe`) so that you can remote to and from the machines.</span></span> <span data-ttu-id="30526-119">A Windowshoz készült OpenSSH mostantól elérhető a Windows 10 Build 1809 és a Windows Server 2019 rendszerben.</span><span class="sxs-lookup"><span data-stu-id="30526-119">OpenSSH for Windows is now available in Windows 10 build 1809 and Windows Server 2019.</span></span> <span data-ttu-id="30526-120">További információ: [OpenSSH for Windows](/windows-server/administration/openssh/openssh_overview).</span><span class="sxs-lookup"><span data-stu-id="30526-120">For more information, see [OpenSSH for Windows](/windows-server/administration/openssh/openssh_overview).</span></span> <span data-ttu-id="30526-121">Linux esetén telepítse a platformnak megfelelő SSH-t (beleértve az sshd-kiszolgálót is).</span><span class="sxs-lookup"><span data-stu-id="30526-121">For Linux, install SSH (including sshd server) appropriate to your platform.</span></span> <span data-ttu-id="30526-122">Telepítenie kell a PowerShell Core-t is a GitHubról az SSH távelérési szolgáltatásának beszerzéséhez.</span><span class="sxs-lookup"><span data-stu-id="30526-122">You also need to install PowerShell Core from GitHub to get the SSH remoting feature.</span></span> <span data-ttu-id="30526-123">Az SSH-kiszolgálót úgy kell konfigurálni, hogy hozzon létre egy SSH-alrendszert a távoli gépen futó PowerShell-folyamat futtatásához.</span><span class="sxs-lookup"><span data-stu-id="30526-123">The SSH server must be configured to create an SSH subsystem to host a PowerShell process on the remote machine.</span></span> <span data-ttu-id="30526-124">Emellett konfigurálnia kell a jelszó vagy a kulcs alapú hitelesítés engedélyezését is.</span><span class="sxs-lookup"><span data-stu-id="30526-124">You also must configure enable password or key-based authentication.</span></span>

## <a name="set-up-on-windows-machine"></a><span data-ttu-id="30526-125">Beállítás Windows rendszerű gépen</span><span class="sxs-lookup"><span data-stu-id="30526-125">Set up on Windows Machine</span></span>

1. <span data-ttu-id="30526-126">A [PowerShell Core for Windows](../../install/installing-powershell-core-on-windows.md#msi) legújabb verziójának telepítése</span><span class="sxs-lookup"><span data-stu-id="30526-126">Install the latest version of [PowerShell Core for Windows](../../install/installing-powershell-core-on-windows.md#msi)</span></span>

   - <span data-ttu-id="30526-127">Megtudhatja, hogy rendelkezik-e az SSH távelérési támogatással a következő paraméterekkel:`New-PSSession`</span><span class="sxs-lookup"><span data-stu-id="30526-127">You can tell if it has the SSH remoting support by looking at the parameter sets for `New-PSSession`</span></span>

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. <span data-ttu-id="30526-128">Telepítse a legújabb Win32 OpenSSH-t.</span><span class="sxs-lookup"><span data-stu-id="30526-128">Install the latest Win32 OpenSSH.</span></span> <span data-ttu-id="30526-129">A telepítési utasításokért lásd: [az OpenSSH telepítése](/windows-server/administration/openssh/openssh_install_firstuse).</span><span class="sxs-lookup"><span data-stu-id="30526-129">For installation instructions, see [Installation of OpenSSH](/windows-server/administration/openssh/openssh_install_firstuse).</span></span>
3. <span data-ttu-id="30526-130">Szerkessze `sshd_config` a következő helyen `$env:ProgramData\ssh`található fájlt:.</span><span class="sxs-lookup"><span data-stu-id="30526-130">Edit the `sshd_config` file located at `$env:ProgramData\ssh`.</span></span>

   - <span data-ttu-id="30526-131">Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van</span><span class="sxs-lookup"><span data-stu-id="30526-131">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > <span data-ttu-id="30526-132">Hiba történt a Windows OpenSSH-ban, amely megakadályozza, hogy a szóközök nem működnek az alrendszer végrehajtható fájljainak elérési útjain.</span><span class="sxs-lookup"><span data-stu-id="30526-132">There is a bug in OpenSSH for Windows that prevents spaces from working in subsystem executable paths.</span></span> <span data-ttu-id="30526-133">További információkért tekintse meg [ezt a GitHub-problémát](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span><span class="sxs-lookup"><span data-stu-id="30526-133">For more information, see [this GitHub issue](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span></span>

     <span data-ttu-id="30526-134">Az egyik megoldás egy olyan symlink létrehozása a PowerShell telepítési könyvtárához, amely nem rendelkezik szóközökkel:</span><span class="sxs-lookup"><span data-stu-id="30526-134">One solution is to create a symlink to the PowerShell installation directory that doesn't have spaces:</span></span>

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6"
     ```

     <span data-ttu-id="30526-135">majd írja be az alrendszerbe:</span><span class="sxs-lookup"><span data-stu-id="30526-135">and then enter it in the subsystem:</span></span>

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="30526-136">Kulcsos hitelesítés opcionális engedélyezése</span><span class="sxs-lookup"><span data-stu-id="30526-136">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

4. <span data-ttu-id="30526-137">Az sshd szolgáltatás újraindítása</span><span class="sxs-lookup"><span data-stu-id="30526-137">Restart the sshd service</span></span>

   ```powershell
   Restart-Service sshd
   ```

5. <span data-ttu-id="30526-138">Adja meg az elérési utat, ahol az OpenSSH telepítve van a PATH környezeti változóba.</span><span class="sxs-lookup"><span data-stu-id="30526-138">Add the path where OpenSSH is installed to your Path environment variable.</span></span> <span data-ttu-id="30526-139">Például: `C:\Program Files\OpenSSH\`.</span><span class="sxs-lookup"><span data-stu-id="30526-139">For example, `C:\Program Files\OpenSSH\`.</span></span> <span data-ttu-id="30526-140">Ez a bejegyzés lehetővé teszi az SSH. exe megkeresését.</span><span class="sxs-lookup"><span data-stu-id="30526-140">This entry allows for the ssh.exe to be found.</span></span>

## <a name="set-up-on-linux-ubuntu-1604-machine"></a><span data-ttu-id="30526-141">Beállítás Linux (Ubuntu 16,04) rendszerű gépen</span><span class="sxs-lookup"><span data-stu-id="30526-141">Set up on Linux (Ubuntu 16.04) Machine</span></span>

1. <span data-ttu-id="30526-142">Telepítse a legújabb [PowerShell Core for Linux](../../install/installing-powershell-core-on-linux.md#ubuntu-1604) buildet a githubról</span><span class="sxs-lookup"><span data-stu-id="30526-142">Install the latest [PowerShell Core for Linux](../../install/installing-powershell-core-on-linux.md#ubuntu-1604) build from GitHub</span></span>
2. <span data-ttu-id="30526-143">[Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html) telepítése igény szerint</span><span class="sxs-lookup"><span data-stu-id="30526-143">Install [Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html) as needed</span></span>

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. <span data-ttu-id="30526-144">A sshd_config-fájl szerkesztése a következő helyen:/etc/ssh</span><span class="sxs-lookup"><span data-stu-id="30526-144">Edit the sshd_config file at location /etc/ssh</span></span>

   - <span data-ttu-id="30526-145">Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van</span><span class="sxs-lookup"><span data-stu-id="30526-145">Make sure password authentication is enabled</span></span>

   ```
   PasswordAuthentication yes
   ```

   - <span data-ttu-id="30526-146">PowerShell alrendszer bejegyzésének hozzáadása</span><span class="sxs-lookup"><span data-stu-id="30526-146">Add a PowerShell subsystem entry</span></span>

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - <span data-ttu-id="30526-147">Kulcsos hitelesítés opcionális engedélyezése</span><span class="sxs-lookup"><span data-stu-id="30526-147">Optionally enable key authentication</span></span>

   ```
   PubkeyAuthentication yes
   ```

4. <span data-ttu-id="30526-148">Az sshd szolgáltatás újraindítása</span><span class="sxs-lookup"><span data-stu-id="30526-148">Restart the sshd service</span></span>

   ```bash
   sudo service sshd restart
   ```

## <a name="set-up-on-macos-machine"></a><span data-ttu-id="30526-149">Beállítás MacOS rendszerű gépen</span><span class="sxs-lookup"><span data-stu-id="30526-149">Set up on MacOS Machine</span></span>

1. <span data-ttu-id="30526-150">A legújabb [PowerShell-mag telepítése MacOS](../../install/installing-powershell-core-on-macos.md) -buildhez</span><span class="sxs-lookup"><span data-stu-id="30526-150">Install the latest [PowerShell Core for MacOS](../../install/installing-powershell-core-on-macos.md) build</span></span>

   - <span data-ttu-id="30526-151">Győződjön meg arról, hogy az SSH távelérés engedélyezve van a következő lépések végrehajtásával:</span><span class="sxs-lookup"><span data-stu-id="30526-151">Make sure SSH Remoting is enabled by following these steps:</span></span>
     - <span data-ttu-id="30526-152">Nyissa meg`System Preferences`</span><span class="sxs-lookup"><span data-stu-id="30526-152">Open `System Preferences`</span></span>
     - <span data-ttu-id="30526-153">Kattintson a`Sharing`</span><span class="sxs-lookup"><span data-stu-id="30526-153">Click on `Sharing`</span></span>
     - <span data-ttu-id="30526-154">Be `Remote Login` kell mondani`Remote Login: On`</span><span class="sxs-lookup"><span data-stu-id="30526-154">Check `Remote Login` - Should say `Remote Login: On`</span></span>
     - <span data-ttu-id="30526-155">A megfelelő felhasználók hozzáférésének engedélyezése</span><span class="sxs-lookup"><span data-stu-id="30526-155">Allow access to appropriate users</span></span>

2. <span data-ttu-id="30526-156">A fájl `sshd_config` szerkesztése a helyen`/private/etc/ssh/sshd_config`</span><span class="sxs-lookup"><span data-stu-id="30526-156">Edit the `sshd_config` file at location `/private/etc/ssh/sshd_config`</span></span>

   - <span data-ttu-id="30526-157">Használja kedvenc szerkesztőjét vagy</span><span class="sxs-lookup"><span data-stu-id="30526-157">Use your favorite editor or</span></span>

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - <span data-ttu-id="30526-158">Győződjön meg arról, hogy a jelszó-hitelesítés engedélyezve van</span><span class="sxs-lookup"><span data-stu-id="30526-158">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

   - <span data-ttu-id="30526-159">PowerShell alrendszer bejegyzésének hozzáadása</span><span class="sxs-lookup"><span data-stu-id="30526-159">Add a PowerShell subsystem entry</span></span>

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="30526-160">Kulcsos hitelesítés opcionális engedélyezése</span><span class="sxs-lookup"><span data-stu-id="30526-160">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

3. <span data-ttu-id="30526-161">Az sshd szolgáltatás újraindítása</span><span class="sxs-lookup"><span data-stu-id="30526-161">Restart the sshd service</span></span>

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="authentication"></a><span data-ttu-id="30526-162">Hitelesítés</span><span class="sxs-lookup"><span data-stu-id="30526-162">Authentication</span></span>

<span data-ttu-id="30526-163">A PowerShell távoli SSH-kapcsolaton keresztüli hitelesítése az SSH-ügyfél és az SSH-szolgáltatás közötti hitelesítési Exchange-re támaszkodik, és nem valósít meg saját hitelesítési sémákat.</span><span class="sxs-lookup"><span data-stu-id="30526-163">PowerShell remoting over SSH relies on the authentication exchange between the SSH client and SSH service and does not implement any authentication schemes itself.</span></span> <span data-ttu-id="30526-164">Ez azt jelenti, hogy minden konfigurált hitelesítési sémát, beleértve a többtényezős hitelesítést, az SSH és a PowerShelltől függetlenül kezeli.</span><span class="sxs-lookup"><span data-stu-id="30526-164">This means that any configured authentication schemes including multi-factor authentication is handled by SSH and independent of PowerShell.</span></span> <span data-ttu-id="30526-165">Beállíthatja például, hogy az SSH szolgáltatás nyilvános kulcsú hitelesítésre, valamint egy egyszeri jelszóra legyen szükség a további biztonság érdekében.</span><span class="sxs-lookup"><span data-stu-id="30526-165">For example, you can configure the SSH service to require public key authentication as well as a one-time password for added security.</span></span> <span data-ttu-id="30526-166">A többtényezős hitelesítés konfigurációja kívül esik a dokumentáció hatókörén.</span><span class="sxs-lookup"><span data-stu-id="30526-166">Configuration of multi-factor authentication is outside the scope of this documentation.</span></span> <span data-ttu-id="30526-167">A többtényezős hitelesítés helyes konfigurálásához és a PowerShellen kívüli működésének ellenőrzéséhez tekintse meg az SSH dokumentációját, mielőtt a PowerShell távelérési szolgáltatással próbálja használni.</span><span class="sxs-lookup"><span data-stu-id="30526-167">Refer to documentation for SSH on how to correctly configure multi-factor authentication and validate it works outside of PowerShell before attempting to use it with PowerShell remoting.</span></span>

## <a name="powershell-remoting-example"></a><span data-ttu-id="30526-168">PowerShell-távelérés – példa</span><span class="sxs-lookup"><span data-stu-id="30526-168">PowerShell Remoting Example</span></span>

<span data-ttu-id="30526-169">A távelérés tesztelésének legegyszerűbb módja, ha egyetlen gépen próbálja ki.</span><span class="sxs-lookup"><span data-stu-id="30526-169">The easiest way to test remoting is to try it on a single machine.</span></span> <span data-ttu-id="30526-170">Ebben a példában egy távoli munkamenetet hozunk létre ugyanarra a Linux-gépre.</span><span class="sxs-lookup"><span data-stu-id="30526-170">In this example, we create a remote session back to the same Linux machine.</span></span> <span data-ttu-id="30526-171">A PowerShell-parancsmagokat interaktívan használjuk, ezért a rendszer kéri az SSH-t, hogy ellenőrizze a gazdaszámítógép ellenőrzését és a jelszó megadását.</span><span class="sxs-lookup"><span data-stu-id="30526-171">We are using PowerShell cmdlets interactively so we see prompts from SSH asking to verify the host computer and prompting for a password.</span></span> <span data-ttu-id="30526-172">Ugyanezt megteheti a Windows rendszerű gépen is a távelérés működésének biztosításához.</span><span class="sxs-lookup"><span data-stu-id="30526-172">You can do the same thing on a Windows machine to ensure remoting is working.</span></span> <span data-ttu-id="30526-173">Ezután a gépek közötti távoli kapcsolat megváltoztatásával adja meg a gazdagép nevét.</span><span class="sxs-lookup"><span data-stu-id="30526-173">Then remote between machines by changing the host name.</span></span>

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

### <a name="known-issues"></a><span data-ttu-id="30526-174">Ismert problémák</span><span class="sxs-lookup"><span data-stu-id="30526-174">Known Issues</span></span>

<span data-ttu-id="30526-175">A sudo parancs nem működik a távoli munkamenetben a Linux rendszerű gépeken.</span><span class="sxs-lookup"><span data-stu-id="30526-175">The sudo command doesn't work in remote session to Linux machine.</span></span>

## <a name="see-also"></a><span data-ttu-id="30526-176">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="30526-176">See Also</span></span>

[<span data-ttu-id="30526-177">Windows PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="30526-177">PowerShell Core for Windows</span></span>](../../install/installing-powershell-core-on-windows.md#msi)

[<span data-ttu-id="30526-178">A Linux PowerShell-magja</span><span class="sxs-lookup"><span data-stu-id="30526-178">PowerShell Core for Linux</span></span>](../../install/installing-powershell-core-on-linux.md#ubuntu-1604)

[<span data-ttu-id="30526-179">A MacOS-hez készült PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="30526-179">PowerShell Core for MacOS</span></span>](../../install/installing-powershell-core-on-macos.md)

[<span data-ttu-id="30526-180">Windowsos OpenSSH</span><span class="sxs-lookup"><span data-stu-id="30526-180">OpenSSH for Windows</span></span>](/windows-server/administration/openssh/openssh_overview)

[<span data-ttu-id="30526-181">Ubuntu SSH</span><span class="sxs-lookup"><span data-stu-id="30526-181">Ubuntu SSH</span></span>](https://help.ubuntu.com/lts/serverguide/openssh-server.html)
