---
title: TypeName elemet a vezérlők (formátum) konfiguráció SelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 477c8711-fffc-4f92-af45-6d4f80990474
caps.latest.revision: 7
ms.openlocfilehash: 60f02f3240c5574e1b1f9027b060bd9af89a11d2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083943"
---
# <a name="typename-element-for-selectioncondition-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó SelectionCondition TypeName eleme (Formátum)

A .NET típusát, amely elindítja a feltételt határozza meg. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők Configuration (formátum) CustomEntries elemhez tartozó CustomControl vezérlők, a vezérlő konfigurációja (formátum) CustomControl elemhez Konfiguráció (formátum) CustomEntry elemet a vezérlők, a vezérlők, a Configuration (formátum) SelectionCondition elem esetében a CustomEntry EntrySelectedBy a CustomEntry Configuration (formátum) EntrySelectedBy elemhez CustomControl Konfiguráció (formátum) TypeName eleme SelectionCondition vezérlők konfiguráció (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<TypeName>Nameof.NetType</TypeName>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[A konfiguráció (formátum) CustomEntry EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)|Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.|

## <a name="text-value"></a>A szöveges érték

Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.

## <a name="remarks"></a>Megjegyzés

## <a name="see-also"></a>Lásd még:

[A konfiguráció (formátum) CustomEntry EntrySelectedBy SelectionCondition elem.](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
