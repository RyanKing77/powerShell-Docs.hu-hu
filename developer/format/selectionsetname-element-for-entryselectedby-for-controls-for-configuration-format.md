---
title: SelectionSetName elemet a vezérlők (formátum) konfiguráció EntrySelectedBy |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 42143d1e-7cda-4c4a-b568-fa1951bb9417
caps.latest.revision: 6
ms.openlocfilehash: 9060ee54d6f88c7f910b16cf5c9b87f37844b736
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850245"
---
# <a name="selectionsetname-element-for-entryselectedby-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)

Ez a definíció, a vezérlő használó .NET-típusok egy halmazát határozza meg. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a Configuration (formátum) EntrySelectedBy elem CustomEntry vezérlők EntrySelectedBy vezérlők (formátum) konfiguráció esetén a Configuration (formátum) SelectionSetName elemhez tartozó CustomControl

## <a name="syntax"></a>Szintaxis

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.

### <a name="attributes"></a>Attribútumok

Egyik sem

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)|A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.|

## <a name="text-value"></a>Szöveges érték

Adja meg a kijelölt csoport nevét.

## <a name="remarks"></a>Megjegyzés

Minden vezérlő definíció rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.

Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok. Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja a kijelölés](./defining-selection-sets.md).

## <a name="see-also"></a>Lásd még:

[Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
