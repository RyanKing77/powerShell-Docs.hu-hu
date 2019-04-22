---
title: A PowerShell Core telepítése Windows rendszerre
description: Információ a Windows PowerShell Core telepítése
ms.date: 08/06/2018
ms.openlocfilehash: 910ee5a653fc1703bfddaf6367225f3b654d600f
ms.sourcegitcommit: 17ce42f97e13e8b3286779dc3f583474b0357023
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59293010"
---
# <a name="installing-powershell-core-on-windows"></a><span data-ttu-id="1714a-103">A PowerShell Core telepítése Windows rendszerre</span><span class="sxs-lookup"><span data-stu-id="1714a-103">Installing PowerShell Core on Windows</span></span>

<span data-ttu-id="1714a-104">A Windows PowerShell Core telepítése többféle módon lehet.</span><span class="sxs-lookup"><span data-stu-id="1714a-104">There are multiple ways to install PowerShell Core in Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1714a-105">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="1714a-105">Prerequisites</span></span>

<span data-ttu-id="1714a-106">PowerShell-távelérés engedélyezése a WSMan felett, a következő előfeltételeknek kell teljesülniük:</span><span class="sxs-lookup"><span data-stu-id="1714a-106">To enable PowerShell remoting over WSMan, the following prerequisites need to be met:</span></span>

