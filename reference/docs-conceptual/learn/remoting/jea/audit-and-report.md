---
ms.date: 07/10/2019
keywords: jea, PowerShell, biztonság
title: Naplózás és jelentéskészítés a JEA
ms.openlocfilehash: 2afefe83acecc1fc3643d49766120ffecc25378f
ms.sourcegitcommit: e894ed833cef57967cdaf002f8c883f66864e836
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017922"
---
# <a name="auditing-and-reporting-on-jea"></a><span data-ttu-id="ad57a-103">Naplózás és jelentéskészítés a JEA</span><span class="sxs-lookup"><span data-stu-id="ad57a-103">Auditing and Reporting on JEA</span></span>

<span data-ttu-id="ad57a-104">A JEA üzembe helyezése után rendszeresen ellenőriznie kell a JEA konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="ad57a-104">After you've deployed JEA, you need to regularly audit the JEA configuration.</span></span> <span data-ttu-id="ad57a-105">A naplózás segít felmérni, hogy a megfelelő személyek férhetnek hozzá a JEA-végponthoz, és a hozzájuk rendelt szerepkörök továbbra is megfelelőek-e.</span><span class="sxs-lookup"><span data-stu-id="ad57a-105">Auditing helps you assess that the correct people have access to the JEA endpoint and their assigned roles are still appropriate.</span></span>

## <a name="find-registered-jea-sessions-on-a-machine"></a><span data-ttu-id="ad57a-106">Regisztrált JEA-munkamenetek keresése a gépen</span><span class="sxs-lookup"><span data-stu-id="ad57a-106">Find registered JEA sessions on a machine</span></span>

<span data-ttu-id="ad57a-107">A [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) parancsmaggal ellenőrizhető, hogy mely JEA-munkamenetek vannak regisztrálva a gépen.</span><span class="sxs-lookup"><span data-stu-id="ad57a-107">To check which JEA sessions are registered on a machine, use the [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) cmdlet.</span></span>

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

