---
ms.date: 07/10/2019
keywords: a jea, powershell, biztonsági
title: Naplózás és a JEA-jelentések
ms.openlocfilehash: 2afefe83acecc1fc3643d49766120ffecc25378f
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726758"
---
# <a name="auditing-and-reporting-on-jea"></a><span data-ttu-id="f5573-103">Naplózás és a JEA-jelentések</span><span class="sxs-lookup"><span data-stu-id="f5573-103">Auditing and Reporting on JEA</span></span>

<span data-ttu-id="f5573-104">Miután telepítette a JEA, kell rendszeresen naplózása a JEA-konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="f5573-104">After you've deployed JEA, you need to regularly audit the JEA configuration.</span></span> <span data-ttu-id="f5573-105">A naplózás segítségével felmérheti, hogy a megfelelő felhasználók is hozzáférhetnek a JEA-végpont, és a hozzárendelt szerepkörök továbbra is megfelelőek.</span><span class="sxs-lookup"><span data-stu-id="f5573-105">Auditing helps you assess that the correct people have access to the JEA endpoint and their assigned roles are still appropriate.</span></span>

## <a name="find-registered-jea-sessions-on-a-machine"></a><span data-ttu-id="f5573-106">Keresse meg a regisztrált JEA munkamenetek gépen</span><span class="sxs-lookup"><span data-stu-id="f5573-106">Find registered JEA sessions on a machine</span></span>

<span data-ttu-id="f5573-107">Ellenőrizze, hogy mely JEA munkamenetek gépen regisztrált, használja a [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="f5573-107">To check which JEA sessions are registered on a machine, use the [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) cmdlet.</span></span>

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }
```

```Output
Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed,
                CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

<span data-ttu-id="f5573-108">A végpont a hatályos jogosultságok láthatók a **engedély** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="f5573-108">The effective rights for the endpoint are listed in the **Permission** property.</span></span> <span data-ttu-id="f5573-109">Ezek a felhasználók csatlakozni a JEA-végpont áll.</span><span class="sxs-lookup"><span data-stu-id="f5573-109">These users have the right to connect to the JEA endpoint.</span></span> <span data-ttu-id="f5573-110">Azonban a szerepkörök és a parancsok férhet hozzá, határozza meg a **RoleDefinitions** tulajdonságot a [munkamenet konfigurációs fájl](session-configurations.md) használt végpont.</span><span class="sxs-lookup"><span data-stu-id="f5573-110">However, the roles and commands they have access to is determined by the **RoleDefinitions** property in the [session configuration file](session-configurations.md) that was used to register the endpoint.</span></span> <span data-ttu-id="f5573-111">Bontsa ki a **RoleDefinitions** tulajdonság egy regisztrált a JEA-végpont a szerepkör-hozzárendelések kiértékeléséhez.</span><span class="sxs-lookup"><span data-stu-id="f5573-111">Expand the **RoleDefinitions** property to evaluate the role mappings in a registered JEA endpoint.</span></span>

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{
  Name = 'Role Capabilities'
  Expression = { $_.Value.RoleCapabilities }
}
```

## <a name="find-available-role-capabilities-on-the-machine"></a><span data-ttu-id="f5573-112">A gépen elérhető szerepköri funkciók keresése</span><span class="sxs-lookup"><span data-stu-id="f5573-112">Find available role capabilities on the machine</span></span>

<span data-ttu-id="f5573-113">A JEA szerepkör-szolgáltatásait, lekérdezi a `.psrc` tárolt fájlok a **RoleCapabilities** belüli egy PowerShell-modul.</span><span class="sxs-lookup"><span data-stu-id="f5573-113">JEA gets role capabilities from the `.psrc` files stored in the **RoleCapabilities** folder inside a PowerShell module.</span></span> <span data-ttu-id="f5573-114">A következő függvényt egy számítógépen elérhető szerepköri funkciók keresése.</span><span class="sxs-lookup"><span data-stu-id="f5573-114">The following function finds all role capabilities available on a computer.</span></span>

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
    $results | Select-Object @{ Name = 'Name'; Expression = { $_.Name.TrimEnd('.psrc') }}, @{
        Name = 'Path'; Expression = { $_.FullName }
    } | Sort-Object Name
}
```

