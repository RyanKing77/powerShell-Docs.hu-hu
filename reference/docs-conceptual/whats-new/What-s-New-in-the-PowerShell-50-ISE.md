---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Újdonságai a PowerShell 50 ISE-ben
ms.assetid: 38648d47-7c27-4b37-a40e-ad29948519c2
ms.openlocfilehash: 2d953bc4553de7720c590304d29750b84a1ef3b2
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058182"
---
# <a name="what39s-new-in-the-windows-powershell-ise"></a>Mi&#39;újdonságai a Windows PowerShell ISE-ben
Ez a témakör ismerteti a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) verzióban bevezetett új és frissített funkciókat.

## <a name="feature-description"></a>A szolgáltatás leírása
A Windows PowerShell ISE-ben egy fogadó alkalmazás, amely lehetővé teszi, hogy írási, futtatása és tesztelése a szkriptek és modulok grafikus és intuitív környezetben. Például a szintaxis-színezést, a legfontosabb jellemzők lapon befejezését, vizuális hibakeresési, Unicode-megfelelőség és környezetfüggő súgó gazdag parancsfájl-kezelési felületet biztosít.

Windows PowerShell ISE-ben áttekintését lásd: [Windows PowerShell integrált parancsfájlkezelési környezet áttekintése](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).

## <a name="new-and-changed-functionality-in-windows-powershell-ise"></a>Új és módosított funkciók a Windows PowerShell ISE-ben
A következő táblázat felsorolja az új és módosított szolgáltatások a Windows PowerShell ISE-ben a Windows PowerShellben, kiadás.

