# <a name="installing-powershell-core-on-windows"></a><span data-ttu-id="10b29-101">A PowerShell Core telepítése Windows rendszerre</span><span class="sxs-lookup"><span data-stu-id="10b29-101">Installing PowerShell Core on Windows</span></span>

## <a name="msi"></a><span data-ttu-id="10b29-102">MSI-FÁJL</span><span class="sxs-lookup"><span data-stu-id="10b29-102">MSI</span></span>

<span data-ttu-id="10b29-103">PowerShell telepítsen egy Windows ügyfél vagy a Windows Server (működik a Windows 7 SP1, Server 2008 R2 és újabb verziók), az MSI-csomag letölthető a GitHub [kiadásokban]-[] oldalon.</span><span class="sxs-lookup"><span data-stu-id="10b29-103">To install PowerShell on a Windows client or Windows Server (works on Windows 7 SP1, Server 2008 R2, and later), download the MSI package from our GitHub [releases][] page.</span></span>

<span data-ttu-id="10b29-104">Az MSI-fájl néz ki- `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well --></span><span class="sxs-lookup"><span data-stu-id="10b29-104">The MSI file looks like this - `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well --></span></span>

<span data-ttu-id="10b29-105">Miután letöltötte, kattintson duplán a telepítő, és kövesse az utasításokat.</span><span class="sxs-lookup"><span data-stu-id="10b29-105">Once downloaded, double-click the installer and follow the prompts.</span></span>

<span data-ttu-id="10b29-106">A telepítés után a Start menü helyezett helyi van.</span><span class="sxs-lookup"><span data-stu-id="10b29-106">There is a shortcut placed in the Start Menu upon installation.</span></span>

