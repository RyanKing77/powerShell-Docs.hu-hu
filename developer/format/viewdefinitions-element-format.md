---
title: ViewDefinitions elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 29840c10-2b30-4bb1-a8a0-ddf84d19c2d0
caps.latest.revision: 18
ms.openlocfilehash: c5ec80350c7707ccd41112ab5e1952e5dc198cca
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851071"
---
# <a name="viewdefinitions-element-format"></a>ViewDefinitions elem (Formátum)

A .NET-objektumokat megjelenítő nézetek határozza meg. Ezek a nézetek megjelenítheti a tulajdonságok és parancsfájl-értékek az objektum egy táblázatos formátumú, listaformátumban, széles és egyéni vezérlő formátumban.

Konfigurációs elem (formátum) ViewDefinitions (XML formátum) elem

## <a name="syntax"></a>Szintaxis

```xml

<ViewDefinitions>
  <View>...</View>
</ViewDefinitions>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `ViewDefinitions` elemet. Nem korlátozott a formázási-fájlban definiált nézetek számát, és bármilyen sorrendben követően adhatók hozzá.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet elem (formátum)](./view-element-format.md)|Meghatározza egy nézetet, amely legalább egy .NET-objektumokká megjelenítésére szolgál.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfigurációs elem (formátum)](./configuration-element-format.md)|A legfelső szintű elem egy formázási fájl jelöli.|

## <a name="remarks"></a>Megjegyzés

A nézetek különböző típusainak összetevőivel kapcsolatos további információkért lásd a következő témaköröket:

- [Tábla nézet létrehozása](./creating-a-table-view.md)

- [Lista nézet létrehozása](./creating-a-list-view.md)

- [Egy széles nézet létrehozása](./creating-a-wide-view.md)

- [Egyéni vezérlők](./creating-custom-controls.md)

## <a name="example"></a>Példa

Ez a példa bemutatja egy `ViewDefinitions` elem, amely a táblázatos nézetre, és megjelenítheti a szülő elemeket tartalmazza.

```xml
<Configuration>
  <ViewDefinitions>
    <View>
      <TableControl>...</TableControl>
    </View>
    <View>
      <ListControl>...</ListControl>
    </View>
  </ViewDefinitions>
</Configuration>
```

## <a name="see-also"></a>Lásd még:

[Konfigurációs elem (formátum)](./configuration-element-format.md)

[Nézet elem (formátum)](./view-element-format.md)

[Tábla nézet létrehozása](./creating-a-table-view.md)

[Lista nézet létrehozása](./creating-a-list-view.md)

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[Egyéni vezérlők](./creating-custom-controls.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
