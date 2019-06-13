---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Windows PowerShell integrált parancsfájl-kezelési környezet ISE
ms.openlocfilehash: 9bcb297a9e1990ede2cfff1e147aeda7cd69e873
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030552"
---
# <a name="windows-powershell-integrated-scripting-environment-ise"></a>Windows PowerShell integrált parancsfájl-kezelési környezet ISE

A Windows PowerShell integrált parancsfájl-kezelési környezet (ISE) a Windows PowerShell-motor és a nyelv két gazdagép egyike. Azt is írhat futtassa, és parancsfájlok tesztelése, hogy nem érhetők el a Windows PowerShell-konzolon. A ISE hozzáadja a szintaxis-színezést, kiegészítés, az IntelliSense, vizuális hibakeresési és környezetfüggő súgó.

A ISE lehetővé teszi, hogy a konzol ablaktáblában parancsok futtatása, de ablaktáblára van felosztva, segítségével egyszerre tekinthet meg a forráskódot a parancsfájl és egyéb eszközöket, amelyek segítségével csatlakoztassa az ISE-ben is támogatja. Akkor is megnyithatja több parancsfájl a Windows egy időben, ami akkor hasznos, ha egy parancsfájl, amely az egyéb parancsfájlokat vagy modulok meghatározott függvényeket használja hibakeresés.

## <a name="whats-new"></a>What’s New (Újdonságok)

Íme néhány lettek hozzáadva az ISE-ben a PowerShell legújabb verzióiban található funkciók.

### <a name="added-in-powershell-30-windows-server-2012-windows-8"></a>Új funkció a PowerShell 3.0 (a Windows Server 2012, Windows 8)

**Az IntelliSense** automatikusan elvégzi az egyező parancsmagok, paraméterek, paraméterértékeket, fájlok vagy mappák menük megjelenítésével beírása a parancsokat.

**A kódrészletek** kódot, hogy könnyen beilleszthet a parancsfájlok az írási rövid szakaszait is. Hasznos kódrészletek gyűjteménye szerepel a mezőben, és több használatával is a **New-kódrészlet** parancsmagot.

**Bővítmény eszközök** ír kódot, amellyel kommunikál hozhat létre az ISE funkciók hozzáadása, amely [a Windows PowerShell ISE parancsfájl-kezelési objektummodell](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md).

Ezek az eszközök gomb lapnézetben panelen beállítások megjelenítéséhez, vagy alapfeladatokat működik a háttérben is. A **parancsok** bővítmény jó példa, és 3.0-s verzió részét képezi, és később, amely megjeleníti az elérhető parancsok és a Súgó listáját.

**Indítsa újra a Manager és az automatikus mentés** automatikusan a parancsfájlok két percenként mentse a munkáját, egy összeomlási vagy váratlan újraindítás esetén adatvesztés elkerülése érdekében.

**A legtöbb a legutóbb használt lista** a fájl megnyitása menüben, hogy megkönnyítsék az eljutást a leggyakrabban használt fájlok tartoznak.

**Egyesített konzolpanelen**. A ISE korábbi verzióiban voltak külön parancsot és a kimeneti ablaktábla. Akkor most mostantól egyetlen, hogy több közvetlenül utánozza lásd a Windows PowerShell-konzolon.

**Parancssori kapcsolók**. Számos új parancssori kapcsolók jobban szabályozhatja az ISE működésének biztosítanak. -NoProfile profil parancsfájl futtatása nélkül indítja el az ISE-ben. -Súgó egy Súgó az ISE-ablakot nyit meg. -mta elindítja a "több szálon futó apartman módban" az ISE-ben. Az alapértelmezett érték az egyszálas.

**Új szerkesztő szolgáltatások** könnyebben hozhat létre, és olvassa el a kódot:

- **XML-szintaxis színezést**. A ISE-szerkesztő, azt a Windows PowerShell-kód szintaxis színek most színek syntaxe XML megegyező módon.

- **Kapcsos zárójel megfelelő**. A ISEWindows PowerShell ISE kiemeli a megfelelő zárójelek segítségével ellenőrizze, hogy a megfelelő számú záró zárójelnek megfelelően a nyitó megjelennek. Használja a CTRL -\[ a kapcsos zárójelet, amely megfelel a, amely a kurzort a nyitó zárójel található.

- **Vázlat nézetben**. Akkor is kibonthatja vagy összecsukhatja szakasza a kód a plusz és csökkentve a bal oldali margó bejelentkezik. Így könnyebb megtalálni a kód egy hosszú parancsfájlban keres.

- **Áthúzása szövegszerkesztés**. Jelöljön ki egy szöveget, és húzza át egy másik helyre. Ha Ön a Ctrl billentyűt lenyomva tartva húzza a kijelölt szöveg helyett másolja át.

- **Elemzési hiba megjelenített**. Windows PowerShell a parancsfájl megvizsgálja a beírás közben. Ha hibát észlel, a hibát okozó kód egy piros hullámos jeleníti meg. Ha az egérmutatót a jelzett hiba, a elemleírásokban bemutatja, a probléma, amely található.

- **Nagyítás**. Szabadon nagyíthatja könnyebb olvasni, vagy a nagyobb méretű kép megjelenítéséhez az ISE-ablak jobb alsó sarkában található csúszkával kicsinyítés a szöveg.

- **Rich text másolás és Beillesztés**. Amikor másol az ISE-ben a vágólapra, a betűtípus, méretét és színét információkat a kijelölt szöveg képezi.

- **Letiltja a kijelölés**. Szöveg kiválasztásakor az egérrel a parancsfájl panelen az ALT billentyűt lenyomva vagy billentyű lenyomásával kiválaszthatja egy blokk-alakú szövegrészletet, **Alt + Shift + nyíl**.

### <a name="added-in-powershell-20-windows-server-2008-r2-windows-7"></a>Új funkció a PowerShell 2.0-s (Windows Server 2008 R2, Windows 7)

Az ISE-ben a PowerShell 2.0-jelent meg.

## <a name="requirements-for-running-the-windows-powershell-ise"></a>A Windows PowerShell ISE futtatásának követelményei

Az ISE-ben elérhető bármely Windows-számítógépen futtatható a Windows PowerShell 2.0-s verziójú vagy újabb verzió. Windows és Windows Server minden verziója tartalmazza a Windows PowerShell és az ISE verzióját, de frissítheti a legújabb elérhető a Windows Management Framework (WMF) telepítésével. Tekintse meg a [WMF](/powershell/wmf) dokumentációjában talál további információt.

> [!NOTE]
> Grafikus felhasználói felületet igényel a Windows PowerShell ISE-ben, mert a Windows Server Server Core beállítást nem futtatható.

## <a name="see-also"></a>Lásd még:

[A windows power shell ise parancsfájl-kezelési objektummodelljének célja](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
