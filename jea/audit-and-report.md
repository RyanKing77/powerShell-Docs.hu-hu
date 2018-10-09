---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: Naplózás és a JEA-jelentések
ms.openlocfilehash: 2388c735840d8d3683aa8bc9869b9fb0371e5902
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851220"
---
# <a name="auditing-and-reporting-on-jea"></a><span data-ttu-id="d8cf0-103">Naplózás és a JEA-jelentések</span><span class="sxs-lookup"><span data-stu-id="d8cf0-103">Auditing and Reporting on JEA</span></span>

> <span data-ttu-id="d8cf0-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="d8cf0-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="d8cf0-105">Miután telepítette a JEA, célszerű rendszeresen naplózása a JEA-konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-105">After you've deployed JEA, you will want to regularly audit the JEA configuration.</span></span>
<span data-ttu-id="d8cf0-106">Ez segít mérje fel, ha a megfelelő személyeknek fér hozzá a JEA-végpont, és a hozzárendelt szerepkörök továbbra is megfelelőek.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-106">This will help you assess if the correct people have access to the JEA endpoint and if their assigned roles are still appropriate.</span></span>

<span data-ttu-id="d8cf0-107">Ez a témakör ismerteti a különböző módszereket a JEA-végpont naplózhatók.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-107">This topic describes the various ways you can audit a JEA endpoint.</span></span>

## <a name="find-registered-jea-sessions-on-a-machine"></a><span data-ttu-id="d8cf0-108">Keresse meg a regisztrált JEA munkamenetek gépen</span><span class="sxs-lookup"><span data-stu-id="d8cf0-108">Find registered JEA sessions on a machine</span></span>

<span data-ttu-id="d8cf0-109">Ellenőrizze, hogy mely JEA munkamenetek gépen regisztrált, használja a [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-109">To check which JEA sessions are registered on a machine, use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet.</span></span>

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
PS C:\> Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }


Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed, CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

<span data-ttu-id="d8cf0-110">A hatékony jogok a végpont a "Engedély" tulajdonság szerepel.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-110">The effective rights for the endpoint are listed in the "Permission" property.</span></span>
<span data-ttu-id="d8cf0-111">Ezek a felhasználók jogosult csatlakozni a JEA-végpont, de mely szerepkörök (és, parancsok) határozza meg a "RoleDefinitions" mezője hozzáféréssel rendelkeznek a [munkamenet konfigurációs fájl](session-configurations.md) regisztrálásához használt a a végpont.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-111">These users have the right to connect to the JEA endpoint, but which roles (and, by extension, commands) they have access to is determined by the "RoleDefinitions" field in the [session configuration file](session-configurations.md) that was used to register the endpoint.</span></span>

