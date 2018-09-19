---
title: PowerShell távoli eljáráshívás SSH-n keresztül
description: Távoli eljáráshívás a PowerShell Core SSH-val
ms.date: 08/14/2018
ms.openlocfilehash: 451a55a588381cc9bec265895b2bfad6b6f6e73c
ms.sourcegitcommit: a652b12a0b87cdd0c8eb76381ae015467dd7b8cd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/18/2018
ms.locfileid: "46134280"
---
# <a name="powershell-remoting-over-ssh"></a><span data-ttu-id="e26da-103">PowerShell távoli eljáráshívás SSH-n keresztül</span><span class="sxs-lookup"><span data-stu-id="e26da-103">PowerShell Remoting Over SSH</span></span>

## <a name="overview"></a><span data-ttu-id="e26da-104">Áttekintés</span><span class="sxs-lookup"><span data-stu-id="e26da-104">Overview</span></span>

<span data-ttu-id="e26da-105">PowerShell távoli eljáráshívás általában winrm funkciót használ a kapcsolat egyeztetési és adatátvitel.</span><span class="sxs-lookup"><span data-stu-id="e26da-105">PowerShell remoting normally uses WinRM for connection negotiation and data transport.</span></span> <span data-ttu-id="e26da-106">Az SSH Linux és Windows platformokon elérhető, és lehetővé teszi a valódi többplatformos PowerShell távoli eljáráshívás.</span><span class="sxs-lookup"><span data-stu-id="e26da-106">SSH is now available for Linux and Windows platforms and allows true multiplatform PowerShell remoting.</span></span>

<span data-ttu-id="e26da-107">A Rendszerfelügyeleti webszolgáltatások egy robusztus üzemeltetési modellt biztosít a távoli PowerShell-munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="e26da-107">WinRM provides a robust hosting model for PowerShell remote sessions.</span></span> <span data-ttu-id="e26da-108">amely a megvalósítás SSH-alapú távoli eljáráshívás jelenleg nem támogatja a távoli végpont-konfiguráció és a JEA (Just Enough Administration).</span><span class="sxs-lookup"><span data-stu-id="e26da-108">which this implementation SSH-based remoting doesn't currently support remote endpoint configuration and JEA (Just Enough Administration).</span></span>

<span data-ttu-id="e26da-109">Az SSH a távelérés lehetővé teszi egyszerű PowerShell-munkamenet távelérés Windows és Linux gép között.</span><span class="sxs-lookup"><span data-stu-id="e26da-109">SSH remoting lets you do basic PowerShell session remoting between Windows and Linux machines.</span></span> <span data-ttu-id="e26da-110">SSH távoli eljáráshívás hoz létre, mint egy SSH-alrendszer egy PowerShell gazdafolyamat a célgépen.</span><span class="sxs-lookup"><span data-stu-id="e26da-110">SSH Remoting creates a PowerShell host process on the target machine as an SSH subsystem.</span></span>
<span data-ttu-id="e26da-111">Végül hoznunk egy általános üzemeltetési modell, a Rendszerfelügyeleti webszolgáltatások, a végpont-konfiguráció és a JEA hasonló lesz.</span><span class="sxs-lookup"><span data-stu-id="e26da-111">Eventually we'll implement a general hosting model, similar to WinRM, to support endpoint configuration and JEA.</span></span>

<span data-ttu-id="e26da-112">A `New-PSSession`, `Enter-PSSession`, és `Invoke-Command` parancsmagok most már támogatja az új távelérési kapcsolat új paramétert.</span><span class="sxs-lookup"><span data-stu-id="e26da-112">The `New-PSSession`, `Enter-PSSession`, and `Invoke-Command` cmdlets now have a new parameter set to support this new remoting connection.</span></span>

```
[-HostName <string>]  [-UserName <string>]  [-KeyFilePath <string>]
```

<span data-ttu-id="e26da-113">Hozzon létre egy távoli munkamenetet, adja meg a célszámítógépen a `HostName` paramétert, és adja meg a felhasználónevet, `UserName`.</span><span class="sxs-lookup"><span data-stu-id="e26da-113">To create a remote session, you specify the target machine with the `HostName` parameter and provide the user name with `UserName`.</span></span> <span data-ttu-id="e26da-114">Amikor interaktívan futtatja a parancsmagok, kéri a jelszót.</span><span class="sxs-lookup"><span data-stu-id="e26da-114">When running the cmdlets interactively, you're prompted for a password.</span></span> <span data-ttu-id="e26da-115">Emellett, a titkos kulcsfájl használata SSH kulcsos hitelesítést a `KeyFilePath` paraméter.</span><span class="sxs-lookup"><span data-stu-id="e26da-115">You can also, use SSH key authentication using a private key file with the `KeyFilePath` parameter.</span></span>

