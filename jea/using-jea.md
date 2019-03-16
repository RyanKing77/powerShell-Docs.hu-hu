---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: A JEA használata
ms.openlocfilehash: fa3d3a3c8bc0090ec9ad788585ec5df933134173
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054679"
---
# <a name="using-jea"></a><span data-ttu-id="6a0a7-103">A JEA használata</span><span class="sxs-lookup"><span data-stu-id="6a0a7-103">Using JEA</span></span>

> <span data-ttu-id="6a0a7-104">Érintett kiadások: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="6a0a7-104">Applies to: Windows PowerShell 5.0</span></span>

<span data-ttu-id="6a0a7-105">Ez a témakör ismerteti a különböző módokon csatlakozhat, és a JEA-végpont használata.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-105">This topic describes the various ways you can connect to and use a JEA endpoint.</span></span>

## <a name="using-jea-interactively"></a><span data-ttu-id="6a0a7-106">A JEA interaktív használata</span><span class="sxs-lookup"><span data-stu-id="6a0a7-106">Using JEA interactively</span></span>

<span data-ttu-id="6a0a7-107">Ha teszteli a JEA-konfiguráció vagy egyszerű feladatok végrehajtásához a felhasználók számára, használhatja a normál PowerShell távoli eljáráshívás munkamenet ugyanúgy JEA.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-107">If you are testing your JEA configuration or have simple tasks for users to perform, you can use JEA the same way you would a regular PowerShell remoting session.</span></span>
<span data-ttu-id="6a0a7-108">Összetett távoli eljáráshívás feladatokhoz, javasoljuk, hogy használjon [implicit távelérési](#using-jea-with-implicit-remoting) inkább hogy egyszerűbb legyen a felhasználók számára azáltal, hogy megfelelően működjenek a felhasználók az adatobjektumok helyileg.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-108">For complex remoting tasks, it is recommended to use [implicit remoting](#using-jea-with-implicit-remoting) instead to make it easier for your users by allowing users to operate with the data objects locally.</span></span>

<span data-ttu-id="6a0a7-109">A JEA interaktív használatához szüksége lesz:</span><span class="sxs-lookup"><span data-stu-id="6a0a7-109">To use JEA interactively, you will need:</span></span>
- <span data-ttu-id="6a0a7-110">A számítógép kapcsolódik a nevét (a helyi gép is lehet)</span><span class="sxs-lookup"><span data-stu-id="6a0a7-110">The name of the computer you are connecting to (can be the local machine)</span></span>
- <span data-ttu-id="6a0a7-111">A regisztrált ezen a számítógépen a JEA-végpont neve</span><span class="sxs-lookup"><span data-stu-id="6a0a7-111">The name of the JEA endpoint registered on that computer</span></span>
- <span data-ttu-id="6a0a7-112">Hitelesítő adatok a számítógép, amelyhez hozzáférése a JEA-végpont</span><span class="sxs-lookup"><span data-stu-id="6a0a7-112">Credentials for the computer that have access to the JEA endpoint</span></span>

<span data-ttu-id="6a0a7-113">Az aktuális adatnak megkezdheti a JEA munkamenet [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) vagy [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).</span><span class="sxs-lookup"><span data-stu-id="6a0a7-113">With that information in hand, you can start a JEA session using [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) or [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).</span></span>

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

<span data-ttu-id="6a0a7-114">Ha a fiók van jelenleg bejelentkezve szerint a JEA-végpont hozzáféréssel rendelkezik, akkor kihagyhatja a `-Credential` paraméter.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-114">If the account you're currently logged in as has access to the JEA endpoint, you can omit the `-Credential` parameter.</span></span>

<span data-ttu-id="6a0a7-115">Ha a PowerShell kérni a módosítások `[localhost]: PS>` , hogy most már használja a távoli munkamenetet a JEA-tudni fogja.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-115">When the PowerShell prompt changes to `[localhost]: PS>` you will know that you are now interacting with the remote JEA session.</span></span>
<span data-ttu-id="6a0a7-116">Futtathat `Get-Command` ellenőrizze a rendelkezésre álló parancsokat.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-116">You can run `Get-Command` to check which commands are available.</span></span>
<span data-ttu-id="6a0a7-117">Tekintse meg a rendszergazdát, ismerje meg, ha a rendelkezésre álló paraméterek vagy a megengedett értékei korlátozások kell.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-117">You will need to consult with your administrator to learn if there are any restrictions on the available parameters or allowable parameter values.</span></span>

<span data-ttu-id="6a0a7-118">Ne feledje a JEA-munkamenetek módban működik NoLanguage, ezért általában a powershellel több szempontból nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-118">As a reminder, JEA sessions operate in NoLanguage mode, so some of the ways you typically use PowerShell may not be available.</span></span>
<span data-ttu-id="6a0a7-119">Például az adatok tárolására, vagy vizsgálja meg a parancsmag által visszaadott objektumok tulajdonságainak változók nem használhatók.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-119">For instance, you cannot use variables to store data or inspect the properties on objects returned from cmdlets.</span></span>
<span data-ttu-id="6a0a7-120">Az alábbi példa mutat egy példát, előfordulhat, hogy a PowerShell még ma, és azonos első két módszer parancs NoLanguage módban működik.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-120">The below example shows an example of how you may be using PowerShell today, and two approaches to get the same command working in NoLanguage mode.</span></span>

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

<span data-ttu-id="6a0a7-121">Az összetettebb parancs meghívásához, amelyek megnehezítik a ezt a módszert, fontolja meg [implicit távelérési](#using-jea-with-implicit-remoting) vagy [egyéni funkciók létrehozásával](role-capabilities.md#creating-custom-functions) , amely burkolása az a Funkciók, amennyit csak szeretne.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-121">For more complex command invocations that make this approach difficult, consider using [implicit remoting](#using-jea-with-implicit-remoting) or [creating custom functions](role-capabilities.md#creating-custom-functions) that wrap the functionality you desire.</span></span>

## <a name="using-jea-with-implicit-remoting"></a><span data-ttu-id="6a0a7-122">Implicit távelérési JEA használata</span><span class="sxs-lookup"><span data-stu-id="6a0a7-122">Using JEA with implicit remoting</span></span>

<span data-ttu-id="6a0a7-123">PowerShell-alternatív távoli eljáráshívás modell, ahol webalkalmazásproxy-parancsmagok importálásához egy távoli számítógépről a helyi számítógépen, és dolgozhat velük, mintha helyi parancsok támogatja.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-123">PowerShell supports an alternative remoting model where you can import proxy cmdlets from a remote machine on your local computer and interact with them as if they were local commands.</span></span>
<span data-ttu-id="6a0a7-124">Ez implicit távelérési nevezzük, és és kifejtett [ez *Hey, Scripting Guy!* blogbejegyzés](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).</span><span class="sxs-lookup"><span data-stu-id="6a0a7-124">This is called implicit remoting, and is explained well in [this *Hey, Scripting Guy!* blog post](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).</span></span>
<span data-ttu-id="6a0a7-125">Implicit távelérési különösen hasznos, ha JEA dolgozik, mivel lehetővé teszi a JEA-parancsmagok teljes nyelvi üzemmódban működik.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-125">Implicit remoting is particularly useful when working with JEA because it allows you to work with JEA cmdlets in a full language mode.</span></span>
<span data-ttu-id="6a0a7-126">Ez azt jelenti, kiegészítés, a változók használata, objektumok módosítását, és helyi parancsfájlok használatával könnyebben automatizálhatja a JEA-végponton.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-126">This means you can use tab completion, variables, manipulate objects, and even use local scripts to more easily automate against a JEA endpoint.</span></span>
<span data-ttu-id="6a0a7-127">Visszaállít egy proxy parancsot indít el, az adatokat küldeni a JEA-végpont a távoli számítógépen, és ott hajtja végre.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-127">Anytime you invoke a proxy command, the data will be sent to the JEA endpoint on the remote machine and executed there.</span></span>

<span data-ttu-id="6a0a7-128">Implicit távelérési parancsmagok importál egy meglévő PowerShell-munkamenetet úgy működik.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-128">Implicit remoting works by importing cmdlets from an existing PowerShell session.</span></span>
<span data-ttu-id="6a0a7-129">Igény szerint kiválaszthatja megkereshetők a főnevek minden proxy parancsmag egy karakterlánccal megszakíthatja a távoli rendszer parancsai megkülönböztetni előtagot.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-129">You can optionally choose to prefix the nouns of each proxy cmdlet with a string of your choosing to distinguish which commands are for the remote system.</span></span>
<span data-ttu-id="6a0a7-130">Egy ideiglenes szkriptmodulba tartalmazó összes proxy parancsot jön létre, és használhatja a helyi PowerShell-munkamenet időtartamát.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-130">A temporary script module containing all of the proxy commands will be created and can be used for the duration of your local PowerShell session.</span></span>

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> <span data-ttu-id="6a0a7-131">Egyes rendszerek nem lehet képes importálni a alapértelmezett JEA parancsmagok megkötések miatt egy teljes JEA-munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-131">Some systems may not be able to import an entire JEA session due to constraints in the default JEA cmdlets.</span></span>
> <span data-ttu-id="6a0a7-132">Ennek elkerülése érdekében, az importálás kizárólag a szükséges parancsokat a JEA-munkamenet azáltal, hogy explicit módon a nevük a `-CommandName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-132">To get around this, only import the commands you need from the JEA session by explicitly providing their names to the `-CommandName` parameter.</span></span>
> <span data-ttu-id="6a0a7-133">Egy következő frissítés fogja oldja meg az érintett rendszerek teljes JEA-munkamenetek importálásával kapcsolatos hiba.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-133">A future update will address the issue with importing entire JEA sessions on affected systems.</span></span>

<span data-ttu-id="6a0a7-134">Ha Ön nem lehet importálni a JEA munkamenet alapértelmezett JEA paraméterek korlátai miatt, követheti a szűrje ki az importált beállítása a alapértelmezett parancsokat az alábbi lépéseket.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-134">If you are unable to import a JEA session due to constraints on the default JEA parameters, you can follow the steps below to filter out the default commands from the imported set.</span></span>
<span data-ttu-id="6a0a7-135">Ön továbbra is képesek lesznek parancsok, például `Select-Object` – csak fogja használni a távoli egy, a JEA-munkamenet helyett a számítógépre telepített helyi verziója.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-135">You will still be able to use commands like `Select-Object` -- you'll just use the local version installed on your computer instead of the remote one in the JEA session.</span></span>

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

<span data-ttu-id="6a0a7-136">A proxy parancsmagok implicit távelérési használatával is megőrizheti [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).</span><span class="sxs-lookup"><span data-stu-id="6a0a7-136">You can also persist the proxied cmdlets from implicit remoting using [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).</span></span>
<span data-ttu-id="6a0a7-137">Implicit távelérési kapcsolatos további információkért tekintse meg a Súgó dokumentációját [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) és [Import-Module](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/import-module).</span><span class="sxs-lookup"><span data-stu-id="6a0a7-137">For more information about implicit remoting, check out the help documentation for [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) and [Import-Module](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/import-module).</span></span>

## <a name="using-jea-programmatically"></a><span data-ttu-id="6a0a7-138">Programozott módon a JEA használata</span><span class="sxs-lookup"><span data-stu-id="6a0a7-138">Using JEA programmatically</span></span>

<span data-ttu-id="6a0a7-139">A JEA is használható, az automatizálási rendszer és a felhasználói alkalmazásokban, például a segélyszolgálat belső fejlesztésű alkalmazásokat és webhelyeket.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-139">JEA can also be used in automation systems and in user applications, such as in-house helpdesk apps and web sites.</span></span>
<span data-ttu-id="6a0a7-140">A módszer megegyezik, az alkalmazások létrehozásához, amely kommunikációhoz korlátozás PowerShell-végpontokra, hogy a program érdemes figyelembe venni, hogy a JEA korlátozná a távoli munkamenet futtatott parancsok csoportosítani.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-140">The approach is the same as that for building apps that talk to unconstrained PowerShell endpoints, with the caveat that the program should be aware that JEA is limiting the commands that can be run in the remote session.</span></span>

<span data-ttu-id="6a0a7-141">Egyszerű, egyszeri feladatokhoz használhatja [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) a JEA használata parancsok futtatására.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-141">For simple, one-off tasks, you can use [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) to run a set of commands using JEA.</span></span>

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

<span data-ttu-id="6a0a7-142">Ellenőrizze, hogy mely parancsok állnak rendelkezésre, amikor csatlakozik a JEA-munkamenet, futtassa a `Get-Command` közzétételt és iterációt az eredmények ellenőrzése az engedélyezett paraméterek között.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-142">To check which commands are available for use when you connect to a JEA session, run `Get-Command` and iterate through the results to check for the allowed parameters.</span></span>

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

<span data-ttu-id="6a0a7-143">Ha egy C# alkalmazást, létrehozhat egy PowerShell futási teret, amely kapcsolódik a JEA-munkamenet megadásával a konfiguráció nevét a egy [WSManConnectionInfo](https://msdn.microsoft.com/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) objektum.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-143">If you are building a C# app, you can create a PowerShell runspace that connects to a JEA session by specifying the configuration name in a [WSManConnectionInfo](https://msdn.microsoft.com/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) object.</span></span>

```csharp
// using System.Management.Automation;
var computerName = "SERVER01";
var configName   = "JEAMaintenance";
var creds        = // create a PSCredential object here (https://msdn.microsoft.com/library/system.management.automation.pscredential(v=vs.85).aspx)

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

## <a name="using-jea-with-powershell-direct"></a><span data-ttu-id="6a0a7-144">A JEA használata a PowerShell Direct használatával</span><span class="sxs-lookup"><span data-stu-id="6a0a7-144">Using JEA with PowerShell Direct</span></span>

<span data-ttu-id="6a0a7-145">A Windows 10 és Windows Server 2016 Hyper-V kínál [PowerShell Directet](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/vmsession), egy szolgáltatást, amely lehetővé teszi, hogy a Hyper-V rendszergazdák, függetlenül a hálózati konfiguráció vagy a távoli felügyelet a PowerShell használatával a virtuális gépek kezeléséhez a virtuális gép beállításait.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-145">Hyper-V in Windows 10 and Windows Server 2016 offers [PowerShell Direct](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/vmsession), a feature which allows Hyper-V administrators to manage virtual machines with PowerShell regardless of the network configuration or remote management settings on the virtual machine.</span></span>

<span data-ttu-id="6a0a7-146">A JEA PowerShell Direct használatával egy Hyper-V korlátozott rendszergazdai hozzáférést biztosíthat a virtuális gép, amely lehet hasznos, ha a virtuális gép hálózati kapcsolatát, és a egy adatközpont-felügyeleti el kell hárítania a hálózati beállításokat.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-146">You can use PowerShell Direct with JEA to give a Hyper-V administrator limited access to your VM, which can be useful if you lose network connectivity to your VM and need a datacenter admin to fix the network settings.</span></span>

<span data-ttu-id="6a0a7-147">További konfiguráció nélkül nem szükséges a JEA használata a PowerShell directtel, azonban lehet, hogy a virtuális gépen futó operációs rendszer Windows 10-es vagy Windows Server 2016-ban.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-147">No additional configuration is required to use JEA over PowerShell Direct, however the operating system running inside the virtual machine must be Windows 10 or Windows Server 2016.</span></span>
<span data-ttu-id="6a0a7-148">A Hyper-V-rendszergazda segítségével csatlakoztathatók a JEA-végpont a `-VMName` vagy `-VMId` PSRemoting parancsmagok a paramétereket:</span><span class="sxs-lookup"><span data-stu-id="6a0a7-148">The Hyper-V admin can connect to the JEA endpoint by using the `-VMName` or `-VMId` parameters on PSRemoting cmdlets:</span></span>

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

<span data-ttu-id="6a0a7-149">Erősen ajánlott, hogy hoz létre egy dedikált helyi felhasználót a rendszer a Hyper-V-rendszergazdáknak használata kezelheti semmilyen egyéb jog.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-149">It is strongly recommended that you create a dedicated local user with no other rights to manage the system for your Hyper-V administrators to use.</span></span>
<span data-ttu-id="6a0a7-150">Ne feledje, hogy még egy nem rendszerjogosultságú felhasználói továbbra is be tud jelentkezni a Windows-gépek alapértelmezés szerint, beleértve a korlátozás PowerShell használatával.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-150">Remember that even an unprivileged user can still log into a Windows machine by default, including using unconstrained PowerShell.</span></span>
<span data-ttu-id="6a0a7-151">Amely lehetővé teszi számukra (néhány) keresse meg a fájlrendszer és a további információ az operációs rendszer környezetében.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-151">That will allow them to browse (some of) the file system and learn more about your OS environment.</span></span>
<span data-ttu-id="6a0a7-152">Egy Hyper-V-rendszergazdát, hogy csakis azokhoz a virtuális gép PowerShell Direct használatával a JEA zárolhat, szüksége lesz megtagadása helyi bejelentkezési jogosultságai a Hyper-V-rendszergazda a JEA-fiókhoz.</span><span class="sxs-lookup"><span data-stu-id="6a0a7-152">To lock down a Hyper-V administrator to only access a VM using PowerShell Direct with JEA, you will need to deny local logon rights to the Hyper-V admin's JEA account.</span></span>
