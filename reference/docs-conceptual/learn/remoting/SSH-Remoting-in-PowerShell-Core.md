---
title: PowerShell távoli eljáráshívás SSH-n keresztül
description: Távoli eljáráshívás a PowerShell Core SSH-val
ms.date: 08/14/2018
ms.openlocfilehash: b5c6bd70841e270c2c128601612c07af9d9aa6e4
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655293"
---
# <a name="powershell-remoting-over-ssh"></a><span data-ttu-id="77f45-103">PowerShell távoli eljáráshívás SSH-n keresztül</span><span class="sxs-lookup"><span data-stu-id="77f45-103">PowerShell Remoting Over SSH</span></span>

## <a name="overview"></a><span data-ttu-id="77f45-104">Áttekintés</span><span class="sxs-lookup"><span data-stu-id="77f45-104">Overview</span></span>

<span data-ttu-id="77f45-105">PowerShell távoli eljáráshívás általában winrm funkciót használ a kapcsolat egyeztetési és adatátvitel.</span><span class="sxs-lookup"><span data-stu-id="77f45-105">PowerShell remoting normally uses WinRM for connection negotiation and data transport.</span></span> <span data-ttu-id="77f45-106">Az SSH Linux és Windows platformokon elérhető, és lehetővé teszi a valódi többplatformos PowerShell távoli eljáráshívás.</span><span class="sxs-lookup"><span data-stu-id="77f45-106">SSH is now available for Linux and Windows platforms and allows true multiplatform PowerShell remoting.</span></span>

<span data-ttu-id="77f45-107">A Rendszerfelügyeleti webszolgáltatások egy robusztus üzemeltetési modellt biztosít a távoli PowerShell-munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="77f45-107">WinRM provides a robust hosting model for PowerShell remote sessions.</span></span> <span data-ttu-id="77f45-108">Távoli eljáráshívás SSH-alapú jelenleg nem támogatja a távoli végpont-konfiguráció és a JEA (Just Enough Administration).</span><span class="sxs-lookup"><span data-stu-id="77f45-108">SSH-based remoting doesn't currently support remote endpoint configuration and JEA (Just Enough Administration).</span></span>

<span data-ttu-id="77f45-109">Az SSH a távelérés lehetővé teszi egyszerű PowerShell-munkamenet távelérés Windows és Linux gép között.</span><span class="sxs-lookup"><span data-stu-id="77f45-109">SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines.</span></span> <span data-ttu-id="77f45-110">SSH távoli eljáráshívás hoz létre, mint egy SSH-alrendszer egy PowerShell gazdafolyamat a célgépen.</span><span class="sxs-lookup"><span data-stu-id="77f45-110">SSH Remoting creates a PowerShell host process on the target machine as an SSH subsystem.</span></span>
<span data-ttu-id="77f45-111">Végül hoznunk egy általános üzemeltetési modell, a Rendszerfelügyeleti webszolgáltatások, a végpont-konfiguráció és a JEA hasonló lesz.</span><span class="sxs-lookup"><span data-stu-id="77f45-111">Eventually we'll implement a general hosting model, similar to WinRM, to support endpoint configuration and JEA.</span></span>

<span data-ttu-id="77f45-112">A `New-PSSession`, `Enter-PSSession`, és `Invoke-Command` parancsmagok most már támogatja az új távelérési kapcsolat új paramétert.</span><span class="sxs-lookup"><span data-stu-id="77f45-112">The `New-PSSession`, `Enter-PSSession`, and `Invoke-Command` cmdlets now have a new parameter set to support this new remoting connection.</span></span>

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

<span data-ttu-id="77f45-113">Hozzon létre egy távoli munkamenetet, adja meg a célszámítógépen a `HostName` paramétert, és adja meg a felhasználónevet, `UserName`.</span><span class="sxs-lookup"><span data-stu-id="77f45-113">To create a remote session, you specify the target machine with the `HostName` parameter and provide the user name with `UserName`.</span></span> <span data-ttu-id="77f45-114">Amikor interaktívan futtatja a parancsmagok, kéri a jelszót.</span><span class="sxs-lookup"><span data-stu-id="77f45-114">When running the cmdlets interactively, you're prompted for a password.</span></span> <span data-ttu-id="77f45-115">Emellett, a titkos kulcsfájl használata SSH kulcsos hitelesítést a `KeyFilePath` paraméter.</span><span class="sxs-lookup"><span data-stu-id="77f45-115">You can also, use SSH key authentication using a private key file with the `KeyFilePath` parameter.</span></span>

