# <a name="ws-management-wsman-remoting-in-powershell-core"></a><span data-ttu-id="087c7-101">A PowerShell Core a WS-Management (WSMan) távoli eljáráshívási</span><span class="sxs-lookup"><span data-stu-id="087c7-101">WS-Management (WSMan) Remoting in PowerShell Core</span></span> 

## <a name="instructions-to-create-a-remoting-endpoint"></a><span data-ttu-id="087c7-102">Utasítások a távoli eljáráshívás-végpont létrehozása</span><span class="sxs-lookup"><span data-stu-id="087c7-102">Instructions to Create a Remoting Endpoint</span></span>

<span data-ttu-id="087c7-103">A Windows PowerShell Core csomag tartalmaz egy beépülő modul Rendszerfelügyeleti webszolgáltatások (`pwrshplugin.dll`) és egy telepítési parancsfájlt (`Install-PowerShellRemoting.ps1`) a `$PSHome`.</span><span class="sxs-lookup"><span data-stu-id="087c7-103">The PowerShell Core package for Windows includes a WinRM plug-in (`pwrshplugin.dll`) and an installation script (`Install-PowerShellRemoting.ps1`) in `$PSHome`.</span></span>
<span data-ttu-id="087c7-104">Ezek a fájlok bejövő távoli PowerShell-kapcsolatok fogadására, ha meg van adva a végpont PowerShell engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="087c7-104">These files enable PowerShell to accept incoming PowerShell remote connections when its endpoint is specified.</span></span>

### <a name="motivation"></a><span data-ttu-id="087c7-105">Kifejlesztésének</span><span class="sxs-lookup"><span data-stu-id="087c7-105">Motivation</span></span>