<span data-ttu-id="d8cf0-112">Az adatok a "RoleDefinitions" tulajdonságban kibontásával kiértékelheti egy regisztrált a JEA-végpont a szerepkör-hozzárendelések.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-112">You can evaluate the role mappings in a registered JEA endpoint by expanding the data in the "RoleDefinitions" property.</span></span>

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{ Name = 'Role Capabilities'; Expression = { $_.Value.RoleCapabilities } }
```

## <a name="find-available-role-capabilities-on-the-machine"></a><span data-ttu-id="d8cf0-113">A gépen elérhető szerepköri funkciók keresése</span><span class="sxs-lookup"><span data-stu-id="d8cf0-113">Find available role capabilities on the machine</span></span>

<span data-ttu-id="d8cf0-114">Szerepkör képesség fájlok csak által használandó JEA belül egy érvényes PowerShell-modul egy "RoleCapabilities" mappában vannak tárolva.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-114">Role capability files will only be used by JEA if they are stored in a "RoleCapabilities" folder inside a valid PowerShell module.</span></span>
<span data-ttu-id="d8cf0-115">A számítógépen elérhető összes szerepköri funkciók az elérhető modulok listáját kereséssel találhatja meg.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-115">You can find all role capabilities available on a computer by searching the list of available modules.</span></span>

```powershell
function Find-LocalRoleCapability {
    $results = @()

    # Find modules with a "RoleCapabilities" subfolder and add any PSRC files to the result set
    Get-Module -ListAvailable | ForEach-Object {
        $psrcpath = Join-Path -Path $_.ModuleBase -ChildPath 'RoleCapabilities'
        if (Test-Path $psrcpath) {
            $results += Get-ChildItem -Path $psrcpath -Filter *.psrc
        }
    }

    # Format the results nicely to make it easier to read
    $results | Select-Object @{ Name = 'Name'; Expression = { $_.Name.TrimEnd('.psrc') }}, @{ Name = 'Path'; Expression = { $_.FullName }} | Sort-Object Name
}
```

> [!NOTE]
> <span data-ttu-id="d8cf0-116">Ez a függvény eredményeinek sorrendje nem feltétlenül a sorrend, amelyben a szerepkörrel képességeket lesz kiválasztva, ha több szerepkörrel képességeket rendelkezik ugyanazzal a névvel.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-116">The order of results from this function is not necessarily the order in which the role capabilities will be selected if multiple role capabilities share the same name.</span></span>

## <a name="check-effective-rights-for-a-specific-user"></a><span data-ttu-id="d8cf0-117">Egy adott felhasználó hatékony jogok ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="d8cf0-117">Check effective rights for a specific user</span></span>

<span data-ttu-id="d8cf0-118">A JEA-végpont beállítása után érdemes ellenőrizni a JEA munkamenetben egy adott felhasználó számára rendelkezésre álló parancsokat.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-118">Once you have set up a JEA endpoint, you may want to check which commands are available to a specific user in a JEA session.</span></span>
<span data-ttu-id="d8cf0-119">Használhat [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) számbavétele az összes alkalmazható egy felhasználó számára a parancsok, mintha azok az aktuális csoporttagságok JEA munkamenet indításához.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-119">You can use [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) to enumerate all of the commands applicable to a user if they were to start a JEA session with their current group memberships.</span></span>
<span data-ttu-id="d8cf0-120">A kimenet a `Get-PSSessionCapability` megegyezik-e a megadott futtató felhasználó `Get-Command -CommandType All` JEA munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-120">The output of `Get-PSSessionCapability` is identical to that of the specified user running `Get-Command -CommandType All` in a JEA session.</span></span>

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

<span data-ttu-id="d8cf0-121">Ha a felhasználók nem lenne jogosultságokat őket további JEA csoportokat állandó tagjai, ez a parancsmag nem tükrözik az extra engedélyeket.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-121">If your users are not permanent members of groups which would grant them additional JEA rights, this cmdlet may not reflect those extra permissions.</span></span>
<span data-ttu-id="d8cf0-122">Általában ez a helyzet, just-in-time privileged access management systems használatakor a felhasználók ideiglenesen biztonsági csoporthoz tartozik.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-122">This is typically the case when using just-in-time privileged access management systems to allow users to temporarily belong to a security group.</span></span>
<span data-ttu-id="d8cf0-123">Mindig gondosan határozza meg a felhasználók szerepkörökhöz hozzárendelését és a felhasználók csak kihozhatják a parancsok a munkájuk sikeres elvégzéséhez szükséges lehető legkevesebb való hozzáférés biztosítása érdekében szerepkörönként tartalmát.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-123">Always carefully evaluate the mapping of users to roles and the contents of each role to ensure users are only getting access to the least amount of commands needed to do their jobs successfully.</span></span>

## <a name="powershell-event-logs"></a><span data-ttu-id="d8cf0-124">PowerShell-eseménynaplók</span><span class="sxs-lookup"><span data-stu-id="d8cf0-124">PowerShell event logs</span></span>

<span data-ttu-id="d8cf0-125">Ha engedélyezte a rendszer a bejelentkezés modul és/vagy parancsfájl letiltása, lesz a Windows eseménynaplóiban keresse az egyes parancsok a JEA munkamenetekhez, futtatott egy felhasználó események található.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-125">If you enabled module and/or script block logging on the system, you will be able to find events in the Windows event logs for each command a user ran in their JEA sessions.</span></span>
<span data-ttu-id="d8cf0-126">Ezek az események megkereséséhez nyissa meg a Windows eseménynaplót, keresse meg a **Microsoft-Windows-PowerShell/műveleti** eseménynaplót, és keresse meg az események event ID **4104**.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-126">To find these events, open the Windows Event Viewer, navigate to the **Microsoft-Windows-PowerShell/Operational** event log, and look for events with event ID **4104**.</span></span>

<span data-ttu-id="d8cf0-127">Minden eseménynapló-bejegyzést, amelyben a parancs futtatása a munkamenet vonatkozó információk is.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-127">Each event log entry will include information about the session in which the command was run.</span></span>
<span data-ttu-id="d8cf0-128">JEA-munkamenetet, ez kiterjed a fontos információk a **ConnectedUser**, vagyis az aktuális felhasználó, aki létrehozta a JEA-munkamenetben, valamint a **felhasználó** amely azonosítja a JEA használt fiók hajtsa végre a parancsot.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-128">For JEA sessions, this includes important information about the **ConnectedUser**, which is the actual user who created the JEA session, as well as the **RunAsUser** which identifies the account JEA used to execute the command.</span></span>
<span data-ttu-id="d8cf0-129">Alkalmazás eseménynaplóit megjelenik a felhasználó által végrehajtott változtatások, így kellene az átiratok vagy modul parancsfájl naplózás engedélyezve kell tudniuk követni egy adott parancs meghívása vissza egy felhasználó számára rendkívül fontos.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-129">Application event logs will show changes being made by the RunAsUser, so having transcripts or module/script logging enabled is crucial to be able to trace a specific command invocation back to a user.</span></span>

## <a name="application-event-logs"></a><span data-ttu-id="d8cf0-130">Alkalmazás eseménynaplóit</span><span class="sxs-lookup"><span data-stu-id="d8cf0-130">Application event logs</span></span>

<span data-ttu-id="d8cf0-131">A JEA-munkamenetben, amellyel kommunikál egy külső alkalmazás vagy szolgáltatás egy parancs futtatásakor a ezeket az alkalmazásokat a saját eseménynaplók előfordulhat, hogy jelentkezzen események.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-131">When you run a command in a JEA session that interacts with an external application or service, those applications may log events to their own event logs.</span></span>
<span data-ttu-id="d8cf0-132">PowerShell-naplók és szövegekben, ellentétben más naplózási mechanizmusok nem rögzíti a JEA-munkamenet csatlakoztatott felhasználói, és inkább csak naplózza a virtuális futtató felhasználó vagy a csoportosan felügyelt szolgáltatásfiók.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-132">Unlike PowerShell logs and transcripts, other logging mechanisms will not capture the connected user of the JEA session, and will instead only log the virtual run-as user or group managed service account.</span></span>
<span data-ttu-id="d8cf0-133">Határozza meg, akik a parancsot futtatta, kell tekintenie a [munkamenet átiratok](#session-transcripts) vagy vesse össze a PowerShell-eseménynaplók az idő és a felhasználó látható az alkalmazások eseménynaplójában.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-133">In order to determine who ran the command, you will need to consult a [session transcript](#session-transcripts) or correlate PowerShell event logs with the time and user shown in the application event log.</span></span>

<span data-ttu-id="d8cf0-134">A WinRM-naplók is segíthetnek összekapcsolását futtató felhasználók az alkalmazások eseménynaplójában a csatlakozó felhasználó.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-134">The WinRM log can also help you correlate run as users in an application event log with the connecting user.</span></span>
<span data-ttu-id="d8cf0-135">Eseményazonosító **193** a a **Microsoft-Windows-Windows távoli felügyeleti/műveleti** rögzíti a biztonsági azonosítóval (SID) és a fiók a csatlakozó felhasználó nevét és a felhasználó minden alkalommal futtassa a JEA naplózása munkamenet jön létre.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-135">Event ID **193** in the **Microsoft-Windows-Windows Remote Management/Operational** log records the security identifier (SID) and account name for both the connecting user and run as user every time a JEA session is created.</span></span>

## <a name="session-transcripts"></a><span data-ttu-id="d8cf0-136">Munkamenet szövegekben</span><span class="sxs-lookup"><span data-stu-id="d8cf0-136">Session transcripts</span></span>

<span data-ttu-id="d8cf0-137">Ha konfigurálta a JEA egy szöveges létrehozása minden felhasználói munkamenetet, minden felhasználói műveletek szöveges másolatának a megadott mappában kell tárolni.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-137">If you configured JEA to create a transcript for each user session, a text copy of every user's actions will be stored in the specified folder.</span></span>

<span data-ttu-id="d8cf0-138">Keresse meg az összes szöveges könyvtár, az alábbi parancsot rendszergazdaként azon a számítógépen konfigurált JEA:</span><span class="sxs-lookup"><span data-stu-id="d8cf0-138">To find all transcript directories, run the following command as an administrator on the computer configured with JEA:</span></span>

```powershell
Get-PSSessionConfiguration | Where-Object { $_.TranscriptDirectory -ne $null } | Format-Table Name, TranscriptDirectory
```

<span data-ttu-id="d8cf0-139">Minden szöveges kapcsolatos információkat a munkamenet kezdete, mely a munkamenetet, és mely JEA identitás hozzá volt rendelve, a hozzájuk kapcsolódó felhasználó kezdődik.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-139">Each transcript starts with information about the time the session started, which user connected to the session, and which JEA identity was assigned to them.</span></span>

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

<span data-ttu-id="d8cf0-140">Az átirat törzsében minden egyes parancsot, a felhasználó meghívása kapcsolatos naplózott információk.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-140">In the body of the transcript, information is logged about each command the user invoked.</span></span>
<span data-ttu-id="d8cf0-141">A pontos szintaxist a parancsot futtatta a felhasználó nem érhető el a parancsokat a PowerShell-távelérést, átalakításának lehet a JEA-munkamenetek, azonban továbbra is meghatározhatja a hatékony a végrehajtott parancs.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-141">The exact syntax of the command the user ran is unavailable in JEA sessions due to the way commands are transformed for PowerShell remoting, however you can still determine the effective command that was executed.</span></span>
<span data-ttu-id="d8cf0-142">Alul látható egy példa a szövegben kódrészlet futtató felhasználó `Get-Service Dns` JEA munkamenetben:</span><span class="sxs-lookup"><span data-stu-id="d8cf0-142">Below is an example transcript snippet from a user running `Get-Service Dns` in a JEA session:</span></span>

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

<span data-ttu-id="d8cf0-143">Az egyes parancsok egy felhasználó futtatja a "CommandInvocation" sor lesz írva, amely leírja a parancsmag, vagy a meghívott felhasználó működik.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-143">For each command a user runs, a "CommandInvocation" line will be written, describing the cmdlet or function the user invoked.</span></span>
<span data-ttu-id="d8cf0-144">ParameterBindings hajtsa végre az egyes CommandInvocation állapítható meg, akkor minden paraméter és érték, amely a parancs lett megadva.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-144">ParameterBindings follow each CommandInvocation to tell you about each parameter and value that was supplied with the command.</span></span>
<span data-ttu-id="d8cf0-145">A fenti példában láthatja, hogy a "név" paraméter megadott értéke "Dns" a "Get-Service" parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-145">In the above example, you can see that the parameter "Name" was supplied the value "Dns" for the "Get-Service" cmdlet.</span></span>

<span data-ttu-id="d8cf0-146">Minden parancs kimenete is kezdeményezi egy CommandInvocation általában élekről alapértelmezettként.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-146">The output of each command will also trigger a CommandInvocation, usually to Out-Default.</span></span>
<span data-ttu-id="d8cf0-147">A Out-Default InputObject olyan PowerShell-objektum, a parancs által visszaadott.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-147">The InputObject of Out-Default is the PowerShell object returned from the command.</span></span>
<span data-ttu-id="d8cf0-148">Nyomtatási objektum részleteit az alábbi szorosan mimicking, mi a felhasználó lenne látott néhány sort.</span><span class="sxs-lookup"><span data-stu-id="d8cf0-148">The details of that object are printed a few lines below, closely mimicking what the user would have seen.</span></span>

## <a name="see-also"></a><span data-ttu-id="d8cf0-149">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d8cf0-149">See also</span></span>

- [<span data-ttu-id="d8cf0-150">*PowerShell a kék csapat ♥* biztonsági blogbejegyzés</span><span class="sxs-lookup"><span data-stu-id="d8cf0-150">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)