<span data-ttu-id="ad57a-108">A végpontra érvényes jogosultságok az **engedély** tulajdonságban szerepelnek.</span><span class="sxs-lookup"><span data-stu-id="ad57a-108">The effective rights for the endpoint are listed in the **Permission** property.</span></span> <span data-ttu-id="ad57a-109">Ezek a felhasználók jogosultak a JEA-végponthoz való kapcsolódásra.</span><span class="sxs-lookup"><span data-stu-id="ad57a-109">These users have the right to connect to the JEA endpoint.</span></span> <span data-ttu-id="ad57a-110">Azonban az azokhoz a szerepkörökhöz és parancsokhoz, amelyekhez hozzáférnek, a végpont regisztrálásához használt [munkamenet-konfigurációs fájlban](session-configurations.md) található **RoleDefinitions** tulajdonság határozza meg.</span><span class="sxs-lookup"><span data-stu-id="ad57a-110">However, the roles and commands they have access to is determined by the **RoleDefinitions** property in the [session configuration file](session-configurations.md) that was used to register the endpoint.</span></span> <span data-ttu-id="ad57a-111">Bontsa ki a **RoleDefinitions** tulajdonságot a szerepkör-hozzárendelések kiértékeléséhez egy regisztrált JEA-végponton.</span><span class="sxs-lookup"><span data-stu-id="ad57a-111">Expand the **RoleDefinitions** property to evaluate the role mappings in a registered JEA endpoint.</span></span>

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{
  Name = 'Role Capabilities'
  Expression = { $_.Value.RoleCapabilities }
}
```

## <a name="find-available-role-capabilities-on-the-machine"></a><span data-ttu-id="ad57a-112">Elérhető szerepkör-képességek keresése a gépen</span><span class="sxs-lookup"><span data-stu-id="ad57a-112">Find available role capabilities on the machine</span></span>

<span data-ttu-id="ad57a-113">A JEA beolvassa `.psrc` a szerepkör-képességeket a **RoleCapabilities** mappában tárolt fájlokból egy PowerShell-modulon belül.</span><span class="sxs-lookup"><span data-stu-id="ad57a-113">JEA gets role capabilities from the `.psrc` files stored in the **RoleCapabilities** folder inside a PowerShell module.</span></span> <span data-ttu-id="ad57a-114">A következő függvény megkeresi a számítógépen elérhető összes szerepkör-funkciót.</span><span class="sxs-lookup"><span data-stu-id="ad57a-114">The following function finds all role capabilities available on a computer.</span></span>

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
> <span data-ttu-id="ad57a-115">A függvény eredményeinek sorrendje nem feltétlenül jelenti azt a sorrendet, amelyben a szerepkör-képességek ki lesznek választva, ha több szerepkör-képesség is ugyanazzal a névvel van megosztva.</span><span class="sxs-lookup"><span data-stu-id="ad57a-115">The order of results from this function is not necessarily the order in which the role capabilities will be selected if multiple role capabilities share the same name.</span></span>

## <a name="check-effective-rights-for-a-specific-user"></a><span data-ttu-id="ad57a-116">Egy adott felhasználóra érvényes jogosultságok keresése</span><span class="sxs-lookup"><span data-stu-id="ad57a-116">Check effective rights for a specific user</span></span>

<span data-ttu-id="ad57a-117">A [Get-PSSessionCapability](/powershell/module/microsoft.powershell.core/Get-PSSessionCapability) PARANCSMAG egy JEA-végponton elérhető összes parancsot enumerálja egy felhasználó csoporttagságok alapján.</span><span class="sxs-lookup"><span data-stu-id="ad57a-117">The [Get-PSSessionCapability](/powershell/module/microsoft.powershell.core/Get-PSSessionCapability) cmdlet enumerates all the commands available on a JEA endpoint based on a user's group memberships.</span></span>
<span data-ttu-id="ad57a-118">A kimenete `Get-PSSessionCapability` megegyezik a JEA-munkamenetben futó `Get-Command -CommandType All` megadott felhasználó nevével.</span><span class="sxs-lookup"><span data-stu-id="ad57a-118">The output of `Get-PSSessionCapability` is identical to that of the specified user running `Get-Command -CommandType All` in a JEA session.</span></span>

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

<span data-ttu-id="ad57a-119">Ha a felhasználók nem rendelkeznek a csoportok olyan állandó tagjaival, amelyek további JEA jogokat biztosítanak, akkor ez a parancsmag nem tükrözi ezeket az extra engedélyeket.</span><span class="sxs-lookup"><span data-stu-id="ad57a-119">If your users aren't permanent members of groups that would grant them additional JEA rights, this cmdlet may not reflect those extra permissions.</span></span> <span data-ttu-id="ad57a-120">Ez akkor fordul elő, ha az igény szerinti privilegizált hozzáférés-kezelési rendszerek használata lehetővé teszi, hogy a felhasználók átmenetileg egy biztonsági csoporthoz tartozzanak.</span><span class="sxs-lookup"><span data-stu-id="ad57a-120">This happens when using just-in-time privileged access management systems to allow users to temporarily belong to a security group.</span></span> <span data-ttu-id="ad57a-121">Alaposan értékelje ki a felhasználók szerepkörökhöz és képességekhez való hozzárendelését annak biztosításához, hogy a felhasználók csak a feladatok sikeres elvégzéséhez szükséges hozzáférési szintet kapják meg.</span><span class="sxs-lookup"><span data-stu-id="ad57a-121">Carefully evaluate the mapping of users to roles and capabilities to ensure that users only get the level of access needed to do their jobs successfully.</span></span>

## <a name="powershell-event-logs"></a><span data-ttu-id="ad57a-122">PowerShell-eseménynaplók</span><span class="sxs-lookup"><span data-stu-id="ad57a-122">PowerShell event logs</span></span>

<span data-ttu-id="ad57a-123">Ha engedélyezte a modul-vagy parancsfájl-blokkoló naplózását a rendszeren, a Windows-eseménynaplókban láthatja az eseményeket, amelyeket a felhasználók egy JEA-munkamenetben futtatnak.</span><span class="sxs-lookup"><span data-stu-id="ad57a-123">If you enabled module or script block logging on the system, you can see events in the Windows event logs for each command a user runs in a JEA session.</span></span> <span data-ttu-id="ad57a-124">Ezeknek az eseményeknek a megkereséséhez nyissa meg a **Microsoft-Windows-PowerShell/operatív** eseménynaplót, és keresse meg az eseményeket a **4104**-es azonosítójú eseménnyel.</span><span class="sxs-lookup"><span data-stu-id="ad57a-124">To find these events, open **Microsoft-Windows-PowerShell/Operational** event log and look for events with event ID **4104**.</span></span>

<span data-ttu-id="ad57a-125">Minden eseménynapló-bejegyzés tartalmaz információt arról a munkamenetről, amelyben a parancs futott.</span><span class="sxs-lookup"><span data-stu-id="ad57a-125">Each event log entry includes information about the session in which the command was run.</span></span> <span data-ttu-id="ad57a-126">A JEA-munkamenetek esetében az esemény a **ConnectedUser** és a **RunAsUser**kapcsolatos információkat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="ad57a-126">For JEA sessions, the event includes information about the **ConnectedUser** and the **RunAsUser**.</span></span> <span data-ttu-id="ad57a-127">A **ConnectedUser** az a tényleges felhasználó, aki létrehozta a JEA-munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="ad57a-127">The **ConnectedUser** is the actual user who created the JEA session.</span></span> <span data-ttu-id="ad57a-128">A **RunAsUser** a parancs végrehajtásához használt JEA-fiók.</span><span class="sxs-lookup"><span data-stu-id="ad57a-128">The **RunAsUser** is the account JEA used to execute the command.</span></span>

<span data-ttu-id="ad57a-129">Az alkalmazás eseménynaplói megjelenítik a **RunAsUser**által végzett módosításokat.</span><span class="sxs-lookup"><span data-stu-id="ad57a-129">Application event logs show changes being made by the **RunAsUser**.</span></span> <span data-ttu-id="ad57a-130">Így a modul és a parancsfájlok naplózása engedélyezve van ahhoz, hogy egy adott parancs visszahívása visszakerüljön a **ConnectedUser**.</span><span class="sxs-lookup"><span data-stu-id="ad57a-130">So having module and script logging enabled is required to trace a specific command invocation back to the **ConnectedUser**.</span></span>

## <a name="application-event-logs"></a><span data-ttu-id="ad57a-131">Alkalmazás-eseménynaplók</span><span class="sxs-lookup"><span data-stu-id="ad57a-131">Application event logs</span></span>

<span data-ttu-id="ad57a-132">A külső alkalmazásokkal vagy szolgáltatásokkal folytatott JEA-munkamenetekben futtatott parancsok a saját eseménynaplóba is naplózhatók az eseményeket.</span><span class="sxs-lookup"><span data-stu-id="ad57a-132">Commands run in a JEA session that interact with external applications or services may log events to their own event logs.</span></span> <span data-ttu-id="ad57a-133">A PowerShell-naplók és-átiratok eltérően más naplózási mechanizmusok nem rögzítik a JEA-munkamenet csatlakoztatott felhasználóját.</span><span class="sxs-lookup"><span data-stu-id="ad57a-133">Unlike PowerShell logs and transcripts, other logging mechanisms don't capture the connected user of the JEA session.</span></span> <span data-ttu-id="ad57a-134">Ehelyett ezek az alkalmazások csak a virtuális futtató felhasználót naplózzák.</span><span class="sxs-lookup"><span data-stu-id="ad57a-134">Instead, those applications only log the virtual run-as user.</span></span>
<span data-ttu-id="ad57a-135">Ha meg szeretné állapítani, hogy ki futtatta a parancsot, akkor meg kell tekintenie egy [munkamenet](#session-transcripts) -átírást, vagy korrelálnia kell a PowerShell-eseménynaplókat az alkalmazás eseménynaplójában látható idővel és felhasználóval.</span><span class="sxs-lookup"><span data-stu-id="ad57a-135">To determine who ran the command, you need to consult a [session transcript](#session-transcripts) or correlate PowerShell event logs with the time and user shown in the application event log.</span></span>

<span data-ttu-id="ad57a-136">A Rendszerfelügyeleti webszolgáltatások naplója segítséget nyújthat a futtató felhasználóknak az alkalmazás-eseménynaplóban való összekapcsolásához is.</span><span class="sxs-lookup"><span data-stu-id="ad57a-136">The WinRM log can also help you correlate run-as users to the connecting user in an application event log.</span></span> <span data-ttu-id="ad57a-137">**193** -es azonosítójú esemény a **Microsoft-Windows rendszerben –** a Rendszerfelügyeleti webszolgáltatások/operatív napló rögzíti a biztonsági azonosító (SID) és a fiók nevét mind a kapcsolódó felhasználó, mind pedig a futtató felhasználó számára minden új JEA-munkamenethez.</span><span class="sxs-lookup"><span data-stu-id="ad57a-137">Event ID **193** in the **Microsoft-Windows-Windows Remote Management/Operational** log records the security identifier (SID) and account name for both the connecting user and run as user for every new JEA session.</span></span>

## <a name="session-transcripts"></a><span data-ttu-id="ad57a-138">Munkamenet-átiratok</span><span class="sxs-lookup"><span data-stu-id="ad57a-138">Session transcripts</span></span>

<span data-ttu-id="ad57a-139">Ha úgy konfigurálta a JEA, hogy az egyes felhasználói munkamenetek számára hozzon létre egy átiratot, a rendszer az összes felhasználó műveletének szöveges másolatát a megadott mappában tárolja.</span><span class="sxs-lookup"><span data-stu-id="ad57a-139">If you configured JEA to create a transcript for each user session, a text copy of every user's actions are stored in the specified folder.</span></span>

<span data-ttu-id="ad57a-140">A következő parancs (rendszergazdaként) megkeresi az összes átirat könyvtárat.</span><span class="sxs-lookup"><span data-stu-id="ad57a-140">The following command (as an administrator) finds all transcript directories.</span></span>

```powershell
Get-PSSessionConfiguration |
  Where-Object { $_.TranscriptDirectory -ne $null } |
    Format-Table Name, TranscriptDirectory
