---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell szószedet"
ms.assetid: b0f88cbe-cb83-4912-a301-184534cb35c7
ms.openlocfilehash: 48e5d832ead720c8bc7753c94f757ddb21846fc9
ms.sourcegitcommit: ced46469e064736eeb1f5608abbc792ec69bdc92
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/08/2017
---
# <a name="windows-powershell-glossary"></a>A Windows PowerShell szószedet


|Kifejezés|Meghatározás|
|--------|--------------|
|bináris modul|Windows PowerShell modul, amelynek gyökérmodult egy olyan bináris modul fájl (.dll). A bináris modulok is, illetve nem tartalmazhatnak egy moduljegyzék.|
|általános paraméter|A Windows PowerShell-motor minden parancsmagok, speciális függvények és munkafolyamatok hozzáadott paraméter.|
|ponttal kezdődő forrás|A Windows PowerShell parancssorába írja be a önmagában egy pontot és egy helyet, a parancs előtt egy parancs indítását. Parancsok, amelyek forrása pont futtassa az új hatókör ahelyett, hogy az aktuális hatókörben. Bármely változók, aliasok, Funkciók, vagy meghajtók parancs létrehozó jönnek létre az aktuális hatókörben és érhetők el a felhasználók számára, ha a parancs végrehajtása után.|
|dinamikus modul|Ez a modul létezik csak a memória. A New-modul és a Import-PSSession parancsmagok a dinamikus modulok létrehozása.|
|dinamikus paraméterek|Egy paraméter, amely egy Windows PowerShell-parancsmag, függvény vagy parancsfájl bizonyos körülmények között szerepel. Parancsmagok, függvények, szolgáltatókat és parancsfájlok dinamikus paraméterek adhat hozzá.|
|fájl formázása|A Windows PowerShell XML-fájl, amely a. format.ps1xml bővítményt, és határozza meg, hogyan jeleníti meg a Windows PowerShell egy objektumot, a .NET-keretrendszer típusa alapján.|
|globális munkamenet-állapot|A munkamenet-állapot, amely tartalmazza az adatokat, amely hozzáférhető annak a felhasználónak egy Windows PowerShell-munkamenetben.|
|állomás|A felület a Windows PowerShell motor által, a felhasználó folytatott kommunikációhoz. Például az állomás kérések kezelésének módja Windows PowerShell és a felhasználó között.|
|gazdagép-alkalmazás|A program, amely a Windows PowerShell-motor betölti a feldolgozás és a műveletek végrehajtásához használja.|
|a bemeneti feldolgozási mód|Bemeneti kap egy, a parancsmag segítségével a rekordok feldolgozásához metódust. A bemeneti feldolgozási módszerek közé tartozik a BeginProcessing metódus, a ProcessRecord, a EndProcessing metódust, és a StopProcessing módszer.|
|manifest modul|A Windows PowerShell-modult, amely rendelkezik a jegyzék, amelynek ModulesToProcess kulcs értéke üres.|
|moduljegyzék|A Windows PowerShell adatfájlt (.psd1), amely leírja, hogy a modul tartalmának és, amely meghatározza, hogy a modul feldolgozásának módja.|
|a munkamenet-állapot modul|A munkamenet-állapot, amely tartalmazza a nyilvános és titkos adatokat a Windows PowerShell-modulok. A személyes adatokat a a munkamenet-állapot nem érhető el egy Windows PowerShell-munkamenet a felhasználó számára.|
|nem okozó hibát|Hiba, amely nem áll le a Windows PowerShell folyamatos a parancs végrehajtásához.|
|főnév|A word, amelyeket a kötőjel egy Windows PowerShell-parancsmag neve követ. A főnév ismerteti az erőforrásokat, amelyre a parancsmag működik.|
|A paraméterhalmaz|Egy csoport, amely ugyanezt a parancsot egy adott művelet végrehajtására használható paraméterek.|
|Az adatcsatorna|A Windows PowerShellben, az előző parancs küldése a következő parancsot az adatcsatorna számára.|
|Adatcsatorna|Parancsokat csővezeték operátorral egymáshoz csatolt (&#124;) csatlakoztatva (ASCII 124). Minden egyes csővezeték-kezelőt az előző parancs küldése a következő parancs számára.|
|PSSession|Egy Windows PowerShell-munkamenetben létrehozott, felügyelt, és a felhasználó által lezárt típusú.|
|legfelső szintű modul|Egy moduljegyzék ModuleToProcess kulcsában a megadott modul.|
|Futási térben|A Windows PowerShell, a működési környezetben, amelyben a folyamat minden parancs végrehajtása.|
|parancsprogram-blokkot tartalmazzon|A Windows PowerShell programozási nyelv, utasítások vagy egyetlen egységként használható kifejezések gyűjteménye. Parancsprogram-blokkot tartalmazzon argumentumokat fogadják el, és visszatérési értékek.|
|parancsfájl-modul|Egy Windows PowerShell modul, amelynek gyökérmodult modul parancsfájl (.psm1). Előfordulhat, hogy egy szkriptmodulba, vagy nem tartalmazhatnak egy moduljegyzék.|
|parancsfájl-modul|Egy Windows PowerShell-parancsfájlt tartalmazó fájl. A parancsfájl, amely a parancsfájl modul exportálja tagokat definiálja. Modul parancsprogramok a .psm1 fájlnévkiterjesztéssel rendelkeznek.|
|rendszerhéj|A parancsértelmező használt parancsok átadása az operációs rendszer.|
|kapcsolóparaméter|Egy paraméter, amely nem alkalmaz argumentumot.|
|lezáró hibát|Hiba a parancs feldolgozása a Windows PowerShell leáll.|
|Tranzakció|Egy atomi munkaegysége. A munkahelyi tranzakción belül el kell végezni egészére; Ha valamely része a tranzakció sikertelen, a teljes tranzakció sikertelen.|
|típusú fájl|Egy Windows PowerShell XML-fájl, amely .ps1xml kiterjesztése, és, amely kiterjeszti a Microsoft .NET-keretrendszer típusok a Windows PowerShell tulajdonságait.|
|Művelet|A word, amely megelőzi a kötőjel egy Windows PowerShell-parancsmag neve. A művelet a végrehajtandó műveletet a parancsmaggal ismerteti.|
|Windows PowerShell|Egy parancssori rendszerhéj és feladatalapú parancsprogramozási technológiát, amely az informatikai rendszergazdák teljes körű vezérlését és automatizálás rendszer azokat a felügyeleti feladatokat.|
|A Windows PowerShell-paranccsal|Egy folyamat elemei, amelyek olyan műveleteket kell elvégezni. A Windows PowerShell-parancsok adta-e a billentyűzet, vagy programozott módon meghívni.|
|A Windows PowerShell-adatfájlt|Egy szövegfájlt, amely a .psd1 fájlnévkiterjesztéssel rendelkezik. A Windows PowerShell modul jegyzék adattárolás és tárolja a lefordított karakterláncokat parancsfájl nemzetközivé tétel például különböző célú adatok fájlokat használja.|
|A Windows PowerShell-meghajtó|A virtuális meghajtókat, amely a tárolóban közvetlen hozzáférést biztosít. Azt határozza meg a Windows PowerShell-szolgáltató vagy létrehozása a parancssorból. A parancssorból létre munkamenet-specifikus meghajtók és elvesznek, ha a munkamenet lezárult.|
|Windows PowerShell integrált parancsfájlkezelési környezet (ISE)|Egy Windows PowerShell gazdagép-alkalmazás, amely lehetővé teszi, hogy parancsokat és írási, tesztelése és hibakeresése parancsfájlok rövid, a szintaxis színű Unicode-kompatibilis környezetben.|
|A Windows PowerShell-modul|Önálló újrafelhasználható egysége, amely lehetővé teszi, hogy a partíció, rendezése és a Windows PowerShell-kódjába absztrakt. A modul parancsmagok, szolgáltatók, Funkciók, változók és más erőforrások, amelyek egyetlen egységként importálhatók típusú tartalmazhat.|
|Windows PowerShell-szolgáltató|A Microsoft .NET-keretrendszer-alapú program az adatok egy speciális adattár elérhetővé teszi a Windows PowerShellben, hogy megtekintheti és kezelheti azt.|
|A Windows PowerShell-parancsfájl|Egy parancsfájl, amely a Windows PowerShell nyelven.|
|A Windows PowerShell-parancsfájl|A .ps1 kiterjesztéssel rendelkező és a Windows PowerShell nyelven írt parancsfájlt tartalmazó fájl.|
|A Windows PowerShell beépülő modul|Meghatározza a parancsmagok, a szolgáltatók és a Microsoft .NET-keretrendszer típusok a Windows PowerShell környezethez adható hozzá egy készletét erőforrás.|
|A Windows PowerShell munkafolyamat|A munkafolyamat olyan programozott, összekapcsolódó lépések sora, amik hosszan futó feladatokat végeznek el vagy több eszközön vagy felügyelt csomóponton keresztül végrehajtandó, több lépés koordinációját igénylik. A Windows PowerShell munkafolyamat lehetővé teszi, hogy az informatikai szakemberek és fejlesztők hozhatnak létre Többeszközös felügyeleti tevékenységek, vagy egy munkafolyamaton belül egyetlen feladatok munkafolyamatként. A Windows PowerShell munkafolyamat lehetővé teszi a igazítja, és futtassa a Windows PowerShell-parancsfájlok és a XAML-fájlokkal munkafolyamatként.|

