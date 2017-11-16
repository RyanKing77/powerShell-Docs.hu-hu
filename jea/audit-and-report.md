---
ms.date: 2017-06-12
author: rpsqrd
ms.topic: conceptual
keywords: "jea, a powershell, a biztonsági"
title: "Naplózási és jelentéskészítési összetevője JEA"
ms.openlocfilehash: 60bc7a4213c75735628207bb21078bf90f7b1ca3
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="auditing-and-reporting-on-jea"></a><span data-ttu-id="33fcc-103">Naplózási és jelentéskészítési összetevője JEA</span><span class="sxs-lookup"><span data-stu-id="33fcc-103">Auditing and Reporting on JEA</span></span>

> <span data-ttu-id="33fcc-104">A következőkre vonatkozik: a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="33fcc-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="33fcc-105">JEA telepítése után célszerű rendszeresen rendszervizsgálati JEA konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="33fcc-105">After you've deployed JEA, you will want to regularly audit the JEA configuration.</span></span>
<span data-ttu-id="33fcc-106">Ez segítséget nyújt a megfelelő személyek hozzáférhetnek a JEA végpont, és a hozzárendelt szerepkörök továbbra is megfelelőek.</span><span class="sxs-lookup"><span data-stu-id="33fcc-106">This will help you assess if the correct people have access to the JEA endpoint and if their assigned roles are still appropriate.</span></span>

<span data-ttu-id="33fcc-107">Ez a témakör ismerteti a különböző módszereket a JEA végpont naplózhatók.</span><span class="sxs-lookup"><span data-stu-id="33fcc-107">This topic describes the various ways you can audit a JEA endpoint.</span></span>

## <a name="find-registered-jea-sessions-on-a-machine"></a><span data-ttu-id="33fcc-108">Regisztrált JEA munkamenetek található a gépen</span><span class="sxs-lookup"><span data-stu-id="33fcc-108">Find registered JEA sessions on a machine</span></span>

<span data-ttu-id="33fcc-109">Mely JEA munkamenetek regisztrált gépen ellenőrzéséhez használja a [Get-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="33fcc-109">To check which JEA sessions are registered on a machine, use the [Get-PSSessionConfiguration](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) cmdlet.</span></span>

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
PS C:\> Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }


Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed, CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

<span data-ttu-id="33fcc-110">A végpont a hatályos jogosultságok láthatók a "Engedély" tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="33fcc-110">The effective rights for the endpoint are listed in the "Permission" property.</span></span>
<span data-ttu-id="33fcc-111">Ezek a felhasználók jogosultak a JEA-végponthoz, de mely szerepkörök (és bővítmény parancsok által) kapcsolódni hozzáférhetnek a "RoleDefinitions" mező határozza meg a [munkamenet konfigurációs fájl](session-configurations.md) használt regisztrálja a a végpont.</span><span class="sxs-lookup"><span data-stu-id="33fcc-111">These users have the right to connect to the JEA endpoint, but which roles (and, by extension, commands) they have access to is determined by the "RoleDefinitions" field in the [session configuration file](session-configurations.md) that was used to register the endpoint.</span></span>