## <a name="general-setup-information"></a><span data-ttu-id="e26da-116">Általános beállítási adatok</span><span class="sxs-lookup"><span data-stu-id="e26da-116">General setup information</span></span>

<span data-ttu-id="e26da-117">SSH minden gépen telepítve kell lennie.</span><span class="sxs-lookup"><span data-stu-id="e26da-117">SSH must be installed on all machines.</span></span> <span data-ttu-id="e26da-118">Mindkét az SSH-ügyfél telepítése (`ssh.exe`) és a kiszolgáló (`sshd.exe`) segítségével távoli, és onnan a gépek.</span><span class="sxs-lookup"><span data-stu-id="e26da-118">Install both the SSH client (`ssh.exe`) and server (`sshd.exe`) so that you can remote to and from the machines.</span></span> <span data-ttu-id="e26da-119">Telepítse a Windows, [a Githubról történő Win32-OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/releases).</span><span class="sxs-lookup"><span data-stu-id="e26da-119">For Windows, install [Win32 OpenSSH from GitHub](https://github.com/PowerShell/Win32-OpenSSH/releases).</span></span>
<span data-ttu-id="e26da-120">A Linux telepítse az SSH (beleértve sshd-kiszolgálót) a platformjának megfelelő.</span><span class="sxs-lookup"><span data-stu-id="e26da-120">For Linux, install SSH (including sshd server) appropriate to your platform.</span></span> <span data-ttu-id="e26da-121">Emellett telepítenie kell a PowerShell Core a Githubról, a távoli eljáráshívás SSH szolgáltatás beolvasása.</span><span class="sxs-lookup"><span data-stu-id="e26da-121">You also need to install PowerShell Core from GitHub to get the SSH remoting feature.</span></span> <span data-ttu-id="e26da-122">Az SSH-kiszolgálót úgy kell konfigurálni, egy SSH-alrendszer üzemeltetéséhez a távoli gépen egy PowerShell-folyamat létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="e26da-122">The SSH server must be configured to create an SSH subsystem to host a PowerShell process on the remote machine.</span></span> <span data-ttu-id="e26da-123">Emellett konfigurálnia kell jelszó engedélyezése vagy kulcs alapú hitelesítés.</span><span class="sxs-lookup"><span data-stu-id="e26da-123">You also must configure enable password or key-based authentication.</span></span>

## <a name="set-up-on-windows-machine"></a><span data-ttu-id="e26da-124">Windows-gépen beállítása</span><span class="sxs-lookup"><span data-stu-id="e26da-124">Set up on Windows Machine</span></span>

1. <span data-ttu-id="e26da-125">Telepítse a legújabb verzióját, [a Windows PowerShell Core]</span><span class="sxs-lookup"><span data-stu-id="e26da-125">Install the latest version of [PowerShell Core for Windows]</span></span>

   - <span data-ttu-id="e26da-126">Is megadhatja, hogy a távoli eljáráshívás SSH-támogatás, ha megnézzük a paraméterkészletek számára `New-PSSession`</span><span class="sxs-lookup"><span data-stu-id="e26da-126">You can tell if it has the SSH remoting support by looking at the parameter sets for `New-PSSession`</span></span>

   ```powershell
   Get-Command New-PSSession -syntax
   ```

   ```output
   New-PSSession [-HostName] <string[]> [-Name <string[]>] [-UserName <string>] [-KeyFilePath <string>] [-SSHTransport] [<CommonParameters>]
   ```

2. <span data-ttu-id="e26da-127">A legújabb [Win32 OpenSSH] build telepítése [telepítés] utasításai a githubról</span><span class="sxs-lookup"><span data-stu-id="e26da-127">Install the latest [Win32 OpenSSH] build from GitHub using the [installation] instructions</span></span>
3. <span data-ttu-id="e26da-128">A helyen, amelyre telepítve van a Win32-OpenSSH sshd_config fájlban szerkesztése</span><span class="sxs-lookup"><span data-stu-id="e26da-128">Edit the sshd_config file at the location where you installed Win32 OpenSSH</span></span>

   - <span data-ttu-id="e26da-129">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="e26da-129">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

     ```
     Subsystem    powershell c:/program files/powershell/6.0.4/pwsh.exe -sshs -NoLogo -NoProfile
     ```

     > [!NOTE]
     > <span data-ttu-id="e26da-130">Az OpenSSH a Windows, amely megakadályozza, hogy a tárolóhelyek alrendszer végrehajtható elérési utak használata programhiba van.</span><span class="sxs-lookup"><span data-stu-id="e26da-130">There is a bug in OpenSSH for Windows that prevents spaces from working in subsystem executable paths.</span></span> <span data-ttu-id="e26da-131">További információkért lásd: [a GitHub-problémát](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span><span class="sxs-lookup"><span data-stu-id="e26da-131">For more information, see [this GitHub issue](https://github.com/PowerShell/Win32-OpenSSH/issues/784).</span></span>

     <span data-ttu-id="e26da-132">Az egyik megoldás, a Powershell telepítési könyvtárát, amely nem rendelkezik a tárolóhelyek szimbolikus létrehozásához:</span><span class="sxs-lookup"><span data-stu-id="e26da-132">One solution is to create a symlink to the Powershell installation directory that doesn't have spaces:</span></span>

     ```powershell
     mklink /D c:\pwsh "C:\Program Files\PowerShell\6.0.4"
     ```

     <span data-ttu-id="e26da-133">és a alrendszer írja be:</span><span class="sxs-lookup"><span data-stu-id="e26da-133">and then enter it in the subsystem:</span></span>

     ```
     Subsystem    powershell c:\pwsh\pwsh.exe -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="e26da-134">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="e26da-134">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

4. <span data-ttu-id="e26da-135">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="e26da-135">Restart the sshd service</span></span>

   ```powershell
   Restart-Service sshd
   ```

5. <span data-ttu-id="e26da-136">Adja hozzá az elérési útját a Path környezeti változóba OpenSSH helyéül.</span><span class="sxs-lookup"><span data-stu-id="e26da-136">Add the path where OpenSSH is installed to your Path environment variable.</span></span> <span data-ttu-id="e26da-137">Például: `C:\Program Files\OpenSSH\`.</span><span class="sxs-lookup"><span data-stu-id="e26da-137">For example, `C:\Program Files\OpenSSH\`.</span></span> <span data-ttu-id="e26da-138">Ez a bejegyzés lehetővé teszi a ssh.exe is meg lehet találni.</span><span class="sxs-lookup"><span data-stu-id="e26da-138">This entry allows for the ssh.exe to be found.</span></span>

## <a name="set-up-on-linux-ubuntu-1404-machine"></a><span data-ttu-id="e26da-139">Állítsa be a Linux (Ubuntu 14.04) gépen</span><span class="sxs-lookup"><span data-stu-id="e26da-139">Set up on Linux (Ubuntu 14.04) Machine</span></span>

1. <span data-ttu-id="e26da-140">Telepítse a legújabb [a PowerShell Core for Linux] build a Githubról</span><span class="sxs-lookup"><span data-stu-id="e26da-140">Install the latest [PowerShell Core for Linux] build from GitHub</span></span>
2. <span data-ttu-id="e26da-141">Telepítése [Ubuntu SSH] igény szerint</span><span class="sxs-lookup"><span data-stu-id="e26da-141">Install [Ubuntu SSH] as needed</span></span>

   ```bash
   sudo apt install openssh-client
   sudo apt install openssh-server
   ```

3. <span data-ttu-id="e26da-142">Az sshd_config fájlban a következő helyen /etc/ssh szerkesztése</span><span class="sxs-lookup"><span data-stu-id="e26da-142">Edit the sshd_config file at location /etc/ssh</span></span>

   - <span data-ttu-id="e26da-143">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="e26da-143">Make sure password authentication is enabled</span></span>

   ```
   PasswordAuthentication yes
   ```

   - <span data-ttu-id="e26da-144">PowerShell alrendszer bejegyzés hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e26da-144">Add a PowerShell subsystem entry</span></span>

   ```
   Subsystem powershell /usr/bin/pwsh -sshs -NoLogo -NoProfile
   ```

   - <span data-ttu-id="e26da-145">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="e26da-145">Optionally enable key authentication</span></span>

   ```
   PubkeyAuthentication yes
   ```

4. <span data-ttu-id="e26da-146">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="e26da-146">Restart the sshd service</span></span>

   ```bash
   sudo service sshd restart
   ```

## <a name="set-up-on-macos-machine"></a><span data-ttu-id="e26da-147">Állítsa be a MacOS rendszerű gépén</span><span class="sxs-lookup"><span data-stu-id="e26da-147">Set up on MacOS Machine</span></span>

1. <span data-ttu-id="e26da-148">Telepítse a legújabb [PowerShell Core for MacOS keretrendszert]-build</span><span class="sxs-lookup"><span data-stu-id="e26da-148">Install the latest [PowerShell Core for MacOS] build</span></span>

   - <span data-ttu-id="e26da-149">Győződjön meg arról, hogy SSH-távelérés engedélyezve van az alábbi lépéseket:</span><span class="sxs-lookup"><span data-stu-id="e26da-149">Make sure SSH Remoting is enabled by following these steps:</span></span>
     - <span data-ttu-id="e26da-150">Nyissa meg `System Preferences`</span><span class="sxs-lookup"><span data-stu-id="e26da-150">Open `System Preferences`</span></span>
     - <span data-ttu-id="e26da-151">Kattintson a `Sharing`</span><span class="sxs-lookup"><span data-stu-id="e26da-151">Click on `Sharing`</span></span>
     - <span data-ttu-id="e26da-152">Ellenőrizze `Remote Login` – a következő: `Remote Login: On`</span><span class="sxs-lookup"><span data-stu-id="e26da-152">Check `Remote Login` - Should say `Remote Login: On`</span></span>
     - <span data-ttu-id="e26da-153">Megfelelő felhasználók férhessenek hozzá</span><span class="sxs-lookup"><span data-stu-id="e26da-153">Allow access to appropriate users</span></span>

2. <span data-ttu-id="e26da-154">Szerkessze a `sshd_config` helyen található fájl `/private/etc/ssh/sshd_config`</span><span class="sxs-lookup"><span data-stu-id="e26da-154">Edit the `sshd_config` file at location `/private/etc/ssh/sshd_config`</span></span>

   - <span data-ttu-id="e26da-155">Használja kedvenc szerkesztőjében, vagy</span><span class="sxs-lookup"><span data-stu-id="e26da-155">Use your favorite editor or</span></span>

     ```bash
     sudo nano /private/etc/ssh/sshd_config
     ```

   - <span data-ttu-id="e26da-156">Győződjön meg arról, hogy engedélyezve van a jelszó-hitelesítés</span><span class="sxs-lookup"><span data-stu-id="e26da-156">Make sure password authentication is enabled</span></span>

     ```
     PasswordAuthentication yes
     ```

   - <span data-ttu-id="e26da-157">PowerShell alrendszer bejegyzés hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e26da-157">Add a PowerShell subsystem entry</span></span>

     ```
     Subsystem powershell /usr/local/bin/pwsh -sshs -NoLogo -NoProfile
     ```

   - <span data-ttu-id="e26da-158">Igény szerint a kulcs alapú hitelesítés engedélyezése</span><span class="sxs-lookup"><span data-stu-id="e26da-158">Optionally enable key authentication</span></span>

     ```
     PubkeyAuthentication yes
     ```

3. <span data-ttu-id="e26da-159">Indítsa újra az sshd szolgáltatást</span><span class="sxs-lookup"><span data-stu-id="e26da-159">Restart the sshd service</span></span>

   ```bash
   sudo launchctl stop com.openssh.sshd
   sudo launchctl start com.openssh.sshd
   ```

## <a name="authentication"></a><span data-ttu-id="e26da-160">Hitelesítés</span><span class="sxs-lookup"><span data-stu-id="e26da-160">Authentication</span></span>

<span data-ttu-id="e26da-161">PowerShell távoli eljáráshívás ssh-n keresztül az SSH-ügyfél és az SSH-szolgáltatást között a hitelesítési csere támaszkodik, és nem valósítja meg a hitelesítési sémát magát.</span><span class="sxs-lookup"><span data-stu-id="e26da-161">PowerShell remoting over SSH relies on the authentication exchange between the SSH client and SSH service and does not implement any authentication schemes itself.</span></span>
<span data-ttu-id="e26da-162">Ez azt jelenti, hogy többek között a multi-factor authentication szolgáltatáshoz beállított hitelesítési sémát az SSH és PowerShell függetlenül történik.</span><span class="sxs-lookup"><span data-stu-id="e26da-162">This means that any configured authentication schemes including multi-factor authentication is handled by SSH and independent of PowerShell.</span></span>
<span data-ttu-id="e26da-163">Például konfigurálhatja a nyilvános kulcsos hitelesítés, valamint az egyszeri jelszó megkövetelése a fokozott biztonság az SSH-szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="e26da-163">For example, you can configure the SSH service to require public key authentication as well as a one-time password for added security.</span></span>
<span data-ttu-id="e26da-164">A multi-factor authentication konfigurálása az ebben a dokumentációban hatókörén kívül számára.</span><span class="sxs-lookup"><span data-stu-id="e26da-164">Configuration of multi-factor authentication is outside the scope of this documentation.</span></span>
<span data-ttu-id="e26da-165">Hogyan kell megfelelően multi-factor authentication konfigurálásához, és a PowerShell-en kívül működik, a PowerShell-táveléréssel használata előtt az SSH számára dokumentációban tájékozódhat.</span><span class="sxs-lookup"><span data-stu-id="e26da-165">Refer to documentation for SSH on how to correctly configure multi-factor authentication and validate it works outside of PowerShell before attempting to use it with PowerShell remoting.</span></span>

## <a name="powershell-remoting-example"></a><span data-ttu-id="e26da-166">Távoli eljáráshívás a PowerShell-példa</span><span class="sxs-lookup"><span data-stu-id="e26da-166">PowerShell Remoting Example</span></span>

<span data-ttu-id="e26da-167">A legegyszerűbb módon távelérésének lehetővé tétele, hogy egyetlen gépen kipróbálására.</span><span class="sxs-lookup"><span data-stu-id="e26da-167">The easiest way to test remoting is to try it on a single machine.</span></span> <span data-ttu-id="e26da-168">Ebben a példában létrehozunk egy távoli munkamenetet vissza ugyanaz a Linux rendszerű gép.</span><span class="sxs-lookup"><span data-stu-id="e26da-168">In this example, we create a remote session back to the same Linux machine.</span></span> <span data-ttu-id="e26da-169">PowerShell-parancsmagok interaktív módon, így láthatjuk, kérni fogja az SSH kéri ellenőrzése a gazdaszámítógépen, és a jelszót kérő üzenet használjuk.</span><span class="sxs-lookup"><span data-stu-id="e26da-169">We are using PowerShell cmdlets interactively so we see prompts from SSH asking to verify the host computer and prompting for a password.</span></span> <span data-ttu-id="e26da-170">Megteheti ugyanezt egy Windows-gépen annak érdekében, hogy működik a távoli eljáráshívás.</span><span class="sxs-lookup"><span data-stu-id="e26da-170">You can do the same thing on a Windows machine to ensure remoting is working.</span></span> <span data-ttu-id="e26da-171">Aztán távoli állomásnév módosításával gépek között.</span><span class="sxs-lookup"><span data-stu-id="e26da-171">Then remote between machines by changing the host name.</span></span>

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

### <a name="known-issues"></a><span data-ttu-id="e26da-172">Ismert problémák</span><span class="sxs-lookup"><span data-stu-id="e26da-172">Known Issues</span></span>

<span data-ttu-id="e26da-173">A sudo parancs nem működik a távoli munkamenet Linux rendszerű gépen.</span><span class="sxs-lookup"><span data-stu-id="e26da-173">The sudo command doesn't work in remote session to Linux machine.</span></span>

## <a name="see-also"></a><span data-ttu-id="e26da-174">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e26da-174">See Also</span></span>

[<span data-ttu-id="e26da-175">A Windows PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="e26da-175">PowerShell Core for Windows</span></span>](../setup/installing-powershell-core-on-windows.md#msi)

[<span data-ttu-id="e26da-176">A PowerShell Core linuxhoz</span><span class="sxs-lookup"><span data-stu-id="e26da-176">PowerShell Core for Linux</span></span>](../setup/installing-powershell-core-on-linux.md#ubuntu-1404)

[<span data-ttu-id="e26da-177">MacOS-hez a PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="e26da-177">PowerShell Core for MacOS</span></span>](../setup/installing-powershell-core-on-macos.md)

[<span data-ttu-id="e26da-178">A Win32-OpenSSH</span><span class="sxs-lookup"><span data-stu-id="e26da-178">Win32 OpenSSH</span></span>](https://github.com/PowerShell/Win32-OpenSSH/releases)

[<span data-ttu-id="e26da-179">telepítés</span><span class="sxs-lookup"><span data-stu-id="e26da-179">installation</span></span>](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

[<span data-ttu-id="e26da-180">Ubuntu SSH</span><span class="sxs-lookup"><span data-stu-id="e26da-180">Ubuntu SSH</span></span>](https://help.ubuntu.com/lts/serverguide/openssh-server.html)
