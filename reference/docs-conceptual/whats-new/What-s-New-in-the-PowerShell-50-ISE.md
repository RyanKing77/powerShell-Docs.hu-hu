---
ms.date: 09/06/2019
keywords: PowerShell, parancsmag
title: A PowerShell 5,0 ISE újdonságai
ms.openlocfilehash: a719baef0da1600f0a5377e1b72c81b67e37eef2
ms.sourcegitcommit: a74ae7ed089301992fed201fbe55d827a622afa0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70746224"
---
# <a name="whats-new-in-the-windows-powershell-50-ise"></a>A Windows PowerShell 5,0 ISE újdonságai

Ez a témakör a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) verzióiban bevezetett új és frissített funkciókat ismerteti.

## <a name="feature-description"></a>A szolgáltatás leírása

A Windows PowerShell integrált parancsprogram-kezelési környezet egy olyan gazda-alkalmazás, amely lehetővé teszi parancsfájlok és modulok írását, futtatását és tesztelését grafikus és intuitív környezetben. A főbb funkciók, mint például a szintaxis – színezés, a tabulátorok befejezése, a vizualizációs hibakeresés, a Unicode-megfelelőség és a környezetfüggő súgó nyújt széles körű programozási élményt.

További információ: [a Windows PowerShell integrált parancsprogram-kezelési környezet bemutatása](../components/ise/Introducing-the-Windows-PowerShell-ISE.md).

A következő táblázat a Windows PowerShell integrált parancsprogram-kezelési környezet ezen kiadásának új és megváltozott funkcióit sorolja fel a Windows PowerShellben.

## <a name="intellisense"></a>IntelliSense

> Az ISE 3,0-ben hozzáadva

Az IntelliSense egy automatikus kiegészítési szolgáltatás, amely a Windows PowerShell integrált parancsprogram-kezelési környezet részét képezi.
Az IntelliSense a beíráskor a potenciálisan egyező parancsmagok, paraméterek, paraméterérték, fájlok vagy mappák kattintható menüit jeleníti meg.

**Milyen értéket vesz fel ez a változás?**

Az IntelliSense hozzáadásával könnyebben felderítheti a parancsmagokat és a szintaxist, ha a Windows PowerShell integrált parancsprogram-kezelési környezet használatával parancsfájlokat hoz létre. Az új parancsfájlok létrehozásakor Windows PowerShell integrált parancsprogram-kezelési környezet is megismerheti a Windows PowerShellt.

**Mi működik másképp?**

Ha parancsmagokat gépel be a Windows PowerShell integrált parancsprogram-kezelési környezetba, egy görgethető és kattintható menü jelenik meg, amely lehetővé teszi a megfelelő parancsok tallózását és kiválasztását.

## <a name="snippets"></a>Kódrészletek

> Az ISE 3,0-ben hozzáadva

A *kódrészletek* a Windows PowerShell-kód rövid részei, amelyeket beillesztheti a Windows PowerShell integrált parancsprogram-kezelési környezetban létrehozott parancsfájlba. A Windows PowerShell integrált parancsprogram-kezelési környezet a kódrészletek alapértelmezett készletét tartalmazza. Kódrészleteket a `New-Snippet` parancsmag használatával adhat hozzá Windows PowerShell integrált parancsprogram-kezelési környezetban való munka közben.

**Milyen értéket vesz fel ez a változás?**

A kódrészletek használatával gyorsan összeállíthat és létrehozhat parancsfájlokat a környezet automatizálásához.

**Mi működik másképp?**

Ha a kódrészleteket a Windows PowerShell 3,0-es vagy újabb verziójában szeretné használni, akkor a **Szerkesztés** menüben kattintson a **kódrészletek indítása**lehetőségre, vagy nyomja le a <kbd>CTRL</kbd>+<kbd>J</kbd>billentyűt.

## <a name="add-on-tools"></a>Kiegészítő eszközök

> A PowerShell 3,0-ben hozzáadva

A Windows PowerShell integrált parancsprogram-kezelési környezet mostantól támogatja a kiegészítő eszközöket az objektummodell használatával. Ezek a bővítmények Windows megjelenítési alaprendszer (WPF) vezérlők, amelyek függőleges vagy vízszintes ablaktáblában jelennek meg a konzolon. Egy panelen több kiegészítő eszköz jelenik meg Többlapos vezérlőelemként. A nem Microsoft felek által készített kiegészítő eszközöket is hozzáadhat vagy eltávolíthat. További információkért tekintse meg a [Windows PowerShell integrált parancsprogram-kezelési környezet parancsfájl-objektummodell célját](../components/ise/object-model/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md).

