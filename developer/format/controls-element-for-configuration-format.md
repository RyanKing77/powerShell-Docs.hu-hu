---
title: (Formátum) konfigurációs elem szabályozza |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4d4ef63d-5866-4319-ba00-7ed96de26821
caps.latest.revision: 18
ms.openlocfilehash: ac9f7ff08f6e87ef83b5a2fe23fc58ee2651566d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066872"
---
# <a name="controls-element-for-configuration-format"></a>A Konfiguráció elem Vezérlők eleme (Formátum)

A Gyakori vezérlők, amelyek segítségével az összes nézetben megtekinthetők a formázási fájl határozza meg.

Konfigurációs elem (formátum) vezérlők elem konfiguráció (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Controls>
  <Control>...</Control>
</Controls>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Controls` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Vezérlő elemet a vezérlők konfiguráció (formátum)](./control-element-for-controls-for-configuration-format.md)|Szükséges eleme.<br /><br /> Egy közös vezérlőelem, amelyek segítségével az összes nézetben megtekinthetők a formázási fájl határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfigurációs elem (formátum)](./configuration-element-format.md)|A legfelső szintű elem egy formázási fájl jelöli.|

## <a name="remarks"></a>Megjegyzés

Gyakori vezérlők tetszőleges számú hozhat létre. Az egyes vezérlőelemek neve, amellyel hivatkozni a vezérlő és a vezérlő összetevői kell megadnia.

## <a name="see-also"></a>Lásd még:

[Konfigurációs elem (formátum)](./configuration-element-format.md)

[Vezérlő elemet a vezérlők konfiguráció (formátum)](./control-element-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
