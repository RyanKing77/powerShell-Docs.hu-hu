---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: fcf2adf67f36edb534df3e2a849459fb20e1c2de
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085354"
---
# <a name="extract-and-parse-structured-objects-out-of-string"></a>Strukturált objektumok sztringekből való kibontása és elemzése

Néhány további funkciókat is azzal az `ConvertFrom-String` parancsmagot:

- Eltávolítja a mértékben a text tulajdonság alapértelmezés szerint. Megadhatja a - IncludeExtent paraméterrel.

- Számos tanulási algoritmus hibajavítások az MVP és a közösségi visszajelzések.

- Új - UpdateTemplate paraméter a tanulási algoritmus-eredményeket menteni a sablonfájlt megjegyzést. Ez lehetővé teszi a learning feldolgozásához (a leglassabb fázis) egy egyszeri költség. Futó Convert-karakterlánc, amely tartalmazza a kódolt tanulási algoritmus-sablonnal már szinte azonnali.

## <a name="extract-and-parse-structured-objects-out-of-string-content"></a>Strukturált objektumok karakterlánc tartalmakhoz kibontása és elemzése

Együttműködve [a Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F), egy új `ConvertFrom-String` parancsmaggal hozzá lett adva.

Ez a parancsmag két módot támogat: alapszintű tagolt elemzés, és automatikusan létrehozott példa adatvezérelt elemzése.

Tagolt elemzés, alapértelmezés szerint bontja a bemenet üres helyet, és a tulajdonságnevek rendel az eredményül kapott csoportok. Testre szabhatja az elválasztó karakter:

```powershell
"Hello World" | ConvertFrom-String | Format-Table -Auto
```

```output
P1     P2
--     --
Hello  World
```

A parancsmag is támogatja a alapján automatikusan létrehozott példa adatvezérelt elemzés a [FlashExtract](https://www.microsoft.com/en-us/research/publication/flashextract-framework-data-extraction-examples/?from=http%3A%2F%2Fresearch.microsoft.com%2Fen-us%2Fum%2Fpeople%2Fsumitg%2Fflashextract.html) kutatási munka [a Microsoft Research](https://www.microsoft.com/en-us/research/?from=http%3A%2F%2Fresearch.microsoft.com%2F).

Első lépésként fontolja meg egy szöveges alapú címjegyzék:

```
    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA

    Thomas Hardy

    Seattle, WA

    Christina Berglund

    Redmond, WA

    Hanna Moos

    Puyallup, WA
```

Néhány példa másolja egy fájlba, melyiket fogja használni a sablont:

```
    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA
```

Nevezi el, hogy ehhez kapcsos zárójelek körül adatokat szeretne kinyerni, helyezze el. Mivel a **neve** tulajdonság (és a kapcsolódó egyéb tulajdonságok) is többször jelenik meg, egy csillag (\*) jelzi, hogy ennek hatására a több rekord (nem pedig a tulajdonságok többféle csomagolja ki az egyik rekord):

```
    {Name\*:Ana Trujillo}

    {City:Redmond}, {State:WA}

    {Name\*:Antonio Moreno}

    {City:Renton}, {State:WA}
```

A példákban egy készlete `ConvertFrom-String` most már automatikusan kinyerheti az objektum alapú kimeneti bemeneti fájlok hasonló struktúrával.

```powershell
Get-Content .\addresses.output.txt | ConvertFrom-String -TemplateFile .\addresses.template.txt | Format-Table -Auto
```

```output
ExtentText                     Name               City     State
----------                     ----               ----     -----
Ana Trujillo...                Ana Trujillo       Redmond  WA
Antonio Moreno...              Antonio Moreno     Renton   WA
Thomas Hardy...                Thomas Hardy       Seattle  WA
Christina Berglund...          Christina Berglund Redmond  WA
Hanna Moos...                  Hanna Moos         Puyallup WA
```

Ehhez a kinyert szöveg további adatkezelés a **ExtentText** tulajdonság a nyers szöveg, amelyből a rekordot kinyert rögzíti. Szeretne visszajelzést adni ezt a szolgáltatást, vagy oszthat meg tartalmakat, amelyhez problémái vannak példák írása, írjon e-mailt <psdmfb@microsoft.com>.