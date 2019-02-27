---
title: Bontsa ki az elemet (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: faa0314b-f6f1-44fd-ad2b-b00cbe38923f
caps.latest.revision: 9
ms.openlocfilehash: 8b924c989133b47e4d95d8429778003c76595d58
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848614"
---
# <a name="expand-element-format"></a>Elem kibontása (Formátum)

Itt adhatja meg, hogyan az objektum ki van bontva, a definíció.

Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) bontsa ki az elemet (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<Expand>EnumOnly, CoreOnly, Both</Expand>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Expand` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[EnumerableExpansion elem (formátum)](./enumerableexpansion-element-format.md)|Határozza meg, hogyan adott .NET gyűjtemény objektumok kibontott nézetben megjelenésekor.|

## <a name="text-value"></a>Szöveges érték

Adja meg a következő értékek egyikét:

- EnumOnly: Megjeleníti a gyűjtemény csak az objektumok tulajdonságait.

- CoreOnly: Csak az objektum tulajdonságait jeleníti meg.

- Mindkettő: A gyűjtemény és az objektum tulajdonságait jeleníti meg az objektumok tulajdonságait.

## <a name="remarks"></a>Megjegyzés

Ez az elem gyűjtemény és az objektumok a gyűjtemény megjelenítését meghatározására szolgál. Ebben az esetben a gyűjteményobjektum objektumra hivatkozik, bármely, amely támogatja a **"System.Collections.ICollection"** felületet.

Az alapértelmezett viselkedést, hogy csak az objektumok tulajdonságait megjeleníti a gyűjteményben.

## <a name="see-also"></a>Lásd még:

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