```

<span data-ttu-id="ad57a-141">Az egyes átiratok a munkamenet elindításának idejével, a munkamenethez kapcsolódó felhasználóval és a hozzájuk rendelt JEA-identitással kapcsolatos információkkal kezdődnek.</span><span class="sxs-lookup"><span data-stu-id="ad57a-141">Each transcript starts with information about the time the session started, which user connected to the session, and which JEA identity was assigned to them.</span></span>

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

<span data-ttu-id="ad57a-142">Az átirat törzse információt tartalmaz a felhasználó által meghívott parancsokról.</span><span class="sxs-lookup"><span data-stu-id="ad57a-142">The body of the transcript contains information about each command the user invoked.</span></span> <span data-ttu-id="ad57a-143">A használt parancs pontos szintaxisa nem érhető el a JEA-munkamenetekben, mert az átalakított parancsok a PowerShell távelérési szolgáltatásban.</span><span class="sxs-lookup"><span data-stu-id="ad57a-143">The exact syntax of the command used is unavailable in JEA sessions because of the way commands are transformed for PowerShell remoting.</span></span> <span data-ttu-id="ad57a-144">Azonban továbbra is meghatározhatja a végrehajtott érvényes parancsot.</span><span class="sxs-lookup"><span data-stu-id="ad57a-144">However, you can still determine the effective command that was executed.</span></span> <span data-ttu-id="ad57a-145">Az alábbi példa egy JEA-munkamenetben futó `Get-Service Dns` felhasználó egy példáját mutatja be:</span><span class="sxs-lookup"><span data-stu-id="ad57a-145">Below is an example transcript snippet from a user running `Get-Service Dns` in a JEA session:</span></span>

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

<span data-ttu-id="ad57a-146">A rendszer minden egyes, a felhasználó által futtatott parancshoz **CommandInvocation** -sort ír.</span><span class="sxs-lookup"><span data-stu-id="ad57a-146">A **CommandInvocation** line is written for each command a user runs.</span></span> <span data-ttu-id="ad57a-147">A **ParameterBindings** rögzíti a parancshoz megadott összes paramétert és értéket.</span><span class="sxs-lookup"><span data-stu-id="ad57a-147">**ParameterBindings** record each parameter and value supplied with the command.</span></span> <span data-ttu-id="ad57a-148">Az előző példában látható, hogy a paraméter **neve** a ( `Get-Service` z) parancsmaghoz tartozó **DNS** értéket adta meg.</span><span class="sxs-lookup"><span data-stu-id="ad57a-148">In the previous example, you can see that the parameter **Name** was supplied the with value **Dns** for the `Get-Service` cmdlet.</span></span>

<span data-ttu-id="ad57a-149">Az egyes parancsok kimenete **CommandInvocation**is indít, általában `Out-Default`a következőhöz:.</span><span class="sxs-lookup"><span data-stu-id="ad57a-149">The output of each command also triggers a **CommandInvocation**, usually to `Out-Default`.</span></span> <span data-ttu-id="ad57a-150">A **inputobject elemnél** `Out-Default` a parancs által visszaadott PowerShell-objektum.</span><span class="sxs-lookup"><span data-stu-id="ad57a-150">The **InputObject** of `Out-Default` is the PowerShell object returned from the command.</span></span> <span data-ttu-id="ad57a-151">Az objektum részletei az alábbi néhány sorban vannak kinyomtatva, és szorosan utánozzák, hogy a felhasználó mit látott.</span><span class="sxs-lookup"><span data-stu-id="ad57a-151">The details of that object are printed a few lines below, closely mimicking what the user would have seen.</span></span>

## <a name="see-also"></a><span data-ttu-id="ad57a-152">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ad57a-152">See also</span></span>

[<span data-ttu-id="ad57a-153">*A PowerShell-♥ a Blue Team* blogjának biztonsági bejegyzése</span><span class="sxs-lookup"><span data-stu-id="ad57a-153">*PowerShell ♥ the Blue Team* blog post on security</span></span>](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)