## <a name="general-setup-information"></a><span data-ttu-id="77f45-116">Általános beállítási adatok</span><span class="sxs-lookup"><span data-stu-id="77f45-116">General setup information</span></span>

<span data-ttu-id="77f45-117">SSH minden gépen telepítve kell lennie.</span><span class="sxs-lookup"><span data-stu-id="77f45-117">SSH must be installed on all machines.</span></span> <span data-ttu-id="77f45-118">Mindkét az SSH-ügyfél telepítése (`ssh.exe`) és a kiszolgáló (`sshd.exe`) segítségével távoli, és onnan a gépek.</span><span class="sxs-lookup"><span data-stu-id="77f45-118">Install both the SSH client (`ssh.exe`) and server (`sshd.exe`) so that you can remote to and from the machines.</span></span> <span data-ttu-id="77f45-119">Az OpenSSH for Windows már rendelkezésre álló, a Windows 10-es build 1809 és a Windows Server 2019.</span><span class="sxs-lookup"><span data-stu-id="77f45-119">OpenSSH for Windows is now availabe in Windows 10 build 1809 and Windows Server 2019.</span></span> <span data-ttu-id="77f45-120">További információkért lásd: [OpenSSH for Windows](/windows-server/administration/openssh/openssh_overview).</span><span class="sxs-lookup"><span data-stu-id="77f45-120">For more information, see [OpenSSH for Windows](/windows-server/administration/openssh/openssh_overview).</span></span> <span data-ttu-id="77f45-121">A Linux telepítse az SSH (beleértve sshd-kiszolgálót) a platformjának megfelelő.</span><span class="sxs-lookup"><span data-stu-id="77f45-121">For Linux, install SSH (including sshd server) appropriate to your platform.</span></span> <span data-ttu-id="77f45-122">Emellett telepítenie kell a PowerShell Core a Githubról, a távoli eljáráshívás SSH szolgáltatás beolvasása.</span><span class="sxs-lookup"><span data-stu-id="77f45-122">You also need to install PowerShell Core from GitHub to get the SSH remoting feature.</span></span> <span data-ttu-id="77f45-123">Az SSH-kiszolgálót úgy kell konfigurálni, egy SSH-alrendszer üzemeltetéséhez a távoli gépen egy PowerShell-folyamat létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="77f45-123">The SSH server must be configured to create an SSH subsystem to host a PowerShell process on the remote machine.</span></span> <span data-ttu-id="77f45-124">Emellett konfigurálnia kell jelszó engedélyezése vagy kulcs alapú hitelesítés.</span><span class="sxs-lookup"><span data-stu-id="77f45-124">You also must configure enable password or key-based authentication.</span></span>

## <a name="set-up-on-windows-machine"></a><span data-ttu-id="77f45-125">Windows-gépen beállítása</span><span class="sxs-lookup"><span data-stu-id="77f45-125">Set up on Windows Machine</span></span>

