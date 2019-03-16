---
title: Séma XML-hivatkozása formázása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ac6f7aaa-d0cc-4c7b-a341-85e736174579
caps.latest.revision: 21
ms.openlocfilehash: 437b3d6bb62fdd3a74f3392ec71df360c01a1974
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58056651"
---
# <a name="format-schema-xml-reference"></a>Séma XML-referenciájának formázása

Ez a szakasz témakörei ismertetik a formázás fájlok (Format.ps1xml) által használt XML-elemeket. Formázási fájlok határozza meg, hogyan jelenik meg a .NET-objektum; maga az objektum nem módosítják a.

## <a name="in-this-section"></a>A szakasz tartalma

[Zarovnání eleme TableColumnHeader TableControl (formátum) a](./alignment-element-for-tablecolumnheader-for-tablecontrol-format.md) határozza meg, hogyan jelenjen meg az adatok egy oszlopfejlécre.

[Zarovnání eleme TableColumnItem TableControl (formátum) a](./alignment-element-for-tablecolumnitem-for-tablecontrol-format.md) határozza meg, hogyan jelenjen meg az adatokat a sorban.

[Automatikus méretezés eleme TableControl (formátum)](./autosize-element-for-tablecontrol-format.md) e igazított oszlop méretét és az oszlopok számát az adatok mérete alapján határozza meg.

[Automatikus méretezés eleme WideControl (formátum)](./autosize-element-for-widecontrol-format.md) e igazított oszlop méretét és az oszlopok számát az adatok mérete alapján határozza meg.

[(Formátum) WideControl ColumnNumber eleme](./columnnumber-element-for-widecontrol-format.md) a széles nézet oszlopainak számát adja meg.

[Konfigurációs elem (formátum)](./configuration-element-format.md) a legfelső szintű elem a formázási fájlt jelöli.

[Szabályozhatja a vezérlők (formátum) konfigurációs elemet](./control-element-for-controls-for-configuration-format.md) határozza meg egy közös ellenőrzés, hogy a formázási fájlja és a neve, amellyel hivatkozni a vezérlőelem összes nézet is lehet.

[Szabályozhatja a vezérlők megjelenítéséhez (formátum) elem](./control-element-for-controls-for-view-format.md) határozza meg olyan vezérlő, amely a nézet és a neve, amellyel hivatkozni a vezérlő által használható.

[Azt szabályozza, (formátum) konfigurációs elemet](./controls-element-for-configuration-format.md) a Gyakori vezérlők, amelyek segítségével az összes nézetben megtekinthetők a formázási fájl határozza meg.

[Azt szabályozza, nézet (formátum) elem](./controls-element-for-view-format.md) határozza meg a nézet szabályozza, hogy egy adott nézet is lehet.

[Konfiguráció (formátum) vezérlőelem CustomControl elem](./customcontrol-element-for-control-for-controls-for-configuration-format.md) határozza meg olyan vezérlő. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[Vezérlő (formátum) nézet vezérlők CustomControl elem](./customcontrol-element-for-control-for-controls-for-view-format.md) határozza meg olyan vezérlő, amely a nézetet használja.

[GroupBy (formátum) CustomControl eleme](./customcontrol-element-for-groupby-format.md) határozza meg az egyéni vezérlő, amely megjeleníti az új csoport.

[CustomControl elem (formátum)](./customcontrol-element-for-groupby-format.md) határozza meg a nézet egy egyéni vezérlő formátumát.

[CustomControlName elemet a vezérlők (formátum) konfiguráció ExpressionBinding](./customcontrolname-element-for-expressionbinding-for-controls-for-configuration-format.md) közös vezérlő nevét adja meg. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[CustomControlName elemet a vezérlők (formátum) nézet ExpressionBindine](./customcontrolname-element-for-expressionbinding-for-controls-for-view-format.md) egy közös vezérlőelem vagy a nézet nevét adja meg. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[GroupBy (formátum) CustomControlName eleme](./customcontrolname-element-for-groupby-format.md) egyéni vezérlőt, amellyel megjelenjen az új csoport nevét adja meg. Ez az elem szolgál egy táblázat, lista, szélesre vagy egyéni vezérlő nézetében meghatározásakor.

[CustomEntry elemet a vezérlők (formátum) konfiguráció CustomControl](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md) nyújt a közös ellenőrzési meghatározását. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[CustomEntry elemet a vezérlők (formátum) nézet CustomEntries](./customentry-element-for-customentries-for-controls-for-view-format.md) biztosít egy definíciót ovládacího prvku. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[CustomEntry elemet a nézet (formátum) CustomEntries](./customentry-element-for-customentries-for-customcontrol-for-view-format.md) biztosít az egyéni vezérlő nézet definíciójának.

[A GroupBy (formátum) CustomControl CustomEntry eleme](./customentry-element-for-customcontrol-for-groupby-format.md) ovládacího prvku definici biztosít. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[Konfiguráció (formátum) CustomControl CustomEntries eleme](./customentries-element-for-customcontrol-for-controls-for-configuration-format.md) a közös ellenőrzési definícióit tartalmazza. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[CustomEntries elemet a vezérlők (formátum) nézet CustomControl](./customentries-element-for-customcontrol-for-controls-for-view-format.md) a vezérlő definícióit tartalmazza. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[A GroupBy (formátum) CustomControl CustomEntries eleme](./customentries-element-for-customcontrol-for-groupby-format.md) a vezérlő definícióit tartalmazza. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[CustomEntries elemet a nézet (formátum) CustomControl](./customentries-element-for-customcontrol-for-view-format.md) biztosít az egyéni vezérlő nézet definíciói. Az egyéni vezérlő nézetében meg kell adnia egy vagy több definíciót.

[CustomItem elemet a vezérlők, a konfigurációhoz CustomEntry](./customitem-element-for-customentry-for-controls-for-configuration-format.md) határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[CustomItem elemet a vezérlők (formátum) nézet CustomEntry](./customitem-element-for-customentry-for-controls-for-view-format.md) határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[CustomItem elemet a nézet (formátum) CustomEntry](./customitem-element-for-customentry-for-customcontrol-for-view-format.md) határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[A GroupBy (formátum) CustomEntry CustomItem eleme](./customitem-element-for-customentry-for-groupby-format.md) határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[DefaultSettings elem (formátum)](./defaultsettings-element-format.md) határozza meg a formázási fájl összes nézet vonatkozó általános beállításokat. Általános beállítások közé tartozik a hibák megjelenítése a táblákat, hogyan gyűjtemények vannak bontva, definiálása, valamint további lehetőségek szöveg.

[DisplayError elem (formátum)](./displayerror-element-format.md) Megadja, hogy a karakterlánc #ERR megjelenik-e, ha hiba történik az adatok megjelenítése.

[EntrySelectedBy elemet a vezérlők (formátum) konfiguráció CustomEntry](./entryselectedby-element-for-customentry-for-controls-for-configuration-format.md) határozza meg a .NET-típusokat, amelyek a közös vezérlő vagy a feltétellel, hogy léteznie kell a Pro tento ovládací prvek használandó definíciója. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[EntrySelectedBy elemet a vezérlők (formátum) nézet CustomEntry](./entryselectedby-element-for-customentry-for-controls-for-view-format.md) határozza meg a .NET-típusokat, amelyek a vezérlő definition vagy a feltételt, amelyet a definíció használandó léteznie kell. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[EntrySelectedBy elemet a nézet (formátum) CustomEntry](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md) határozza meg a .NET-típusokat, amelyek egyéni tételhez vagy a feltétellel, hogy a bejegyzés használandó léteznie kell.

[(Formátum) EnumerableExpansion EntrySelectedBy eleme](./entryselectedby-element-for-enumerableexpansion-format.md) határozza meg a .NET-típusokat, amelyek a definition vagy a feltételt, amelyet a definíció használandó léteznie kell.

[A GroupBy (formátum) CustomEntry EntrySelectedBy eleme](./entryselectedby-element-for-customentry-for-groupby-format.md) határozza meg a .NET-típusokat, amelyek a vezérlő definition vagy a feltételt, amelyet a definíció használandó léteznie kell. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[ListControl (formátum) a ListEntry EntrySelectedBy eleme](./entryselectedby-element-for-listentry-for-listcontrol-format.md) határozza meg a .NET-típusokat, amelyek a lista nézetdefinícióban, illetve a feltételt, amelyet a definíció használandó léteznie kell. A legtöbb esetben csak egyetlen definíciót lista nézetben van szükség. Azonban a listanézet víc definic biztosít, ha azt szeretné használni a ugyanabban listanézetet jelennek meg a különböző objektumok különböző adatok.

[(Formátum) TableRowEntry EntrySelectedBy eleme](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md) határozza meg a .NET-típusokat, melynek tulajdonság értékei jelennek meg a sorban.

[(Formátum) WideEntry EntrySelectedBy eleme](./entryselectedby-element-for-wideentry-format.md) határozza meg a .NET-típusokat, amelyek a definíció az széles nézet vagy a feltételt, amelyet a definíció használandó léteznie kell.

[EnumerableExpansion elem (formátum)](./enumerableexpansion-element-format.md) objektumok kibontott nézetben megjelenésekor egyes .NET gyűjteményt határozza meg.

[EnumerableExpansions elem (formátum)](./enumerableexpansions-element-format.md) határozza meg, hogyan .NET gyűjtemény objektumok kibontott nézetben megjelenésekor.

[EnumerateCollection elemet a vezérlők (formátum) konfiguráció ExpressionBinding](./enumeratecollection-element-for-expressionbinding-for-controls-for-configuration-format.md) , hogy az elemek a gyűjtemények jelennek meg a vezérlő által megadott. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[EnumerateCollection elemet a vezérlők (formátum) nézet ExpressionBinding](./enumeratecollection-element-for-expressionbinding-for-controls-for-view-format.md) megadott jelennek meg, hogy a gyűjtemény elemeit. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[Kifejezés kötelező érvényű, a nézet (formátum) CustomControl EnumerateCollection elem](./enumeratecollection-element-for-expressionbinding-for-customcontrol-for-view-format.md) Megadja, hogy megjelenik-e a gyűjtemény elemei. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[A GroupBy (formátum) ExpressionBinding EnumerateCollection eleme](./enumeratecollection-element-for-expressionbinding-for-groupby-format.md) Megadja, hogy megjelenik-e a gyűjtemény elemei. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[Bontsa ki az elemet (formátum)](./expand-element-format.md) Itt adhatja meg, hogyan az objektum ki van bontva, a definíció.