**Milyen értéket vesz fel ez a változás?**

A bővítmények lehetővé teszik a Windows PowerShell integrált parancsprogram-kezelési környezet bővítését és testreszabását olyan eszközökkel, amelyek funkciókkal bővítik és javítják a parancsfájl-kezelési élményt.

**Mi működik másképp?**

A Windows PowerShell integrált parancsprogram-kezelési környezet 3,0-es és újabb verzióiban az Add-on **parancs** szerepel. A **parancsok** bővítmény lehetővé teszi a parancsmagok tallózását, és a parancsmagokkal kapcsolatos súgó elérését a **parancsfájl** és a **konzol** ablaktáblán.

További bővítmények a **bővítmények** menüjének a kiegészítő **eszközök webhely megnyitása** parancsával érhetők el.

## <a name="restart-manager-and-auto-save"></a>Újraindítás-kezelő és automatikus mentés

> A PowerShell 3,0-ben hozzáadva

Windows PowerShell integrált parancsprogram-kezelési környezet mostantól két percenként automatikusan menti a megnyitott parancsfájlokat egy külön helyen. Ha a Windows PowerShell integrált parancsprogram-kezelési környezet váratlan összeomlás vagy újraindítás után újraindul, akkor a a legutóbbi munkamenetben megnyitott parancsfájlokat is helyreállítja, még akkor is, ha a parancsfájlok nem lettek mentve.

Az automatikus mentési időköz módosításához futtassa a következő parancsot a konzol ablaktáblán: `$psise.Options.AutoSaveMinuteInterval`.

**Milyen értéket vesz fel ez a változás?**

Mostantól Windows PowerShell integrált parancsprogram-kezelési környezet tudja, hogy a megnyitott parancsfájlok automatikusan mentve lesznek.

**Mi működik másképp?**

Windows PowerShell integrált parancsprogram-kezelési környezet 2,0 nem menti automatikusan a parancsfájlokat.

## <a name="most-recently-used-list"></a>Legutóbb használt lista

> A PowerShell 3,0-ben hozzáadva

Windows PowerShell integrált parancsprogram-kezelési környezet mostantól a fájlok legutóbb használt listája szerepel. Amikor megnyit egy fájlt a Windows PowerShell integrált parancsprogram-kezelési környezetban, a fájl hozzá lesz adva a **fájl** menü legutóbb használt listájához.

A legutóbb használt listán szereplő fájlok alapértelmezett számának módosításához futtassa a következő parancsot a konzol ablaktáblán: `$psise.Options.MruCount`.

**Milyen értéket vesz fel ez a változás?**

Mostantól a leggyakrabban használt lista használatával könnyedén hozzáférhet a gyakran használt fájlokhoz.

**Mi működik másképp?**

Windows PowerShell integrált parancsprogram-kezelési környezet 2,0 nem rendelkezik legutóbb használt listával.

## <a name="console-pane"></a>Konzol ablaktábla

> A PowerShell 3,0-ben hozzáadva

A Windows PowerShell integrált parancsprogram-kezelési környezet első kiadásában elérhető külön parancs-és kimeneti ablaktábla egyetlen konzol ablaktáblába lett egyesítve. A konzol ablaktábla hasonló a függvényhez és a megjelenéshez egy tipikus Windows PowerShell-konzolon, de a következő fejlesztéseket tartalmazza:

- A bemeneti szöveg (nem kimeneti szöveg) szintaxisának színezése, beleértve az XML-szintaxist is
- IntelliSense
- Zárójel egyeztetése
- Hiba jelzése
- Teljes Unicode-támogatás
- Az <kbd>F1</kbd> környezetfüggő súgója
- <kbd></kbd>CTRL+<kbd>F1</kbd> Context-szenzitív show-parancs
- Összetett parancsfájl és jobbról balra író támogatás
- Betűkészlet-támogatás
- Nagyítás
- Vonal kiválasztása és letiltása – válasszon üzemmódot
- A beírt tartalom megőrzése a parancssorban, amikor megnyomja a <kbd>felfelé mutató nyilat</kbd> a konzolon megjelenő előzmények megtekintéséhez

