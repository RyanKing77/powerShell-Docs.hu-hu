---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A Windows PowerShell ISE kisegítő lehetőségei
ms.assetid: a078f9d1-dd6b-4323-b16d-0622cd993aa8
ms.openlocfilehash: 272dd502ff9d220e82236c93cbffaf4e12054cfe
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/07/2018
ms.locfileid: "34482981"
---
# <a name="accessibility-in-windows-powershell-ise"></a>A Windows PowerShell ISE kisegítő lehetőségei

Ez a témakör a Windows PowerShell integrált parancsfájlkezelési környezet (ISE), előfordulhat, hogy a hasznos kisegítő lehetőségeinek ismertetése.

* [A méret és a konzol és a parancsfájl ablaktáblák helyének módosítása](#how-to-change-the-size-and-location-of-the-console-and-script-panes)
* [Billentyűparancsok szöveg szerkesztése](#keyboard-shortcuts-for-editing-text)
* [A parancsfájlok futtatásához használható billentyűparancsok](#keyboard-shortcuts-for-running-scripts)
* [A nézet testreszabására használható billentyűparancsok](#keyboard-shortcuts-for-customizing-the-view)
* [A parancsfájlok hibakereséshez használható billentyűparancsok](#keyboard-shortcuts-for-debugging-scripts)
* [A Windows PowerShell lapok használható billentyűparancsok](#keyboard-shortcuts-for-windows-powershell-tabs)
* [Billentyűparancsok indítása és leállítása](#keyboard-shortcuts-for-starting-and-exiting)

A Microsoft törekszik arra, hogy mindenki számára megkönnyítse termékei és szolgáltatásai használatát. A következő témakörök információt nyújtanak azokról a funkciókat, termékeket és szolgáltatásokat, amelyek a Windows PowerShell ISE elérhetőbbé teszik a fogyatékkal élők számára.

A Windows PowerShell ISE kontrasztos módot támogatja. A gyengén látó, a töréspont információk érhető el a töréspontokat, például kezelésére szolgáló parancsmagok [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) és [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420). További információt lásd: "How to töréspontok kezelése" a [parancsfájlok hibakeresése a Windows PowerShell ISE hogyan](../core-powershell/ise/How-to-Debug-Scripts-in-Windows-PowerShell-ISE.md). Kisegítő lehetőségei és segédprogramjai a Microsoft Windows mellett a következő funkciók Windows PowerShell ISE elérhetőbbé teszik könnyebben használhatóvá a fogyatékkal élők számára:

- Billentyűparancsok

- Szintaxis színezése tábla és módosítását, több más szín beállításainak a [$psISE.Options](https://technet.microsoft.com/library/75e2a76f-f3d1-490b-ad5d-e3829946aabb) scripting objektum.

- Szöveg méretének módosítása

## <a name="how-to-change-the-size-and-location-of-the-console-and-script-panes"></a>A méret és a konzol és a parancsfájl ablaktáblák helyének módosítása

Az alábbi lépések segítségével a méret és a konzol és a parancsfájl ablaktábla helyének módosítása. Ha újra megnyitja a Windows PowerShell ISE, a méret és elhelyezkedés módosítások megmaradnak.

### <a name="to-resize-the-script-pane-and-console-pane"></a>A parancsfájl és konzol ablaktábla átméretezéséhez

1. Az egérmutatót a felosztás sor a parancsfájl és konzol ablaktábla között.

2. Amikor az egérmutató egy kétirányú nyíl, húzza a szegély ablaktábla méretének módosításához.

### <a name="to-move-the-script-pane-and-console-pane"></a>A parancsfájl és a konzol ablaktáblában áthelyezése

Tegye a következők egyikét:

- Helyezze át a parancssori panelbe fent a konzol ablaktáblában, nyomja meg az **CTRL + 1** vagy az eszköztáron kattintson a **megjelenítése parancsfájl ablaktábla felső** ikonra, vagy a a **nézet** menüben kattintson a **megjelenítése Parancsfájl-ablaktábla felső**.

- Helyezze át a parancssori panelbe jobb oldalán a konzol ablaktáblában, nyomja meg az **CTRL + 2** vagy az eszköztáron kattintson a **megjelenítése parancsfájl ablak jobb** ikonra, vagy a a **nézet** menü kattintson**Parancsfájl ablak jobb megjelenítése**.

- A parancssori panelbe maximalizálása érdekében a nyomja le az ENTER **CTRL + 3** vagy az eszköztáron kattintson a **megjelenítése parancsfájl ablaktábla teljes méretű** ikonra, vagy a a **nézet** menüben kattintson a **parancsfájl megjelenítése Teljes méretű ablaktábla**.

- Maximalizálhatja a konzol ablaktáblában, és a parancsfájl ablak jobb szélén lapján sorára elrejtéséhez kattintson a **parancsfájl ablaktábla elrejtése** ikonra, a a **nézet** menü, törölje a kattintson a **parancsfájl-ablaktáblamegjelenítése** menüjét.

- A parancsfájl ablaktábla megjelenítése, amikor a konzol ablaktáblában teljes méretű, lapján sorára jobb szélén kattintson a **parancsfájl ablaktábla megjelenítése** ikonra, vagy a **nézet** menüben kattintással jelölje ki a **parancsfájl megjelenítése Ablaktábla** menüjét.

## <a name="keyboard-shortcuts-for-editing-text"></a>Billentyűparancsok szöveg szerkesztése

A következő billentyűparancsokat használhatja szöveg szerkesztésekor.

|Művelet|Billentyűparancsok|A használatára|
|----------|----------------------|----------|
|**Másolás**|CTRL+C|Parancsfájl ablaktáblán, a konzol ablaktábla|
|**Cut**|CTRL+X|Parancsfájl ablaktáblán, a konzol ablaktábla|
|**A parancsfájl található**|CTRL+F|A parancssori panelbe|
|**A parancsfájl következő keresése**|F3|A parancssori panelbe|
|**A parancsfájl előző keresése**|SHIFT+F3|A parancssori panelbe|
|**Paste**|CTRL+V|Parancsfájl ablaktáblán, a konzol ablaktábla|
|**Ismét:**|CTRL+Y|Parancsfájl ablaktáblán, a konzol ablaktábla|
|**Cserélje le a parancsfájl**|CTRL+H|A parancssori panelbe|
|**Mentés**|CTRL+S|A parancssori panelbe|
|**Az összes kijelölése**|CTRL+A|Parancsfájl ablaktáblán, a konzol ablaktábla|
|**Visszavonása**|CTRL+Z|Parancsfájl ablaktáblán, a konzol ablaktábla|

## <a name="keyboard-shortcuts-for-running-scripts"></a>A parancsfájlok futtatásához használható billentyűparancsok

A következő billentyűparancsokat használhatja a parancssori panelbe parancsfájlok futtatásakor.

|Művelet|Billentyűparancs|
|----------|---------------------|
|**új**|CTRL+N|
|**Open**|CTRL+O|
|**Futtatás**|F5|
|**Kijelölés futtatása**|F8|
|**Állítsa le a végrehajtás**|CTRL + BREAK BILLENTYŰKOMBINÁCIÓT. CTRL + C is használható, ha a környezet egyértelműen (Ha nincs kijelölt szöveg).|
|**A lapon** (a következő parancsfájl)|CTRL + TAB **Megjegyzés:** lapon a következő parancsfájl csak működik, ha Ön egy egyetlen PowerShell lap van megnyitva, amikor meg egynél több PowerShell lap van megnyitva, de a parancssori panelbe célja.|
|**A lapon** (az előző parancsfájl)|CTRL + SHIFT + TAB **Megjegyzés:** előző parancsfájl lapon működik, ha csak egy PowerShell lapon nyissa meg, vagy ha egynél több PowerShell lap van megnyitva, és a parancssori panelbe célja.|

## <a name="keyboard-shortcuts-for-customizing-the-view"></a>A nézet testreszabására használható billentyűparancsok

A következő billentyűparancsokat segítségével testre szabhatja a Windows PowerShell ISE nézetet. Az alkalmazás ablaktábláinak a elérhetők legyenek.

|Művelet|Billentyűparancs|
|----------|---------------------|
|**Ugrás a konzol ablaktáblában**|CTRL+D|
|**Nyissa meg a parancssori panelbe**|CTRL+I|
|**Parancsfájl ablaktábla megjelenítése**|CTRL + R|
|**Parancsfájl ablaktábla elrejtése**|CTRL + R|
||
|**A parancssori panelbe mozgatása felfelé**|CTRL+1|
|**A parancssori panelbe mozgatása jobbra**|CTRL+2|
|**A parancssori panelbe maximalizálása érdekében**|CTRL+3|
|**Nagyítás**|CTRL + PLUSZJEL|
|**Kicsinyítés**|CTRL + MÍNUSZJEL|

## <a name="keyboard-shortcuts-for-debugging-scripts"></a>A parancsfájlok hibakereséshez használható billentyűparancsok

A következő billentyűparancsokat használhatja a parancsfájlok hibakeresése.

|Művelet|Billentyűparancs|A használatára|
|----------|---------------------|----------|
|**Futtatás/folytatása**|F5|Parancsfájl ablaktáblán, ha a parancsprogram-hibakeresés|
|**Lépjen be**|F11|Parancsfájl ablaktáblán, ha a parancsprogram-hibakeresés|
|**Átlépés**|F10|Parancsfájl ablaktáblán, ha a parancsprogram-hibakeresés|
|**Kilépés**|SHIFT+F11|Parancsfájl ablaktáblán, ha a parancsprogram-hibakeresés|
|**Megjelenítési hívási verem**|CTRL + SHIFT + D|Parancsfájl ablaktáblán, ha a parancsprogram-hibakeresés|
|**Lista töréspontok**|CTRL+SHIFT+L|Parancsfájl ablaktáblán, ha a parancsprogram-hibakeresés|
|**Toggle Breakpoint**|F9|Parancsfájl ablaktáblán, ha a parancsprogram-hibakeresés|
|**Törölje a töréspontokat**|CTRL+SHIFT+F9|Parancsfájl ablaktáblán, ha a parancsprogram-hibakeresés|
|**A hibakereső leállítása**|SHIFT+F5|Parancsfájl ablaktáblán, ha a parancsprogram-hibakeresés|

> ![Megjegyzés:](../core-powershell/web-access/images/Note.jpeg)**Megjegyzés**
>
> A billentyűparancsok, a Windows PowerShell konzolhoz készült Windows PowerShell ISE parancsfájlok hibakeresése is használhatók. Használja ezeket a parancsokat, a konzol ablaktáblában írja be a helyi, és nyomja le az ENTER BILLENTYŰT.

|Művelet|Billentyűparancs|A használatára|
|----------|---------------------|----------|
|**Továbbra is**|C|Konzol ablaktáblában, ha a parancsprogram-hibakeresés|
|**Lépjen be**|S|Konzol ablaktáblában, ha a parancsprogram-hibakeresés|
|**Átlépés**|V|Konzol ablaktáblában, ha a parancsprogram-hibakeresés|
|**Kilépés**|O|Konzol ablaktáblában, ha a parancsprogram-hibakeresés|
|**Ismételje meg az utolsó parancs** (a lépésben azokat vagy Átlépés)|ENTER|Konzol ablaktáblában, ha a parancsprogram-hibakeresés|
|**Megjelenítési hívási verem**|K|Konzol ablaktáblában, ha a parancsprogram-hibakeresés|
|**Állítsa le a hibakeresést**|A Q|Konzol ablaktáblában, ha a parancsprogram-hibakeresés|
|**A parancsfájl felsorolása**|L|Konzol ablaktáblában, ha a parancsprogram-hibakeresés|
|**A konzol parancsok hibakeresés megjelenítése**|H vagy?|Konzol ablaktáblában, ha a parancsprogram-hibakeresés|

## <a name="keyboard-shortcuts-for-windows-powershell-tabs"></a>A Windows PowerShell lapok használható billentyűparancsok

A következő billentyűparancsokat használhatja lapok Windows PowerShell használatakor.

|Művelet|Billentyűparancs|
|----------|---------------------|
|**Zárja be a PowerShell lap**|CTRL+W|
|**Új PowerShell lap**|CTRL+T|
|**Előző PowerShell lap**|CTRL + SHIFT + TAB. Ezzel a billentyűparanccsal csak működik, ha nincs fájl megnyitva, a PowerShell lapon.|
|**Következő Windows PowerShell lap**|CTRL+TAB. Ezzel a billentyűparanccsal csak működik, ha nincs fájl megnyitva, a PowerShell lapon.|

## <a name="keyboard-shortcuts-for-starting-and-exiting"></a>Billentyűparancsok indítása és leállítása

A következő billentyűparancsokat használhatja a Windows PowerShell konzol indítása (PowerShell.exe) vagy a kilépéshez a Windows PowerShell ISE.

|Művelet|Billentyűparancs|
|----------|---------------------|
|**Exit**|ALT+F4|
|**Indítsa el a PowerShell.exe** (a Windows PowerShell konzol)|CTRL+SHIFT+P|

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE bemutatása](../core-powershell/ise/Introducing-the-Windows-PowerShell-ISE.md)