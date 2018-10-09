---
ms.date: 06/12/2017
keywords: a jea, powershell, biztonsági
title: Naplózás és a JEA-jelentések
ms.openlocfilehash: 2388c735840d8d3683aa8bc9869b9fb0371e5902
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851220"
---
# <a name="auditing-and-reporting-on-jea"></a>Naplózás és a JEA-jelentések

> A következőkre vonatkozik: Windows PowerShell 5.0

Miután telepítette a JEA, célszerű rendszeresen naplózása a JEA-konfigurációt.
Ez segít mérje fel, ha a megfelelő személyeknek fér hozzá a JEA-végpont, és a hozzárendelt szerepkörök továbbra is megfelelőek.

Ez a témakör ismerteti a különböző módszereket a JEA-végpont naplózhatók.

## <a name="find-registered-jea-sessions-on-a-machine"></a>Keresse meg a regisztrált JEA munkamenetek gépen

Ellenőrizze, hogy mely JEA munkamenetek gépen regisztrált, használja a [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) parancsmagot.

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
PS C:\> Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }


Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed, CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

A hatékony jogok a végpont a "Engedély" tulajdonság szerepel.
Ezek a felhasználók jogosult csatlakozni a JEA-végpont, de mely szerepkörök (és, parancsok) határozza meg a "RoleDefinitions" mezője hozzáféréssel rendelkeznek a [munkamenet konfigurációs fájl](session-configurations.md) regisztrálásához használt a a végpont.