> [!NOTE]
> <span data-ttu-id="f5573-115">Ez a függvény eredményeinek sorrendje nem feltétlenül a sorrend, amelyben a szerepkörrel képességeket lesz kiválasztva, ha több szerepkörrel képességeket rendelkezik ugyanazzal a névvel.</span><span class="sxs-lookup"><span data-stu-id="f5573-115">The order of results from this function is not necessarily the order in which the role capabilities will be selected if multiple role capabilities share the same name.</span></span>

## <a name="check-effective-rights-for-a-specific-user"></a><span data-ttu-id="f5573-116">Egy adott felhasználó hatékony jogok ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="f5573-116">Check effective rights for a specific user</span></span>

<span data-ttu-id="f5573-117">A [Get-PSSessionCapability](/powershell/module/microsoft.powershell.core/Get-PSSessionCapability) parancsmag a JEA-végpont egy vendégfelhasználói csoporttagságok alapján elérhető összes parancs enumerálása.</span><span class="sxs-lookup"><span data-stu-id="f5573-117">The [Get-PSSessionCapability](/powershell/module/microsoft.powershell.core/Get-PSSessionCapability) cmdlet enumerates all the commands available on a JEA endpoint based on a user's group memberships.</span></span>
<span data-ttu-id="f5573-118">A kimenet a `Get-PSSessionCapability` megegyezik-e a megadott futtató felhasználó `Get-Command -CommandType All` JEA munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="f5573-118">The output of `Get-PSSessionCapability` is identical to that of the specified user running `Get-Command -CommandType All` in a JEA session.</span></span>

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

<span data-ttu-id="f5573-119">Ha a felhasználók számára szeretne jogosultságokat őket további JEA csoportok állandó tagjai nem, ez a parancsmag nem tükrözik az extra engedélyeket.</span><span class="sxs-lookup"><span data-stu-id="f5573-119">If your users aren't permanent members of groups that would grant them additional JEA rights, this cmdlet may not reflect those extra permissions.</span></span> <span data-ttu-id="f5573-120">Ez történik, ha használatával just-in-time rendszerjogosultságú hozzáférés ideiglenesen biztonsági csoporthoz tartozó felhasználók felügyeleti rendszerekkel.</span><span class="sxs-lookup"><span data-stu-id="f5573-120">This happens when using just-in-time privileged access management systems to allow users to temporarily belong to a security group.</span></span> <span data-ttu-id="f5573-121">Gondosan mérlegelje, szerepkörök és funkciók annak érdekében, hogy felhasználók csak a munkájuk sikeres elvégzéséhez szükséges hozzáférési szintet, hogy a felhasználók leképezése.</span><span class="sxs-lookup"><span data-stu-id="f5573-121">Carefully evaluate the mapping of users to roles and capabilities to ensure that users only get the level of access needed to do their jobs successfully.</span></span>

## <a name="powershell-event-logs"></a><span data-ttu-id="f5573-122">PowerShell-eseménynaplók</span><span class="sxs-lookup"><span data-stu-id="f5573-122">PowerShell event logs</span></span>

<span data-ttu-id="f5573-123">Ha engedélyezte a rendszer a bejelentkezés modul vagy a parancsfájl letiltása, láthatja az összes parancs a JEA munkamenet egy felhasználó futtatja a Windows eseménynaplóiban események.</span><span class="sxs-lookup"><span data-stu-id="f5573-123">If you enabled module or script block logging on the system, you can see events in the Windows event logs for each command a user runs in a JEA session.</span></span> <span data-ttu-id="f5573-124">Ezeket az eseményeket, nyissa meg **Microsoft-Windows-PowerShell/műveleti** eseménynaplót, és keresse meg az eseményazonosító események **4104**.</span><span class="sxs-lookup"><span data-stu-id="f5573-124">To find these events, open **Microsoft-Windows-PowerShell/Operational** event log and look for events with event ID **4104**.</span></span>