- <span data-ttu-id="10b29-107">Alapértelmezés szerint a csomag telepítés `$env:ProgramFiles\PowerShell\<version>`</span><span class="sxs-lookup"><span data-stu-id="10b29-107">By default the package is installed to `$env:ProgramFiles\PowerShell\<version>`</span></span>
- <span data-ttu-id="10b29-108">PowerShell keresztül a Start menüből indíthatja el vagy `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span><span class="sxs-lookup"><span data-stu-id="10b29-108">You can launch PowerShell via the Start Menu or `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`</span></span>

### <a name="prerequisites"></a><span data-ttu-id="10b29-109">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="10b29-109">Prerequisites</span></span>

<span data-ttu-id="10b29-110">A PowerShell-távelérés engedélyezése WSMan keresztül, a következő előfeltételeket kell teljesíteni:</span><span class="sxs-lookup"><span data-stu-id="10b29-110">To enable PowerShell remoting over WSMan, the following prerequisites need to be met:</span></span>

- <span data-ttu-id="10b29-111">Telepítse a [Universal C futásidejű](https://www.microsoft.com/download/details.aspx?id=50410) Windows 10 előtti Windows-verziókban.</span><span class="sxs-lookup"><span data-stu-id="10b29-111">Install the [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) on Windows versions prior to Windows 10.</span></span>
  <span data-ttu-id="10b29-112">Érhető el közvetlen letöltési vagy a Windows Update segítségével.</span><span class="sxs-lookup"><span data-stu-id="10b29-112">It is available via direct download or Windows Update.</span></span>
  <span data-ttu-id="10b29-113">Teljes lett (beleértve a csomagok nem kötelező), a támogatott rendszerek már rendelkezik a telepített.</span><span class="sxs-lookup"><span data-stu-id="10b29-113">Fully patched (including optional packages), supported systems will already have this installed.</span></span>
- <span data-ttu-id="10b29-114">Telepítse a Windows Management Framework (WMF) 4.0-s vagy újabb Windows 7 és Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="10b29-114">Install the Windows Management Framework (WMF) 4.0 or newer on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="zip"></a><span data-ttu-id="10b29-115">A ZIP-</span><span class="sxs-lookup"><span data-stu-id="10b29-115">ZIP</span></span>

<span data-ttu-id="10b29-116">PowerShell bináris ZIP-archívum biztosított speciális telepítési forgatókönyvek engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="10b29-116">PowerShell binary ZIP archives are provided to enable advanced deployment scenarios.</span></span>
<span data-ttu-id="10b29-117">Megjegyzendő, hogy a ZIP-archívum használata esetén nem jelenik meg az előfeltételek ellenőrzésének, mint az MSI-csomagot.</span><span class="sxs-lookup"><span data-stu-id="10b29-117">Be noted that when using the ZIP archive, you won't get the prerequisites check as in the MSI package.</span></span>
<span data-ttu-id="10b29-118">Így megfelelően működjön, a Windows verzió előtti Windows 10 távoli eljáráshívás keresztül WSMan érdekében győződjön meg arról, hogy kell a [Előfeltételek](#prerequisites) teljesülnek.</span><span class="sxs-lookup"><span data-stu-id="10b29-118">So in order for remoting over WSMan to work properly on Windows versions prior to Windows 10, you need to make sure the [prerequisites](#prerequisites) are met.</span></span>

## <a name="deploying-on-windows-iot"></a><span data-ttu-id="10b29-119">A Windows IoT központi telepítése</span><span class="sxs-lookup"><span data-stu-id="10b29-119">Deploying on Windows IoT</span></span>

<span data-ttu-id="10b29-120">Windows IoT már rendelkezik a Windows PowerShell használatával, amely PowerShell Core 6 telepítendő használjuk.</span><span class="sxs-lookup"><span data-stu-id="10b29-120">Windows IoT already comes with Windows PowerShell which we will use to deploy PowerShell Core 6.</span></span>

1. <span data-ttu-id="10b29-121">Hozzon létre `PSSession` a céleszköz</span><span class="sxs-lookup"><span data-stu-id="10b29-121">Create `PSSession` to target device</span></span>

   ```powershell
   $s = New-PSSession -ComputerName <deviceIp> -Credential Administrator
   ```

2. <span data-ttu-id="10b29-122">Másolja át a ZIP-csomagját az eszközre</span><span class="sxs-lookup"><span data-stu-id="10b29-122">Copy the ZIP package to the device</span></span>

   ```powershell
   # change the destination to however you had partitioned it with sufficient
   # space for the zip and the unzipped contents
   # the path should be local to the device
   Copy-Item .\PowerShell-6.0.2-win-arm32.zip -Destination u:\users\administrator\Downloads -ToSession $s
   ```

3. <span data-ttu-id="10b29-123">Az eszköz csatlakozhat, és bontsa ki az archívumban</span><span class="sxs-lookup"><span data-stu-id="10b29-123">Connect to the device and expand the archive</span></span>

   ```powershell
   Enter-PSSession $s
   cd u:\users\administrator\downloads
   Expand-Archive .\PowerShell-6.0.2-win-arm32.zip
   ```

4. <span data-ttu-id="10b29-124">A telepítő a távelérés PowerShell Core 6</span><span class="sxs-lookup"><span data-stu-id="10b29-124">Setup remoting to PowerShell Core 6</span></span>

   ```powershell
   cd .\PowerShell-6.0.2-win-arm32
   # Be sure to use the -PowerShellHome parameter otherwise it'll try to create a new
   # endpoint with Windows PowerShell 5.1
   .\Install-PowerShellRemoting.ps1 -PowerShellHome .
   # You'll get an error message and will be disconnected from the device because it has to restart WinRM
   ```

5. <span data-ttu-id="10b29-125">Hogy eszközön PowerShell Core 6 végponthoz kapcsolódjon.</span><span class="sxs-lookup"><span data-stu-id="10b29-125">Connect to PowerShell Core 6 endpoint on device</span></span>

   ```powershell
   # Be sure to use the -Configuration parameter.  If you omit it, you will connect to Windows PowerShell 5.1
   Enter-PSSession -ComputerName <deviceIp> -Credential Administrator -Configuration powershell.6.0.2
   ```

## <a name="deploying-on-nano-server"></a><span data-ttu-id="10b29-126">A Nano Server telepítése</span><span class="sxs-lookup"><span data-stu-id="10b29-126">Deploying on Nano Server</span></span>

<span data-ttu-id="10b29-127">Ezek az utasítások azt feltételezik, hogy egy PowerShell verziója már fut a Nano Server lemezképet, és, hogy a létrehozott által a [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).</span><span class="sxs-lookup"><span data-stu-id="10b29-127">These instructions assume that a version of PowerShell is already running on the Nano Server image and that it has been generated by the [Nano Server Image Builder](/windows-server/get-started/deploy-nano-server).</span></span>
<span data-ttu-id="10b29-128">Nano Server egy "távfelügyeleti" operációs rendszer.</span><span class="sxs-lookup"><span data-stu-id="10b29-128">Nano Server is a "headless" OS.</span></span> <span data-ttu-id="10b29-129">Core bináris két különböző módszerekkel telepítheti meg.</span><span class="sxs-lookup"><span data-stu-id="10b29-129">Core binaries can be deploy using two different methods.</span></span>

1. <span data-ttu-id="10b29-130">Kapcsolat nélküli - a Nano Server VHD csatlakoztatására, és csomagolja ki a zip-fájl a megadott helyre belül a csatlakoztatott lemezkép tartalmát.</span><span class="sxs-lookup"><span data-stu-id="10b29-130">Offline - Mount the Nano Server VHD and unzip the contents of the zip file to your chosen location within the mounted image.</span></span>
2. <span data-ttu-id="10b29-131">Online – a zip-fájl átvitel egy PowerShell-munkamenetet, és bontsa ki azt a kiválasztott helyen.</span><span class="sxs-lookup"><span data-stu-id="10b29-131">Online - Transfer the zip file over a PowerShell Session and unzip it in your chosen location.</span></span>

<span data-ttu-id="10b29-132">Mindkét esetben szüksége lesz a Windows 10 x64 ZIP kiadást csomagba, és futtassa a parancsokat egy "Rendszergazda" PowerShell példányán belül kell.</span><span class="sxs-lookup"><span data-stu-id="10b29-132">In both cases, you will need the Windows 10 x64 ZIP release package and will need to run the commands within an "Administrator" PowerShell instance.</span></span>

### <a name="offline-deployment-of-powershell-core"></a><span data-ttu-id="10b29-133">PowerShell Core offline központi telepítése</span><span class="sxs-lookup"><span data-stu-id="10b29-133">Offline Deployment of PowerShell Core</span></span>

1. <span data-ttu-id="10b29-134">A kedvenc zip segédprogram használatával csomagolja ki a csomagot a csatlakoztatott Nano Server-lemezképben.</span><span class="sxs-lookup"><span data-stu-id="10b29-134">Use your favorite zip utility to unzip the package to a directory within the mounted Nano Server image.</span></span>
2. <span data-ttu-id="10b29-135">Válassza le a lemezképet, és indítsa el azt.</span><span class="sxs-lookup"><span data-stu-id="10b29-135">Unmount the image and boot it.</span></span>
3. <span data-ttu-id="10b29-136">Csatlakozzon a Beérkezett üzenetek példányához a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10b29-136">Connect to the inbox instance of Windows PowerShell.</span></span>
4. <span data-ttu-id="10b29-137">Egy távoli eljáráshívás-végpontot a létrehozásához kövesse a ["egy másik példány technika"](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="10b29-137">Follow the instructions to create a remoting endpoint using the ["another instance technique"](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

### <a name="online-deployment-of-powershell-core"></a><span data-ttu-id="10b29-138">Online PowerShell központi telepítése</span><span class="sxs-lookup"><span data-stu-id="10b29-138">Online Deployment of PowerShell Core</span></span>

<span data-ttu-id="10b29-139">A következő lépések végigvezetik PowerShell központi telepítését a Nano Server és a távoli végpont konfigurációja futó példányát.</span><span class="sxs-lookup"><span data-stu-id="10b29-139">The following steps guide you through the deployment of PowerShell Core to a running instance of Nano Server and the configuration of its remote endpoint.</span></span>

- <span data-ttu-id="10b29-140">Csatlakozzon a Beérkezett üzenetek példányához a Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="10b29-140">Connect to the inbox instance of Windows PowerShell</span></span>

  ```powershell
  $session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
  ```

- <span data-ttu-id="10b29-141">A fájl átmásolása a Nano Server-példány</span><span class="sxs-lookup"><span data-stu-id="10b29-141">Copy the file to the Nano Server instance</span></span>

  ```powershell
  Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
  ```

- <span data-ttu-id="10b29-142">Adja meg a munkamenet</span><span class="sxs-lookup"><span data-stu-id="10b29-142">Enter the session</span></span>

  ```powershell
  Enter-PSSession $session
  ```

- <span data-ttu-id="10b29-143">A ZIP-fájl kibontása</span><span class="sxs-lookup"><span data-stu-id="10b29-143">Extract the ZIP file</span></span>

  ```powershell
  # Insert the appropriate version.
  Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
  ```

- <span data-ttu-id="10b29-144">Ha azt szeretné, hogy a WSMan-alapú távoli eljáráshívás, kövesse az utasításokat, a távoli eljáráshívás-végpontot a létrehozásához a ["egy másik példány technika"](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="10b29-144">If you want WSMan-based remoting, follow the instructions to create a remoting endpoint using the ["another instance technique"](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="10b29-145">Utasítások a távoli eljáráshívás-végpont létrehozása</span><span class="sxs-lookup"><span data-stu-id="10b29-145">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="10b29-146">PowerShell Core WSMan és az SSH a PowerShell távelérése protokoll (PSRP) támogatja.</span><span class="sxs-lookup"><span data-stu-id="10b29-146">PowerShell Core supports the PowerShell Remoting Protocol (PSRP) over both WSMan and SSH.</span></span>
<span data-ttu-id="10b29-147">További információ:</span><span class="sxs-lookup"><span data-stu-id="10b29-147">For more information, see:</span></span>

- <span data-ttu-id="10b29-148">[SSH PowerShell Core a távoli eljáráshívás] [ssh-távoli eljáráshívási]</span><span class="sxs-lookup"><span data-stu-id="10b29-148">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
- <span data-ttu-id="10b29-149">[A PowerShell Core WSMan távoli eljáráshívási] [a wsman-távelérése]</span><span class="sxs-lookup"><span data-stu-id="10b29-149">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

## <a name="artifact-installation-instructions"></a><span data-ttu-id="10b29-150">Összetevő telepítési utasításokat</span><span class="sxs-lookup"><span data-stu-id="10b29-150">Artifact Installation Instructions</span></span>

<span data-ttu-id="10b29-151">A minden CI build [AppVeyor] szögletes CoreCLR bites archiválhatja közzétesszük.</span><span class="sxs-lookup"><span data-stu-id="10b29-151">We publish an archive with CoreCLR bits on every CI build with [AppVeyor][].</span></span>

<span data-ttu-id="10b29-152">PowerShell Core CoreCLR összetevő telepítését:</span><span class="sxs-lookup"><span data-stu-id="10b29-152">To install PowerShell Core from the CoreCLR Artifact:</span></span>

1. <span data-ttu-id="10b29-153">Töltse le a ZIP-csomagját **összetevők** az adott build fülre.</span><span class="sxs-lookup"><span data-stu-id="10b29-153">Download ZIP package from **artifacts** tab of the particular build.</span></span>
2. <span data-ttu-id="10b29-154">ZIP-fájl feloldása: kattintson a jobb gombbal a Fájlkezelőben -> tulajdonságai -> jelölőnégyzet jelölését -> Unblock alkalmazása</span><span class="sxs-lookup"><span data-stu-id="10b29-154">Unblock ZIP file: right-click in File Explorer -> Properties -> check 'Unblock' box -> apply</span></span>
3. <span data-ttu-id="10b29-155">Bontsa ki a zip-fájlt `bin` könyvtár</span><span class="sxs-lookup"><span data-stu-id="10b29-155">Extract zip file to `bin` directory</span></span>
4. `./bin/pwsh.exe`

<span data-ttu-id="10b29-156"><!-- [download-center]: TODO --> [kiadott]: https://github.com/PowerShell/PowerShell/releases [ssh-távoli eljáráshívási]:... [a wsman-távelérése] /Core-PowerShell/SSH-Remoting-in-PowerShell-Core.md:... [AppVeyor] /Core-PowerShell/WSMan-Remoting-in-PowerShell-Core.md: https://ci.appveyor.com/project/PowerShell/powershell</span><span class="sxs-lookup"><span data-stu-id="10b29-156"><!-- [download-center]: TODO --> [releases]: https://github.com/PowerShell/PowerShell/releases [ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md [wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md [AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell</span></span>