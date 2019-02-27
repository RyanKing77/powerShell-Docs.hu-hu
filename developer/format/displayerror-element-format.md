---
title: DisplayError elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 45c45800-a87d-456e-b07c-12d4d8c27c67
caps.latest.revision: 8
ms.openlocfilehash: 431e5d8407b9f689a5224b329d8c7b52802e19e1
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846052"
---
# <a name="displayerror-element-format"></a>DisplayError elem (Formátum)

Itt adhatja meg, hogy a karakterlánc #ERR megjelenik-e, ha hiba történik az adatok megjelenítése.

Konfigurációs elem (formátum) DefaultSettings elem (formátum) DisplayError elem (Frmat)

## <a name="syntax"></a>Szintaxis

```xml
<DisplayError/>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `DisplayError` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[DefaultSettings elem (formátum)](./defaultsettings-element-format.md)|Határozza meg a formázási fájl összes nézet vonatkozó általános beállításokat.|

## <a name="remarks"></a>Megjegyzés

Alapértelmezés szerint az adatok, megjelenítése közben hiba esetén az adatok helye üres. Ha ez az elem értéke igaz, a #ERR karakterlánc jelenik meg.

## <a name="see-also"></a>Lásd még:

[DefaultSettings elem (formátum)](./defaultsettings-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
