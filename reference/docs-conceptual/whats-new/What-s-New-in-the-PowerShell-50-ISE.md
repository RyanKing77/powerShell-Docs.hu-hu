---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A PowerShell 50 a milyen s ISE
ms.assetid: 38648d47-7c27-4b37-a40e-ad29948519c2
ms.openlocfilehash: 9fd25a4759602bebf2b5df2c17d0c816a15e5e2b
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="what39s-new-in-the-windows-powershell-ise"></a>Mi&#39;a újdonságai a Windows PowerShell ISE s
Ez a témakör ismerteti a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) verzióban bevezetett új és frissített szolgáltatásai.

## <a name="feature-description"></a>A szolgáltatás leírása
A Windows PowerShell ISE még egy fogadó alkalmazás, amely lehetővé teszi a írási, futtatására, és tesztelje a parancsfájlokat és a modulok grafikus és intuitív környezetben. A legfontosabb jellemzők zintaxisszínek, például lapon befejezését, visual-hibakeresés, Unicode-megfelelőségi és környezetfüggő Súgó hatékony programozási környezetet biztosítson.

A Windows PowerShell ISE áttekintését lásd: [Windows PowerShell integrált parancsfájlkezelési környezet áttekintése](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).

## <a name="new-and-changed-functionality-in-windows-powershell-ise"></a>A Windows PowerShell ISE új és módosított funkciók
A következő táblázat felsorolja az új és módosított szolgáltatások a jelen kiadása a Windows PowerShell ISE a Windows PowerShellben.