1. <span data-ttu-id="77f45-126">Telepítse a legújabb verzióját, [a Windows PowerShell Core](../../install/installing-powershell-core-on-windows.md#msi)</span><span class="sxs-lookup"><span data-stu-id="77f45-126">Install the latest version of [PowerShell Core for Windows](../../install/installing-powershell-core-on-windows.md#msi)</span></span>

   - <span data-ttu-id="77f45-127">Is megadhatja, hogy a távoli eljáráshívás SSH-támogatás, ha megnézzük a paraméterkészletek számára `New-PSSession`</span><span class="sxs-lookup"><span data-stu-id="77f45-127">You can tell if it has the SSH remoting support by looking at the parameter sets for `New-PSSession`</span></span>

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. <span data-ttu-id="77f45-128">Telepítse a legújabb Win32-OpenSSH.</span><span class="sxs-lookup"><span data-stu-id="77f45-128">Install the latest Win32 OpenSSH.</span></span> <span data-ttu-id="77f45-129">A telepítési utasításokért lásd: [telepítési az OpenSSH](/windows-server/administration/openssh/openssh_install_firstuse).</span><span class="sxs-lookup"><span data-stu-id="77f45-129">For installation instructions, see [Installation of OpenSSH](/windows-server/administration/openssh/openssh_install_firstuse).</span></span>
3. <span data-ttu-id="77f45-130">Szerkessze a `sshd_config` helyen található fájl `%ProgramData%\ssh`.</span><span class="sxs-lookup"><span data-stu-id="77f45-130">Edit the `sshd_config` file located at `%ProgramData%\ssh`.</span></span>

   - <span data-ttu-id="77f45-131">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="77f45-131">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > <span data-ttu-id="77f45-132">Az OpenSSH a Windows, amely megakadályozza, hogy a tárolóhelyek alrendszer végrehajtható elérési utak használata programhiba van.</span><span class="sxs-lookup"><span data-stu-id="77f45-132">There is a bug in OpenSSH for Windows that prevents spaces from working in subsystem executable paths.</span></span> <span data-ttu-id="77f45-133">További információkért lásd: [a GitHub-problémát](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span><span class="sxs-lookup"><span data-stu-id="77f45-133">For more information, see [this GitHub issue](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span></span>

     <span data-ttu-id="77f45-134">Az egyik megoldás, a Powershell telepítési könyvtárát, amely nem rendelkezik a tárolóhelyek szimbolikus létrehozásához:</span><span class="sxs-lookup"><span data-stu-id="77f45-134">One solution is to create a symlink to the Powershell installation directory that doesn't have spaces:</span></span>

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6"
     ```

     <span data-ttu-id="77f45-135">és a alrendszer írja be:</span><span class="sxs-lookup"><span data-stu-id="77f45-135">and then enter it in the subsystem:</span></span>

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="77f45-136">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="77f45-136">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

4. <span data-ttu-id="77f45-137">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="77f45-137">Restart the sshd service</span></span>

   ```powershell
   Restart-Service sshd
   ```

5. <span data-ttu-id="77f45-138">Adja hozzá az elérési útját a Path környezeti változóba OpenSSH helyéül.</span><span class="sxs-lookup"><span data-stu-id="77f45-138">Add the path where OpenSSH is installed to your Path environment variable.</span></span> <span data-ttu-id="77f45-139">Például: `C:\Program Files\OpenSSH\`.</span><span class="sxs-lookup"><span data-stu-id="77f45-139">For example, `C:\Program Files\OpenSSH\`.</span></span> <span data-ttu-id="77f45-140">Ez a bejegyzés lehetővé teszi a ssh.exe is meg lehet találni.</span><span class="sxs-lookup"><span data-stu-id="77f45-140">This entry allows for the ssh.exe to be found.</span></span>

## <a name="set-up-on-linux-ubuntu-1404-machine"></a><span data-ttu-id="77f45-141">Állítsa be a Linux (Ubuntu 14.04) gépen</span><span class="sxs-lookup"><span data-stu-id="77f45-141">Set up on Linux (Ubuntu 14.04) Machine</span></span>

1. <span data-ttu-id="77f45-142">Telepítse a legújabb [PowerShell Core for Linux](../../install/installing-powershell-core-on-linux.md#ubuntu-1404) létrehozása a Githubról</span><span class="sxs-lookup"><span data-stu-id="77f45-142">Install the latest [PowerShell Core for Linux](../../install/installing-powershell-core-on-linux.md#ubuntu-1404) build from GitHub</span></span>
2. <span data-ttu-id="77f45-143">Telepítés [Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html) igény szerint</span><span class="sxs-lookup"><span data-stu-id="77f45-143">Install [Ubuntu SSH](https://help.ubuntu.com/lts/serverguide/openssh-server.html) as needed</span></span>

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. <span data-ttu-id="77f45-144">Az sshd_config fájlban a következő helyen /etc/ssh szerkesztése</span><span class="sxs-lookup"><span data-stu-id="77f45-144">Edit the sshd_config file at location /etc/ssh</span></span>

   - <span data-ttu-id="77f45-145">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="77f45-145">Make sure password authentication is enabled</span></span>

   ```
   PasswordAuthentication yes
   ```

   - <span data-ttu-id="77f45-146">PowerShell alrendszer bejegyzés hozzáadása</span><span class="sxs-lookup"><span data-stu-id="77f45-146">Add a PowerShell subsystem entry</span></span>

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - <span data-ttu-id="77f45-147">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="77f45-147">Optionally enable key authentication</span></span>

   ```
   PubkeyAuthentication yes
   ```

4. <span data-ttu-id="77f45-148">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="77f45-148">Restart the sshd service</span></span>

   ```bash
   sudo service sshd restart
   ```

## <a name="set-up-on-macos-machine"></a><span data-ttu-id="77f45-149">Állítsa be a MacOS rendszerű gépén</span><span class="sxs-lookup"><span data-stu-id="77f45-149">Set up on MacOS Machine</span></span>

1. <span data-ttu-id="77f45-150">Telepítse a legújabb [MacOS-hez a PowerShell Core](../../install/installing-powershell-core-on-macos.md) összeállítása</span><span class="sxs-lookup"><span data-stu-id="77f45-150">Install the latest [PowerShell Core for MacOS](../../install/installing-powershell-core-on-macos.md) build</span></span>

   - <span data-ttu-id="77f45-151">Győződjön meg arról, hogy SSH-távelérés engedélyezve van az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="77f45-151">Make sure SSH Remoting is enabled by following these steps:</span></span>
     - <span data-ttu-id="77f45-152">Nyissa meg `System Preferences`</span><span class="sxs-lookup"><span data-stu-id="77f45-152">Open `System Preferences`</span></span>
     - <span data-ttu-id="77f45-153">Kattintson a `Sharing`</span><span class="sxs-lookup"><span data-stu-id="77f45-153">Click on `Sharing`</span></span>
     - <span data-ttu-id="77f45-154">Ellenőrizze `Remote Login` – a következő: `Remote Login: On`</span><span class="sxs-lookup"><span data-stu-id="77f45-154">Check `Remote Login` - Should say `Remote Login: On`</span></span>
     - <span data-ttu-id="77f45-155">Megfelelő felhasználók férhessenek hozzá</span><span class="sxs-lookup"><span data-stu-id="77f45-155">Allow access to appropriate users</span></span>

2. <span data-ttu-id="77f45-156">Szerkessze a `sshd_config` helyen található fájl `/private/etc/ssh/sshd_config`</span><span class="sxs-lookup"><span data-stu-id="77f45-156">Edit the `sshd_config` file at location `/private/etc/ssh/sshd_config`</span></span>

   - <span data-ttu-id="77f45-157">Használja kedvenc szerkesztőjében, vagy</span><span class="sxs-lookup"><span data-stu-id="77f45-157">Use your favorite editor or</span></span>

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - <span data-ttu-id="77f45-158">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="77f45-158">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

   - <span data-ttu-id="77f45-159">PowerShell alrendszer bejegyzés hozzáadása</span><span class="sxs-lookup"><span data-stu-id="77f45-159">Add a PowerShell subsystem entry</span></span>

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="77f45-160">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="77f45-160">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

3. <span data-ttu-id="77f45-161">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="77f45-161">Restart the sshd service</span></span>

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="authentication"></a><span data-ttu-id="77f45-162">Hitelesítés</span><span class="sxs-lookup"><span data-stu-id="77f45-162">Authentication</span></span>

<span data-ttu-id="77f45-163">PowerShell távoli eljáráshívás ssh-n keresztül az SSH-ügyfél és az SSH-szolgáltatást között a hitelesítési csere támaszkodik, és nem valósítja meg a hitelesítési sémát magát.</span><span class="sxs-lookup"><span data-stu-id="77f45-163">PowerShell remoting over SSH relies on the authentication exchange between the SSH client and SSH service and does not implement any authentication schemes itself.</span></span>
<span data-ttu-id="77f45-164">Ez azt jelenti, hogy többek között a multi-factor authentication szolgáltatáshoz beállított hitelesítési sémát az SSH és PowerShell függetlenül történik.</span><span class="sxs-lookup"><span data-stu-id="77f45-164">This means that any configured authentication schemes including multi-factor authentication is handled by SSH and independent of PowerShell.</span></span>
<span data-ttu-id="77f45-165">Például konfigurálhatja a nyilvános kulcsos hitelesítés, valamint az egyszeri jelszó megkövetelése a fokozott biztonság az SSH-szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="77f45-165">For example, you can configure the SSH service to require public key authentication as well as a one-time password for added security.</span></span>
<span data-ttu-id="77f45-166">A multi-factor authentication konfigurálása az ebben a dokumentációban hatókörén kívül számára.</span><span class="sxs-lookup"><span data-stu-id="77f45-166">Configuration of multi-factor authentication is outside the scope of this documentation.</span></span>
<span data-ttu-id="77f45-167">Hogyan kell megfelelően multi-factor authentication konfigurálásához, és a PowerShell-en kívül működik, a PowerShell-táveléréssel használata előtt az SSH számára dokumentációban tájékozódhat.</span><span class="sxs-lookup"><span data-stu-id="77f45-167">Refer to documentation for SSH on how to correctly configure multi-factor authentication and validate it works outside of PowerShell before attempting to use it with PowerShell remoting.</span></span>

## <a name="powershell-remoting-example"></a><span data-ttu-id="77f45-168">Távoli eljáráshívás a PowerShell-példa</span><span class="sxs-lookup"><span data-stu-id="77f45-168">PowerShell Remoting Example</span></span>

<span data-ttu-id="77f45-169">A legegyszerűbb módon távelérésének lehetővé tétele, hogy egyetlen gépen kipróbálására.</span><span class="sxs-lookup"><span data-stu-id="77f45-169">The easiest way to test remoting is to try it on a single machine.</span></span> <span data-ttu-id="77f45-170">Ebben a példában létrehozunk egy távoli munkamenetet vissza ugyanaz a Linux rendszerű gép.</span><span class="sxs-lookup"><span data-stu-id="77f45-170">In this example, we create a remote session back to the same Linux machine.</span></span> <span data-ttu-id="77f45-171">PowerShell-parancsmagok interaktív módon, így láthatjuk, kérni fogja az SSH kéri ellenőrzése a gazdaszámítógépen, és a jelszót kérő üzenet használjuk.</span><span class="sxs-lookup"><span data-stu-id="77f45-171">We are using PowerShell cmdlets interactively so we see prompts from SSH asking to verify the host computer and prompting for a password.</span></span> <span data-ttu-id="77f45-172">Megteheti ugyanezt egy Windows-gépen annak érdekében, hogy működik a távoli eljáráshívás.</span><span class="sxs-lookup"><span data-stu-id="77f45-172">You can do the same thing on a Windows machine to ensure remoting is working.</span></span> <span data-ttu-id="77f45-173">Aztán távoli állomásnév módosításával gépek között.</span><span class="sxs-lookup"><span data-stu-id="77f45-173">Then remote between machines by changing the host name.</span></span>

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

### <a name="known-issues"></a><span data-ttu-id="77f45-174">Ismert problémák</span><span class="sxs-lookup"><span data-stu-id="77f45-174">Known Issues</span></span>

<span data-ttu-id="77f45-175">A sudo parancs nem működik a távoli munkamenet Linux rendszerű gépen.</span><span class="sxs-lookup"><span data-stu-id="77f45-175">The sudo command doesn't work in remote session to Linux machine.</span></span>

## <a name="see-also"></a><span data-ttu-id="77f45-176">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="77f45-176">See Also</span></span>

[<span data-ttu-id="77f45-177">A Windows PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="77f45-177">PowerShell Core for Windows</span></span>](../../install/installing-powershell-core-on-windows.md#msi)

[<span data-ttu-id="77f45-178">A PowerShell Core linuxhoz</span><span class="sxs-lookup"><span data-stu-id="77f45-178">PowerShell Core for Linux</span></span>](../../install/installing-powershell-core-on-linux.md#ubuntu-1404)

[<span data-ttu-id="77f45-179">MacOS-hez a PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="77f45-179">PowerShell Core for MacOS</span></span>](../../install/installing-powershell-core-on-macos.md)

[<span data-ttu-id="77f45-180">A Windows OpenSSH</span><span class="sxs-lookup"><span data-stu-id="77f45-180">OpenSSH for Windows</span></span>](/windows-server/administration/openssh/openssh_overview)

[<span data-ttu-id="77f45-181">Ubuntu SSH</span><span class="sxs-lookup"><span data-stu-id="77f45-181">Ubuntu SSH</span></span>](https://help.ubuntu.com/lts/serverguide/openssh-server.html)