<span data-ttu-id="33fcc-112">A szerepkör-hozzárendelések a regisztrált JEA-végpont kiértékelheti az adatokat a "RoleDefinitions" kibontásával.</span><span class="sxs-lookup"><span data-stu-id="33fcc-112">You can evaluate the role mappings in a registered JEA endpoint by expanding the data in the "RoleDefinitions" property.</span></span>

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{ Name = 'Role Capabilities'; Expression = { $_.Value.RoleCapabilities } }
```

## <a name="find-available-role-capabilities-on-the-machine"></a><span data-ttu-id="33fcc-113">A számítógépen elérhető szerepkör képességek keresése</span><span class="sxs-lookup"><span data-stu-id="33fcc-113">Find available role capabilities on the machine</span></span>

<span data-ttu-id="33fcc-114">Szerepkör szolgáltatásfájlokban csak által használandó JEA egy érvényes PowerShell-modul belül "RoleCapabilities" mappában vannak tárolva.</span><span class="sxs-lookup"><span data-stu-id="33fcc-114">Role capability files will only be used by JEA if they are stored in a "RoleCapabilities" folder inside a valid PowerShell module.</span></span>
<span data-ttu-id="33fcc-115">Az összes szerepkör lehetőségeinek számítógépen elérhető listájához keresve található.</span><span class="sxs-lookup"><span data-stu-id="33fcc-115">You can find all role capabilities available on a computer by searching the list of available modules.</span></span>

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
> <span data-ttu-id="33fcc-116">Ez a funkció eredményeinek sorrendje nem feltétlenül a sorrendben, amelyben a szerepkör képességek fog jelölhető ki, ha több szerepkör képességek megosztás neve.</span><span class="sxs-lookup"><span data-stu-id="33fcc-116">The order of results from this function is not necessarily the order in which the role capabilities will be selected if multiple role capabilities share the same name.</span></span>

## <a name="check-effective-rights-for-a-specific-user"></a><span data-ttu-id="33fcc-117">Jelölje be a felhasználó hatékony jogok</span><span class="sxs-lookup"><span data-stu-id="33fcc-117">Check effective rights for a specific user</span></span>

<span data-ttu-id="33fcc-118">A JEA végpont beállítása után érdemes lehet, mely parancsok elérhető egy adott felhasználónak JEA munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="33fcc-118">Once you have set up a JEA endpoint, you may want to check which commands are available to a specific user in a JEA session.</span></span>
<span data-ttu-id="33fcc-119">Használhat [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) operációs rendszer összes felhasználó alkalmazandó parancs, ha azok az aktuális csoporttagságok JEA munkamenet indításához.</span><span class="sxs-lookup"><span data-stu-id="33fcc-119">You can use [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) to enumerate all of the commands applicable to a user if they were to start a JEA session with their current group memberships.</span></span>
<span data-ttu-id="33fcc-120">A kimeneti `Get-PSSessionCapability` megegyezik-e a megadott futtató felhasználó `Get-Command -CommandType All` JEA munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="33fcc-120">The output of `Get-PSSessionCapability` is identical to that of the specified user running `Get-Command -CommandType All` in a JEA session.</span></span>

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

<span data-ttu-id="33fcc-121">Ha a felhasználók nem lenne jogot adni őket további JEA csoportokat állandó tagjai, ez a parancsmag nem tükrözik az extra engedélyeket.</span><span class="sxs-lookup"><span data-stu-id="33fcc-121">If your users are not permanent members of groups which would grant them additional JEA rights, this cmdlet may not reflect those extra permissions.</span></span>
<span data-ttu-id="33fcc-122">Általában ez a helyzet, a felhasználók ideiglenesen egy biztonsági csoporthoz tartozó just-in-time privileged access management rendszerek használata esetén.</span><span class="sxs-lookup"><span data-stu-id="33fcc-122">This is typically the case when using just-in-time privileged access management systems to allow users to temporarily belong to a security group.</span></span>
<span data-ttu-id="33fcc-123">Mindig gondosan értékelje ki a felhasználói szerepkör a leképezési és a felhasználók csak kap a parancsok a munkájuk sikeres elvégzéséhez szükséges lehető legkisebb mennyiségű való hozzáférés biztosításához szerepkörönként tartalmát.</span><span class="sxs-lookup"><span data-stu-id="33fcc-123">Always carefully evaluate the mapping of users to roles and the contents of each role to ensure users are only getting access to the least amount of commands needed to do their jobs successfully.</span></span>

## <a name="powershell-event-logs"></a><span data-ttu-id="33fcc-124">PowerShell-eseménynaplók</span><span class="sxs-lookup"><span data-stu-id="33fcc-124">PowerShell event logs</span></span>

<span data-ttu-id="33fcc-125">Ha engedélyezte a rendszer a bejelentkezés modul és/vagy parancsfájl-blokk, lesz, a Windows eseménynaplóiban keresse meg az egyes a felhasználó a JEA-munkamenetekben futtatott parancsok események található.</span><span class="sxs-lookup"><span data-stu-id="33fcc-125">If you enabled module and/or script block logging on the system, you will be able to find events in the Windows event logs for each command a user ran in their JEA sessions.</span></span>
<span data-ttu-id="33fcc-126">Ezek az események kereséséhez nyissa meg a Windows eseménynaplót, keresse meg a **Microsoft-Windows-PowerShell/műveleti** Eseménynapló, és keresse meg az Eseménynapló azonosítójú események **4104**.</span><span class="sxs-lookup"><span data-stu-id="33fcc-126">To find these events, open the Windows Event Viewer, navigate to the **Microsoft-Windows-PowerShell/Operational** event log, and look for events with event ID **4104**.</span></span>

<span data-ttu-id="33fcc-127">Minden egyes eseménynapló-bejegyzés, amelyben a parancs futtatása a munkamenet adatait is tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="33fcc-127">Each event log entry will include information about the session in which the command was run.</span></span>
<span data-ttu-id="33fcc-128">A JEA-munkamenetekben, ide tartoznak a fontos információk a **ConnectedUser**, ez az a tényleges felhasználó, aki létrehozta a JEA munkamenet, valamint a **felhasználó** amely azonosítja az JEA használandó fiókot hajtsa végre a parancsot.</span><span class="sxs-lookup"><span data-stu-id="33fcc-128">For JEA sessions, this includes important information about the **ConnectedUser**, which is the actual user who created the JEA session, as well as the **RunAsUser** which identifies the account JEA used to execute the command.</span></span>
<span data-ttu-id="33fcc-129">Alkalmazás eseménynaplóiban megjeleníti a felhasználó által végrehajtott módosítások, amelyek ki, vagy modul, a parancsfájl-naplózás engedélyezve különösen fontos tudja nyomon követni egy adott parancs meghívása vissza egy felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="33fcc-129">Application event logs will show changes being made by the RunAsUser, so having transcripts or module/script logging enabled is crucial to be able to trace a specific command invocation back to a user.</span></span>

## <a name="application-event-logs"></a><span data-ttu-id="33fcc-130">Alkalmazás eseménynaplóiban</span><span class="sxs-lookup"><span data-stu-id="33fcc-130">Application event logs</span></span>

<span data-ttu-id="33fcc-131">A parancs futtatásakor, hogy a külső alkalmazás vagy szolgáltatás kommunikációja JEA munkamenetben ezeket az alkalmazásokat a saját eseménynaplók előfordulhat, hogy jelentkezzen események.</span><span class="sxs-lookup"><span data-stu-id="33fcc-131">When you run a command in a JEA session that interacts with an external application or service, those applications may log events to their own event logs.</span></span>
<span data-ttu-id="33fcc-132">Ellentétben a PowerShell naplókat, valamint ki más naplózási mechanizmusok nem rögzíti a csatlakoztatott felhasználói a JEA-munkamenet, és inkább csak naplózza a virtuális futtató felhasználó vagy a csoportosan felügyelt szolgáltatásfiók.</span><span class="sxs-lookup"><span data-stu-id="33fcc-132">Unlike PowerShell logs and transcripts, other logging mechanisms will not capture the connected user of the JEA session, and will instead only log the virtual run-as user or group managed service account.</span></span>
<span data-ttu-id="33fcc-133">Annak megállapítására, hogy ki futtatta a parancsot, szüksége lesz a további részleteket a [munkamenet Beszélgetés szövegének](#session-transcripts) vagy PowerShell-eseménynaplók okozták az az idő és a felhasználó az alkalmazások eseménynaplójában.</span><span class="sxs-lookup"><span data-stu-id="33fcc-133">In order to determine who ran the command, you will need to consult a [session transcript](#session-transcripts) or correlate PowerShell event logs with the time and user shown in the application event log.</span></span>

<span data-ttu-id="33fcc-134">A Rendszerfelügyeleti webszolgáltatások napló segítségével összefüggéseket futtassa az alkalmazások eseménynaplójában keresse meg a felhasználók a csatlakozó felhasználó.</span><span class="sxs-lookup"><span data-stu-id="33fcc-134">The WinRM log can also help you correlate run as users in an application event log with the connecting user.</span></span>
<span data-ttu-id="33fcc-135">Eseményazonosító **193** a a **Microsoft-Windows-Windows távoli felügyeleti/műveleti** naplórekordok a biztonsági azonosító (SID) és a fiók a csatlakozó felhasználó neve és futtató felhasználó mindig a JEA munkamenet jön létre.</span><span class="sxs-lookup"><span data-stu-id="33fcc-135">Event ID **193** in the **Microsoft-Windows-Windows Remote Management/Operational** log records the security identifier (SID) and account name for both the connecting user and run as user every time a JEA session is created.</span></span>

## <a name="session-transcripts"></a><span data-ttu-id="33fcc-136">Munkamenet ki</span><span class="sxs-lookup"><span data-stu-id="33fcc-136">Session transcripts</span></span>

<span data-ttu-id="33fcc-137">Ha JEA egy Beszélgetés szövegének létrehozása minden felhasználói munkamenetet konfigurálta, minden felhasználói műveletek szöveges másolatának tárolódnak a megadott mappát.</span><span class="sxs-lookup"><span data-stu-id="33fcc-137">If you configured JEA to create a transcript for each user session, a text copy of every user's actions will be stored in the specified folder.</span></span>

<span data-ttu-id="33fcc-138">Összes beszélgetés szövegének könyvtár megkeresése, a következő parancsot futtassa rendszergazdaként a számítógépen JEA konfigurálva:</span><span class="sxs-lookup"><span data-stu-id="33fcc-138">To find all transcript directories, run the following command as an administrator on the computer configured with JEA:</span></span>

```powershell
Get-PSSessionConfiguration | Where-Object { $_.TranscriptDirectory -ne $null } | Format-Table Name, TranscriptDirectory
```

<span data-ttu-id="33fcc-139">Minden egyes Beszélgetés szövegének kezdődik-e a indításakor a munkamenet, mely felhasználó csatlakozik, a munkamenet, mely JEA identitás lett rendelve kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="33fcc-139">Each transcript starts with information about the time the session started, which user connected to the session, and which JEA identity was assigned to them.</span></span>

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

<span data-ttu-id="33fcc-140">A Beszélgetés szövegének törzsében minden parancs, a felhasználó meghívott kapcsolatos naplózott információk.</span><span class="sxs-lookup"><span data-stu-id="33fcc-140">In the body of the transcript, information is logged about each command the user invoked.</span></span>
<span data-ttu-id="33fcc-141">Pontos szintaxisa az a felhasználó futtatja a parancsot nem érhető el a parancsokat a PowerShell távelérése átalakítaná módjának JEA-munkamenetekben, azonban továbbra is meghatározhatja, hogy végre lett hajtva a hatékony parancs.</span><span class="sxs-lookup"><span data-stu-id="33fcc-141">The exact syntax of the command the user ran is unavailable in JEA sessions due to the way commands are transformed for PowerShell remoting, however you can still determine the effective command that was executed.</span></span>
<span data-ttu-id="33fcc-142">Egy példa Beszélgetés szövegének részlet futtató felhasználók az alábbiakban található `Get-Service Dns` JEA-munkamenetben:</span><span class="sxs-lookup"><span data-stu-id="33fcc-142">Below is an example transcript snippet from a user running `Get-Service Dns` in a JEA session:</span></span>

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

<span data-ttu-id="33fcc-143">Az egyes parancsok egy felhasználó futtatja a "CommandInvocation" sor kerülnek, a parancsmag leíró, vagy a meghívott felhasználó működik.</span><span class="sxs-lookup"><span data-stu-id="33fcc-143">For each command a user runs, a "CommandInvocation" line will be written, describing the cmdlet or function the user invoked.</span></span>
<span data-ttu-id="33fcc-144">ParameterBindings hajtsa végre az egyes CommandInvocation, amely közli, minden paraméter és érték, amely a parancs lett megadva.</span><span class="sxs-lookup"><span data-stu-id="33fcc-144">ParameterBindings follow each CommandInvocation to tell you about each parameter and value that was supplied with the command.</span></span>
<span data-ttu-id="33fcc-145">A fenti példában láthatja, hogy a paraméter "Name" lett megadva az érték "Dns" a "Get-szolgáltatás" parancsmaghoz.</span><span class="sxs-lookup"><span data-stu-id="33fcc-145">In the above example, you can see that the parameter "Name" was supplied the value "Dns" for the "Get-Service" cmdlet.</span></span>

<span data-ttu-id="33fcc-146">Minden parancs is elindítja egy CommandInvocation általában az alapértelmezett kimenő irányú.</span><span class="sxs-lookup"><span data-stu-id="33fcc-146">The output of each command will also trigger a CommandInvocation, usually to Out-Default.</span></span> <span data-ttu-id="33fcc-147">A Out-Default InputObject egy, a parancs által visszaadott PowerShell-objektum.</span><span class="sxs-lookup"><span data-stu-id="33fcc-147">The InputObject of Out-Default is the PowerShell object returned from the command.</span></span>
<span data-ttu-id="33fcc-148">Lista tartalmazza az objektumokat, amelyek részleteit az alábbi szorosan mimicking Mi a felhasználó akkor amint láthatta néhány sor.</span><span class="sxs-lookup"><span data-stu-id="33fcc-148">The details of that object are printed a few lines below, closely mimicking what the user would have seen.</span></span>

## <a name="see-also"></a><span data-ttu-id="33fcc-149">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="33fcc-149">See also</span></span>

- [<span data-ttu-id="33fcc-150">A JEA-munkamenetben felhasználói műveletek naplózása</span><span class="sxs-lookup"><span data-stu-id="33fcc-150">Audit user actions in a JEA session</span></span>](audit-and-report.md)
- [<span data-ttu-id="33fcc-151">*PowerShell ♥ a kék Team* a biztonsági által írt blogbejegyzés</span><span class="sxs-lookup"><span data-stu-id="33fcc-151">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

