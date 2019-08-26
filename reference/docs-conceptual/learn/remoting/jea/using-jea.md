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
# <a name="using-jea"></a>A JEA használata

Ez a cikk ismerteti a JEA-végpontokhoz való kapcsolódás különböző módszereit és használatát.

## <a name="using-jea-interactively"></a>A JEA interaktív használata

Ha teszteli a JEA-konfigurációt, vagy egyszerű feladatokat használ a felhasználók számára, ugyanúgy használhatja a JEA-t, mint egy hagyományos PowerShell-távelérési munkamenetet. Az összetett távelérési feladatok esetében ajánlott az [implicit távelérés](#using-jea-with-implicit-remoting)használata. Az implicit távelérés lehetővé teszi, hogy a felhasználók helyileg működjenek együtt az adatobjektumokkal.

A JEA interaktív használatához a következőkre lesz szüksége:

- Annak a számítógépnek a neve, amelyhez csatlakozik (a helyi gép lehet)
- A számítógépen regisztrált JEA-végpont neve
- A számítógépen található JEA-végponthoz hozzáféréssel rendelkező hitelesítő adatok

Ezen információk alapján elindíthat egy JEA-munkamenetet a [New-PSSession](/powershell/module/microsoft.powershell.core/New-PSSession) vagy a [ENTER-PSSession](/powershell/module/microsoft.powershell.core/enter-pssession) parancsmaggal.

```powershell
$nonAdminCred = Get-Credential
Enter-PSSession -ComputerName localhost -ConfigurationName JEAMaintenance -Credential $nonAdminCred
```

Ha az aktuális felhasználói fiók rendelkezik hozzáféréssel az JEA-végponthoz, kihagyhatja a **hitelesítő adat** paramétert.

Amikor a PowerShell felszólítja `[localhost]: PS>` , hogy tudja, hogy most már együttműködik a távoli JEA-munkamenettel. A futtatásával `Get-Command` ellenőrizhető, hogy mely parancsok érhetők el. Forduljon a rendszergazdához, és Ismerje meg, hogy van-e korlátozás az elérhető paraméterekkel vagy az engedélyezett paraméterek értékeivel kapcsolatban.

Ne feledje, hogy a JEA-munkamenetek nem nyelvi módban működnek. Előfordulhat, hogy a PowerShell használatának néhány módja nem érhető el. Például nem használhat változókat adatok tárolására, vagy megvizsgálhatja a parancsmagokból visszaadott objektumok tulajdonságait. Az alábbi példa két módszert mutat be, amelyekkel ugyanazokat a parancsokat lehet a nem nyelvi módban dolgozni.

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

Az ezt a megközelítést megnehezíti, összetettebb parancs-hívásokhoz használjon [implicit távelérést](#using-jea-with-implicit-remoting) , vagy [hozzon létre olyan egyéni függvényeket](role-capabilities.md#creating-custom-functions) , amelyek betakarják a szükséges funkciókat.

## <a name="using-jea-with-implicit-remoting"></a>JEA használata implicit táveléréssel

A PowerShell implicit távelérési modellel rendelkezik, amely lehetővé teszi a proxy-parancsmagok távoli gépről történő importálását, és a velük való interakciót, mintha helyi parancsok lennének. Az implicit távelérést ebben a **Hey, Scripting Guy** -ban ismertetjük. [blogbejegyzés](https://devblogs.microsoft.com/scripting/remoting-the-implicit-way/).
Az implicit távelérés akkor hasznos, ha a JEA dolgozik, mivel lehetővé teszi a JEA-parancsmagok teljes nyelvi módban való használatát. Használhatja a TAB-kiegészítést, a változókat, az objektumok módosítását, és akár helyi parancsfájlokat is használhat a JEA-végpontra irányuló feladatok automatizálásához. A proxy parancs meghívása után az adatküldés a távoli gépen található JEA-végpontra történik, és ott hajtja végre.

Az implicit távelérés úgy működik, hogy parancsmagokat importál egy meglévő PowerShell-munkamenetből. Opcionálisan megadhatja, hogy az egyes proxy-parancsmagok neve előtaggal legyen elválasztva. Az előtag lehetővé teszi a távoli rendszerhez tartozó parancsok megkülönböztetését. A rendszer az összes proxy parancsot tartalmazó ideiglenes parancsfájl-modult hozza létre és importálja a helyi PowerShell-munkamenet időtartama alatt.

```powershell
# Create a new PSSession to your JEA endpoint
$jeasession = New-PSSession -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance'

# Import the entire PSSession and prefix each imported cmdlet with "JEA"
Import-PSSession -Session $jeasession -Prefix 'JEA'

# Invoke "Get-Command" on the remote JEA endpoint using the proxy cmdlet
Get-JEACommand
```

> [!IMPORTANT]
> Előfordulhat, hogy egyes rendszerek nem tudnak teljes JEA-munkamenetet importálni az alapértelmezett JEA-parancsmagok korlátai miatt. Ennek megkezdéséhez csak a szükséges parancsokat kell importálnia a JEA-munkamenetből, ha explicit módon megadja nevüket `-CommandName` a paraméternek. A jövőbeli frissítések a teljes JEA-munkamenetek importálásával foglalkoznak az érintett rendszereken.

Ha nem tudja importálni a JEA-munkamenetet az alapértelmezett paraméterek JEA megkötése miatt, kövesse az alábbi lépéseket az importált készlet alapértelmezett parancsainak kiszűréséhez. Továbbra is használhatja az olyan `Select-Object`parancsokat, mint a, de a távoli JEA-munkamenetből importált helyett csak a számítógépen telepített helyi verziót fogja használni.

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

Az [export-PSSession](/powershell/microsoft.powershell.utility/Export-PSSession)használatával is megtarthatja a proxyn belüli parancsmagokat az implicit távelérésből.
Az implicit távoli eljáráshívás szolgáltatással kapcsolatos további információkért tekintse meg az [import-PSSession](/powershell/microsoft.powershell.utility/import-pssession) és az [import-Module](/powershell/microsoft.powershell.core/import-module)dokumentációját.

## <a name="using-jea-programmatically"></a>A JEA programozott módon történő használata

A JEA automatizálási rendszerekben és felhasználói alkalmazásokban is használhatók, például a házon belüli segélyszolgálat alkalmazásaiban és webhelyein. A módszer ugyanaz, mint a nem korlátozott PowerShell-végpontokkal kommunikáló alkalmazások létrehozásához. Győződjön meg arról, hogy a program úgy van kialakítva, hogy a JEA által megszabott korlátozásokkal működjön.

Egyszerű, egyszeri feladatokhoz használhatja a Meghívási [parancsot](/powershell/module/microsoft.powershell.core/invoke-command) a JEA-munkamenetben lévő parancsok futtatásához.

```powershell
Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Process; Get-Service }
```

A JEA-munkamenethez való csatlakozáskor használható parancsok megadásához futtassa `Get-Command` a parancsot, és ismételje meg az eredményeket az engedélyezett paraméterek kereséséhez.

```powershell
$allowedCommands = Invoke-Command -ComputerName 'SERVER01' -ConfigurationName 'JEAMaintenance' -ScriptBlock { Get-Command }
$allowedCommands | Where-Object { $_.CommandType -in 'Function', 'Cmdlet' } | Format-Table Name, Parameters
```

Ha C# alkalmazást készít, LÉTREHOZHAT egy JEA-munkamenethez csatlakozó PowerShell-RunSpace egy [WSManConnectionInfo](/dotnet/api/system.management.automation.runspaces.wsmanconnectioninfo) -objektumban található konfigurációs név megadásával.

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

## <a name="using-jea-with-powershell-direct"></a>A JEA használata a PowerShell Directtel

A Hyper-V a Windows 10 és a Windows Server 2016 rendszerben a [PowerShell Direct](/virtualization/hyper-v-on-windows/user-guide/powershell-direct)szolgáltatást kínálja, amely lehetővé teszi a Hyper-v-rendszergazdák számára a virtuális gépek kezelését a PowerShell-lel függetlenül a virtuális gép hálózati konfigurációjától vagy távfelügyeleti beállításaitól függetlenül. gép.

A JEA használatával a PowerShell Directtel engedélyezheti a Hyper-V-rendszergazda számára a virtuális gép elérését.
Ez akkor lehet hasznos, ha elveszti a hálózati kapcsolatot a virtuális géppel, és szükség van egy adatközpont-rendszergazdára a hálózati beállítások kijavításához.

A JEA használatához nincs szükség további konfigurációra a PowerShell Direct használatával. A virtuális gépen futó vendég operációs rendszernek azonban Windows 10, Windows Server 2016 vagy újabb rendszernek kell lennie. A Hyper-V rendszergazdája a `-VMName` PSRemoting-parancsmagok vagy `-VMId` paraméterek használatával tud csatlakozni az JEA-végponthoz:

```powershell
# Entering a JEA session using PowerShell Direct when the VM name is unique
Enter-PSSession -VMName 'SQL01' -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'

# Entering a JEA session using PowerShell Direct using VM ids
$vm = Get-VM -VMName 'MyVM' | Select-Object -First 1
Enter-PSSession -VMId $vm.VMId -ConfigurationName 'NICMaintenance' -Credential 'localhost\JEAformyHoster'
```

Javasoljuk, hogy hozzon létre egy dedikált felhasználói fiókot a rendszer a Hyper-V-rendszergazda általi használatához szükséges minimális jogosultságokkal. Ne feledje, hogy még egy nem rendszerjogosultságú felhasználó is bejelentkezhet a Windows rendszerű gépre, például a nem korlátozott PowerShell használatával. Ez lehetővé teszi számukra, hogy böngésszék a fájlrendszert, és többet tudjon meg az operációs rendszer környezetéről. Ha le szeretné zárni a Hyper-V-rendszergazdát, és korlátozni szeretné a virtuális gépeket a JEA-mel közvetlenül a PowerShell közvetlen használatával, meg kell tagadnia a helyi bejelentkezési jogosultságokat a Hyper-V rendszergazdai JEA fiókjához.
