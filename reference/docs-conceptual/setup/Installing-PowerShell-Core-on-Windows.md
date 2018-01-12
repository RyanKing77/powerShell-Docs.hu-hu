# <a name="installing-powershell-core-on-windows"></a><span data-ttu-id="dc223-101">A Windows PowerShell központi telepítése</span><span class="sxs-lookup"><span data-stu-id="dc223-101">Installing PowerShell Core on Windows</span></span>

## <a name="msi"></a><span data-ttu-id="dc223-102">MSI-FÁJL</span><span class="sxs-lookup"><span data-stu-id="dc223-102">MSI</span></span>

<span data-ttu-id="dc223-103">PowerShell telepítsen egy Windows ügyfél vagy a Windows Server (működik a Windows 7 SP1, Server 2008 R2 és újabb verziók), töltse le az MSI-csomagot</span><span class="sxs-lookup"><span data-stu-id="dc223-103">To install PowerShell on a Windows client or Windows Server (works on Windows 7 SP1, Server 2008 R2, and later), download the MSI package from</span></span>
<!-- TODO: either the Download Center or -->
<span data-ttu-id="dc223-104">a GitHub [kiadott][] lap.</span><span class="sxs-lookup"><span data-stu-id="dc223-104">our GitHub [releases][] page.</span></span>
<span data-ttu-id="dc223-105">Az MSI-fájl néz ki-`PowerShell-6.0.0.<buildversion>.<os-arch>.msi`</span><span class="sxs-lookup"><span data-stu-id="dc223-105">The MSI file looks like this - `PowerShell-6.0.0.<buildversion>.<os-arch>.msi`</span></span>

<span data-ttu-id="dc223-106">Miután letöltötte, kattintson duplán a telepítő, és kövesse az utasításokat.</span><span class="sxs-lookup"><span data-stu-id="dc223-106">Once downloaded, double-click the installer and follow the prompts.</span></span>

<span data-ttu-id="dc223-107">A telepítés után a Start menü helyezett helyi van.</span><span class="sxs-lookup"><span data-stu-id="dc223-107">There is a shortcut placed in the Start Menu upon installation.</span></span>

