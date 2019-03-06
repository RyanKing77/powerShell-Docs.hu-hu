---
title: A Windows PowerShell navigációs szolgáltató létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- navigation providers [PowerShell Programmer's Guide]
- providers [PowerShell Programmer's Guide], navigation provider
ms.assetid: 8bd3224d-ca6f-4640-9464-cb4d9f4e13b1
caps.latest.revision: 5
ms.openlocfilehash: cbc8ce0600553f9e9ab973d6f92ea5eafde310e2
ms.sourcegitcommit: 69abc5ad16e5dd29ddfb1853e266a4bfd1d59d59
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/05/2019
ms.locfileid: "57430032"
---
# <a name="creating-a-windows-powershell-navigation-provider"></a>Windows PowerShelles navigációszolgáltató létrehozása

Ez a témakör ismerteti, hogyan hozhat létre egy Windows PowerShell navigációs szolgáltató, amely az adattár navigálhat. Az ilyen típusú szolgáltató támogatja a rekurzív parancsok, a beágyazott tárolók és a relatív elérési utakat.

> [!NOTE]
> Letöltheti a C# forrásfájl (AccessDBSampleProvider05.cs) a szolgáltató a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
>
> A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.
>
> Más Windows PowerShell-szolgáltató esetében kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).

Az itt ismertetett szolgáltató a felhasználóazonosító Access-adatbázisok meghajtóként lehetővé teszi, hogy a felhasználó el lehet érni a data-táblát az adatbázisban. A saját navigációs szolgáltató létrehozásakor valósítható meg, amely képes győződjön meg arról, a meghajtó minősített elérési utak, így a Navigálás szükséges, relatív útvonalakat normalizálása, az adattár, valamint a gyermek nevének lekérése, a szülő elérési útjának egy elemet és teszteléséhez módszerek az elemek áthelyezése módszerek Ha egy elem a tároló azonosításához.

> [!CAUTION]
> Vegye figyelembe, hogy ez a kialakítás feltételezi, hogy egy adatbázis, amely egy mező neve azonosítóval rendelkezik, és hogy a mező típusát LongInteger.

A következők szakaszokat tartalmazza az ebben a témakörben. Ha nem ismeri a Windows PowerShell-navigációs szolgáltató írása, olvassa el ezt az információt a sorrendben, amely akkor jelenik meg. Azonban ha ismeri a Windows PowerShell-navigációs szolgáltató írása, nyissa meg közvetlenül a keresett információt.

- [A PS-navigációs szolgáltató osztálya meghatározása](#Define-the-Windows-PowerShell-provider)

- [Alapfunkciók meghatározása](#Defining-Base-Functionality)

- [A PS-elérési út létrehozása](#Creating-a-Windows-PowerShell-Path)

- [A szülő elérési útjának beolvasása](#Retrieving-the-Parent-Path)

- [A gyermek elérési útja beolvasása](#Retrieve-the-Child-Path-Name)

- [Ha egy elem van-e a tároló](#Determining-if-an-Item-is-a-Container)

- [Egy elem áthelyezése](#Moving-an-Item)

- [Dinamikus paraméterek csatolása a `Move-Item` parancsmag](#Attaching-Dynamic-Parameters-to-the-Move-Item-Cmdlet)

- [Relatív elérési út normalizálása](#Normalizing-a-Relative-Path)

- [Kódminta](#Code-Sample)

- [Objektumtípusok definiálása és formázása](#Defining-Object-Types-and-Formatting)

- [A Windows PowerShell-szolgáltató létrehozása](#Building-the-Windows-PowerShell-provider)

- [A Windows PowerShell-szolgáltatóban tesztelése](#Testing-the-Windows-PowerShell-provider)

## <a name="define-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltató megadása

A Windows PowerShell-navigációs szolgáltató létre kell hoznia egy .NET-osztályt, amely az a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) alaposztály. Itt látható az ebben a szakaszban leírt navigációs szolgáltató osztály definícióját.

[!code-csharp[AccessDBProviderSample05.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample05/AccessDBProviderSample05.cs#L31-L32 "AccessDBProviderSample05.cs")]

Vegye figyelembe, hogy a szolgáltató a [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribútum tartalmazza a két paramétert. Az első paraméter adja meg a Windows PowerShell által használt szolgáltató felhasználóbarát nevét. A második paraméter adja meg a Windows PowerShell adott képességeket, amelyek a szolgáltató tesz elérhetővé a Windows PowerShell-modul a parancs feldolgozása közben. A szolgáltató nincsenek nem hozzáadott adott Windows PowerShell-képességekkel.

## <a name="defining-base-functionality"></a>Alapfunkciók meghatározása

Leírtak szerint [tervezési az PS szolgáltatója](./designing-your-windows-powershell-provider.md), a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) alaposztály származik-e más osztályok másik szolgáltatót a megadott a funkció. A Windows PowerShell-navigációs szolgáltató, ezért meg kell határoznia az összes az adott osztályok által biztosított funkciókat.

Munkamenet-specifikus inicializálási információk hozzáadása és a szolgáltató által használt erőforrások felszabadítása funkció megvalósítását, lásd: [egy alapszintű PS-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md). A legtöbb szolgáltatók (beleértve a szolgáltató az itt leírtak szerint) is használják, ez a funkció Windows PowerShell által biztosított alapértelmezett megvalósítása.

Az adattár eléréséhez keresztül egy Windows PowerShell meghajtót, be kell állítani a módszereket a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) alaposztály. Ezek a metódusok megvalósításával kapcsolatos további információkért lásd: [egy Windows PowerShell-meghajtó szolgáltató létrehozása](./creating-a-windows-powershell-drive-provider.md).

Egy adattár, például az első, a beállítás és a elszámolási elemek, a cikkek módosítására a szolgáltató által biztosított metódusokkal meg kell valósítania az [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) alaposztály. Ezek a metódusok megvalósításával kapcsolatos további információkért lásd: [egy Windows PowerShell elem szolgáltató létrehozása](./creating-a-windows-powershell-item-provider.md).

Első bejárásához, vagy az adattárban, valamint a módszereket, amelyek létrehozása, másolja, átnevezése és eltávolítani is az elemeket, a nevük által biztosított metódusokkal meg kell valósítania az [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)alaposztály. Ezek a metódusok megvalósításával kapcsolatos további információkért lásd: [létrehozása a Windows PowerShell-tároló szolgáltató](./creating-a-windows-powershell-container-provider.md).

## <a name="creating-a-windows-powershell-path"></a>A Windows PowerShell-elérési út létrehozása

Windows PowerShell-navigációs szolgáltató egy Windows PowerShell szolgáltató belső elérési utat használatával keresse meg az adattár elemeit. A provider – belső elérési útja a szolgáltató létrehozásához meg kell valósítani a [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) módszer támogatja az összevonás-Path parancsmag hívásait. Ez a módszer egy szülő és gyermek elérési egyesíti a provider – belső elérési utat, a szülő és gyermek görbék között szolgáltatóhoz tartozó elérési út elválasztóval.

Alapértelmezett megvalósítása veszi az elérési utak "/" vagy "\\"elérési út elválasztóként normalizálja az elválasztó az elérési útban a"\\", a szülő és gyermek elérési útjának részei ötvözi az elválasztó közöttük és a egy karakterláncot, amely tartalmazza majd ad vissza, a Kombinált elérési utak.

A navigációs szolgáltató nem valósítja meg ezt a módszert. Azonban az alábbi kód-e az alapértelmezett megvalósítása a [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) metódust.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidermakepath](Msh_samplestestcmdlets#testprovidermakepath)]  -->

#### <a name="things-to-remember-about-implementing-makepath"></a>Megjegyzendő MakePath megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath):

- A megvalósítását az [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) metódus kell ellenőrzi a elérési útját a szolgáltatói névtér jogi teljesen minősített elérési. Vegye figyelembe, hogy minden paraméter csak hozhat létre egy elérési út egy része, a kombinált részek nem hozhat létre egy teljes elérési útját. Például a [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) metódus a fájlrendszer szolgáltató "windows\system32" kapni a `parent` paraméter és a "abc.dll"`child` paraméter. A metódus csatlakozik az ezeket az értékeket a "\\" elválasztó és a "windows\system32\abc.dll" értéket ad vissza, amely nem a fájl teljes elérési útjára.

  > [!IMPORTANT]
  > Az elérésiút-részleteket hívásában megadott [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) a szolgáltató névterének neve nem engedélyezett karaktereket tartalmaz. Ezek a karakterek nagy valószínűséggel használják helyettesítő bővítés céljából, és ez a metódus végrehajtásának kell távolítja el azokat.

## <a name="retrieving-the-parent-path"></a>A szülő elérési útjának beolvasása

Windows PowerShell navigációs szolgáltatók megvalósítása a [System.Management.Automation.Provider.Navigationcmdletprovider.Getparentpath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetParentPath) metódusának segítéségével lekérheti a szülő része a jelzett teljes vagy részleges Szolgáltatóspecifikus elérési útja. A metódus az elérési út gyermek részét távolítja el, és adja vissza a szülő elérési útjának része. A `root` paraméter teljes elérési útját adja meg a meghajtó gyökérkönyvtára. Ez a paraméter lehet null értékű vagy üres, ha a csatlakoztatott meghajtó nem használja a lekérési művelet. Ha a legfelső szintű van megadva, a metódus egy elérési utat kell visszaadnia ugyanabban a fában a legfelső szintű tárolóba.

A minta navigáció szolgáltató nem bírálja felül ezt a módszert, de használja az alapértelmezett implementációja. Elérési utak, amely egyaránt fogad el "/" és "\\" elérési út elválasztóként. Először Normalizálja a elérési útja csak "\\" elválasztók, majd felosztja a szülő elérési útja ki, az utolsó "\\" és a szülő elérési utat adja vissza.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidergetparentpath](Msh_samplestestcmdlets#testprovidergetparentpath)]  -->

#### <a name="to-remember-about-implementing-getparentpath"></a>GetParentPath megvalósításával kapcsolatos tudnivalók

A megvalósítását az [System.Management.Automation.Provider.Navigationcmdletprovider.Getparentpath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetParentPath) metódus fel kell betűrendbe-kiszolgálón, az elválasztó az elérési útban a szolgáltatói névtér. Például a fájlrendszer-szolgáltatót használja ezt a módszert keresse meg az utolsó "\\" és az elválasztó balra adja vissza minden.

## <a name="retrieve-the-child-path-name"></a>A gyermek elérési útja beolvasása

A navigációs szolgáltató valósítja meg a [System.Management.Automation.Provider.Navigationcmdletprovider.Getchildname*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetChildName) metódussal lehet bekérni az elem a gyermek nevére (levél elem) található a megadott teljes vagy Szolgáltatóspecifikus részleges elérési útja.

A minta navigáció szolgáltató nem bírálja felül ezt a módszert. Az alapértelmezett implementációja alább látható. Elérési utak, amely egyaránt fogad el "/" és "\\" elérési út elválasztóként. Először Normalizálja a elérési útja csak "\\" elválasztók, majd felosztja a szülő elérési útja ki, az utolsó "\\" és a gyermek nevének beolvasása elérési út része.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidergetchildname](Msh_samplestestcmdlets#testprovidergetchildname)]  -->

#### <a name="things-to-remember-about-implementing-getchildname"></a>Megjegyzendő GetChildName megvalósításával kapcsolatos tudnivalók

A megvalósítását az [System.Management.Automation.Provider.Navigationcmdletprovider.Getchildname*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetChildName) metódus fel kell betűrendbe-kiszolgálón, az elválasztó az elérési útban. Ha a megadott elérési úthoz nem elérési út elválasztók tartalmaz, a metódus az elérési út kívánja módosítani kell visszaadnia.

> [!IMPORTANT]
> Ez a metódus hívásában megadott elérési úton a szolgáltatói névtér nem megengedett karaktereket tartalmazhat. Ezek a karakterek legvalószínűbb helyettesítő bővítése vagy reguláris kifejezések egyeztetésének használja, és ez a metódus végrehajtásának kell távolítja el azokat.

## <a name="determining-if-an-item-is-a-container"></a>Ha egy elem van-e a tároló

A navigációs szolgáltató valósíthat meg a [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) módszert meghatározni, ha a megadott elérési út azt jelzi, hogy egy tárolót. IGAZ, ha az elérési utat jelöl egy tárolót, és hamis értéket más módon adja vissza. A felhasználónak kell tudni használni szeretné ezt a módszert a `Test-Path` parancsmag a megadott elérési útja.

A következő kód bemutatja a [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) megvalósítása a minta navigáció szolgáltatóban. A módszer ellenőrzi, hogy a megadott elérési út helyességét, és ha a tábla létezik, és ha az elérési út azt jelzi, hogy a tároló igaz értéket ad vissza.

[!code-csharp[AccessDBProviderSample05.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample05/AccessDBProviderSample05.cs#L847-L872 "AccessDBProviderSample05.cs")]

#### <a name="things-to-remember-about-implementing-isitemcontainer"></a>Megjegyzendő IsItemContainer megvalósításával kapcsolatos tudnivalók

A navigációs szolgáltatói .NET-osztály előfordulhat, hogy deklarálja ExpandWildcards, szűrő, belefoglalása vagy kizárása, szolgáltató képességeit a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. Ebben az esetben végrehajtásának [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) meg kell győződnie arról, hogy az elérési út átadott megfelel-e a követelményeknek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) tulajdonság.

## <a name="moving-an-item"></a>Egy elem áthelyezése

Támogatja az a `Move-Item` parancsmagot, a navigációs szolgáltató valósítja meg a [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) metódust. Ezzel a módszerrel helyezi át az elemazonosító által meghatározott elem a `path` a tároló megadott elérési útja a paramétert a `destination` paraméter.

A minta navigáció szolgáltató nem bírálja felül a [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) metódust. Alapértelmezett megvalósítása a következő:

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidermoveitem](Msh_samplestestcmdlets#testprovidermoveitem)]  -->

#### <a name="things-to-remember-about-implementing-moveitem"></a>Megjegyzendő MoveItem megvalósításával kapcsolatos tudnivalók

A navigációs szolgáltatói .NET-osztály előfordulhat, hogy deklarálja ExpandWildcards, szűrő, belefoglalása vagy kizárása, szolgáltató képességeit a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. Ebben az esetben végrehajtásának [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) biztosítania kell, hogy az elérési út átadott megfelel-e a követelményeknek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a **CmdletProvider.Exclude** tulajdonság.

Alapértelmezés szerint ez a metódus felülbírálását ne helyezze át objektumokat keresztül a meglévő objektumok, kivéve, ha a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Ha például a fájlrendszer-szolgáltatót nem másolja c:\temp\abc.txt egy már létező c:\bar.txt fájl, kivéve, ha a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Ha a megadott elérési útja a `destination` paraméter létezik, és egy tárolót a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonság nem kötelező. Ebben az esetben [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) helyezze át az elem jelzi a `path` által megadott a tárolóhoz a paraméter a `destination` gyermek paraméter.

A megvalósítását az [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) metódus meg kell hívnia [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) , és ellenőrizze a visszaadott érték az adattár változtatások előtt. Ez a módszer segítségével amikor módosításakor a rendszer állapotáról, például fájlokat törli, győződjön meg arról, hogy egy művelet végrehajtását. [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) küld a felhasználó a Windows PowerShell-futtatókörnyezetben, figyelembe véve parancssori beállítást vagy a preferenciaváltozók módosítani az erőforrás neve annak meghatározása, mi megjelenjenek a felhasználó számára.

Hívása után [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) adja vissza `true`, a [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) metódus meg kell hívnia a [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) metódust. Ez a módszer egy üzenetet küld a felhasználó számára lehetővé tegyük fel, ha a művelet folytatni kell a visszajelzés. Meg kell hívnia a szolgáltató [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) , egy potenciálisan veszélyes rendszermódosítások további keresése.

## <a name="attaching-dynamic-parameters-to-the-move-item-cmdlet"></a>Az elem áthelyezése parancsmag dinamikus paraméterek csatolása

Egyes esetekben a `Move-Item` parancsmaghoz szükséges további paraméterek, amelyet dinamikusan futásidőben. Ahhoz, hogy ezek a dinamikus paraméterek, a navigációs a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItemDynamicParameters) módszer a szükséges paraméterértékeket. a megadott elérési út, és lépjen vissza a konfigurációelemet egy objektum, amely rendelkezik a tulajdonságokat és mezőket az elemzés attribútumok hasonlít egy parancsmag osztály vagy egy [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum.

A navigációs szolgáltató nem valósítja meg ezt a módszert. Azonban az alábbi kód-e az alapértelmezett megvalósítása [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItemDynamicParameters).

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidermoveitemdynamicparameters](Msh_samplestestcmdlets#testprovidermoveitemdynamicparameters)]  -->

## <a name="normalizing-a-relative-path"></a>Relatív elérési út normalizálása

A navigációs szolgáltató valósítja meg a [System.Management.Automation.Provider.Navigationcmdletprovider.Normalizerelativepath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.NormalizeRelativePath) jelzett metódus optimalizálására a teljes elérési útját a `path` paraméter által megadott elérési útként állapottal a `basePath` paraméter. A metódus a normalizált elérési karakterláncként adja vissza. Ha a hiba ír a `path` paraméter adja meg egy nem létező elérési utat.

A minta navigáció szolgáltató nem bírálja felül ezt a módszert. Alapértelmezett megvalósítása a következő:

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidernormalizepath](Msh_samplestestcmdlets#testprovidernormalizepath)]  -->

#### <a name="things-to-remember-about-implementing-normalizerelativepath"></a>Megjegyzendő NormalizeRelativePath megvalósításával kapcsolatos tudnivalók

Megvalósítását [System.Management.Automation.Provider.Navigationcmdletprovider.Normalizerelativepath*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.NormalizeRelativePath) kell elemezni a `path` paraméter, de nem kell pusztán szintaktikai elemzés használata. Ezt a módszert, az elérési út használatával megkeresheti az elérési út információkat az adattárban és az elérési utat hoz létre, amely megfelel a kis-és tervezési arra biztatjuk, és a szabványosított syntaxe cesty.

## <a name="code-sample"></a>Kódminta

Teljes minta kódja, lásd: [AccessDbProviderSample05 kódminta](./accessdbprovidersample05-code-sample.md).

## <a name="defining-object-types-and-formatting"></a>Objektumtípusok definiálása és formázása

Tagok hozzáadása a meglévő objektumok, vagy új objektumokat meghatározásához szolgáltató lehetőség. További információkért lásd:[objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).

## <a name="building-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltató létrehozása

További információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltatóban tesztelése

Ha a Windows PowerShell-szolgáltató regisztrálva van a Windows PowerShell-lel, tesztelheti a támogatott parancsmagok futtatásával a parancssorban, beleértve a Származtatás által elérhetővé tett parancsmagok. Ez a példa a minta navigáció szolgáltató teszteli.

1. Futtassa az új felületet, és a `Set-Location` -parancsmaggal beállítható jelzik az Access-adatbázis elérési útját.

   ```powershell
   Set-Location mydb:
   ```

2. Most futtassa a `Get-Childitem` az adatbázis elemeket, amelyek a rendelkezésre álló adatbázistáblák listájának beolvasásához. Minden táblához Ez a parancsmag is lekéri a tábla sorainak számát.

   ```powershell
   Get-ChildItem | Format-Table rowcount,name -AutoSize
   ```

   ```output
   RowCount   Name
   --------   ----
        180   MSysAccessObjects
          0   MSysACEs
          1   MSysCmdbars
          0   MSysIMEXColumns
          0   MSysIMEXSpecs
          0   MSysObjects
          0   MSysQueries
          7   MSysRelationships
          8   Categories
         91   Customers
          9   Employees
       2155   Order Details
        830   Orders
         77   Products
          3   Shippers
         29   Suppliers
   ```

3. Használja a `Set-Location` újra-parancsmaggal beállítható az alkalmazottak adattábla helyét.

   ```powershell
   Set-Location Employees
   ```

4. Használjuk a `Get-Location` elérési útját az Employees tábla beolvasásához.

   ```powershell
   Get-Location
   ```

   ```output
   Path
   ----
   mydb:\Employees
   ```

5. Mostantól használhatja a `Get-Childitem` parancsmag olyan parancsoknak, a `Format-Table` parancsmagot. A parancsmagok készletét az alkalmazottak adattábla a elemei, amelyek a tábla sorait olvassa be. Formázási által meghatározott a `Format-Table` parancsmagot.

   ```powershell
   Get-ChildItem | Format-Table rownumber,psiscontainer,data -AutoSize
   ```

   ```output
   RowNumber   PSIsContainer   Data
   ---------   --------------   ----
   0           False            System.Data.DataRow
   1           False            System.Data.DataRow
   2           False            System.Data.DataRow
   3           False            System.Data.DataRow
   4           False            System.Data.DataRow
   5           False            System.Data.DataRow
   6           False            System.Data.DataRow
   7           False            System.Data.DataRow
   8           False            System.Data.DataRow
   ```

6. Most már futtathatja az `Get-Item` az alkalmazottak adattábla 0 sorára elemek beolvasásához.

   ```powershell
   Get-Item 0
   ```

   ```output
   PSPath        : AccessDB::C:\PS\Northwind.mdb\Employees\0
   PSParentPath  : AccessDB::C:\PS\Northwind.mdb\Employees
   PSChildName   : 0
   PSDrive       : mydb
   PSProvider    : System.Management.Automation.ProviderInfo
   PSIsContainer : False
   Data           : System.Data.DataRow
   RowNumber      : 0
   ```

7. Használja a `Get-Item` parancsmag újbóli sor 0 elemeinek az alkalmazotti adatokat.

   ```powershell
   (Get-Item 0).data
   ```

   ```output
   EmployeeID      : 1
   LastName        : Davis
   FirstName       : Sara
   Title           : Sales Representative
   TitleOfCourtesy : Ms.
   BirthDate       : 12/8/1968 12:00:00 AM
   HireDate        : 5/1/1992 12:00:00 AM
   Address         : 4567 Main Street
                     Apt. 2A
   City            : Buffalo
   Region          : NY
   PostalCode      : 98052
   Country         : USA
   HomePhone       : (206) 555-9857
   Extension       : 5467
   Photo           : EmpID1.bmp
   Notes           : Education includes a BA in psychology from
                     Colorado State University. She also completed "The
                     Art of the Cold Call."  Nancy is a member of
                     Toastmasters International.
   ReportsTo       : 2
   ```

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-szolgáltató létrehozása](./how-to-create-a-windows-powershell-provider.md)

[Terv a Windows PowerShell-szolgáltató](./designing-your-windows-powershell-provider.md)

[Objektumtípusok kiterjesztése és formázása](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[Egy tároló Windows PowerShell-szolgáltatóban megvalósítása](./creating-a-windows-powershell-container-provider.md)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)