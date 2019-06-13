---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Windows PowerShell-szószedet
ms.openlocfilehash: 0827ec771b1744b87a8c0f0ddf48438f9ba484b2
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030359"
---
# <a name="windows-powershell-glossary"></a>Windows PowerShell-szószedet


|Kifejezés|Meghatározás|
|--------|--------------|
|bináris modul|A Windows PowerShell-modul amelynek gyökérmodult egy olyan bináris modul fájl (.dll). Egy bináris modul is, vagy egy moduljegyzék nem feltétlenül tartalmazzák.|
|általános paraméter|Egy paraméter, amely a Windows PowerShell motor által hozzáadott összes parancsmagok, a Speciális függvények és munkafolyamatok.|
|pont forrás|A Windows PowerShell indítása a parancs egy pont és a egy szóközt, mielőtt a parancs beírásával. Parancsok, amelyek pont forráskódú futtassa az új hatókör helyett az aktuális hatókörben. Minden olyan változók, aliasok, funkciók vagy meghajtókat, amely a parancs létrehoz jönnek létre az aktuális hatókörben és a parancs végrehajtása után a felhasználók számára elérhetők.|
|a dinamikus modul|Ez a modul létezik csak a memóriában. A New-modul és a Import-PSSession-parancsmagok a dinamikus modulok létrehozása.|
|dinamikus paraméterek|Ez a paraméter adnak hozzá egy Windows PowerShell-parancsmagot, függvény vagy parancsfájl bizonyos körülmények között. Parancsmagok, függvények, szolgáltatók és -parancsfájlok dinamikus paramétereket adhat hozzá.|
|fájl formázása|A Windows PowerShell XML-fájl, amely rendelkezik a. format.ps1xml bővítményt, és határozza meg, hogyan jeleníti meg a Windows PowerShell-objektumot a .NET-keretrendszer típusa alapján.|
|globális munkamenet-állapot|A munkamenet-állapot, amely tartalmazza az adatokat, amely hozzáférhető annak a felhasználónak egy Windows PowerShell-munkamenetet.|
|host|A felület, amely a Windows PowerShell motor segítségével a felhasználó kommunikál. Például az állomás kérések kezelésének módja Windows PowerShell és a felhasználó között.|
|gazdagép-alkalmazás|A program, amely betölti a Windows PowerShell-motor és a folyamatot, és használja a műveletek végrehajtásához.|
|a bemeneti metódus feldolgozása|Ez a módszer a parancsmag segítségével feldolgozásához bemenetként fogadott rekordokat. A bemeneti feldolgozási módszerek közé tartozik a BeginProcessing metódus, a ProcessRecord metódus, a EndProcessing módszer és a StopProcessing metódus.|
|a modul manifest|A Windows PowerShell-modul, amely rendelkezik egy jegyzéket, amelynek RootModule kulcs értéke üres.|
|moduljegyzék|Egy Windows PowerShell adatfájlt (.psd1), amely leírja, hogy a modul tartalmának és, amely szabályozza, hogy a modul feldolgozásának módja.|
|a modul munkamenet-állapot|A munkamenet-állapot, amely egy Windows PowerShell-modul nyilvános és titkos adatait tartalmazza. Egy Windows PowerShell-munkamenet a felhasználó személyes adatait a munkamenet-állapot nem érhető el.|
|megszakítást nem okozó hiba|Egy hiba, amely nem áll le a Windows PowerShell, a parancs feldolgozása továbbra is.|
|főnév|A kötőjel egy Windows PowerShell-parancsmag neve a következő szót. A főnév ismerteti az erőforrásokat, amelyen a parancsmag funkcionál.|
|Paraméterkészlet|Egy csoport, amely ugyanazt a parancsot egy adott művelet végrehajtására használható paraméterek.|
|függőleges vonal|A Windows PowerShell, az előző parancs eredményének küldése a következő parancsot a folyamat bemenetként.|
|Folyamat|Köti a csővezeték operátorral egymáshoz csatolt parancsokat (&#124;) (ASCII 124). Minden egyes csővezeték-kezelőt bemenetként a következő parancsot az előző parancs eredményének küld.|
|PSSession|Egy Windows PowerShell-munkamenetben létrehozott, felügyelt, és a felhasználó által lezárt típusú.|
|legfelső szintű modul|Egy moduljegyzék a RootModule kulcsot a megadott modul.|
|Futási térben|A Windows PowerShell, a üzemeltetési környezet, amelyben a folyamat minden parancs végrehajtásakor.|
|parancsprogram-blokkot|A Windows PowerShellben programozási nyelv, az utasítások vagy egyetlen egységként használt kifejezések gyűjteménye. Parancsprogram-blokkot fogadhat argumentumok és értéket ad vissza.|
|modul skriptu|A Windows PowerShell-modul amelynek gyökérmodult modul parancsfájl (.psm1). Előfordulhat, hogy egy szkriptmodulba, vagy egy moduljegyzék nem feltétlenül tartalmazzák.|
|parancsfájl-modul|Egy Windows PowerShell-parancsfájlt tartalmazó fájl. A parancsfájl, amely a modul skriptu exportálja tagokat definiálja. Parancsfájlok modul .psm1 fájlnévkiterjesztéssel rendelkezik.|
|Rendszerhéj|A parancsértelmezőt, amellyel parancsokat át az operációs rendszer.|
|új kapcsolóparaméter|Egy paraméter, amely nem vesz egy argumentum.|
|megszakítást okozó hiba|Egy hiba, amely leállítja a Windows PowerShell, a parancs feldolgozása.|
|Tranzakció|Egy atomi munkaegysége. A munka egy tranzakcióban kell végezni, teljes; Ha a tranzakció bármelyik részét nem sikerül, a teljes tranzakció sikertelen lesz.|
|a fájl típusa|A Windows PowerShell XML-fájl, amely .ps1xml kiterjesztése, és, amely kiterjeszti a Windows PowerShell a Microsoft .NET-keretrendszer típusok tulajdonságait.|
|művelet|A szó, amely megelőzi a kötőjel a egy Windows PowerShell-parancsmag neve. A művelet azt ismerteti, hogy a, a parancsmag által végrehajtandó műveletet.|
|Windows PowerShell|Egy parancssori rendszerhéj és feladatalapú parancsprogramozási technológiát, amely biztosítja az informatikai rendszergazdák teljes körű vezérlését és automatizálási rendszer felügyeleti feladatokat.|
|Windows PowerShell-paranccsal|Az elemek a folyamat, amely olyan műveleteket kell elvégezni. Windows PowerShell-parancsok vannak, vagy a billentyűzet begépelt vagy programozott módon meghívott.|
|Windows PowerShell-adatfájlt|Egy szöveges fájl, amely a .psd1 fájlnévkiterjesztéssel rendelkezik. Windows PowerShell modul jegyzékfájl adatok tárolására, és tárolja a lefordított sztringeket a parancsfájl nemzetközivé például különböző célú adatfájlok használ.|
|Windows PowerShell meghajtót|Egy virtuális meghajtó, amely egy adattár közvetlen hozzáférést biztosít. Ez egy Windows PowerShell-szolgáltató által definiált vagy létrehozása a parancssorból. A parancssorban létrehozott meghajtók a munkamenet-specifikus meghajtó, és elvesznek, ha a munkamenet lezárult.|
|Windows PowerShell integrált parancsfájl-kezelési környezet ISE|Amely lehetővé teszi, hogy a parancsok futtatását, valamint hogy írni, tesztelése és szkriptek hibakeresése egy barátságos és a szintaxis-színes, Unicode-kompatibilis környezetben a Windows PowerShell gazdaalkalmazást.|
|Windows PowerShell-modul|Önálló újrafelhasználható egység, amely lehetővé teszi, hogy a partíció, rendezése és a Windows PowerShell-kód absztrakt. Egy modul parancsmagok, a szolgáltatók, a Funkciók, a változók és a más típusú erőforrás, amelyet aztán egyetlen egységként is tartalmazhat.|
|Windows PowerShell-szolgáltató|A Microsoft .NET-keretrendszer-alapú program, amely egy speciális adattárban elérhetővé teszi a Windows PowerShellben, hogy megtekintheti és felügyelheti azokat.|
|Windows PowerShell-parancsfájl|A Windows PowerShell nyelven írt parancsprogram.|
|Windows PowerShell-parancsfájlt|Egy fájl, amely a .ps1 kiterjesztéssel rendelkezik, és egy parancsfájlt, amely a Windows PowerShell nyelven írt tartalmazza.|
|Windows PowerShell beépülő modul|Egy erőforrás, amely meghatározza a parancsmagok, a szolgáltatók és a Microsoft .NET-keretrendszer típusok a Windows PowerShell környezethez is hozzáadhatók.|
|Windows PowerShell-munkafolyamat|A munkafolyamat olyan programozott, összekapcsolódó lépések sora, amik hosszan futó feladatokat végeznek el vagy több eszközön vagy felügyelt csomóponton keresztül végrehajtandó, több lépés koordinációját igénylik. Windows PowerShell-munkafolyamat lehetővé teszi, hogy az informatikai szakemberek és fejlesztők Többeszközös felügyeleti tevékenységek és munkafolyamatként egy munkafolyamaton belül egyetlen feladatok sorozatát hozhat létre. Windows PowerShell-munkafolyamat lehetővé teszi alkalmazkodjon és munkafolyamatok futtatása Windows PowerShell-parancsprogramok és XAML-fájljait is.|
