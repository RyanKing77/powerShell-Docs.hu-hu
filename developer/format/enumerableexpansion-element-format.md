---
title: EnumerableExpansion elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 93d27173-9ae4-46e5-bb78-90525915cd70
caps.latest.revision: 9
ms.openlocfilehash: bc1e58c00ca8419f9204076f0a46050281e704db
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847396"
---
# <a name="enumerableexpansion-element-format"></a>EnumerableExpansion elem (Formátum)

Határozza meg, hogyan adott .NET gyűjtemény objektumok kibontott nézetben megjelenésekor.

Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<EnumerableExpansion>
  <EntrySelectedBy>...</EntrySelectedBy>
  <Expand>EnumOnly, CoreOnly, Both</Expand>
</EnumerableExpansion>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EnumerableExpansion` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[EntrySelectedBy eleme EnumerableExpansion (formátum)](./entryselectedby-element-for-enumerableexpansion-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg, melyik gyűjtemény .NET-objektumokat a definíció szerint bontva.|
|[Bontsa ki az elemet (formátum)](./expand-element-format.md)|Itt adhatja meg, hogyan az objektum ki van bontva, a definíció.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[EnumerableExpansions elem (formátum)](./enumerableexpansions-element-format.md)|Határozza meg a különböző módokon objektumok kibontott nézetben megjelenésekor .NET gyűjteménynek.|

## <a name="remarks"></a>Megjegyzés

Ez az elem gyűjtemény és az objektumok a gyűjtemény megjelenítését meghatározására szolgál. Ebben az esetben a gyűjteményobjektum objektumra hivatkozik, bármely, amely támogatja a **"System.Collections.ICollection"** felületet.

Az alapértelmezett viselkedést, hogy csak az objektumok tulajdonságait megjeleníti a gyűjteményben.

## <a name="see-also"></a>Lásd még:

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
