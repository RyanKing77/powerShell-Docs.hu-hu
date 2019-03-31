---
title: A PowerShell Core telepítése Windows rendszerre
description: Információ a Windows PowerShell Core telepítése
ms.date: 08/06/2018
ms.openlocfilehash: 450a38a1ef2e2890059094774fcc3f2ad4fcda6e
ms.sourcegitcommit: 8dd4394cf867005a8b9ef0bb74b744c964fbc332
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/30/2019
ms.locfileid: "58748958"
---
# <a name="installing-powershell-core-on-windows"></a><span data-ttu-id="9bb5a-103">A PowerShell Core telepítése Windows rendszerre</span><span class="sxs-lookup"><span data-stu-id="9bb5a-103">Installing PowerShell Core on Windows</span></span>

## <a name="msi"></a><span data-ttu-id="9bb5a-104">MSI</span><span class="sxs-lookup"><span data-stu-id="9bb5a-104">MSI</span></span>

<span data-ttu-id="9bb5a-105">PowerShell telepíthető a Windows ügyfél vagy a Windows Server (a Windows 7 SP1, Server 2008 R2 esetében használható, és újabb verziók), töltse le az MSI-csomag github [kiadások][] lap.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-105">To install PowerShell on a Windows client or Windows Server (works on Windows 7 SP1, Server 2008 R2, and later), download the MSI package from our GitHub [releases][] page.</span></span>  <span data-ttu-id="9bb5a-106">Görgessen le a **eszközök** telepíteni szeretné a kiadás szakaszában.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-106">Scroll down to the **Assets** section of the Release you want to install.</span></span>  <span data-ttu-id="9bb5a-107">Az eszközök szakaszban össze lehet csukni, ezért szükség lehet annak kibontásához kattintson.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-107">The Assets section may be collapsed, so you may need to click to expand it.</span></span>

<span data-ttu-id="9bb5a-108">Az MSI-fájlt a következőhöz hasonló- `PowerShell-<version>-win-<os-arch>.msi`</span><span class="sxs-lookup"><span data-stu-id="9bb5a-108">The MSI file looks like this - `PowerShell-<version>-win-<os-arch>.msi`</span></span>
<!-- TODO: should be updated to point to the Download Center as well -->

<span data-ttu-id="9bb5a-109">A letöltést követően kattintson duplán a, és kövesse az utasításokat.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-109">Once downloaded, double-click the installer and follow the prompts.</span></span>

<span data-ttu-id="9bb5a-110">Nincs egy helyi helyezi el a Start menüben a telepítés után.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-110">There is a shortcut placed in the Start Menu upon installation.</span></span>

- <span data-ttu-id="9bb5a-111">Alapértelmezés szerint a csomag telepítése `$env:ProgramFiles\PowerShell\<version>`</span><span class="sxs-lookup"><span data-stu-id="9bb5a-111">By default the package is installed to `$env:ProgramFiles\PowerShell\<version>`</span></span>
- <span data-ttu-id="9bb5a-112">PowerShell a Start menü használatával indíthatja el vagy `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span><span class="sxs-lookup"><span data-stu-id="9bb5a-112">You can launch PowerShell via the Start Menu or `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9bb5a-113">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="9bb5a-113">Prerequisites</span></span>

<span data-ttu-id="9bb5a-114">PowerShell-távelérés engedélyezése a WSMan felett, a következő előfeltételeknek kell teljesülniük:</span><span class="sxs-lookup"><span data-stu-id="9bb5a-114">To enable PowerShell remoting over WSMan, the following prerequisites need to be met:</span></span>

