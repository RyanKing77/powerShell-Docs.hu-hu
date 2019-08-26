---
ms.date: 07/10/2019
keywords: jea, PowerShell, biztonság
title: A JEA használata
ms.openlocfilehash: 8f3cc9186c61a2ae5b64eb3dc4f72ca83f1a58c5
ms.sourcegitcommit: e894ed833cef57967cdaf002f8c883f66864e836
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017894"
---
# <a name="using-jea"></a><span data-ttu-id="d8358-103">A JEA használata</span><span class="sxs-lookup"><span data-stu-id="d8358-103">Using JEA</span></span>

<span data-ttu-id="d8358-104">Ez a cikk ismerteti a JEA-végpontokhoz való kapcsolódás különböző módszereit és használatát.</span><span class="sxs-lookup"><span data-stu-id="d8358-104">This article describes the various ways you can connect to and use a JEA endpoint.</span></span>

## <a name="using-jea-interactively"></a><span data-ttu-id="d8358-105">A JEA interaktív használata</span><span class="sxs-lookup"><span data-stu-id="d8358-105">Using JEA interactively</span></span>

<span data-ttu-id="d8358-106">Ha teszteli a JEA-konfigurációt, vagy egyszerű feladatokat használ a felhasználók számára, ugyanúgy használhatja a JEA-t, mint egy hagyományos PowerShell-távelérési munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="d8358-106">If you're testing your JEA configuration or have simple tasks for users, you can use JEA the same way you would a regular PowerShell remoting session.</span></span> <span data-ttu-id="d8358-107">Az összetett távelérési feladatok esetében ajánlott az [implicit távelérés](#using-jea-with-implicit-remoting)használata.</span><span class="sxs-lookup"><span data-stu-id="d8358-107">For complex remoting tasks, it's recommended to use [implicit remoting](#using-jea-with-implicit-remoting).</span></span> <span data-ttu-id="d8358-108">Az implicit távelérés lehetővé teszi, hogy a felhasználók helyileg működjenek együtt az adatobjektumokkal.</span><span class="sxs-lookup"><span data-stu-id="d8358-108">Implicit remoting allows users to operate with the data objects locally.</span></span>

<span data-ttu-id="d8358-109">A JEA interaktív használatához a következőkre lesz szüksége:</span><span class="sxs-lookup"><span data-stu-id="d8358-109">To use JEA interactively, you need:</span></span>

- <span data-ttu-id="d8358-110">Annak a számítógépnek a neve, amelyhez csatlakozik (a helyi gép lehet)</span><span class="sxs-lookup"><span data-stu-id="d8358-110">The name of the computer you're connecting to (can be the local machine)</span></span>
- <span data-ttu-id="d8358-111">A számítógépen regisztrált JEA-végpont neve</span><span class="sxs-lookup"><span data-stu-id="d8358-111">The name of the JEA endpoint registered on that computer</span></span>
- <span data-ttu-id="d8358-112">A számítógépen található JEA-végponthoz hozzáféréssel rendelkező hitelesítő adatok</span><span class="sxs-lookup"><span data-stu-id="d8358-112">Credentials that have access to the JEA endpoint on that computer</span></span>

<span data-ttu-id="d8358-113">Ezen információk alapján elindíthat egy JEA-munkamenetet a [New-PSSession](/powershell/module/microsoft.powershell.core/New-PSSession) vagy a [ENTER-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="d8358-113">Given that information, you can start a JEA session using the [New-PSSession](/powershell/module/microsoft.powershell.core/New-PSSession) or [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) cmdlets.</span></span>

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

<span data-ttu-id="d8358-114">Ha az aktuális felhasználói fiók rendelkezik hozzáféréssel az JEA-végponthoz, kihagyhatja a **hitelesítő adat** paramétert.</span><span class="sxs-lookup"><span data-stu-id="d8358-114">If the current user account has access to the JEA endpoint, you can omit the **Credential** parameter.</span></span>

<span data-ttu-id="d8358-115">Amikor a PowerShell felszólítja `[localhost]: PS>` , hogy tudja, hogy most már együttműködik a távoli JEA-munkamenettel.</span><span class="sxs-lookup"><span data-stu-id="d8358-115">When the PowerShell prompt changes to `[localhost]: PS>` you know that you're now interacting with the remote JEA session.</span></span> <span data-ttu-id="d8358-116">A futtatásával `Get-Command` ellenőrizhető, hogy mely parancsok érhetők el.</span><span class="sxs-lookup"><span data-stu-id="d8358-116">You can run `Get-Command` to check which commands are available.</span></span> <span data-ttu-id="d8358-117">Forduljon a rendszergazdához, és Ismerje meg, hogy van-e korlátozás az elérhető paraméterekkel vagy az engedélyezett paraméterek értékeivel kapcsolatban.</span><span class="sxs-lookup"><span data-stu-id="d8358-117">Consult with your administrator to learn if there are any restrictions on the available parameters or allowed parameter values.</span></span>

<span data-ttu-id="d8358-118">Ne feledje, hogy a JEA-munkamenetek nem nyelvi módban működnek.</span><span class="sxs-lookup"><span data-stu-id="d8358-118">Remember, JEA sessions operate in NoLanguage mode.</span></span> <span data-ttu-id="d8358-119">Előfordulhat, hogy a PowerShell használatának néhány módja nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="d8358-119">Some of the ways you typically use PowerShell may not be available.</span></span> <span data-ttu-id="d8358-120">Például nem használhat változókat adatok tárolására, vagy megvizsgálhatja a parancsmagokból visszaadott objektumok tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="d8358-120">For instance, you can't use variables to store data or inspect the properties on objects returned from cmdlets.</span></span> <span data-ttu-id="d8358-121">Az alábbi példa két módszert mutat be, amelyekkel ugyanazokat a parancsokat lehet a nem nyelvi módban dolgozni.</span><span class="sxs-lookup"><span data-stu-id="d8358-121">The following example shows two approaches to get the same commands to work in NoLanguage mode.</span></span>

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

<span data-ttu-id="d8358-122">Az ezt a megközelítést megnehezíti, összetettebb parancs-hívásokhoz használjon [implicit távelérést](#using-jea-with-implicit-remoting) , vagy [hozzon létre olyan egyéni függvényeket](role-capabilities.md#creating-custom-functions) , amelyek betakarják a szükséges funkciókat.</span><span class="sxs-lookup"><span data-stu-id="d8358-122">For more complex command invocations that make this approach difficult, consider using [implicit remoting](#using-jea-with-implicit-remoting) or [creating custom functions](role-capabilities.md#creating-custom-functions) that wrap the functionality you require.</span></span>

## <a name="using-jea-with-implicit-remoting"></a><span data-ttu-id="d8358-123">JEA használata implicit táveléréssel</span><span class="sxs-lookup"><span data-stu-id="d8358-123">Using JEA with implicit remoting</span></span>

<span data-ttu-id="d8358-124">A PowerShell implicit távelérési modellel rendelkezik, amely lehetővé teszi a proxy-parancsmagok távoli gépről történő importálását, és a velük való interakciót, mintha helyi parancsok lennének.</span><span class="sxs-lookup"><span data-stu-id="d8358-124">PowerShell has an implicit remoting model that lets you import proxy cmdlets from a remote machine and interact with them as if they were local commands.</span></span> <span data-ttu-id="d8358-125">Az implicit távelérést ebben a **Hey, Scripting Guy** -ban ismertetjük.</span><span class="sxs-lookup"><span data-stu-id="d8358-125">Implicit remoting is explained in this **Hey, Scripting Guy!**</span></span> <span data-ttu-id="d8358-126">[blogbejegyzés](https://devblogs.microsoft.com/scripting/remoting-the-implicit-way/).</span><span class="sxs-lookup"><span data-stu-id="d8358-126">[blog post](https://devblogs.microsoft.com/scripting/remoting-the-implicit-way/).</span></span>
<span data-ttu-id="d8358-127">Az implicit távelérés akkor hasznos, ha a JEA dolgozik, mivel lehetővé teszi a JEA-parancsmagok teljes nyelvi módban való használatát.</span><span class="sxs-lookup"><span data-stu-id="d8358-127">Implicit remoting is useful when working with JEA because it allows you to work with JEA cmdlets in a full language mode.</span></span> <span data-ttu-id="d8358-128">Használhatja a TAB-kiegészítést, a változókat, az objektumok módosítását, és akár helyi parancsfájlokat is használhat a JEA-végpontra irányuló feladatok automatizálásához.</span><span class="sxs-lookup"><span data-stu-id="d8358-128">You can use tab completion, variables, manipulate objects, and even use local scripts to automate tasks against a JEA endpoint.</span></span> <span data-ttu-id="d8358-129">A proxy parancs meghívása után az adatküldés a távoli gépen található JEA-végpontra történik, és ott hajtja végre.</span><span class="sxs-lookup"><span data-stu-id="d8358-129">Anytime you invoke a proxy command, the data is sent to the JEA endpoint on the remote machine and executed there.</span></span>

<span data-ttu-id="d8358-130">Az implicit távelérés úgy működik, hogy parancsmagokat importál egy meglévő PowerShell-munkamenetből.</span><span class="sxs-lookup"><span data-stu-id="d8358-130">Implicit remoting works by importing cmdlets from an existing PowerShell session.</span></span> <span data-ttu-id="d8358-131">Opcionálisan megadhatja, hogy az egyes proxy-parancsmagok neve előtaggal legyen elválasztva.</span><span class="sxs-lookup"><span data-stu-id="d8358-131">You can optionally choose to prefix the nouns of each proxy cmdlet with a string of your choosing.</span></span> <span data-ttu-id="d8358-132">Az előtag lehetővé teszi a távoli rendszerhez tartozó parancsok megkülönböztetését.</span><span class="sxs-lookup"><span data-stu-id="d8358-132">The prefix allows you to distinguish the commands that are for the remote system.</span></span> <span data-ttu-id="d8358-133">A rendszer az összes proxy parancsot tartalmazó ideiglenes parancsfájl-modult hozza létre és importálja a helyi PowerShell-munkamenet időtartama alatt.</span><span class="sxs-lookup"><span data-stu-id="d8358-133">A temporary script module containing all the proxy commands is created and imported for the duration of your local PowerShell session.</span></span>

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> <span data-ttu-id="d8358-134">Előfordulhat, hogy egyes rendszerek nem tudnak teljes JEA-munkamenetet importálni az alapértelmezett JEA-parancsmagok korlátai miatt.</span><span class="sxs-lookup"><span data-stu-id="d8358-134">Some systems may not be able to import an entire JEA session due to constraints in the default JEA cmdlets.</span></span> <span data-ttu-id="d8358-135">Ennek megkezdéséhez csak a szükséges parancsokat kell importálnia a JEA-munkamenetből, ha explicit módon megadja nevüket `-CommandName` a paraméternek.</span><span class="sxs-lookup"><span data-stu-id="d8358-135">To get around this, only import the commands you need from the JEA session by explicitly providing their names to the `-CommandName` parameter.</span></span> <span data-ttu-id="d8358-136">A jövőbeli frissítések a teljes JEA-munkamenetek importálásával foglalkoznak az érintett rendszereken.</span><span class="sxs-lookup"><span data-stu-id="d8358-136">A future update will address the issue with importing entire JEA sessions on affected systems.</span></span>

<span data-ttu-id="d8358-137">Ha nem tudja importálni a JEA-munkamenetet az alapértelmezett paraméterek JEA megkötése miatt, kövesse az alábbi lépéseket az importált készlet alapértelmezett parancsainak kiszűréséhez.</span><span class="sxs-lookup"><span data-stu-id="d8358-137">If you're unable to import a JEA session because of JEA constraints on the default parameters, follow the steps below to filter out the default commands from the imported set.</span></span> <span data-ttu-id="d8358-138">Továbbra is használhatja az olyan `Select-Object`parancsokat, mint a, de a távoli JEA-munkamenetből importált helyett csak a számítógépen telepített helyi verziót fogja használni.</span><span class="sxs-lookup"><span data-stu-id="d8358-138">You can continue use commands like `Select-Object`, but you'll just use the local version installed on your computer instead of the one imported from the remote JEA session.</span></span>

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

<span data-ttu-id="d8358-139">Az [export-PSSession](/powershell/microsoft.powershell.utility/Export-PSSession)használatával is megtarthatja a proxyn belüli parancsmagokat az implicit távelérésből.</span><span class="sxs-lookup"><span data-stu-id="d8358-139">You can also persist the proxied cmdlets from implicit remoting using [Export-PSSession](/powershell/microsoft.powershell.utility/Export-PSSession).</span></span>
<span data-ttu-id="d8358-140">Az implicit távoli eljáráshívás szolgáltatással kapcsolatos további információkért tekintse meg az [import-PSSession](/powershell/microsoft.powershell.utility/import-pssession) és az [import-Module](/powershell/microsoft.powershell.core/import-module)dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="d8358-140">For more information about implicit remoting, see the documentation for [Import-PSSession](/powershell/microsoft.powershell.utility/import-pssession) and [Import-Module](/powershell/microsoft.powershell.core/import-module).</span></span>

## <a name="using-jea-programmatically"></a><span data-ttu-id="d8358-141">A JEA programozott módon történő használata</span><span class="sxs-lookup"><span data-stu-id="d8358-141">Using JEA programmatically</span></span>

<span data-ttu-id="d8358-142">A JEA automatizálási rendszerekben és felhasználói alkalmazásokban is használhatók, például a házon belüli segélyszolgálat alkalmazásaiban és webhelyein.</span><span class="sxs-lookup"><span data-stu-id="d8358-142">JEA can also be used in automation systems and in user applications, such as in-house helpdesk apps and websites.</span></span> <span data-ttu-id="d8358-143">A módszer ugyanaz, mint a nem korlátozott PowerShell-végpontokkal kommunikáló alkalmazások létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="d8358-143">The approach is the same as that for building apps that talk to unconstrained PowerShell endpoints.</span></span> <span data-ttu-id="d8358-144">Győződjön meg arról, hogy a program úgy van kialakítva, hogy a JEA által megszabott korlátozásokkal működjön.</span><span class="sxs-lookup"><span data-stu-id="d8358-144">Ensure the program is designed to work with limitation imposed by JEA.</span></span>

<span data-ttu-id="d8358-145">Egyszerű, egyszeri feladatokhoz használhatja a Meghívási [parancsot](/powershell/module/microsoft.powershell.core/invoke-command) a JEA-munkamenetben lévő parancsok futtatásához.</span><span class="sxs-lookup"><span data-stu-id="d8358-145">For simple, one-off tasks, you can use [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command) to run commands in a JEA session.</span></span>

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

<span data-ttu-id="d8358-146">A JEA-munkamenethez való csatlakozáskor használható parancsok megadásához futtassa `Get-Command` a parancsot, és ismételje meg az eredményeket az engedélyezett paraméterek kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="d8358-146">To check which commands are available for use when you connect to a JEA session, run `Get-Command` and iterate through the results to check for the allowed parameters.</span></span>

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

<span data-ttu-id="d8358-147">Ha C# alkalmazást készít, LÉTREHOZHAT egy JEA-munkamenethez csatlakozó PowerShell-RunSpace egy [WSManConnectionInfo](/dotnet/api/system.management.automation.runspaces.wsmanconnectioninfo) -objektumban található konfigurációs név megadásával.</span><span class="sxs-lookup"><span data-stu-id="d8358-147">If you're building a C# app, you can create a PowerShell runspace that connects to a JEA session by specifying the configuration name in a [WSManConnectionInfo](/dotnet/api/system.management.automation.runspaces.wsmanconnectioninfo) object.</span></span>

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

## <a name="using-jea-with-powershell-direct"></a><span data-ttu-id="d8358-148">A JEA használata a PowerShell Directtel</span><span class="sxs-lookup"><span data-stu-id="d8358-148">Using JEA with PowerShell Direct</span></span>

<span data-ttu-id="d8358-149">A Hyper-V a Windows 10 és a Windows Server 2016 rendszerben a [PowerShell Direct](/virtualization/hyper-v-on-windows/user-guide/powershell-direct)szolgáltatást kínálja, amely lehetővé teszi a Hyper-v-rendszergazdák számára a virtuális gépek kezelését a PowerShell-lel függetlenül a virtuális gép hálózati konfigurációjától vagy távfelügyeleti beállításaitól függetlenül. gép.</span><span class="sxs-lookup"><span data-stu-id="d8358-149">Hyper-V in Windows 10 and Windows Server 2016 offers [PowerShell Direct](/virtualization/hyper-v-on-windows/user-guide/powershell-direct), a feature that allows Hyper-V administrators to manage virtual machines with PowerShell regardless of the network configuration or remote management settings on the virtual machine.</span></span>

<span data-ttu-id="d8358-150">A JEA használatával a PowerShell Directtel engedélyezheti a Hyper-V-rendszergazda számára a virtuális gép elérését.</span><span class="sxs-lookup"><span data-stu-id="d8358-150">You can use PowerShell Direct with JEA to give a Hyper-V administrator limited access to your VM.</span></span>
<span data-ttu-id="d8358-151">Ez akkor lehet hasznos, ha elveszti a hálózati kapcsolatot a virtuális géppel, és szükség van egy adatközpont-rendszergazdára a hálózati beállítások kijavításához.</span><span class="sxs-lookup"><span data-stu-id="d8358-151">This can be useful if you lose network connectivity to your VM and need a datacenter admin to fix the network settings.</span></span>

<span data-ttu-id="d8358-152">A JEA használatához nincs szükség további konfigurációra a PowerShell Direct használatával.</span><span class="sxs-lookup"><span data-stu-id="d8358-152">No additional configuration is required to use JEA over PowerShell Direct.</span></span> <span data-ttu-id="d8358-153">A virtuális gépen futó vendég operációs rendszernek azonban Windows 10, Windows Server 2016 vagy újabb rendszernek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="d8358-153">However, the guest operating system running inside the virtual machine must be Windows 10, Windows Server 2016, or higher.</span></span> <span data-ttu-id="d8358-154">A Hyper-V rendszergazdája a `-VMName` PSRemoting-parancsmagok vagy `-VMId` paraméterek használatával tud csatlakozni az JEA-végponthoz:</span><span class="sxs-lookup"><span data-stu-id="d8358-154">The Hyper-V admin can connect to the JEA endpoint by using the `-VMName` or `-VMId` parameters on PSRemoting cmdlets:</span></span>

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

<span data-ttu-id="d8358-155">Javasoljuk, hogy hozzon létre egy dedikált felhasználói fiókot a rendszer a Hyper-V-rendszergazda általi használatához szükséges minimális jogosultságokkal.</span><span class="sxs-lookup"><span data-stu-id="d8358-155">It's recommended you create a dedicated user account with the minimum rights needed to manage the system for use by a Hyper-V administrator.</span></span> <span data-ttu-id="d8358-156">Ne feledje, hogy még egy nem rendszerjogosultságú felhasználó is bejelentkezhet a Windows rendszerű gépre, például a nem korlátozott PowerShell használatával.</span><span class="sxs-lookup"><span data-stu-id="d8358-156">Remember, even an unprivileged user can sign into a Windows machine by default, including using unconstrained PowerShell.</span></span> <span data-ttu-id="d8358-157">Ez lehetővé teszi számukra, hogy böngésszék a fájlrendszert, és többet tudjon meg az operációs rendszer környezetéről.</span><span class="sxs-lookup"><span data-stu-id="d8358-157">That allows them to browse the file system and learn more about your OS environment.</span></span> <span data-ttu-id="d8358-158">Ha le szeretné zárni a Hyper-V-rendszergazdát, és korlátozni szeretné a virtuális gépeket a JEA-mel közvetlenül a PowerShell közvetlen használatával, meg kell tagadnia a helyi bejelentkezési jogosultságokat a Hyper-V rendszergazdai JEA fiókjához.</span><span class="sxs-lookup"><span data-stu-id="d8358-158">To lock down a Hyper-V administrator and limit them to only access a VM using PowerShell Direct with JEA, you must deny local logon rights to the Hyper-V admin's JEA account.</span></span>
