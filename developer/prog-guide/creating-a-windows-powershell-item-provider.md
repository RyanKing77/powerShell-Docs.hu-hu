---
title: A Windows PowerShell elem szolgáltató létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- item providers [PowerShell Programmer's Guide]
- providers [PowerShell Programmer's Guide], item provider
ms.assetid: a5a304ce-fc99-4a5b-a779-de7d85e031fe
caps.latest.revision: 6
ms.openlocfilehash: f2c9e10f0dc392399cf062500b7f28b3d1c07f6e
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055121"
---
# <a name="creating-a-windows-powershell-item-provider"></a>Windows PowerShelles elemszolgáltató létrehozása

Ez a témakör ismerteti, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, amely a tárolóban lévő adatok is módosíthatja. Ebben a témakörben a tárolóban lévő adatok elemeinek neve, az "elem" az adatok tárolására. Ennek következményeképpen is módosíthatja a tárolóban lévő adatok szolgáltató nevezzük egy Windows PowerShell-elem szolgáltató.

> [!NOTE]
> Letöltheti a C# forrásfájl (AccessDBSampleProvider03.cs) a szolgáltató a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
>
> A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.
>
> Más Windows PowerShell-szolgáltató esetében kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).

A jelen témakörben ismertetett Windows PowerShell elem szolgáltató adatokat olvas be az Access-adatbázisok. Ebben az esetben a "elem" vagy a hozzáférés-adatbázisban lévő táblából vagy egy adatbázistábla.

Az alábbi lista tartalmazza az ebben a témakörben szakaszokban. Ha nem ismeri a Windows PowerShell-elem szolgáltató írása, olvassa el az ezekben a szakaszokban a sorrendben jelennek meg. Azonban ha ismeri a Windows PowerShell-elem szolgáltató írása, folytassa a szükséges információkat:

- [A Windows PowerShell elem szolgáltató osztály meghatározása](#Defining-the-Windows-PowerShell-Item-Provider-Class)

- [Alapfunkciók meghatározása](#Defining-Base-Functionality)

- [Elérési út érvényességének ellenőrzése](#Checking-for-Path-Validity)

- [Ha létezik egy elem meghatározása](#Determining-if-an-Item-Exists)

- [Dinamikus paraméterek csatolása a `Test-Path` parancsmag](#Attaching-Dynamic-Parameters-to-the-Test-Path-Cmdlet)

- [Egy elem beolvasása](#Retrieving-an-Item)

- [Dinamikus paraméterek csatolása a `Get-Item` parancsmag](#Attaching-Dynamic-Parameters-to-the-Get-Item-Cmdlet)

- [Egy elem beállítása](#Setting-an-Item)

- [Dinamikus paraméterek csatolása a `Set-Item` parancsmag](#Retrieving-Dynamic-Parameters-for-SetItem)

- [Egy elem törlése](#Clearing-an-Item)

- [Dinamikus paraméterek csatolása a Clear-cikk parancsmaghoz](#Retrieve-Dynamic-Parameters-for-ClearItem)

- [Alapértelmezett művelet végrehajtása egy elem](#Performing-a-Default-Action-for-an-Item)

- [Dinamikus paraméterek InvokeDefaultAction beolvasása](#Retrieve-Dynamic-Parameters-for-InvokeDefaultAction)

- [Végrehajtási Segédmetódusokat és -osztályok](#Implementing-Helper-Methods-and-Classes)

- [Kódminta](#Code-Sample)

- [Objektumtípusok definiálása és formázása](#Defining-Object-Types-and-Formatting)

- [A Windows PowerShell-szolgáltató létrehozása](#Building-the-Windows-PowerShell-provider)

- [A Windows PowerShell-szolgáltatóban tesztelése](#Testing-the-Windows-PowerShell-provider)

## <a name="defining-the-windows-powershell-item-provider-class"></a>A Windows PowerShell elem szolgáltató osztály meghatározása

A Windows PowerShell-elem szolgáltató definiálnia kell egy .NET-osztályt, amely az a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) alaposztály. A jelen szakaszban bemutatott elem szolgáltató osztály definícióját a következő:

[!code-csharp[AccessDBProviderSample03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample03/AccessDBProviderSample03.cs#L34-L36 "AccessDBProviderSample03.cs")]

Vegye figyelembe, hogy ez az osztály definícióját, a [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribútum tartalmazza a két paramétert. Az első paraméter adja meg a Windows PowerShell által használt szolgáltató felhasználóbarát nevét. A második paraméter adja meg a Windows PowerShell adott képességeket, amelyek a szolgáltató tesz elérhetővé a Windows PowerShell-modul a parancs feldolgozása közben. A szolgáltató nem hozzáadott meghatározott Windows PowerShell-képességekre van.

## <a name="defining-base-functionality"></a>Alapfunkciók meghatározása

Leírtak szerint [terv a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md), a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) más osztályok megadott különböző származik szolgáltatói funkciót. A Windows PowerShell-elem szolgáltató, ezért meg kell határoznia az összes az adott osztályok által biztosított funkciókat.

Munkamenet-specifikus inicializálási információk hozzáadása és a szolgáltató által használt erőforrások felszabadítása funkciók megvalósítása kapcsolatos további információkért lásd: [alapvető Windows PowerShell-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md). Azonban a legtöbb szolgáltatók, beleértve a szolgáltató, az itt leírtak szerint használhatja ezt a funkciót, amely a Windows PowerShell által biztosított alapértelmezett megvalósítása.

A Windows PowerShell-elem szolgáltató is módosíthatja a tárolóban lévő elemek, mielőtt azt módszereket is meg kell valósítani a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) alaposztály elérni az adattárhoz. Ez az osztály megvalósításával kapcsolatos további információkért lásd: [egy Windows PowerShell-meghajtó szolgáltató létrehozása](./creating-a-windows-powershell-drive-provider.md).

## <a name="checking-for-path-validity"></a>Elérési út érvényességének ellenőrzése

Az adatok egy elem keresésekor a Windows PowerShell-modul bizonyítékot szolgáltat a szolgáltató egy Windows PowerShell elérési útja "PSPath fogalmak" szakaszában meghatározott [Windows PowerShell működése](http://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58). Egy Windows PowerShell-elem szolgáltatót kell ellenőrizni a szintaktikai és Szemantikus végrehajtási által átadott bármilyen útvonalat a [System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) metódust. A metódus visszatérése `true` elérési út érvényes, és `false` más módon. Vegye figyelembe, hogy ez a metódus végrehajtása nem ellenőrizze az elérési út szintaktikailag az elem elérési úton, de csak létezik-e és szemantikailag helyes-e lennie.

Itt van a megvalósítása a [System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) metódust a szolgáltató. Vegye figyelembe, hogy ez a megvalósítás meghív egy NormalizePath segédmetódus minden elválasztó az elérési út átalakítása egy egységes.

[!code-csharp[AccessDBProviderSample03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample03/AccessDBProviderSample03.cs#L274-L298 "AccessDBProviderSample03.cs")]

## <a name="determining-if-an-item-exists"></a>Ha létezik egy elem meghatározása

Ellenőrizte, hogy az elérési utat, a Windows PowerShell-modul döntse el, ha létezik-e egy elem, az adatok adott elérési úton. Ilyen típusú lekérdezések támogatásához, a Windows PowerShell-elem szolgáltató valósítja meg a [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) metódust. A metódus visszatérése `true` egy elemet a megadott elérési úton található, és `false` (alapértelmezett) ellenkező esetben.

Itt van a megvalósítása a [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) metódust a szolgáltató. Vegye figyelembe, hogy ez a metódus meghívja a PathIsDrive ChunkPath és GetTable segédmetódusokat, és a egy szolgáltató definiált DatabaseTableInfo objektum.

[!code-csharp[AccessDBProviderSample03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample03/AccessDBProviderSample03.cs#L229-L267 "AccessDBProviderSample03.cs")]

#### <a name="things-to-remember-about-implementing-itemexists"></a>Megjegyzendő ItemExists megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-elem szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) metódus biztosítania kell, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott képességeket. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Ez a metódus végrehajtásának kezelje a elemet, előfordulhat, hogy az elem láthatóvá tegye a felhasználó számára a hozzáférést minden olyan formájában. Például ha egy felhasználónak írási hozzáférése van egy fájlba a fájlrendszer-szolgáltatót (a Windows PowerShell által biztosított), de nem olvasási hozzáférés keresztül, a fájl még létezik és [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) adja vissza `true`. Az implementációs megtekintheti, ha az alárendelt elem számba vehetők egy szülő elem ellenőrzése.

## <a name="attaching-dynamic-parameters-to-the-test-path-cmdlet"></a>A Test-Path parancsmag dinamikus paraméterek csatolása

Egyes esetekben a `Test-Path` parancsmag, amely meghívja ezt [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) van szükség a további paramétereket, amelyeket dinamikusan futásidőben. Ezek a dinamikus paraméterek a Windows PowerShell elem a szolgáltatónak tartalmaznia kell adnia a [System.Management.Automation.Provider.Itemcmdletprovider.Itemexistsdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExistsDynamicParameters) metódust. Ez a módszer lekéri a dinamikus paraméterek az elem elérési útja a jelzett és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [ System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a `Test-Path` parancsmagot.

A Windows PowerShell-elem szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovideritemexistdynamicparameters](Msh_samplestestcmdlets#testprovideritemexistdynamicparameters)]  -->

## <a name="retrieving-an-item"></a>Egy elem beolvasása

Lekérdezni egy elemet, a Windows PowerShell-elem szolgáltató felül kell írnia [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) metódus támogatja a hívást a `Get-Item` parancsmagot. Ez a módszer az elem használatával írja a [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject) metódust.

Itt van a megvalósítása a [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) metódust a szolgáltató. Vegye figyelembe, hogy ezt a módszert használja-e a GetTable és GetRow segédmetódusokat elemek, amelyek az Access-adatbázis, vagy egy adatok soraihoz lekéréséhez.

[!code-csharp[AccessDBProviderSample03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample03/AccessDBProviderSample03.cs#L132-L163 "AccessDBProviderSample03.cs")]

#### <a name="things-to-remember-about-implementing-getitem"></a>Megjegyzendő GetItem megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-elem szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)enumerálása. Ezekben az esetekben végrehajtásának [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) biztosítania kell, hogy az elérési utat, a metódusnak átadott megfelel ezeknek a követelményeknek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását nem kell lekérni objektumok, amelyek általában a felhasználó elől rejtve vannak, kivéve, ha a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Például a [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) módszer a fájlrendszer szolgáltató ellenőrzi a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonság, mielőtt megpróbálja meghívni [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject) a rejtett vagy a rendszerfájlokat.

## <a name="attaching-dynamic-parameters-to-the-get-item-cmdlet"></a>A Get-Item parancsmag dinamikus paraméterek csatolása

Egyes esetekben a `Get-Item` parancsmaghoz szükséges további paramétereket, amelyeket dinamikusan futásidőben. Ezek a dinamikus paraméterek a Windows PowerShell elem a szolgáltatónak tartalmaznia kell adnia a [System.Management.Automation.Provider.Itemcmdletprovider.Getitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItemDynamicParameters) metódust. Ez a módszer lekéri a dinamikus paraméterek az elem elérési útja a jelzett és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [ System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a `Get-Item` parancsmagot.

Ez a szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidergetitemdynamicparameters](Msh_samplestestcmdlets#testprovidergetitemdynamicparameters)]  -->

## <a name="setting-an-item"></a>Egy elem beállítása

Egy elem beállítása, a Windows PowerShell-elem szolgáltató felül kell írnia a [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) metódus támogatja a hívást a `Set-Item` parancsmagot. Ez a módszer az elem értékét állítja be a megadott elérési úton.

Ez a szolgáltató nem biztosít egy felülbírálást a [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) metódust. Azonban a következő: Ez a módszer alapértelmezett megvalósítása

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidersetitem](Msh_samplestestcmdlets#testprovidersetitem)]  -->

#### <a name="things-to-remember-about-implementing-setitem"></a>Megjegyzendő SetItem megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-elem szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)enumerálása. Ezekben az esetekben végrehajtásának [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) biztosítania kell, hogy az elérési utat, a metódusnak átadott megfelel ezeknek a követelményeknek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását ne állítsa be és írhat, kivéve, ha a felhasználó elől rejtett objektumok a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Kell küldeni a hiba a [System.Management.Automation.Provider.Cmdletprovider.WriteError](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteError) módszert, ha az elérési utat jelöl egy rejtett elemet és [ System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) értékre van állítva `false`.

- A megvalósítását az [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) metódus meg kell hívnia [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess), és ellenőrizze a visszaadott érték az adattár változtatások előtt. Ez a módszer segítségével amikor módosításakor az adattárolóhoz, például fájlokat törli, győződjön meg arról, hogy egy művelet végrehajtását. A [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) metódus küld a felhasználónak, a Windows PowerShell-futtatókörnyezetben, figyelembe véve a parancssori beállításokat módosítani az erőforrás nevét, vagy a preferenciaváltozók meghatározásához, mit üzenetnek kell megjelennie.

  Hívása után [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) adja vissza `true`, a [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem)metódus meg kell hívnia a [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) metódust. Ez a módszer egy üzenetet küld a felhasználó számára lehetővé teszi a visszajelzés ellenőrizheti, ha a művelet folytatni kell. A hívás [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) lehetővé teszi, hogy egy potenciálisan veszélyes rendszermódosítások további keresése.

## <a name="retrieving-dynamic-parameters-for-setitem"></a>Dinamikus paraméterek SetItem beolvasása

Egyes esetekben a `Set-Item` parancsmaghoz szükséges további paramétereket, amelyeket dinamikusan futásidőben. Ezek a dinamikus paraméterek a Windows PowerShell elem a szolgáltatónak tartalmaznia kell adnia a [System.Management.Automation.Provider.Itemcmdletprovider.Setitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItemDynamicParameters) metódust. Ez a módszer lekéri a dinamikus paraméterek az elem elérési útja a jelzett és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [ System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a `Set-Item` parancsmagot.

Ez a szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidersetitemdynamicparameters](Msh_samplestestcmdlets#testprovidersetitemdynamicparameters)]  -->

## <a name="clearing-an-item"></a>Egy elem törlése

Ha törölni szeretne egy elemet, a Windows PowerShell-elem szolgáltató valósítja meg a [System.Management.Automation.Provider.Itemcmdletprovider.Clearitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItem) metódus támogatja a hívást a `Clear-Item` parancsmagot. Ez a módszer törli az elem a megadott elérési úton.

Ez a szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderclearitem](Msh_samplestestcmdlets#testproviderclearitem)]  -->

#### <a name="things-to-remember-about-implementing-clearitem"></a>Megjegyzendő ClearItem megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Itemcmdletprovider.Clearitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItem):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-elem szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)enumerálása. Ezekben az esetekben végrehajtásának [System.Management.Automation.Provider.Itemcmdletprovider.Clearitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItem) biztosítania kell, hogy az elérési utat, a metódusnak átadott megfelel ezeknek a követelményeknek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását ne állítsa be és írhat, kivéve, ha a felhasználó elől rejtett objektumok a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Küldjön el egy hiba történt a [System.Management.Automation.Provider.Cmdletprovider.WriteError](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteError) módszert, ha az elérési utat jelöl egy elemet a felhasználó elől elrejtett és [ System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) értékre van állítva `false`.

- A megvalósítását az [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) metódus meg kell hívnia [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess), és ellenőrizze a visszaadott érték az adattár változtatások előtt. Ez a módszer segítségével amikor módosításakor az adattárolóhoz, például fájlokat törli, győződjön meg arról, hogy egy művelet végrehajtását. A [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) metódus küld a felhasználónak, a Windows PowerShell-modul módosítható, és a parancssori beállítást vagy preferencia szerint kezelésére az erőforrás neve változók meghatározása, mi megjelenjenek.

  Hívása után [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) adja vissza `true`, a [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem)metódus meg kell hívnia a [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) metódust. Ez a módszer egy üzenetet küld a felhasználó számára lehetővé teszi a visszajelzés ellenőrizheti, ha a művelet folytatni kell. A hívás [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) lehetővé teszi, hogy egy potenciálisan veszélyes rendszermódosítások további keresése.

## <a name="retrieve-dynamic-parameters-for-clearitem"></a>Dinamikus paraméterek lekérése a ClearItem

Egyes esetekben a `Clear-Item` parancsmaghoz szükséges további paramétereket, amelyeket dinamikusan futásidőben. Ezek a dinamikus paraméterek a Windows PowerShell elem a szolgáltatónak tartalmaznia kell adnia a [System.Management.Automation.Provider.Itemcmdletprovider.Clearitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ClearItemDynamicParameters) metódust. Ez a módszer lekéri a dinamikus paraméterek az elem elérési útja a jelzett és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [ System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a `Clear-Item` parancsmagot.

Ez a cikk szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderclearitemdynamicparameters](Msh_samplestestcmdlets#testproviderclearitemdynamicparameters)]  -->

## <a name="performing-a-default-action-for-an-item"></a>Alapértelmezett művelet végrehajtása egy elem

Valósíthat meg egy Windows PowerShell-elem szolgáltató a [System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultaction*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction) metódus támogatja a hívást a `Invoke-Item` parancsmagot, amely lehetővé teszi, hogy a szolgáltató a hajtsa végre az alapértelmezett művelet a megadott elérési úton a cikkhez. Például a fájlrendszer-szolgáltatót előfordulhat, hogy ezt a módszert ShellExecute hívja az adott cikkhez.

Ez a szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderinvokedefaultaction](Msh_samplestestcmdlets#testproviderinvokedefaultaction)]  -->

#### <a name="things-to-remember-about-implementing-invokedefaultaction"></a>Megjegyzendő InvokeDefaultAction megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultaction*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-elem szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)enumerálása. Ezekben az esetekben végrehajtásának [System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultaction*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultAction) biztosítania kell, hogy az elérési utat, a metódusnak átadott megfelel ezeknek a követelményeknek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását ne állítsa be és írni, kivéve, ha a felhasználó elől rejtett objektum a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Küldjön el egy hiba történt a [System.Management.Automation.Provider.Cmdletprovider.WriteError](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteError) módszert, ha az elérési utat jelöl egy elemet a felhasználó elől elrejtett és [ System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) értékre van állítva `false`.

## <a name="retrieve-dynamic-parameters-for-invokedefaultaction"></a>Dinamikus paraméterek lekérése a InvokeDefaultAction

Egyes esetekben a `Invoke-Item` parancsmaghoz szükséges további paramétereket, amelyeket dinamikusan futásidőben. Ezek a dinamikus paraméterek a Windows PowerShell elem a szolgáltatónak tartalmaznia kell adnia a [System.Management.Automation.Provider.Itemcmdletprovider.Invokedefaultactiondynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.InvokeDefaultActionDynamicParameters) metódust. Ez a módszer lekéri a dinamikus paraméterek az elem elérési útja a jelzett és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [ System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum használja a dinamikus paraméterek hozzáadása a `Invoke-Item` parancsmagot.

Ez a cikk szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderinvokedefaultactiondynamicparameters](Msh_samplestestcmdlets#testproviderinvokedefaultactiondynamicparameters)]  -->

## <a name="implementing-helper-methods-and-classes"></a>Végrehajtási Segédmetódusokat és -osztályok

Ez a cikk szolgáltató számos valósítja meg, és a nyilvános által használt osztályok Windows PowerShell által definiált metódusok felülbírálása. A kód ezen segédmetódusokat és osztályok jelennek meg a [kódminta](#Code-Sample) szakaszban.

### <a name="normalizepath-method"></a>NormalizePath Method

Ez a cikk szolgáltató valósít meg egy NormalizePath segédmetódus, hogy az elérési út formátuma legyen-e. A megadott formátumot használja egy fordított perjel (\\) elválasztására.

### <a name="pathisdrive-method"></a>PathIsDrive metódus

Ez a cikk szolgáltató valósít meg egy PathIsDrive segédmetódus annak megállapításához, hogy a megadott elérési út ténylegesen a meghajtó nevét.

### <a name="chunkpath-method"></a>ChunkPath metódus

Ez a cikk szolgáltató valósít meg egy ChunkPath segédmetódus, amely megtöri a megadott elérési út mentése, a szolgáltató azonosíthassa az egyes elemei. Az elérési út elemekből fel egy tömböt ad vissza.

### <a name="gettable-method"></a>GetTable metódus

Ez a cikk szolgáltató valósítja meg a táblák beolvasása segédmetódus, amely egy DatabaseTableInfo hívásában megadott táblázat információkat képviselő objektumot adja vissza.

### <a name="getrow-method"></a>GetRow metódus

A [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) GetRows hívás segédmetódus metódushívások az elemet szolgáltató. A segítő metódus lekér egy DatabaseRowInfo képviselő objektum, amely a megadott sort a táblázatban kapcsolatos információkat.

### <a name="databasetableinfo-class"></a>DatabaseTableInfo osztályban

Ez a cikk szolgáltató DatabaseTableInfo osztály, amely az adatbázis-adatok a táblázatban szereplő információk gyűjteményét határozza meg. Ez az osztály hasonlít a [System.IO.Directoryinfo](/dotnet/api/System.IO.DirectoryInfo) osztály.

A minta elem szolgáltató határozza meg, hogy egy DatabaseTableInfo.GetTables metódus meghatározása a táblák az adatbázisban táblázat információkat objektumok gyűjteményét adja vissza. Ez a módszer is tartalmaz, győződjön meg arról, hogy bármely adatbázishiba megjelenik-e egy-egy sornak nulla és a egy try/catch blokkban.

### <a name="databaserowinfo-class"></a>DatabaseRowInfo osztályban

Ez a cikk szolgáltató határozza meg a DatabaseRowInfo helper osztály, amely egy sort a táblázatban az adatbázis jelöli. Ez az osztály hasonlít a [System.IO.FileInfo](/dotnet/api/System.IO.FileInfo) osztály.

A minta-szolgáltató határozza meg, hogy egy DatabaseRowInfo.GetRows metódus a megadott tábla sor információk objektumok gyűjteményét adja vissza. Ez a módszer egy try/catch blokkban, ha a kivételek tartalmazza. Hibák sor információ nem eredményez.

## <a name="code-sample"></a>Kódminta

Teljes minta kódja, lásd: [AccessDbProviderSample03 kódminta](./accessdbprovidersample03-code-sample.md).

## <a name="defining-object-types-and-formatting"></a>Objektumtípusok definiálása és formázása

A szolgáltató írásakor tagok hozzáadása a meglévő objektumok vagy új objektumokat megadása szükség lehet. Amikor végzett, hozzon létre egy típusok fájlt, amely a Windows PowerShell használatával azonosíthatja az objektum tagjait, és a egy formátumfájlt, amely meghatározza, hogyan jelenjen meg az objektum. További információ: [objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).

## <a name="building-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltató létrehozása

Lásd: [parancsmagok,-szolgáltatók regisztrálása és alkalmazások üzemeltetése](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltatóban tesztelése

A Windows PowerShell-elem szolgáltató regisztrációja esetén a Windows PowerShell-lel, csak az alapszintű teszt és a szolgáltató funkciójának meghajtó. Az adatkezelési elemek teszteléséhez is lépésekre van szükség ismertetett tároló funkció [tároló Windows PowerShell-szolgáltatóban végrehajtási](./creating-a-windows-powershell-container-provider.md).

## <a name="see-also"></a>Lásd még:

[Windows PowerShell SDK](../windows-powershell-reference.md)

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell-szolgáltató létrehozása](./how-to-create-a-windows-powershell-provider.md)

[A Windows PowerShell-szolgáltató tervezése](./designing-your-windows-powershell-provider.md)

[Objektumtípusok kiterjesztése és formázása](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[Hogyan működik a Windows PowerShell](http://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58)

[Egy tároló Windows PowerShell-szolgáltató létrehozása](./creating-a-windows-powershell-container-provider.md)

[A meghajtó Windows PowerShell-szolgáltató létrehozása](./creating-a-windows-powershell-drive-provider.md)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)