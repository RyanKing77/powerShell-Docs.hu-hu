---
title: Adatok megjelenítése feltételek meghatározása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c1e05821-6aec-437b-84a5-218a5727f88b
caps.latest.revision: 10
ms.openlocfilehash: 8a5b84b6a461e9fc340a5981578d95ca2ac6b9f7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846563"
---
# <a name="defining-conditions-for-displaying-data"></a>Adatok megjelenítésére vonatkozó feltételek definiálása

Nézet vagy egy vezérlőelem által megjelenített adatok meghatározásakor megadhat egy feltételt, amely a megjeleníteni kívánt adatok léteznie kell. A feltétel is elindítható, egy adott tulajdonság, vagy ha egy parancsfájl vagy tulajdonság-érték kiértékelésének `true`. Amikor a kiválasztási feltétel teljesül, a nézet vagy a definíció szolgál.

## <a name="specifying-a-selection-condition-for-a-definition"></a>Adja meg a definíciófrissítés számára kijelölt feltétel

Nézet vagy vezérlőben definícióját létrehozásakor a `EntrySelectedBy` elem azt adhatja meg, hogy mely objektumok fogja használni a definíció, vagy milyen feltételt a definíciójában használt léteznie kell. A feltétel szerint van megadva a `SelectionCondition` elemet.

A következő példában egy táblázat nézet definíciójának kiválasztási feltétel van megadva. Ebben a példában a definíció használt, csak akkor, ha a megadott parancsfájl kiértékelése `true`.

```xml
<TableRowEntry>
  <EntrySelectedBy>
    <SelectionCondition>
      <ScriptBlock>ScriptToEvaluate</ScriptBlock>
    </SelectionCondition>
  </EntrySelectedBy>
  <TableColumnItems>
  </TableColumnItems>
</TableRowEntry>

```

Kiválasztási feltételek definícióját a nézet vagy vezérlő megadható száma nincs korlátozva van. A csak követelmények a következők:

- A kiválasztási feltétel egy tulajdonság neve vagy a feltétel indítható parancsfájlt kell megadnia, de nem adható meg egyszerre.

- A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.

## <a name="specifying-a-selection-condition-for-an-item"></a>Egy elem kiválasztási feltétel megadása

Megadhatja azt is, ha egy elem a lista nézet vagy a vezérlő használja többek között a `ItemSelectionCondition` elem a cikk definíciójában. A következő példában egy elem a lista nézet kiválasztási feltétel van megadva. Ebben a példában az elem csak akkor, ha a parancsfájl kiértékelése használt `true`.

```xml
<ListItem>
  <ItemSelectionCondition>
    <ScriptBlock>ScriptToEvaluate</ScriptBlock>
  </ItemSelectionCondition>
</ListItem>

```

Egy elem csak egy kijelölés feltételt is megadhat. És a feltétel egy tulajdonság neve vagy a feltétel indítható parancsfájlt kell megadnia, de nem adható meg egyszerre.

## <a name="xml-elements"></a>XML-elemek

 A következő XML-elemeket hozhat létre egy kiválasztási feltétel szolgálnak.

- A következő elemeket adja meg a nézet definíciói kiválasztási feltételek:

    - [A TableControl (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)

    - [A ListControl (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

    - [A WideControl (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

    - [A CustomControl (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)

- A következő elemeket adja meg a kiválasztási feltételek a gyakori és a nézet definíciók szabályozhatja:

    - [Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)

    - [Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)

- A következő elem azt határozza meg, a kiválasztási feltétel bővített gyűjtemény objektumok:

    - [A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

- A következő elemet a kiválasztási feltétel az adatok új csoport megjelenítéséhez adja meg:

    - [A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)

- A következő elem azt határozza meg, az adott nézet egy elem kiválasztási feltétel:

    - [A ListControl (formátum) ListItem ItemSelectionCondition eleme](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md)

- A következő elemeket adja meg, hogy egy elem kiválasztási feltétel vezérlők:

    - [Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)

    - [Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)

    - [A CustomControl (formátum) ExpressionBinding ItemSelectionCondition elem.](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)

## <a name="see-also"></a>Lásd még:

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