- <span data-ttu-id="9bb5a-115">Telepítse a [Universal C futásidejű](https://www.microsoft.com/download/details.aspx?id=50410) előtt a Windows 10-es Windows-verzión.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-115">Install the [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) on Windows versions prior to Windows 10.</span></span>
  <span data-ttu-id="9bb5a-116">Közvetlen letöltésére vagy a Windows Update-n keresztül érhető el.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-116">It is available via direct download or Windows Update.</span></span>
  <span data-ttu-id="9bb5a-117">Teljes mértékben javítva (választható csomagot is beleértve), a támogatott rendszerek már rendelkezik a telepített.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-117">Fully patched (including optional packages), supported systems will already have this installed.</span></span>
- <span data-ttu-id="9bb5a-118">Telepítse a Windows Management Framework (WMF) 4.0-s vagy újabb Windows 7 és Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-118">Install the Windows Management Framework (WMF) 4.0 or newer on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="zip"></a><span data-ttu-id="9bb5a-119">ZIP</span><span class="sxs-lookup"><span data-stu-id="9bb5a-119">ZIP</span></span>

<span data-ttu-id="9bb5a-120">PowerShell-bináris ZIP-archívumok állnak rendelkezésre a speciális telepítési forgatókönyvek megvalósítását teszik lehetővé.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-120">PowerShell binary ZIP archives are provided to enable advanced deployment scenarios.</span></span>
<span data-ttu-id="9bb5a-121">Fontos megjegyezni, hogy a ZIP-archívumot használata esetén nem jelenik meg az Előfeltételek ellenőrzése, mint az MSI-csomag.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-121">Be noted that when using the ZIP archive, you won't get the prerequisites check as in the MSI package.</span></span>
<span data-ttu-id="9bb5a-122">Ezért ahhoz a wsman által használt keresztül távelérése megfelelő működéséhez a Windows 10-es előtti Windows-verzión, győződjön meg arról, hogy kell a [Előfeltételek](#prerequisites) teljesülnek-e.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-122">So in order for remoting over WSMan to work properly on Windows versions prior to Windows 10, you need to make sure the [prerequisites](#prerequisites) are met.</span></span>

## <a name="deploying-on-windows-iot"></a><span data-ttu-id="9bb5a-123">A Windows IoT üzembe helyezése</span><span class="sxs-lookup"><span data-stu-id="9bb5a-123">Deploying on Windows IoT</span></span>

<span data-ttu-id="9bb5a-124">A Windows PowerShell-lel történő üzembe helyezése a PowerShell Core 6-os használjuk, amely már van Windows IoT.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-124">Windows IoT already comes with Windows PowerShell which we will use to deploy PowerShell Core 6.</span></span>

1. <span data-ttu-id="9bb5a-125">Hozzon létre `PSSession` a céleszköz</span><span class="sxs-lookup"><span data-stu-id="9bb5a-125">Create `PSSession` to target device</span></span>

   ```powershell
   $s = New-PSSession -ComputerName <deviceIp> -Credential Administrator
   ```

2. <span data-ttu-id="9bb5a-126">Másolja a ZIP-csomagját az eszközön</span><span class="sxs-lookup"><span data-stu-id="9bb5a-126">Copy the ZIP package to the device</span></span>

   ```powershell
   # change the destination to however you had partitioned it with sufficient
   # space for the zip and the unzipped contents
   # the path should be local to the device
   Copy-Item .\PowerShell-<version>-win-<os-arch>.zip -Destination u:\users\administrator\Downloads -ToSession $s
   ```

3. <span data-ttu-id="9bb5a-127">Az eszköz csatlakozik, és bontsa ki az archívum</span><span class="sxs-lookup"><span data-stu-id="9bb5a-127">Connect to the device and expand the archive</span></span>

   ```powershell
   Enter-PSSession $s
   Set-Location u:\users\administrator\downloads
   Expand-Archive .\PowerShell-<version>-win-<os-arch>.zip
   ```

4. <span data-ttu-id="9bb5a-128">A telepítő távoli eljáráshívás a PowerShell Core 6-os</span><span class="sxs-lookup"><span data-stu-id="9bb5a-128">Setup remoting to PowerShell Core 6</span></span>

   ```powershell
   Set-Location .\PowerShell-<version>-win-<os-arch>
   # Be sure to use the -PowerShellHome parameter otherwise it'll try to create a new
   # endpoint with Windows PowerShell 5.1
   .\Install-PowerShellRemoting.ps1 -PowerShellHome .
   # You'll get an error message and will be disconnected from the device because it has to restart WinRM
   ```

5. <span data-ttu-id="9bb5a-129">Csatlakozhat a PowerShell Core 6-os végpont az eszközön</span><span class="sxs-lookup"><span data-stu-id="9bb5a-129">Connect to PowerShell Core 6 endpoint on device</span></span>

   ```powershell
   # Be sure to use the -Configuration parameter.  If you omit it, you will connect to Windows PowerShell 5.1
   Enter-PSSession -ComputerName <deviceIp> -Credential Administrator -Configuration powershell.<version>
   ```

## <a name="deploying-on-nano-server"></a><span data-ttu-id="9bb5a-130">A Nano Server üzembe helyezése</span><span class="sxs-lookup"><span data-stu-id="9bb5a-130">Deploying on Nano Server</span></span>

<span data-ttu-id="9bb5a-131">Ezek az utasítások feltételezik, hogy egy PowerShell-verzió már fut a Nano Server-rendszerképet és, hogy a létrehozott által a [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).</span><span class="sxs-lookup"><span data-stu-id="9bb5a-131">These instructions assume that a version of PowerShell is already running on the Nano Server image and that it has been generated by the [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).</span></span>
<span data-ttu-id="9bb5a-132">A nano Server egy "távfelügyelt" operációs rendszer.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-132">Nano Server is a "headless" OS.</span></span> <span data-ttu-id="9bb5a-133">Az alapvető bináris fájlokat telepítheti két különböző módszer használatával.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-133">Core binaries can be deploy using two different methods.</span></span>

1. <span data-ttu-id="9bb5a-134">Offline – a Nano Server virtuális merevlemez csatlakoztatása, és csomagolja ki a zip-fájlt a kiválasztott helyen belül a csatlakoztatott lemezkép tartalmát.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-134">Offline - Mount the Nano Server VHD and unzip the contents of the zip file to your chosen location within the mounted image.</span></span>
2. <span data-ttu-id="9bb5a-135">Online – a zip-fájl átvitel egy PowerShell-munkamenetet, és bontsa ki azt a kiválasztott helyen.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-135">Online - Transfer the zip file over a PowerShell Session and unzip it in your chosen location.</span></span>

<span data-ttu-id="9bb5a-136">Mindkét esetben szüksége lesz a Windows 10-es x64 ZIP kiadási csomag és a egy "Rendszergazda" PowerShell-példány belül lévő parancsok futtatásával.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-136">In both cases, you will need the Windows 10 x64 ZIP release package and will need to run the commands within an "Administrator" PowerShell instance.</span></span>

### <a name="offline-deployment-of-powershell-core"></a><span data-ttu-id="9bb5a-137">Offline állapotban van a PowerShell Core telepítése</span><span class="sxs-lookup"><span data-stu-id="9bb5a-137">Offline Deployment of PowerShell Core</span></span>

1. <span data-ttu-id="9bb5a-138">A kedvenc zip segédprogrammal tömörítse ki a csomagot egy könyvtárba, a csatlakoztatott Nano Server-rendszerképben.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-138">Use your favorite zip utility to unzip the package to a directory within the mounted Nano Server image.</span></span>
2. <span data-ttu-id="9bb5a-139">Válassza le a lemezképet, és indítsa el azt.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-139">Unmount the image and boot it.</span></span>
3. <span data-ttu-id="9bb5a-140">Csatlakozzon a Windows PowerShell Beérkezett üzenetek példányához.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-140">Connect to the inbox instance of Windows PowerShell.</span></span>
4. <span data-ttu-id="9bb5a-141">Kövesse az utasításokat, hozzon létre egy távoli eljáráshívás végpont a ["egy másik példány technikával"](../learn/remoting/wsman-remoting-in-powershell-core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="9bb5a-141">Follow the instructions to create a remoting endpoint using the ["another instance technique"](../learn/remoting/wsman-remoting-in-powershell-core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

### <a name="online-deployment-of-powershell-core"></a><span data-ttu-id="9bb5a-142">Online-hoz a PowerShell Core telepítése</span><span class="sxs-lookup"><span data-stu-id="9bb5a-142">Online Deployment of PowerShell Core</span></span>

<span data-ttu-id="9bb5a-143">A következő lépések végigvezetik a PowerShell Core telepítése a Nano Server és a távoli végpont konfigurációját egy futó példányával.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-143">The following steps guide you through the deployment of PowerShell Core to a running instance of Nano Server and the configuration of its remote endpoint.</span></span>

- <span data-ttu-id="9bb5a-144">Csatlakozzon a Windows PowerShell Beérkezett üzenetek példányához</span><span class="sxs-lookup"><span data-stu-id="9bb5a-144">Connect to the inbox instance of Windows PowerShell</span></span>

  ```powershell
  $session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
  ```

- <span data-ttu-id="9bb5a-145">Másolja a fájlt a Nano Server-példány</span><span class="sxs-lookup"><span data-stu-id="9bb5a-145">Copy the file to the Nano Server instance</span></span>

  ```powershell
  Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
  ```

- <span data-ttu-id="9bb5a-146">Adja meg a munkamenet</span><span class="sxs-lookup"><span data-stu-id="9bb5a-146">Enter the session</span></span>

  ```powershell
  Enter-PSSession $session
  ```

- <span data-ttu-id="9bb5a-147">Bontsa ki a ZIP-fájl</span><span class="sxs-lookup"><span data-stu-id="9bb5a-147">Extract the ZIP file</span></span>

  ```powershell
  # Insert the appropriate version.
  Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
  ```

- <span data-ttu-id="9bb5a-148">Ha azt szeretné, hogy a WSMan-alapú távoli eljáráshívás, kövesse az utasításokat hozzon létre egy távoli eljáráshívás végpont a ["egy másik példány technikával"](../learn/remoting/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="9bb5a-148">If you want WSMan-based remoting, follow the instructions to create a remoting endpoint using the ["another instance technique"](../learn/remoting/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="9bb5a-149">A távoli eljáráshívás végpont létrehozására vonatkozó utasításokat</span><span class="sxs-lookup"><span data-stu-id="9bb5a-149">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="9bb5a-150">A PowerShell Core a PowerShell távoli eljáráshívás protokoll (PSRP) támogatja a wsman által használt és az SSH keresztül.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-150">PowerShell Core supports the PowerShell Remoting Protocol (PSRP) over both WSMan and SSH.</span></span>
<span data-ttu-id="9bb5a-151">További információ:</span><span class="sxs-lookup"><span data-stu-id="9bb5a-151">For more information, see:</span></span>

- <span data-ttu-id="9bb5a-152">[SSH távoli eljáráshívás a PowerShell Core][ssh-remoting]</span><span class="sxs-lookup"><span data-stu-id="9bb5a-152">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
- <span data-ttu-id="9bb5a-153">[A PowerShell Core a wsman által használt távoli eljáráshívás][wsman-remoting]</span><span class="sxs-lookup"><span data-stu-id="9bb5a-153">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

## <a name="artifact-installation-instructions"></a><span data-ttu-id="9bb5a-154">Összetevő telepítési utasításokat</span><span class="sxs-lookup"><span data-stu-id="9bb5a-154">Artifact Installation Instructions</span></span>

<span data-ttu-id="9bb5a-155">Coreclr-nek bits minden CI-build-a az archívumot közzétesszük [AppVeyor][].</span><span class="sxs-lookup"><span data-stu-id="9bb5a-155">We publish an archive with CoreCLR bits on every CI build with [AppVeyor][].</span></span>

<span data-ttu-id="9bb5a-156">A PowerShell Core telepítése a coreclr-nek összetevő:</span><span class="sxs-lookup"><span data-stu-id="9bb5a-156">To install PowerShell Core from the CoreCLR Artifact:</span></span>

1. <span data-ttu-id="9bb5a-157">Töltse le a ZIP-csomagját **összetevők** az adott build lapján.</span><span class="sxs-lookup"><span data-stu-id="9bb5a-157">Download ZIP package from **artifacts** tab of the particular build.</span></span>
2. <span data-ttu-id="9bb5a-158">Feloldása ZIP-fájl: kattintson a jobb gombbal a Fájlkezelőben -> Properties -> box -> feloldása a alkalmazni ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="9bb5a-158">Unblock ZIP file: right-click in File Explorer -> Properties -> check 'Unblock' box -> apply</span></span>
3. <span data-ttu-id="9bb5a-159">Bontsa ki a zip-fájlt `bin` könyvtár</span><span class="sxs-lookup"><span data-stu-id="9bb5a-159">Extract zip file to `bin` directory</span></span>
4. `./bin/pwsh.exe`

<!-- [download-center]: TODO -->

[Kiadások]: https://github.com/PowerShell/PowerShell/releases
[releases]: https://github.com/PowerShell/PowerShell/releases
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell
