---
title: A parancsmag – áttekintés |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cmdlets [PowerShell SDK]
- cmdlets [PowerShell SDK], described
ms.assetid: 0aa32589-4447-4ead-a5dd-a3be99113140
caps.latest.revision: 21
ms.openlocfilehash: a53b1ada46ad614af3522e6cc11e187afb76e7b1
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846332"
---
# <a name="cmdlet-overview"></a>Parancsmag – áttekintés

A parancsmag a Windows PowerShell környezetben használt egyszerűsített parancs. A Windows PowerShell-modult meghívja ezeket a parancsmagokat a parancssorban biztosított automatizálási szkriptek kontextusában. A Windows PowerShell-modul is elindítja azokat programozott módon Windows PowerShell API-kon keresztül.

## <a name="cmdlets"></a>Parancsmagok

Parancsmagok egy műveletet, és általában a Microsoft .NET-keretrendszer objektum térjen vissza a következő parancsot a folyamat. A parancsmag írhat, meg kell valósítani egy parancsmag-osztályt, amely a két speciális parancsmag alaposztályok közül. A származtatott osztály kell:

- Olyan attribútum, amely azonosítja a származtatott osztály, a parancsmag deklarálható.

- Az attribútumok, amelyek azonosítják a nyilvános tulajdonságokat a parancsmag-paraméterek vannak kitüntetett nyilvános tulajdonságok meghatározásához.

- Bírálja felül egy vagy több bemeneti feldolgozási módszerek rekordok feldolgozásához.

Az osztály segítségével közvetlenül tartalmazó szerelvény betöltése a [Import-Module](/powershell/module/microsoft.powershell.core/import-module) parancsmagot, vagy létrehozhat egy fogadó alkalmazás, amely betölti a szerelvény segítségével az [ System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) API-t. Mindkét módszer programozott hozzáférés biztosítása és parancssori a parancsmag működését.

## <a name="cmdlet-terms"></a>A parancsmag használati

Az alábbi feltételek gyakran használják a Windows PowerShell-parancsmag dokumentáció:

- **A parancsmag attribútum**: A .NET-keretrendszer attribútum, amely szerint a parancsmag egy parancsmag osztály kódcsomagjaihoz. Bár Windows PowerShell számos más attribútum megadása nem kötelező, a parancsmag attribútumot kötelező megadni. Ez az attribútum kapcsolatos további információkért lásd: [parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md).

- **Parancsmag-paraméterben**: A nyilvános tulajdonságok, amelyek meghatározzák a paramétereket, vagy az alkalmazásban, amelyek a parancsmagot a felhasználó számára elérhető. Parancsmagok is szükséges, nevesített, Helyzetbeállító, és *váltson* paramétereket. Kapcsolóparaméterek lehetővé teszik a kiértékelt csak akkor, ha a paraméterek vannak megadva a hívás paramétereit. A különböző típusú paraméterekkel kapcsolatos további információkért lásd: [parancsmag-paraméterek](./cmdlet-parameters.md).

- **Paraméterkészlet**: Egy csoport, amely ugyanazt a parancsot egy adott művelet végrehajtására használható paraméterek. A parancsmag több paraméterkészlettel is rendelkezhet, de egyes paraméterkészletet rendelkeznie kell legalább egy paramétert, amely egyedi. Jó parancsmag tervezési erősen javasolja, hogy az egyedi paramétereket is kell-e egy szükséges paraméter. Paraméterkészlettel kapcsolatos további információkért lásd: [parancsmag paraméterkészletek](./cmdlet-parameter-sets.md).

- **Dinamikus paraméterek**: Egy paraméter, amely a futásidőben a parancsmag kerül. Általában a dinamikus paramétereket a parancsmaghoz, ha egy másik paraméter egy adott értékre van állítva. Dinamikus paraméterekkel kapcsolatos további információkért lásd: [dinamikus parancsmag-paraméterek](./cmdlet-dynamic-parameters.md).

