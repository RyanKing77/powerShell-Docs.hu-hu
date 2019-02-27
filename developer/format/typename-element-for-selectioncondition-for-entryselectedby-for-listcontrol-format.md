---
title: SelectionCondition EntrySelectedBy ListControl (formátum) esetében a TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bd025a3a-3780-40db-a068-873e7df38015
caps.latest.revision: 9
ms.openlocfilehash: 2b76b040b39088cc9c3b9d6890c38df3c533b39f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851554"
---
# <a name="typename-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format"></a>Az ListControl EntrySelectedBy eleméhez tartozó SelectionCondition TypeName eleme (Formátum)

A .NET típusát, amely elindítja a feltételt határozza meg. Ez a típus meghatározva, a regisztrációslista-bejegyzés használ.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem ListControl (formátum) ListEntry elemhez tartozó ListEntries ListControl (formátum) EntrySelectedBy elemhez tartozó ListEntry EntrySelectedBy SelectionCondition EntrySelectedBy ListControl (formátum) esetében a vonatkozó ListControl (formátum) TypeName elemhez tartozó ListControl (formátum) SelectionCondition elemhez

## <a name="syntax"></a>Szintaxis

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A ListControl (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|Meghatározza a feltétellel, hogy a lista bejegyzés használandó léteznie kell.|

## <a name="text-value"></a>Szöveges érték

Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.

## <a name="remarks"></a>Megjegyzés

A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre. Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

További információ más olyan listanézetet összetevőinek: [lista nézet létrehozásával](./creating-a-list-view.md).

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[Mikor jelenik meg adat feltételeinek meghatározása](./defining-conditions-for-displaying-data.md)

[A ListControl (formátum) EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
