---
title: Windows PowerShell programozói&#39;s útmutató |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows PowerShell Programmer's Guide
ms.assetid: f3aaf667-af84-4ea8-a5ad-d454d0d700b8
caps.latest.revision: 9
ms.openlocfilehash: 75425fbd38141fc82dd834835912c357ecfa6d2b
ms.sourcegitcommit: 0ca836d1044e46d3a7dcbc69fa93d84f74848559
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/04/2019
ms.locfileid: "58920390"
---
# <a name="windows-powershell-programmer39s-guide"></a>Windows PowerShell programozói&#39;s útmutató

A programozói útmutató célja fejlesztőknek szól, akik egy parancssori felügyeleti környezet biztosítása a rendszergazdák iránt. Windows PowerShell tegye elérhetővé a .NET-objektumokat, miközben lehetővé teszi a Windows PowerShell-lel Ön helyett ezt a munkát a legtöbb felügyeleti parancsok hozhat létre egy egyszerű lehetőséget biztosít.

A parancs a hagyományos fejlesztési kell írni az egyik paraméter elemző, egy paraméter binder, szűrők és minden más funkciója, minden parancs által elérhetővé tett. Windows PowerShell-parancsok írásával, megkönnyíti a következő tartalmazza:

- Egy hatékony Windows PowerShell modul (végrehajtóprogramja) a saját elemzési és a egy mechanizmust automatikusan kötési parancs paraméterei.

- Segédprogramok formázására és megjelenítése a parancs eredménye egy parancssor-értelmező (CLI) használatával.

- Támogatja a magas teljesítményszintet is (a Windows PowerShell-szolgáltatók) funkcióit, amelyek megkönnyítik a tárolt adatok elérésére.

  Kis költséggel a .NET-objektumokat gazdag parancsot vagy be, amely egy teljes körű parancssori felület felajánlja, hogy a rendszergazda által megfelelhet.

  Ez a szakasz ismerteti az alapfogalmakat Windows PowerShell és a feltételek. Ismerkedjen meg ezekkel a fogalmakkal és használati fejlesztés megkezdése előtt.

## <a name="about-windows-powershell"></a>A Windows PowerShell névjegye

Windows PowerShell parancsokat, amelyekkel számos különböző típusú fejlesztési határozza meg. Ezek a parancsok a következők: funkciók, a szűrők, a parancsfájlok, az aliasok és a végrehajtható fájlok (alkalmazások). A jelen útmutatóban tárgyalt fő parancstípus "parancsmag" nevű egyszerű, kis parancs. Windows PowerShell parancsmagok egy halmaza bizonyítékot szolgáltat, és teljes mértékben támogatja a környezethez illeszkedve kell parancsmag testreszabása. A Windows PowerShell-modul összes típusú dolgozza fel, ugyanúgy, ahogy parancsmagot folyamatok használatával.

