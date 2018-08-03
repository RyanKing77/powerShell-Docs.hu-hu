# <a name="installing-powershell-core-on-windows"></a><span data-ttu-id="c753b-101">A PowerShell Core telepítése Windows rendszerre</span><span class="sxs-lookup"><span data-stu-id="c753b-101">Installing PowerShell Core on Windows</span></span>

## <a name="msi"></a><span data-ttu-id="c753b-102">MSI</span><span class="sxs-lookup"><span data-stu-id="c753b-102">MSI</span></span>

<span data-ttu-id="c753b-103">PowerShell telepíthető a Windows ügyfél vagy a Windows Server (a Windows 7 SP1, Server 2008 R2 esetében használható, és újabb verziók), töltse le az MSI-csomag github [kiadások][] lap.</span><span class="sxs-lookup"><span data-stu-id="c753b-103">To install PowerShell on a Windows client or Windows Server (works on Windows 7 SP1, Server 2008 R2, and later), download the MSI package from our GitHub [releases][] page.</span></span>

<span data-ttu-id="c753b-104">Az MSI-fájlt a következőhöz hasonló- `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well --></span><span class="sxs-lookup"><span data-stu-id="c753b-104">The MSI file looks like this - `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well --></span></span>

<span data-ttu-id="c753b-105">A letöltést követően kattintson duplán a, és kövesse az utasításokat.</span><span class="sxs-lookup"><span data-stu-id="c753b-105">Once downloaded, double-click the installer and follow the prompts.</span></span>

<span data-ttu-id="c753b-106">Nincs egy helyi helyezi el a Start menüben a telepítés után.</span><span class="sxs-lookup"><span data-stu-id="c753b-106">There is a shortcut placed in the Start Menu upon installation.</span></span>

- <span data-ttu-id="c753b-107">Alapértelmezés szerint a csomag telepítése `$env:ProgramFiles\PowerShell\<version>`</span><span class="sxs-lookup"><span data-stu-id="c753b-107">By default the package is installed to `$env:ProgramFiles\PowerShell\<version>`</span></span>
- <span data-ttu-id="c753b-108">PowerShell a Start menü használatával indíthatja el vagy `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span><span class="sxs-lookup"><span data-stu-id="c753b-108">You can launch PowerShell via the Start Menu or `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c753b-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="c753b-109">Prerequisites</span></span>

<span data-ttu-id="c753b-110">PowerShell-távelérés engedélyezése a WSMan felett, a következő előfeltételeknek kell teljesülniük:</span><span class="sxs-lookup"><span data-stu-id="c753b-110">To enable PowerShell remoting over WSMan, the following prerequisites need to be met:</span></span>