- <span data-ttu-id="1714a-107">Telepítse a [Universal C futásidejű](https://www.microsoft.com/download/details.aspx?id=50410) előtt a Windows 10-es Windows-verzión.</span><span class="sxs-lookup"><span data-stu-id="1714a-107">Install the [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) on Windows versions prior to Windows 10.</span></span> <span data-ttu-id="1714a-108">Közvetlen letöltésére vagy a Windows Update-n keresztül érhető el.</span><span class="sxs-lookup"><span data-stu-id="1714a-108">It is available via direct download or Windows Update.</span></span> <span data-ttu-id="1714a-109">Teljes mértékben javítva (választható csomagot is beleértve), a támogatott rendszerek már rendelkezik a telepített.</span><span class="sxs-lookup"><span data-stu-id="1714a-109">Fully patched (including optional packages), supported systems will already have this installed.</span></span>
- <span data-ttu-id="1714a-110">Telepítse a Windows Management Framework (WMF) 4.0-s vagy újabb Windows 7 és Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="1714a-110">Install the Windows Management Framework (WMF) 4.0 or newer on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="a-idmsi-installing-the-msi-package"></a><span data-ttu-id="1714a-111"><a id="msi" />Az MSI-csomag telepítése</span><span class="sxs-lookup"><span data-stu-id="1714a-111"><a id="msi" />Installing the MSI package</span></span>

<span data-ttu-id="1714a-112">PowerShell telepíthető a Windows ügyfél vagy a Windows Server (működik a Windows 7 SP1, Server 2008 R2 és újabb verziók), az MSI-csomag letöltése a Githubról [kiadások] [] oldalát.</span><span class="sxs-lookup"><span data-stu-id="1714a-112">To install PowerShell on a Windows client or Windows Server (works on Windows 7 SP1, Server 2008 R2, and later), download the MSI package from our GitHub [releases][] page.</span></span> <span data-ttu-id="1714a-113">Görgessen le a **eszközök** telepíteni szeretné a kiadás szakaszában.</span><span class="sxs-lookup"><span data-stu-id="1714a-113">Scroll down to the **Assets** section of the Release you want to install.</span></span> <span data-ttu-id="1714a-114">Az eszközök szakaszban össze lehet csukni, ezért szükség lehet annak kibontásához kattintson.</span><span class="sxs-lookup"><span data-stu-id="1714a-114">The Assets section may be collapsed, so you may need to click to expand it.</span></span>

<span data-ttu-id="1714a-115">Az MSI-fájlt a következőhöz hasonló- `PowerShell-<version>-win-<os-arch>.msi`</span><span class="sxs-lookup"><span data-stu-id="1714a-115">The MSI file looks like this - `PowerShell-<version>-win-<os-arch>.msi`</span></span>
<!-- TODO: should be updated to point to the Download Center as well -->

<span data-ttu-id="1714a-116">A letöltést követően kattintson duplán a, és kövesse az utasításokat.</span><span class="sxs-lookup"><span data-stu-id="1714a-116">Once downloaded, double-click the installer and follow the prompts.</span></span>

<span data-ttu-id="1714a-117">A telepítő létrehoz egy parancsikont a Windows Start menü.</span><span class="sxs-lookup"><span data-stu-id="1714a-117">The installer creates a shortcut in the Windows Start Menu.</span></span>

- <span data-ttu-id="1714a-118">Alapértelmezés szerint a csomag telepítése `$env:ProgramFiles\PowerShell\<version>`</span><span class="sxs-lookup"><span data-stu-id="1714a-118">By default the package is installed to `$env:ProgramFiles\PowerShell\<version>`</span></span>
- <span data-ttu-id="1714a-119">PowerShell a Start menü használatával indíthatja el vagy `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span><span class="sxs-lookup"><span data-stu-id="1714a-119">You can launch PowerShell via the Start Menu or `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span></span>

### <a name="administrative-install-from-the-command-line"></a><span data-ttu-id="1714a-120">Felügyeleti telepítése a parancssorból</span><span class="sxs-lookup"><span data-stu-id="1714a-120">Administrative install from the command line</span></span>

<span data-ttu-id="1714a-121">MSI-csomagok a parancssorból is telepíthető.</span><span class="sxs-lookup"><span data-stu-id="1714a-121">MSI packages can be installed from the command line.</span></span> <span data-ttu-id="1714a-122">Ez lehetővé teszi a rendszergazdák felhasználói beavatkozás nélkül-csomagok üzembe helyezése.</span><span class="sxs-lookup"><span data-stu-id="1714a-122">This allows administrators to deploy packages without user interaction.</span></span> <span data-ttu-id="1714a-123">PowerShell az MSI-csomag tartalmazza a következő tulajdonságokat a telepítési beállítások:</span><span class="sxs-lookup"><span data-stu-id="1714a-123">The MSI package for PowerShell includes the following properties to control the installation options:</span></span>

- <span data-ttu-id="1714a-124">**ADD_EXPLORER_CONTEXT_MENU_OPENPOWERSHELL** – Ez a tulajdonság azt szabályozza, a beállítás hozzáadásához a **megnyitott PowerShell** elemet a helyi menüben, a Windows Intézőben.</span><span class="sxs-lookup"><span data-stu-id="1714a-124">**ADD_EXPLORER_CONTEXT_MENU_OPENPOWERSHELL** - This property controls the option for adding the **Open PowerShell** item to the context menu in Windows Explorer.</span></span>
- <span data-ttu-id="1714a-125">**ENABLE_PSREMOTING** – Ez a tulajdonság azt szabályozza, a beállítást, a PowerShell-távelérés engedélyezése a telepítés során.</span><span class="sxs-lookup"><span data-stu-id="1714a-125">**ENABLE_PSREMOTING** - This property controls the option for enabling PowerShell remoting during installation.</span></span>
- <span data-ttu-id="1714a-126">**REGISTER_MANIFEST** – Ez a tulajdonság azt szabályozza, a Windows Eseménynapló jegyzékfájl regisztrálása a kívánt beállítást.</span><span class="sxs-lookup"><span data-stu-id="1714a-126">**REGISTER_MANIFEST** - This property controls the option for registering the Windows Event Logging manifest.</span></span>

<span data-ttu-id="1714a-127">A következő példa bemutatja, hogyan csendes telepítésére a PowerShell Core engedélyezve van az összes telepítési lehetőségekkel.</span><span class="sxs-lookup"><span data-stu-id="1714a-127">The following examples shows how to silently install PowerShell Core with all the install options enabled.</span></span>

```powershell
msiexec.exe /package PowerShell-<version>-win-<os-arch>.msi /quiet ADD_EXPLORER_CONTEXT_MENU_OPENPOWERSHELL=1 ENABLE_PSREMOTING=1 REGISTER_MANIFEST=1
```

<span data-ttu-id="1714a-128">Msiexec.exe parancssori kapcsolók teljes listáját lásd: [parancssori kapcsolók](/windows/desktop/Msi/command-line-options).</span><span class="sxs-lookup"><span data-stu-id="1714a-128">For a full list of command line options for Msiexec.exe, see [Command line options](/windows/desktop/Msi/command-line-options).</span></span>

## <a name="a-idzip-installing-the-zip-package"></a><span data-ttu-id="1714a-129"><a id="zip" />A ZIP-csomag telepítése</span><span class="sxs-lookup"><span data-stu-id="1714a-129"><a id="zip" />Installing the ZIP package</span></span>

<span data-ttu-id="1714a-130">PowerShell-bináris ZIP-archívumok állnak rendelkezésre a speciális telepítési forgatókönyvek megvalósítását teszik lehetővé.</span><span class="sxs-lookup"><span data-stu-id="1714a-130">PowerShell binary ZIP archives are provided to enable advanced deployment scenarios.</span></span> <span data-ttu-id="1714a-131">Fontos megjegyezni, hogy a ZIP-archívumot használata esetén nem jelenik meg az Előfeltételek ellenőrzése, mint az MSI-csomag.</span><span class="sxs-lookup"><span data-stu-id="1714a-131">Be noted that when using the ZIP archive, you won't get the prerequisites check as in the MSI package.</span></span> <span data-ttu-id="1714a-132">A távoli eljáráshívás keresztül WSMan megfelelően működjön, győződjön meg arról, hogy teljesül-e a [Előfeltételek](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="1714a-132">For remoting over WSMan to work properly,, ensure that you have met the [prerequisites](#prerequisites).</span></span>

## <a name="deploying-on-windows-iot"></a><span data-ttu-id="1714a-133">A Windows IoT üzembe helyezése</span><span class="sxs-lookup"><span data-stu-id="1714a-133">Deploying on Windows IoT</span></span>

<span data-ttu-id="1714a-134">A Windows PowerShell-lel történő üzembe helyezése a PowerShell Core 6-os használjuk, amely már van Windows IoT.</span><span class="sxs-lookup"><span data-stu-id="1714a-134">Windows IoT already comes with Windows PowerShell which we will use to deploy PowerShell Core 6.</span></span>

1. <span data-ttu-id="1714a-135">Hozzon létre `PSSession` a céleszköz</span><span class="sxs-lookup"><span data-stu-id="1714a-135">Create `PSSession` to target device</span></span>

   ```powershell
   $s = New-PSSession -ComputerName <deviceIp> -Credential Administrator
   ```

2. <span data-ttu-id="1714a-136">Másolja a ZIP-csomagját az eszközön</span><span class="sxs-lookup"><span data-stu-id="1714a-136">Copy the ZIP package to the device</span></span>

   ```powershell
   # change the destination to however you had partitioned it with sufficient
   # space for the zip and the unzipped contents
   # the path should be local to the device
   Copy-Item .\PowerShell-<version>-win-<os-arch>.zip -Destination u:\users\administrator\Downloads -ToSession $s
   ```

3. <span data-ttu-id="1714a-137">Az eszköz csatlakozik, és bontsa ki az archívum</span><span class="sxs-lookup"><span data-stu-id="1714a-137">Connect to the device and expand the archive</span></span>

   ```powershell
   Enter-PSSession $s
   Set-Location u:\users\administrator\downloads
   Expand-Archive .\PowerShell-<version>-win-<os-arch>.zip
   ```

4. <span data-ttu-id="1714a-138">A telepítő távoli eljáráshívás a PowerShell Core 6-os</span><span class="sxs-lookup"><span data-stu-id="1714a-138">Setup remoting to PowerShell Core 6</span></span>

   ```powershell
   Set-Location .\PowerShell-<version>-win-<os-arch>
   # Be sure to use the -PowerShellHome parameter otherwise it'll try to create a new
   # endpoint with Windows PowerShell 5.1
   .\Install-PowerShellRemoting.ps1 -PowerShellHome .
   # You'll get an error message and will be disconnected from the device because it has to restart WinRM
   ```

5. <span data-ttu-id="1714a-139">Csatlakozhat a PowerShell Core 6-os végpont az eszközön</span><span class="sxs-lookup"><span data-stu-id="1714a-139">Connect to PowerShell Core 6 endpoint on device</span></span>

   ```powershell
   # Be sure to use the -Configuration parameter.  If you omit it, you will connect to Windows PowerShell 5.1
   Enter-PSSession -ComputerName <deviceIp> -Credential Administrator -Configuration powershell.<version>
   ```

## <a name="deploying-on-nano-server"></a><span data-ttu-id="1714a-140">A Nano Server üzembe helyezése</span><span class="sxs-lookup"><span data-stu-id="1714a-140">Deploying on Nano Server</span></span>

<span data-ttu-id="1714a-141">Ezek az utasítások feltételezik, hogy egy PowerShell-verzió már fut a Nano Server-rendszerképet és, hogy a létrehozott által a [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).</span><span class="sxs-lookup"><span data-stu-id="1714a-141">These instructions assume that a version of PowerShell is already running on the Nano Server image and that it has been generated by the [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).</span></span>
<span data-ttu-id="1714a-142">A nano Server egy "távfelügyelt" operációs rendszer.</span><span class="sxs-lookup"><span data-stu-id="1714a-142">Nano Server is a "headless" OS.</span></span> <span data-ttu-id="1714a-143">Az alapvető bináris fájlokat telepítheti két különböző módszer használatával.</span><span class="sxs-lookup"><span data-stu-id="1714a-143">Core binaries can be deploy using two different methods.</span></span>

1. <span data-ttu-id="1714a-144">Offline – a Nano Server virtuális merevlemez csatlakoztatása, és csomagolja ki a zip-fájlt a kiválasztott helyen belül a csatlakoztatott lemezkép tartalmát.</span><span class="sxs-lookup"><span data-stu-id="1714a-144">Offline - Mount the Nano Server VHD and unzip the contents of the zip file to your chosen location within the mounted image.</span></span>
2. <span data-ttu-id="1714a-145">Online – a zip-fájl átvitel egy PowerShell-munkamenetet, és bontsa ki azt a kiválasztott helyen.</span><span class="sxs-lookup"><span data-stu-id="1714a-145">Online - Transfer the zip file over a PowerShell Session and unzip it in your chosen location.</span></span>

<span data-ttu-id="1714a-146">Mindkét esetben szüksége lesz a Windows 10-es x64 ZIP kiadási csomag és a egy "Rendszergazda" PowerShell-példány belül lévő parancsok futtatásával.</span><span class="sxs-lookup"><span data-stu-id="1714a-146">In both cases, you will need the Windows 10 x64 ZIP release package and will need to run the commands within an "Administrator" PowerShell instance.</span></span>

### <a name="offline-deployment-of-powershell-core"></a><span data-ttu-id="1714a-147">Offline állapotban van a PowerShell Core telepítése</span><span class="sxs-lookup"><span data-stu-id="1714a-147">Offline Deployment of PowerShell Core</span></span>

1. <span data-ttu-id="1714a-148">A kedvenc zip segédprogrammal tömörítse ki a csomagot egy könyvtárba, a csatlakoztatott Nano Server-rendszerképben.</span><span class="sxs-lookup"><span data-stu-id="1714a-148">Use your favorite zip utility to unzip the package to a directory within the mounted Nano Server image.</span></span>
2. <span data-ttu-id="1714a-149">Válassza le a lemezképet, és indítsa el azt.</span><span class="sxs-lookup"><span data-stu-id="1714a-149">Unmount the image and boot it.</span></span>
3. <span data-ttu-id="1714a-150">Csatlakozzon a Windows PowerShell Beérkezett üzenetek példányához.</span><span class="sxs-lookup"><span data-stu-id="1714a-150">Connect to the inbox instance of Windows PowerShell.</span></span>
4. <span data-ttu-id="1714a-151">Kövesse az utasításokat, hozzon létre egy távoli eljáráshívás végpont a ["egy másik példány technikával"](../learn/remoting/wsman-remoting-in-powershell-core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="1714a-151">Follow the instructions to create a remoting endpoint using the ["another instance technique"](../learn/remoting/wsman-remoting-in-powershell-core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

### <a name="online-deployment-of-powershell-core"></a><span data-ttu-id="1714a-152">Online-hoz a PowerShell Core telepítése</span><span class="sxs-lookup"><span data-stu-id="1714a-152">Online Deployment of PowerShell Core</span></span>

<span data-ttu-id="1714a-153">A következő lépések végigvezetik a PowerShell Core telepítése a Nano Server és a távoli végpont konfigurációját egy futó példányával.</span><span class="sxs-lookup"><span data-stu-id="1714a-153">The following steps guide you through the deployment of PowerShell Core to a running instance of Nano Server and the configuration of its remote endpoint.</span></span>

- <span data-ttu-id="1714a-154">Csatlakozzon a Windows PowerShell Beérkezett üzenetek példányához</span><span class="sxs-lookup"><span data-stu-id="1714a-154">Connect to the inbox instance of Windows PowerShell</span></span>

  ```powershell
  $session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
  ```

- <span data-ttu-id="1714a-155">Másolja a fájlt a Nano Server-példány</span><span class="sxs-lookup"><span data-stu-id="1714a-155">Copy the file to the Nano Server instance</span></span>

  ```powershell
  Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
  ```

- <span data-ttu-id="1714a-156">Adja meg a munkamenet</span><span class="sxs-lookup"><span data-stu-id="1714a-156">Enter the session</span></span>

  ```powershell
  Enter-PSSession $session
  ```

- <span data-ttu-id="1714a-157">Bontsa ki a ZIP-fájl</span><span class="sxs-lookup"><span data-stu-id="1714a-157">Extract the ZIP file</span></span>

  ```powershell
  # Insert the appropriate version.
  Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
  ```

- <span data-ttu-id="1714a-158">Ha azt szeretné, hogy a WSMan-alapú távoli eljáráshívás, kövesse az utasításokat hozzon létre egy távoli eljáráshívás végpont a ["egy másik példány technikával"](../learn/remoting/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="1714a-158">If you want WSMan-based remoting, follow the instructions to create a remoting endpoint using the ["another instance technique"](../learn/remoting/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

## <a name="how-to-create-a-remoting-endpoint"></a><span data-ttu-id="1714a-159">A távoli eljáráshívás-végpont létrehozása</span><span class="sxs-lookup"><span data-stu-id="1714a-159">How to create a remoting endpoint</span></span>

<span data-ttu-id="1714a-160">A PowerShell Core a PowerShell távoli eljáráshívás protokoll (PSRP) támogatja a wsman által használt és az SSH keresztül.</span><span class="sxs-lookup"><span data-stu-id="1714a-160">PowerShell Core supports the PowerShell Remoting Protocol (PSRP) over both WSMan and SSH.</span></span> <span data-ttu-id="1714a-161">További információ:</span><span class="sxs-lookup"><span data-stu-id="1714a-161">For more information, see:</span></span>

- <span data-ttu-id="1714a-162">[SSH távoli eljáráshívás a PowerShell Core] [ssh-távoli eljáráshívás]</span><span class="sxs-lookup"><span data-stu-id="1714a-162">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
- <span data-ttu-id="1714a-163">[A PowerShell Core a wsman által használt távoli eljáráshívás] [a wsman-távelérése]</span><span class="sxs-lookup"><span data-stu-id="1714a-163">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

<!-- [download-center]: TODO -->
[kiadások]: https://github.com/PowerShell/PowerShell/releases [ssh-távoli eljáráshívás]:... [a wsman-távelérése] /Core-PowerShell/SSH-Remoting-in-PowerShell-Core.md:... [AppVeyor] /Core-PowerShell/WSMan-Remoting-in-PowerShell-Core.md: https://ci.appveyor.com/project/PowerShell/powershell
[releases]: https://github.com/PowerShell/PowerShell/releases [ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md [wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md [AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell
