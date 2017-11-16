---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Tárolási objektumok változók használata"
ms.assetid: b1688d73-c173-491e-9ba6-6d0c1cc852de
ms.openlocfilehash: 9a95d421fa2686608a565987c16fecc41c3c6d20
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/13/2017
---
# <a name="using-variables-to-store-objects"></a>Tárolási objektumok változók használata
PowerShell objektumok működik. PowerShell lehetővé teszi változók, alapvetően az objektumok megőrizni későbbi felhasználásra kimeneti nevű létrehozását. Más változók használata esetén ismertetése ne feledje, hogy PowerShell változók objektumokat, nem szöveges.

Változók mindig vannak-e megadva, a kezdeti karakter $, és a alfanumerikus karaktereket vagy a aláhúzásjellel is tartalmazhat, a név.

### <a name="creating-a-variable"></a>Egy változó létrehozása
Írja be egy érvényes változónevet hozhat létre egy változót:

```
PS> $loc
PS>
```

Ez eredményt adja vissza, nem mert **$loc** rendelkezik értékkel. Hozzon létre egy változót, és rendelje hozzá az azonos lépésben értéket. PowerShell csak létrehozza a változót, ha nem létezik. Ellenkező esetben a megadott érték rendel a létező változó. Az aktuális helyen tárolja a változóban **$loc**, típus:

```
$loc = Get-Location
```

Nem jelenik meg ez a parancs beírásakor, mert a kimeneti $helyi küld kimeneti van A PowerShellben megjelenített eredménye az, hogy az adatokat, amely nem egyéb irányítva, mindig küldi el a képernyőre egyik mellékhatása. Írja be a $loc megjeleníti az aktuális hely:

```
PS> $loc

Path
----
C:\temp
```

Használhat **Get-tag** változók tartalma kapcsolatos információk megjelenítéséhez. A Get-tag $loc ismertetett láthatja, hogy a rendszer egy **PathInfo** objektum, csakúgy, mint a kimenet a Get-helyről:

```
PS> $loc | Get-Member -MemberType Property

   TypeName: System.Management.Automation.PathInfo

Name         MemberType Definition
----         ---------- ----------
Drive        Property   System.Management.Automation.PSDriveInfo Drive {get;}
Path         Property   System.String Path {get;}
Provider     Property   System.Management.Automation.ProviderInfo Provider {...
ProviderPath Property   System.String ProviderPath {get;}
```

### <a name="manipulating-variables"></a>Változók módosítása
PowerShell biztosít több parancsok, változók módosítására. Írja be a teljes listáját a olvasható formában látható:

```
Get-Command -Noun Variable | Format-Table -Property Name,Definition -AutoSize -Wrap
```

A változók hoz létre az aktuális PowerShell-munkamenetben kívül több rendszer által definiált változókat. Használhatja a **Remove-változó** parancsmag segítségével törölje a jelet a változókat, amelyek nem szabályozzák PowerShell kijelentkezik. Írja be a következő parancs futtatásával törölje az összes változó:

```
Remove-Variable -Name * -Force -ErrorAction SilentlyContinue
```

Ez a művelet létrehoz a megerősítést kérő alább látható.

```
Confirm
Are you sure you want to perform this action?
Performing operation "Remove Variable" on Target "Name: Error".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):A
```

Ha ezután futtatja a **Get-Variable** parancsmag, látni fogja a fennmaradó PowerShell változókat. Egy változó PowerShell meghajtó is van, mivel emellett megjeleníthetők összes PowerShell változók beírásával:

```
Get-ChildItem variable:
```

### <a name="using-cmdexe-variables"></a>Cmd.exe változók használata
PowerShell, de nem Cmd.exe parancs-rendszerhéj környezetben fut, és minden környezetben elérhető azonos változókat is használhat, a Windows. Ezek a változók egy meghajtón keresztül közzétett **env**:. Ezek a változók beírásával tekintheti meg:

```
Get-ChildItem env:
```

Bár a szabványos változó parancsmagok vannak nem tudja kezelni a **env:** változók, továbbra is használhatja őket megadásával a **env:** előtag. Például az operációs rendszer gyökérkönyvtárában megtekintéséhez használhatja a parancs-rendszerhéj **% SystemRoot %** belül PowerShell írja be a változót:

```
PS> $env:SystemRoot
C:\WINDOWS
```

Hozhat létre, és PowerShell belül a környezeti változók módosításához. Környezeti változók elérhető Windows PowerShell rendszerben található Windows környezeti változók normál szabályok felelnek meg.

