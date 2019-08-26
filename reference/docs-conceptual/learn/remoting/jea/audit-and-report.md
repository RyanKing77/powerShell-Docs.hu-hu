---
ms.date: 07/10/2019
keywords: jea, PowerShell, biztonság
title: Naplózás és jelentéskészítés a JEA
ms.openlocfilehash: 2afefe83acecc1fc3643d49766120ffecc25378f
ms.sourcegitcommit: e894ed833cef57967cdaf002f8c883f66864e836
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017922"
---
# <a name="auditing-and-reporting-on-jea"></a>Naplózás és jelentéskészítés a JEA

A JEA üzembe helyezése után rendszeresen ellenőriznie kell a JEA konfigurációját. A naplózás segít felmérni, hogy a megfelelő személyek férhetnek hozzá a JEA-végponthoz, és a hozzájuk rendelt szerepkörök továbbra is megfelelőek-e.

## <a name="find-registered-jea-sessions-on-a-machine"></a>Regisztrált JEA-munkamenetek keresése a gépen

A [Get-PSSessionConfiguration](/powershell/module/microsoft.powershell.core/get-pssessionconfiguration) parancsmaggal ellenőrizhető, hogy mely JEA-munkamenetek vannak regisztrálva a gépen.

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

A végpontra érvényes jogosultságok az **engedély** tulajdonságban szerepelnek. Ezek a felhasználók jogosultak a JEA-végponthoz való kapcsolódásra. Azonban az azokhoz a szerepkörökhöz és parancsokhoz, amelyekhez hozzáférnek, a végpont regisztrálásához használt [munkamenet-konfigurációs fájlban](session-configurations.md) található **RoleDefinitions** tulajdonság határozza meg. Bontsa ki a **RoleDefinitions** tulajdonságot a szerepkör-hozzárendelések kiértékeléséhez egy regisztrált JEA-végponton.

```powershell
# Get the desired session configuration
$jea = Get-PSSessionConfiguration -Name 'JEAMaintenance'

# Enumerate users/groups and which roles they have access to
$jea.RoleDefinitions.GetEnumerator() | Select-Object Name, @{
  Name = 'Role Capabilities'
  Expression = { $_.Value.RoleCapabilities }
}
```

## <a name="find-available-role-capabilities-on-the-machine"></a>Elérhető szerepkör-képességek keresése a gépen

A JEA beolvassa `.psrc` a szerepkör-képességeket a **RoleCapabilities** mappában tárolt fájlokból egy PowerShell-modulon belül. A következő függvény megkeresi a számítógépen elérhető összes szerepkör-funkciót.

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
> A függvény eredményeinek sorrendje nem feltétlenül jelenti azt a sorrendet, amelyben a szerepkör-képességek ki lesznek választva, ha több szerepkör-képesség is ugyanazzal a névvel van megosztva.

## <a name="check-effective-rights-for-a-specific-user"></a>Egy adott felhasználóra érvényes jogosultságok keresése

A [Get-PSSessionCapability](/powershell/module/microsoft.powershell.core/Get-PSSessionCapability) PARANCSMAG egy JEA-végponton elérhető összes parancsot enumerálja egy felhasználó csoporttagságok alapján.
A kimenete `Get-PSSessionCapability` megegyezik a JEA-munkamenetben futó `Get-Command -CommandType All` megadott felhasználó nevével.

```powershell
Get-PSSessionCapability -ConfigurationName 'JEAMaintenance' -Username 'CONTOSO\Alice'
```

Ha a felhasználók nem rendelkeznek a csoportok olyan állandó tagjaival, amelyek további JEA jogokat biztosítanak, akkor ez a parancsmag nem tükrözi ezeket az extra engedélyeket. Ez akkor fordul elő, ha az igény szerinti privilegizált hozzáférés-kezelési rendszerek használata lehetővé teszi, hogy a felhasználók átmenetileg egy biztonsági csoporthoz tartozzanak. Alaposan értékelje ki a felhasználók szerepkörökhöz és képességekhez való hozzárendelését annak biztosításához, hogy a felhasználók csak a feladatok sikeres elvégzéséhez szükséges hozzáférési szintet kapják meg.

## <a name="powershell-event-logs"></a>PowerShell-eseménynaplók

Ha engedélyezte a modul-vagy parancsfájl-blokkoló naplózását a rendszeren, a Windows-eseménynaplókban láthatja az eseményeket, amelyeket a felhasználók egy JEA-munkamenetben futtatnak. Ezeknek az eseményeknek a megkereséséhez nyissa meg a **Microsoft-Windows-PowerShell/operatív** eseménynaplót, és keresse meg az eseményeket a **4104**-es azonosítójú eseménnyel.