<span data-ttu-id="f5573-125">Minden eseménynapló-bejegyzést, amelyben a parancs futtatása a munkamenet kapcsolatos információkat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="f5573-125">Each event log entry includes information about the session in which the command was run.</span></span> <span data-ttu-id="f5573-126">A JEA-munkamenetet, az eseményt az alábbiakról tájékozódhat a **ConnectedUser** és a **felhasználó**.</span><span class="sxs-lookup"><span data-stu-id="f5573-126">For JEA sessions, the event includes information about the **ConnectedUser** and the **RunAsUser**.</span></span> <span data-ttu-id="f5573-127">A **ConnectedUser** van az aktuális felhasználó, aki létrehozta a JEA-munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="f5573-127">The **ConnectedUser** is the actual user who created the JEA session.</span></span> <span data-ttu-id="f5573-128">A **felhasználó** JEA a parancs végrehajtásához használt fiók.</span><span class="sxs-lookup"><span data-stu-id="f5573-128">The **RunAsUser** is the account JEA used to execute the command.</span></span>

<span data-ttu-id="f5573-129">Alkalmazás eseménynaplóit által végrehajtott változtatások megjelenítése a **felhasználó**.</span><span class="sxs-lookup"><span data-stu-id="f5573-129">Application event logs show changes being made by the **RunAsUser**.</span></span> <span data-ttu-id="f5573-130">Így modul és a parancsfájl-naplózás engedélyezve szükség egy adott parancs meghívása biztonsági másolatot a nyomkövetés a **ConnectedUser**.</span><span class="sxs-lookup"><span data-stu-id="f5573-130">So having module and script logging enabled is required to trace a specific command invocation back to the **ConnectedUser**.</span></span>

## <a name="application-event-logs"></a><span data-ttu-id="f5573-131">Alkalmazás eseménynaplóit</span><span class="sxs-lookup"><span data-stu-id="f5573-131">Application event logs</span></span>

