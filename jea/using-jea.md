---
ms.date: 06/12/2017
author: rpsqrd
ms.topic: conceptual
keywords: jea, a powershell, a biztonsági
title: A JEA használata
ms.openlocfilehash: 8a6fb2682cf82de8dd20a8699178d4abde4954c2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="using-jea"></a>A JEA használata

> A következőkre vonatkozik: a Windows PowerShell 5.0

Ez a témakör ismerteti a különböző módokon csatlakozhat, és használja a JEA végpontot.

## <a name="using-jea-interactively"></a>JEA interaktív futtatása

Ha teszteli az JEA konfigurációját, vagy vannak-e egyszerű feladatok felhasználók számára, használhatja a rendszeres PowerShell távoli eljáráshívás munkamenet ugyanúgy JEA.
Összetett távelérése feladatokhoz, javasoljuk, hogy használjon [implicit távoli eljáráshívás](#using-jea-with-implicit-remoting) helyette számára megkönnyíti a felhasználók által a felhasználók kapnak az adatok objektumokat helyileg.

A JEA interaktív használatához szüksége lesz:
- A számítógép csatlakozik a nevét (a helyi számítógépen is lehet)
- A JEA-végpont a számítógépen regisztrált neve
- A számítógép hitelesítő adatainak a JEA végpontot elérő

Az aktuális adatnak, megkezdheti a JEA munkamenet [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) vagy [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

Ha a fiók jelenleg jelentkezett be, ha a JEA végponthoz való hozzáférést, akkor kihagyhatja a `-Credential` paraméter.

Amikor a PowerShell kérni módosításai `[localhost]: PS>` megtudják, hogy most interakció a távoli JEA-munkamenet.
Futtathat `Get-Command` , mely parancsok elérhető.
Szüksége lesz a rendszergazdát, hogy ismerje meg, ha a rendelkezésre álló paramétereket vagy megengedett értékei korlátozások vegye fel a kapcsolatot.

Ne feledje JEA munkamenetek üzemmódban működjenek NoLanguage, ezért néhány módot általában a PowerShellben nem érhető el.
Például adatok tárolására, vagy vizsgálja meg a parancsmagok által visszaadott objektumok tulajdonságainak változók nem használhatók.
Az alábbi példa azt mutatja meg, például hogy miként lehet használhat PowerShell ma, és ugyanazt a beolvasandó két megközelítés parancs NoLanguage módban működik.

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

Az összetettebb parancs-indítások megnehezítik ezt a módszert használja, érdemes lehet [implicit távoli eljáráshívás](#using-jea-with-implicit-remoting) vagy [egyéni függvények létrehozása](role-capabilities.md#creating-custom-functions) , amely a kívánt funkció burkolja.

## <a name="using-jea-with-implicit-remoting"></a>Implicit távelérése JEA használata

PowerShell ahol webalkalmazásproxy-parancsmagok importálásához egy távoli számítógépről a helyi számítógépen, és kezelheti azokat helyi parancsok, mintha egy alternatív távelérése modellt támogatja.
Ez implicit távelérése nevezik, és esetén, tekintse meg a helyes [ez *Hey, Scripting Guy!* blogbejegyzés](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).
Implicit távoli eljáráshívási akkor különösen hasznos, ha olyan JEA, mert lehetővé teszi a JEA-parancsmaggal egy teljes nyelvi módban működik.
Ez azt jelenti, hogy kiegészítés, a változók használata, módosíthat objektumokat, és még a helyi parancsfájlok használatával könnyebben automatizálhatja a JEA végpont ellen.
A proxy-utasítás hívása, bármikor az adatokat elküldi a JEA végpontnak a távoli számítógépen, és ott hajtja végre.

Implicit távelérési parancsmagok importálása egy meglévő PowerShell-munkamenetet úgy működik.
Kiválaszthatja a parancsokat minden egyes proxy parancsmag segítségével különböztetheti meg egymástól, mely parancsok vannak a távoli rendszer kiválasztása a karakterláncot előtag nem kötelező.
Egy ideiglenes szkriptmodulba tartalmazó összes proxy parancs létrehozza, és a helyi PowerShell-munkamenet időtartama alatt is használható.

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> Előfordulhat, hogy egyes rendszerek nem importálni egy teljes JEA-munkamenet az alapértelmezett JEA parancsmagokban korlátok miatt.
> Ennek elkerülése érdekében, csak akkor importálja a szükséges parancsokat a JEA-munkamenetből, explicit módon adja meg a saját nevét a `-CommandName` paraméter.
> Egy következő frissítés megoldja a teljes JEA munkamenetek érintett rendszerek importálása.

Ha nem tudja importálni a JEA-munkamenet alapértelmezett JEA paramétereknek vonatkozó korlátozások miatt, követheti az alábbi lépéseket az alapértelmezett parancsok az importált készletből kiszűrésére.
Továbbra is fogja tudni használni a parancsok például `Select-Object` – csak a helyi távoli helyett a JEA-munkamenetben a számítógépre telepített verzió fogja használni.

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

Megőrizni a implicit távoli eljáráshívás segítségével a proxy parancsmagjait [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).
Implicit távelérése kapcsolatos további információkért tekintse meg a Súgó dokumentációját [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) és [Import-Module](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/import-module).

## <a name="using-jea-programatically"></a>JEA programozottan használatával

JEA is használható, az automatizálási rendszerek és felhasználói alkalmazásokban, például a belső fejlesztésű támogató alkalmazások és a webhelyek.
A megoldás, azonos módon, amely alkalmazások készítéséhez, amely kommunikálni, korlátozás nélküli PowerShell végpontokhoz, hogy a program kell vegye figyelembe, hogy JEA korlátozza-e a távoli munkamenet futtatott parancsok szerint.

Egyszerű, egyszeri feladatokhoz használhatja [Invoke-Command](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/invoke-command) JEA használatával parancsok futtatásához.

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

Ellenőrizze, hogy mely parancsok állnak rendelkezésre, amikor csatlakozik egy JEA munkamenet, futtassa a `Get-Command` és iterációt az eredmények a megengedett paraméterek kereséséhez.

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

Ha egy C# alkalmazást fejleszt, a PowerShell futási térből, amely összeköti a JEA munkamenet lévő megadásával hozhat létre egy [WSManConnectionInfo](https://msdn.microsoft.com/en-us/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) objektum.

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

## <a name="using-jea-with-powershell-direct"></a>PowerShell közvetlen JEA használatával

Hyper-V a Windows 10 és Windows Server 2016 kínál [PowerShell közvetlen](https://msdn.microsoft.com/en-us/virtualization/hyperv_on_windows/user_guide/vmsession), egy szolgáltatás, amely lehetővé teszi, hogy a Hyper-V rendszergazdák, függetlenül a hálózati konfiguráció vagy a távoli felügyelet a PowerShell segítségével a virtuális gépek kezeléséhez a virtuális gép beállításait.

PowerShell közvetlen JEA biztosítanak a Hyper-V korlátozott rendszergazdai hozzáférés a virtuális Gépet, amely lehet hasznos, ha megszakad a hálózati kapcsolat a virtuális gépre, és hárítsa el a hálózati beállításokat kell egy adatközpont-felügyeleti használható.

Nincs további beállításokat kell megadnia PowerShell közvetlen keresztül használja a JEA, azonban a virtuális gépen futó operációs rendszer kell lennie a Windows 10 vagy Windows Server 2016.
A Hyper-V felügyeleti használatával csatlakozhat a JEA végpont a `-VMName` vagy `-VMId` PSRemoting parancsmagok paraméterek:

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

Erősen ajánlott, hogy hozzon létre egy dedikált helyi felhasználói jogosultságokkal nincs más kezelheti a Hyper-V rendszergazdák számára, hogy a rendszer.
Ne feledje, hogy még nem rendszerjogosultságú felhasználói továbbra is be tud jelentkezni egy Windows-számítógép alapértelmezés, beleértve a korlátozás nélküli PowerShell használatával.
Amely lehetővé teszi (néhány) keresse meg a fájlrendszer és a további tudnivalók az operációs rendszer környezetében.
A Hyper-V rendszergazdák is képesek csak akkor férhessenek hozzá a virtuális gépek PowerShell közvetlenül a JEA zárolását, szüksége lesz a Hyper-V rendszergazdai JEA fiókot a helyi bejelentkezési jogokkal megtagadása.