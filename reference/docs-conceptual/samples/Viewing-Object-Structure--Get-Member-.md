---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Megtekintés objektum struktúra Get-Member
ms.openlocfilehash: 80b36abd303a708195f12d96511e616178d11b5a
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030705"
---
# <a name="viewing-object-structure-get-member"></a>Az objektumstruktúra (Get-Member)

Objektumok ilyen központi szerepet játszik a Windows PowerShell, mert nincsenek több natív parancsok tetszőleges objektumtípusok való használatra készült. A legfontosabb az egyik a **Get-Member** parancsot.

A legegyszerűbb módszer, amely a parancs visszaadja az objektumok elemzése, hogy a kimenetet, hogy a parancs a **Get-Member** parancsmagot. A **Get-Member** parancsmag megjeleníti az objektumtípus formális nevét és a tagjai teljes listáját. A visszaadott elemek száma néha elsöprő is lehet. Ha például egy folyamat objektumot rendelkezhet több mint 100 tag.

Egy folyamat objektumot és a kimeneti oldal összes tagját jelenik meg, hogy minden adatot meg tudja tekinteni, írja be:

```powershell
Get-Process | Get-Member | Out-Host -Paging
```

Ez a parancs kimenete ehhez hasonló fog kinézni:

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

Azt is, hogy információk hosszú listája használhatóbbá szeretnénk megnézni elemek szűrése. A **Get-Member** listában csak a tagok, amelyek a Tulajdonságok parancs segítségével. Nincsenek tulajdonságok több formáját. A parancsmag bármilyen típusú tulajdonságokat jeleníti meg, ha be van állítva a **Get-Member MemberType** paraméter értékére **tulajdonságok**. Az eredményül kapott bejegyzéslista még mindig nagyon hosszú, de egy kicsit jobban kezelhető:

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
> Az engedélyezett értékek a MemberType: AliasProperty, CodeProperty, tulajdonságot, NoteProperty, ScriptProperty, tulajdonságok, PropertySet, metódus, CodeMethod, ScriptMethod, módszerek, ParameterizedProperty, MemberSet és az összes.

Nincsenek a folyamat több mint 60 tulajdonságait. A Windows PowerShell gyakran látható csak néhány rekordra minden olyan jól ismert objektum tulajdonságait, hogy ezek mindegyike megjelenítő OK akkor az eredmény egy Kezelhetetlen mennyiségű olyan információt.

> [!NOTE]
> Windows PowerShell egy objektum típusának megjelenítése végződésű névvel rendelkező XML-fájlokban tárolt információk alapján határozza meg. format.ps1xml. A folyamat objektumok, amelyek .NET System.Diagnostics.Process objektumok, adatok formázása DotNetTypes.format.ps1xml van tárolva.

Ha kivételével, amelyek a Windows PowerShell alapértelmezés szerint megjeleníti a tulajdonságainak megjelenítéséhez szüksége, szüksége lesz a kimeneti adatok formázásához, saját magának. Ez a formátum parancsmagok segítségével teheti meg.