Minden eseménynapló-bejegyzés tartalmaz információt arról a munkamenetről, amelyben a parancs futott. A JEA-munkamenetek esetében az esemény a **ConnectedUser** és a **RunAsUser**kapcsolatos információkat tartalmaz. A **ConnectedUser** az a tényleges felhasználó, aki létrehozta a JEA-munkamenetet. A **RunAsUser** a parancs végrehajtásához használt JEA-fiók.

Az alkalmazás eseménynaplói megjelenítik a **RunAsUser**által végzett módosításokat. Így a modul és a parancsfájlok naplózása engedélyezve van ahhoz, hogy egy adott parancs visszahívása visszakerüljön a **ConnectedUser**.

## <a name="application-event-logs"></a>Alkalmazás-eseménynaplók

A külső alkalmazásokkal vagy szolgáltatásokkal folytatott JEA-munkamenetekben futtatott parancsok a saját eseménynaplóba is naplózhatók az eseményeket. A PowerShell-naplók és-átiratok eltérően más naplózási mechanizmusok nem rögzítik a JEA-munkamenet csatlakoztatott felhasználóját. Ehelyett ezek az alkalmazások csak a virtuális futtató felhasználót naplózzák.
Ha meg szeretné állapítani, hogy ki futtatta a parancsot, akkor meg kell tekintenie egy [munkamenet](#session-transcripts) -átírást, vagy korrelálnia kell a PowerShell-eseménynaplókat az alkalmazás eseménynaplójában látható idővel és felhasználóval.

A Rendszerfelügyeleti webszolgáltatások naplója segítséget nyújthat a futtató felhasználóknak az alkalmazás-eseménynaplóban való összekapcsolásához is. **193** -es azonosítójú esemény a **Microsoft-Windows rendszerben –** a Rendszerfelügyeleti webszolgáltatások/operatív napló rögzíti a biztonsági azonosító (SID) és a fiók nevét mind a kapcsolódó felhasználó, mind pedig a futtató felhasználó számára minden új JEA-munkamenethez.

## <a name="session-transcripts"></a>Munkamenet-átiratok

Ha úgy konfigurálta a JEA, hogy az egyes felhasználói munkamenetek számára hozzon létre egy átiratot, a rendszer az összes felhasználó műveletének szöveges másolatát a megadott mappában tárolja.

A következő parancs (rendszergazdaként) megkeresi az összes átirat könyvtárat.

```powershell
Get-PSSessionConfiguration |
  Where-Object { $_.TranscriptDirectory -ne $null } |
    Format-Table Name, TranscriptDirectory
```

Az egyes átiratok a munkamenet elindításának idejével, a munkamenethez kapcsolódó felhasználóval és a hozzájuk rendelt JEA-identitással kapcsolatos információkkal kezdődnek.

```
**********************
Windows PowerShell transcript start
Start time: 20160710144736
Username: CONTOSO\Alice
RunAs User: WinRM Virtual Users\WinRM VA_1_CONTOSO_Alice
Machine: SERVER01 (Microsoft Windows NT 10.0.14393.0)
[...]
```

Az átirat törzse információt tartalmaz a felhasználó által meghívott parancsokról. A használt parancs pontos szintaxisa nem érhető el a JEA-munkamenetekben, mert az átalakított parancsok a PowerShell távelérési szolgáltatásban. Azonban továbbra is meghatározhatja a végrehajtott érvényes parancsot. Az alábbi példa egy JEA-munkamenetben futó `Get-Service Dns` felhasználó egy példáját mutatja be:

```
PS>CommandInvocation(Get-Service): "Get-Service"
>> ParameterBinding(Get-Service): name="Name"; value="Dns"
>> CommandInvocation(Out-Default): "Out-Default"
>> ParameterBinding(Out-Default): name="InputObject"; value="Dns"

Running  Dns                DNS Server
```

A rendszer minden egyes, a felhasználó által futtatott parancshoz **CommandInvocation** -sort ír. A **ParameterBindings** rögzíti a parancshoz megadott összes paramétert és értéket. Az előző példában látható, hogy a paraméter **neve** a ( `Get-Service` z) parancsmaghoz tartozó **DNS** értéket adta meg.

Az egyes parancsok kimenete **CommandInvocation**is indít, általában `Out-Default`a következőhöz:. A **inputobject elemnél** `Out-Default` a parancs által visszaadott PowerShell-objektum. Az objektum részletei az alábbi néhány sorban vannak kinyomtatva, és szorosan utánozzák, hogy a felhasználó mit látott.

## <a name="see-also"></a>Lásd még:

[*A PowerShell-♥ a Blue Team* blogjának biztonsági bejegyzése](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)
