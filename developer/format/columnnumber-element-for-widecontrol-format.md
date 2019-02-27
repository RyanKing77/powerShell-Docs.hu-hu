---
title: (Formátum) WideControl ColumnNumber eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fe9eb5f9-a193-41a4-ad47-a96ba3f8d7e3
caps.latest.revision: 8
ms.openlocfilehash: 49f501538b8f72777984a5e575b999866abcdebf
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846969"
---
# <a name="columnnumber-element-for-widecontrol-format"></a>A WideControl ColumnNumber eleme (Formátum)

A széles nézet oszlopainak számát adja meg.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) ColumnNumber eleme WideControl (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ColumnNumber>PositiveInteger</ColumnNumber>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ColumnNumber` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[WideControl elem (formátum)](./widecontrol-element-format.md)|A wide (egyetlen érték) határozza meg a Nézet formátuma.|

## <a name="text-value"></a>Szöveges érték

Adjon meg egy pozitív egész értéket.

## <a name="remarks"></a>Megjegyzés

Egy széles nézet meghatározásakor adhat hozzá a `AutoSize` elem vagy a `ColumnNumber` elem, de mindkettő nem adható hozzá.

Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).

Egy széles nézet egy példa: [széles nézet (alapszintű)](./wide-view-basic.md).

## <a name="see-also"></a>Lásd még:

[Automatikus méretezés eleme WideControl (formátum)](./autosize-element-for-widecontrol-format.md)

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[Széles nézet (alapszintű)](./wide-view-basic.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
