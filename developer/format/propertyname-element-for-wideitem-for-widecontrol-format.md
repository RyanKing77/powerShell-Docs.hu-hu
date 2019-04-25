---
title: WideItem WideControl (formátum) a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3d91d0e6-bf18-4587-b651-db66849e5df5
caps.latest.revision: 6
ms.openlocfilehash: 326880834cd82ab826aadc409cd7a8f21cd36824
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064645"
---
# <a name="propertyname-element-for-wideitem-for-widecontrol-format"></a>A WideControl WideItem elemének PropertyName eleme (Formátum)

Itt adhatja meg a tulajdonság az objektum, amelynek az értéke az széles nézetben jelenik meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) WideItem elem (formátum) PropertyName eleme WideItem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `PropertyName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[WideItem elem (formátum)](./wideitem-element-for-widecontrol-format.md)|Határozza meg, tulajdonság vagy parancsfájl, amelynek az értéke az széles nézetben jelenik meg.|

## <a name="text-value"></a>A szöveges érték

Adja meg, amelynek értéke megjelenik a tulajdonság nevét.

## <a name="remarks"></a>Megjegyzés

Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja egy széles nézet, amely a Folyamatnév tulajdonságának értékét jeleníti meg a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.

```xml
View>
  <Name>process</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <WideControl>
    <WideEntries>
      <WideEntry>
        <WideItem>
          <PropertyName>ProcessName</PropertyName>
        </WideItem>
      </WideEntry>
    </WideEntries>
  </WideControl>
</View>

```

## <a name="see-also"></a>Lásd még:

[WideItem elem (formátum)](./wideitem-element-for-widecontrol-format.md)

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
