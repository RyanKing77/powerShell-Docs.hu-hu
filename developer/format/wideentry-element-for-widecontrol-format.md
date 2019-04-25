---
title: (Formátum) WideControl WideEntry eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 014763cb-7716-4931-899c-8375b5d7a3dd
caps.latest.revision: 15
ms.openlocfilehash: d1d13b5c3436871053353814293d9163ea13c7fb
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083671"
---
# <a name="wideentry-element-for-widecontrol-format"></a>A WideControl WideEntry eleme (Formátum)

A széles nézet definíciójának biztosít.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<WideEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <WideItem>...</WideItem>
</WideEntry>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `WideEntry` elemet. Meg kell adnia egy `WideItem` gyermekelemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[EntrySelectedBy eleme WideEntry (formátum)](./entryselectedby-element-for-wideentry-format.md)|Nem kötelező eleme.<br /><br /> A .NET-típusokat, amelyek a széles körű bejegyzés definíció vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.|
|[WideItem elem (formátum)](./wideitem-element-for-widecontrol-format.md)|Szükséges eleme.<br /><br /> Határozza meg, tulajdonság vagy parancsfájl, amelynek értéke megjelenik.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[WideEntries elem (formátum)](./wideentries-element-for-widecontrol-format.md)|A széles nézet a definíciókat tartalmazza.|

## <a name="remarks"></a>Megjegyzés

A széles nézet olyan egyetlen tulajdonság értékét vagy az egyes objektumok parancsfájlérték megjelenítő lista formájában. Ellentétben más típusú nézetek minden egyes nézet definíciójában csak egy elem elem is megadhat. Egy széles nézet az egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `WideEntry` elem, amely meghatározza egy `WideItem` elemet. A `WideItem` elem definiálja a tulajdonságot, amelynek értéke megjelenik a nézetben.

```xml
<WideEntries>
  <WideEntry>
    <WideItem>
      <PropertyName>ProcessName</PropertyName>
    </WideItem>
  </WideEntry>
</WideEntries>

```

Egy széles nézet egy teljes példa: [széles nézet (alapszintű)](./wide-view-basic.md).

## <a name="see-also"></a>Lásd még:

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[SelectionCondition eleme WideEntry (formátum)](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[SelectionSetName eleme WideEntry (formátum)](./selectionsetname-element-for-entryselectedby-for-widecontrol-format.md)

[TypeName eleme WideEntry (formátum)](./typename-element-for-entryselectedby-for-wideentry-format.md)

[WideEntries elem (formátum)](./wideentries-element-for-widecontrol-format.md)

[WideItem elem (formátum)](./wideitem-element-for-widecontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