Parancsok mellett Windows PowerShell támogatja az elérhető adott csoportok parancsmagokat, amelyek különféle testre szabható Windows PowerShell szolgáltatókat. A rendszerhéj a Windows PowerShell által biztosított gazdaalkalmazást (Windows PowerShell.exe) belül működik, de egyéni gazdagép-alkalmazás, amely az adott igényeknek is fejleszthet egyaránt elérhető. További információkért lásd: [Windows PowerShell működése](http://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58).

### <a name="windows-powershell-cmdlets"></a>Windows PowerShell-parancsmagok

A parancsmag a Windows PowerShell környezetben használt egyszerűsített parancs. A Windows PowerShell-modult meghívja ezeket a parancsmagokat a parancssorban biztosított automatizálási szkriptek környezetében, és a Windows PowerShell-modul is meghívja őket programozott módon Windows PowerShell API-kon keresztül.

-Parancsmagokkal kapcsolatos további információkért lásd: [írása egy Windows PowerShell-parancsmag](../cmdlet/writing-a-windows-powershell-cmdlet.md).

### <a name="windows-powershell-providers"></a>Windows PowerShell-szolgáltatók

A rendszergazdai feladatok, a felhasználó szükségessé (például a fájlrendszer, a Windows beállításjegyzék vagy egy tanúsítványtároló) adattárban tárolt adatok vizsgálata. Ezek a műveletek megkönnyítése érdekében a Windows PowerShell egy Windows PowerShell-szolgáltatóban, amely egy adott adattár, például a Windows beállításjegyzék eléréséhez használható nevű modult definiálja. Minden szolgáltató kapcsolódó parancsmagok a felhasználónak egy szimmetrikus megtekintése a tárolóban lévő adatok egy készletét támogatja.

Windows PowerShell a Windows PowerShell-szolgáltató több alapértelmezett biztosít. Például a beállításjegyzék-szolgáltatója támogatja a navigációs és a Windows beállításjegyzék kezelését végzi. Beállításkulcsok elemek helyettesítik, és a beállításkulcs-értékeket számít tulajdonságait.

Ha egy adattár, amelyeket a felhasználónak el kell elérhetővé teszi, szükség lehet a saját Windows PowerShell-szolgáltató írása leírtak szerint [létrehozása Windows PowerShell-szolgáltatók](./how-to-create-a-windows-powershell-provider.md). További információk aboutWindows PowerShell-szolgáltatók, lásd: [Windows PowerShell működése](http://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58).

### <a name="host-application"></a>Gazdagép-alkalmazás

Windows PowerShell az alapértelmezett gazdagép alkalmazás powershell.exe, amely egy konzolalkalmazást, amely a felhasználó kommunikál, és a Windows PowerShell modul használatával a konzolablakban gazdagépeket tartalmaz.

Csak ritkán lesz kell írnia a Windows PowerShell környezethez, a saját gazdaalkalmazást testreszabási támogatják. Egyetlen esetet tartalmaz, amelyekben szüksége lehet a saját alkalmazás akkor, ha rendelkezik egy grafikus felhasználói felület, amely gazdagabb, mint az alapértelmezett gazdagép-alkalmazás által biztosított csatoló előfeltétele. Is érdemes egy egyéni alkalmazást, ha a parancssorban a grafikus felhasználói Felülettel készül. További információkért lásd: [hogyan hozhat létre egy Windows PowerShell gazdaalkalmazást](http://msdn.microsoft.com/en-us/d31355c9-a270-4b09-8f0c-35a7392a7d07).

### <a name="windows-powershell-runtime"></a>Windows PowerShell-modul

A Windows PowerShell-modul az a-végrehajtó motor, amely megvalósítja a parancs feldolgozása. Ez magában foglalja az osztályokat, amelyek a gazdagép-alkalmazás és a Windows PowerShell-parancsokat és szolgáltatók közötti illesztőfelületet biztosítanak. A Windows PowerShell-modul van, a üzemeltetési környezet, amelyben a rendszerhéjat, és a parancsok végrehajtása aktuális Windows PowerShell-munkamenet a futási térben objektum van megvalósítva. Működési részletekért lásd: [Windows PowerShell működése](http://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58).

### <a name="windows-powershell-language"></a>Windows PowerShell nyelv

A Windows PowerShell nyelvi parancsfájl-kezelési funkciók és mechanizmusokat megalkotni, hívhat meg parancsokat biztosít. Teljes körű parancsfájl-kezelési információkért lásd: a Windows PowerShell nyelv leírása tartalmazza a szükséges a Windows PowerShell-lel.

### <a name="extended-type-system-ets"></a>Kiterjesztett típus System (ETS)

Windows PowerShell számos különböző objektumok, például a .NET és az XML-objektumok hozzáférést biztosít. Ennek következményeképpen minden objektum esetében egy közös absztrakciós nyújtjuk a rendszerhéj a kiterjesztett típus rendszert (ETS) használja. A legtöbb ETS funkció a felhasználó számára, de a parancsfájl vagy a .NET-fejlesztői használja, a következő célokra:

- Megtekintés – meghatározott objektumokat tagjai egy részét. Egy adott objektum számos különböző "igazítani" áttekintést nyújt a Windows PowerShell.

- Tagok felvétele a meglévő objektumok.

- Való hozzáférés szerializált objektumokat.

- Írás egyéni objektumokat.

  Használatával ETS, hozhat létre rugalmas új "típusú", amely kompatibilis a Windows PowerShell nyelv. Ha .NET-fejlesztők, le is tudja meghatározni, ha egy objektum kiértékelése, objektumok segítségével azonos, a Windows PowerShell nyelv vonatkozik, a parancsprogramok, például `true`.

  ETS, és hogyan használja a Windows PowerShell az objektumok kapcsolatos további információkért lásd: [Windows PowerShell objektum fogalmak](http://msdn.microsoft.com/en-us/12700631-be23-4e6b-9bf0-81ea0d166353).

## <a name="programming-for-windows-powershell"></a>Windows PowerShell-alapú programozása

Windows PowerShell parancsok, a szolgáltatók és más program modulok, a .NET-keretrendszer használatával a kód határozza meg. Meg nem korlátozódnak Microsoft Visual Studio használata egyéni modulok létrehozásához Windows PowerShell, bár a jelen útmutatóban ismertetett minták ismert, hogy az eszköz futtatásához. Használhat bármely osztályöröklődés és attribútumok használatát támogató .NET programozási nyelvvel. Bizonyos esetekben a Windows PowerShell API-k obecné typy hozzáférhet programozási nyelv szükséges.

## <a name="programmers-reference"></a>Programozói dokumentáció

Ha a Windows PowerShell környezethez fejlesztése során, olvassa el a [Windows PowerShell SDK](../windows-powershell-reference.md).

## <a name="getting-started-using-windows-powershell"></a>Ismerkedés a Windows PowerShell-lel

A Windows PowerShell-rendszerhéj használata indításával kapcsolatos további információkért lásd: a [első lépések a Windows PowerShell-lel](/powershell/scripting/getting-started/getting-started-with-windows-powershell) kiszállított Windows PowerShell használatával. Egy rövid összefoglaló háromrészes dokumentumot is csakúgy, mint a parancsmag használata-nek.

## <a name="contents-of-this-guide"></a>Ez az útmutató tartalma

|Témakör|Meghatározás|
|-----------|----------------|
|[Windows PowerShell-szolgáltató létrehozása](./how-to-create-a-windows-powershell-provider.md)|Ez a szakasz ismerteti, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, a Windows PowerShell környezethez.|
|[A Windows PowerShell-gazdagépet alkalmazás létrehozása](http://msdn.microsoft.com/en-us/d31355c9-a270-4b09-8f0c-35a7392a7d07)|Ez a szakasz ismerteti, hogyan írhat egy fogadó alkalmazás, amely kezeli a futási térben és a egy fogadó alkalmazás, amely megvalósítja a saját egyéni gazdagép írásával.|
|[Windows PowerShelles beépülő modul létrehozása](../cmdlet/how-to-create-a-windows-powershell-snap-in.md)|Ez a szakasz ismerteti, hogyan hozhat létre beépülő modul szerelvények regisztrálható az összes parancsmagok és szolgáltatók és a egy egyéni beépülő modul létrehozása.|
|[Konzolfelület létrehozása](./how-to-create-a-console-shell.md)|Ez a szakasz ismerteti, hogyan hozhat létre egy konzol rendszerhéj, amely nem bővíthető.|
|[Windows PowerShell – Fogalmak](./windows-powershell-concepts.md)|Ez a szakasz tartalmazza a elméleti információk segítségével megismerheti a Windows PowerShell a fejlesztők szempontjából.|

## <a name="see-also"></a>Lásd még:

[Windows PowerShell SDK](../windows-powershell-reference.md)
