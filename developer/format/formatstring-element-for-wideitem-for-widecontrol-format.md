---
title: WideItem WideControl (formátum) a FormatString eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5bc6ea26-3ca6-4bab-8a13-29189821ba15
caps.latest.revision: 7
ms.openlocfilehash: a1dc145864a6904fd4af6c3b9187819c49e224b0
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065682"
---
# <a name="formatstring-element-for-wideitem-for-widecontrol-format"></a>A WideControl WideItem elemének FormatString eleme (Formátum)

Meghatározza formátumú mintát, amely meghatározza, hogy a tulajdonság vagy parancsfájl érték hogyan jelenjen meg a nézetben.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem WideControl (formátum) FormatString elemhez (formátum) WideControl WideItem elemhez a WideItem a WideControl (formátum)

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
|[WideItem eleme WideControl (formátum)](./wideitem-element-for-widecontrol-format.md)|A tulajdonság, vagy a parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határoz meg.|

## <a name="text-value"></a>A szöveges érték

Adja meg az adatok formázásához használt mintáját. Például használhatja ezt a mintát bármilyen típusú tulajdonság értékének [System.Timespan](/dotnet/api/System.TimeSpan): {0: MMM} {0:dd} {0:HH}: {0:mm}.

## <a name="remarks"></a>Megjegyzés

Formázási karakterláncokat is használható, nézetek, nézetek, széles nézetek vagy az egyéni nézetek létrehozása során. További információ a nézetben megjelenített érték formázása: [megjelenített adatok formázása](./formatting-displayed-data.md).

A széles körű nézetekben formázási karakterláncokat használatával kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.

```xml
<WideItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</WideItem>
```

## <a name="see-also"></a>Lásd még:

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[WideItem eleme WideControl (formátum)](./wideitem-element-for-widecontrol-format.md)

[Egy Windows PowerShell formázás és a fájl típusai](./writing-a-powershell-formatting-file.md)
