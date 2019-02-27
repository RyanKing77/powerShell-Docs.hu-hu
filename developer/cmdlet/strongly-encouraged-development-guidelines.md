---
title: Erősen javasolt, fejlesztői útmutató |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4d68a8f3-fba0-44c5-97b9-9fc191d269a5
caps.latest.revision: 13
ms.openlocfilehash: 2bf2447eba07b74f8cc14c9820fc1c1774370b2f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845415"
---
# <a name="strongly-encouraged-development-guidelines"></a>Javasolt fejlesztői útmutató

Ez a szakasz ismerteti, amely a parancsmagok írásakor követendő útmutatást. Útmutató a parancsmagok és a parancsmag kód írására vonatkozó irányelvek tervezése oszthatók. Előfordulhat, hogy ezeket az irányelveket mindegyik forgatókönyv nem vonatkoznak. Azonban ha vonatkoznak, és nem követi ezeket az irányelveket, a felhasználók rendelkezhet egy rossz élmény a parancsmagok használata esetén.

## <a name="design-guidelines"></a>Tervezési útmutató

- [A parancsmag neve (SD01) egy adott főnév használata](./strongly-encouraged-development-guidelines.md#use-a-specific-noun-for-a-cmdlet-name-sd01)

- [A parancsmag neve (SD02) Pascal használatieset](./strongly-encouraged-development-guidelines.md#use-pascal-case-for-cmdlet-names-sd02)

- [A paraméter tervezési útmutató (SD03)](./strongly-encouraged-development-guidelines.md#parameter-design-guidelines-sd03)

- [Visszajelzés küldése a felhasználónak (SD04)](./strongly-encouraged-development-guidelines.md#provide-feedback-to-the-user-sd04)

- [Hozzon létre egy parancsmag súgóját fájlt (SD05)](./strongly-encouraged-development-guidelines.md#create-a-cmdlet-help-file-sd05)

## <a name="code-guidelines"></a>Kód irányelvek

- [Kódolási paraméterek (SC01)](./strongly-encouraged-development-guidelines.md#coding-parameters-sc01)

- [Támogatja a jól meghatározott adatcsatorna bemenetének (SC02)](./strongly-encouraged-development-guidelines.md#support-well-defined-pipeline-input-sc02)

- [Egyetlen rekord írni a folyamat (SC03)](./strongly-encouraged-development-guidelines.md#write-single-records-to-the-pipeline-sc03)

- [Győződjön meg, a parancsmagok kis-és nagybetűket (SC04), és](./strongly-encouraged-development-guidelines.md#make-cmdlets-case-insensitive-and-case-preserving-sc04)

## <a name="design-guidelines"></a>Tervezési útmutató

A parancsmagokkal és más parancsmagok közötti egységes felhasználói élmény biztosításához parancsmagok tervezésekor a következő irányelveket kell követni. Ha megtalálta a tervezési útmutató arra az esetre, amely a helyzetére vonatkozik, mindenképpen tekintse meg hasonló irányelvek kód irányelvei.

### <a name="use-a-specific-noun-for-a-cmdlet-name-sd01"></a>A parancsmag neve (SD01) egy adott főnév használata

A parancsmag elnevezési használt főneveket kell címkeszakaszt konkrétan meg kell, hogy a felhasználó felderíthessék a parancsmagokat. Például a "kiszolgáló", a termék neve akkor használhatja rövidített verziójával általános főneveket előtagot. Ha főnév, amely a Microsoft SQL Server-példányt futtató kiszolgálóra utal, például egy főnév, például az "SQLServer" használja. Adott főneveket kombinációja és a rövid jóváhagyott igék felsorolása lehetővé teszik a felhasználónak gyors észlelését, és előrejelezheti a funkciók között parancsmagok neveivel duplikáció elkerülhető.

A felhasználói élmény javítása érdekében a főnév, amely egy parancsmag neve ki teljesülését kell lennie. Például a nevét használja `Get-Process` helyett **Get-folyamatok**. A legcélszerűbb akkor is, ha a parancsmag valószínűleg számára, hogy egynél több elem hajtsa végre a Ez a szabály az összes parancsmag-nevekkel kapcsolatban.

### <a name="use-pascal-case-for-cmdlet-names-sd02"></a>A parancsmag neve (SD02) Pascal használatieset

Használjon Pascal eset paraméterek nevei. Más szóval az első betűje művelet és az összes kifejezést a főnév használatban. Például "`Clear-ItemProperty`".

### <a name="parameter-design-guidelines-sd03"></a>A paraméter tervezési útmutató (SD03)

Egy parancsmag-igényeihez paramétereket, amelyek fogadják az adatokat, amelyen működik, és a paraméterek, amely jelzi, amely azt határozza meg a műveletet jellemzőit információkat. A parancsmag Előfordulhat például, egy `Name` paraméter, amely adatokat fogad az a folyamat, és a parancsmag előfordulhat, hogy rendelkezik egy `Force` paraméter jelzi, hogy a parancsmag is kényszeríthető a művelet végrehajtásához. A parancsmag meghatározó paraméterek száma nincs korlátozva van.

#### <a name="use-standard-parameter-names"></a>Standard paraméter neve

A parancsmag standard paraméterneveket kell használnia, úgy, hogy a felhasználók gyorsan megállapíthassák egy adott paraméter azt jelenti. Ha szükség egy pontosabb nevet, használja a normál paraméter neve, és majd adjon meg egy pontosabb nevet aliasként. Ha például a `Get-Service` parancsmag paramétereinek rendelkezik egy általános nevet (`Name`) és a egy pontosabb alias (`ServiceName`). Nagy valószínűséggel mindkét kifejezéssel segítségével adja meg a paramétert.

Paraméter- és adattípusaikat kapcsolatos további információkért lásd: [parancsmag paraméter nevének és a funkciók irányelvek](./standard-cmdlet-parameter-names-and-types.md).

#### <a name="use-singular-parameter-names"></a>Egyetlen paraméter neve

Kerülje a többes számú nevek paraméterek, amelynek az értéke az elemet. Ez a paramétereket, amelyek tömbök, vagy sorolja fel, mert a felhasználó előfordulhat, hogy adja meg, egy tömb, vagy csak egy elemet a listában.

Többes számú paraméterek nevei csak az azokban az esetekben, ahol a paraméter értéke mindig többelemű értéket kell használni. Ezekben az esetekben a parancsmag ellenőrizze, hogy több elem van megadva, és a parancsmag kell megjelenítenie a felhasználónak egy figyelmeztetés, ha több elem nem rendelkeznek.

#### <a name="use-pascal-case-for-parameter-names"></a>A paraméterek nevei Pascal használatieset

Használjon Pascal eset paraméterek nevei. Más szóval nagybetűvel a paraméternév megadásához, beleértve a nevének első betűje szereplő minden szó első betűjét. Ha például a paraméternév `ErrorAction` használja a megfelelő kis-és nagybetűk. A következő paraméter helytelen kis-és nagybetűk használnak:

- `errorAction`

- `erroraction`

#### <a name="parameters-that-take-a-list-of-options"></a>Paraméterek, amelyek a lehetőségek listája

Két módon hozzon létre egy paramétert, amelynek értéke a beállítási lehetőségek lehet kiválasztani.

- Egy enumerálás típusúnak határozza meg (vagy használjon egy már meglévő felsorolási típus), amely meghatározza, hogy az érvényes értékek. Ezt követően a számbavételi típus használatával hozzon létre egy adott típusú paramétert.

- Adja hozzá a **ValidateSet** a paraméterdeklarációhoz attribútumot. Ez az attribútum kapcsolatos további információkért lásd: [ValidateSet típusattribútum-deklaráció](./validateset-attribute-declaration.md).

#### <a name="use-standard-types-for-parameters"></a>Standard típusú paramétereket

A többi parancsmag konzisztencia biztosításához használja alaptípusok paraméterek, ahol ashley lehetséges. A különböző paraméter használandó típusaival kapcsolatos további információkért lásd: [szabványos parancsmag-paraméterek nevei és típusok](./standard-cmdlet-parameter-names-and-types.md). Ez a témakör nevét és .NET-keretrendszer szabványos paraméterek, például a "tevékenység-paraméterek" csoportjait típusainak leíró több témakörök mutató hivatkozásokat tartalmaz.

#### <a name="use-strongly-typed-net-framework-types"></a>Szigorú típusmegadású .NET-keretrendszer típusok használata

Paraméterek jobb paraméter ellenőrzése biztosít a .NET-keretrendszer típusú lehet definiálni. Például paramétereket, az értékek közül csak az egyik érték számbavételi, meg kell határozni. Egységes erőforrás-azonosító (URI) értékét támogatják, definiálni kell a paramétert, a [System.Uri](/dotnet/api/System.Uri) típusa. Kerülje el az összes, de szabad formátumú szöveges tulajdonságainak alapszintű karakterlánc paraméterei.

#### <a name="use-consistent-parameter-types"></a>Használjon egységes paramétertípusok

Több parancsmag használja ugyanezt a paramétert, ha mindig használja az ugyanazon paraméter típusa.  Például ha a `Process` paraméter egy [System.Int16](/dotnet/api/System.Int16) írjon be egy parancsmag, ne tegye elérhetővé a `Process` paraméter egy másik parancsmag egy [System.Uint16](/dotnet/api/System.UInt16) típusa.

#### <a name="parameters-that-take-true-and-false"></a>Paraméterek, amelyek a True és False

Ha a paraméter csak `true` és `false`, adja meg a paraméter típusa [System.Management.Automation.Switchparameter](/dotnet/api/System.Management.Automation.SwitchParameter). Egy új kapcsolóparaméter számít `true` egy parancsban megadott mikor. A paraméter nem szerepel a parancs, ha a Windows PowerShell figyelembe veszi a paraméter kívánt értékét `false`. Logikai típusú paraméterek nem határoznak meg.

Ha a paramétert meg kell megkülönböztetni a 3 érték: $true, $false és "Ismeretlen", majd határozza meg a paraméter Nullable típusú\<bool >.  A 3. a szükségességét "Ismeretlen" érték általában akkor fordul elő, amikor a parancsmag egy objektum logikai tulajdonság módosítható. Ebben az esetben "Ismeretlen" azt jelenti, hogy ne módosítsa a tulajdonság aktuális értéke.

#### <a name="support-arrays-for-parameters"></a>Paraméterek tömbök támogatása

Felhasználók gyakran több argumentumot elleni ugyanazt a műveletet kell végrehajtania. Ezeknek a felhasználóknak a parancsmag kell fogadnia a tömböt, hogy a felhasználó az argumentumokat adhat át a paramétert, egy Windows PowerShell-változóban történő bemeneti paraméterként. Ha például a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmagot használja egy tömb nevének lekéréséhez a folyamatok azonosítása a karakterláncokat.
Felhasználók gyakran több argumentumot elleni ugyanazt a műveletet kell végrehajtania. Ezeknek a felhasználóknak a parancsmag kell fogadnia a tömböt, hogy a felhasználó az argumentumokat adhat át a paramétert, egy Windows PowerShell-változóban történő bemeneti paraméterként. Ha például a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmagot használja egy tömb nevének lekéréséhez a folyamatok azonosítása a karakterláncokat.

#### <a name="support-the-passthru-parameter"></a>A PassThru paraméter támogatása

Alapértelmezés szerint számos parancsmagot, amely módosítása a rendszer, mint például a [Stop-Process](/powershell/module/Microsoft.PowerShell.Management/Stop-Process) parancsmag "fogadóként" objektumok szerepét, és nem adott vissza eredményt. Ezen parancsmag meg kell valósítania az `PassThru` paraméter kényszerítése a parancsmagot, amely egy objektumot ad vissza. Ha a `PassThru` paraméter meg van adva, a parancsmag egy objektumot ad vissza a hívást a [System.Management.Automation.Cmdlet.Writeobject*](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) metódust. Például a következő parancs leállítja a Információmodelleket folyamatot, és a létrejövő folyamat átadása az adatcsatornának.

```powershell
Stop-Process calc -passthru
```

A legtöbb esetben támogatnia kell a Hozzáadás, Set és új parancsmagok egy `PassThru` paraméter.

#### <a name="support-parameter-sets"></a>Támogatási paraméterkészlettel

A parancsmag elvégezni egy egyetlen célt szolgál. Van azonban gyakran több módon le a műveletet, vagy a művelet célja. Például egy folyamatot azonosítja a nevével, az azonosítót, vagy egy folyamat objektumot. A parancsmag támogatnia kell a saját céljainak ésszerű ábrázolásai. Általában a parancsmagot paraméterek (néven paraméterkészlettel) együtt működő csoportok megadásával megfelel ennek a követelménynek. Egyetlen paraméter paraméterkészlettel tetszőleges számú is tartozhat. Paraméterkészlettel kapcsolatos további információkért lásd: [parancsmag paraméterkészletek](./cmdlet-parameter-sets.md).

Paraméterkészlettel megadásakor be csak egy paraméter a ValueFromPipeline beállítása. Deklarálja kapcsolatos további információ a **paraméter** attribútumot, lásd: [ParameterAttribute Deklarace](./parameter-attribute-declaration.md).

Paraméterkészlettel használatakor az alapértelmezett paraméterkészletet határozza meg a **parancsmag** attribútum. Az alapértelmezett paraméterkészletet tartalmaznia kell a legnagyobb valószínűséggel egy interaktív Windows PowerShell-munkamenetben használandó paramétereket. Deklarálja kapcsolatos további információ a **parancsmag** attribútumot, lásd: [CmdletAttribute Deklarace](./cmdlet-attribute-declaration.md).

### <a name="provide-feedback-to-the-user-sd04"></a>Visszajelzés küldése a felhasználónak (SD04)

Ebben a szakaszban az irányelvek segítségével visszajelzés küldése a felhasználónak. A visszajelzés lehetővé teszi, hogy a felhasználó tudni, mi történik a rendszerben, és jobban felügyeleti döntéseket hozhat.

A Windows PowerShell-modul lehetővé teszi, hogy a felhasználót, hogy adja meg, hogyan kezelje az egyes hívások kimenete a `Write` metódus-preferenciaváltozó beállításával. A felhasználó beállíthat több preferenciaváltozók, beleértve egy változó, amely meghatározza, hogy a rendszer információkat és a egy változó, amely meghatározza, hogy a rendszer további műveletek végrehajtása előtti lekérdezése a a felhasználó megjelenjen-e.

#### <a name="support-the-writewarning-writeverbose-and-writedebug-methods"></a>Támogatja a WriteWarning, WriteVerbose és WriteDebug módszerek

A parancsmag meg kell hívnia a [System.Management.Automation.Cmdlet.Writewarning*](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning) metódust, amikor a parancsmag arra készül, hogy előfordulhat, hogy egy nem kívánt eredmények művelet végrehajtására. Például a parancsmag kell hívnia ezt a módszert, ha a parancsmag arra készül, hogy egy csak olvasható fájl felülírása.

A parancsmag meg kell hívnia a [System.Management.Automation.Cmdlet.Writeverbose*](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) metódust, amikor a felhasználó néhány részletet a parancsmag mire van szükség. Például a parancsmag kell hívnia ezt az információt, ha a parancsmag szerzője úgy érzi, hogy nincsenek-e további információt a parancsmag mire igénylő forgatókönyvek.

A parancsmag meg kell hívnia a [System.Management.Automation.Cmdlet.Writedebug*](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) metódust, amikor egy fejlesztői vagy a termékverzió támogatási szakértő ismernie kell, mi van sérült a parancsmag-műveletet. Már nem szükséges a parancsmag hívja a [System.Management.Automation.Cmdlet.Writedebug*](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) metódus az ugyanazt a kódot, amely meghívja a [System.Management.Automation.Cmdlet.Writeverbose*](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) módszer mert a `Debug` paraméter megadja mindkét információt.

#### <a name="support-writeprogress-for-operations-that-take-a-long-time"></a>Műveletek, amelyek hosszú ideig tarthat WriteProgress támogatása

A parancsmag operations egy hosszú ideig, és hogy nem fut a háttérben hosszabb időt igénylő támogatnia kell a jelentési rendszeres hívásainak keresztül a [System.Management.Automation.Cmdlet.Writeprogress*](/dotnet/api/System.Management.Automation.Cmdlet.WriteProgress) metódust.

#### <a name="use-the-host-interfaces"></a>A gazdagép-felület használata

Néha előfordul, a parancsmag kell közvetlenül helyett a felhasználó használatával kommunikálnak a különböző írási vagy által támogatott módszerek kell a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály. Ebben az esetben a parancsmag típusból kell származtatni a [System.Management.Automation.Pscmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) osztályt, és használja a [System.Management.Automation.Pscmdlet.Host*](/dotnet/api/System.Management.Automation.PSCmdlet.Host) tulajdonság. Ez a tulajdonság támogatja a kommunikációs típusa, többek között a PromptForChoice, a parancssort és a WriteLine/ReadLine különböző szinteken. A leginkább adott szint is biztosít írási és olvasási egyedi kulcsok és pufferek kezelésére.

Kivéve, ha a parancsmag kifejezetten célja, hogy hozzon létre egy grafikus felhasználói felületen (GUI), azt kell nem kerüli meg a gazdagép használatával a [System.Management.Automation.Pscmdlet.Host*](/dotnet/api/System.Management.Automation.PSCmdlet.Host) tulajdonság. Hozzon létre egy grafikus felhasználói Felülettel, amely a parancsmag egy példát a [Out-prvku GridView](/powershell/module/Microsoft.PowerShell.Utility/Out-GridView) parancsmagot.

> [!NOTE]
> Ne használjon parancsmagok a [System.Console](/dotnet/api/System.Console) API-t.

### <a name="create-a-cmdlet-help-file-sd05"></a>Hozzon létre egy parancsmag súgóját fájlt (SD05)

Minden parancsmag szerelvény hozzon létre egy Help.xml a parancsmaggal kapcsolatos információkat tartalmazó fájlt. Ezen információk közé tartozik a leírása a parancsmagot, a parancsmag-paraméterek leírását, a parancsmag feltételeit, és a további példákat.

## <a name="code-guidelines"></a>Kód irányelvek

Amikor kódolási parancsmagok a parancsmagokkal és más parancsmagok közötti egységes felhasználói élmény biztosításához a következő irányelveket kell követni. Ha megtalálta, amely a helyzetére vonatkozik kód útmutatásként, mindenképpen tekintse meg a tervezési útmutató hasonló szakaszát.

### <a name="coding-parameters-sc01"></a>Kódolási paraméterek (SC01)

Adjon meg paramétert is deklarálni kell a parancsmag osztály, amely a rendelkeznie kell nyilvános tulajdonsága az **paraméter** attribútum. Paraméterek nem rendelkezik statikus tagjaiként a .NET-keretrendszer osztály a parancsmaghoz. Deklarálja kapcsolatos további információ a **paraméter** attribútumot, lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).

#### <a name="support-windows-powershell-paths"></a>Támogatja a Windows PowerShell-elérési utak

A Windows PowerShell elérési út a mechanizmusa normalizálása névterek való hozzáférést. Egy Windows PowerShell-elérési út hozzárendelése a parancsmag egy paramétert, ha a felhasználó "meghajtó", amely a megadott elérési útra mutató egyéni adhatja meg. Amikor a felhasználó ilyen egy meghajtót jelöl ki, tárolt adatok, például a beállításjegyzékben lévő adatok konzisztens módon használható.

A parancsmag lehetővé teszi, hogy a felhasználó számára adjon meg egy fájl vagy egy adatforrásból, ha azt egy típusú paramétert is meg kell határoznia [System.String](/dotnet/api/System.String). Ha egynél több meghajtó támogatott, a típus egy tömb kell lennie. A paraméter neve legyen `Path`, és a egy aliast `PSPath`. Ezenkívül a `Path` paraméter támogatnia kell a helyettesítő karaktereket. Ha támogatja a helyettesítő karaktereket, nem szükséges, adja meg egy `LiteralPath` paraméter.

Ha a fájl rendelkezik az adatok, amelyek a parancsmagot olvas vagy ír, a parancsmag kell fogadja el a Windows PowerShell-elérési út bemeneti és a parancsmagot kell használnia a [System.Management.Automation.Sessionstate.Path](/dotnet/api/System.Management.Automation.SessionState.Path) lefordítani a Windows tulajdonság A fájlrendszer felismeri görbékké PowerShell elérési utak. Az adott mechanizmusok az alábbi módszerek az alábbiak:

- [System.Management.Automation.Pscmdlet.Getresolvedproviderpathfrompspath](/dotnet/api/System.Management.Automation.PSCmdlet.GetResolvedProviderPathFromPSPath)

- [System.Management.Automation.Pscmdlet.Getunresolvedproviderpathfrompspath](/dotnet/api/System.Management.Automation.PSCmdlet.GetUnresolvedProviderPathFromPSPath)

- [System.Management.Automation.Pathintrinsics.Getresolvedproviderpathfrompspath](/dotnet/api/System.Management.Automation.PathIntrinsics.GetResolvedProviderPathFromPSPath)

- [System.Management.Automation.Pathintrinsics.Getunresolvedproviderpathfrompspath](/dotnet/api/System.Management.Automation.PathIntrinsics.GetUnresolvedProviderPathFromPSPath)

Ha az adatokat, amelyek a parancsmagot olvas vagy ír, csak karakterláncok helyett egy fájlt, a parancsmag egy készletét a szolgáltató tartalommal kapcsolatos információkat kell használnia (`Content` tag) olvasását és írását. Ez az információ szerezhető az [System.Management.Automation.Provider.Cmdletprovider.Invokeprovider*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.InvokeProvider) tulajdonság. Ezek a mechanizmusok engedélyezése más adattárakban olvasását és írását az adatok a való részvételre.

#### <a name="support-wildcard-characters"></a>Támogatja a helyettesítő karakterek

A parancsmag támogatnia kell a helyettesítő karakterek Ha lehetséges. Helyettesítő karakterek támogatása a parancsmag sok helyen történik (különösen akkor, ha egy paraméter azonosításához objektumok közül az egyik objektum egy karakterláncot vesz igénybe). Például a minta **állítsa le a folyamaton** parancsmagot a [StopProc oktatóanyag](./stopproc-tutorial.md) meghatározása egy `Name` paraméter karakterláncok, amelyek a folyamat nevét kezelésére. Ez a paraméter támogatja a helyettesítő karaktereket, hogy a felhasználó egyszerűen adja meg a folyamat leállítása.

Ha támogatja a helyettesítő karakterek érhető el, egy parancsmag művelet általában egy tömböt hoz létre. Néha előfordul akkor nem értelme tömböt támogatására, mert a felhasználó egyszerre csak egy elemet lehet, hogy használ. Ha például a [hely beállítása](/powershell/module/Microsoft.PowerShell.Management/Set-Location) parancsmag nem támogatja a tömböt, mert a felhasználó beállítása csak egyetlen helyen kell. Ebben a példában a parancsmag továbbra is támogatja a helyettesítő karaktereket, de feloldási kényszerül, egyetlen helyen.

Helyettesítő karakteres minták kapcsolatos további információkért lásd: [helyettesítő karakterek támogató parancsmag-paraméterek](./supporting-wildcard-characters-in-cmdlet-parameters.md).

#### <a name="defining-objects"></a>Objektumok meghatározása

Ez a szakasz definiálása objektumok parancsmagok és a meglévő objektumok kiterjesztésére vonatkozó irányelveket tartalmaz.

##### <a name="define-standard-members"></a>Standard tagok megadása

Adja meg a standard tagok kiterjesztését egy objektumtípust, egy egyéni Types.ps1xml fájlban (a Windows PowerShell Types.ps1xml fájl sablonként használható). Standard tagok PSStandardMembers nevű csomópont határozzák meg. Ezeknek a definícióknak engedélyezése más parancsmagok és a Windows PowerShell modul az objektum konzisztens módon működnek.

##### <a name="define-objectmembers-to-be-used-as-parameters"></a>Adja meg paraméterekként használandó ObjectMembers

A parancsmag egy objektum tervezésekor, győződjön meg arról, hogy a tagok képezhetők le közvetlenül a paramétereket a parancsmagok, amelyek használják azt. Ez a leképezés lehetővé teszi, hogy az objektum egyszerűen kell küldeni a folyamat és átadandó egy parancsmag egy másikba.

Már létező .NET keretrendszer objektumait parancsmagok által visszaadott gyakran hiányzik néhány fontos vagy kényelmes tagot, a szkript fejlesztői vagy a felhasználó szükséges. Ezek a hiányzó tagok különösen fontos, megjelenítés és létrehozásához a neveket a megfelelő tag, hogy az objektum megfelelően adható át a folyamat lehet. Hozzon létre egy egyéni Types.ps1xml fájlt a szükséges tagokkal együtt azonnal dokumentálni. Ez a fájl létrehozásakor javasoljuk az alábbi elnevezési szabályt követik: *< Your_Product_Name >*. Types.ps1xml.

Például hozzáadhat egy `Mode` parancsfájl-tulajdonságot a [System.IO.Fileinfo](/dotnet/api/System.IO.FileInfo) írja be a fájl attribútumainak egyértelműbben megjelenítése. Emellett hozzáadhat egy `Count` alias tulajdonságot a [System.Array](/dotnet/api/System.Array) írja be a tulajdonság neve konzisztens használatának engedélyezése a (helyett `Length`).

##### <a name="implement-the-icomparable-interface"></a>A IComparable felület megvalósítása

Alkalmazzon egy [System.Icomparable](/dotnet/api/System.IComparable) összes kimeneti objektumának felületet. Ez lehetővé teszi a különböző rendezési és elemzési parancsmagok egyszerűen irányíthatja át a kimeneti objektumok.

##### <a name="update-display-information"></a>Megjelenítési adatok frissítése

Ha jelenítse meg az objektum nem ad meg a várt eredményt, hozzon létre egy egyéni  *\<YourProductName >*. Az objektum Format.ps1xml fájlt.

### <a name="support-well-defined-pipeline-input-sc02"></a>Támogatja a jól meghatározott adatcsatorna bemenetének (SC02)

#### <a name="implement-for-the-middle-of-a-pipeline"></a>A folyamat közepéről megvalósítása

Feltételezve, hogy azt fogja meghívni egy folyamat közepéről származó parancsmag végrehajtása (azt jelenti, más parancsmagokkal fog előállítani a bemeneti vagy a kimenetét felhasználása). Például előfordulhat, hogy feltételeztük, hogy a `Get-Process` parancsmag hozza azt létre adatokat, mert használatos csak az első parancsmag egy folyamatban. Azonban ezt a parancsmagot egy folyamat közepéről lett tervezve, mert ez a parancsmag lehetővé teszi, hogy előző parancsmagok vagy adatokat a folyamatban, hogy a folyamatok lekéréséhez adja meg.

#### <a name="support-input-from-the-pipeline"></a>A folyamat támogatja a bemenetet

Állítsa be a parancsmag minden paraméter, legalább egy paramétert, amely támogatja a folyamat a bemenetet. Adatcsatorna bemenetének támogatása lehetővé teszi, hogy az adatokat vagy objektumokat, küldje el azokat a megfelelő paraméterkészletet, és adja át az eredményeket közvetlenül a parancsmag a lekérdezni kívánt felhasználó.

Egy paramétert a folyamat a bemenetet fogad el, ha a **paraméter** attribútum tartalmazza a `ValueFromPipeline` kulcsszó, a `ValueFromPipelineByPropertyName` kulcsszó attribútumot, vagy két kulcsszó a deklarációjában szereplő értékkorlátozással. Ha a paramétereket egy paraméterben egyike állítsa be a támogatási a `ValueFromPipeline` vagy `ValueFromPipelineByPropertyName` kulcsszavakat, a parancsmag nem közérthetően helyezhető után más parancsmagok, mert azt figyelmen kívül bármely adatcsatorna bemenetének.

#### <a name="support-the-processrecord-method"></a>Támogatja a ProcessRecord metódus

Fogadja el a fenti parancsmag a folyamat minden rekordját, hogy a parancsmag meg kell valósítani a [System.Management.Automation.Cmdlet.Processrecord*](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) metódust. Windows PowerShell meghívja ezt a metódust többször, egyszer minden rekord, amelyet elküld a parancsmaghoz.

### <a name="write-single-records-to-the-pipeline-sc03"></a>Egyetlen rekord írni a folyamat (SC03)

A parancsmag objektumokat adja vissza, ha a parancsmagot kell írnia az objektumok azonnal akkor jönnek létre. A parancsmag kell nem tartja őket annak érdekében, hogy a puffer őket egy kombinált tömbbe. A parancsmagokkal, amelyeket az objektumokat fogad bemenetként tudnak dolgozza fel, megjelenítéséhez, vagy feldolgozni és megjeleníteni a kimeneti objektumok késedelem nélkül. A parancsmag által létrehozott kimeneti objektumok egyenként meg kell hívnia a [System.Management.Automation.Cmdlet.Writeobject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) metódust. A parancsmag által létrehozott kimeneti objektumok kötegekben (például azért, mert az alapul szolgáló API kimeneti objektumok egy tömbjét adja vissza) meg kell hívnia a [System.Managemet.Automation.Cmdlet.Writeobject](/dotnet/api/System.Managemet.Automation.Cmdlet.WriteObject) a második módszer beállítása a `true`.

### <a name="make-cmdlets-case-insensitive-and-case-preserving-sc04"></a>Győződjön meg, a parancsmagok kis-és nagybetűket (SC04), és

Alapértelmezés szerint a Windows PowerShell magát a kis-és nagybetűket. Azonban számos már létező rendszer foglalkozik, mert Windows PowerShell egyszerű esetet műveletet és kompatibilitás megőrzése. Más szóval ha karakter van megadva a nagybetűs Windows PowerShell tartja azt a nagybetűk. Rendszerekhez való megfelelően működjön a parancsmag kell ezt a konvenciót követi. Ha lehetséges hogy kell működnie a és nagybetűk megkülönböztetése. Akkor kell, azonban megőrzi az eredeti esetben parancsmagok, amelyek később egy paranccsal vagy a folyamat.

## <a name="see-also"></a>Lásd még:

[Szükséges fejlesztési irányelvek](./required-development-guidelines.md)

[Tanácsadói fejlesztői útmutató](./advisory-development-guidelines.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