<span data-ttu-id="087c7-106">Egy PowerShell telepítéséhez létesíthet-e távoli számítógépekről, amelyek PowerShell-munkamenetekben `New-PSSession` és `Enter-PSSession`.</span><span class="sxs-lookup"><span data-stu-id="087c7-106">An installation of PowerShell can establish PowerShell sessions to remote computers using `New-PSSession` and `Enter-PSSession`.</span></span>
<span data-ttu-id="087c7-107">A felhasználó engedélyezi a bejövő PowerShell távoli kapcsolatok fogadására, a Rendszerfelügyeleti webszolgáltatások távoli eljáráshívási végpont kell létrehozni.</span><span class="sxs-lookup"><span data-stu-id="087c7-107">To enable it to accept incoming PowerShell remote connections, the user must create a WinRM remoting endpoint.</span></span>
<span data-ttu-id="087c7-108">Ezt a explicit részt lehetőséget a felhasználó futtató Install-PowerShellRemoting.ps1 a WinRM-végpont létrehozása.</span><span class="sxs-lookup"><span data-stu-id="087c7-108">This is an explicit opt-in scenario where the user runs Install-PowerShellRemoting.ps1 to create the WinRM endpoint.</span></span>
<span data-ttu-id="087c7-109">A telepítési parancsfájl egy olyan rövid távú megoldás még nem működik a további funkciók `Enable-PSRemoting` ugyanaz a művelet végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="087c7-109">The installation script is a short-term solution until we add additional functionality to `Enable-PSRemoting` to perform the same action.</span></span>
<span data-ttu-id="087c7-110">További részletekért lásd: a probléma [#1193](https://github.com/PowerShell/PowerShell/issues/1193).</span><span class="sxs-lookup"><span data-stu-id="087c7-110">For more details, please see issue [#1193](https://github.com/PowerShell/PowerShell/issues/1193).</span></span>

### <a name="script-actions"></a><span data-ttu-id="087c7-111">A Parancsfájlműveletek</span><span class="sxs-lookup"><span data-stu-id="087c7-111">Script Actions</span></span>

<span data-ttu-id="087c7-112">A parancsfájl</span><span class="sxs-lookup"><span data-stu-id="087c7-112">The script</span></span>

1. <span data-ttu-id="087c7-113">A beépülő modul %windir%\System32\PowerShell belül könyvtár létrehozása</span><span class="sxs-lookup"><span data-stu-id="087c7-113">Creates a directory for the plug-in within %windir%\System32\PowerShell</span></span>
1. <span data-ttu-id="087c7-114">Erre a helyre másolja át a pwrshplugin.dll</span><span class="sxs-lookup"><span data-stu-id="087c7-114">Copies pwrshplugin.dll to that location</span></span>
1. <span data-ttu-id="087c7-115">Létrehoz egy konfigurációs fájl</span><span class="sxs-lookup"><span data-stu-id="087c7-115">Generates a configuration file</span></span>
1. <span data-ttu-id="087c7-116">Regiszterekben, amely a Rendszerfelügyeleti webszolgáltatások beépülő modul</span><span class="sxs-lookup"><span data-stu-id="087c7-116">Registers that plug-in with WinRM</span></span>

### <a name="registration"></a><span data-ttu-id="087c7-117">Regisztráció</span><span class="sxs-lookup"><span data-stu-id="087c7-117">Registration</span></span>

<span data-ttu-id="087c7-118">A parancsfájl egy rendszergazdai szintű PowerShell-munkamenetet, és két módban fut. belül kell végrehajtani.</span><span class="sxs-lookup"><span data-stu-id="087c7-118">The script must be executed within an Administrator-level PowerShell session and runs in two modes.</span></span>

#### <a name="executed-by-the-instance-of-powershell-that-it-will-register"></a><span data-ttu-id="087c7-119">Végrehajtja az, hogy regisztrálja PowerShell példánya</span><span class="sxs-lookup"><span data-stu-id="087c7-119">Executed by the instance of PowerShell that it will register</span></span>

``` powershell
Install-PowerShellRemoting.ps1
```

#### <a name="executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register"></a><span data-ttu-id="087c7-120">Hajtja végre a nevében a példányon, amely regisztrálja a PowerShell egy másik példánya</span><span class="sxs-lookup"><span data-stu-id="087c7-120">Executed by another instance of PowerShell on behalf of the instance that it will register</span></span>

``` powershell
<path to powershell>\Install-PowerShellRemoting.ps1 -PowerShellHome "<absolute path to the instance's $PSHOME>" -PowerShellVersion "<the powershell version tag>"
```

<span data-ttu-id="087c7-121">Példa:</span><span class="sxs-lookup"><span data-stu-id="087c7-121">For Example:</span></span>

``` powershell
C:\Program Files\PowerShell\6.0.0.9\Install-PowerShellRemoting.ps1 -PowerShellHome "C:\Program Files\PowerShell\6.0.0.9\" -PowerShellVersion "6.0.0-alpha.9"
```

<span data-ttu-id="087c7-122">**Megjegyzés:** a távoli eljáráshívás regisztrációs parancsfájl újraindul a Rendszerfelügyeleti webszolgáltatások, így az összes meglévő PSRP munkamenet befejeződik, a parancsfájl futtatása után azonnal.</span><span class="sxs-lookup"><span data-stu-id="087c7-122">**NOTE:** The remoting registration script will restart WinRM, so all existing PSRP sessions will terminate immediately after the script is run.</span></span> <span data-ttu-id="087c7-123">Ha futtatása egy távoli munkamenet közben, ez megszünteti a kapcsolatot.</span><span class="sxs-lookup"><span data-stu-id="087c7-123">If run during a remote session, this will terminate the connection.</span></span>

## <a name="how-to-connect-to-the-new-endpoint"></a><span data-ttu-id="087c7-124">Az új végpont csatlakoztatása</span><span class="sxs-lookup"><span data-stu-id="087c7-124">How to Connect to the New Endpoint</span></span>

<span data-ttu-id="087c7-125">Hozza létre az új PowerShell-végpont PowerShell munkamenetet megadásával `-ConfigurationName "some endpoint name"`.</span><span class="sxs-lookup"><span data-stu-id="087c7-125">Create a PowerShell session to the new PowerShell endpoint by specifying `-ConfigurationName "some endpoint name"`.</span></span> <span data-ttu-id="087c7-126">Ha csatlakozni szeretne a PowerShell-példány a fenti példa, használja:</span><span class="sxs-lookup"><span data-stu-id="087c7-126">To connect to the PowerShell instance from the example above, use either:</span></span>

``` powershell
New-PSSession ... -ConfigurationName "powershell.6.0.0-alpha.9"
Enter-PSSession ... -ConfigurationName "powershell.6.0.0-alpha.9"
```

<span data-ttu-id="087c7-127">Vegye figyelembe, hogy `New-PSSession` és `Enter-PSSession` , amely nem ad meg indítások `-ConfigurationName` az alapértelmezett PowerShell végpont által megcélzott `microsoft.powershell`.</span><span class="sxs-lookup"><span data-stu-id="087c7-127">Note that `New-PSSession` and `Enter-PSSession` invocations that do not specify `-ConfigurationName` will target the default PowerShell endpoint, `microsoft.powershell`.</span></span>
