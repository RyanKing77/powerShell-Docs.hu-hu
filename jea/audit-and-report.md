---
ms.date: 07/10/2019
keywords: a jea, powershell, biztonsági
title: Naplózás és a JEA-jelentések
ms.openlocfilehash: 2afefe83acecc1fc3643d49766120ffecc25378f
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726758"
---
# <a name="auditing-and-reporting-on-jea"></a>Naplózás és a JEA-jelentések

Miután telepítette a JEA, kell rendszeresen naplózása a JEA-konfigurációt. A naplózás segítségével felmérheti, hogy a megfelelő felhasználók is hozzáférhetnek a JEA-végpont, és a hozzárendelt szerepkörök továbbra is megfelelőek.

## <a name="find-registered-jea-sessions-on-a-machine"></a>Keresse meg a regisztrált JEA munkamenetek gépen

Ellenőrizze, hogy mely JEA munkamenetek gépen regisztrált, használja a [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) parancsmagot.

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

A végpont a hatályos jogosultságok láthatók a **engedély** tulajdonság. Ezek a felhasználók csatlakozni a JEA-végpont áll. Azonban a szerepkörök és a parancsok férhet hozzá, határozza meg a **RoleDefinitions** tulajdonságot a [munkamenet konfigurációs fájl](session-configurations.md) használt végpont. Bontsa ki a **RoleDefinitions** tulajdonság egy regisztrált a JEA-végpont a szerepkör-hozzárendelések kiértékeléséhez.

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{
  Name = 'Role Capabilities'
  Expression = { $_.Value.RoleCapabilities }
}
```

## <a name="find-available-role-capabilities-on-the-machine"></a>A gépen elérhető szerepköri funkciók keresése

A JEA szerepkör-szolgáltatásait, lekérdezi a `.psrc` tárolt fájlok a **RoleCapabilities** belüli egy PowerShell-modul. A következő függvényt egy számítógépen elérhető szerepköri funkciók keresése.

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
> Ez a függvény eredményeinek sorrendje nem feltétlenül a sorrend, amelyben a szerepkörrel képességeket lesz kiválasztva, ha több szerepkörrel képességeket rendelkezik ugyanazzal a névvel.

## <a name="check-effective-rights-for-a-specific-user"></a>Egy adott felhasználó hatékony jogok ellenőrzése

A [Get-PSSessionCapability](/powershell/module/microsoft.powershell.core/Get-PSSessionCapability) parancsmag a JEA-végpont egy vendégfelhasználói csoporttagságok alapján elérhető összes parancs enumerálása.
A kimenet a `Get-PSSessionCapability` megegyezik-e a megadott futtató felhasználó `Get-Command -CommandType All` JEA munkamenetben.

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

Ha a felhasználók számára szeretne jogosultságokat őket további JEA csoportok állandó tagjai nem, ez a parancsmag nem tükrözik az extra engedélyeket. Ez történik, ha használatával just-in-time rendszerjogosultságú hozzáférés ideiglenesen biztonsági csoporthoz tartozó felhasználók felügyeleti rendszerekkel. Gondosan mérlegelje, szerepkörök és funkciók annak érdekében, hogy felhasználók csak a munkájuk sikeres elvégzéséhez szükséges hozzáférési szintet, hogy a felhasználók leképezése.

## <a name="powershell-event-logs"></a>PowerShell-eseménynaplók

Ha engedélyezte a rendszer a bejelentkezés modul vagy a parancsfájl letiltása, láthatja az összes parancs a JEA munkamenet egy felhasználó futtatja a Windows eseménynaplóiban események. Ezeket az eseményeket, nyissa meg **Microsoft-Windows-PowerShell/műveleti** eseménynaplót, és keresse meg az eseményazonosító események **4104**.

Minden eseménynapló-bejegyzést, amelyben a parancs futtatása a munkamenet kapcsolatos információkat tartalmaz. A JEA-munkamenetet, az eseményt az alábbiakról tájékozódhat a **ConnectedUser** és a **felhasználó**. A **ConnectedUser** van az aktuális felhasználó, aki létrehozta a JEA-munkamenetet. A **felhasználó** JEA a parancs végrehajtásához használt fiók.

Alkalmazás eseménynaplóit által végrehajtott változtatások megjelenítése a **felhasználó**. Így modul és a parancsfájl-naplózás engedélyezve szükség egy adott parancs meghívása biztonsági másolatot a nyomkövetés a **ConnectedUser**.

## <a name="application-event-logs"></a>Alkalmazás eseménynaplóit

Parancsok futtatása a JEA-munkamenetet, amely együttműködik a külső alkalmazások vagy szolgáltatások események naplózása a saját ügyfélesemény-naplókba. PowerShell-naplók és szövegekben, ellentétben más naplózási mechanizmusok a JEA-munkamenet csatlakoztatott felhasználói nem rögzíti. Ehelyett ezeket az alkalmazásokat csak a virtuális futtató felhasználó naplózása.
Határozza meg, akik a parancsot futtatta, egyeztetniük kell egy [munkamenet átiratok](#session-transcripts) vagy vesse össze a PowerShell-eseménynaplók az idő és a felhasználó látható az alkalmazások eseménynaplójában.

A WinRM-naplót is segíthet futtató felhasználóknak a kapcsolódó felhasználó az alkalmazás eseménynaplója összekapcsolását. Eseményazonosító **193** a a **Microsoft-Windows-Windows távoli felügyeleti/műveleti** naplófájl rögzíti a biztonsági azonosítóval (SID) és a kapcsolódó felhasználó és a futtató fiók nevét felhasználóként minden új JEA munkamenet.

## <a name="session-transcripts"></a>Munkamenet szövegekben

Ha konfigurálta a JEA egy szöveges létrehozása minden felhasználói munkamenetet, minden felhasználói műveletek szöveges másolatának a megadott mappában vannak tárolva.

Az alábbi parancsot (rendszergazdaként) megkeresi az összes szöveges könyvtár.

```powershell
Get-PSSessionConfiguration |
  Where-Object { $_.TranscriptDirectory -ne $null } |
    Format-Table Name, TranscriptDirectory
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

Az átirat törzse tartalmazza minden egyes parancsot, a felhasználó meghívása kapcsolatos információkat. A pontos szintaxist a használt parancs a parancsokat a PowerShell távelérése átalakításának módja miatt nem érhető el a JEA-munkamenetekben. Azonban továbbra is meghatározhatja a hatékony parancsot, amely végre lett hajtva. Alul látható egy példa a szövegben kódrészlet futtató felhasználó `Get-Service Dns` JEA munkamenetben:

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

A **CommandInvocation** sor írt minden egyes parancsnál egy felhasználó futtatja. **ParameterBindings** minden paraméter és a parancs a megadott érték. Az előző példában láthatja, hogy a paraméter **neve** lett megadva a értékkel **Dns** számára a `Get-Service` parancsmagot.

A kimenet minden egyes parancsot is eseményindítók egy **CommandInvocation**, általában az `Out-Default`. A **InputObject** , `Out-Default` a PowerShell-objektumot a parancs által visszaadott. Nyomtatási objektum részleteit az alábbi szorosan mimicking, mi a felhasználó lenne látott néhány sort.

## <a name="see-also"></a>Lásd még:

[*PowerShell a kék csapat ♥* biztonsági blogbejegyzés](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)
