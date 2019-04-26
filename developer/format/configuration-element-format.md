---
title: Konfigurációs elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d46df0cb-50b7-4b81-82ba-37186a7b7a7f
caps.latest.revision: 28
ms.openlocfilehash: 296c63d0c774a0bf56e90dbaa32f2c221d4c3dbd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066821"
---
# <a name="configuration-element-format"></a>Konfigurációs elem (Formátum)

A legfelső szintű elem egy formázási fájl jelöli.

Konfigurációs elem

## <a name="syntax"></a>Szintaxis

```xml
<Configuration>
  <DefaultSettings>...</DefaultSettings>
  <SelectionSets>...</SelectionSets>
  <Controls>...</Controls>
  <ViewDefinitions>...</ViewDefinitions>
</Configuration>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Configuration` elemet. Ez az elemnek kell lennie a gyökérelem formázási fájl esetében, és ezt az elemet tartalmaznia kell legalább egy gyermekelemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[Vezérlők elemet a konfigurációs (formátum)](./controls-element-for-configuration-format.md)|Nem kötelező eleme.<br /><br /> A Gyakori vezérlők, amelyek segítségével az összes nézetben megtekinthetők a formázási fájl határozza meg.|
|[DefaultSettings elem (formátum)](./defaultsettings-element-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg a formázási fájl összes nézet vonatkozó általános beállításokat.|
|[SelectionSets elem formátuma](./selectionsets-element-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg a gyakori eljárások egyikét a formázási fájl összes nézetek által használható .NET-objektumokat.|
|[ViewDefinitions elem (formátum)](./viewdefinitions-element-format.md)|Nem kötelező eleme.<br /><br /> Határozza meg az objektumokat megjelenítő nézetek.|

### <a name="parent-elements"></a>Szülőelemek

Nincs.

## <a name="remarks"></a>Megjegyzés

Formázási fájlokat adja meg, hogyan jelennek meg objektumok. A legtöbb esetben a legfelső szintű elem tartalmaz egy [ViewDefinitions](./viewdefinitions-element-format.md) elem, amely meghatározza a táblázat, lista és a formázási fájl széles nézetek. A nézetdefiníciókból mellett a formázási fájl határozhatja meg közös kijelölt csoportok, a beállításokat és a vezérlőket, amellyel adott nézeteket létrehozták.

## <a name="see-also"></a>Lásd még:

[Vezérlők elemet a konfigurációs (formátum)](./controls-element-for-configuration-format.md)

[DefaultSettings elem (formátum)](./defaultsettings-element-format.md)

[SelectionSets elem (formátum)](./selectionsets-element-format.md)

[ViewDefinitions elem (formátum)](./viewdefinitions-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
