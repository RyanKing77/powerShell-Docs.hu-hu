---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, powershell, beállítás"
ms.openlocfilehash: 3413672e73705252225300a853c10a514500baa2
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="extract-and-parse-structured-objects-out-of-string"></a>Bontsa ki és Structured objektumok kívül karakterlánc elemzése
Az azzal a ConvertFrom-karakterlánc parancsmag további funkciókkal is:

-   Alapértelmezés szerint eltávolítja a mértékben text tulajdonságához. Megadhatja a - IncludeExtent paraméterrel.

-   Sok tanulási algoritmus hibajavításokat tartalmaz az MVP és közösségi visszajelzését.

-   Új - UpdateTemplate paramétere a tanulási algoritmus-eredményeket menteni a sablonfájl megjegyzést. Így a tanulási (a leglassabb szakasza) feldolgozása egy egyszeri költség. A sablont, amely tartalmazza a kódolt tanulási algoritmus Convert-karakterlánc fut már szinte azonnali.


<a name="extract-and-parse-structured-objects-out-of-string-content"></a>Bontsa ki és értelmezni a karakterlánc tartalmakhoz strukturált objektumok
----------------------------------------------------------

Együttműködve [Microsoft Research](http://research.microsoft.com/), egy új **ConvertFrom-karakterlánc** parancsmaggal hozzá lett adva.

Ez a parancsmag két módot támogat: basic tagolt elemzése, és automatikusan létrejön példa adatvezérelt elemzésekor.

Tagolt elemzése, alapértelmezés szerint felosztja a bemeneti: szóköz, és a tulajdonságnevek rendel az eredményül kapott csoportok. Testre szabhatja az elválasztó karakter:

> 1 \[C:\\temp\] &gt; &gt; "Hello, World" |} ConvertFrom-karakterlánc |} Táblázat formázása-automatikus

P1    P2
--    --

A parancsmag is támogatja a alapján automatikusan létrehozott példa adatvezérelt elemzése a [FlashExtract](http://research.microsoft.com/en-us/um/people/sumitg/flashextract.html) munka kutatás [Microsoft Research](http://research.microsoft.com).

A kezdéshez, fontolja meg a szöveges címjegyzék:

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

Néhány példa átmásolja a fájlt, amely a sablont használhatja:

    Ana Trujillo

    Redmond, WA

    Antonio Moreno

    Renton, WA

   

Helyezze a kinyerési, kívánt adatok körül kapcsos zárójelek adjon neki egy nevet, azt megteheti. Mivel a **neve** tulajdonság (és a kapcsolódó egyéb tulajdonságok) is többször jelenik meg, használja a csillag (\*) jelzi, hogy az eredmény több rekordot (helyett álló, lemezcsoport típusú tulajdonságok csomagolja ki egy rekord):

    {Name\*:Ana Trujillo}

    {City:Redmond}, {State:WA}

    {Name\*:Antonio Moreno}

    {City:Renton}, {State:WA}

Példák, a készletből **ConvertFrom-karakterlánc** mostantól automatikusan nyerhet objektum alapú kimeneti hasonló struktúrájú bemeneti fájlokból.

> 2 \[C:\\temp\]
>
> &gt;&gt; Get-tartalom. \\addresses.output.txt |} ConvertFrom-karakterlánc - TemplateFile. \\addresses.template.txt |} &gt; &gt; &gt; Format-Table-automatikus
>
> ExtentText neve város állapota
> ----------                     ----               ----     -----
> Ana Trujillo...                Ana Trujillo Redmond WA Antonio Moreno...              Antonio Moreno Renton WA Thomas Zsigmond...                Thomas Zsigmond Seattle WA lengyel Berglund...          Lengyel Berglund Redmond WA Hanna Moos...                  Hanna Moos Puyallup WA

További adatok módosítását. a kibontott szöveg, amelyet ehhez a **ExtentText** tulajdonság rögzíti a raw szöveg, amelyből a rekordot ki lett olvasni. Visszajelzés a szolgáltatást, vagy amelynek nehézségei vannak példák írása tartalmak megosztása, írjon e-mailt <psdmfb@microsoft.com>.

