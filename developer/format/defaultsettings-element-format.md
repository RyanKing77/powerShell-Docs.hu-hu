---
title: DefaultSettings elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 41c56499-ee20-4821-830a-478fdcc33f83
caps.latest.revision: 11
ms.openlocfilehash: bc95c62222eb2806f92499257a397c2e4ec5dbab
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059065"
---
# <a name="defaultsettings-element-format"></a>DefaultSettings elem (Formátum)

Határozza meg a formázási fájl összes nézet vonatkozó általános beállításokat. Általános beállítások közé tartozik a hibák megjelenítése a táblákat, hogyan gyűjtemények vannak bontva, definiálása, valamint további lehetőségek szöveg.

Konfigurációs elem (formátum) DefaultSettings elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<DefaultSettings>
  <ShowError/>
  <DisplayError/>
 <PropertyCountForTable>NumberOfProperties</PropertyCountFortable>
  <WrapTables/>
  <EnumerableExpansions>...</EnumerableExpansions>
</DefaultSettings>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `DefaultSettings` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[DisplayError elem (formátum)](./displayerror-element-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg, hogy a karakterlánc #ERR megjelenik-e, ha hiba történik az adatok megjelenítése közben.|
|[EnumerableExpansions elem (formátum)](./enumerableexpansions-element-format.md)|Nem kötelező eleme.<br /><br /> Meghatározza a .NET-vannak bontva, amikor a nézetben megjelenített objektumok különböző lehetőségeket.|
|[PropertyCountForTable (formátum)](./propertycountfortable-element-format.md)|Nem kötelező eleme.<br /><br /> Meghatározza, hogy az objektum táblázatos nézetre az objektum megjelenítendő tulajdonságai minimális számát.|
|[ShowError elem (formátum)](./showerror-element-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg, hogy megjelenik-e a teljes rekordot, ha hiba történik az adatok megjelenítése közben.|
|[WrapTables elem (formátum)](./wraptables-element-format.md)|Nem kötelező eleme.<br /><br /> Itt adhatja meg, hogy a tábla adatainak áthelyezése a következő sorra, ha az oszlop szélessége nem illik-e.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Konfigurációs elem](./configuration-element-format.md)|A legfelső szintű elem egy formázási fájl jelöli.|

## <a name="remarks"></a>Megjegyzés

## <a name="see-also"></a>Lásd még:

[Konfigurációs elem](./configuration-element-format.md)

[DisplayError elem (formátum)](./displayerror-element-format.md)

[EnumerableExpansions elem (formátum)](./enumerableexpansions-element-format.md)

[PropertyCountForTable (formátum)](./propertycountfortable-element-format.md)

[ShowError elem (formátum)](./showerror-element-format.md)

[WrapTables elem (formátum)](./wraptables-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