**Milyen értéket vesz fel ez a változás?**

A konzol ablaktáblájának módosításai mellett a konzol felületének konzisztens programozási élménye is elérhető.

**Mi működik másképp?**

A Windows PowerShell integrált parancsprogram-kezelési környezet 2,0 külön parancs-és kimeneti ablaktáblával rendelkezik.

## <a name="command-line-switches"></a>Parancssori kapcsolók

> A PowerShell 3,0-ben hozzáadva

Ha a parancssorból indítja a Windows PowerShell integrált parancsprogram-kezelési környezett (a **powershell_ise. exe**beírásával), a következő új parancssori kapcsolók adhatók hozzá.

- `-NoProfile`: Windows PowerShell integrált parancsprogram-kezelési környezet futtatása nélkül elindul`$profile`
- `-Help`: Súgóablak megjelenítése
- `-mta`: A Windows PowerShell integrált parancsprogram-kezelési környezet elindítása többszálú lakás módban. Windows PowerShell integrált parancsprogram-kezelési környezet alapértelmezett működési módja az egyszálas apartman mód vagy `-sta`a.

**Milyen értéket vesz fel ez a változás?**

Ezen parancssori kapcsolók hozzáadásával szabályozhatja azt a környezetet, amelyben a Windows PowerShell integrált parancsprogram-kezelési környezet fut.

**Mi működik másképp?**

Windows PowerShell integrált parancsprogram-kezelési környezet 2,0 nem ismeri fel ezeket a parancssori kapcsolókat.

## <a name="new-editor-features"></a>Új szerkesztői funkciók

> A PowerShell 3,0-ben hozzáadva

Más Windows PowerShell integrált parancsprogram-kezelési környezet szerkesztési funkciói a következők:

- Az **XML-szintaxis színezése** – Windows PowerShell integrált parancsprogram-kezelési környezet a színek XML-szintaxisa ugyanúgy, mint a Windows PowerShell-szintaxis.
- A **kapcsos zárójelek** – Windows PowerShell integrált parancsprogram-kezelési környezet kapcsos zárójeleket és kiemeléseket tartalmaz, és a következő módokon használhatók: (például az **Ugrás egyezési** paranccsal vagy a <kbd>CTRL billentyűvel</kbd>+<kbd>)</kbd> a záró kapcsos zárójelek megkeresése, ha nyitó zárójel van kiválasztva).
- **Vázlat nézet** A parancsfájl panel támogatja a kibontást, amely lehetővé teszi a kódok összecsukását vagy kibővítését a bal oldali margón a plusz vagy a mínusz jelre kattintva. Használhat kapcsos zárójeleket, illetve a `#region` és `#endregion` címkéket is egy összecsukható szakasz elejének vagy végének megjelöléséhez. Az összes régió kibontásához vagy összecsukásához nyomja le a <kbd>CTRL</kbd>+<kbd>M</kbd>billentyűkombinációt.
- **A szöveg szerkesztésének húzása – a** Windows PowerShell integrált parancsprogram-kezelési környezet mostantól támogatja a szövegszerkesztés húzását. Bármelyik szövegrészt kiválaszthatja, és a szövegszerkesztőben vagy a konzolon áthelyezheti a szöveget egy másik helyre. Ha lenyomva tartja a <kbd>CTRL</kbd> billentyűt a kijelölt szöveg húzása közben, az egérgomb felengedésekor a rendszer az új helyre másolja a szöveget. Windows PowerShell integrált parancsprogram-kezelési környezet jelen verziójában a fájlok Windows PowerShell integrált parancsprogram-kezelési környezetre húzásakor Windows PowerShell integrált parancsprogram-kezelési környezet megnyitja a fájlt.
- **Elemzési hiba megjelenítése** – az elemzési hibák piros aláhúzással vannak jelezve. Ha egy jelzett hiba fölé viszi a mutatót, az elemleírás szövege megjeleníti a kódban talált problémát.
- **Nagyítás** – a konzol tartalmának nagyítási aránya a nagyítás csúszkával állítható be (a Windows PowerShell integrált parancsprogram-kezelési környezet ablak jobb alsó sarkában), vagy a konzol ablaktáblán a parancs `$psise.options.Zoom` megadásával.
- **Rich Text másolás és beillesztés** – a vágólapra másolása Windows PowerShell integrált parancsprogram-kezelési környezet megőrzi az eredeti kijelölés betűtípusát, méretét és színét.
- **Kijelölés tiltása** – kijelölhet egy szövegrészt úgy, hogy lenyomja az <kbd>ALT</kbd> billentyűt, miközben kiválasztja a szöveget a szkript ablaktáblán az egérrel, vagy az <kbd>ALT</kbd>+<kbd>SHIFT</kbd>+<kbd>billentyű lenyomásával.</kbd>

