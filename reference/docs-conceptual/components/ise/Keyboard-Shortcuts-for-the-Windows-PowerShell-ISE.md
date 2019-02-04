---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A Windows PowerShell ISE billentyűparancsai
ms.assetid: 8328b946-0f02-4ef4-ac28-2743a1b4043b
ms.openlocfilehash: 1abae849ce599b586357fd2a8db46c608932bd4e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686711"
---
# <a name="keyboard-shortcuts-for-the-windows-powershell-ise"></a>A Windows PowerShell ISE billentyűparancsai

Az alábbi billentyűparancsok segítségével hajtsa végre a műveleteket a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE). Windows PowerShell ISE-ben érhető el, mert része a Windows Server és a Windows ügyfél-operációsrendszert, de még néhány régebbi Windows operációs rendszer részeként telepíteni a [Windows Management Framework 4.0 letöltőcsomag](https://go.microsoft.com/fwlink/?LinkID=293881).

## <a name="keyboard-shortcuts-for-editing-text"></a>Szöveg szerkesztése billentyűparancsai

A következő billentyűparancsokat használhatja a szöveg szerkesztésekor.

|Művelet|Billentyűparancsok|Használja a|
|----------|----------------------|----------|
|**segítség**|F1|A parancsfájl panelen **fontos:** Megadhatja, hogy F1 súgó származik, a TechNet-könyvtárban a weben, vagy letöltött Súgó (lásd az Update-Help). Kiválasztásához kattintson **eszközök**, **beállítások**, majd a a **általános beállítások**lapon állítsa be vagy törölje a jelet **online tartalom helyett használja a helyi súgó tartalma.**|
|**Másolás**|CTRL+C|A parancsfájl panelen, a parancs ablaktáblán, a Tesztkimenet ablaktáblán|
|**Cut**|CTRL+X|Szkriptpanel parancs panel|
|**Kibontás vagy összecsukás tagolása**|CTRL+M|Szkriptpanel|
|**Szkript helye**|CTRL+F|Szkriptpanel|
|**A szkript a következő keresése**|F3|Szkriptpanel|
|**Előző szkriptben keresése**|SHIFT+F3|Szkriptpanel|
|**Párjának keresése**|CTRL+]|Szkriptpanel|
|**Paste**|CTRL+V|Szkriptpanel parancs panel|
|**Redo**|CTRL+Y|Szkriptpanel parancs panel|
|**Cserélje le a parancsfájlt**|CTRL+H|Szkriptpanel|
|**Mentés**|CTRL+S|Szkriptpanel|
|**Az összes kijelölése**|CTRL+A|A parancsfájl panelen, a parancs ablaktáblán, a Tesztkimenet ablaktáblán|
|**A kódrészletek megjelenítése**|CTRL+J|Szkriptpanel parancs panel|
|**A Visszavonás**|CTRL+Z|Szkriptpanel parancs panel|

## <a name="keyboard-shortcuts-for-running-scripts"></a>Parancsfájlok futtatásához használható billentyűparancsok

A következő billentyűparancsokat használhatja a parancsfájlok futtatásakor, a parancsfájl panelen.

|Művelet|Billentyűparancs|
|----------|---------------------|
|**Új**|CTRL+N|
|**Open**|CTRL+O|
|**Futtatás**|F5|
|**Kijelölés futtatása**|F8|
|**Végrehajtási leállítása**|CTRL + BREAK BILLENTYŰKOMBINÁCIÓT. CTRL + C is használható, ha a környezet nem egyértelmű, (Ha nincs szöveg kijelölve).|
|**Lap** (a következő szkript)|A CTRL + TAB **Megjegyzés:** Lapon a következő parancsfájl működik, csak ha egyetlen Windows PowerShell-lap megnyitásához, vagy egynél több Windows PowerShell-lap megnyitásához, de a parancsfájl panelen célja.|
|**Lap** (az előző parancsfájlt)|CTRL + SHIFT + TAB **Megjegyzés:** Előző script lapon működik, ha csak egy Windows PowerShell-lap megnyitásához, vagy ha egynél több Windows PowerShell-lap megnyitásához, és célja a parancsfájl panelen.|

## <a name="keyboard-shortcuts-for-customizing-the-view"></a>A nézet testreszabására használható billentyűparancsok

A következő billentyűparancsokat használhatja testreszabásához a Windows PowerShell ISE-ben. Azok az alkalmazásban lévő összes ablaktáblák hozzáférhetőek.

|Művelet|Billentyűparancs|
|----------|---------------------|
|**Nyissa meg a parancs (v2), vagy (v3-as és újabb verziók) panel**|CTRL+D|
|**Ugrás a Tesztkimenet ablaktáblán (csak v2)**|CTRL+SHIFT+O|
|**Ugrás a parancsfájl panelen**|CTRL+I|
|**Parancsfájl ablaktábla megjelenítése**|CTRL+R|
|**Parancsfájl ablaktábla elrejtése**|CTRL+R|
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
> Használhatja a billentyűparancsokat Windows PowerShell ISE-ben szkriptek hibakeresése a Windows PowerShell-konzol tervezve. A billentyűparancsok használatához a parancs panelen írja be a helyi, és nyomja le az ENTER billentyűt.

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
|**Előző PowerShell-lap**|CTRL + SHIFT + TAB. Ez a parancs csak akkor, ha nincs olyan nyissa meg a Windows PowerShell lapon működik.|
|**Következő Windows PowerShell-lap**|CTRL+TAB. Ez a parancs csak akkor, ha nincs olyan nyissa meg a Windows PowerShell lapon működik.|

## <a name="keyboard-shortcuts-for-starting-and-exiting"></a>Billentyűparancsok indítása és leállítása

A következő billentyűparancsokat használhatja, indítsa el a Windows PowerShell-konzolt (PowerShell.exe), vagy lépjen ki a Windows PowerShell ISE-ben.

|Művelet|Billentyűparancs|
|----------|---------------------|
|**Exit**|ALT+F4|
|**Indítsa el a PowerShell.exe** (Windows PowerShell-konzolon)|CTRL+SHIFT+P|

## <a name="see-also"></a>Lásd még:

- [PowerShell Magazine: A teljes listát a Windows PowerShell ISE billentyűparancsai](https://www.powershellmagazine.com/2013/01/29/the-complete-list-of-powershell-ise-3-0-keyboard-shortcuts/)