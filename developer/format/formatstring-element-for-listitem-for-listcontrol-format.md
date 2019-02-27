---
title: Listaelem ListControl (formátum) a FormatString eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fd2cac66-88bb-449f-9d47-bd2cd4fe1801
caps.latest.revision: 13
ms.openlocfilehash: e6024ec4f7fc490c92408047c8c15c775e45bf9d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849846"
---
# <a name="formatstring-element-for-listitem-for-listcontrol--format"></a>A ListControl ListItem eleméhez tartozó FormatString elem (Formátum)

Itt adhatja meg, amely meghatározza, hogyan jelenjen meg a tulajdonság vagy parancsfájl érték formátuma mintát.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem ListControl (formátum) ListEntry elem ListControl (formátum) ListItems elemek elemhez tartozó ListControl (formátum) Listaelem eleme ListItem ListControl (formátum) a FormatString eleme ListControl (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<FormatString>PropertyPattern</FormatString>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `FormatString` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Listaelem elem (formátum)](./listitem-element-for-listitems-for-listcontrol-format.md)|A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.|

## <a name="text-value"></a>Szöveges érték

Adja meg az adatok formázásához használt mintáját. Például használhatja ezt a mintát bármilyen típusú tulajdonság értékének [System.Timespan](/dotnet/api/System.TimeSpan): {0: MMM} {0:dd} {0:HH}: {0:mm}.

## <a name="remarks"></a>Megjegyzés

Formázási karakterláncokat is használható, nézetek, nézetek, széles nézetek vagy az egyéni nézetek létrehozása során. További információ a nézetben megjelenített érték formázása: [megjelenített adatok formázása](./formatting-displayed-data.md).

Listanézetek a formázási karakterláncokat használatával kapcsolatos további információkért lásd: [lista nézet létrehozása](./creating-a-list-view.md).

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.

```xml
<ListItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</ListItem>
```

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[Listaelem elem (formátum)](./listitem-element-for-listitems-for-listcontrol-format.md)

[Egy Windows PowerShell formázás és a fájl típusai](./writing-a-powershell-formatting-file.md)
