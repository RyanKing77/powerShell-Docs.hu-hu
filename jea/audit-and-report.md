---
ms.date: 06/12/2017
keywords: jea, a powershell, a biztonsági
title: Naplózási és jelentéskészítési összetevője JEA
ms.openlocfilehash: e68206cd6fe94c51507f42ae2c3e6702f6fd4e0f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188852"
---
# <a name="auditing-and-reporting-on-jea"></a>Naplózási és jelentéskészítési összetevője JEA

> A következőkre vonatkozik: a Windows PowerShell 5.0

JEA telepítése után célszerű rendszeresen rendszervizsgálati JEA konfigurációját.
Ez segítséget nyújt a megfelelő személyek hozzáférhetnek a JEA végpont, és a hozzárendelt szerepkörök továbbra is megfelelőek.

Ez a témakör ismerteti a különböző módszereket a JEA végpont naplózhatók.

## <a name="find-registered-jea-sessions-on-a-machine"></a>Regisztrált JEA munkamenetek található a gépen

Mely JEA munkamenetek regisztrált gépen ellenőrzéséhez használja a [Get-PSSessionConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/get-pssessionconfiguration) parancsmag.

```powershell
# Filter for sessions that are configured as 'RestrictedRemoteServer' to find JEA-like session configurations
PS C:\> Get-PSSessionConfiguration | Where-Object { $_.SessionType -eq 'RestrictedRemoteServer' }


Name          : JEAMaintenance
PSVersion     : 5.1
StartupScript :
RunAsUser     :
Permission    : CONTOSO\JEA_DNS_ADMINS AccessAllowed, CONTOSO\JEA_DNS_OPERATORS AccessAllowed, CONTOSO\JEA_DNS_AUDITORS AccessAllowed
```

A végpont a hatályos jogosultságok láthatók a "Engedély" tulajdonság.
Ezek a felhasználók jogosultak a JEA-végponthoz, de mely szerepkörök (és bővítmény parancsok által) kapcsolódni hozzáférhetnek a "RoleDefinitions" mező határozza meg a [munkamenet konfigurációs fájl](session-configurations.md) használt regisztrálja a a végpont.

