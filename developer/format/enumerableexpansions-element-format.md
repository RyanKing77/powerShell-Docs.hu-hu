---
title: EnumerableExpansions elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 50c33892-2ade-44c2-906c-81e5f5ca21f2
caps.latest.revision: 9
ms.openlocfilehash: 1ecbda8a3b623757517019105e3b1ee46ccbb55c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849790"
---
# <a name="enumerableexpansions-element-format"></a>EnumerableExpansions elem (Formátum)

Határozza meg, hogyan .NET gyűjtemény objektumok kibontott nézetben megjelenésekor.

Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<EnumerableExpansions>
  <EnumerableExpansion>...</EnumerableExpansion>
</EnumerableExpansions>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EnumerableExpansions` elemet. Gyermekelemek használható száma nincs korlátozva van.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[EnumerableExpansion elem (formátum)](./enumerableexpansion-element-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg a konkrét .NET gyűjtemény objektumokat, amelyeket a nézetben megjelenésekor bontva.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[DefaultSettings elem (formátum)](./defaultsettings-element-format.md)|Határozza meg a formázási fájl összes nézet vonatkozó általános beállításokat.|

## <a name="remarks"></a>Megjegyzés

Ez az elem gyűjtemény és az objektumok a gyűjtemény megjelenítését meghatározására szolgál. Ebben az esetben a gyűjteményobjektum objektumra hivatkozik, bármely, amely támogatja a **"System.Collections.ICollection"** felületet.

## <a name="see-also"></a>Lásd még:

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