|Szolgáltatás/funkció|A Windows PowerShell ISE 4.0|A Windows PowerShell ISE 3.0|Windows PowerShell ISE 2.0|
|--------------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
|**[IntelliSense](#intellisense)**|X|X||
|**[Részletek](#snippets)**|X|X||
|**[Bővítmény eszközök](#add-on-tools)**|X|X||
|**[Indítsa újra a Manager és az automatikus mentés](#restart-manager-and-auto-save)**|X|X||
|**[A legtöbb-legutóbbi listája](#most-recently-used-list)**|X|X||
|**[Konzol ablaktáblában](#console-pane)**|X|X||
|**[Parancssori kapcsolók](#command-line-switches)**|X|X||
|**[Új szerkesztő szolgáltatások](#new-editor-features)**|X|X||
|**[Új súgó-megjelenítő ablakban](#new-help-viewer-window)**|X|X||
|**[Megjelenítése-Command parancsmaggal](#show-command-cmdlet)**|X|X||

### <a name="intellisense"></a>IntelliSense
**A hozzáadott ISE 3.0**

IntelliSense az automatikus-végrehajtási segítséget szolgáltatása, amely része a Windows PowerShell ISE. IntelliSense megjeleníti a parancsmagok, paraméterek, a paraméterértékek, fájlok vagy mappák potenciálisan megfelelő beíráskor kattintható menük.

**Milyen hozzáadott értéket nyújt ez a változás?**

IntelliSense hozzáadásával ezért könnyebben parancsmagok és szintaxis észleléséhez, amikor a Windows PowerShell ISE parancsfájlok létrehozására használhatja. A Windows PowerShell ISE segítségével ismerje meg a Windows PowerShell új parancsfájlok létrehozása során.

**Mi működik másképp?**

Amikor beírja parancsmagok a Windows PowerShell ISE 3.0-s vagy újabb, egy görgethető és kattintható menü jeleníti meg, keresse meg és jelölje ki a megfelelő parancsokat.

### <a name="snippets"></a>Részletek
**A hozzáadott ISE 3.0**

*Kódtöredékek* a Windows PowerShell-kódot hoz létre a Windows PowerShell ISE parancsfájlok beilleszthet rövid szakaszok is vannak. A Windows PowerShell ISE kódtöredékek alapértelmezett készletét tartalmazza. Kódtöredékek használatával adhat hozzá a **New-részlet** parancsmag a Windows PowerShell ISE végzett munka közben.

**Milyen hozzáadott értéket nyújt ez a változás?**

Részletek segítségével gyorsan állítson össze és automatizálását a környezetében parancsfájlokat hozhatnak létre.

**Mi működik másképp?**

Kódtöredékek használata a Windows PowerShell 3.0-s vagy újabb, a **szerkesztése** menüben kattintson a **Start kódtöredékek**, vagy nyomja le az ENTER **Ctrl-J**.

### <a name="add-on-tools"></a>Bővítmény eszközök
**A PowerShell 3.0 hozzáadva**

A Windows PowerShell ISE mostantól támogatja a bővítmény eszközök, amelyek Windows megjelenítési alaprendszer (WPF) vezérlők, amelyek felhasználásával a hálózatiobjektum-modellt. Bővítmények megjelenítése a konzol egy függőleges vagy vízszintes ablaktáblát. Lapokra vezérlőként több bővítmény eszközök ablaktáblában jelennek meg. Hozzáadhat, vagy távolítsa el a bővítmény eszközök, amelyek a Microsofton kívüli más felek hozzák létre. Importálandó, vagy távolítsa el a bővítmény eszközök kapcsolatos további információkért lásd: [Windows PowerShell ISE műveletek](http://technet.microsoft.com/library/cc732148.aspx).

**Milyen hozzáadott értéket nyújt ez a változás?**

A bővítmények lehetővé teszik bővíthető és testreszabható a Windows PowerShell ISE, amelyek a parancsfájl-kezelési élmény javítása érdekében vagy funkciókat adnak hozzá a Windows PowerShell ISE eszközökkel.

**Mi működik másképp?**

A Windows PowerShell ISE 3.0-s és újabb verziói rendelkeznek a **parancsok** bővítmény. A **parancsok** bővítmény lehetővé teszi a parancsmagok keresse meg és érheti el a parancsmagok-mellé a vonatkozó súgó megjelenítéséhez a **parancsfájl** és **konzol** ablaktábla.

További bővítmények található használatával a **bővítmény eszközök webhely megnyitása** parancs a **bővítmények** menü.

### <a name="restart-manager-and-auto-save"></a>Indítsa újra a manager és az automatikus mentés
**A PowerShell 3.0 hozzáadva**

Windows PowerShell ISE mostantól automatikusan menti a Megnyitás parancsfájlokba két percenként másik helyen.  Ha a Windows PowerShell ISE nem működik, vagy ha az operációs rendszer újraindítása után a Windows PowerShell ISE újraindul, helyreállítja parancsfájlok, melyeket nyissa meg az utolsó munkamenetnek, még akkor is, ha a parancsfájlok nem sikerült menteni.

Az automatikus mentése időköz módosításához futtassa a következő parancsot a konzol ablaktáblában: **$psise. Options.AutoSaveMinuteInterval**.

**Milyen hozzáadott értéket nyújt ez a változás?**

Most már dolgozhat ismerete, hogy a Megnyitás parancsfájlokba automatikusan menti a rendszer váratlan újraindítása esetén a Windows PowerShell ISE belül.

**Mi működik másképp?**

A Windows PowerShell ISE 2.0 nem menti a parancsfájlok automatikusan esetén a számítógép újraindítását.

### <a name="most-recently-used-list"></a>A legtöbb-legutóbbi listája
**A PowerShell 3.0 hozzáadva**

Windows PowerShell ISE most már rendelkezik a legtöbb legutóbb használt fájlok listáját. Amikor megnyit egy fájlt a Windows PowerShell ISE, a fájl kerül a legtöbb legutóbb használt lista a a **fájl** menü.

A legtöbb legutóbb használt fájlok alapértelmezett számának módosításához, futtassa a következő parancsot a konzol ablaktáblában: **$psise. Options.MruCount**.

**Milyen hozzáadott értéket nyújt ez a változás?**

A legtöbb legutóbb használt lista segítségével mostantól egyszerűen hozzáférhessenek a gyakran használt fájlokat.

**Mi működik másképp?**

A Windows PowerShell ISE 2.0 nem rendelkezik a legtöbb legutóbb használt listáját.

### <a name="console-pane"></a>Konzol ablaktáblában
**A PowerShell 3.0 hozzáadva**

A külön parancs és a kimeneti ablaktábla elérhető Windows PowerShell ISE első kiadása már megtörtént egyesített konzol egytáblás. A konzol ablaktáblában függvény és egy tipikus Windows PowerShell-konzolba megjelenése hasonló, de (a legtöbb ebben a témakörben ismertetett) a következő fejlesztéseket tartalmazza.

- Zintaxisszínek bemeneti szöveg (kimeneti szöveg nem), beleértve az XML-szintaxis

- IntelliSense

- Megfelelő zárójel

- Hiba arra utal, hogy

- Teljes Unicode-támogatás

- **F1** környezetfüggő súgó

- **CTRL + F1** környezetfüggő megjelenítése-parancs

- Összetett parancsfájl és jobbról balra támogatás

- Betűtípus-támogatás

- Nagyítás

- Vonal-válassza ki, és a blokk-válassza módok

- A parancssorban megnyomásakor beírt tartalom megőrzése a **mentése** mutató nyílra kattintva a konzol előzményeinek megtekintése

**Milyen hozzáadott értéket nyújt ez a változás?**

A konzol ablaktáblában módosítások hozzáadását, amely több azonos-e a konzol felületét parancsfájl-kezelési élményt nyújt.

**Mi működik másképp?**

A Windows PowerShell ISE 2.0 rendelkezik, külön parancs és a kimeneti ablaktábla.

### <a name="command-line-switches"></a>Parancssori kapcsolók
**A PowerShell 3.0 hozzáadva**

Ha a parancssorból indítsa el a Windows PowerShell ISE (írja be a **powershell_ise.exe**), a következő új parancssori kapcsolókat is hozzáadhat.

- *-NoProfile*: elindul a Windows PowerShell ISE futtatása nélkül **$profile**

- *-Súgó*: a súgóablak megjelenítése

- *-mta*: Windows PowerShell ISE többszálas apartman módban indul. Az alapértelmezett működési mód a Windows PowerShell ISE egyszálas apartman módban, vagy *- sta*.

**Milyen hozzáadott értéket nyújt ez a változás?**

A parancssori kapcsolók hozzáadása lehetővé teszi, hogy a környezet, amelyben a Windows PowerShell ISE fut. szabályozzák.

**Mi működik másképp?**

A Windows PowerShell ISE 2.0 nem ismeri fel a parancssori kapcsolók.

### <a name="new-editor-features"></a>Új szerkesztő szolgáltatások
**A PowerShell 3.0 hozzáadva**

Más Windows PowerShell ISE szerkesztési funkciói a következők:

- **XML-zintaxisszínek**Windows PowerShell ISE most színek XML szintaxis ugyanúgy, mint azt a Windows PowerShell-szintaxis színek.

- **Megfelelő zárójel** Windows PowerShell ISE megfelelő zárójel és kiemelve, és a következőképpen használható: (használata esetén például a **egyezés Ugrás** parancs vagy **Ctrl +]** megkeresi a záró zárójel, ha egy kijelölt nyitó zárójel).

- **Vázlat nézetben** a parancssori panelbe támogatja, tagolás, amely lehetővé teszi, hogy összecsukás és kód szakasza Kibontás plusz vagy mínusz kattintva jelentkezik be a bal margó. Használhatja a kapcsos zárójelek vagy a **#region** és **#endregion** címkék elején vagy végén egy összecsukható szakasz megjelölni. Kibontásához vagy összecsukásához minden egyes, nyomja le az **Ctrl + M**.

- **Áthúzása szöveg szerkesztése**Windows PowerShell ISE most támogatja áthúzása szöveg szerkesztése. Jelöljön ki egyetlen szövegrészt, és húzza a szöveget a szerkesztő vagy a konzol a szöveg áthelyezése egy másik helyre. Ha lenyomva tartja a Ctrl billentyűt, miközben a kijelölt szöveg az egérgomb felengedésekor a szöveget az új helyre másolódik. Ebben a Windows PowerShell ISE, valamint a Windows PowerShell ISE korábbi verzióját, a Windows PowerShell ISE fájlokat áthúzása Windows PowerShell ISE megnyitja a fájlt.

- **Elemzési hiba megjelenítési** piros aláhúzás jelöl, elemzési hibákat. Ha hibát jelzett, telepített mutat, elemleírás jelenik meg a probléma megoldására a kódban található.

- **Nagyítás** nagyítás százalékos aránya a konzol "™ s tartalom állítható be a nagyítási csúszkát (a jobb alsó sarkában Windows PowerShell ISE ablaka), vagy a parancs **$psise.options.Zoom** a konzol ablaktáblában.

- **Rich text másolás és Beillesztés** a betűtípus mérete és szín adatokat az eredeti kijelölés a Windows PowerShell ISE megtartja a vágólapra másolása.

- **Kijelölés blokkolása** szövegblokk választhatja ki a parancsfájl ablaktáblán az egérrel szöveg kijelölése közben az ALT billentyűt lenyomva tartja, vagy billentyűkombináció lenyomásával **Alt + Shift + mutató nyílra**.

**Milyen hozzáadott értéket nyújt ez a változás?**

A további szerkesztési funkcióival egy egységes és hatékony szerkesztési környezetben.

**Mi működik másképp?**

Szerkesztési fejlesztéseknek nem volt megtalálható a Windows PowerShell ISE 2.0.

### <a name="new-help-viewer-window"></a>Új súgó-megjelenítő ablakban
**A PowerShell 3.0 hozzáadva**

Ha lenyomja az **F1** parancsmag a kurzor áll, vagy van kiemelve parancsmag részét, az új súgómegjelenítő nyílik meg a kijelölt parancsmag vonatkozó környezetfüggő súgó. A Windows PowerShell vonatkozó súgó megjelenítéséhez írja be **operátorok** a konzol ablaktáblában, majd nyomja le az **F1**.

Ez a funkció használatához Windows PowerShell súgója témakörök legújabb verziója letölthető a Microsoft webhelyén. A legegyszerűbb módja, ha a súgótémakörök letöltése futtatni a **Update-Help** parancsmag a konzol ablaktáblában, ha fut a Windows PowerShell ISE rendszergazdaként.

Hol megváltoztathatja a **F1** kulcs segítséget keres. A a **eszközök**/**beállítások** menü, az a **általános beállítások** lap **egyéb beállítások**, állítsa be, vagy törölje a jelölőnégyzet **online tartalom helyett használja a helyi súgó tartalma**. Ha be van jelölve, majd az ügyfél keresi a parancsmag segítségre van szüksége a letöltött súgó modulok mappában található.  Ha a jelölőnégyzet nincs bejelölve, majd az ügyfél jelenik meg a TechNet könyvtárban a parancsmag súgóját.

**Milyen hozzáadott értéket nyújt ez a változás?**

Környezetfüggő súgó anélkül, hogy az aktuális parancsmag vagy parancsfájl tanulási zökkenőmentes élményt nyújt.

**Mi működik másképp?**

A súgófájl a helyi számítógépen a Windows PowerShell ISE korábbi verzióiban az F1 billentyű megnyomásával megnyitva. A Windows PowerShell ISE 3.0-s és újabb verziók megnyílik egy ablak, amely tartalmazza a parancsmag, amely kereshető és konfigurálható a Súgó gombra. A Súgó élmény új Windows PowerShell ISE 3.0, és új Windows PowerShell 3.0 frissített súgó.

### <a name="show-command-cmdlet"></a>Megjelenítése-Command parancsmaggal
**A PowerShell 3.0 hozzáadva**

A **megjelenítése-parancs** parancsmag lehetővé teszi állítható össze, vagy futtassa egy parancsmag vagy a függvény egy grafikus űrlap kitöltésével. Az űrlap lehetővé teszi, hogy a felhasználók grafikus környezetben a Windows PowerShell-lel dolgozni. **A parancs megjelenítése** is lehetővé teszi, hogy speciális, amely a gyors Windows PowerShell-alapú grafikus felhasználói felületének létrehozásához.

**Milyen hozzáadott értéket nyújt ez a változás?**

A **megjelenítése-parancs** a Windows PowerShell-parancsfájlok, megadhatja a felhasználók a grafikus környezet, amelyhez nem ismeri. **A parancs megjelenítése** is hozzájárulhat a bevezető felhasználók ismerje meg a Windows PowerShell.

**Mi működik másképp?**

Show-parancsot az új Windows PowerShell ISE 3.0.

## <a name="see-also"></a>Lásd még:
A Windows PowerShell ISE a Windows PowerShell használatával kapcsolatos további információkért tekintse meg a következőket.

- [A Windows PowerShell integrált parancsfájlkezelési környezet felfedezése](../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
- [A TechNet Wiki ISE](http://social.technet.microsoft.com/wiki/search/searchresults.aspx?q=ISE)
- [Script Center](http://technet.microsoft.com/scriptcenter/default)

