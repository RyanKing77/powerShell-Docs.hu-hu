---
title: Automatikus méretezés eleme WideControl (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: def37479-7b6e-40cf-bc81-0f7cbc651b31
caps.latest.revision: 11
ms.openlocfilehash: 6dbaef5886a0600bd9fe96dbc8d21f00a674dfcf
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066923"
---
# <a name="autosize-element-for-widecontrol-format"></a>A WideControl AutoSize eleme (Formátum)

Itt adhatja meg, hogy az oszlop méretét és az oszlopok számát módosulnak az adatok mérete alapján.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) Autosize eleme WideControl (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<AutoSize/>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `AutoSize` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Egyik sem

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[WideControl elem (formátum)](./widecontrol-element-format.md)|A wide (egyetlen érték) határozza meg a Nézet formátuma.|

## <a name="remarks"></a>Megjegyzés

Egy széles nézet meghatározásakor adhat hozzá a `AutoSize` elem vagy a [ColumnNumber](./columnnumber-element-for-widecontrol-format.md) elem, de mindkettő nem adható hozzá.

Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).

Egy széles nézet egy példa: [széles nézet (alapszintű)](./wide-view-basic.md).

## <a name="see-also"></a>Lásd még:

[ColumnNumber eleme WideControl (formátum)](./columnnumber-element-for-widecontrol-format.md)

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[WideControl elem (formátum)](./widecontrol-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