Az adatok a "RoleDefinitions" tulajdonságban kibontásával kiértékelheti egy regisztrált a JEA-végpont a szerepkör-hozzárendelések.

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{ Name = 'Role Capabilities'; Expression = { $_.Value.RoleCapabilities } }
```

## <a name="find-available-role-capabilities-on-the-machine"></a>A gépen elérhető szerepköri funkciók keresése

Szerepkör képesség fájlok csak által használandó JEA belül egy érvényes PowerShell-modul egy "RoleCapabilities" mappában vannak tárolva.
A számítógépen elérhető összes szerepköri funkciók az elérhető modulok listáját kereséssel találhatja meg.

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
> Ez a függvény eredményeinek sorrendje nem feltétlenül a sorrend, amelyben a szerepkörrel képességeket lesz kiválasztva, ha több szerepkörrel képességeket rendelkezik ugyanazzal a névvel.

## <a name="check-effective-rights-for-a-specific-user"></a>Egy adott felhasználó hatékony jogok ellenőrzése

A JEA-végpont beállítása után érdemes ellenőrizni a JEA munkamenetben egy adott felhasználó számára rendelkezésre álló parancsokat.
Használhat [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) számbavétele az összes alkalmazható egy felhasználó számára a parancsok, mintha azok az aktuális csoporttagságok JEA munkamenet indításához.
A kimenet a `Get-PSSessionCapability` megegyezik-e a megadott futtató felhasználó `Get-Command -CommandType All` JEA munkamenetben.

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

Ha a felhasználók nem lenne jogosultságokat őket további JEA csoportokat állandó tagjai, ez a parancsmag nem tükrözik az extra engedélyeket.
Általában ez a helyzet, just-in-time privileged access management systems használatakor a felhasználók ideiglenesen biztonsági csoporthoz tartozik.
Mindig gondosan határozza meg a felhasználók szerepkörökhöz hozzárendelését és a felhasználók csak kihozhatják a parancsok a munkájuk sikeres elvégzéséhez szükséges lehető legkevesebb való hozzáférés biztosítása érdekében szerepkörönként tartalmát.

## <a name="powershell-event-logs"></a>PowerShell-eseménynaplók

Ha engedélyezte a rendszer a bejelentkezés modul és/vagy parancsfájl letiltása, lesz a Windows eseménynaplóiban keresse az egyes parancsok a JEA munkamenetekhez, futtatott egy felhasználó események található.
Ezek az események megkereséséhez nyissa meg a Windows eseménynaplót, keresse meg a **Microsoft-Windows-PowerShell/műveleti** eseménynaplót, és keresse meg az események event ID **4104**.

Minden eseménynapló-bejegyzést, amelyben a parancs futtatása a munkamenet vonatkozó információk is.
JEA-munkamenetet, ez kiterjed a fontos információk a **ConnectedUser**, vagyis az aktuális felhasználó, aki létrehozta a JEA-munkamenetben, valamint a **felhasználó** amely azonosítja a JEA használt fiók hajtsa végre a parancsot.
Alkalmazás eseménynaplóit megjelenik a felhasználó által végrehajtott változtatások, így kellene az átiratok vagy modul parancsfájl naplózás engedélyezve kell tudniuk követni egy adott parancs meghívása vissza egy felhasználó számára rendkívül fontos.

## <a name="application-event-logs"></a>Alkalmazás eseménynaplóit

A JEA-munkamenetben, amellyel kommunikál egy külső alkalmazás vagy szolgáltatás egy parancs futtatásakor a ezeket az alkalmazásokat a saját eseménynaplók előfordulhat, hogy jelentkezzen események.
PowerShell-naplók és szövegekben, ellentétben más naplózási mechanizmusok nem rögzíti a JEA-munkamenet csatlakoztatott felhasználói, és inkább csak naplózza a virtuális futtató felhasználó vagy a csoportosan felügyelt szolgáltatásfiók.
Határozza meg, akik a parancsot futtatta, kell tekintenie a [munkamenet átiratok](#session-transcripts) vagy vesse össze a PowerShell-eseménynaplók az idő és a felhasználó látható az alkalmazások eseménynaplójában.

A WinRM-naplók is segíthetnek összekapcsolását futtató felhasználók az alkalmazások eseménynaplójában a csatlakozó felhasználó.
Eseményazonosító **193** a a **Microsoft-Windows-Windows távoli felügyeleti/műveleti** rögzíti a biztonsági azonosítóval (SID) és a fiók a csatlakozó felhasználó nevét és a felhasználó minden alkalommal futtassa a JEA naplózása munkamenet jön létre.

## <a name="session-transcripts"></a>Munkamenet szövegekben

Ha konfigurálta a JEA egy szöveges létrehozása minden felhasználói munkamenetet, minden felhasználói műveletek szöveges másolatának a megadott mappában kell tárolni.

Keresse meg az összes szöveges könyvtár, az alábbi parancsot rendszergazdaként azon a számítógépen konfigurált JEA:

```powershell
Get-PSSessionConfiguration | Where-Object { $_.TranscriptDirectory -ne $null } | Format-Table Name, TranscriptDirectory
```

Minden szöveges kapcsolatos információkat a munkamenet kezdete, mely a munkamenetet, és mely JEA identitás hozzá volt rendelve, a hozzájuk kapcsolódó felhasználó kezdődik.

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

Az átirat törzsében minden egyes parancsot, a felhasználó meghívása kapcsolatos naplózott információk.
A pontos szintaxist a parancsot futtatta a felhasználó nem érhető el a parancsokat a PowerShell-távelérést, átalakításának lehet a JEA-munkamenetek, azonban továbbra is meghatározhatja a hatékony a végrehajtott parancs.
Alul látható egy példa a szövegben kódrészlet futtató felhasználó `Get-Service Dns` JEA munkamenetben:

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

Az egyes parancsok egy felhasználó futtatja a "CommandInvocation" sor lesz írva, amely leírja a parancsmag, vagy a meghívott felhasználó működik.
ParameterBindings hajtsa végre az egyes CommandInvocation állapítható meg, akkor minden paraméter és érték, amely a parancs lett megadva.
A fenti példában láthatja, hogy a "név" paraméter megadott értéke "Dns" a "Get-Service" parancsmagot.

Minden parancs kimenete is kezdeményezi egy CommandInvocation általában élekről alapértelmezettként.
A Out-Default InputObject olyan PowerShell-objektum, a parancs által visszaadott.
Nyomtatási objektum részleteit az alábbi szorosan mimicking, mi a felhasználó lenne látott néhány sort.

## <a name="see-also"></a>Lásd még:

- [*PowerShell a kék csapat ♥* biztonsági blogbejegyzés](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)
