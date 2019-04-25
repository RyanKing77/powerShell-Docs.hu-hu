---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: A JEA használata
ms.openlocfilehash: fa3d3a3c8bc0090ec9ad788585ec5df933134173
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084045"
---
# <a name="using-jea"></a>A JEA használata

> Érintett kiadások: Windows PowerShell 5.0

Ez a témakör ismerteti a különböző módokon csatlakozhat, és a JEA-végpont használata.

## <a name="using-jea-interactively"></a>A JEA interaktív használata

Ha teszteli a JEA-konfiguráció vagy egyszerű feladatok végrehajtásához a felhasználók számára, használhatja a normál PowerShell távoli eljáráshívás munkamenet ugyanúgy JEA.
Összetett távoli eljáráshívás feladatokhoz, javasoljuk, hogy használjon [implicit távelérési](#using-jea-with-implicit-remoting) inkább hogy egyszerűbb legyen a felhasználók számára azáltal, hogy megfelelően működjenek a felhasználók az adatobjektumok helyileg.

A JEA interaktív használatához szüksége lesz:
- A számítógép kapcsolódik a nevét (a helyi gép is lehet)
- A regisztrált ezen a számítógépen a JEA-végpont neve
- Hitelesítő adatok a számítógép, amelyhez hozzáférése a JEA-végpont

Az aktuális adatnak megkezdheti a JEA munkamenet [New-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/New-PSSession) vagy [Enter-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enter-pssession).

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

Ha a fiók van jelenleg bejelentkezve szerint a JEA-végpont hozzáféréssel rendelkezik, akkor kihagyhatja a `-Credential` paraméter.

Ha a PowerShell kérni a módosítások `[localhost]: PS>` , hogy most már használja a távoli munkamenetet a JEA-tudni fogja.
Futtathat `Get-Command` ellenőrizze a rendelkezésre álló parancsokat.
Tekintse meg a rendszergazdát, ismerje meg, ha a rendelkezésre álló paraméterek vagy a megengedett értékei korlátozások kell.

Ne feledje a JEA-munkamenetek módban működik NoLanguage, ezért általában a powershellel több szempontból nem érhető el.
Például az adatok tárolására, vagy vizsgálja meg a parancsmag által visszaadott objektumok tulajdonságainak változók nem használhatók.
Az alábbi példa mutat egy példát, előfordulhat, hogy a PowerShell még ma, és azonos első két módszer parancs NoLanguage módban működik.

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

Az összetettebb parancs meghívásához, amelyek megnehezítik a ezt a módszert, fontolja meg [implicit távelérési](#using-jea-with-implicit-remoting) vagy [egyéni funkciók létrehozásával](role-capabilities.md#creating-custom-functions) , amely burkolása az a Funkciók, amennyit csak szeretne.

## <a name="using-jea-with-implicit-remoting"></a>Implicit távelérési JEA használata

PowerShell-alternatív távoli eljáráshívás modell, ahol webalkalmazásproxy-parancsmagok importálásához egy távoli számítógépről a helyi számítógépen, és dolgozhat velük, mintha helyi parancsok támogatja.
Ez implicit távelérési nevezzük, és és kifejtett [ez *Hey, Scripting Guy!* blogbejegyzés](https://blogs.technet.microsoft.com/heyscriptingguy/2013/09/08/remoting-the-implicit-way/).
Implicit távelérési különösen hasznos, ha JEA dolgozik, mivel lehetővé teszi a JEA-parancsmagok teljes nyelvi üzemmódban működik.
Ez azt jelenti, kiegészítés, a változók használata, objektumok módosítását, és helyi parancsfájlok használatával könnyebben automatizálhatja a JEA-végponton.
Visszaállít egy proxy parancsot indít el, az adatokat küldeni a JEA-végpont a távoli számítógépen, és ott hajtja végre.

Implicit távelérési parancsmagok importál egy meglévő PowerShell-munkamenetet úgy működik.
Igény szerint kiválaszthatja megkereshetők a főnevek minden proxy parancsmag egy karakterlánccal megszakíthatja a távoli rendszer parancsai megkülönböztetni előtagot.
Egy ideiglenes szkriptmodulba tartalmazó összes proxy parancsot jön létre, és használhatja a helyi PowerShell-munkamenet időtartamát.

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> Egyes rendszerek nem lehet képes importálni a alapértelmezett JEA parancsmagok megkötések miatt egy teljes JEA-munkamenetet.
> Ennek elkerülése érdekében, az importálás kizárólag a szükséges parancsokat a JEA-munkamenet azáltal, hogy explicit módon a nevük a `-CommandName` paraméter.
> Egy következő frissítés fogja oldja meg az érintett rendszerek teljes JEA-munkamenetek importálásával kapcsolatos hiba.

Ha Ön nem lehet importálni a JEA munkamenet alapértelmezett JEA paraméterek korlátai miatt, követheti a szűrje ki az importált beállítása a alapértelmezett parancsokat az alábbi lépéseket.
Ön továbbra is képesek lesznek parancsok, például `Select-Object` – csak fogja használni a távoli egy, a JEA-munkamenet helyett a számítógépre telepített helyi verziója.

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

A proxy parancsmagok implicit távelérési használatával is megőrizheti [Export-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/Export-PSSession).
Implicit távelérési kapcsolatos további információkért tekintse meg a Súgó dokumentációját [Import-PSSession](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.utility/import-pssession) és [Import-Module](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/import-module).

## <a name="using-jea-programmatically"></a>Programozott módon a JEA használata

A JEA is használható, az automatizálási rendszer és a felhasználói alkalmazásokban, például a segélyszolgálat belső fejlesztésű alkalmazásokat és webhelyeket.
A módszer megegyezik, az alkalmazások létrehozásához, amely kommunikációhoz korlátozás PowerShell-végpontokra, hogy a program érdemes figyelembe venni, hogy a JEA korlátozná a távoli munkamenet futtatott parancsok csoportosítani.

Egyszerű, egyszeri feladatokhoz használhatja [Invoke-Command](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/invoke-command) a JEA használata parancsok futtatására.

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

Ellenőrizze, hogy mely parancsok állnak rendelkezésre, amikor csatlakozik a JEA-munkamenet, futtassa a `Get-Command` közzétételt és iterációt az eredmények ellenőrzése az engedélyezett paraméterek között.

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

Ha egy C# alkalmazást, létrehozhat egy PowerShell futási teret, amely kapcsolódik a JEA-munkamenet megadásával a konfiguráció nevét a egy [WSManConnectionInfo](https://msdn.microsoft.com/library/system.management.automation.runspaces.wsmanconnectioninfo(v=vs.85).aspx) objektum.

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

## <a name="using-jea-with-powershell-direct"></a>A JEA használata a PowerShell Direct használatával

A Windows 10 és Windows Server 2016 Hyper-V kínál [PowerShell Directet](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/vmsession), egy szolgáltatást, amely lehetővé teszi, hogy a Hyper-V rendszergazdák, függetlenül a hálózati konfiguráció vagy a távoli felügyelet a PowerShell használatával a virtuális gépek kezeléséhez a virtuális gép beállításait.

A JEA PowerShell Direct használatával egy Hyper-V korlátozott rendszergazdai hozzáférést biztosíthat a virtuális gép, amely lehet hasznos, ha a virtuális gép hálózati kapcsolatát, és a egy adatközpont-felügyeleti el kell hárítania a hálózati beállításokat.

További konfiguráció nélkül nem szükséges a JEA használata a PowerShell directtel, azonban lehet, hogy a virtuális gépen futó operációs rendszer Windows 10-es vagy Windows Server 2016-ban.
A Hyper-V-rendszergazda segítségével csatlakoztathatók a JEA-végpont a `-VMName` vagy `-VMId` PSRemoting parancsmagok a paramétereket:

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

Erősen ajánlott, hogy hoz létre egy dedikált helyi felhasználót a rendszer a Hyper-V-rendszergazdáknak használata kezelheti semmilyen egyéb jog.
Ne feledje, hogy még egy nem rendszerjogosultságú felhasználói továbbra is be tud jelentkezni a Windows-gépek alapértelmezés szerint, beleértve a korlátozás PowerShell használatával.
Amely lehetővé teszi számukra (néhány) keresse meg a fájlrendszer és a további információ az operációs rendszer környezetében.
Egy Hyper-V-rendszergazdát, hogy csakis azokhoz a virtuális gép PowerShell Direct használatával a JEA zárolhat, szüksége lesz megtagadása helyi bejelentkezési jogosultságai a Hyper-V-rendszergazda a JEA-fiókhoz.