|Szolgáltatás/funkció|Windows PowerShell ISE-ben 4.0|Windows PowerShell ISE-ben 3.0|Windows PowerShell ISE-ben 2.0|
|--------------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
|**[IntelliSense](#intellisense)**|X|X||
|**[A kódrészletek](#snippets)**|X|X||
|**[Bővítmény-eszközök](#add-on-tools)**|X|X||
|**[Indítsa újra a Manager és az automatikus mentés](#restart-manager-and-auto-save)**|X|X||
|**[Legutóbb használt listája](#most-recently-used-list)**|X|X||
|**[Konzol panelen](#console-pane)**|X|X||
|**[Parancssori kapcsolók](#command-line-switches)**|X|X||
|**[Új szerkesztő szolgáltatások](#new-editor-features)**|X|X||
|**[Új súgó-megjelenítő ablakban](#new-help-viewer-window)**|X|X||
|**[Show-Command parancsmaggal](#show-command-cmdlet)**|X|X||

### <a name="intellisense"></a>IntelliSense
**A ISE-ben 3.0 hozzáadva**

Az IntelliSense az automatikus kiegészítését támogatás szolgáltatása, amely része a Windows PowerShell ISE-ben. Az IntelliSense potenciálisan egyező parancsmagok, paraméterek, paraméterértékeket, fájlok vagy mappák beírása kattintható menük jeleníti meg.

**Milyen hozzáadott értéket nyújt ez a változás?**

Az IntelliSense igény szerinti hozzáadásával célszerűbb a parancsmagok és a szintaxis észleléséhez, amikor a parancsfájlok létrehozásához használt Windows PowerShell ISE-ben. További Windows PowerShell új parancsfájlok létrehozásakor használhatja a Windows PowerShell ISE-ben.

**Mi működik másképp?**

Írja be a parancsmagok a Windows PowerShell ISE 3.0-s vagy újabb verzió, amikor egy görgethető és kattintható menü jeleníti meg, keresse meg és válassza ki a megfelelő parancsokat lehetővé teszi.

### <a name="snippets"></a>A kódrészletek
**A ISE-ben 3.0 hozzáadva**

*A kódrészletek* rövid szakaszok szúrhat be a parancsfájlok a Windows PowerShell ISE-ben létrehozhat Windows PowerShell-szabályzat. Windows PowerShell ISE-ben tartalmaz egy alapértelmezett részletek. A kódrészletek használatával adhat hozzá a **New-kódrészlet** parancsmag használatakor a Windows PowerShell ISE-ben.

**Milyen hozzáadott értéket nyújt ez a változás?**

A kódrészletek, gyorsan összeállíthat és a környezet automatizáló szkriptek létrehozására.

**Mi működik másképp?**

Kódrészletek a használata a Windows PowerShell 3.0-s vagy újabb, a **szerkesztése** menüben kattintson a **Start kódrészletek**, vagy nyomja le az **Ctrl-J**.

### <a name="add-on-tools"></a>Bővítmény-eszközök
**Új funkció a PowerShell 3.0**

Windows PowerShell ISE-ben mostantól támogatja a bővítmény eszközöket, amelyek a Windows megjelenítési Alaprendszeri (WPF) vezérlőelem, amely lehet hozzáadni a hálózatiobjektum-modellt. Bővítmény eszközök is megjeleníthetők a konzol egy függőleges vagy vízszintes ablaktáblát. A többlapos vezérlőként több bővítmény Eszközök panelen jelennek meg. Is hozzáadhat, vagy távolítsa el a Microsofton kívüli felek által készített eszközök bővítményt. Importálhatja, vagy távolítsa el a bővítményt eszközök kapcsolatos további információkért lásd: [Windows PowerShell ISE Operations](https://technet.microsoft.com/library/cc732148.aspx).

**Milyen hozzáadott értéket nyújt ez a változás?**

A bővítmények lehetővé teszik a kiterjesztéséhez és testre szabásához Windows PowerShell ISE-ben az eszközök, amelyek további funkciókkal bővítik a Windows PowerShell ISE-ben vagy a parancsfájl-kezelési környezet minőségét.

**Mi működik másképp?**

Windows PowerShell ISE-ben, 3.0-s és újabb verziók kapható a **parancsok** bővítményt. A **parancsok** bővítmény lehetővé teszi, hogy a parancsmagok keresse meg és érheti el a parancsmagok egymás mellett a Súgó a **parancsfájl** és **konzol** ablaktáblái.

További bővítmények találhatók használatával a **nyílt bővítmény eszközök webhely** parancs a **bővítmények** menü.

### <a name="restart-manager-and-auto-save"></a>Indítsa újra a manager és az automatikus mentés
**Új funkció a PowerShell 3.0**

Windows PowerShell ISE-ben mostantól automatikusan menti a megnyitott parancsfájlok két percenként, egy külön helyet.  Ha a Windows PowerShell ISE-ben nem működik, vagy ha az operációs rendszer újraindul, Windows PowerShell ISE újraindítása után, működés, visszaadhatja parancsfájlok, amelyek korábban nyissa meg a legutóbbi munkamenet akkor is, ha a parancsfájlok nem lettek mentve.

Az automatikus mentése időköz módosításához futtassa a következő parancsot a konzolablakban: **$psise. Options.AutoSaveMinuteInterval**.

**Milyen hozzáadott értéket nyújt ez a változás?**

Most már dolgozhat, hogy a nyílt parancsprogramok a rendszer automatikusan menti váratlan újraindítása esetén, hogy a Windows PowerShell ISE belül.

**Mi működik másképp?**

Windows PowerShell ISE 2.0 nem menti a parancsfájlok automatikus újraindítás esetén.

### <a name="most-recently-used-list"></a>Legutóbb használt listája
**Új funkció a PowerShell 3.0**

Windows PowerShell ISE-ben a legutóbb használt listáját a fájlok most már rendelkezik. Amikor megnyit egy fájlt a Windows PowerShell ISE-ben, a fájl bekerül a legutóbb használt listájának a a **fájl** menü.

A legutóbb használt listán fájl alapértelmezett számának módosításához futtassa a következő parancsot a konzolablakban: **$psise. Options.MruCount**.

**Milyen hozzáadott értéket nyújt ez a változás?**

A legutóbb használt lista használatával most már könnyedén elérheti a gyakran használt fájlok.

**Mi működik másképp?**

Windows PowerShell ISE 2.0 nem rendelkezik a legutóbb használt listáját.

### <a name="console-pane"></a>Konzol panelen
**Új funkció a PowerShell 3.0**

A külön parancsot és a Windows PowerShell ISE-ben az első kiadásban elérhető kimeneti ablaktábla mostantól egy egyetlen konzol ablaktáblában. A konzol ablaktáblában a függvény és a egy tipikus Windows PowerShell-konzolt a megjelenése hasonló, de (a legtöbb olyan ebben a témakörben leírtak szerint) a következő fejlesztéseket tartalmazza.

- Szintaxis színezést bemeneti szöveg (nem kimeneti szöveg), beleértve syntaxe XML

- IntelliSense

- Egyező kapcsos zárójel

- Hiba történt annak jelzése

- Teljes Unicode-támogatás

- **F1** környezetfüggő súgó

- **CTRL + F1** környezetfüggő Show-parancs

- A parancsfájl komplex és támogatja a jobbról balra

- Betűtípus-támogatás

- Nagyítás

- Vonal-válasszon és a blokk-válasszon módok

- A parancssorban, amikor lenyomja a beírt tartalom megőrzése az **mentése** nyílra a konzolon előzményeinek megtekintése

**Milyen hozzáadott értéket nyújt ez a változás?**

A konzolablakban a módosítások hozzáadása, amely megfelel a konzol felületét a parancsfájl-kezelési élményt nyújt.

**Mi működik másképp?**

Windows PowerShell ISE 2.0 rendelkezik, külön parancsot és a kimeneti ablaktábla.

### <a name="command-line-switches"></a>Parancssori kapcsolók
**Új funkció a PowerShell 3.0**

Ha a parancssorból indítsa el Windows PowerShell ISE-ben (beírásával **powershell_ise.exe**), a következő új parancssori kapcsolókat is hozzáadhat.

- *-NoProfile*: Elindítja a Windows PowerShell ISE-ben futó nélkül **$profile**

- *-Súgó*: A súgóablak megjelenítése

- *-mta*: Többszálú apartman módban indul el a Windows PowerShell ISE-ben. Az alapértelmezett működési mód a Windows PowerShell ISE-ben az egyszálas apartman módban, vagy *- sta*.

**Milyen hozzáadott értéket nyújt ez a változás?**

A parancssori kapcsolók igény szerinti hozzáadásával lehetővé teszi a környezet, amelyben a Windows PowerShell ISE-t futtató szabályozását.

**Mi működik másképp?**

Windows PowerShell ISE 2.0 nem ismeri fel a parancssori kapcsolók.

### <a name="new-editor-features"></a>Új szerkesztő szolgáltatások
**Új funkció a PowerShell 3.0**

Más Windows PowerShell ISE-ben szerkesztési funkciók a következők:

- **XML-szintaxis színezést**Windows PowerShell ISE-ben mostantól színek syntaxe XML ugyanúgy, ahogy azt a Windows PowerShell-szintaxis színek.

- **Kapcsos zárójel megfelelő** Windows PowerShell ISE-ben kiterjed kapcsos zárójel megfelelő, és a kiemelés, és az alábbi módon használható: (használata esetén például a **egyezés Ugrás** parancs vagy **Ctrl +]** megkeresi a Záró kapcsos zárójel, ha rendelkezik egy nyitó zárójel jelölve).

- **Vázlat nézetben** a parancsfájl panelen támogatja, felvázolva, amellyel összecsukás és kód szakaszait Kibontás plusz vagy mínusz kattintson a bal oldali margó bejelentkezik. Zárójelek között is használhatja, vagy a **#region** és **#endregion** címkék elején vagy végén egy összecsukható szakasz megjelölni. Kibontása vagy összecsukása minden régióban, nyomja le a **Ctrl + M**.

- **Áthúzása szövegszerkesztés**Windows PowerShell ISE-ben mostantól támogatja a áthúzása szöveg szerkesztése. Válassza ki bármelyik szövegblokk, és húzza át azt a szerkesztő vagy a konzol a szöveg áthelyezése egy másik helyre. Ha meg a Ctrl billentyűt lenyomva tartva húzza a kijelölt szöveg az egérgomb felengedésekor a szöveget az új helyre másolódik. Ebben a Windows PowerShell ISE-ben, valamint a régebbi Windows PowerShell ISE-ben, a Windows PowerShell ISE-ben, fájlokat áthúzása Windows PowerShell ISE-t megnyitja a fájlt.

- **Elemzési hiba megjelenített** piros aláhúzás jelöl, elemzési hibákat. Ha az egérmutatót a jelzett hiba, elemleírás jelenik meg a a probléma, amely a kódban található.

- **Nagyítás** nagyítás százalékos aránya a konzoltartalmak nagyítás csúszka segítségével (a jobb alsó sarokban a Windows PowerShell ISE-ablakot), vagy a parancs beírásával állítható **$psise.options.Zoom** a konzol ablaktáblában.

- **Rich text másolás és Beillesztés** betűtípusát, méretét, és az eredeti kijelölés színe információkat a Windows PowerShell ISE-ben megtartja a vágólapra másolása.

- **Letiltja a kijelölés** szöveg kiválasztásakor az egérrel a parancsfájl panelen az ALT billentyűt lenyomva vagy billentyű lenyomásával kiválaszthatja szövegblokk **Alt + Shift + nyíl**.

**Milyen hozzáadott értéket nyújt ez a változás?**

A további szerkesztési funkciók adjon meg egy egységes és a hatékony Kódszerkesztő környezetében.

**Mi működik másképp?**

Ezek a szerkesztési fejlesztések nem volt megtalálható a Windows PowerShell ISE 2.0.

### <a name="new-help-viewer-window"></a>Új súgó-megjelenítő ablakban
**Új funkció a PowerShell 3.0**

Ha lenyomja **F1** a kurzort egy parancsmag vagy van kiemelve a parancsmag részét, ha az új súgómegjelenítő megnyílik a környezetfüggő súgó a kiemelt parancsmaggal kapcsolatban. Windows PowerShell kapcsolatban súgójának megjelenítéséhez írja be a **operátorok** a konzol ablaktáblában, és nyomja le az **F1**.

Ez a funkció használatához töltse le a Windows PowerShell súgója témakörök legfrissebb verzióját a Microsoft webhelyén. A legegyszerűbb módja, ha a súgótémakörök letöltése, hogy futtassa a **Update-Help** parancsmag a konzol ablaktáblában, ha rendszergazdaként futtatja a Windows PowerShell ISE-ben.

Hol módosíthatja a **F1** kulcs segítséget keres. Az a **eszközök**/**beállítások** menü, az a **általános beállítások** lap **egyéb beállítások**, állítsa be, vagy törölje a jelet a jelölőnégyzet **online tartalom helyett használja a helyi súgó tartalma**. Ha be van jelölve, az ügyfél az a parancsmagot a letöltött súgó modulok mappában található segítséget keres.  Ha a jelölőnégyzet nincs bejelölve, majd az ügyfél néz ki mindez a TechNet könyvtárban a parancsmag súgóját.

**Milyen hozzáadott értéket nyújt ez a változás?**

Az aktuális parancsmag vagy szkript elhagyása nélkül környezetfüggő súgó zökkenőmentes tanulási élményt nyújt.

**Mi működik másképp?**

Korábbi verzióiban a Windows PowerShell ISE-ben az F1 billentyű megnyomásával megnyitni a súgófájlban a helyi számítógépen. A Windows PowerShell ISE 3.0-s és újabb verziók megnyílik egy ablak, amely tartalmazza a kereshető és konfigurálható a parancsmag súgóját. Az ügyféltámogatási élmény a Windows PowerShell ISE 3.0 új, és új Windows PowerShell 3.0 a frissíthető súgó.

### <a name="show-command-cmdlet"></a>Show-Command parancsmaggal
**Új funkció a PowerShell 3.0**

A **Show-parancs** parancsmag lehetővé teszi, hogy compose vagy egy parancsmag vagy függvény futtatása egy grafikus űrlap kitöltésével. Az űrlap lehetővé teszi, hogy a felhasználók grafikus környezetben a Windows PowerShell-lel dolgozni. **Show-parancs** is lehetővé teszi, hogy komplex, amely a Windows PowerShell-alapú gyors grafikus létrehozásához.

**Milyen hozzáadott értéket nyújt ez a változás?**

Használatával **Show-parancs** a Windows PowerShell-szkriptek, megadhatja a felhasználók számára, amellyel nem ismeri a grafikus környezetet. **Show-parancs** ismerje meg a Windows PowerShell bevezető felhasználók is segít.

**Mi működik másképp?**

Show-parancsot az új Windows PowerShell ISE 3.0.

## <a name="see-also"></a>Lásd még:
Windows PowerShell ISE-ben a Windows PowerShellben való használatáról további információkért lásd az alábbi hivatkozásokat.

- [A Windows PowerShell integrált parancsfájlkezelési környezetet felfedezése](../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
- [ISE-ben a TechNet-Wikiben](https://social.technet.microsoft.com/wiki/search/searchresults.aspx?q=ISE)
- [Script Center](https://technet.microsoft.com/scriptcenter/default)