A szerepkör-hozzárendelések a regisztrált JEA-végpont kiértékelheti az adatokat a "RoleDefinitions" kibontásával.

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{ Name = 'Role Capabilities'; Expression = { $_.Value.RoleCapabilities } }
```

## <a name="find-available-role-capabilities-on-the-machine"></a>A számítógépen elérhető szerepkör képességek keresése

Szerepkör szolgáltatásfájlokban csak által használandó JEA egy érvényes PowerShell-modul belül "RoleCapabilities" mappában vannak tárolva.
Az összes szerepkör lehetőségeinek számítógépen elérhető listájához keresve található.

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
> Ez a funkció eredményeinek sorrendje nem feltétlenül a sorrendben, amelyben a szerepkör képességek fog jelölhető ki, ha több szerepkör képességek megosztás neve.

## <a name="check-effective-rights-for-a-specific-user"></a>Jelölje be a felhasználó hatékony jogok

A JEA végpont beállítása után érdemes lehet, mely parancsok elérhető egy adott felhasználónak JEA munkamenetben.
Használhat [Get-PSSessionCapability](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/Get-PSSessionCapability) operációs rendszer összes felhasználó alkalmazandó parancs, ha azok az aktuális csoporttagságok JEA munkamenet indításához.
A kimeneti `Get-PSSessionCapability` megegyezik-e a megadott futtató felhasználó `Get-Command -CommandType All` JEA munkamenetben.

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

Ha a felhasználók nem lenne jogot adni őket további JEA csoportokat állandó tagjai, ez a parancsmag nem tükrözik az extra engedélyeket.
Általában ez a helyzet, a felhasználók ideiglenesen egy biztonsági csoporthoz tartozó just-in-time privileged access management rendszerek használata esetén.
Mindig gondosan értékelje ki a felhasználói szerepkör a leképezési és a felhasználók csak kap a parancsok a munkájuk sikeres elvégzéséhez szükséges lehető legkisebb mennyiségű való hozzáférés biztosításához szerepkörönként tartalmát.

## <a name="powershell-event-logs"></a>PowerShell-eseménynaplók

Ha engedélyezte a rendszer a bejelentkezés modul és/vagy parancsfájl-blokk, lesz, a Windows eseménynaplóiban keresse meg az egyes a felhasználó a JEA-munkamenetekben futtatott parancsok események található.
Ezek az események kereséséhez nyissa meg a Windows eseménynaplót, keresse meg a **Microsoft-Windows-PowerShell/műveleti** Eseménynapló, és keresse meg az Eseménynapló azonosítójú események **4104**.

Minden egyes eseménynapló-bejegyzés, amelyben a parancs futtatása a munkamenet adatait is tartalmazza.
A JEA-munkamenetekben, ide tartoznak a fontos információk a **ConnectedUser**, ez az a tényleges felhasználó, aki létrehozta a JEA munkamenet, valamint a **felhasználó** amely azonosítja az JEA használandó fiókot hajtsa végre a parancsot.
Alkalmazás eseménynaplóiban megjeleníti a felhasználó által végrehajtott módosítások, amelyek ki, vagy modul, a parancsfájl-naplózás engedélyezve különösen fontos tudja nyomon követni egy adott parancs meghívása vissza egy felhasználó számára.

## <a name="application-event-logs"></a>Alkalmazás eseménynaplóiban

A parancs futtatásakor, hogy a külső alkalmazás vagy szolgáltatás kommunikációja JEA munkamenetben ezeket az alkalmazásokat a saját eseménynaplók előfordulhat, hogy jelentkezzen események.
Ellentétben a PowerShell naplókat, valamint ki más naplózási mechanizmusok nem rögzíti a csatlakoztatott felhasználói a JEA-munkamenet, és inkább csak naplózza a virtuális futtató felhasználó vagy a csoportosan felügyelt szolgáltatásfiók.
Annak megállapítására, hogy ki futtatta a parancsot, szüksége lesz a további részleteket a [munkamenet Beszélgetés szövegének](#session-transcripts) vagy PowerShell-eseménynaplók okozták az az idő és a felhasználó az alkalmazások eseménynaplójában.

A Rendszerfelügyeleti webszolgáltatások napló segítségével összefüggéseket futtassa az alkalmazások eseménynaplójában keresse meg a felhasználók a csatlakozó felhasználó.
Eseményazonosító **193** a a **Microsoft-Windows-Windows távoli felügyeleti/műveleti** naplórekordok a biztonsági azonosító (SID) és a fiók a csatlakozó felhasználó neve és futtató felhasználó mindig a JEA munkamenet jön létre.

## <a name="session-transcripts"></a>Munkamenet ki

Ha JEA egy Beszélgetés szövegének létrehozása minden felhasználói munkamenetet konfigurálta, minden felhasználói műveletek szöveges másolatának tárolódnak a megadott mappát.

Összes beszélgetés szövegének könyvtár megkeresése, a következő parancsot futtassa rendszergazdaként a számítógépen JEA konfigurálva:

```powershell
Get-PSSessionConfiguration | Where-Object { $_.TranscriptDirectory -ne $null } | Format-Table Name, TranscriptDirectory
```

Minden egyes Beszélgetés szövegének kezdődik-e a indításakor a munkamenet, mely felhasználó csatlakozik, a munkamenet, mely JEA identitás lett rendelve kapcsolatos információkat.

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

A Beszélgetés szövegének törzsében minden parancs, a felhasználó meghívott kapcsolatos naplózott információk.
Pontos szintaxisa az a felhasználó futtatja a parancsot nem érhető el a parancsokat a PowerShell távelérése átalakítaná módjának JEA-munkamenetekben, azonban továbbra is meghatározhatja, hogy végre lett hajtva a hatékony parancs.
Egy példa Beszélgetés szövegének részlet futtató felhasználók az alábbiakban található `Get-Service Dns` JEA-munkamenetben:

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

Az egyes parancsok egy felhasználó futtatja a "CommandInvocation" sor kerülnek, a parancsmag leíró, vagy a meghívott felhasználó működik.
ParameterBindings hajtsa végre az egyes CommandInvocation, amely közli, minden paraméter és érték, amely a parancs lett megadva.
A fenti példában láthatja, hogy a paraméter "Name" lett megadva az érték "Dns" a "Get-szolgáltatás" parancsmaghoz.

Minden parancs is elindítja egy CommandInvocation általában az alapértelmezett kimenő irányú.
A Out-Default InputObject egy, a parancs által visszaadott PowerShell-objektum.
Lista tartalmazza az objektumokat, amelyek részleteit az alábbi szorosan mimicking Mi a felhasználó akkor amint láthatta néhány sor.

## <a name="see-also"></a>Lásd még:

- [A JEA-munkamenetben felhasználói műveletek naplózása](audit-and-report.md)
- [*PowerShell ♥ a kék Team* a biztonsági által írt blogbejegyzés](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)