- **Bemeneti metódusához feldolgozási**: Ez a módszer a parancsmag segítségével feldolgozásához bemenetként fogadott rekordokat. A bemeneti feldolgozási módszerek közé tartozik a [System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) metódus, a [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódus, a [System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódust, és a [System.Management.Automation.Cmdlet.Stopprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.StopProcessing) metódust. A parancsmag megvalósításakor, felül kell írnia legalább egyike a [System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing), [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), és [ System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) módszereket. Általában a [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) módszer esetében a módszert, bírálhatja felül, mert a parancsmag rekordot nevezzük. Ezzel szemben a [System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) módszer és a [System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) metódus végrehajtásához nevezzük egyszer előzetesen feldolgozni, vagy a rekordok utófeldolgozása. Ezek a metódusok kapcsolatos további információkért lásd: [bemenet feldolgozása módszerek](./cmdlet-input-processing-methods.md).

- **A szolgáltatás ShouldProcess**: Windows PowerShell-parancsmagokkal kéri a felhasználótól a visszajelzéseket, mielőtt a parancsmag egy módosítást hajt végre a rendszer létrehozását teszi lehetővé. Ez a funkció használatához a parancsmag deklarálni kell, hogy a parancsmag attribútum deklarálhatja, és hívja meg, a parancsmag a ShouldProcess funkció támogatja a [System.Management.Automation.Cmdlet.Shouldprocess*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [ System.Management.Automation.Cmdlet.Shouldcontinue*](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) módszerek a feldolgozási mód egy bemeneti adatban. A ShouldProcess funkciót kapcsolatos további információkért lásd: [megerősítést kérő](./requesting-confirmation-from-cmdlets.md).

- **Tranzakció**: Logikai csoport, amely egyetlen feladat számít. A feladat automatikusan sikertelen lesz, ha a csoportban lévő bármely parancs meghiúsul, és a felhasználónak a választás elfogadja vagy elutasítja a tranzakción belül végrehajtott műveleteket. A tranzakcióban részt, a parancsmag deklarálni kell, hogy amikor a parancsmag attribútum lett deklarálva tranzakciók támogatja. Tranzakciók támogatása Windows PowerShell 2.0-s verziójában jelent meg. Tranzakciókkal kapcsolatos további információkért lásd: [Windows PowerShell-tranzakciók](http://msdn.microsoft.com/en-us/74d7bac7-bc53-49f1-a47a-272e8da84710).

## <a name="how-cmdlets-differ-from-commands"></a>Hogyan parancsmagok eltérnek-e a parancsok

Parancsmagok eltérnek más parancshéj környezetekben parancsok a következő módon:

- A parancsmagok olyan .NET-osztályok; példánya azok nem önálló végrehajtható fájlok.

- Parancsmagok a fájlformátumba egy tucat sornyi kód hozható létre.

- Parancsmagok általánosan még nem a saját elemzés hiba bemutatót vagy kimeneti formázás. Elemzés, a hiba bemutató és a kimeneti formázás a Windows PowerShell-modul a kezeli.

- Parancsmagok folyamat bemeneti objektumok a folyamatból, nem pedig az a szöveg adatfolyamokat, és a parancsmagok kimenetét a folyamat általában objektumok kínált.

- A parancsmagok olyan rekord-orientált mert azok egyetlen objektum egyszerre feldolgozni.

## <a name="cmdlet-base-classes"></a>A parancsmag Base-osztályok

Windows PowerShell-parancsmagokkal a következő két alaposztályok alapján támogatja.

- .NET-keretrendszer osztályokat, amelyek származtatást alapján a legtöbb parancsmagok a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) alaposztály. Ez az osztály kapcsolatból származtatott kapcsolatot lehetővé teszi, hogy a parancsmag a Windows PowerShell-modul a függőségek minimálisan használandó. Ez a két előnye van. Az első előnye, hogy a parancsmag objektumok kisebb, és kevésbé valószínű, hogy a Windows PowerShell-modul által érintett. A második előnye, hogy meg kell, ha közvetlenül létrehozhat a parancsmag objektum egy példányát és majd meghívása helyett közvetlenül ad meg, a Windows PowerShell-modul segítségével.

- Az összetettebb parancsmagok célosztályából származik, a .NET-keretrendszer kulcsfontosságúként alapulnak a [System.Management.Automation.Pscmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) alaposztály. Ez az osztály kapcsolatból származtatott kapcsolatot sokkal több hozzáférést biztosít a Windows PowerShell-modul. A hozzáférés lehetővé teszi, hogy a parancsfájlok, szolgáltatók eléréséhez, és az aktuális munkamenet-állapot eléréséhez hívja a parancsmaghoz. (Az aktuális munkamenet-állapot eléréséhez, lekérése és állítsa be a munkamenet-változókat és a beállításokat.) Azonban ez az osztály kapcsolatból származtatott kapcsolatot növeli a méretét, a parancsmag objektum, és az azt jelenti, hogy a parancsmag nagyobb mértékben használja a Windows PowerShell-modul az aktuális verzióra.

Általánosságban elmondható, kivéve, ha a Windows PowerShell-modulban a kiterjesztett hozzáférésre van szüksége, akkor típusból kell származtatni a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály. Azonban a Windows PowerShell-modul rendelkezik parancsmag végrehajtásának részletes naplózási képességeket. Ha a naplózási modell attól függ, hogy a naplózás, a parancsmag belül egy másik parancsmag végrehajtásának megakadályozása kapcsolatból származtatott kapcsolatot a [System.Management.Automation.Pscmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) osztály.

## <a name="input-processing-methods"></a>Adjon meg feldolgozási módszerek

A [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály biztosít a rekordok feldolgozásához használt következő virtuální metody. A parancsmag származtatott osztályokat felül kell írnia egy vagy több első három módszer:

- [System.Management.Automation.Cmdlet.Beginprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing): A parancsmag nem kötelező egyszeri, előfeldolgozási funkciók biztosításához használt.

- [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord): A rekord-rekord feldolgozási funkcionalitással a parancsmag segítségével. A [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódus tetszőleges szám, ahányszor, vagy egyáltalán nem, a parancsmag bemeneti függően előfordulhat, hogy hívható.

- [System.Management.Automation.Cmdlet.Endprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing): A parancsmag nem kötelező egyszeri, utófeldolgozási funkciók biztosításához használt.

- [System.Management.Automation.Cmdlet.Stopprocessing*](/dotnet/api/System.Management.Automation.Cmdlet.StopProcessing): Leállítja a feldolgozást, ha a felhasználó leállítja a parancsmag aszinkron módon (például a CTRL + C billentyűkombinációval) segítségével.

Ezek a metódusok kapcsolatos további információkért lásd: [parancsmag bemeneti feldolgozása módszerek](./cmdlet-input-processing-methods.md).

## <a name="cmdlet-attributes"></a>Parancsmag-attribútumok

Windows PowerShell parancsmagok kezeléséhez, és adja meg az általános funkciókkal, amelyek Windows PowerShell által biztosított és, amely szükséges lehet a parancsmag által használt számos .NET-keretrendszer-attribútum határozza meg. Például attribútumok használhatók egy osztály megjelölni egy parancsmagot, adja meg a parancsmag paramétereit, és az érvényesítés bemenet igénylése, hogy a parancsmag a fejlesztők kelljen várniuk a parancsmag programkódban implementálni. Az attribútumokkal kapcsolatos további információkért lásd: [Windows PowerShell-attribútumok](./cmdlet-attributes.md).

## <a name="cmdlet-names"></a>A parancsmag neve

Windows PowerShell-parancsmagok neve ige-főnév neve kulcspárt használó. Ha például a `Get-Command` szereplő Windows PowerShell parancsmaggal kéri le a parancsmagok, amelyek a parancs-rendszerhéjban. A művelet azonosítására, a parancsmag hajt végre műveletet és a főnév azonosítja az erőforrást, amelyen a parancsmag hajt végre a műveletet.

Ezek a neve meg van határozva, amikor a .NET-keretrendszer osztály van deklarálva, a parancsmag. A parancsmag egy .NET-keretrendszer osztályban deklaráljon kapcsolatos további információkért lásd: [parancsmag típusattribútum-deklaráció](./cmdlet-class-declaration.md).

## <a name="writing-cmdlet-code"></a>A parancsmag kód írása

Ez a dokumentum felderíteni, hogyan parancsmag kód írása kétféle módszert biztosít. Ha inkább a kód sok magyarázat nélkül, tekintse meg [parancsmag kód példák](./examples-of-cmdlet-code.md). Ha inkább a kód kapcsolatos további részletekért, lásd: a [GetProc oktatóanyag](./getproc-tutorial.md), [StopProc oktatóanyag](./stopproc-tutorial.md), vagy [SelectStr oktatóanyag](./selectstr-tutorial.md) témaköröket.

Az irányelvek írása parancsmagok kapcsolatos további információkért lásd: [parancsmag fejlesztési irányelvek](./cmdlet-development-guidelines.md).

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-parancsmaggal kapcsolatos fogalmak](./windows-powershell-cmdlet-concepts.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)
