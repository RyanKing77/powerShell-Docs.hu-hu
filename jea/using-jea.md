---
ms.date: 07/10/2019
keywords: a jea, powershell, biztonsági
title: A JEA használata
ms.openlocfilehash: 8f3cc9186c61a2ae5b64eb3dc4f72ca83f1a58c5
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734216"
---
# <a name="using-jea"></a><span data-ttu-id="374fd-103">A JEA használata</span><span class="sxs-lookup"><span data-stu-id="374fd-103">Using JEA</span></span>

<span data-ttu-id="374fd-104">Ez a cikk ismerteti a különböző módokon csatlakozhat, és a JEA-végpont használata.</span><span class="sxs-lookup"><span data-stu-id="374fd-104">This article describes the various ways you can connect to and use a JEA endpoint.</span></span>

## <a name="using-jea-interactively"></a><span data-ttu-id="374fd-105">A JEA interaktív használata</span><span class="sxs-lookup"><span data-stu-id="374fd-105">Using JEA interactively</span></span>

<span data-ttu-id="374fd-106">Ha a JEA-konfiguráció tesztel, vagy rendelkezik az egyszerű feladatokat a felhasználók számára, használhatja a normál PowerShell távoli eljáráshívás munkamenet ugyanúgy JEA.</span><span class="sxs-lookup"><span data-stu-id="374fd-106">If you're testing your JEA configuration or have simple tasks for users, you can use JEA the same way you would a regular PowerShell remoting session.</span></span> <span data-ttu-id="374fd-107">Összetett távoli eljáráshívás feladatokhoz, azt javasoljuk, hogy használjon [implicit távelérési](#using-jea-with-implicit-remoting).</span><span class="sxs-lookup"><span data-stu-id="374fd-107">For complex remoting tasks, it's recommended to use [implicit remoting](#using-jea-with-implicit-remoting).</span></span> <span data-ttu-id="374fd-108">Implicit távelérési lehetővé teszi a felhasználóknak az adatobjektumok helyileg kapnak.</span><span class="sxs-lookup"><span data-stu-id="374fd-108">Implicit remoting allows users to operate with the data objects locally.</span></span>

<span data-ttu-id="374fd-109">A JEA interaktív használatához az alábbiak szükségesek:</span><span class="sxs-lookup"><span data-stu-id="374fd-109">To use JEA interactively, you need:</span></span>

- <span data-ttu-id="374fd-110">A számítógép, amelyhez csatlakozik a nevét (a helyi gép is lehet)</span><span class="sxs-lookup"><span data-stu-id="374fd-110">The name of the computer you're connecting to (can be the local machine)</span></span>
- <span data-ttu-id="374fd-111">A regisztrált ezen a számítógépen a JEA-végpont neve</span><span class="sxs-lookup"><span data-stu-id="374fd-111">The name of the JEA endpoint registered on that computer</span></span>
- <span data-ttu-id="374fd-112">Hitelesítő adatokat, amelyek a JEA-végpont a hozzáférést az adott számítógépen</span><span class="sxs-lookup"><span data-stu-id="374fd-112">Credentials that have access to the JEA endpoint on that computer</span></span>

<span data-ttu-id="374fd-113">Adja meg ezt az információt, megkezdheti a JEA munkamenet a [New-PSSession](/powershell/module/microsoft.powershell.core/New-PSSession) vagy [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="374fd-113">Given that information, you can start a JEA session using the [New-PSSession](/powershell/module/microsoft.powershell.core/New-PSSession) or [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) cmdlets.</span></span>

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

<span data-ttu-id="374fd-114">Ha az aktuális felhasználói fiók hozzáfér a JEA-végpont, kihagyhatja a **Credential** paraméter.</span><span class="sxs-lookup"><span data-stu-id="374fd-114">If the current user account has access to the JEA endpoint, you can omit the **Credential** parameter.</span></span>

<span data-ttu-id="374fd-115">Ha a PowerShell kérni a módosítások `[localhost]: PS>` tudja, hogy Ön már műveleteket végeznek a JEA távoli munkamenet.</span><span class="sxs-lookup"><span data-stu-id="374fd-115">When the PowerShell prompt changes to `[localhost]: PS>` you know that you're now interacting with the remote JEA session.</span></span> <span data-ttu-id="374fd-116">Futtathat `Get-Command` ellenőrizze a rendelkezésre álló parancsokat.</span><span class="sxs-lookup"><span data-stu-id="374fd-116">You can run `Get-Command` to check which commands are available.</span></span> <span data-ttu-id="374fd-117">Kérje a rendszergazdát, hogy ismerje meg, hogy vannak-e a paramétereket, vagy engedélyezett értékei korlátozások.</span><span class="sxs-lookup"><span data-stu-id="374fd-117">Consult with your administrator to learn if there are any restrictions on the available parameters or allowed parameter values.</span></span>

<span data-ttu-id="374fd-118">Ne feledje, hogy a JEA-munkamenetek NoLanguage módban működik.</span><span class="sxs-lookup"><span data-stu-id="374fd-118">Remember, JEA sessions operate in NoLanguage mode.</span></span> <span data-ttu-id="374fd-119">Általában a powershellel több szempontból nem lehet érhető el.</span><span class="sxs-lookup"><span data-stu-id="374fd-119">Some of the ways you typically use PowerShell may not be available.</span></span> <span data-ttu-id="374fd-120">Például az adatok tárolására, vagy vizsgálja meg a parancsmag által visszaadott objektumok tulajdonságainak változók nem használhatók.</span><span class="sxs-lookup"><span data-stu-id="374fd-120">For instance, you can't use variables to store data or inspect the properties on objects returned from cmdlets.</span></span> <span data-ttu-id="374fd-121">Az alábbi példa bemutatja a két megközelítés ugyanazokat a parancsokat NoLanguage módban való működésre beolvasásához.</span><span class="sxs-lookup"><span data-stu-id="374fd-121">The following example shows two approaches to get the same commands to work in NoLanguage mode.</span></span>

```powershell
# Using variables is prohibited in NoLanguage mode. The following will not work:
# $vm = Get-VM -Name 'SQL01'
# Start-VM -VM $vm

# You can use pipes to pass data through to commands that accept input from the pipeline
Get-VM -Name 'SQL01' | Start-VM

# You can also wrap subcommands in parentheses and enter them inline as arguments
Start-VM -VM (Get-VM -Name 'SQL01')

# You can also use parameter sets that don't require extra data to be passed in
Start-VM -VMName 'SQL01'
```

<span data-ttu-id="374fd-122">Az összetettebb parancs meghívásához, amelyek megnehezítik a ezt a módszert, fontolja meg [implicit távelérési](#using-jea-with-implicit-remoting) vagy [egyéni funkciók létrehozásával](role-capabilities.md#creating-custom-functions) , amely burkolhatja a funkciókra van szüksége.</span><span class="sxs-lookup"><span data-stu-id="374fd-122">For more complex command invocations that make this approach difficult, consider using [implicit remoting](#using-jea-with-implicit-remoting) or [creating custom functions](role-capabilities.md#creating-custom-functions) that wrap the functionality you require.</span></span>

## <a name="using-jea-with-implicit-remoting"></a><span data-ttu-id="374fd-123">Implicit távelérési JEA használata</span><span class="sxs-lookup"><span data-stu-id="374fd-123">Using JEA with implicit remoting</span></span>

<span data-ttu-id="374fd-124">PowerShell-implicit távelérési modell, amely lehetővé teszi a webalkalmazásproxy-parancsmagok importálásához egy távoli számítógépről, és dolgozhat velük, mintha helyi parancsokat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="374fd-124">PowerShell has an implicit remoting model that lets you import proxy cmdlets from a remote machine and interact with them as if they were local commands.</span></span> <span data-ttu-id="374fd-125">A jelen kifejtett implicit távelérési **Hey, Scripting Guy!**</span><span class="sxs-lookup"><span data-stu-id="374fd-125">Implicit remoting is explained in this **Hey, Scripting Guy!**</span></span> <span data-ttu-id="374fd-126">[blogbejegyzés](https://devblogs.microsoft.com/scripting/remoting-the-implicit-way/).</span><span class="sxs-lookup"><span data-stu-id="374fd-126">[blog post](https://devblogs.microsoft.com/scripting/remoting-the-implicit-way/).</span></span>
<span data-ttu-id="374fd-127">Implicit távelérési akkor hasznos, ha a JEA használata, mert lehetővé teszi, hogy a JEA-parancsmagok teljes nyelvi üzemmódban.</span><span class="sxs-lookup"><span data-stu-id="374fd-127">Implicit remoting is useful when working with JEA because it allows you to work with JEA cmdlets in a full language mode.</span></span> <span data-ttu-id="374fd-128">Kiegészítés, a változók használata, objektumok módosítását, és akár a helyi parancsprogramok használatával automatizálhatja a feladatokat a JEA-végpont.</span><span class="sxs-lookup"><span data-stu-id="374fd-128">You can use tab completion, variables, manipulate objects, and even use local scripts to automate tasks against a JEA endpoint.</span></span> <span data-ttu-id="374fd-129">Visszaállít egy proxy parancsot indít el, az adatok a távoli gépen a JEA-végpont fogadja és ott hajtja végre.</span><span class="sxs-lookup"><span data-stu-id="374fd-129">Anytime you invoke a proxy command, the data is sent to the JEA endpoint on the remote machine and executed there.</span></span>

<span data-ttu-id="374fd-130">Implicit távelérési parancsmagok importál egy meglévő PowerShell-munkamenetet úgy működik.</span><span class="sxs-lookup"><span data-stu-id="374fd-130">Implicit remoting works by importing cmdlets from an existing PowerShell session.</span></span> <span data-ttu-id="374fd-131">Igény szerint kiválaszthatja előtagot megkereshetők a főnevek minden proxy parancsmag egy tetszőleges karakterláncra.</span><span class="sxs-lookup"><span data-stu-id="374fd-131">You can optionally choose to prefix the nouns of each proxy cmdlet with a string of your choosing.</span></span> <span data-ttu-id="374fd-132">Az előtag lehetővé teszi a távoli rendszer parancsok megkülönböztetéséhez.</span><span class="sxs-lookup"><span data-stu-id="374fd-132">The prefix allows you to distinguish the commands that are for the remote system.</span></span> <span data-ttu-id="374fd-133">A proxy-parancsok tartalmazó ideiglenes parancsfájl modul létrejött, és importálja a helyi PowerShell-munkamenetben időtartamára.</span><span class="sxs-lookup"><span data-stu-id="374fd-133">A temporary script module containing all the proxy commands is created and imported for the duration of your local PowerShell session.</span></span>

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> <span data-ttu-id="374fd-134">Egyes rendszerek nem lehet képes importálni a alapértelmezett JEA parancsmagok megkötések miatt egy teljes JEA-munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="374fd-134">Some systems may not be able to import an entire JEA session due to constraints in the default JEA cmdlets.</span></span> <span data-ttu-id="374fd-135">Ennek elkerülése érdekében, az importálás kizárólag a szükséges parancsokat a JEA-munkamenet azáltal, hogy explicit módon a nevük a `-CommandName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="374fd-135">To get around this, only import the commands you need from the JEA session by explicitly providing their names to the `-CommandName` parameter.</span></span> <span data-ttu-id="374fd-136">Egy következő frissítés fogja oldja meg az érintett rendszerek teljes JEA-munkamenetek importálásával kapcsolatos hiba.</span><span class="sxs-lookup"><span data-stu-id="374fd-136">A future update will address the issue with importing entire JEA sessions on affected systems.</span></span>

<span data-ttu-id="374fd-137">Ha Ön nem lehet importálni a JEA-munkamenet alapértelmezett paramétereihez JEA korlátozások miatt, kövesse az alábbi lépéseket az alapértelmezett parancsok közül az importált szűréséhez.</span><span class="sxs-lookup"><span data-stu-id="374fd-137">If you're unable to import a JEA session because of JEA constraints on the default parameters, follow the steps below to filter out the default commands from the imported set.</span></span> <span data-ttu-id="374fd-138">Továbbra is használható parancsok, például `Select-Object`, azonban csak a helyi verziója helyett a JEA távoli munkamenet importált egy számítógépre telepített fogja használni.</span><span class="sxs-lookup"><span data-stu-id="374fd-138">You can continue use commands like `Select-Object`, but you'll just use the local version installed on your computer instead of the one imported from the remote JEA session.</span></span>

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

<span data-ttu-id="374fd-139">A proxy parancsmagok implicit távelérési használatával is megőrizheti [Export-PSSession](/powershell/microsoft.powershell.utility/Export-PSSession).</span><span class="sxs-lookup"><span data-stu-id="374fd-139">You can also persist the proxied cmdlets from implicit remoting using [Export-PSSession](/powershell/microsoft.powershell.utility/Export-PSSession).</span></span>
<span data-ttu-id="374fd-140">Implicit távelérési kapcsolatos további információkért lásd a dokumentációban [Import-PSSession](/powershell/microsoft.powershell.utility/import-pssession) és [Import-Module](/powershell/microsoft.powershell.core/import-module).</span><span class="sxs-lookup"><span data-stu-id="374fd-140">For more information about implicit remoting, see the documentation for [Import-PSSession](/powershell/microsoft.powershell.utility/import-pssession) and [Import-Module](/powershell/microsoft.powershell.core/import-module).</span></span>

## <a name="using-jea-programmatically"></a><span data-ttu-id="374fd-141">Programozott módon a JEA használata</span><span class="sxs-lookup"><span data-stu-id="374fd-141">Using JEA programmatically</span></span>

<span data-ttu-id="374fd-142">A JEA is használható, az automatizálási rendszer és a felhasználói alkalmazásokban, például a segélyszolgálat belső fejlesztésű alkalmazásokat és webhelyeket.</span><span class="sxs-lookup"><span data-stu-id="374fd-142">JEA can also be used in automation systems and in user applications, such as in-house helpdesk apps and websites.</span></span> <span data-ttu-id="374fd-143">A módszer ugyanaz, mint amellyel korlátozás PowerShell végpontok kommunikálhatnak alkalmazások készítéséhez.</span><span class="sxs-lookup"><span data-stu-id="374fd-143">The approach is the same as that for building apps that talk to unconstrained PowerShell endpoints.</span></span> <span data-ttu-id="374fd-144">Győződjön meg arról, a program célja által a JEA használata.</span><span class="sxs-lookup"><span data-stu-id="374fd-144">Ensure the program is designed to work with limitation imposed by JEA.</span></span>

<span data-ttu-id="374fd-145">Egyszerű, egyszeri feladatokhoz használhatja [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command) JEA munkamenet-parancsok futtatásához.</span><span class="sxs-lookup"><span data-stu-id="374fd-145">For simple, one-off tasks, you can use [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command) to run commands in a JEA session.</span></span>

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

<span data-ttu-id="374fd-146">Ellenőrizze, hogy mely parancsok állnak rendelkezésre, amikor csatlakozik a JEA-munkamenet, futtassa a `Get-Command` közzétételt és iterációt az eredmények ellenőrzése az engedélyezett paraméterek között.</span><span class="sxs-lookup"><span data-stu-id="374fd-146">To check which commands are available for use when you connect to a JEA session, run `Get-Command` and iterate through the results to check for the allowed parameters.</span></span>

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

<span data-ttu-id="374fd-147">Ha készít egy C# alkalmazást, létrehozhat egy PowerShell futási teret, amely kapcsolódik a JEA-munkamenet megadásával a konfiguráció nevét a egy [WSManConnectionInfo](/dotnet/api/system.management.automation.runspaces.wsmanconnectioninfo) objektum.</span><span class="sxs-lookup"><span data-stu-id="374fd-147">If you're building a C# app, you can create a PowerShell runspace that connects to a JEA session by specifying the configuration name in a [WSManConnectionInfo](/dotnet/api/system.management.automation.runspaces.wsmanconnectioninfo) object.</span></span>

```csharp
// using System.Management.Automation;
var computerName = "SERVER01";
var configName   = "JEAMaintenance";
// See https://docs.microsoft.com/dotnet/api/system.management.automation.pscredential
var creds        = // create a PSCredential object here

WSManConnectionInfo connectionInfo = new WSManConnectionInfo(
    false,                 // Use SSL
    computerName,          // Computer name
    5985,                  // WSMan Port
    "/wsman",              // WSMan Path
                           // Connection URI with config name
    string.Format(CultureInfo.InvariantCulture, "http://schemas.microsoft.com/powershell/{0}", configName),
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

## <a name="using-jea-with-powershell-direct"></a><span data-ttu-id="374fd-148">A JEA használata a PowerShell Direct használatával</span><span class="sxs-lookup"><span data-stu-id="374fd-148">Using JEA with PowerShell Direct</span></span>

<span data-ttu-id="374fd-149">A Windows 10 és Windows Server 2016 Hyper-V kínál [PowerShell Directet](/virtualization/hyper-v-on-windows/user-guide/powershell-direct), lehetővé teszi, hogy a Hyper-V rendszergazdák, függetlenül a hálózati konfiguráció vagy a távoli felügyelet a PowerShell használatával a virtuális gépek kezeléséhez a virtuális gép beállításait.</span><span class="sxs-lookup"><span data-stu-id="374fd-149">Hyper-V in Windows 10 and Windows Server 2016 offers [PowerShell Direct](/virtualization/hyper-v-on-windows/user-guide/powershell-direct), a feature that allows Hyper-V administrators to manage virtual machines with PowerShell regardless of the network configuration or remote management settings on the virtual machine.</span></span>

<span data-ttu-id="374fd-150">A JEA PowerShell Direct használatával egy Hyper-V korlátozott rendszergazdai hozzáférést biztosíthat a virtuális gép.</span><span class="sxs-lookup"><span data-stu-id="374fd-150">You can use PowerShell Direct with JEA to give a Hyper-V administrator limited access to your VM.</span></span>
<span data-ttu-id="374fd-151">Ez hasznos lehet, ha a virtuális gép hálózati kapcsolatát, és egy adatközpont-rendszergazdát, hogy javítsa a hálózati beállításokat.</span><span class="sxs-lookup"><span data-stu-id="374fd-151">This can be useful if you lose network connectivity to your VM and need a datacenter admin to fix the network settings.</span></span>

<span data-ttu-id="374fd-152">A JEA használata a PowerShell directtel szükséges további konfiguráció nélkül.</span><span class="sxs-lookup"><span data-stu-id="374fd-152">No additional configuration is required to use JEA over PowerShell Direct.</span></span> <span data-ttu-id="374fd-153">Azonban a vendég operációs rendszer a virtuális gépen futó Windows 10, Windows Server 2016 vagy újabb kell lennie.</span><span class="sxs-lookup"><span data-stu-id="374fd-153">However, the guest operating system running inside the virtual machine must be Windows 10, Windows Server 2016, or higher.</span></span> <span data-ttu-id="374fd-154">A Hyper-V-rendszergazda segítségével csatlakoztathatók a JEA-végpont a `-VMName` vagy `-VMId` PSRemoting parancsmagok a paramétereket:</span><span class="sxs-lookup"><span data-stu-id="374fd-154">The Hyper-V admin can connect to the JEA endpoint by using the `-VMName` or `-VMId` parameters on PSRemoting cmdlets:</span></span>

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

<span data-ttu-id="374fd-155">Javasoljuk egy dedikált felhasználói fiókot hoz létre a Hyper-V rendszergazda kezelésére használható a rendszer szükséges minimális jogokkal.</span><span class="sxs-lookup"><span data-stu-id="374fd-155">It's recommended you create a dedicated user account with the minimum rights needed to manage the system for use by a Hyper-V administrator.</span></span> <span data-ttu-id="374fd-156">Ne feledje, hogy még egy nem rendszerjogosultságú felhasználói egy Windows-számítógép be tud jelentkezni az alapértelmezés szerint, beleértve a korlátozás PowerShell használatával.</span><span class="sxs-lookup"><span data-stu-id="374fd-156">Remember, even an unprivileged user can sign into a Windows machine by default, including using unconstrained PowerShell.</span></span> <span data-ttu-id="374fd-157">Amely lehetővé teszi számukra, hogy a fájlrendszer tallózása és további információ az operációs rendszer környezetében.</span><span class="sxs-lookup"><span data-stu-id="374fd-157">That allows them to browse the file system and learn more about your OS environment.</span></span> <span data-ttu-id="374fd-158">A Hyper-V-rendszergazdák zárolását, és korlátozhatja a azokat csak a virtuális gép PowerShell Direct használatával a JEA eléréséhez, megtagadja a helyi bejelentkezési jogosultságai a Hyper-V-rendszergazda a JEA-fiókhoz.</span><span class="sxs-lookup"><span data-stu-id="374fd-158">To lock down a Hyper-V administrator and limit them to only access a VM using PowerShell Direct with JEA, you must deny local logon rights to the Hyper-V admin's JEA account.</span></span>