[ExpressionBinding elemet a vezérlők (formátum) konfiguráció CustomItem](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md) definiálja a vezérlő által megjelenített adatokat. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[ExpressionBinding elemet a vezérlők (formátum) nézet CustomItem](./expressionbinding-element-for-customitem-for-controls-for-view-format.md) definiálja a vezérlő által megjelenített adatokat. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[A nézet (formátum) CustomControl CustomItem ExpressionBinding eleme](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md) definiálja a vezérlő által megjelenített adatokat. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[A GroupBy (formátum) CustomItem ExpressionBinding eleme](./expressionbinding-element-for-customitem-for-groupby-format.md) definiálja a vezérlő által megjelenített adatokat. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[Keret (formátum) konfiguráció vezérlők FirstLineHanging elem](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md) megadja a bal oldali adatok első sora úgy, hogy hány karakter. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[Keret a vezérlőelemek a nézet (formátum) FirstLineHanging elem](./firstlinehanging-element-for-frame-for-controls-for-view-format.md) megadja a bal oldali adatok első sora úgy, hogy hány karakter. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[Nézet (formátum) CustomControl-keret FirstLineHanging elem](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md) megadja a bal oldali adatok első sora úgy, hogy hány karakter. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[GroupBy (formátum)-keret FirstLineHanging elem](./firstlinehanging-element-for-frame-for-groupby-format.md) megadja a bal oldali adatok első sora úgy, hogy hány karakter. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[Keret (formátum) konfiguráció vezérlők FirstLineIndent elem](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md) megadja az adatok első sorának jobb úgy, hogy hány karakter. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[Keret a vezérlőelemek a nézet (formátum) FirstLineIndent elem](./firstlineindent-element-for-frame-for-controls-for-view-format.md) megadja az adatok első sorának jobb úgy, hogy hány karakter. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[FirstLineIndent elem](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md) megadja az adatok első sorának jobb úgy, hogy hány karakter. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[GroupBy (formátum)-keret FirstLineIndent elem](./firstlineindent-element-for-frame-for-groupby-format.md) megadja az adatok első sorának jobb úgy, hogy hány karakter. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[Listaelem (formátum) FormatString eleme](./formatstring-element-for-listitem-for-listcontrol-format.md) meghatározza formátumú mintát, amely meghatározza, hogyan jelenjen meg a tulajdonság vagy parancsfájl érték.

[(Formátum) TableColumnItem FormatString eleme](./formatstring-element-for-tablecolumnitem-for-tablecontrol-format.md) meghatározza formátumú mintát, amely meghatározza, hogyan jelenjen meg a táblázat tulajdonság, vagy parancsprogram értékét.

[WideItem WideControl (formátum) a FormatString eleme](./formatstring-element-for-wideitem-for-widecontrol-format.md) meghatározza formátumú mintát, amely meghatározza, hogy a tulajdonság vagy parancsfájl érték hogyan jelenjen meg a nézetben.

[Elem keretet számára (formátum) konfiguráció vezérlők CustomItem](./frame-element-for-customitem-for-controls-for-configuration-format.md) határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[Elem keretet számára (formátum) nézet vezérlők CustomItem](./frame-element-for-customitem-for-controls-for-view-format.md) határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[Elem keretet CustomItem számára a nézet (formátum) CustomControl](./frame-element-for-customitem-for-customcontrol-for-view-format.md) határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[Elem keretet CustomItem számára a GroupBy (formátum)](./frame-element-for-customitem-for-groupby-format.md) határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[GroupBy elem (formátum) nézet](./groupby-element-for-view-format.md) határozza meg, hogyan jeleníti meg a Windows PowerShell-objektumok egy új csoportot.

[HideTableHeaders elem (formátum)](./hidetableheaders-element-format.md) Megadja, hogy a fejlécek, a tábla nem jelenik meg.

[ItemSelectionCondition elemet a vezérlők (formátum) konfiguráció ExpressionBinding](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md) határozza meg a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition eleme](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md) határozza meg a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[Kifejezés kötelező érvényű, a nézet (formátum) CustomControl ItemSelectionCondition elem](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md) határozza meg a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell. Van egy vezérlő elemhez megadható kiválasztási feltételek száma nincs korlátozva. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[A GroupBy (formátum) ExpressionBinding ItemSelectionCondition eleme](./itemselectioncondition-element-for-expressionbinding-for-groupby-format.md) határozza meg a feltételt, amelyet Pro tento ovládací prvek használandó léteznie kell. Van egy vezérlő elemhez megadható kiválasztási feltételek száma nincs korlátozva. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[Listaelem (formátum) ItemSelectionCondition eleme](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md) határozza meg a feltétel, a listaelem használandó léteznie kell.

[Címke elem a ListItem ListControl(Format) a](./label-element-for-listitem-for-listcontrol-format.md) címkéjét adja meg a tulajdonság, vagy parancsprogram érték sorában.

[Címke elem a GroupBy (formátum)](./label-element-for-groupby-format.md) meghatározza a felirat jelenik meg, ha egy új csoportot észlelt.

[Címke elem TableColumnHeader (formátum) a](./label-element-for-tablecolumnheader-for-tablecontrol-format.md) határozza meg a címke az oszlop tetején jelenik meg.

[Keret (formátum) konfiguráció vezérlők LeftIndent elem](./leftindent-element-for-frame-for-controls-for-configuration-format.md) adja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[Keret a vezérlőelemek a nézet (formátum) LeftIndent elem](./leftindent-element-for-frame-for-controls-for-view-format.md) adja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[Nézet (formátum) CustomControl-keret LeftIndent elem](./leftindent-element-for-frame-for-customcontrol-for-view-format.md) adja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[GroupBy (formátum)-keret LeftIndent elem](./leftindent-element-for-frame-for-groupby-format.md) adja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[ListControl elem (formátum)](./listcontrol-element-format.md) határozza meg a nézet lista formájában.

[ListEntry elem (formátum)](./listentry-element-for-listcontrol-format.md) biztosít a lista nézet definíciójának.

[ListEntries elem (formátum)](./listentries-element-for-listcontrol-format.md) határozza meg, hogyan a listanézet a sorok jelennek meg.

[Listaelem elem (formátum)](./listitem-element-for-listitems-for-listcontrol-format.md) tulajdonság vagy parancsfájl, amelynek értéke megjelenik a lista nézet sorában lévő határozza meg.

[ListItems elemek elem (formátum)](./listitems-element-for-listentry-for-listcontrol-format.md) határozza meg a tulajdonságokat és a parancsfájlok, amelyek a listanézetet jelennek meg.

[Elem nevét vezérlési konfiguráció (formátum) vezérlők](./name-element-for-control-for-controls-for-configuration-format.md) a vezérlő nevét adja meg. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[Elem name (formátum) SelectionSet](./name-element-for-selectionset-format.md) mutató hivatkozás a kijelölés-készlet nevét adja meg.

[Elem name (formátum) nézet](./name-element-for-view-format.md) nevét adja meg, hogy a nézet azonosítására szolgál.

[Soremelés elemet a vezérlők (formátum) konfiguráció CustomItem](./newline-element-for-customitem-for-controls-for-configuration-format.md) egy üres sort ad hozzá a vezérlő megjelenését. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[Soremelés elemet a vezérlők (formátum) nézet CustomItem](./newline-element-for-customitem-for-controls-for-view-format.md) egy üres sort ad hozzá a vezérlő megjelenését. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[A nézet (formátum) CustomControl CustomItem soremelés eleme](./newline-element-for-customitem-for-customcontrol-for-view-format.md) egy üres sort ad hozzá a vezérlő megjelenését. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[A GroupBy (formátum) CustomItem soremelés eleme](./newline-element-for-customitem-for-groupby-format.md) egy üres sort ad hozzá a vezérlő megjelenését. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[PropertyName elemet a vezérlők (formátum) konfiguráció ExpressionBinding](./propertyname-element-for-expressionbinding-for-controls-for-configuration-format.md) adja meg azt a .NET tulajdonságot, amelynek értéke megjelenik a közös felügyelete által. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[PropertyName elemet a vezérlők (formátum) nézet ExpressionBinding](./propertyname-element-for-expressionbinding-for-controls-for-view-format.md) adja meg azt a .NET-tulajdonságot, amelynek értéke megjelenik a vezérlőelem által. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[A nézet (formátum) CustomControl ExpressionBinding PropertyName eleme](./propertyname-element-for-expressionbinding-for-customcontrol-for-view-format.md) adja meg azt a .NET-tulajdonságot, amelynek értéke megjelenik a vezérlőelem által. Ez az elem szolgál, ha egyéni vezérlő nézet definiálása

[A GroupBy (formátum) ExpressionBinding PropertyName eleme](./propertyname-element-for-expressionbinding-for-groupby-format.md) adja meg azt a .NET-tulajdonságot, amelynek értéke megjelenik a vezérlőelem által. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[A PropertyName elemet a GroupBy (formátum)](./propertyname-element-for-groupby-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja egy új csoportot, amikor annak értéke módosul.

[PropertyName elemet a vezérlők (formátum) konfiguráció ItemSeclectionCondition](./propertyname-element-for-itemseclectioncondition-for-controls-for-configuration-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a vezérlő használatos. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[PropertyName elemet a vezérlők (formátum) nézet ItemSelectionCondition](./propertyname-element-for-itemselectioncondition-for-controls-for-view-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a vezérlő használatos. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[A nézet CustomControl ItemSelectionCondition PropertyName eleme (formátum](./propertyname-element-for-itemselectioncondition-for-customcontrol-for-view-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a vezérlő használatos. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[A GroupBy (formátum) ItemSelectionCondition PropertyName eleme](./propertyname-element-for-itemselectioncondition-for-groupby-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a vezérlő használatos. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[ItemSelectionCondition ListItem (formátum) a PropertyName eleme](./propertyname-element-for-itemselectioncondition-for-listcontrol-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a nézetet használja. Ez az elem akkor használatos, ha a lista nézet definiálása.

[Listaelem ListControl (formátum) a PropertyName eleme](./propertyname-element-for-listitem-for-listcontrol-format.md) adja meg azt a .NET-tulajdonságot, amelynek értéke megjelenik a listában.

[SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a PropertyName eleme](./propertyname-element-for-selectioncondition-for-controls-for-configuration-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a bejegyzés szolgál. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[PropertyName elemet a vezérlők (formátum) nézet SelectionCondition](./propertyname-element-for-selectioncondition-for-controls-for-view-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a bejegyzés szolgál. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[A nézet (formátum) CustomControl SelectionCondition PropertyName eleme](./propertyname-element-for-selectioncondition-for-customcontrol-for-view-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a definíció szolgál. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a PropertyName eleme](./propertyname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a definíció szolgál.

[A GroupBy (formátum) SelectionCondition PropertyName eleme](./propertyname-element-for-selectioncondition-for-groupby-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a definíció szolgál. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a PropertyName eleme](./propertyname-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a regisztrációslista-bejegyzés szolgál.

[SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a PropertyName eleme](./propertyname-element-for-selectioncondition-for-entryselectedby-for-tablerowentry-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a táblabejegyzés szolgál.

[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a PropertyName eleme](./propertyname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md) adja meg azt a .NET-tulajdonságot, amely elindítja a feltételt. Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a definíció szolgál.

[(Formátum) TableColumnItem PropertyName eleme](./propertyname-element-for-tablecolumnitem-for-tablecontrol-format.md) megadja a tulajdonságot, amelynek értéke megjelenik a sor oszlopában.

[(Formátum) WideItem PropertyName eleme](./propertyname-element-for-wideitem-for-widecontrol-format.md) adja meg azt a tulajdonságot az objektum, amelynek az értéke az széles nézetben jelenik meg.

[Keret (formátum) konfiguráció vezérlők RightIndent elem](./rightindent-element-for-frame-for-controls-for-configuration-format.md) adja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[Keret a vezérlőelemek a nézet (formátum) RightIndent elem](./rightindent-element-for-frame-for-controls-for-view-format.md) adja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[RightIndent elem](./rightindent-element-for-frame-for-customcontrol-for-view-format.md) adja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[GroupBy (formátum)-keret RightIndent elem](./rightindent-element-for-frame-for-groupby-format.md) adja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[ScriptBlock elemet a vezérlők (formátum) konfiguráció ExpressionBinding](./scriptblock-element-for-expressionbinding-for-controls-for-configuration-format.md) megadja a parancsprogramot, amelynek értéke megjelenik a közös felügyelete által. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[ScriptBlock elemet a vezérlők (formátum) nézet ExpressionBinding](./scriptblock-element-for-expressionbinding-for-controls-for-view-format.md) megadja a parancsprogramot, amelynek értéke megjelenik a vezérlőelem által. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[ExpressionBinding CustomCustomControl nézet (formátum) a scriptblock kulcsszót eleme](./scriptblock-element-for-expressionbinding-for-customcontrol-for-view-format.md) megadja a parancsprogramot, amelynek értéke megjelenik a vezérlőelem által. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[ExpressionBinding GroupBy (formátum) a scriptblock kulcsszót eleme](./scriptblock-element-for-expressionbinding-for-groupby-format.md) megadja a parancsprogramot, amelynek értéke megjelenik a vezérlőelem által. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[GroupBy (formátum) a scriptblock kulcsszót elem](./scriptblock-element-for-groupby-format.md) meghatározza a parancsfájl, amely elindítja egy új csoportot, amikor annak értéke módosul.

[ScriptBlock elemet a vezérlők (formátum) konfiguráció ItemSelectionCondition](./scriptblock-element-for-itemseclectioncondition-for-controls-for-configuration-format.md) megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a vezérlő használatos. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[ScriptBlock elemet a vezérlők (formátum) nézet ItemSelectionCondition](./scriptblock-element-for-itemselectioncondition-for-controls-for-view-format.md) megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a vezérlő használatos. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[ItemSelectionCondition CustomControl nézet (formátum) a scriptblock kulcsszót eleme](./scriptblock-element-for-itemselectioncondition-for-customcontrol-for-view-format.md) megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a vezérlő használatos. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[ItemSelectionCondition GroupBy (formátum) a scriptblock kulcsszót eleme](./scriptblock-element-for-itemselectioncondition-for-groupby-format.md) megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a vezérlő használatos. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[ItemSelectionCondition ListControl (formátum) a scriptblock kulcsszót eleme](./scriptblock-element-for-itemselectioncondition-for-listcontrol-format.md) megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a listaelem szolgál. Ez az elem akkor használatos, ha a lista nézet definiálása.

[Listaelem (formátum) a scriptblock kulcsszót elem](./scriptblock-element-for-listitem-for-listcontrol-format.md) megadja a parancsprogramot, amelynek értéke megjelenik a lista a sorban.

[ScriptBlock elemet a vezérlők (formátum) konfiguráció SelectionCondition](./scriptblock-element-for-selectioncondition-for-controls-for-configuration-format.md) megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a definíció szolgál. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[ScriptBlock elemet a vezérlők (formátum) nézet SelectionCondition](./scriptblock-element-for-selectioncondition-for-controls-for-view-format.md) megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a definíció szolgál. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[SelectionCondition CustomControl nézet (formátum) a scriptblock kulcsszót eleme](./scriptblock-element-for-selectioncondition-for-customcontrol-for-view-format.md) megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a definíció szolgál. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a scriptblock kulcsszót eleme](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md) megadja a parancsprogramot, amely elindítja a feltétel.

[SelectionCondition GroupBy (formátum) a scriptblock kulcsszót eleme](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-groupby-format.md) megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a definíció szolgál. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a scriptblock kulcsszót eleme](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md) megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a regisztrációslista-bejegyzés szolgál.

[SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a scriptblock kulcsszót eleme](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md) adja meg a parancsprogram-blokkot, amely elindítja a feltételt. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a táblabejegyzés szolgál.

[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a scriptblock kulcsszót eleme](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md) megadja a parancsprogramot, amely elindítja a feltétel. Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a széles körű bejegyzés definíciót használja.

[TableColumnItem (formátum) a scriptblock kulcsszót elem](./scriptblock-element-for-tablecolumnitem-for-tablecontrol-format.md) megadja a parancsprogramot, amelynek értéke megjelenik a sor oszlopában.

[WideItem (formátum) a scriptblock kulcsszót elem](./scriptblock-element-for-wideitem-for-widecontrol-format.md) megadja a parancsprogramot, amelynek az értéke az széles nézetben jelenik meg.

[A konfiguráció (formátum) CustomEntry EntrySelectedBy SelectionCondition eleme](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md) határozza meg egy feltételt, amely használt gyakori ellenőrzési definíció léteznie kell. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[SelectionCondition elemet a vezérlők (formátum) nézet EntrySelectedBy](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md) határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[A nézet (formátum) CustomControl EntrySelectedBy SelectionCondition eleme](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md) határozza meg egy feltételt, amely használható vezérlő definíció léteznie kell. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[EnumerableExpansion (formátum) a EntrySelectedBy SelectionCondition eleme](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md) határozza meg a feltétel, bontsa ki a gyűjtemény objektumokat, ez a definíció, léteznie kell.

[A GroupBy (formátum) EntrySelectedBy SelectionCondition eleme](./selectioncondition-element-for-entryselectedby-for-groupby-format.md) határozza meg egy feltételt, amely használható vezérlő definíció léteznie kell. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[ListEntry (formátum) a EntrySelectedBy SelectionCondition eleme](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md) határozza meg a feltétellel, hogy ez a definíció a listanézet használata léteznie kell. Kiválasztási feltételek, amelyek egy definíciója adható meg száma nincs korlátozva van.

[TableRowEntry (formátum) a EntrySelectedBy SelectionCondition eleme](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md) határozza meg a feltétellel, hogy ez a táblázat nézet definícióját használandó léteznie kell. Kiválasztási feltételek, amelyek a tábla definíciója adható meg száma nincs korlátozva van.

[WideEntry (formátum) a EntrySelectedBy SelectionCondition eleme](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md) határozza meg a feltételt, amelyet a definíció használandó léteznie kell. Kiválasztási feltételek széles bejegyzés-definíció adható meg száma nincs korlátozva van.

[SelectionSet elem (formátum)](./selectionset-element-format.md) határozza meg, amely a készlet neve szerint lehet hivatkozni .NET-objektumokat.

[SelectionSetName elemet a vezérlők (formátum) konfiguráció EntrySelectedBy](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md) .NET-típusokat, amelyek a vezérlő Ez a definíció egy halmazát határozza meg. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[SelectionSetName elemet a vezérlők (formátum) nézet EntrySelectedBy](./selectionsetname-element-for-entryselectedby-for-controls-for-view-format.md) .NET-típusokat, amelyek a vezérlő Ez a definíció egy halmazát határozza meg. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[CustomEntry (formátum) a EntrySelectedBy SelectionSetName eleme](./selectionsetname-element-for-entryselectedby-for-customcontrol-for-view-format.md) regisztrációslista-bejegyzés a .NET-objektumokat egy halmazát határozza meg. Nincs kijelölt csoportok bejegyzés adható meg száma nincs korlátozva.

[EnumerableExpansion (formátum) a EntrySelectedBy SelectionSetName eleme](./selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format.md) Megadja, hogy ez a definíció szerint bontva .NET típusú.

[A GroupBy (formátum) EntrySelectedBy SelectionSetName eleme](./selectionsetname-element-for-entryselectedby-for-groupby-format.md) regisztrációslista-bejegyzés a .NET-objektumokat egy halmazát határozza meg. Nincs kijelölt csoportok bejegyzés adható meg száma nincs korlátozva. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[ListEntry (formátum) a EntrySelectedBy SelectionSetName eleme](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md) regisztrációslista-bejegyzés a .NET-objektumokat egy halmazát határozza meg. Nincs kijelölt csoportok bejegyzés adható meg száma nincs korlátozva.

[TableRowEntry (formátum) a EntrySelectedBy SelectionSetName eleme](./selectionsetname-element-for-entryselectedby-for-tablecontrol-format.md) megadja a .NET készletét típusok használatát a bejegyzés a táblázat nézet. Nincs kijelölt csoportok bejegyzés adható meg száma nincs korlátozva.

[WideEntry (formátum) a EntrySelectedBy SelectionSetName eleme](./selectionsetname-element-for-entryselectedby-for-widecontrol-format.md) .NET-objektumokat a definíció egy halmazát határozza meg. A definíció használatos, amikor ezek az objektumok egyike jelenik meg.

[SelectionSetName elemet a vezérlők (formátum) konfiguráció SelectionCondition](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md) Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[SelectionSetName elemet a vezérlők (formátum) nézet SelectionCondition](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md) Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[EntrySelectedBy elemet a nézet (formátum) CustomEntry](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md) Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[EntrySelectedBy EnumerableExpansion (formátum) esetében a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md) Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül.

[A GroupBy (formátum) SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-groupby-format.md) Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[EntrySelectedBy ListEntry (formátum) esetében a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-listentry-format.md) Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik ez a definíció a listanézet használatával.

[EntrySelectedBy TableRowEntry (formátum) esetében a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md) Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik ez a definíció, a táblázat nézet használatával.

[EntrySelectedBy WideEntry (formátum) esetében a SelectionCondition SelectionSetName eleme](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md) Megadja azt a feltételt .NET típusú. Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik ez a definíció, a széles nézet használatával.

[(Formátum) ViewSelectedBy SelectionSetName eleme](./selectionsetname-element-for-viewselectedby-format.md) jelennek meg a nézet által .NET-objektumokat egy halmazát határozza meg.

[SelectionSets elem (formátum)](./selectionsets-element-format.md) meghatározza formátumú egyéni nézetek által használható .NET-objektumokat a különböző.

[ShowError elem (formátum)](./showerror-element-format.md) Megadja, hogy megjelenik-e a teljes rekordot, ha hiba történik az adatok megjelenítése közben.

[TableControl (formátum) a TableHeaders TableColumnHeader eleme](./tablecolumnheader-element-format.md) határozza meg a címke, az oszlopok szélességét és a egy oszlop a tábla a címke zarovnání.

[TableColumnItem elem (formátum)](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) tulajdonság vagy parancsfájl, amelynek értéke megjelenik a sor oszlop határozza meg.

[TableColumnItems elem (formátum)](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md) határozza meg a Tulajdonságok vagy parancsfájlok, melynek értékei jelennek meg a sorban.

[TableControl elem (formátum)](./tablecontrol-element-format.md) határozza meg a nézet táblázatos formában.

[TableHeaders elem (formátum)](./tableheaders-element-format.md) meghatározza egy tábla oszlopait az fejlécek.

[TableRowEntries elem (formátum)](./tablerowentries-element-for-tablecontrol-format.md) határozza meg a tábla sorait.

[TableRowEntry elem (formátum)](./tablerowentry-element-for-tablerowentries-for-tablecontrol-format.md) határozza meg, amely egy sort a táblában megjelennek az adatok.

[Szöveg elemet a vezérlők (formátum) konfiguráció CustomItem](./text-element-for-customitem-for-controls-for-configuration-format.md) megadja szöveg, amely az adatok, például címke, a vezérlő által megjelenített szögletes zárójeleket az adatok és a tárolóhelyek szolgáltatás számára az adatok behúzás adni. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[Szöveg elemet a vezérlők (formátum) nézet CustomItem](./text-element-for-customitem-for-controls-for-view-format.md) megadja szöveg, amely az adatok, például címke, a vezérlő által megjelenített szögletes zárójeleket az adatok és a tárolóhelyek szolgáltatás számára az adatok behúzás adni. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[A CustomItem (formátum) elem](./text-element-for-customitem-for-customview-for-view-format.md) megadja szöveg, amely az adatok, például címke, a vezérlő által megjelenített szögletes zárójeleket az adatok és a tárolóhelyek szolgáltatás számára az adatok behúzás adni. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[A CustomItem a GroupBy (formátum) elem](./text-element-for-customitem-for-groupby-format.md) megadja szöveg, amely az adatok, például címke, a vezérlő által megjelenített szögletes zárójeleket az adatok és a tárolóhelyek szolgáltatás számára az adatok behúzás adni. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[TypeName elemet a vezérlők (formátum) konfiguráció EntrySelectedBy](./typename-element-for-entryselectedby-for-controls-for-configuration-format.md) használ, ez a definíció, a vezérlő .NET típust ad meg. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[TypeName elemet a vezérlők (formátum) nézet EntrySelectedBy](./typename-element-for-entryselectedby-for-controls-for-view-format.md) használ, ez a definíció, a vezérlő .NET típust ad meg. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[A nézet (formátum) CustomEntry EntrySelectedBy TypeName eleme](./typename-element-for-entryselectedby-for-customentry-for-view-format.md) megadja a .NET-típus, amely használja ezt az egyéni vezérlő nézet definícióját. Nincs korlátozva a definíciófrissítés számára megadható típusok számával.

[EntrySelectedBy EnumerableExpansion (formátum) a TypeName eleme](./typename-element-for-entryselectedby-for-enumerableexpansion-format.md) , amely ki van bontva, ez a definíció szerint .NET típust határozzon meg. Ez az elem szolgál egy alapértelmezett beállítások meghatározásakor.

[A GroupBy (formátum) EntrySelectedBy TypeName eleme](./typename-element-for-entryselectedby-for-groupby-format.md) Ez a definíció az egyéni vezérlő használó .NET típust határozzon meg. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[EntrySelectedBy ListControl (formátum) a TypeName eleme](./typename-element-for-entryselectedby-for-listcontrol-format.md) Ez a bejegyzés a listanézet használó .NET típust határozzon meg. Regisztrációslista-bejegyzés adható meg-típusok száma nincs korlátozva van.

[EntrySelectedBy TableRowEntry (formátum) a TypeName eleme](./typename-element-for-entryselectedby-for-tablecontrol-format.md) Ez a bejegyzés a táblázat nézet használó .NET típust határozzon meg. A tábla bejegyzés adható meg-típusok száma nincs korlátozva van.

[EntrySelectedBy WideEntry (formátum) a TypeName eleme](./typename-element-for-entryselectedby-for-wideentry-format.md) a definíció számára .NET típust határozzon meg. A definíció használatos, amikor az objektum jelenik meg.

[TypeName elemet a vezérlők (formátum) konfiguráció SelectionCondition](./typename-element-for-selectioncondition-for-controls-for-configuration-format.md) egy .NET típusát, amely elindítja a feltételt határozza meg. Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.

[TypeName elemet a vezérlők (formátum) nézet SelectionCondition](./typename-element-for-selectioncondition-for-controls-for-view-format.md) egy .NET típusát, amely elindítja a feltételt határozza meg. Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.

[A nézet (formátum) CustomControl SelectionCondition TypeName eleme](./typename-element-for-selectioncondition-for-customcontrol-for-view-format.md) egy .NET típusát, amely elindítja a feltételt határozza meg. Ehhez az elemhez használt egyéni vezérlő nézet definiálása.

[SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a TypeName eleme](./typename-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md) egy .NET típusát, amely elindítja a feltételt határozza meg.

[A GroupBy (formátum) SelectionCondition TypeName eleme](./typename-element-for-selectioncondition-for-groupby-format.md) egy .NET típusát, amely elindítja a feltételt határozza meg. Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.

[SelectionCondition EntrySelectedBy ListControl (formátum) esetében a TypeName eleme](./typename-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md) egy .NET típusát, amely elindítja a feltételt határozza meg. Ez a típus meghatározva, a regisztrációslista-bejegyzés használ.

[SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a TypeName eleme](./typename-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md) egy .NET típusát, amely elindítja a feltételt határozza meg. Ha ez a típus meghatározva, a feltétel nem teljesül, és a táblázatsor szolgál.

[SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a TypeName eleme](./typename-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md) egy .NET típusát, amely elindítja a feltételt határozza meg. Ez a típus meghatározva, a definíciót használ.

[TypeName elem esetében (formátum)](./typename-element-for-types-format.md) olyan objektum, amely a kijelölt csoporthoz tartozó .NET típusát határozza meg.

[ViewSelectedBy (formátum) TypeName eleme](./typename-element-for-viewselectedby-format.md) adja meg a nézet által megjelenített .NET-objektumokat.

[Elem (formátum) típusokat](./types-element-for-selectionset-format.md) határozza meg a .NET-objektumok, amelyek a kijelölés beállítva.

[Elem (formátum) megtekintéséhez](./view-element-format.md) meghatározása egy nézetet, amely legalább egy .NET-objektumokká megjelenítésére szolgál.

[ViewDefinitions elem (formátum)](./viewdefinitions-element-format.md) határozza meg az objektumokat megjelenítő nézetek.

[ViewSelectedBy elem (formátum)](./viewselectedby-element-format.md) határozza meg a .NET-objektumokat, amely szerint a nézetben jelennek meg.

[WideControl elem (formátum)](./widecontrol-element-format.md) Defines (egyetlen érték) teljes listáját a nézet formázása. Ez a nézet jeleníti meg, egy egyetlen tulajdonságát érték vagy parancsfájlt minden objektum esetén.

[WideEntries elem (formátum)](./wideentries-element-for-widecontrol-format.md) biztosít a széles nézet definíciói. A széles nézet meg kell adnia egy vagy több definíciót.

[WideEntry elem (formátum)](./wideentry-element-for-widecontrol-format.md) biztosít a széles nézet definíciójának.

[WideItem elem (formátum)](./wideitem-element-for-widecontrol-format.md) határozza meg, tulajdonság vagy parancsfájl, amelynek értéke megjelenik.

[Szélesség elem (formátum)](./width-element-for-tablecolumnheader-for-tablecontrol-format.md) határozza meg az oszlopok szélességét (a karakter).

[Elem (formátum) burkolása](./wrap-element-for-tablerowentry-for-tablecontrol-format.md) megadja a szöveg, amely meghaladja a Oszlopszélesség a következő sorban jelenik meg.

[WrapTables elem (formátum)](./wraptables-element-format.md) Megadja, hogy egy cellába adatok áthelyezése a következő sorra, ha az adatok hosszabb, mint az oszlopok szélességét.

## <a name="see-also"></a>Lásd még:

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