- <span data-ttu-id="c753b-111">Telepítse a [Universal C futásidejű](https://www.microsoft.com/download/details.aspx?id=50410) előtt a Windows 10-es Windows-verzión.</span><span class="sxs-lookup"><span data-stu-id="c753b-111">Install the [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) on Windows versions prior to Windows 10.</span></span>
  <span data-ttu-id="c753b-112">Közvetlen letöltésére vagy a Windows Update-n keresztül érhető el.</span><span class="sxs-lookup"><span data-stu-id="c753b-112">It is available via direct download or Windows Update.</span></span>
  <span data-ttu-id="c753b-113">Teljes mértékben javítva (választható csomagot is beleértve), a támogatott rendszerek már rendelkezik a telepített.</span><span class="sxs-lookup"><span data-stu-id="c753b-113">Fully patched (including optional packages), supported systems will already have this installed.</span></span>
- <span data-ttu-id="c753b-114">Telepítse a Windows Management Framework (WMF) 4.0-s vagy újabb Windows 7 és Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="c753b-114">Install the Windows Management Framework (WMF) 4.0 or newer on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="zip"></a><span data-ttu-id="c753b-115">ZIP</span><span class="sxs-lookup"><span data-stu-id="c753b-115">ZIP</span></span>

<span data-ttu-id="c753b-116">PowerShell-bináris ZIP-archívumok állnak rendelkezésre a speciális telepítési forgatókönyvek megvalósítását teszik lehetővé.</span><span class="sxs-lookup"><span data-stu-id="c753b-116">PowerShell binary ZIP archives are provided to enable advanced deployment scenarios.</span></span>
<span data-ttu-id="c753b-117">Fontos megjegyezni, hogy a ZIP-archívumot használata esetén nem jelenik meg az Előfeltételek ellenőrzése, mint az MSI-csomag.</span><span class="sxs-lookup"><span data-stu-id="c753b-117">Be noted that when using the ZIP archive, you won't get the prerequisites check as in the MSI package.</span></span>
<span data-ttu-id="c753b-118">Ezért ahhoz a wsman által használt keresztül távelérése megfelelő működéséhez a Windows 10-es előtti Windows-verzión, győződjön meg arról, hogy kell a [Előfeltételek](#prerequisites) teljesülnek-e.</span><span class="sxs-lookup"><span data-stu-id="c753b-118">So in order for remoting over WSMan to work properly on Windows versions prior to Windows 10, you need to make sure the [prerequisites](#prerequisites) are met.</span></span>

## <a name="deploying-on-windows-iot"></a><span data-ttu-id="c753b-119">A Windows IoT üzembe helyezése</span><span class="sxs-lookup"><span data-stu-id="c753b-119">Deploying on Windows IoT</span></span>

<span data-ttu-id="c753b-120">A Windows PowerShell-lel történő üzembe helyezése a PowerShell Core 6-os használjuk, amely már van Windows IoT.</span><span class="sxs-lookup"><span data-stu-id="c753b-120">Windows IoT already comes with Windows PowerShell which we will use to deploy PowerShell Core 6.</span></span>

1. <span data-ttu-id="c753b-121">Hozzon létre `PSSession` a céleszköz</span><span class="sxs-lookup"><span data-stu-id="c753b-121">Create `PSSession` to target device</span></span>

   ```powershell
   $s = New-PSSession -ComputerName <deviceIp> -Credential Administrator
   ```

2. <span data-ttu-id="c753b-122">Másolja a ZIP-csomagját az eszközön</span><span class="sxs-lookup"><span data-stu-id="c753b-122">Copy the ZIP package to the device</span></span>

   ```powershell
   # change the destination to however you had partitioned it with sufficient
   # space for the zip and the unzipped contents
   # the path should be local to the device
   Copy-Item .\PowerShell-6.0.2-win-arm32.zip -Destination u:\users\administrator\Downloads -ToSession $s
   ```

3. <span data-ttu-id="c753b-123">Az eszköz csatlakozik, és bontsa ki az archívum</span><span class="sxs-lookup"><span data-stu-id="c753b-123">Connect to the device and expand the archive</span></span>

   ```powershell
   Enter-PSSession $s
   cd u:\users\administrator\downloads
   Expand-Archive .\PowerShell-6.0.2-win-arm32.zip
   ```

4. <span data-ttu-id="c753b-124">A telepítő távoli eljáráshívás a PowerShell Core 6-os</span><span class="sxs-lookup"><span data-stu-id="c753b-124">Setup remoting to PowerShell Core 6</span></span>

   ```powershell
   cd .\PowerShell-6.0.2-win-arm32
   # Be sure to use the -PowerShellHome parameter otherwise it'll try to create a new
   # endpoint with Windows PowerShell 5.1
   .\Install-PowerShellRemoting.ps1 -PowerShellHome .
   # You'll get an error message and will be disconnected from the device because it has to restart WinRM
   ```

5. <span data-ttu-id="c753b-125">Csatlakozhat a PowerShell Core 6-os végpont az eszközön</span><span class="sxs-lookup"><span data-stu-id="c753b-125">Connect to PowerShell Core 6 endpoint on device</span></span>

   ```powershell
   # Be sure to use the -Configuration parameter.  If you omit it, you will connect to Windows PowerShell 5.1
   Enter-PSSession -ComputerName <deviceIp> -Credential Administrator -Configuration powershell.6.0.2
   ```

## <a name="deploying-on-nano-server"></a><span data-ttu-id="c753b-126">A Nano Server üzembe helyezése</span><span class="sxs-lookup"><span data-stu-id="c753b-126">Deploying on Nano Server</span></span>

<span data-ttu-id="c753b-127">Ezek az utasítások feltételezik, hogy egy PowerShell-verzió már fut a Nano Server-rendszerképet és, hogy a létrehozott által a [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).</span><span class="sxs-lookup"><span data-stu-id="c753b-127">These instructions assume that a version of PowerShell is already running on the Nano Server image and that it has been generated by the [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).</span></span>
<span data-ttu-id="c753b-128">A nano Server egy "távfelügyelt" operációs rendszer.</span><span class="sxs-lookup"><span data-stu-id="c753b-128">Nano Server is a "headless" OS.</span></span> <span data-ttu-id="c753b-129">Az alapvető bináris fájlokat telepítheti két különböző módszer használatával.</span><span class="sxs-lookup"><span data-stu-id="c753b-129">Core binaries can be deploy using two different methods.</span></span>

1. <span data-ttu-id="c753b-130">Offline – a Nano Server virtuális merevlemez csatlakoztatása, és csomagolja ki a zip-fájlt a kiválasztott helyen belül a csatlakoztatott lemezkép tartalmát.</span><span class="sxs-lookup"><span data-stu-id="c753b-130">Offline - Mount the Nano Server VHD and unzip the contents of the zip file to your chosen location within the mounted image.</span></span>
2. <span data-ttu-id="c753b-131">Online – a zip-fájl átvitel egy PowerShell-munkamenetet, és bontsa ki azt a kiválasztott helyen.</span><span class="sxs-lookup"><span data-stu-id="c753b-131">Online - Transfer the zip file over a PowerShell Session and unzip it in your chosen location.</span></span>

<span data-ttu-id="c753b-132">Mindkét esetben szüksége lesz a Windows 10-es x64 ZIP kiadási csomag és a egy "Rendszergazda" PowerShell-példány belül lévő parancsok futtatásával.</span><span class="sxs-lookup"><span data-stu-id="c753b-132">In both cases, you will need the Windows 10 x64 ZIP release package and will need to run the commands within an "Administrator" PowerShell instance.</span></span>

### <a name="offline-deployment-of-powershell-core"></a><span data-ttu-id="c753b-133">Offline állapotban van a PowerShell Core telepítése</span><span class="sxs-lookup"><span data-stu-id="c753b-133">Offline Deployment of PowerShell Core</span></span>

1. <span data-ttu-id="c753b-134">A kedvenc zip segédprogrammal tömörítse ki a csomagot egy könyvtárba, a csatlakoztatott Nano Server-rendszerképben.</span><span class="sxs-lookup"><span data-stu-id="c753b-134">Use your favorite zip utility to unzip the package to a directory within the mounted Nano Server image.</span></span>
2. <span data-ttu-id="c753b-135">Válassza le a lemezképet, és indítsa el azt.</span><span class="sxs-lookup"><span data-stu-id="c753b-135">Unmount the image and boot it.</span></span>
3. <span data-ttu-id="c753b-136">Csatlakozzon a Windows PowerShell Beérkezett üzenetek példányához.</span><span class="sxs-lookup"><span data-stu-id="c753b-136">Connect to the inbox instance of Windows PowerShell.</span></span>
4. <span data-ttu-id="c753b-137">Kövesse az utasításokat, hozzon létre egy távoli eljáráshívás végpont a ["egy másik példány technikával"](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="c753b-137">Follow the instructions to create a remoting endpoint using the ["another instance technique"](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

### <a name="online-deployment-of-powershell-core"></a><span data-ttu-id="c753b-138">Online-hoz a PowerShell Core telepítése</span><span class="sxs-lookup"><span data-stu-id="c753b-138">Online Deployment of PowerShell Core</span></span>

<span data-ttu-id="c753b-139">A következő lépések végigvezetik a PowerShell Core telepítése a Nano Server és a távoli végpont konfigurációját egy futó példányával.</span><span class="sxs-lookup"><span data-stu-id="c753b-139">The following steps guide you through the deployment of PowerShell Core to a running instance of Nano Server and the configuration of its remote endpoint.</span></span>

- <span data-ttu-id="c753b-140">Csatlakozzon a Windows PowerShell Beérkezett üzenetek példányához</span><span class="sxs-lookup"><span data-stu-id="c753b-140">Connect to the inbox instance of Windows PowerShell</span></span>

  ```powershell
  $session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
  ```

- <span data-ttu-id="c753b-141">Másolja a fájlt a Nano Server-példány</span><span class="sxs-lookup"><span data-stu-id="c753b-141">Copy the file to the Nano Server instance</span></span>

  ```powershell
  Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
  ```

- <span data-ttu-id="c753b-142">Adja meg a munkamenet</span><span class="sxs-lookup"><span data-stu-id="c753b-142">Enter the session</span></span>

  ```powershell
  Enter-PSSession $session
  ```

- <span data-ttu-id="c753b-143">Bontsa ki a ZIP-fájl</span><span class="sxs-lookup"><span data-stu-id="c753b-143">Extract the ZIP file</span></span>

  ```powershell
  # Insert the appropriate version.
  Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
  ```

- <span data-ttu-id="c753b-144">Ha azt szeretné, hogy a WSMan-alapú távoli eljáráshívás, kövesse az utasításokat hozzon létre egy távoli eljáráshívás végpont a ["egy másik példány technikával"](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="c753b-144">If you want WSMan-based remoting, follow the instructions to create a remoting endpoint using the ["another instance technique"](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="c753b-145">A távoli eljáráshívás végpont létrehozására vonatkozó utasításokat</span><span class="sxs-lookup"><span data-stu-id="c753b-145">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="c753b-146">A PowerShell Core a PowerShell távoli eljáráshívás protokoll (PSRP) támogatja a wsman által használt és az SSH keresztül.</span><span class="sxs-lookup"><span data-stu-id="c753b-146">PowerShell Core supports the PowerShell Remoting Protocol (PSRP) over both WSMan and SSH.</span></span>
<span data-ttu-id="c753b-147">További információ:</span><span class="sxs-lookup"><span data-stu-id="c753b-147">For more information, see:</span></span>

- <span data-ttu-id="c753b-148">[SSH távoli eljáráshívás a PowerShell Core][ssh-remoting]</span><span class="sxs-lookup"><span data-stu-id="c753b-148">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
- <span data-ttu-id="c753b-149">[A PowerShell Core a wsman által használt távoli eljáráshívás][wsman-remoting]</span><span class="sxs-lookup"><span data-stu-id="c753b-149">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

## <a name="artifact-installation-instructions"></a><span data-ttu-id="c753b-150">Összetevő telepítési utasításokat</span><span class="sxs-lookup"><span data-stu-id="c753b-150">Artifact Installation Instructions</span></span>

<span data-ttu-id="c753b-151">Coreclr-nek bits minden CI-build-a az archívumot közzétesszük [AppVeyor][].</span><span class="sxs-lookup"><span data-stu-id="c753b-151">We publish an archive with CoreCLR bits on every CI build with [AppVeyor][].</span></span>

<span data-ttu-id="c753b-152">A PowerShell Core telepítése a coreclr-nek összetevő:</span><span class="sxs-lookup"><span data-stu-id="c753b-152">To install PowerShell Core from the CoreCLR Artifact:</span></span>

1. <span data-ttu-id="c753b-153">Töltse le a ZIP-csomagját **összetevők** az adott build lapján.</span><span class="sxs-lookup"><span data-stu-id="c753b-153">Download ZIP package from **artifacts** tab of the particular build.</span></span>
2. <span data-ttu-id="c753b-154">Feloldása ZIP-fájl: kattintson a jobb gombbal a Fájlkezelőben -> Properties -> box -> feloldása a alkalmazni ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="c753b-154">Unblock ZIP file: right-click in File Explorer -> Properties -> check 'Unblock' box -> apply</span></span>
3. <span data-ttu-id="c753b-155">Bontsa ki a zip-fájlt `bin` könyvtár</span><span class="sxs-lookup"><span data-stu-id="c753b-155">Extract zip file to `bin` directory</span></span>
4. `./bin/pwsh.exe`

<!-- [download-center]: TODO -->

[kiadások]: https://github.com/PowerShell/PowerShell/releases
[releases]: https://github.com/PowerShell/PowerShell/releases
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell
