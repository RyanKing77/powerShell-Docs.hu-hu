---
ms.date: 06/12/2017
keywords: jea, a powershell, a biztonsági
title: A JEA használata
ms.openlocfilehash: 891e4be4c3fadceeff5ede7ac5cab04a5f80e5c1
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190077"
---
# <a name="using-jea"></a><span data-ttu-id="dc97a-103">A JEA használata</span><span class="sxs-lookup"><span data-stu-id="dc97a-103">Using JEA</span></span>

> <span data-ttu-id="dc97a-104">A következőkre vonatkozik: a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="dc97a-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="dc97a-105">Ez a témakör ismerteti a különböző módokon csatlakozhat, és használja a JEA végpontot.</span><span class="sxs-lookup"><span data-stu-id="dc97a-105">This topic describes the various ways you can connect to and use a JEA endpoint.</span></span>

## <a name="using-jea-interactively"></a><span data-ttu-id="dc97a-106">JEA interaktív futtatása</span><span class="sxs-lookup"><span data-stu-id="dc97a-106">Using JEA interactively</span></span>

<span data-ttu-id="dc97a-107">Ha teszteli az JEA konfigurációját, vagy vannak-e egyszerű feladatok felhasználók számára, használhatja a rendszeres PowerShell távoli eljáráshívás munkamenet ugyanúgy JEA.</span><span class="sxs-lookup"><span data-stu-id="dc97a-107">If you are testing your JEA configuration or have simple tasks for users to perform, you can use JEA the same way you would a regular PowerShell remoting session.</span></span>
<span data-ttu-id="dc97a-108">Összetett távelérése feladatokhoz, javasoljuk, hogy használjon [implicit távoli eljáráshívás](#using-jea-with-implicit-remoting) helyette számára megkönnyíti a felhasználók által a felhasználók kapnak az adatok objektumokat helyileg.</span><span class="sxs-lookup"><span data-stu-id="dc97a-108">For complex remoting tasks, it is recommended to use [implicit remoting](#using-jea-with-implicit-remoting) instead to make it easier for your users by allowing users to operate with the data objects locally.</span></span>

<span data-ttu-id="dc97a-109">A JEA interaktív használatához szüksége lesz:</span><span class="sxs-lookup"><span data-stu-id="dc97a-109">To use JEA interactively, you will need:</span></span>
- <span data-ttu-id="dc97a-110">A számítógép csatlakozik a nevét (a helyi számítógépen is lehet)</span><span class="sxs-lookup"><span data-stu-id="dc97a-110">The name of the computer you are connecting to (can be the local machine)</span></span>
- <span data-ttu-id="dc97a-111">A JEA-végpont a számítógépen regisztrált neve</span><span class="sxs-lookup"><span data-stu-id="dc97a-111">The name of the JEA endpoint registered on that computer</span></span>
- <span data-ttu-id="dc97a-112">A számítógép hitelesítő adatainak a JEA végpontot elérő</span><span class="sxs-lookup"><span data-stu-id="dc97a-112">Credentials for the computer that have access to the JEA endpoint</span></span>

<span data-ttu-id="dc97a-113">Az aktuális adatnak, megkezdheti a JEA munkamenet [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) vagy [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).</span><span class="sxs-lookup"><span data-stu-id="dc97a-113">With that information in hand, you can start a JEA session using [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) or [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).</span></span>

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

<span data-ttu-id="dc97a-114">Ha a fiók jelenleg jelentkezett be, ha a JEA végponthoz való hozzáférést, akkor kihagyhatja a `-Credential` paraméter.</span><span class="sxs-lookup"><span data-stu-id="dc97a-114">If the account you're currently logged in as has access to the JEA endpoint, you can omit the `-Credential` parameter.</span></span>

<span data-ttu-id="dc97a-115">Amikor a PowerShell kérni módosításai `[localhost]: PS>` megtudják, hogy most interakció a távoli JEA-munkamenet.</span><span class="sxs-lookup"><span data-stu-id="dc97a-115">When the PowerShell prompt changes to `[localhost]: PS>` you will know that you are now interacting with the remote JEA session.</span></span>
<span data-ttu-id="dc97a-116">Futtathat `Get-Command` , mely parancsok elérhető.</span><span class="sxs-lookup"><span data-stu-id="dc97a-116">You can run `Get-Command` to check which commands are available.</span></span>
<span data-ttu-id="dc97a-117">Szüksége lesz a rendszergazdát, hogy ismerje meg, ha a rendelkezésre álló paramétereket vagy megengedett értékei korlátozások vegye fel a kapcsolatot.</span><span class="sxs-lookup"><span data-stu-id="dc97a-117">You will need to consult with your administrator to learn if there are any restrictions on the available parameters or allowable parameter values.</span></span>

<span data-ttu-id="dc97a-118">Ne feledje JEA munkamenetek üzemmódban működjenek NoLanguage, ezért néhány módot általában a PowerShellben nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="dc97a-118">As a reminder, JEA sessions operate in NoLanguage mode, so some of the ways you typically use PowerShell may not be available.</span></span>
<span data-ttu-id="dc97a-119">Például adatok tárolására, vagy vizsgálja meg a parancsmagok által visszaadott objektumok tulajdonságainak változók nem használhatók.</span><span class="sxs-lookup"><span data-stu-id="dc97a-119">For instance, you cannot use variables to store data or inspect the properties on objects returned from cmdlets.</span></span>
<span data-ttu-id="dc97a-120">Az alábbi példa azt mutatja meg, például hogy miként lehet használhat PowerShell ma, és ugyanazt a beolvasandó két megközelítés parancs NoLanguage módban működik.</span><span class="sxs-lookup"><span data-stu-id="dc97a-120">The below example shows an example of how you may be using PowerShell today, and two approaches to get the same command working in NoLanguage mode.</span></span>

```powershell
# Using variables in NoLanguage mode is disallowed, so the following will not work
# $vm = Get-VM -Name 'SQL01'
# Start-VM -VM $vm

# You can use pipes to pass data through to commands that accept input from the pipeline
Get-VM -Name 'SQL01' | Start-VM

# You can also wrap subcommands in parentheses and enter them inline as arguments
Start-VM -VM (Get-VM -Name 'SQL01')

# Better yet, use parameter sets that don't require extra data to be passed in when possible
Start-VM -VMName 'SQL01'
```

<span data-ttu-id="dc97a-121">Az összetettebb parancs-indítások megnehezítik ezt a módszert használja, érdemes lehet [implicit távoli eljáráshívás](#using-jea-with-implicit-remoting) vagy [egyéni függvények létrehozása](role-capabilities.md#creating-custom-functions) , amely a kívánt funkció burkolja.</span><span class="sxs-lookup"><span data-stu-id="dc97a-121">For more complex command invocations that make this approach difficult, consider using [implicit remoting](#using-jea-with-implicit-remoting) or [creating custom functions](role-capabilities.md#creating-custom-functions) that wrap the functionality you desire.</span></span>

## <a name="using-jea-with-implicit-remoting"></a><span data-ttu-id="dc97a-122">Implicit távelérése JEA használata</span><span class="sxs-lookup"><span data-stu-id="dc97a-122">Using JEA with implicit remoting</span></span>

<span data-ttu-id="dc97a-123">PowerShell ahol webalkalmazásproxy-parancsmagok importálásához egy távoli számítógépről a helyi számítógépen, és kezelheti azokat helyi parancsok, mintha egy alternatív távelérése modellt támogatja.</span><span class="sxs-lookup"><span data-stu-id="dc97a-123">PowerShell supports an alternative remoting model where you can import proxy cmdlets from a remote machine on your local computer and interact with them as if they were local commands.</span></span>
<span data-ttu-id="dc97a-124">Ez implicit távelérése nevezik, és esetén, tekintse meg a helyes [ez *Hey, Scripting Guy!* blogbejegyzés](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).</span><span class="sxs-lookup"><span data-stu-id="dc97a-124">This is called implicit remoting, and is explained well in [this *Hey, Scripting Guy!* blog post](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).</span></span>
<span data-ttu-id="dc97a-125">Implicit távoli eljáráshívási akkor különösen hasznos, ha olyan JEA, mert lehetővé teszi a JEA-parancsmaggal egy teljes nyelvi módban működik.</span><span class="sxs-lookup"><span data-stu-id="dc97a-125">Implicit remoting is particularly useful when working with JEA because it allows you to work with JEA cmdlets in a full language mode.</span></span>
<span data-ttu-id="dc97a-126">Ez azt jelenti, hogy kiegészítés, a változók használata, módosíthat objektumokat, és még a helyi parancsfájlok használatával könnyebben automatizálhatja a JEA végpont ellen.</span><span class="sxs-lookup"><span data-stu-id="dc97a-126">This means you can use tab completion, variables, manipulate objects, and even use local scripts to more easily automate against a JEA endpoint.</span></span>
<span data-ttu-id="dc97a-127">A proxy-utasítás hívása, bármikor az adatokat elküldi a JEA végpontnak a távoli számítógépen, és ott hajtja végre.</span><span class="sxs-lookup"><span data-stu-id="dc97a-127">Anytime you invoke a proxy command, the data will be sent to the JEA endpoint on the remote machine and executed there.</span></span>

<span data-ttu-id="dc97a-128">Implicit távelérési parancsmagok importálása egy meglévő PowerShell-munkamenetet úgy működik.</span><span class="sxs-lookup"><span data-stu-id="dc97a-128">Implicit remoting works by importing cmdlets from an existing PowerShell session.</span></span>
<span data-ttu-id="dc97a-129">Kiválaszthatja a parancsokat minden egyes proxy parancsmag segítségével különböztetheti meg egymástól, mely parancsok vannak a távoli rendszer kiválasztása a karakterláncot előtag nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="dc97a-129">You can optionally choose to prefix the nouns of each proxy cmdlet with a string of your choosing to distinguish which commands are for the remote system.</span></span>
<span data-ttu-id="dc97a-130">Egy ideiglenes szkriptmodulba tartalmazó összes proxy parancs létrehozza, és a helyi PowerShell-munkamenet időtartama alatt is használható.</span><span class="sxs-lookup"><span data-stu-id="dc97a-130">A temporary script module containing all of the proxy commands will be created and can be used for the duration of your local PowerShell session.</span></span>

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> <span data-ttu-id="dc97a-131">Előfordulhat, hogy egyes rendszerek nem importálni egy teljes JEA-munkamenet az alapértelmezett JEA parancsmagokban korlátok miatt.</span><span class="sxs-lookup"><span data-stu-id="dc97a-131">Some systems may not be able to import an entire JEA session due to constraints in the default JEA cmdlets.</span></span>
> <span data-ttu-id="dc97a-132">Ennek elkerülése érdekében, csak akkor importálja a szükséges parancsokat a JEA-munkamenetből, explicit módon adja meg a saját nevét a `-CommandName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="dc97a-132">To get around this, only import the commands you need from the JEA session by explicitly providing their names to the `-CommandName` parameter.</span></span>
> <span data-ttu-id="dc97a-133">Egy következő frissítés megoldja a teljes JEA munkamenetek érintett rendszerek importálása.</span><span class="sxs-lookup"><span data-stu-id="dc97a-133">A future update will address the issue with importing entire JEA sessions on affected systems.</span></span>

<span data-ttu-id="dc97a-134">Ha nem tudja importálni a JEA-munkamenet alapértelmezett JEA paramétereknek vonatkozó korlátozások miatt, követheti az alábbi lépéseket az alapértelmezett parancsok az importált készletből kiszűrésére.</span><span class="sxs-lookup"><span data-stu-id="dc97a-134">If you are unable to import a JEA session due to constraints on the default JEA parameters, you can follow the steps below to filter out the default commands from the imported set.</span></span>
<span data-ttu-id="dc97a-135">Továbbra is fogja tudni használni a parancsok például `Select-Object` – csak a helyi távoli helyett a JEA-munkamenetben a számítógépre telepített verzió fogja használni.</span><span class="sxs-lookup"><span data-stu-id="dc97a-135">You will still be able to use commands like `Select-Object` -- you'll just use the local version installed on your computer instead of the remote one in the JEA session.</span></span>

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Get a list of all the commands on the JEA endpoint
$commands = Invoke-Command -Session $jeasession -ScriptBlock { Get-Command }

# Filter out the default cmdlets
$jeaDefaultCmdlets = 'Clear-Host', 'Exit-PSSession', 'Get-Command', 'Get-FormatData', 'Get-Help', 'Measure-Object', 'Out-Default', 'Select-Object'
$filteredCommands = $commands.Name | Where-Object { $jeaDefaultCmdlets -notcontains $_ }

# Import only commands explicitly added in role capabilities and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA' -CommandName $filteredCommands
```

<span data-ttu-id="dc97a-136">Megőrizni a implicit távoli eljáráshívás segítségével a proxy parancsmagjait [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).</span><span class="sxs-lookup"><span data-stu-id="dc97a-136">You can also persist the proxied cmdlets from implicit remoting using [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).</span></span>
<span data-ttu-id="dc97a-137">Implicit távelérése kapcsolatos további információkért tekintse meg a Súgó dokumentációját [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) és [Import-Module](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/import-module).</span><span class="sxs-lookup"><span data-stu-id="dc97a-137">For more information about implicit remoting, check out the help documentation for [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) and [Import-Module](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/import-module).</span></span>

## <a name="using-jea-programatically"></a><span data-ttu-id="dc97a-138">JEA programozottan használatával</span><span class="sxs-lookup"><span data-stu-id="dc97a-138">Using JEA programatically</span></span>

<span data-ttu-id="dc97a-139">JEA is használható, az automatizálási rendszerek és felhasználói alkalmazásokban, például a belső fejlesztésű támogató alkalmazások és a webhelyek.</span><span class="sxs-lookup"><span data-stu-id="dc97a-139">JEA can also be used in automation systems and in user applications, such as in-house helpdesk apps and web sites.</span></span>
<span data-ttu-id="dc97a-140">A megoldás, azonos módon, amely alkalmazások készítéséhez, amely kommunikálni, korlátozás nélküli PowerShell végpontokhoz, hogy a program kell vegye figyelembe, hogy JEA korlátozza-e a távoli munkamenet futtatott parancsok szerint.</span><span class="sxs-lookup"><span data-stu-id="dc97a-140">The approach is the same as that for building apps that talk to unconstrained PowerShell endpoints, with the caveat that the program should be aware that JEA is limiting the commands that can be run in the remote session.</span></span>

<span data-ttu-id="dc97a-141">Egyszerű, egyszeri feladatokhoz használhatja [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) JEA használatával parancsok futtatásához.</span><span class="sxs-lookup"><span data-stu-id="dc97a-141">For simple, one-off tasks, you can use [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) to run a set of commands using JEA.</span></span>

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

<span data-ttu-id="dc97a-142">Ellenőrizze, hogy mely parancsok állnak rendelkezésre, amikor csatlakozik egy JEA munkamenet, futtassa a `Get-Command` és iterációt az eredmények a megengedett paraméterek kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="dc97a-142">To check which commands are available for use when you connect to a JEA session, run `Get-Command` and iterate through the results to check for the allowed parameters.</span></span>

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

<span data-ttu-id="dc97a-143">Ha egy C# alkalmazást fejleszt, a PowerShell futási térből, amely összeköti a JEA munkamenet lévő megadásával hozhat létre egy [WSManConnectionInfo](https://msdn.microsoft.com/en-us/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) objektum.</span><span class="sxs-lookup"><span data-stu-id="dc97a-143">If you are building a C# app, you can create a PowerShell runspace that connects to a JEA session by specifying the configuration name in a [WSManConnectionInfo](https://msdn.microsoft.com/en-us/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) object.</span></span>

```csharp

// using System.Management.Automation;
var computerName = "SERVER01";
var configName   = "JEAMaintenance";
var creds        = // create a PSCredential object here (https://msdn.microsoft.com/en-us/library/system.management.automation.pscredential(v=vs.85).aspx)

WSManConnectionInfo connectionInfo = new WSManConnectionInfo(
                    false,                 // Use SSL
                    computerName,          // Computer name
                    5985,                  // WSMan Port
                    "/wsman",              // WSMan Path
                    string.Format(CultureInfo.InvariantCulture, "http://schemas.microsoft.com/powershell/{0}", configName),  // Connection URI with config name
                    creds);                // Credentials
// Now, use the connection info to create a runspace where you can run the commands
using (Runspace runspace = RunspaceFactory.CreateRunspace(connectionInfo))
{
    // Open the runspace
    runspace.Open();

    using (PowerShell ps = PowerShell.Create())
    {
        // Set the PowerShell object to use the JEA runspace
        ps.Runspace = runspace;

        // Now you can add and invoke commands
        ps.AddCommand("Get-Command");
        foreach (var result in ps.Invoke())
        {
            Console.WriteLine(result);
        }
    }

    // Close the runspace
    runspace.Close();
}
```

## <a name="using-jea-with-powershell-direct"></a><span data-ttu-id="dc97a-144">PowerShell közvetlen JEA használatával</span><span class="sxs-lookup"><span data-stu-id="dc97a-144">Using JEA with PowerShell Direct</span></span>

<span data-ttu-id="dc97a-145">Hyper-V a Windows 10 és Windows Server 2016 kínál [PowerShell közvetlen](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/vmsession), egy szolgáltatás, amely lehetővé teszi, hogy a Hyper-V rendszergazdák, függetlenül a hálózati konfiguráció vagy a távoli felügyelet a PowerShell segítségével a virtuális gépek kezeléséhez a virtuális gép beállításait.</span><span class="sxs-lookup"><span data-stu-id="dc97a-145">Hyper-V in Windows 10 and Windows Server 2016 offers [PowerShell Direct](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/vmsession), a feature which allows Hyper-V administrators to manage virtual machines with PowerShell regardless of the network configuration or remote management settings on the virtual machine.</span></span>

<span data-ttu-id="dc97a-146">PowerShell közvetlen JEA biztosítanak a Hyper-V korlátozott rendszergazdai hozzáférés a virtuális Gépet, amely lehet hasznos, ha megszakad a hálózati kapcsolat a virtuális gépre, és hárítsa el a hálózati beállításokat kell egy adatközpont-felügyeleti használható.</span><span class="sxs-lookup"><span data-stu-id="dc97a-146">You can use PowerShell Direct with JEA to give a Hyper-V administrator limited access to your VM, which can be useful if you lose network connectivity to your VM and need a datacenter admin to fix the network settings.</span></span>

<span data-ttu-id="dc97a-147">Nincs további beállításokat kell megadnia PowerShell közvetlen keresztül használja a JEA, azonban a virtuális gépen futó operációs rendszer kell lennie a Windows 10 vagy Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="dc97a-147">No additional configuration is required to use JEA over PowerShell Direct, however the operating system running inside the virtual machine must be Windows 10 or Windows Server 2016.</span></span>
<span data-ttu-id="dc97a-148">A Hyper-V felügyeleti használatával csatlakozhat a JEA végpont a `-VMName` vagy `-VMId` PSRemoting parancsmagok paraméterek:</span><span class="sxs-lookup"><span data-stu-id="dc97a-148">The Hyper-V admin can connect to the JEA endpoint by using the `-VMName` or `-VMId` parameters on PSRemoting cmdlets:</span></span>

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

<span data-ttu-id="dc97a-149">Erősen ajánlott, hogy hozzon létre egy dedikált helyi felhasználói jogosultságokkal nincs más kezelheti a Hyper-V rendszergazdák számára, hogy a rendszer.</span><span class="sxs-lookup"><span data-stu-id="dc97a-149">It is strongly recommended that you create a dedicated local user with no other rights to manage the system for your Hyper-V administrators to use.</span></span>
<span data-ttu-id="dc97a-150">Ne feledje, hogy még nem rendszerjogosultságú felhasználói továbbra is be tud jelentkezni egy Windows-számítógép alapértelmezés, beleértve a korlátozás nélküli PowerShell használatával.</span><span class="sxs-lookup"><span data-stu-id="dc97a-150">Remember that even an unprivileged user can still log into a Windows machine by default, including using unconstrained PowerShell.</span></span>
<span data-ttu-id="dc97a-151">Amely lehetővé teszi (néhány) keresse meg a fájlrendszer és a további tudnivalók az operációs rendszer környezetében.</span><span class="sxs-lookup"><span data-stu-id="dc97a-151">That will allow them to browse (some of) the file system and learn more about your OS environment.</span></span>
<span data-ttu-id="dc97a-152">A Hyper-V rendszergazdák is képesek csak akkor férhessenek hozzá a virtuális gépek PowerShell közvetlenül a JEA zárolását, szüksége lesz a Hyper-V rendszergazdai JEA fiókot a helyi bejelentkezési jogokkal megtagadása.</span><span class="sxs-lookup"><span data-stu-id="dc97a-152">To lock down a Hyper-V administrator to only access a VM using PowerShell Direct with JEA, you will need to deny local logon rights to the Hyper-V admin's JEA account.</span></span>