---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell ISE felfedezése"
ms.assetid: e0d2c6e8-5126-40e7-a1e1-d1cff29fe94a
ms.openlocfilehash: 979209d4b200728b7e78e341bb9595741d2b8e68
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="exploring-the-windows-powershell-ise"></a>A Windows PowerShell ISE felfedezése
A Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE) hozhat létre, futtatása és hibakeresési parancsaiban és parancsfájljaiban. A Windows PowerShell ISE az egérrel a menüsoron, Windows PowerShell-lapok, az eszköztár, parancsprogram lapfülek, egy parancsfájl ablaktáblán, a konzol ablaktáblában, állapotjelző, szöveges méretű csúszkát és áll környezetfüggő súgó.

> [!NOTE]
> A parancs és a kimeneti ablaktábla Windows PowerShell ISE 3.0-val kezdődő konzol egytáblás egyesítve volt.

## <a name="menu-bar"></a>Menüsáv
Az egérrel a menüsoron tartalmazza a **fájl**, **szerkesztése**, **nézet**, **eszközök**, **Debug**,  **A bővítmények**, és **súgó** menün kellene végiglépkednie. A menük gombok lehetővé teszik írása és futó parancsfájlok és a Windows PowerShell ISE futó parancsokat kapcsolatos feladatok elvégzéséhez. Emellett egy [bővítmény eszköz](../../core-powershell/ise/The-ISEAddOnTool-Object.md) lehet helyezni az egérrel a menüsoron alkalmazó parancsfájlok futtatásával a [Windows PowerShell ISE Scripting objektum modell](../../core-powershell/ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md).

> [!NOTE]
> A Windows PowerShell ISE 2.0 a **eszközök** és **bővítmények** menük nem volt jelen.

## <a name="windows-powershell-tabs"></a>A Windows PowerShell lapokon
A Windows PowerShell lap jelenik meg a környezetben, amelyben egy Windows PowerShell-parancsfájlt futtatja. Új Windows PowerShell-lapok nyithatja meg a Windows PowerShell ISE külön környezetek létrehozása, a helyi számítógépen vagy távoli számítógépeken. Előfordulhat, hogy legfeljebb nyolc PowerShell egyidejűleg nyissa meg a lapokon.

## <a name="toolbar"></a>Eszköztár
A következő gombok találhatók az eszköztáron.

|Gomb|Függvény|
|----------|------------|
|**Új**|Megnyílik egy új parancsfájlt.|
|**Nyissa meg**|Egy meglévő parancsfájl vagy a fájl megnyitása.|
|**Mentése**|Egy parancsfájl vagy a fájl mentése.|
|**Kivágás**|A kijelölt szöveg kivágja, és a vágólapra másolja azt.|
|**Másolás**|A kijelölt szöveg a vágólapra másolja.|
|**Beillesztés**|A kurzor helyen a vágólap tartalmának beillesztése.|
|**Törölje a Tesztkimenet ablaktáblán**|A kimeneti ablaktábla teljes tartalmát törli.|
|**Visszavonása**|A művelet csak végrehajtott visszavonása.|
|**Ismét:**|Az imént visszavont művelet végrehajtása.|
|**Parancsfájl futtatása**|Parancsfájlok futtatására.|
|**Selction futtatása**|Egy kijelölt része egy parancsfájlt futtat.|
|**Állítsa le a végrehajtás**|Egy parancsfájlt futtató leáll.|
|**Új távoli PowerShell lap**|Létrehoz egy új PowerShell-lap, amely létrehozza a munkamenetet egy távoli számítógépen. Egy párbeszédpanel jelenik meg, és megkéri, hogy adja meg a távoli kapcsolat létrehozásához szükséges adatokat.|
|**Indítsa el a PowerShell.exe**|Megnyitja a PowerShell-konzolban.|
|**Parancsfájl ablaktábla felső megjelenítése**|A parancssori panelbe áthelyezése a képernyő tetején.|
|**Parancsfájl ablak jobb megjelenítése**|A parancssori panelbe áthelyezése a képernyő jobb.|
|**Teljes méretű parancsfájl ablaktábla megjelenítése**|A parancsfájl ablaktábla a lehető legnagyobbra növeli.|

## <a name="script-tab"></a>Parancsfájl lap
Megjeleníti a most szerkesztés alatt álló parancsfájl nevét. Kattintson a parancsfájl lapon válassza ki a szerkeszteni kívánt parancsfájlt.

Ha a parancsfájl lapra mutat, a parancsfájl teljes elérési útja a elemleírás jelenik meg.

## <a name="script-pane"></a>A parancssori panelbe
Lehetővé teszi, hogy hozhat létre, és a parancsfájlok futtatása. Nyissa meg, szerkesztheti, és a parancssori panelbe meglévő parancsfájlok futtatása.

## <a name="output-pane"></a>Kimeneti ablaktábla
Megjeleníti az eredményeket a parancsok és a parancsfájlok futtatása. Is másolja, és a kimeneti ablak tartalmának törlése.

## <a name="command-pane"></a>A parancs ablaktábla
Lehetővé teszi a parancsok írása. A parancs ablaktáblán egy egy sort vagy egy többsoros parancsot futtathatja. Nyomja le a SHIFT + ENTER minden sor egy többsoros parancs, és nyomja le az ENTER BILLENTYŰT a többsoros parancs utolsó sora után. A parancssorba a parancs ablaktábla tetején megjeleníteni az aktuális munkakönyvtárban elérési jeleníti meg.

## <a name="status-bar"></a>Állapotsor
Lehetővé teszi, hogy a parancsok és futtatott parancsfájlok teljes. Az állapotsor van nagyon a képernyő alján. Az állapotsor kiválasztott részeinek hibaüzenetek jelennek meg.

## <a name="text-size-slider"></a>Szövegméret – csúszka
Növeli vagy csökkenti a képernyőn megjelenő méretét.

## <a name="help"></a>Súgó
Windows PowerShell ISE súgója is elérhető a weben a TechNet könyvtárban. A Súgó gombra kattintva megnyithatja **Windows PowerShell ISE súgó** a a **súgó** menü vagy bárhol kivéve, ha a kurzor a parancsmag neve vagy a parancsfájl vagy a konzol ablaktáblában az F1 billentyű lenyomásával. Az a **súgó** menü is futtassa az Update-Help parancsmagot, és a parancssori ablakban, amely segítséget nyújt a parancsok kialakításánál jelenít meg minden, a parancsmag paramétereit, és engedélyezésével, hogy adja meg a paramétereket a megjelenítendő egy könnyen használható formátumban.

## <a name="see-also"></a>Lásd még:
- [A Windows PowerShell ISE használatával](../../core-powershell/ise/Using-the-Windows-PowerShell-ISE.md)

