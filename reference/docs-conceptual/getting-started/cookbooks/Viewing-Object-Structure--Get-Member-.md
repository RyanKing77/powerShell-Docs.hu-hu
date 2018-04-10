---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Megtekintés objektum struktúra Get tag
ms.assetid: a1819ed2-2ef3-453a-b2b0-f3589c550481
ms.openlocfilehash: cc93e45e4306b3d623c1d3d1096dd20c1afc59c8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="viewing-object-structure-get-member"></a>Objektum struktúra (Get-tag) megtekintése

Objektumok ilyen központi szerepet játszik a Windows PowerShell, mert nincsenek több natív parancsok tetszőleges objektumtípusokat működik. A legfontosabb az egyik a **Get-tag** parancsot.

A legegyszerűbb módszer a parancs visszaadja az objektumok elemzéséhez, hogy irányítsa a kimenetét a parancsnak a **Get-tag** parancsmag. A **Get-tag** parancsmag elsajátíthatja, hogy az objektum típusának formális nevét és annak tagjait teljes listáját. Visszaadott elemek száma néha túlságosan is lehet. Például egy folyamat objektumot rendelkezhet több mint 100 tagokat.

A Process objektum és a kimeneti oldal összes tagját szeretné megjeleníteni az összes parancsot kell beírnia:

```powershell
Get-Process | Get-Member | Out-Host -Paging
```

A parancs kimenete következőhöz hasonlóan fog kinézni:

```output
TypeName: System.Diagnostics.Process

Name                           MemberType     Definition
----                           ----------     ----------
Handles                        AliasProperty  Handles = Handlecount
Name                           AliasProperty  Name = ProcessName
NPM                            AliasProperty  NPM = NonpagedSystemMemorySize
PM                             AliasProperty  PM = PagedMemorySize
VM                             AliasProperty  VM = VirtualMemorySize
WS                             AliasProperty  WS = WorkingSet
add_Disposed                   Method         System.Void add_Disposed(Event...
...
```

Tökéletesíthetjük információk listája túl hosszú több használható szűréssel szeretnénk megnézni elemeknél használatos. A **Get-tag** parancs segítségével felsorolja, amelyek a tulajdonságok csak tagokat. Nincsenek több űrlap tulajdonságai. A parancsmag bármilyen típusú tulajdonságokat jeleníti meg, ha be van állítva a **Get-tag MemberType** paraméter értéke a **tulajdonságok**. A megjelenő listában még nagyon hosszú, de egy kicsit könnyebben kezelhető:

```
PS> Get-Process | Get-Member -MemberType Properties

   TypeName: System.Diagnostics.Process

Name                       MemberType     Definition
----                       ----------     ----------
Handles                    AliasProperty  Handles = Handlecount
Name                       AliasProperty  Name = ProcessName
...
ExitCode                   Property       System.Int32 ExitCode {get;}
...
Handle                     Property       System.IntPtr Handle {get;}
...
CPU                        ScriptProperty System.Object CPU {get=$this.Total...
...
Path                       ScriptProperty System.Object Path {get=$this.Main...
...
```

> [!NOTE]
> Az engedélyezett értékek MemberType: AliasProperty, CodeProperty, tulajdonság, NoteProperty, ScriptProperty, tulajdonságok, tulajdonsághalmaz, módszer, CodeMethod, ScriptMethod, módszerek, ParameterizedProperty, MemberSet és az összes.

A folyamat több mint 60 tulajdonságok van. A Windows PowerShell gyakran látható, csak kevés a jól ismert objektum tulajdonságait, amely megjeleníti az összes OK Kezelhetetlen mennyiségű információ eredményezne.

> [!NOTE]
> A Windows PowerShell egy objektum típusának megjelenítése a végződése nevű XML-fájlokban tárolt információk segítségével határozza meg. format.ps1xml. A folyamat objektumok, amelyek .NET System.Diagnostics.Process objektumok, formázási adatai DotNetTypes.format.ps1xml tárolja.

Alapértelmezés szerint megjeleníti a Windows PowerShell tulajdonságokat meg kell, ha szüksége lesz a kimeneti adatok formázásához saját maga. Ezt megteheti a formátum-parancsmagok használatával.