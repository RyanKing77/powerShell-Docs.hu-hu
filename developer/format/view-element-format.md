---
title: (Formátum) elem megtekintése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d837d5d4-ed2e-4d84-a306-0b5d2ad2d0bf
caps.latest.revision: 24
ms.openlocfilehash: 2361c1117757569bef0815018c75764430a9e7a8
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846913"
---
# <a name="view-element-format"></a>Nézet elem (Formátum)

Legalább egy .NET-objektumokat megjelenítő nézet határozza meg. Formázási-fájlban definiált nézetek száma nincs korlátozva van.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<View>
  <Name>Friendly name of view.</Name>
  <ViewSelectedBy>...</ViewSelectedBy>
  <Controls>...</Controls>
  <GroupBy>...</GroupBy>
  <TableControl>...</TableControl>
  <ListControl>...</ListControl>
  <WideControl>...</WideControl>
  <CustomControl>...</CustomControl>
</View>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `View` elemet. Meg kell adnia az egyiket a vezérlő gyermekelemek, és meg kell adnia a nézet és az objektumok, amelyek a nézet nevét. Egyéni vezérlők meghatározása, hogyan csoportosítsa objektumokat, és ha a nézet-e a sávon kívüli megadása nem kötelező.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Vezérlők elem nézet (formátum)](./controls-element-for-view-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg, hogy a nézet belül vezérlőelemére név szerint lehet hivatkozni.|
|[CustomControl elem (formátum)](./customcontrol-element-for-groupby-format.md)|Nem kötelező eleme.<br /><br /> A nézet egy egyéni vezérlő formátumát határozza meg.|
|[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg, hogy a .NET-objektumok tagjai vannak csoportosítva.|
|[ListControl elem (formátum)](./listcontrol-element-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg a nézet lista formájában.|
|[Name elemet a nézet (formátum)](./name-element-for-view-format.md)|Szükséges eleme.<br /><br /> Megadja a mutató hivatkozás a nézet nevét.|
|[TableControl elem (formátum)](./tablecontrol-element-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg a nézet táblázatos formában.|
|[ViewSelectedBy elem nézet (formátum)](./viewselectedby-element-format.md)|Szükséges eleme.<br /><br /> Határozza meg, hogy ez a nézet jeleníti meg a .NET-objektumokat.|
|[WideControl elem (formátum)](./widecontrol-element-format.md)|Nem kötelező eleme.<br /><br /> A wide (egyetlen érték) határozza meg a Nézet formátuma.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[ViewDefinitions elem (formátum)](./viewdefinitions-element-format.md)|Határozza meg az objektumokat megjelenítő nézetek.|

## <a name="remarks"></a>Megjegyzés

A különböző nézetek és az egyéni vezérlők az összetevőivel kapcsolatos további információkért lásd a következő témaköröket:

- [Tábla nézet összetevők](./creating-a-table-view.md)

- [Lista nézet összetevők](./creating-a-list-view.md)

- [Széles nézet összetevők](./creating-a-wide-view.md)

- [Egyéni vezérlők](./creating-custom-controls.md)

## <a name="example"></a>Példa

Ez a példa bemutatja egy `View` elem, amely meghatározza a táblázatos nézetre a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum.

```xml
<ViewDefinitions>
  <View>
    <Name>service</Name>
    <ViewSelectedBy>
      <TypeName>System.ServiceProcess.ServiceController</TypeName>
    </ViewSelectedBy>
    <TableControl>...</TableControl>
  </View>
</ViewDefinitions>

```

## <a name="see-also"></a>Lásd még:

[ViewDefinitions elem (formátum)](./viewdefinitions-element-format.md)

[Name elemet a nézet (formátum)](./name-element-for-view-format.md)

[ViewSelectedBy elem (formátum)](./viewselectedby-element-format.md)

[Vezérlők elem nézet (formátum)](./controls-element-for-view-format.md)

[GroupBy elem nézet (formátum)](./groupby-element-for-view-format.md)

[TableControl elem (formátum)](./tablecontrol-element-format.md)

[ListControl elem (formátum)](./listcontrol-element-format.md)

[WideControl elem (formátum)](./widecontrol-element-format.md)

[CustomControl elem (formátum)](./customcontrol-element-for-groupby-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