<span data-ttu-id="f5573-132">Parancsok futtatása a JEA-munkamenetet, amely együttműködik a külső alkalmazások vagy szolgáltatások események naplózása a saját ügyfélesemény-naplókba.</span><span class="sxs-lookup"><span data-stu-id="f5573-132">Commands run in a JEA session that interact with external applications or services may log events to their own event logs.</span></span> <span data-ttu-id="f5573-133">PowerShell-naplók és szövegekben, ellentétben más naplózási mechanizmusok a JEA-munkamenet csatlakoztatott felhasználói nem rögzíti.</span><span class="sxs-lookup"><span data-stu-id="f5573-133">Unlike PowerShell logs and transcripts, other logging mechanisms don't capture the connected user of the JEA session.</span></span> <span data-ttu-id="f5573-134">Ehelyett ezeket az alkalmazásokat csak a virtuális futtató felhasználó naplózása.</span><span class="sxs-lookup"><span data-stu-id="f5573-134">Instead, those applications only log the virtual run-as user.</span></span>
<span data-ttu-id="f5573-135">Határozza meg, akik a parancsot futtatta, egyeztetniük kell egy [munkamenet átiratok](#session-transcripts) vagy vesse össze a PowerShell-eseménynaplók az idő és a felhasználó látható az alkalmazások eseménynaplójában.</span><span class="sxs-lookup"><span data-stu-id="f5573-135">To determine who ran the command, you need to consult a [session transcript](#session-transcripts) or correlate PowerShell event logs with the time and user shown in the application event log.</span></span>

<span data-ttu-id="f5573-136">A WinRM-naplót is segíthet futtató felhasználóknak a kapcsolódó felhasználó az alkalmazás eseménynaplója összekapcsolását.</span><span class="sxs-lookup"><span data-stu-id="f5573-136">The WinRM log can also help you correlate run-as users to the connecting user in an application event log.</span></span> <span data-ttu-id="f5573-137">Eseményazonosító **193** a a **Microsoft-Windows-Windows távoli felügyeleti/műveleti** naplófájl rögzíti a biztonsági azonosítóval (SID) és a kapcsolódó felhasználó és a futtató fiók nevét felhasználóként minden új JEA munkamenet.</span><span class="sxs-lookup"><span data-stu-id="f5573-137">Event ID **193** in the **Microsoft-Windows-Windows Remote Management/Operational** log records the security identifier (SID) and account name for both the connecting user and run as user for every new JEA session.</span></span>

## <a name="session-transcripts"></a><span data-ttu-id="f5573-138">Munkamenet szövegekben</span><span class="sxs-lookup"><span data-stu-id="f5573-138">Session transcripts</span></span>

<span data-ttu-id="f5573-139">Ha konfigurálta a JEA egy szöveges létrehozása minden felhasználói munkamenetet, minden felhasználói műveletek szöveges másolatának a megadott mappában vannak tárolva.</span><span class="sxs-lookup"><span data-stu-id="f5573-139">If you configured JEA to create a transcript for each user session, a text copy of every user's actions are stored in the specified folder.</span></span>

<span data-ttu-id="f5573-140">Az alábbi parancsot (rendszergazdaként) megkeresi az összes szöveges könyvtár.</span><span class="sxs-lookup"><span data-stu-id="f5573-140">The following command (as an administrator) finds all transcript directories.</span></span>

```powershell
Get-PSSessionConfiguration |
  Where-Object { $_.TranscriptDirectory -ne $null } |
    Format-Table Name, TranscriptDirectory
```

<span data-ttu-id="f5573-141">Minden szöveges kapcsolatos információkat a munkamenet kezdete, mely a munkamenetet, és mely JEA identitás hozzá volt rendelve, a hozzájuk kapcsolódó felhasználó kezdődik.</span><span class="sxs-lookup"><span data-stu-id="f5573-141">Each transcript starts with information about the time the session started, which user connected to the session, and which JEA identity was assigned to them.</span></span>

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

<span data-ttu-id="f5573-142">Az átirat törzse tartalmazza minden egyes parancsot, a felhasználó meghívása kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="f5573-142">The body of the transcript contains information about each command the user invoked.</span></span> <span data-ttu-id="f5573-143">A pontos szintaxist a használt parancs a parancsokat a PowerShell távelérése átalakításának módja miatt nem érhető el a JEA-munkamenetekben.</span><span class="sxs-lookup"><span data-stu-id="f5573-143">The exact syntax of the command used is unavailable in JEA sessions because of the way commands are transformed for PowerShell remoting.</span></span> <span data-ttu-id="f5573-144">Azonban továbbra is meghatározhatja a hatékony parancsot, amely végre lett hajtva.</span><span class="sxs-lookup"><span data-stu-id="f5573-144">However, you can still determine the effective command that was executed.</span></span> <span data-ttu-id="f5573-145">Alul látható egy példa a szövegben kódrészlet futtató felhasználó `Get-Service Dns` JEA munkamenetben:</span><span class="sxs-lookup"><span data-stu-id="f5573-145">Below is an example transcript snippet from a user running `Get-Service Dns` in a JEA session:</span></span>

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

<span data-ttu-id="f5573-146">A **CommandInvocation** sor írt minden egyes parancsnál egy felhasználó futtatja.</span><span class="sxs-lookup"><span data-stu-id="f5573-146">A **CommandInvocation** line is written for each command a user runs.</span></span> <span data-ttu-id="f5573-147">**ParameterBindings** minden paraméter és a parancs a megadott érték.</span><span class="sxs-lookup"><span data-stu-id="f5573-147">**ParameterBindings** record each parameter and value supplied with the command.</span></span> <span data-ttu-id="f5573-148">Az előző példában láthatja, hogy a paraméter **neve** lett megadva a értékkel **Dns** számára a `Get-Service` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="f5573-148">In the previous example, you can see that the parameter **Name** was supplied the with value **Dns** for the `Get-Service` cmdlet.</span></span>

<span data-ttu-id="f5573-149">A kimenet minden egyes parancsot is eseményindítók egy **CommandInvocation**, általában az `Out-Default`.</span><span class="sxs-lookup"><span data-stu-id="f5573-149">The output of each command also triggers a **CommandInvocation**, usually to `Out-Default`.</span></span> <span data-ttu-id="f5573-150">A **InputObject** , `Out-Default` a PowerShell-objektumot a parancs által visszaadott.</span><span class="sxs-lookup"><span data-stu-id="f5573-150">The **InputObject** of `Out-Default` is the PowerShell object returned from the command.</span></span> <span data-ttu-id="f5573-151">Nyomtatási objektum részleteit az alábbi szorosan mimicking, mi a felhasználó lenne látott néhány sort.</span><span class="sxs-lookup"><span data-stu-id="f5573-151">The details of that object are printed a few lines below, closely mimicking what the user would have seen.</span></span>

## <a name="see-also"></a><span data-ttu-id="f5573-152">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f5573-152">See also</span></span>

[<span data-ttu-id="f5573-153">*PowerShell a kék csapat ♥* biztonsági blogbejegyzés</span><span class="sxs-lookup"><span data-stu-id="f5573-153">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)
