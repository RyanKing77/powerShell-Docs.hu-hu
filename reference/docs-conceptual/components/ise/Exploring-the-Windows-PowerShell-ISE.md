---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A Windows PowerShell ISE felfedezése
ms.openlocfilehash: 8c47e236e2e345a887fc3af281e429f440e176ff
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67031023"
---
# <a name="exploring-the-windows-powershell-ise"></a>A Windows PowerShell ISE felfedezése

A Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE) segítségével létrehozása, futtatása és hibakeresési parancsaiban és parancsfájljaiban. A Windows PowerShell ISE-ben a menüsávon, Windows PowerShell-lapok, az eszköztáron, parancsfájl lapok, a parancsfájl panelen, a konzol ablaktáblában, állapotjelző, egy szöveg méretű csúszka és környezetfüggő súgó áll.

> [!NOTE]
> Verziótól kezdve a Windows PowerShell ISE 3.0, a parancs, és a kimeneti ablaktábla is mostantól egy egyetlen konzol ablaktáblában.

## <a name="menu-bar"></a>A menüsávon

A menüsávon tartalmazza a **fájl**, **szerkesztése**, **nézet**, **eszközök**, **Debug**,  **A bővítmények**, és **súgó** menün kellene végiglépkednie. A gombok a menük parancsfájlok írása és fut, és a Windows PowerShell ISE-ben futó parancsokat kapcsolatos feladatok lehetővé teszik. Ezenkívül egy [bővítmény eszköz](../../core-powershell/ise/The-ISEAddOnTool-Object.md) használó parancsprogramok futtatásával a menüsávon előfordulhat, hogy helyezni a [az ISE objektummodell-hierarchiája](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md).

> [!NOTE]
> A Windows PowerShell ISE 2.0 a **eszközök** és **bővítmények** menük nem volt jelen.

## <a name="windows-powershell-tabs"></a>Windows PowerShell-lap

Windows PowerShell-lap, a környezet, amelyben egy Windows PowerShell-parancsfájlt futtat. Új Windows PowerShell-lapokon megnyithatja a Windows PowerShell ISE-ben, létrehozhat olyan külön környezeteket a helyi számítógépen vagy távoli számítógépeken. Előfordulhat, hogy legfeljebb nyolc PowerShell lapok egyszerre megnyitásához.

## <a name="toolbar"></a>Eszköztár

A következő gomb az eszköztáron található.

|Gomb|Függvény|
|----------|------------|
|**Új**|Ekkor megnyílik egy új parancsfájlt.|
|**Open**|Egy meglévő parancsfájl vagy fájl megnyitása.|
|**Mentés**|Olyan parancsfájl vagy a fájl mentése.|
|**Cut**|A kijelölt szöveg kivágja, és másolja a vágólapra.|
|**Másolás**|A kijelölt szöveg másolása a vágólapra.|
|**Paste**|A kurzor helyen a vágólap tartalmának beillesztése.|
|**Törölje a Tesztkimenet ablaktáblán**|Törli az összes tartalom a Tesztkimenet ablaktáblán.|
|**A Visszavonás**|Az imént végrehajtott művelet visszavonása.|
|**Redo**|Az imént visszavont művelet végrehajtása.|
|**Parancsfájl futtatása**|Parancsfájlok futtatására szolgál.|
|**Kijelölés futtatása**|Egy kiválasztott része egy parancsfájlt futtat.|
|**Végrehajtási leállítása**|Leállítja egy parancsfájlt, hogy fut-e.|
|**Új távoli PowerShell-lap**|Létrehoz egy új PowerShell-lap, amely létrehozza egy munkamenetet egy távoli számítógépen. Egy párbeszédpanel jelenik meg, és megkéri, hogy adja meg a távoli kapcsolat létrehozásához szükséges adatokat.|
|**Indítsa el a PowerShell.exe**|Megnyílik egy PowerShell-konzolt.|
|**Parancsfájl ablaktábla felső megjelenítése**|A parancsfájl panelen jelennek meg a felső helyezi át.|
|**Jobb oldali parancsfájl ablaktábla megjelenítése**|A parancsfájl panelen jelennek meg a jobbra helyezi át.|
|**Teljes méretű parancsfájl ablaktábla megjelenítése**|Maximalizálja a parancsfájl panelen.|

## <a name="script-tab"></a>Script lapon

Megjeleníti a parancsfájl szerkesztésekor nevét. Kattinthat a parancsfájl lapon válassza ki a szerkeszteni kívánt parancsfájlt.

Ha a parancsfájl lapra mutat, a parancsfájl teljes elérési útja egy elemleírás jelenik meg.

## <a name="script-pane"></a>Szkriptpanel

Szkriptek létrehozása és futtatása teszi lehetővé. Nyissa meg, szerkesztheti és meglévő szkriptek futtatása a parancsfájl panelen.

## <a name="output-pane"></a>Tesztkimenet ablaktáblán

A parancsok és szkriptek futtatása eredményeit jeleníti meg. Emellett másolja, és a tartalmát a Tesztkimenet ablaktáblán.

## <a name="command-pane"></a>A parancs panel

Lehetővé teszi, hogy-parancsok írásával. Egy egysoros vagy egy többsoros parancsot futtathatja a parancsot ablaktáblán. Nyomja le a SHIFT + ENTER billentyűkombinációt minden sor egy többsoros parancs, és nyomja le az ENTER többsoros parancs végrehajtása utolsó sora után. A rendszer kéri, a parancs ablaktábla tetején megjeleníteni az aktuális munkakönyvtárban elérési útját jeleníti meg.

## <a name="status-bar"></a>Állapotsor

Lehetővé teszi, hogy a parancsok és az Ön által futtatott parancsfájlok, vannak-e befejeződött. Az állapotsáv van nagyon a képernyő alján. Az állapotsorban kiválasztott részeinek hibaüzenetek jelennek meg.

## <a name="text-size-slider"></a>Szövegméret – csúszka

Növeli vagy csökkenti a képernyőn megjelenő méretét.

## <a name="help"></a>Súgó

Súgó a Windows PowerShell ISE-ben érhető el a TechNet-könyvtárban a weben. A Súgó gombra kattintva megnyithatja **Windows PowerShell ISE-súgó** a a **súgó** menü vagy bárhol kivéve, ha a kurzort a parancsmag neve Szkriptpanel vagy a konzol ablaktáblában az F1 billentyű lenyomásával. Az a **súgó** menüben is futtassa az Update-Help parancsmagot, és a parancssori ablakba, amely segítséget nyújt parancsokat felépítéséhez megjeleníti az összes a parancsmag paramétereit, és lehetővé téve a töltse ki a paramétereket a megjelenítendő egy könnyen használható űrlap.

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE bemutatása](../../core-powershell/ise/Introducing-the-Windows-PowerShell-ISE.md)