**Milyen értéket vesz fel ez a változás?**

A további szerkesztési funkciók konzisztens és hatékony szerkesztési környezetet biztosítanak.

**Mi működik másképp?**

Ezek a szerkesztési fejlesztések nem voltak jelen a Windows PowerShell integrált parancsprogram-kezelési környezet 2,0-ben.

## <a name="new-help-viewer-window"></a>Új Súgó megjelenítői ablak

> A PowerShell 3,0-ben hozzáadva

Ha lenyomja az <kbd>F1</kbd> billentyűt, amikor a kurzor egy parancsmagban van, vagy ha egy kijelölt parancsmag része, az új Súgó megjelenítő környezetfüggő súgót nyit meg a Kiemelt parancsmaggal kapcsolatban. A **Súgó Windows** PowerShell megjelenítéséhez írja be `operators` a konzolt a konzol ablaktáblán, majd nyomja le az <kbd>F1</kbd>billentyűt.

A szolgáltatás használata előtt töltse le a Windows PowerShell súgójának legújabb verzióját a Microsoft webhelyén. A súgótémakörök letöltésének legegyszerűbb módja, ha a Windows PowerShell integrált parancsprogram-kezelési környezet rendszergazdaként `Update-Help` való futtatásakor a konzol ablaktábláján futtatja a parancsmagot.

Megváltoztathatja az <kbd>F1</kbd> -es kulcs súgóját. Az **eszközök**/**beállításai** menü **általános beállítások** lapján a **többi beállítás**alatt beállíthatja vagy törölheti a jelölőnégyzetet a **helyi súgótartalom használata online tartalom helyett**. Ha be van jelölve, a-ügyfél a modul mappában található letöltött súgóban megkeresi a parancsmag súgóját. Ha a jelölőnégyzet nincs bejelölve, az ügyfél az online súgót keresi.

**Milyen értéket vesz fel ez a változás?**

Környezetfüggő súgó a jelenlegi parancsmag vagy parancsfájl elhagyása nélkül integrált tanulási élményt biztosít.

**Mi működik másképp?**

Windows PowerShell integrált parancsprogram-kezelési környezet korábbi verzióiban az <kbd>F1</kbd> billentyű lenyomásával megnyitotta a súgófájl a helyi számítógépen. A Windows PowerShell integrált parancsprogram-kezelési környezet 3,0-es és újabb verzióiban megnyílik egy ablak, amely tartalmazza a kereshető és konfigurálható parancsmag súgóját. Ez a Windows PowerShell 3,0 újdonsága a Windows PowerShell integrált parancsprogram-kezelési környezet 3,0 és a frissíthető Súgó.

## <a name="show-command-cmdlet"></a>Parancssori parancsmag megjelenítése

> A PowerShell 3,0-ben hozzáadva

A `Show-Command` parancsmag lehetővé teszi a parancsmagok vagy függvények összeállítását és futtatását grafikus űrlapok kitöltésével. Az űrlap lehetővé teszi, hogy a felhasználók grafikus környezetben működjenek a Windows PowerShell használatával.
`Show-Command`a speciális parancsfájlokat is lehetővé tesz a gyors Windows PowerShell-alapú grafikus felhasználói felület létrehozásához.

**Milyen értéket vesz fel ez a változás?**

A használatával `Show-Command` a Windows PowerShell-parancsfájlok segítségével megadhatja a felhasználók számára, hogy milyen grafikus környezettel rendelkeznek. `Show-Command`a a bevezető felhasználók számára is segítséget nyújt a Windows PowerShell megismerésében.

**Mi működik másképp?**

`Show-Command`új Windows PowerShell integrált parancsprogram-kezelési környezet 3,0.

## <a name="see-also"></a>Lásd még:

További információ a Windows PowerShell integrált parancsprogram-kezelési környezet használatáról: [a Windows PowerShell integrált parancsfájlkezelési környezetének feltárása](../getting-started/fundamental/exploring-the-windows-powershell-ise.md).
