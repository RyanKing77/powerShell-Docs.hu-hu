---
title: A Windows PowerShell-szolgáltató tervezése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- providers [PowerShell Programmer's Guide], designing
ms.assetid: 11d20319-cc40-4227-b810-4af33372b182
caps.latest.revision: 10
ms.openlocfilehash: 711a85e9b2eade7b9095d7560f53610e709e380a
ms.sourcegitcommit: 69abc5ad16e5dd29ddfb1853e266a4bfd1d59d59
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57429941"
---
# <a name="designing-your-windows-powershell-provider"></a>A Windows PowerShell-szolgáltató tervezése

Egy Windows PowerShell-szolgáltatóval kell megvalósítania, ha a terméket vagy konfigurációs tesz elérhetővé, tárolt adatok, például egy adatbázis, amely a felhasználó fog lépjen be vagy Tallózza be szeretné. Emellett ha a termék biztosít egy tároló, még akkor is, ha már nem többszintű tároló, logikus megvalósítani egy Windows PowerShell-szolgáltatóban. Például érdemes megvalósítani egy Windows PowerShell-tároló szolgáltató, ha a parancsmag művelet másolási, áthelyezés, átnevezése, új, vagy távolítsa el az így a termék vagy a konfigurációs adatok műveletként.

## <a name="windows-powershell-paths-identify-your-provider"></a>Windows PowerShell-elérési utak a szolgáltató azonosítása

A Windows PowerShell-modul Windows PowerShell-elérési utak a megfelelő Windows PowerShell-szolgáltató elérésére használja. A parancsmag az elérési utak egyikét adja meg, ha a futtatókörnyezet tudja, melyik-szolgáltatót a kapcsolódó adatokat tároló eléréséhez. Az elérési utak közé tartozik a meghajtó minősített elérési utak, a szolgáltató minősített elérési utak, a szolgáltató-direct elérési utak és a provider – belső elérési utak. Minden Windows PowerShell-szolgáltatóban támogatnia kell az elérési utak közül legalább egyet.

Windows PowerShell útvonalakkal kapcsolatos további információkért tekintse meg a Windows PowerShell működése.

### <a name="defining-a-drive-qualified-path"></a>A meghajtó elérési útját meghatározása

Ahhoz, hogy a felhasználó számára egy fizikai meghajtón található adatok elérését, a Windows PowerShell-szolgáltatóban támogatnia kell a meghajtó elérési útját. Ennek az elérési útnak a meghajtó nevét, majd kettőspontot (:), például mydrive:\abc\bar kezdődik.

### <a name="defining-a-provider-qualified-path"></a>A szolgáltató elérési útját meghatározása

Ahhoz, hogy a Windows PowerShell modul inicializálása, és a szolgáltató meghívná, a Windows PowerShell-szolgáltatóban támogatnia kell a szolgáltató elérési útját. Ha például a fájlrendszer::\\\uncshare\abc\bar a szolgáltató elérési útját a fájlrendszer-szolgáltató által a Windows PowerShell.

### <a name="defining-a-provider-direct-path"></a>A szolgáltató-Direct elérési út meghatározása

A távoli hozzáférés lehetővé tételéhez a Windows PowerShell-szolgáltatóban, azt támogatnia kell a szolgáltató-direct elérési útjának át közvetlenül a Windows PowerShell-szolgáltató jelenlegi helyéhez. Például a beállításjegyzék Windows PowerShell-szolgáltatóval használható \\\server\regkeypath szolgáltató-direct elérési útként.

### <a name="defining-a-provider-internal-path"></a>A Provider – belső elérési út meghatározása

Ahhoz, hogy a szolgáltató parancsmag használatával a Windows PowerShell alkalmazásprogramozási felületek (API-k) adatok eléréséhez, a Windows PowerShell-szolgáltatóban támogatnia kell a provider – belső elérési utat. Az elérési út után jelöli a "::" a szolgáltató minősített elérési úton. Ha például a fájlrendszer Windows PowerShell-szolgáltatóban provider – belső elérési útja \\\uncshare\abc\bar.

## <a name="changing-stored-data"></a>A tárolt adatok módosítása

Mindig hívja a módszereket, amelyek módosítják az alapul szolgáló adattár felülbírálásához a [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject) metódus legfrissebb verziójával, az elem, amely módosította a metódus. A szolgáltató infrastruktúra határozza meg, ha az elem objektum kell átadni a folyamat, például amikor a felhasználó adja meg a - PassThru paraméter számára. Ha a legfrissebb elem beolvasása egy erőforrás-igényes művelet (performance-wise), tesztelheti a Context.PassThru tulajdonság határozza meg, ha ténylegesen kell írnia az eredményül kapott elemet.

## <a name="choose-a-base-class-for-your-provider"></a>Válassza ki az osztály a szolgáltató

Windows PowerShell segítségével megvalósítani a saját Windows PowerShell-szolgáltatóban alaposztályok számos biztosít. Amikor egy szolgáltató tervezése az alaposztály alaposztályát, ebben a szakaszban leírt, amely legjobban megfelel az igényeinek megfelelően.

Minden Windows PowerShell szolgáltató alaposztály tesz elérhetővé olyan parancsmagok készletét. Ez a szakasz ismerteti a parancsmagok, de nem ismerteti a paramétereket.

A munkamenet-állapotot használ, a Windows PowerShell-modul elérhetővé teszi számos hely parancsmagok bizonyos Windows PowerShell-szolgáltatóknak, például a `Get-Location`, `Set-Location`, `Pop-Location`, és `Push-Location` parancsmagok. Használhatja a `Get-Help` parancsmag hely parancsmagok használatával kapcsolatos információkért.

### <a name="cmdletprovider-base-class"></a>CmdletProvider alaposztály

A [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) osztály egy alapvető Windows PowerShell-szolgáltató határozza meg. Ez az osztály támogatja a szolgáltató nyilatkozat, és számos tulajdonság és metódus az összes Windows PowerShell-szolgáltatók számára elérhető egy számot ad. Az osztály hív a `Get-PSProvider` parancsmag használatával listázhatja az összes elérhető szolgáltatók a munkamenet. Ez a parancsmag végrehajtásának bemutatásával van a munkamenet-állapot.

> [!NOTE]
> Windows PowerShell-szolgáltatók a Windows PowerShell-nyelv az összes hatókörhöz érhetők el.

### <a name="drivecmdletprovider-base-class"></a>DriveCmdletProvider alaposztály

A [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztály, amely támogatja az új meghajtók hozzáadása, eltávolítása a meglévő meghajtók és alapértelmezett meghajtó inicializálása műveletek Windows PowerShell meghajtót szolgáltató határozza meg. Például a Windows PowerShell által biztosított fájlrendszer-szolgáltatót inicializálja a meghajtókat, amelyek csatlakoztatva vannak, például a merevlemez-meghajtók és a CD/DVD-eszköz meghajtók minden kötet esetében.

Ez az osztály származtatható a a [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) alaposztály. Az alábbi táblázat a parancsmagok, ez az osztály által elérhetővé tett. Fel van sorolva, valamint a `Get-PSDrive` parancsmag (munkamenet-állapot által elérhetővé tett) egy kapcsolódó parancsmag, amely az elérhető meghajtók olvashatók be.

|Parancsmag|Meghatározás|
|------------|----------------|
|`New-PSDrive`|A munkamenetet hoz létre egy új meghajtót, és streameli a meghajtó információi.|
|`Remove-PSDrive`|Egy meghajtót eltávolítja a munkamenetet.|

### <a name="itemcmdletprovider-base-class"></a>ItemCmdletProvider alaposztály

A [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály, amely az egyéni elemek az adattár műveleteket hajt végre a Windows PowerShell elem szolgáltató határozza meg, és nem feltételezi azt minden olyan tárolót, vagy navigációs képességeket. Ez az osztály származtatható a a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) alaposztály. Az alábbi táblázat a parancsmagok, ez az osztály által elérhetővé tett.

|Parancsmag|Meghatározás|
|------------|----------------|
|`Clear-Item`|Törli a elemek a megadott helyen az aktuális tartalmát, és lecseréli a "Törlés", a szolgáltató által megadott értékkel. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|
|`Get-Item`|A megadott helyről elemeket kérdezi le, és streameli az eredményül kapott objektumokat.|
|`Invoke-Item`|Hívja meg az alapértelmezett művelet a megadott elérési úton a cikkhez.|
|`Set-Item`|Beállítja egy elemet a megadott helyen, a megadott értékkel. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|
|`Resolve-Path`|Oldja fel a Windows PowerShell-elérési út és a Streamek útvonaladatait helyettesítő karaktert.|
|`Test-Path`|Megvizsgálja, hogy a megadott elérési út, és visszaadja `true` Ha létezik, és `false` más módon. Ez a parancsmag úgy legyen megvalósítva, hogy támogatja a `IsContainer` paramétere a [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject) metódust.|

### <a name="containercmdletprovider-base-class"></a>ContainerCmdletProvider alaposztály

A [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) osztály, amely közzéteszi az adatokat tároló elemek, a felhasználónak, tárolója Windows PowerShell tároló szolgáltató határozza meg. Vegye figyelembe, hogy egy Windows PowerShell-tároló szolgáltató csak akkor, ha van egy tároló (nem beágyazott tárolók), a benne lévő elemek használhatók-e. Ha beágyazott tárolókat, majd meg kell valósítani egy Windows PowerShell-navigációs szolgáltató.

Ez az osztály származtatható a a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) alaposztály. Az alábbi táblázat a parancsmagok, ez az osztály által megvalósított határozza meg.

|Parancsmag|Meghatározás|
|------------|----------------|
|`Copy-Item`|Másolatok elemek egyik helyről egy másikra. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|
|`Get-Childitem`|Lekéri a megadott helyen bejárásához, és továbbítja azokat objektumokként kezelni.|
|`New-Item`|Új elemeket hozza létre a megadott helyen, és a létrejövő objektum streameli.|
|`Remove-Item`|Eltávolítja a megadott helyről.|
|`Rename-Item`|Átnevezi egy elemet a megadott helyen. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|

### <a name="navigationcmdletprovider-base-class"></a>NavigationCmdletProvider alaposztály

A [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztály meghatározza egy Windows PowerShell navigációs szolgáltató, amely egynél több tárolót használó cikkek műveleteket hajt végre. Ez az osztály származtatható a a [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) alaposztály. A következő táblázat felsorolja a parancsmagok, ez az osztály által elérhetővé tett.

|Parancsmag|Meghatározás|
|------------|----------------|
|Combine-Path|Két útvonalon egyesít egy elérési útvonalat, egy szolgáltatóhoz tartozó elválasztó közötti útvonalak segítségével. Ez a parancsmag karakterláncok streameli.|
|`Move-Item`|Elemek áthelyezése a megadott helyen. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|

Kapcsolódó parancsmag az alapszintű Parse-Path parancsmag Windows PowerShell által. Ez a parancsmag segítségével támogatja a Windows PowerShell elérési útjának elemezni a `Parent` paraméter. A szülő elérési út karakterlánca elemzésének lehetőségeit.

## <a name="select-provider-interfaces-to-support"></a>Válassza ki a szolgáltató kapcsolatok támogatásához

Mellett a Windows PowerShell-alaposztályok egyikéből való származtatás, a Windows PowerShell-szolgáltató által egy vagy több, a következő szolgáltató felületek kapcsolatból származtatott kapcsolatot támogatja a más funkciókat is. Ebben a szakaszban határozza meg, azok az interfészek és a parancsmagok által támogatott. A paraméterek a felület támogatott parancsmagok nem ismerteti. A parancsmag paramétereinek adatai érhető el online használatával a `Get-Command` és `Get-Help` parancsmagok.

### <a name="icontentcmdletprovider"></a>IContentCmdletProvider

A [System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) az illesztő határozza meg, hogy a tartalom egy adatelem műveleteket hajt végre a tartalomszolgáltatón. Az alábbi táblázat a parancsmagok, ez az interfész által elérhetővé tett.

|Parancsmag|Meghatározás|
|------------|----------------|
|`Add-Content`|A megadott érték hossza hozzáfűzi a megadott elem tartalmát. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|
|`Clear-Content`|A "Törlés" értékre állítja be a megadott elem tartalmát. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|
|`Get-Content`|Lekéri a megadott elemek tartalmát, és streameli az eredményül kapott objektumokat.|
|`Set-Content`|Lecseréli a meglévő tartalmának a megadott elemek. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|

### <a name="ipropertycmdletprovider"></a>IPropertyCmdletProvider

A [System.Management.Automation.Provider.Ipropertycmdletprovider](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider) rozhraní definuje egy tulajdonság Windows PowerShell-szolgáltatóban, amely elemek tulajdonságainak műveleteket hajt végre az adattárban. Az alábbi táblázat a parancsmagok, ez az interfész által elérhetővé tett.

> [!NOTE]
> A `Path` ezeket a parancsmagokat a paraméter azt jelzi, hogy helyett azonosító tulajdonság egy elem elérési útját.

|Parancsmag|Meghatározás|
|------------|----------------|
|`Clear-ItemProperty`|A "Törlés" értékre állítja be a megadott elemek tulajdonságai. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|
|`Get-ItemProperty`|Tulajdonságok lekéri a megadott elemek és streameli az eredményül kapott objektumokat.|
|`Set-ItemProperty`|A megadott elemek a megadott értékekkel tulajdonságainak beállítása. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|

### <a name="idynamicpropertycmdletprovider"></a>IDynamicPropertyCmdletProvider

A [System.Management.Automation.Provider.Idynamicpropertycmdletprovider](/dotnet/api/System.Management.Automation.Provider.IDynamicPropertyCmdletProvider) felületen, a származtatott [System.Management.Automation.Provider.Ipropertycmdletprovider](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider), határozza meg a szolgáltató, amely megadja, hogy a támogatott parancsmagok dinamikus paramétereket. Az ilyen típusú szolgáltató kezeli, amelynek tulajdonságai futásidőben, például egy új tulajdonság művelet definiált műveletek. Az ilyen műveletek nem engedélyezettek a kellene statikusan tulajdonságok meghatározott elemek. Az alábbi táblázat a parancsmagok, ez az interfész által elérhetővé tett.

|Parancsmag|Meghatározás|
|------------|----------------|
|`Copy-ItemProperty`|Másolja át egy tulajdonság a megadott elem egy másik cikkhez. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|
|`Move-ItemProperty`|Egy másik cikkhez helyezi át a megadott elem egy tulajdonságot. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|
|`New-ItemProperty`|Létrehoz egy tulajdonság a megadott elemek, és streameli az eredményül kapott objektumokat.|
|`Remove-ItemProperty`|Eltávolítja a megadott elemek tulajdonság.|
|`Rename-ItemProperty`|A megadott elemek egy tulajdonságot átnevezi. Ez a parancsmag nem ad át a folyamat használatával egy kimeneti objektumot, kivéve, ha a `PassThru` paraméter meg van adva.|

### <a name="isecuritydescriptorcmdletprovider"></a>ISecurityDescriptorCmdletProvider

A [System.Management.Automation.Provider.Isecuritydescriptorcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ISecurityDescriptorCmdletProvider) felület biztonsági leíró funkciókkal bővíti a szolgáltató. Ez az interfész lehetővé teszi, hogy a felhasználó, és állítsa be a biztonsági leíró adati egy elem szerepel az adattárban. Az alábbi táblázat a parancsmagok, ez az interfész által elérhetővé tett.

|Parancsmag|Meghatározás|
|------------|----------------|
|`Get-Acl`|A hozzáférés-vezérlési lista (ACL), amely része a használt operációs rendszer erőforrásainak, például megőrzése a biztonsági leíró, a fájl vagy az objektum található adatait kérdezi le.|
|`Set-Acl`|Beállítja a ACL vonatkozó információkat. Az űrlap egy példány van [System.Security.Accesscontrol.Objectsecurity](/dotnet/api/System.Security.AccessControl.ObjectSecurity) található a megadott elérési útja a kijelölt elem(ek). Ez a parancsmag fájlokat, a kulcsok és a alkulcsok állítható be a beállításjegyzéket, vagy bármely más szolgáltató elem, ha a Windows PowerShell-szolgáltató támogatja a biztonsági információk beállításának.|

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-szolgáltató létrehozása](./how-to-create-a-windows-powershell-provider.md)

[Hogyan működik a Windows PowerShell](http://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58)

[Windows PowerShell SDK](../windows-powershell-reference.md)