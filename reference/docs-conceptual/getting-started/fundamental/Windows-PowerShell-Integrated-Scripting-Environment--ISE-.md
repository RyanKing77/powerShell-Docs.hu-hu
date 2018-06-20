---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A Windows PowerShell integrált parancsfájlkezelési környezet ISE
ms.assetid: f156b92d-0203-46d2-89c7-b4989d32e3d2
ms.openlocfilehash: d116ec107c2d07e9fd55ee974008b3636b4ab049
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952069"
---
# <a name="windows-powershell-integrated-scripting-environment-ise"></a>Windows PowerShell integrált parancsfájlkezelési környezet (ISE)

A Windows PowerShell integrált parancsfájlkezelési környezet (ISE) a Windows PowerShell-motor és a nyelv két állomás egyike. Azt írni, futtatására és parancsfájlok tesztelése, melyek nem érhetők el a Windows PowerShell-konzolban. Az ISE ad-zintaxisszínek, kiegészítést, az IntelliSense, visual-Hibakeresés és környezetfüggő súgó.

A ISE lehetővé teszi, hogy a konzol ablaktáblában parancsok futtatását, de is támogatja, amelyek segítségével egyszerre forráskódját a parancsfájl és más, amely az ISE csatlakoztatható eszközök ablaktábla. Akkor is megnyithatja több parancsfájl a Windows egy időben, ami akkor hasznos, ha egy parancsfájl, amely más parancsfájlokat vagy modulok meghatározott funkciókat használja hibakeresés alatt.

## <a name="whats-new"></a>What’s New (Újdonságok)

Az alábbiakban néhány funkciója, amely a legutóbbi kiadásaiban PowerShell ISE lettek hozzáadva.

### <a name="added-in-powershell-30-windows-server-2012-windows-8"></a>Hozzáadva a PowerShell 3.0 (a Windows Server 2012, Windows 8)

**IntelliSense** automatikusan elvégzi a parancsok beíráskor menük egyező parancsmagok, paraméterek, paraméterértékeket, fájlok vagy mappák megjelenítésével.

**Kódtöredékek** , hogy könnyen szúrhat be a parancsfájlok a írási kód rövid szakaszok is vannak. A lista hasznos kódtöredékek gyűjteményét tartalmazza, és segítségével több a **New-részlet** parancsmag.

**Bővítmény eszközök** , adja hozzá az ISE szolgáltatások hozhat létre, amely együttműködik a kód írása [a Windows PowerShell ISE Scripting objektummodell](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md).

Ezek az eszközök vezérlők lapokra ablaktábla megjelenítése, vagy a háttérben láthatatlanul működik. A **parancsok** bővítmény jó példa és 3.0-s verzió megtalálható, és később, amely megjeleníti az elérhető parancsok és azok súgó listáját.

**Indítsa újra a Manager és az automatikus mentési** automatikusan menti a parancsfájlok két percenként összeomlási vagy váratlan újraindítása esetén munkája adatveszteség elkerülése végett.

**A legtöbb legutóbbi lista** tagja mostantól a fájl megnyitása menüből, hogy egyszerűbb legyen a leggyakrabban használt fájlok eléréséhez.

**Egyesített konzolpanelen**. A ISE korábbi verzióiban nem voltak különálló parancs és a kimeneti ablaktábla. Most egyesített egytáblás be, hogy több közvetlenül utánozza lásd a Windows Powershell-konzolban.

**Parancssori kapcsolók**. Számos új parancssori kapcsolókat ad az ISE működésének teljesebb körű vezérlése. -NoProfile elindítja az ISE profil parancsprogram futtatása nélkül. -Help megnyílik az ISE-a Súgó ablakot. -mta "többszálas apartman módban" ISE kezdődik. Az alapértelmezett érték a egyszálas.

**Új szerkesztő szolgáltatások** könnyebben létrehozásához, és olvassa el a kódot:

- **XML-zintaxisszínek**. Az ISE-szerkesztő, azt a Windows PowerShell-kód szintaxis színek most színek XML szintaxis azonos módon.

- **Megfelelő zárójel**. A ISEWindows PowerShell ISE kiemeli a segítségével ellenőrizze, hogy a záró zárójelnek a nyitó kereséséhez megfelelő számú egyező kell használni azokat. Használja a CTRL -\[ található a záró zárójel, amely megfelel a nyitó zárójel a kurzor alatti.

- **Vázlat nézetben**. Csukja össze, vagy a plusz és mínusz jelek a bal margón bontsa ki a szakaszokban a kódot. Így könnyebben megtalálhatja a kód egy hosszú parancsfájlban keres.

- **Áthúzása szöveg szerkesztése**. Jelöljön ki egy szöveget, majd húzza azt áthelyezése egy másik helyre. Ha meg a Ctrl billentyűt lenyomva tartva ahelyett, hogy másolja a kijelölt szöveg húzza át.

- **Elemzési hiba megjelenítési**. A Windows PowerShell a parancsfájl megvizsgálja, közben. Ha hibát észlel, a hibát okozó kód egy piros hullámos jeleníti meg. Ha a jelzett hiba mutat, a elemleírás jeleníti meg a problémát talált.

- **Nagyítás**. A szöveg könnyebb olvasni, vagy hogy áttekintő képet a csúszka használatával az ISE ablak jobb alsó sarkában lévő kicsinyítés nagyítás.

- **Rich text másolás és Beillesztés**. Ha másol az ISE a vágólapra, a betűtípus, mérete és a kijelölt szöveg színét információk része.

- **Kijelölés blokkolása**. Kiválaszthatja a szöveg blokk alakú adattömb szöveg kijelölése az egérrel panelbe közben az ALT billentyűt lenyomva tartja, vagy megnyomja **Alt + Shift + mutató nyílra**.

### <a name="added-in-powershell-20-windows-server-2008-r2-windows-7"></a>Hozzáadva a PowerShell 2.0-s (Windows Server 2008 R2, Windows 7)

A ISE a PowerShell 2.0-ban jelent.

## <a name="requirements-for-running-the-windows-powershell-ise"></a>A Windows PowerShell ISE futtatásának követelményei

Az ISE érhető el minden Windows rendszeren futtatható a Windows PowerShell 2.0-s vagy újabb verzió. Minden Windows és Windows Server verziója a Windows PowerShell és az ISE verzióját is tartalmazza, de frissítheti a legújabb elérhető a Windows Management Framework (WMF) telepítésével. Tekintse meg a [WMF](/powershell/wmf/readme) dokumentációjában talál további információt.

> [!NOTE]
> A Windows PowerShell ISE használatához a grafikus felhasználói felületen, a Windows Server Server Core esetén nem futtatható.

## <a name="see-also"></a>Lásd még:

[A windows a power shell ise objektummodell scripting célja](../../core-powershell/ise/Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)