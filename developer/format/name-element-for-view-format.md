---
title: Elem name (formátum) nézet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3a31010d-1db9-44ae-a7f3-6ed32cb641cb
caps.latest.revision: 16
ms.openlocfilehash: 097d20cb6a04635124d1f96823248df6095ca1af
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849265"
---
# <a name="name-element-for-view-format"></a>A Nézet Név eleme (Formátum)

Itt adhatja meg, amely azonosítja a nézet nevét.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem Name elemet (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Name>ViewName</Name>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Name` elemet. Csak egy `Name` elem engedélyezett-e meg.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet elem (formátum)](./view-element-format.md)|Meghatározza egy nézetet, amely legalább egy .NET-objektumokká tagjai megjelenítésére szolgál.|

## <a name="text-value"></a>Szöveges érték

Adjon meg egy egyedi rövid nevet a nézetet. Ez a név tartalmazhat egy hivatkozást a nézet (például egy táblázat vagy lista nézetben), mely objektum vagy objektumcsoport használja a nézetet, mely a parancs visszaadja az objektumokat, vagy ezek kombinációja típusát.

## <a name="remarks"></a>Megjegyzés

A nézetek különböző típusú kapcsolatos további információkért lásd: a következő témaköröket: [Tábla nézet](./creating-a-table-view.md), [listanézet](./creating-a-list-view.md), [széles nézet](./creating-a-wide-view.md), és [egyéni nézet](./creating-custom-controls.md).

## <a name="example"></a>Példa

A következő példa bemutatja egy `View` elem, amely meghatározza a táblázatos nézetre a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum. A nézet neve "szolgáltatás".

```xml
<View>
  <Name>service</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <TableControl>...</TableControl>
</View>

```

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[Tábla nézet létrehozása](./creating-a-table-view.md)

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[Egyéni vezérlők létrehozását](./creating-custom-controls.md)

[Nézet elem (formátum)](./view-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
