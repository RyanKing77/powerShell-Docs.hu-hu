---
title: Kijelölt csoportok meghatározása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 00dbb5ee-93d4-4914-a082-ef4d8b236b5c
caps.latest.revision: 16
ms.openlocfilehash: 596212f2e64401a751cf3dca0ee7d60b80912c00
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848859"
---
# <a name="defining-selection-sets"></a>Kijelölési csoportok definiálása

Nézetek és a vezérlők létrehozásakor hivatkozott objektumok készleteit kijelölt csoportok szerint adhatja meg. Egy kiválasztási beállítása lehetővé teszi, hogy meghatározza az objektumok egy alkalommal megadásukhoz ismételten mindegyik nézetben vagy vezérlő nélkül. Általában kijelölt csoportok használja egy sor kapcsolódó .NET-objektumokat. Ha például a `FileSystem` formázási fájlt (FileSystem.format.ps1xml) határozza meg a rendszer fájltípusokat, amelyek számos nézet kiválasztása készletét.

## <a name="where-selection-sets-are-defined-and-referenced"></a>Kijelölt csoportok amelyeknél definiált és hivatkozott

Kijelölt csoportok meghatározhatja a common data, a nézetek és a formázási fájlban meghatározott vezérlők által használható részeként. Az alábbi példa bemutatja, hogyan három kijelölési csoportok meghatározására.

```xml
<Configuration>
  <SelectionSets>
    <SelectionSet>...</SelectionSet>
    <SelectionSet>...</SelectionSet>
    <SelectionSet>...</SelectionSet>
  </SelectionSets>
</Configuration>
```

A kijelölés hivatkozhat állítja be a következő módon:

- Mindegyik nézetről tartalmaz egy `ViewSelectedBy` elem, amely meghatározza, hogy mely objektumok jelennek meg a nézet használatával. A `ViewSelectedBy` elemnek egy `SelectionSetName` gyermekelemet, amely meghatározza a kijelölési beállítása, amely a nézet feltételeit a definíciókat. Nincs kijelölt csoportok nézetben hivatkozási száma korlátozva.

- Minden egyes definíciójában nézet vagy -vezérlés a `EntrySelectedBy` elem határozza meg, hogy mely objektumok jelennek meg, hogy a definíció használatával. Általában egy nézetet, vagy a vezérlő csak egy definícióval rendelkezik úgy határozzák meg az objektumokat a `ViewSelectedBy` elemet. A `EntrySelectedBy` elemnek a definíció egy `SelectionSetName` , amely meghatározza a kijelölési set gyermekelemet. Ha a kiválasztása a definíciófrissítés számára adja meg, nem adhat meg, további alárendelt elemek a `EntrySelectedBy` elemet.

- Minden egyes definíciójában nézet vagy -vezérlés a `SelectionCondition` elem segítségével adja meg a definíció használatakor feltételt. A `SelectionCondition` elemnek egy `SelectionSetName` gyermekelemet, amely meghatározza a kijelölési beállítása, amely elindítja a feltételt. A feltétel akkor aktiválódik, ha a kijelölt csoportban meghatározott objektum jelenik meg. Ezek a feltételek beállításával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

## <a name="selection-set-example"></a>Kijelölés példa beállítása

Az alábbi példa bemutatja egy kiválasztási csoportja, amelyek közvetlenül származik a `FileSystem` Windows PowerShell által biztosított fájl formázását. Egyéb formázást fájlok Windows PowerShell kapcsolatos további információkért lásd: [Windows PowerShell formázás fájlok](./powershell-formatting-files.md).

```xml
<SelectionSets>
  <SelectionSet>
    <Name>FileSystemTypes</Name>
    <Types>
     <TypeName>System.IO.DirectoryInfo</TypeName>
     <TypeName>System.IO.FileInfo</TypeName>
     <TypeName>Deserialized.System.IO.DirectoryInfo</TypeName>
     <TypeName>Deserialized.System.IO.FileInfo</TypeName>
    </Types>
  </SelectionSet>
</SelectionSets>
```

Az előző kijelölés készletet hivatkozik a `ViewSelectedBy` elem a táblázatos nézetre.

```xml
<ViewDefinitions>
  <View>
    <Name>Files</Name>
    <ViewSelectedBy>
      <SelectionSetName>FileSystemTypes</SelectionSetName>
    </ViewSelectedBy>
    <TableControl>...</TableControl>
  </View>
</ViewDefinitions>

```

## <a name="xml-elements"></a>XML-elemek

 Nincs kijelölt csoportok definiálható száma nincs korlátozva. A következő XML-elemeket segítségével hozzon létre egy kiválasztási csoportot.

- A [SelectionSets](./selectionsets-element-format.md) elem definiálja a különböző nézetek által hivatkozott .NET-objektumokat és fájl formázási vezérlők.

- A [SelectionSet](./selectionset-element-format.md) elem egy .NET-objektumokká egyetlen csoportját határozza meg.

- A [neve](./name-element-for-selectionset-format.md) elem nevét adja meg, amellyel a kijelölt csoport hivatkozhat.

- A [típusok](./types-element-for-selectionset-format.md) elem azt határozza meg az objektumok a kijelölt csoport .NET tulajdonságtípusokat. (Belül fájlok formázást, objektumok vannak megadva .NET típus szerint.)

 A következő XML-elemeket adjon meg egy kijelölést szolgálnak.

- A következő elem azt határozza meg, a kijelölt állítható be a nézet a definíciók használható:

    - [SelectionSetName eleme ViewSelectedBy (formátum)](./selectionsetname-element-for-viewselectedby-format.md)

    - [A GroupBy (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-groupby-format.md)

- A következő elemeket adja meg a kijelölési készlet egyetlen nézetdefiníció által használt:

    - [A ListControl (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)

    - [A TableControl (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-tablecontrol-format.md)

    - [A WideControl (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-widecontrol-format.md)

    - [A nézet (formátum) CustomControl EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-customcontrol-for-view-format.md)

- A következő elemeket adjon meg a kijelölési közös által használt és vezérlőelem-definíciók megtekintése:

    - [Nézet (formátum) vezérlők EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-controls-for-view-format.md)

    - [Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-controls-for-configuration-format.md)

- A következő elemeket adjon meg a kijelölési bontsa ki a objektum meghatározása során használt:

    - [A EnumerableExpansion (formátum) EntrySelectedBy SelectionSetName elem.](./selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format.md)

- A következő elemeket adjon meg a kijelölési kiválasztási feltételek által használt.

    - [Konfiguráció (formátum) vezérlők SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)

    - [Nézet (formátum) vezérlők SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)

    - [A nézet (formátum) CustomControl SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-customcontrol-for-view-format.md)

    - [SelectionSetName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)

    - [A EntrySelectedBy ListEntry (formátum) a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-listentry-format.md)

    - [A EntrySelectedBy TableControl (formátum) a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

    - [A EntrySelectedBy WideEntry (formátum) a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)

    - [A GroupBy (formátum) SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-groupby-format.md)

## <a name="see-also"></a>Lásd még:

[SelectionSets](./selectionsets-element-format.md)

[SelectionSet](./selectionset-element-format.md)

[Name (Név)](./name-element-for-selectionset-format.md)

[Típusok](./types-element-for-selectionset-format.md)

[PowerShell formázás fájlok](./powershell-formatting-files.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[Egy PowerShell-formázást és típusok fájl írása](./writing-a-powershell-formatting-file.md)