* <span data-ttu-id="dc223-108">Alapértelmezés szerint a csomag telepítés`$env:ProgramFiles\PowerShell\`</span><span class="sxs-lookup"><span data-stu-id="dc223-108">By default the package is installed to `$env:ProgramFiles\PowerShell\`</span></span>
* <span data-ttu-id="dc223-109">PowerShell keresztül a Start menüből indíthatja el vagy`$env:ProgramFiles\PowerShell\pwsh.exe`</span><span class="sxs-lookup"><span data-stu-id="dc223-109">You can launch PowerShell via the Start Menu or `$env:ProgramFiles\PowerShell\pwsh.exe`</span></span>

### <a name="prerequisites"></a><span data-ttu-id="dc223-110">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="dc223-110">Prerequisites</span></span>

<span data-ttu-id="dc223-111">A PowerShell-távelérés engedélyezése WSMan keresztül, a következő előfeltételeket kell teljesíteni:</span><span class="sxs-lookup"><span data-stu-id="dc223-111">To enable PowerShell remoting over WSMan, the following prerequisites need to be met:</span></span>

* <span data-ttu-id="dc223-112">Telepítse a [Universal C futásidejű](https://www.microsoft.com/download/details.aspx?id=50410) Windows 10 előtti Windows-verziókban.</span><span class="sxs-lookup"><span data-stu-id="dc223-112">Install the [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) on Windows versions prior to Windows 10.</span></span>
  <span data-ttu-id="dc223-113">Érhető el közvetlen letöltési vagy a Windows Update segítségével.</span><span class="sxs-lookup"><span data-stu-id="dc223-113">It is available via direct download or Windows Update.</span></span>
  <span data-ttu-id="dc223-114">Teljes lett (beleértve a csomagok nem kötelező), a támogatott rendszerek már rendelkezik a telepített.</span><span class="sxs-lookup"><span data-stu-id="dc223-114">Fully patched (including optional packages), supported systems will already have this installed.</span></span>
* <span data-ttu-id="dc223-115">Telepítse a Windows Management Framework (WMF) [4.0](https://www.microsoft.com/download/details.aspx?id=40855) vagy újabb ([5.1](https://www.microsoft.com/download/details.aspx?id=54616)) Windows 7 és Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="dc223-115">Install the Windows Management Framework (WMF) [4.0](https://www.microsoft.com/download/details.aspx?id=40855) or newer ([5.1](https://www.microsoft.com/download/details.aspx?id=54616)) on Windows 7 and Windows Server 2008 R2.</span></span>

## <a name="zip"></a><span data-ttu-id="dc223-116">A ZIP-</span><span class="sxs-lookup"><span data-stu-id="dc223-116">ZIP</span></span>

<span data-ttu-id="dc223-117">PowerShell bináris ZIP-archívum biztosított speciális telepítési forgatókönyvek engedélyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="dc223-117">PowerShell binary ZIP archives are provided to enable advanced deployment scenarios.</span></span>
<span data-ttu-id="dc223-118">Megjegyzendő, hogy a ZIP-archívum használata esetén nem jelenik meg az előfeltételek ellenőrzésének, mint az MSI-csomagot.</span><span class="sxs-lookup"><span data-stu-id="dc223-118">Be noted that when using the ZIP archive, you won't get the prerequisites check as in the MSI package.</span></span>
<span data-ttu-id="dc223-119">Így megfelelően működjön, a Windows verzió előtti Windows 10 távoli eljáráshívás keresztül WSMan érdekében győződjön meg arról, hogy kell a [Előfeltételek](#prerequisites) teljesülnek.</span><span class="sxs-lookup"><span data-stu-id="dc223-119">So in order for remoting over WSMan to work properly on Windows versions prior to Windows 10, you need to make sure the [prerequisites](#prerequisites) are met.</span></span>

## <a name="deploying-on-nano-server"></a><span data-ttu-id="dc223-120">A Nano Server telepítése</span><span class="sxs-lookup"><span data-stu-id="dc223-120">Deploying on Nano Server</span></span>

<span data-ttu-id="dc223-121">Ezek az utasítások azt feltételezik, hogy egy PowerShell verziója már fut a Nano Server lemezképet, és, hogy a létrehozott által a [Nano Server Image Builder](https://technet.microsoft.com/windows-server-docs/get-started/deploy-nano-server).</span><span class="sxs-lookup"><span data-stu-id="dc223-121">These instructions assume that a version of PowerShell is already running on the Nano Server image and that it has been generated by the [Nano Server Image Builder](https://technet.microsoft.com/windows-server-docs/get-started/deploy-nano-server).</span></span>
<span data-ttu-id="dc223-122">Nano Server egy "távfelügyeleti" operációs rendszer és a PowerShell központ bináris fájljai telepítési folyamatának akkor fordulhat elő, két különböző módon:</span><span class="sxs-lookup"><span data-stu-id="dc223-122">Nano Server is a "headless" OS and deployment of PowerShell Core binaries can happen in two different ways:</span></span>

1. <span data-ttu-id="dc223-123">Kapcsolat nélküli - a Nano Server VHD csatlakoztatására, és csomagolja ki a zip-fájl a megadott helyre belül a csatlakoztatott lemezkép tartalmát.</span><span class="sxs-lookup"><span data-stu-id="dc223-123">Offline - Mount the Nano Server VHD and unzip the contents of the zip file to your chosen location within the mounted image.</span></span>
1. <span data-ttu-id="dc223-124">Online – a zip-fájl átvitel egy PowerShell-munkamenetet, és bontsa ki azt a kiválasztott helyen.</span><span class="sxs-lookup"><span data-stu-id="dc223-124">Online - Transfer the zip file over a PowerShell Session and unzip it in your chosen location.</span></span>

<span data-ttu-id="dc223-125">Mindkét esetben szüksége lesz a Windows 10 x64 Zip kiadást csomagba, és futtassa a parancsokat egy "Rendszergazda" PowerShell példányán belül kell.</span><span class="sxs-lookup"><span data-stu-id="dc223-125">In both cases, you will need the Windows 10 x64 Zip release package and will need to run the commands within an "Administrator" PowerShell instance.</span></span>

### <a name="offline-deployment-of-powershell-core"></a><span data-ttu-id="dc223-126">PowerShell Core offline központi telepítése</span><span class="sxs-lookup"><span data-stu-id="dc223-126">Offline Deployment of PowerShell Core</span></span>

1. <span data-ttu-id="dc223-127">A kedvenc zip segédprogram használatával csomagolja ki a csomagot a csatlakoztatott Nano Server-lemezképben.</span><span class="sxs-lookup"><span data-stu-id="dc223-127">Use your favorite zip utility to unzip the package to a directory within the mounted Nano Server image.</span></span>
1. <span data-ttu-id="dc223-128">Válassza le a lemezképet, és indítsa el azt.</span><span class="sxs-lookup"><span data-stu-id="dc223-128">Unmount the image and boot it.</span></span>
1. <span data-ttu-id="dc223-129">Csatlakozzon a Beérkezett üzenetek példányához a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc223-129">Connect to the inbox instance of Windows PowerShell.</span></span>
1. <span data-ttu-id="dc223-130">Egy távoli eljáráshívás-végpontot a létrehozásához kövesse a [egy másik példány technika](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="dc223-130">Follow the instructions to create a remoting endpoint using the [another instance technique](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

### <a name="online-deployment-of-powershell-core"></a><span data-ttu-id="dc223-131">Online PowerShell központi telepítése</span><span class="sxs-lookup"><span data-stu-id="dc223-131">Online Deployment of PowerShell Core</span></span>

<span data-ttu-id="dc223-132">Az alábbi lépéseket végigvezeti Önt PowerShell központi telepítését a Nano Server és a távoli végpont konfigurációja futó példányát.</span><span class="sxs-lookup"><span data-stu-id="dc223-132">The following steps will guide you through the deployment of PowerShell Core to a running instance of Nano Server and the configuration of its remote endpoint.</span></span>

* <span data-ttu-id="dc223-133">Csatlakozzon a Beérkezett üzenetek példányához a Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc223-133">Connect to the inbox instance of Windows PowerShell</span></span>

```powershell
$session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
```

* <span data-ttu-id="dc223-134">A fájl átmásolása a Nano Server-példány</span><span class="sxs-lookup"><span data-stu-id="dc223-134">Copy the file to the Nano Server instance</span></span>

```powershell
Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
```

* <span data-ttu-id="dc223-135">Adja meg a munkamenet</span><span class="sxs-lookup"><span data-stu-id="dc223-135">Enter the session</span></span>

```powershell
Enter-PSSession $session
```

* <span data-ttu-id="dc223-136">A Zip-fájl kibontása</span><span class="sxs-lookup"><span data-stu-id="dc223-136">Extract the Zip file</span></span>

```powershell
# Insert the appropriate version.
Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
```

* <span data-ttu-id="dc223-137">Ha azt szeretné, hogy a WSMan-alapú távoli eljáráshívás, kövesse az utasításokat, a távoli eljáráshívás-végpontot a létrehozásához a [egy másik példány technika](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span><span class="sxs-lookup"><span data-stu-id="dc223-137">If you want WSMan-based remoting, follow the instructions to create a remoting endpoint using the [another instance technique](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).</span></span>

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="dc223-138">Utasítások a távoli eljáráshívás-végpont létrehozása</span><span class="sxs-lookup"><span data-stu-id="dc223-138">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="dc223-139">PowerShell Core WSMan és az SSH a PowerShell távelérése protokoll (PSRP) támogatja.</span><span class="sxs-lookup"><span data-stu-id="dc223-139">PowerShell Core supports the PowerShell Remoting Protocol (PSRP) over both WSMan and SSH.</span></span> <span data-ttu-id="dc223-140">További információ:</span><span class="sxs-lookup"><span data-stu-id="dc223-140">For more information, see:</span></span>

* <span data-ttu-id="dc223-141">[SSH PowerShell Core a távoli eljáráshívás][ssh-remoting]</span><span class="sxs-lookup"><span data-stu-id="dc223-141">[SSH Remoting in PowerShell Core][ssh-remoting]</span></span>
* <span data-ttu-id="dc223-142">[A PowerShell Core WSMan távelérése][wsman-remoting]</span><span class="sxs-lookup"><span data-stu-id="dc223-142">[WSMan Remoting in PowerShell Core][wsman-remoting]</span></span>

## <a name="artifact-installation-instructions"></a><span data-ttu-id="dc223-143">Összetevő telepítési utasításokat</span><span class="sxs-lookup"><span data-stu-id="dc223-143">Artifact Installation Instructions</span></span>

<span data-ttu-id="dc223-144">CoreCLR bitként a minden CI build az archívumban közzétesszük [AppVeyor][].</span><span class="sxs-lookup"><span data-stu-id="dc223-144">We publish an archive with CoreCLR bits on every CI build with [AppVeyor][].</span></span>

## <a name="coreclr-artifacts"></a><span data-ttu-id="dc223-145">CoreCLR összetevők</span><span class="sxs-lookup"><span data-stu-id="dc223-145">CoreCLR Artifacts</span></span>

* <span data-ttu-id="dc223-146">Töltse le a zip-csomagját **összetevők** az adott build fülre.</span><span class="sxs-lookup"><span data-stu-id="dc223-146">Download zip package from **artifacts** tab of the particular build.</span></span>
* <span data-ttu-id="dc223-147">Zip-fájl feloldása: kattintson a jobb gombbal a Fájlkezelőben -> tulajdonságai -> jelölőnégyzet jelölését -> Unblock alkalmazása</span><span class="sxs-lookup"><span data-stu-id="dc223-147">Unblock zip file: right-click in File Explorer -> Properties -> check 'Unblock' box -> apply</span></span>
* <span data-ttu-id="dc223-148">Bontsa ki a zip-fájlt `bin` könyvtár</span><span class="sxs-lookup"><span data-stu-id="dc223-148">Extract zip file to `bin` directory</span></span>
* `./bin/pwsh.exe`

<!-- [download-center]: TODO -->
[kiadott]: https://github.com/PowerShell/PowerShell/releases
[signing]: ../../tools/Sign-Package.ps1
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell
