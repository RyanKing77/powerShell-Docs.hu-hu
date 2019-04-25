---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A Windows PowerShell ISE kisegítő lehetőségei
ms.assetid: a078f9d1-dd6b-4323-b16d-0622cd993aa8
ms.openlocfilehash: 78a001dbe43a0b005d10a817e05e4cc7a72f5bd0
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058454"
---
# <a name="accessibility-in-windows-powershell-ise"></a>A Windows PowerShell ISE kisegítő lehetőségei

Ez a témakör ismerteti az akadálymentességi funkciók a Windows PowerShell integrált parancsfájlkezelési környezet (ISE), amely hasznos lehet.

* [A méret és a konzol és a parancsfájl ablaktáblák helyének módosítása](#how-to-change-the-size-and-location-of-the-console-and-script-panes)
* [Szöveg szerkesztése billentyűparancsai](#keyboard-shortcuts-for-editing-text)
* [Parancsfájlok futtatásához használható billentyűparancsok](#keyboard-shortcuts-for-running-scripts)
* [A nézet testreszabására használható billentyűparancsok](#keyboard-shortcuts-for-customizing-the-view)
* [Szkriptek hibakeresése billentyűparancsai](#keyboard-shortcuts-for-debugging-scripts)
* [Windows PowerShell-lapok billentyűparancsai](#keyboard-shortcuts-for-windows-powershell-tabs)
* [Billentyűparancsok indítása és leállítása](#keyboard-shortcuts-for-starting-and-exiting)

A Microsoft törekszik arra, hogy mindenki számára megkönnyítse termékei és szolgáltatásai használatát. Az alábbi témakörök ismertetik a Funkciók, termékek és szolgáltatások, amelyek elérhetőbbé teszik a Windows PowerShell ISE-ben a megváltozott fogyatékkal élők számára.

Windows PowerShell ISE-ben a kontrasztos módot támogatja. A gyengén látók számára töréspontot információ érhető el a töréspontok, mint például kezelésére szolgáló parancsmagok [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) és [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420). További részletekért lásd: "töréspontok kezelése című" a [szkriptek hibakeresése a Windows PowerShell ISE-ben hogyan](How-to-Debug-Scripts-in-Windows-PowerShell-ISE.md). Kisegítő lehetőségeket nyújtó szolgáltatásai és a Microsoft Windows segédprogramok kívül a következő funkciók elérhetőbbé teszik a Windows PowerShell ISE-ben fogyatékkal élők számára:

- Billentyűparancsok

- Szintaxis színezése tábla- és számos egyéb szín beállítások módosítása használatával lehetővé teszi a [$psISE.Options](https://technet.microsoft.com/library/75e2a76f-f3d1-490b-ad5d-e3829946aabb) scripting objektum.

- Szöveg méretének módosítása

## <a name="how-to-change-the-size-and-location-of-the-console-and-script-panes"></a>A méret és a konzol és a parancsfájl ablaktáblák helyének módosítása

A következő lépések segítségével módosíthatja a méret- és a parancsfájl panelen és a konzol ablaktáblában. Amikor újra megnyitja a Windows PowerShell ISE-ben, a méret és elhelyezkedés végrehajtott lesznek megőrizve.

### <a name="to-resize-the-script-pane-and-console-pane"></a>Méretezze át a parancsfájl panelen és a konzol panelen

1. Az egérmutatót a felosztás sor között a parancsfájl panelen és a konzol ablaktáblában.

2. Ha az egérmutatót egy kétirányú nyíl vált, húzza a ablaktábla méretének módosítása szegélyét.

### <a name="to-move-the-script-pane-and-console-pane"></a>A parancsfájl panelen és a konzol ablaktáblában áthelyezése

Tegye a következők egyikét:

- Szeretné áthelyezni a parancsfájl panelen a konzol ablaktáblában fent, nyomja le az ENTER **CTRL + 1** vagy az eszköztáron kattintson a **parancsfájl ablaktábla felső megjelenítése** ikonra, vagy a a **nézet** menüben kattintson a **megjelenítése Parancsfájl-panel felső**.

- Helyezze át a parancsfájl panelen jobb oldalán a konzol ablaktáblájában, nyomja le a **CTRL + 2** vagy az eszköztáron kattintson a **megjelenítése a parancsfájl panelen jobb** ikonra, vagy a a **nézet** menüben kattintson**Parancsfájl ablaktábla jobb megjelenítése**.

- A parancsfájl panelen maximalizálása nyomja le az ENTER **CTRL + 3** vagy az eszköztáron kattintson a **Show Script panel teljes méretű** ikonra, vagy a a **nézet** menüben kattintson a **parancsfájl megjelenítése Teljes méretű panel**.

- Maximalizálhatja a konzol ablaktáblában, és a parancsfájl panelen, a lapok, sorának jobb szélén peremhálózaton elrejtése kattintson a **parancsfájl ablaktábla elrejtése** ikonra, a a **nézet** menü, kijelölésének megszüntetéséhez kattintson a **parancsfájl-ablaktáblamegjelenítése** menüpont.

- A parancsfájl panel megjelenítéséhez, ha a konzol ablaktáblában teljes méretű, a lapok, sorának sokkal jobb szélén kattintson a **parancsfájl ablaktábla megjelenítése** ikonra, vagy a a **nézet** menüben kattintással jelölje ki a **parancsfájl megjelenítése Panel** menüpont.

## <a name="keyboard-shortcuts-for-editing-text"></a>Szöveg szerkesztése billentyűparancsai

A következő billentyűparancsokat használhatja a szöveg szerkesztésekor.

|Művelet|Billentyűparancsok|Használja a|
|----------|----------------------|----------|
|**Másolás**|CTRL+C|Szkriptpanel, a konzol panel|
|**Cut**|CTRL+X|Szkriptpanel, a konzol panel|
|**Szkript helye**|CTRL+F|Szkriptpanel|
|**A szkript a következő keresése**|F3|Szkriptpanel|
|**Előző szkriptben keresése**|SHIFT+F3|Szkriptpanel|
|**Paste**|CTRL+V|Szkriptpanel, a konzol panel|
|**Redo**|CTRL+Y|Szkriptpanel, a konzol panel|
|**Cserélje le a parancsfájlt**|CTRL+H|Szkriptpanel|
|**Mentés**|CTRL+S|Szkriptpanel|
|**Az összes kijelölése**|CTRL+A|Szkriptpanel, a konzol panel|
|**A Visszavonás**|CTRL+Z|Szkriptpanel, a konzol panel|

## <a name="keyboard-shortcuts-for-running-scripts"></a>Parancsfájlok futtatásához használható billentyűparancsok

A következő billentyűparancsokat használhatja a parancsfájlok futtatásakor, a parancsfájl panelen.

|Művelet|Billentyűparancs|
|----------|---------------------|
|**Új**|CTRL+N|
|**Open**|CTRL+O|
|**Futtatás**|F5|
|**Kijelölés futtatása**|F8|
|**Végrehajtási leállítása**|CTRL + BREAK BILLENTYŰKOMBINÁCIÓT. CTRL + C is használható, ha a környezet nem egyértelmű, (Ha nincs szöveg kijelölve).|
|**Lap** (a következő szkript)|A CTRL + TAB **Megjegyzés:** Lapon a következő parancsfájl működik, csak ha egyetlen PowerShell-lap megnyitásához, vagy ha egynél több nyissa meg a PowerShell-lap van, de a parancsfájl panelen célja.|
|**Lap** (az előző parancsfájlt)|CTRL + SHIFT + TAB **Megjegyzés:** Előző script lapon működik, ha csak egy PowerShell-lap megnyitásához, vagy ha egynél több PowerShell-lap megnyitásához, és célja a parancsfájl panelen.|

## <a name="keyboard-shortcuts-for-customizing-the-view"></a>A nézet testreszabására használható billentyűparancsok

A következő billentyűparancsokat használhatja testreszabásához a Windows PowerShell ISE-ben. Azok az alkalmazásban lévő összes ablaktáblák hozzáférhetőek.

|Művelet|Billentyűparancs|
|----------|---------------------|
|**Ugrás a konzol panelen**|CTRL+D|
|**Ugrás a parancsfájl panelen**|CTRL+I|
|**Parancsfájl ablaktábla megjelenítése**|CTRL+R|
|**Parancsfájl ablaktábla elrejtése**|CTRL+R|
||
|**Szkriptpanel mozgatása felfelé**|CTRL+1|
|**Szkriptpanel jobbra**|CTRL+2|
|**Maximalizálja a parancsfájl panelen**|CTRL+3|
|**Nagyítás**|CTRL + PLUSZJEL|
|**Kicsinyítés**|CTRL + MÍNUSZJEL|

## <a name="keyboard-shortcuts-for-debugging-scripts"></a>Szkriptek hibakeresése billentyűparancsai

A következő billentyűparancsokat használhatja a parancsfájlok hibakeresése.

|Művelet|Billentyűparancs|Használja a|
|----------|---------------------|----------|
|**Run/Continue**|F5|Szkriptpanel, amikor egy parancsprogram-hibakeresés|
|**Lépjen be**|F11|Szkriptpanel, amikor egy parancsprogram-hibakeresés|
|**Átlépés**|F10|Szkriptpanel, amikor egy parancsprogram-hibakeresés|
|**Krokovat s Vystoupením**|SHIFT+F11|Szkriptpanel, amikor egy parancsprogram-hibakeresés|
|**Hívási verem megjelenítése**|CTRL+SHIFT+D|Szkriptpanel, amikor egy parancsprogram-hibakeresés|
|**Lista töréspontok keresése**|CTRL+SHIFT+L|Szkriptpanel, amikor egy parancsprogram-hibakeresés|
|**Toggle Breakpoint**|F9|Szkriptpanel, amikor egy parancsprogram-hibakeresés|
|**Az összes töréspont eltávolítása**|CTRL+SHIFT+F9|Szkriptpanel, amikor egy parancsprogram-hibakeresés|
|**A hibakereső leállítása**|SHIFT+F5|Szkriptpanel, amikor egy parancsprogram-hibakeresés|

> [!NOTE]
>
> Használhatja a billentyűparancsokat Windows PowerShell ISE-ben szkriptek hibakeresése a Windows PowerShell-konzol tervezve. Használja ezeket a parancsokat, írja be a parancsikont a konzol ablaktáblában, és nyomja le az ENTER billentyűt.

|Művelet|Billentyűparancs|Használja a|
|----------|---------------------|----------|
|**Továbbra is**|C|Konzol ablaktáblában, amikor egy parancsprogram-hibakeresés|
|**Lépjen be**|S|Konzol ablaktáblában, amikor egy parancsprogram-hibakeresés|
|**Átlépés**|V|Konzol ablaktáblában, amikor egy parancsprogram-hibakeresés|
|**Krokovat s Vystoupením**|O|Konzol ablaktáblában, amikor egy parancsprogram-hibakeresés|
|**Ismételje meg az utolsó parancs** (a lépést, vagy keresztül lépés)|ENTER|Konzol ablaktáblában, amikor egy parancsprogram-hibakeresés|
|**Hívási verem megjelenítése**|K|Konzol ablaktáblában, amikor egy parancsprogram-hibakeresés|
|**Állítsa le a hibakeresést**|Q|Konzol ablaktáblában, amikor egy parancsprogram-hibakeresés|
|**A parancsfájl listázása**|L|Konzol ablaktáblában, amikor egy parancsprogram-hibakeresés|
|**Hibakeresés a parancsok konzol megjelenítése**|H vagy?|Konzol ablaktáblában, amikor egy parancsprogram-hibakeresés|

## <a name="keyboard-shortcuts-for-windows-powershell-tabs"></a>Windows PowerShell-lapok billentyűparancsai

A következő billentyűparancsokat használhatja, lapok Windows PowerShell használatakor.

|Művelet|Billentyűparancs|
|----------|---------------------|
|**Zárja be a PowerShell-lap**|CTRL+W|
|**Új PowerShell-lap**|CTRL+T|
|**Előző PowerShell-lap**|CTRL + SHIFT + TAB. Ez a parancs csak akkor, ha nincs olyan nyitott bármely PowerShell lapon működik.|
|**Következő Windows PowerShell-lap**|CTRL+TAB. Ez a parancs csak akkor, ha nincs olyan nyitott bármely PowerShell lapon működik.|

## <a name="keyboard-shortcuts-for-starting-and-exiting"></a>Billentyűparancsok indítása és leállítása

A következő billentyűparancsokat használhatja, indítsa el a Windows PowerShell-konzolt (PowerShell.exe), vagy lépjen ki a Windows PowerShell ISE-ben.

|Művelet|Billentyűparancs|
|----------|---------------------|
|**Exit**|ALT+F4|
|**Indítsa el a PowerShell.exe** (Windows PowerShell-konzolon)|CTRL+SHIFT+P|

## <a name="see-also"></a>Lásd még:

[A Windows PowerShell ISE bemutatása](Introducing-the-Windows-PowerShell-ISE.md)