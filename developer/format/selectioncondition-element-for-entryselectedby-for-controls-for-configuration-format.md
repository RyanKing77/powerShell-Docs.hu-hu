---
title: SelectionCondition elemet a vezérlők (formátum) konfiguráció EntrySelectedBy |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f23ef405-0f1e-4607-b3f4-4017b7ead106
caps.latest.revision: 7
ms.openlocfilehash: a5098da55d0a63272a121b973cb05e26dc47e3e1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62075766"
---
# <a name="selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format"></a>A Konfiguráció Vezérlők eleméhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)

Határozza meg egy feltételt, amely használt gyakori ellenőrzési definíció léteznie kell. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők Configuration (formátum) CustomEntries elemhez tartozó CustomControl vezérlők, a vezérlő konfigurációja (formátum) CustomControl elemhez Konfiguráció (formátum) CustomEntry elemet a vezérlők, a vezérlők, a Configuration (formátum) SelectionCondition elem esetében a CustomEntry EntrySelectedBy a CustomEntry Configuration (formátum) EntrySelectedBy elemhez CustomControl Konfiguráció (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionCondition` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) vezérlők SelectionCondition PropertyName elem.](./propertyname-element-for-selectioncondition-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-tulajdonság, amely elindítja a feltétel.|
|[Konfiguráció (formátum) vezérlők SelectionCondition ScriptBlock eleme](./scriptblock-element-for-selectioncondition-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Megadja a parancsprogramot, amely elindítja a feltétel.|
|[Konfiguráció (formátum) vezérlők SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> Megadja a .NET-típusok, amely elindítja a feltételt.|
|[Konfiguráció (formátum) vezérlők SelectionCondition TypeName elem.](./typename-element-for-selectioncondition-for-controls-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> A .NET típusát, amely elindítja a feltételt határozza meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)|A .NET-típusokat, amelyek a közös ellenőrzési definícióját a bejegyzés határozza meg.|

## <a name="remarks"></a>Megjegyzés

Kiválasztási feltétel meghatározásakor a következő irányelveket kell követni:

- A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.

- A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.

Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).

## <a name="see-also"></a>Lásd még:

[Konfiguráció (formátum) vezérlők SelectionCondition PropertyName elem.](./propertyname-element-for-selectioncondition-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők SelectionCondition ScriptBlock eleme](./scriptblock-element-for-selectioncondition-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők SelectionCondition SelectionSetName elem.](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők SelectionCondition TypeName elem.](./typename-element-for-selectioncondition-for-controls-for-configuration-format.md)

[Konfiguráció (formátum) vezérlők CustomEntry EntrySelectedBy elem.](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md)

[Egy Windows PowerShell formázás és a fájl típusai](./writing-a-powershell-formatting-file.md)
