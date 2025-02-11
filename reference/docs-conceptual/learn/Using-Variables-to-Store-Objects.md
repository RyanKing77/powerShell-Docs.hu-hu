---
ms.date: 08/27/2018
keywords: PowerShell, a parancsmag
title: Objektumok tárolása változókban
ms.openlocfilehash: 2d20d84e48d3f68cab5c1ffa05d689b46415ebc8
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030367"
---
# <a name="using-variables-to-store-objects"></a>Objektumok tárolása változókban

PowerShell-objektumok működik. PowerShell változók néven elnevezett objektumok létrehozását teszi lehetővé.
Változónevek aláhúzásjel és bármely alfanumerikus karaktereket tartalmazhat. A PowerShell használatakor egy változó mindig használatával van megadva a \$ karakter követ a változó nevét.

## <a name="creating-a-variable"></a>Egy változó létrehozása

Írja be egy érvényes változónevet hozhat létre egy változót:

```
PS> $loc
PS>
```

Ebben a példában nincs eredményt adja vissza, mert `$loc` nincs értéke. Hozzon létre egy változót, és rendelje hozzá ugyanazt a lépésben egy értéket. PowerShell csak a változót hoz létre, ha még nem létezik.
Ellenkező esetben a megadott értéket rendel a meglévő változókat. Az alábbi példában az aktuális helyen tárolja a változó `$loc`:

```powershell
$loc = Get-Location
```

PowerShell semmilyen kimenet jeleníti meg, ha ezt a parancsot. PowerShell Get-Location kimenete küld `$loc`. A PowerShell nem hozzárendelt vagy átirányított adatokat küldeni a képernyő. Írja be `$loc` az aktuális tartózkodási helyét jeleníti meg:

```
PS> $loc

Path
----
C:\temp
```

Használhat `Get-Member` a változók tartalma információit jeleníti meg. `Get-Member` azt mutatja be, hogy `$loc` van egy **PathInfo** objektum, csakúgy, mint a kimenetét `Get-Location`:

```powershell
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

## <a name="manipulating-variables"></a>Változók módosítása

PowerShell segítségével kezelheti a változók különböző parancsokat biztosít. Egy olvasható formában felsorolását beírásával tekintheti meg:

```powershell
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

PowerShell számos, a rendszer által meghatározott változókat is létrehoz. Használhatja a `Remove-Variable` változók, amely PowerShell nem szabályozza, távolítsa el a jelenlegi munkamenet-parancsmagot. Írja be a következő parancsot, törölje az összes változót:

```powershell
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

Az előző parancs futtatása után a `Get-Variable` parancsmag megjeleníti a PowerShell rendszerváltozók.

PowerShell létrehoz egy változó meghajtó is. Az alábbi példa használatával megjelenítheti az összes PowerShell változók a változó meghajtót használja:

```powershell
Get-ChildItem variable:
```

## <a name="using-cmdexe-variables"></a>A cmd.exe változók használata

PowerShell bármely Windows-folyamat számára elérhető azonos környezeti változókat is használhat, beleértve a **cmd.exe**. Ezek a változók nevű meghajtó keresztül közzétett `env:`. Ezek a változók a következő parancs beírásával tekintheti meg:

```powershell
Get-ChildItem env:
```

A standard `*-Variable` parancsmagok nem tudja kezelni a környezeti változókat. A környezeti változók használatával elért a `env:` meghajtó előtag. Például a **% SystemRoot %** változóját **cmd.exe** az operációs rendszer legfelső szintű könyvtár nevét tartalmazza. A PowerShellben használja `$env:SystemRoot` elérni ugyanazt az értéket.

```
PS> $env:SystemRoot
C:\WINDOWS
```

Is létrehozhat, és a Powershellen belülről a környezeti változók módosításához. Környezeti változók a PowerShellben hajtsa végre a környezeti változókat az operációs rendszer máshol használja ugyanazokat a szabályokat. A következő példában létrehozunk egy új környezeti változót:

```powershell
$env:LIB_PATH='/usr/local/lib'
```

Bár nem kötelező, szokás a környezeti változók neve csupa nagybetűssé használatához.
