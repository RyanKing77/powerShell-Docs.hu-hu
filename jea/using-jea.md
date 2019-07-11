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
# <a name="using-jea"></a>A JEA használata

Ez a cikk ismerteti a különböző módokon csatlakozhat, és a JEA-végpont használata.

## <a name="using-jea-interactively"></a>A JEA interaktív használata

Ha a JEA-konfiguráció tesztel, vagy rendelkezik az egyszerű feladatokat a felhasználók számára, használhatja a normál PowerShell távoli eljáráshívás munkamenet ugyanúgy JEA. Összetett távoli eljáráshívás feladatokhoz, azt javasoljuk, hogy használjon [implicit távelérési](#using-jea-with-implicit-remoting). Implicit távelérési lehetővé teszi a felhasználóknak az adatobjektumok helyileg kapnak.

A JEA interaktív használatához az alábbiak szükségesek:

- A számítógép, amelyhez csatlakozik a nevét (a helyi gép is lehet)
- A regisztrált ezen a számítógépen a JEA-végpont neve
- Hitelesítő adatokat, amelyek a JEA-végpont a hozzáférést az adott számítógépen

Adja meg ezt az információt, megkezdheti a JEA munkamenet a [New-PSSession](/powershell/module/microsoft.powershell.core/New-PSSession) vagy [Enter-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) parancsmagok.

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

Ha az aktuális felhasználói fiók hozzáfér a JEA-végpont, kihagyhatja a **Credential** paraméter.

Ha a PowerShell kérni a módosítások `[localhost]: PS>` tudja, hogy Ön már műveleteket végeznek a JEA távoli munkamenet. Futtathat `Get-Command` ellenőrizze a rendelkezésre álló parancsokat. Kérje a rendszergazdát, hogy ismerje meg, hogy vannak-e a paramétereket, vagy engedélyezett értékei korlátozások.

Ne feledje, hogy a JEA-munkamenetek NoLanguage módban működik. Általában a powershellel több szempontból nem lehet érhető el. Például az adatok tárolására, vagy vizsgálja meg a parancsmag által visszaadott objektumok tulajdonságainak változók nem használhatók. Az alábbi példa bemutatja a két megközelítés ugyanazokat a parancsokat NoLanguage módban való működésre beolvasásához.

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

Az összetettebb parancs meghívásához, amelyek megnehezítik a ezt a módszert, fontolja meg [implicit távelérési](#using-jea-with-implicit-remoting) vagy [egyéni funkciók létrehozásával](role-capabilities.md#creating-custom-functions) , amely burkolhatja a funkciókra van szüksége.

## <a name="using-jea-with-implicit-remoting"></a>Implicit távelérési JEA használata

PowerShell-implicit távelérési modell, amely lehetővé teszi a webalkalmazásproxy-parancsmagok importálásához egy távoli számítógépről, és dolgozhat velük, mintha helyi parancsokat tartalmaz. A jelen kifejtett implicit távelérési **Hey, Scripting Guy!** [blogbejegyzés](https://devblogs.microsoft.com/scripting/remoting-the-implicit-way/).
Implicit távelérési akkor hasznos, ha a JEA használata, mert lehetővé teszi, hogy a JEA-parancsmagok teljes nyelvi üzemmódban. Kiegészítés, a változók használata, objektumok módosítását, és akár a helyi parancsprogramok használatával automatizálhatja a feladatokat a JEA-végpont. Visszaállít egy proxy parancsot indít el, az adatok a távoli gépen a JEA-végpont fogadja és ott hajtja végre.

Implicit távelérési parancsmagok importál egy meglévő PowerShell-munkamenetet úgy működik. Igény szerint kiválaszthatja előtagot megkereshetők a főnevek minden proxy parancsmag egy tetszőleges karakterláncra. Az előtag lehetővé teszi a távoli rendszer parancsok megkülönböztetéséhez. A proxy-parancsok tartalmazó ideiglenes parancsfájl modul létrejött, és importálja a helyi PowerShell-munkamenetben időtartamára.

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> Egyes rendszerek nem lehet képes importálni a alapértelmezett JEA parancsmagok megkötések miatt egy teljes JEA-munkamenetet. Ennek elkerülése érdekében, az importálás kizárólag a szükséges parancsokat a JEA-munkamenet azáltal, hogy explicit módon a nevük a `-CommandName` paraméter. Egy következő frissítés fogja oldja meg az érintett rendszerek teljes JEA-munkamenetek importálásával kapcsolatos hiba.

Ha Ön nem lehet importálni a JEA-munkamenet alapértelmezett paramétereihez JEA korlátozások miatt, kövesse az alábbi lépéseket az alapértelmezett parancsok közül az importált szűréséhez. Továbbra is használható parancsok, például `Select-Object`, azonban csak a helyi verziója helyett a JEA távoli munkamenet importált egy számítógépre telepített fogja használni.

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

A proxy parancsmagok implicit távelérési használatával is megőrizheti [Export-PSSession](/powershell/microsoft.powershell.utility/Export-PSSession).
Implicit távelérési kapcsolatos további információkért lásd a dokumentációban [Import-PSSession](/powershell/microsoft.powershell.utility/import-pssession) és [Import-Module](/powershell/microsoft.powershell.core/import-module).

## <a name="using-jea-programmatically"></a>Programozott módon a JEA használata

A JEA is használható, az automatizálási rendszer és a felhasználói alkalmazásokban, például a segélyszolgálat belső fejlesztésű alkalmazásokat és webhelyeket. A módszer ugyanaz, mint amellyel korlátozás PowerShell végpontok kommunikálhatnak alkalmazások készítéséhez. Győződjön meg arról, a program célja által a JEA használata.

Egyszerű, egyszeri feladatokhoz használhatja [Invoke-Command](/powershell/module/microsoft.powershell.core/invoke-command) JEA munkamenet-parancsok futtatásához.

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

Ellenőrizze, hogy mely parancsok állnak rendelkezésre, amikor csatlakozik a JEA-munkamenet, futtassa a `Get-Command` közzétételt és iterációt az eredmények ellenőrzése az engedélyezett paraméterek között.

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

Ha készít egy C# alkalmazást, létrehozhat egy PowerShell futási teret, amely kapcsolódik a JEA-munkamenet megadásával a konfiguráció nevét a egy [WSManConnectionInfo](/dotnet/api/system.management.automation.runspaces.wsmanconnectioninfo) objektum.

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

## <a name="using-jea-with-powershell-direct"></a>A JEA használata a PowerShell Direct használatával

A Windows 10 és Windows Server 2016 Hyper-V kínál [PowerShell Directet](/virtualization/hyper-v-on-windows/user-guide/powershell-direct), lehetővé teszi, hogy a Hyper-V rendszergazdák, függetlenül a hálózati konfiguráció vagy a távoli felügyelet a PowerShell használatával a virtuális gépek kezeléséhez a virtuális gép beállításait.

A JEA PowerShell Direct használatával egy Hyper-V korlátozott rendszergazdai hozzáférést biztosíthat a virtuális gép.
Ez hasznos lehet, ha a virtuális gép hálózati kapcsolatát, és egy adatközpont-rendszergazdát, hogy javítsa a hálózati beállításokat.

A JEA használata a PowerShell directtel szükséges további konfiguráció nélkül. Azonban a vendég operációs rendszer a virtuális gépen futó Windows 10, Windows Server 2016 vagy újabb kell lennie. A Hyper-V-rendszergazda segítségével csatlakoztathatók a JEA-végpont a `-VMName` vagy `-VMId` PSRemoting parancsmagok a paramétereket:

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

Javasoljuk egy dedikált felhasználói fiókot hoz létre a Hyper-V rendszergazda kezelésére használható a rendszer szükséges minimális jogokkal. Ne feledje, hogy még egy nem rendszerjogosultságú felhasználói egy Windows-számítógép be tud jelentkezni az alapértelmezés szerint, beleértve a korlátozás PowerShell használatával. Amely lehetővé teszi számukra, hogy a fájlrendszer tallózása és további információ az operációs rendszer környezetében. A Hyper-V-rendszergazdák zárolását, és korlátozhatja a azokat csak a virtuális gép PowerShell Direct használatával a JEA eléréséhez, megtagadja a helyi bejelentkezési jogosultságai a Hyper-V-rendszergazda a JEA-fiókhoz.
