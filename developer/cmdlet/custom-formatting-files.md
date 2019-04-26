---
title: Egyéni formázás fájlok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 85d27545-8097-4010-9947-6d8b3ce2eac0
caps.latest.revision: 15
ms.openlocfilehash: 71c1c181058c5646c817b90d9832976a78c6c7de
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068300"
---
# <a name="custom-formatting-files"></a>Egyéni formázási fájlok

A megjelenítési formátumának parancsmagok, függvények és parancsfájlok által visszaadott objektumokhoz definiált formázási fájlok (format.ps1xml) használatával. Ezek a fájlok számos Windows PowerShell használatával határozza meg azokat az objektumokat Windows PowerShell-parancsmagok által visszaadott alapértelmezett megjelenítési formátumát által biztosított. Azonban a saját egyéni formázási fájlok felülírja az alapértelmezett megjelenítési formátum vagy meghatározásához a saját parancs által visszaadott objektumokhoz megjelenítését is létrehozhat.

Windows PowerShell a formázási ezeket a fájlokat az adatok segítségével határozza meg, mi jelenjen meg, és az adatok formázását. A megjelenített adatok tartalmazhatnak egy objektum tulajdonságait, vagy parancsprogram-blokkot értékét.  Parancsfájl-blokkokban használhatók, ha azt szeretné, néhány érték, amely nem érhető el az objektum tulajdonságainak megjelenítéséhez. Például előfordulhat, hogy szeretné adjon hozzá egy objektum két tulajdonság értékét, és egy különálló adat, az eredményt jeleníti meg. Saját formázás fájl írásakor meg kell határoznia *nézetek* megjeleníteni kívánt objektumokra vonatkozóan. Megadhatja, hogy egyetlen nézetben minden objektum esetén, meghatározhatja, hogy egyetlen nézetben több objektumon, vagy megadhat több nézetet ugyanahhoz az objektumhoz. Nincs nem definiálható nézetek száma nincs korlátozva.

> [!IMPORTANT]
> Formázási fájlokat nem határozzák meg a folyamat visszaadott objektum elemét. A folyamat számára ad vissza egy objektumot, amikor az objektum összes tagja érhetők el.

## <a name="format-views"></a>Formátum nézetek

Formázási nézetek objektumokat megjelenítheti táblázatos formában, a lista formájában, a széles formátumban és a egy egyéni formátum. Az esetek többségében minden egyes formázási definíció nézet leíró XML-címkék csoportja által leírása. Mindegyik nézetről tartalmaz a nézet nevét az objektumok, amelyek a nézet és az elemek a nézetet, például az oszlopok és sorok információk a táblázatos nézetre.

A következő nézetek érhetők el.

Tábla nézet egy objektum vagy egy parancsfájl blokk értéket egy vagy több oszlop tulajdonságai szerepelnek. Minden oszlop egy tulajdonság az objektum vagy egy parancsfájl blokk értéket képvisel. Egy objektum vagy a tulajdonságok és parancsfájl-blokk értékek kombinációjának a tulajdonságok egy részének objektum tulajdonságait megjelenítő táblázat nézet határozhatja meg. A táblázat minden egyes sorára jelenti. a visszaadott objektum. Ez a nézet kapcsolatos további információkért lásd: [táblázatos nézetre](../format/creating-a-table-view.md).

Listanézet-objektum vagy egy parancsfájl blokk érték csak egy oszlop tulajdonságok listája. A lista minden egyes sorára egy nem kötelező címke vagy a tulajdonságot vagy parancsfájl-blokk értékét a tulajdonság nevét jeleníti meg. Ez a nézet kapcsolatos további információkért lásd: [listanézet](../format/creating-a-list-view.md).

Széles nézet egy objektum vagy egy parancsfájl blokk értéket egy vagy több oszlop egyetlen tulajdonságát sorolja fel. Nincs címke vagy fejléc ehhez a nézethez. Ez a nézet kapcsolatos további információkért lásd: [széles nézet](../format/creating-a-wide-view.md).

Egyéni nézet nézetet jelenít meg egy testre szabható objektum tulajdonságai vagy parancsfájl-blokk értékek, amelyek nem követi a nézetek, a nézetek és a széles körű nézetek merev struktúráját. Meghatározhat egy különálló egyéni nézetet, vagy megadhat egy egyéni nézet, amelyet egy másik nézetre, például egy táblázat vagy lista nézetben. Ez a nézet kapcsolatos további információkért lásd: [egyéni nézet](../format/creating-custom-controls.md).

## <a name="view-xml-elements"></a>XML-elemek megtekintése

Az alábbi példa bemutatja a táblázatos nézetre, amely tartalmazza a két oszlopot definiáló XML-címkéket. A [ViewDefinitions](../format/viewdefinitions-element-format.md) elem a tároló eleme a formázási fájlban meghatározott összes nézetben megtekinthetők. A [nézet](../format/view-element-format.md) elem definiálja az adott tábla, list, szélesre vagy egyéni nézet. Minden egyes nézetben a [neve](../format/name-element-for-view-format.md) elem nevét adja meg a nézet a [ViewSelectedBy](../format/viewselectedby-element-format.md) elem definiálja, amelyek a nézetet, és a más típusú vezérlőelem elemeket az objektumok (például a `TableControl` elem) határozza meg a nézet formátumát.

```xml
ViewDefinitions
  <View>
    <Name>Name of View</Name>
    <ViewSelectedBy>
      <TypeName>Object to display using this view</TypeName>
      <TypeName>Object to display using this view</TypeName>
    </ViewSelectedBy>
    <TableControl>
      <TableHeaders>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
      </TableHeaders>
      <TableRowEntries>
        <TableRowEntry>
          <TableColumnItems>
            <TableColumnItem>
              <PropertyName>Header for column 1</PropertyName>
            </TableColumnItem>
            <TableColumnItem>
              <PropertyName>Header for column 2</PropertyName>
            </TableColumnItem>
          </TableColumnItems>
        </TableRowEntry>
      </TableRowEntries>
    </TableControl)
  </View>
</ViewDefinitions>

```

## <a name="see-also"></a>Lásd még:

[Tábla nézet](../format/creating-a-table-view.md)

[Listanézet](../format/creating-a-list-view.md)

[Széles nézet](../format/creating-a-wide-view.md)

[Egyéni nézet](../format/creating-custom-controls.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
