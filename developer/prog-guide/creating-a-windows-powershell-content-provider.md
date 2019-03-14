---
title: Egy Windows PowerShell-tartalmat szolgáltató létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- content providers [PowerShell Programmer's Guide]
- providers [PowerShell Programmer's Guide], content provider
ms.assetid: 3da88ff9-c4c7-4ace-aa24-0a29c8cfa060
caps.latest.revision: 6
ms.openlocfilehash: 1bccbfab55f4ba4476678b130bd9db91eed7df80
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57795317"
---
# <a name="creating-a-windows-powershell-content-provider"></a>Windows PowerShelles tartalomszolgáltató létrehozása

Ez a témakör ismerteti, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, amely lehetővé teszi a felhasználó a adattárban lévő elemek tartalmának módosítására. Ennek következményeképpen is módosíthatja az elemek tartalma szolgáltató nevezzük Windows PowerShell a tartalomszolgáltatón.

> [!NOTE]
> Letöltheti a C# forrásfájl (AccessDBSampleProvider06.cs) a szolgáltató a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
>
> A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.
>
> Más Windows PowerShell-szolgáltató esetében kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).

Az alábbi lista tartalmazza az ebben a témakörben szakaszokban. Ha nem ismeri a Windows PowerShell-tartalom szolgáltató írása, olvassa el az ezekben a szakaszokban a sorrendben jelennek meg. Azonban ha ismeri, a Windows PowerShell a tartalomszolgáltatón írása, folytassa a szükséges információkat.

- [A Windows PowerShell-tartalmat szolgáltató osztály meghatározása](#Define-the-Windows-PowerShell-Content-Provider-Class)

- [Alapfunkciók meghatározása](#Define-Functionality-of-Base-Class)

- [A tartalom olvasó megvalósítása](#Implementing-a-Content-Reader)

- [A tartalom író megvalósítása](#Implementing-a-Content-Writer)

- [A tartalom olvasó beolvasása](#Retrieving-the-Content-Reader)

- [Dinamikus paraméterek csatolása a `Get-Content` parancsmag](#Attaching-Dynamic-Parameters-to-the-Get-Content-Cmdlet)

- [A tartalom író beolvasása](#Retrieving-the-Content-Writer)

- [Dinamikus paraméterek csatolása a Add_Content és `Set-Content` parancsmagok](#Attaching-Dynamic-Parameters-to-the-Add-Content-and-Set-Content-Cmdlets)

- [Tartalom törlése](#Clearing-Content)

- [Dinamikus paraméterek csatolása a `Clear-Content` parancsmag](#Attaching-Dynamic-Parameters-to-the-Clear-Content-Cmdlet)

- [Kódminta](#Code-Sample)

- [Objektumtípusok definiálása és formázása](#defining-object-types-and-formatting)

- [A Windows PowerShell-szolgáltató létrehozása](#Building-the-Windows-PowerShell-Provider)

- [A Windows PowerShell-szolgáltatóban tesztelése](#Testing-the-Windows-PowerShell-Provider)

## <a name="define-the-windows-powershell-content-provider-class"></a>Adja meg a Windows PowerShell-tartalmat szolgáltató osztálya

Windows PowerShell a tartalomszolgáltatón létre kell hoznia egy .NET-osztály, amely támogatja a [System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) felületet. Itt látható az ebben a szakaszban leírt elem szolgáltató osztály definícióját.

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L32-L33 "AccessDBProviderSample06.cs")]

Vegye figyelembe, hogy ez az osztály definícióját, a [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribútum tartalmazza a két paramétert. Az első paraméter adja meg a Windows PowerShell által használt szolgáltató felhasználóbarát nevét. A második paraméter adja meg a Windows PowerShell adott képességeket, amelyek a szolgáltató tesz elérhetővé a Windows PowerShell-modul a parancs feldolgozása közben. A szolgáltató nem hozzáadott meghatározott Windows PowerShell-képességekre van.

## <a name="define-functionality-of-base-class"></a>Alaposztály funkciójának definiálása

Leírtak szerint [terv a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md), a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) más osztályok megadott származik különböző szolgáltatói funkciót. Windows PowerShell a tartalomszolgáltatón, ezért általában határozza meg az összes az adott osztályok által biztosított funkciókat.

Munkamenet-specifikus inicializálási információk hozzáadása és a szolgáltató által használt erőforrások felszabadítása funkciók megvalósítása kapcsolatos további információkért lásd: [alapvető Windows PowerShell-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md). Azonban a legtöbb szolgáltatók, beleértve a szolgáltató, az itt leírtak szerint használhatja ezt a funkciót, amely a Windows PowerShell által biztosított alapértelmezett megvalósítása.

Az adattár eléréséhez, a szolgáltatónak tartalmaznia kell a módszereket a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) alaposztály. Ezek a metódusok megvalósításával kapcsolatos további információkért lásd: [egy Windows PowerShell-meghajtó szolgáltató létrehozása](./creating-a-windows-powershell-drive-provider.md).

Egy adattár, például az első, a beállítás és a elszámolási elemek, a cikkek módosítására a szolgáltató által biztosított metódusokkal meg kell valósítania az [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) alaposztály. Ezek a metódusok megvalósításával kapcsolatos további információkért lásd: [egy Windows PowerShell elem szolgáltató létrehozása](./creating-a-windows-powershell-item-provider.md).

Többrétegű adattárak működjön, a szolgáltató által biztosított metódusokkal meg kell valósítania az [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) alaposztály. Ezek a metódusok megvalósításával kapcsolatos további információkért lásd: [létrehozása a Windows PowerShell-tároló szolgáltató](./creating-a-windows-powershell-container-provider.md).

A rekurzív parancsok, a beágyazott tárolók és a relatív elérési utakat, a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) alaposztály. Emellett a Windows PowerShell tartalomszolgáltató is a rendeli [System.Management.Automation.Provider.Icontentcmdletprovider](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider) a csatoló a [ System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) alaposztály, és ezért meg kell valósítania az adott osztály által biztosított metódusokkal. További információkért tekintse meg a végrehajtási azokat a módszereket, lásd: [navigációs Windows PowerShell-szolgáltatóban megvalósítása](./creating-a-windows-powershell-navigation-provider.md).

## <a name="implementing-a-content-reader"></a>A tartalom olvasó megvalósítása

Egy elem lévő tartalmak olvasását, hogy a szolgáltató megvalósítja kell származó tartalom olvasó osztály [System.Management.Automation.Provider.Icontentreader](/dotnet/api/System.Management.Automation.Provider.IContentReader). A tartalom olvasó a szolgáltatóhoz tartozó adattábla lehetővé teszi a tartalmát egy sort a hozzáférést. A tartalom olvasó osztály egy **olvasási** metódus lekéri az adatokat a megadott sort a és a egy listát ad vissza az adatokat, amely egy **pozicionálási** metódushoz, amely a tartalom olvasó áthelyezi egy  **Bezárás** metódushoz, amely lezárja a tartalom olvasó és a egy **Dispose** metódus.

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L2115-L2241 "AccessDBProviderSample06.cs")]

## <a name="implementing-a-content-writer"></a>A tartalom író megvalósítása

Tartalom írni egy elemet, a szolgáltatónak tartalmaznia kell egy tartalom író származik- [System.Management.Automation.Provider.Icontentwriter](/dotnet/api/System.Management.Automation.Provider.IContentWriter). A tartalom író osztály egy **írási** metódushoz, amely a megadott sor tartalmat ír egy **pozicionálási** metódushoz, amely a tartalom író áthelyezi egy **Bezárás** metódushoz, amely lezárja a tartalom írta, és a egy **Dispose** metódust.

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L2250-L2394 "AccessDBProviderSample06.cs")]

## <a name="retrieving-the-content-reader"></a>A tartalom olvasó beolvasása

Egyikből tartalmakat beolvasni egy konfigurációelemet, a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) támogatásához a `Get-Content` parancsmagot. Ez a módszer az elem található a megadott elérési úton az content olvasó adja vissza. Az Adatolvasó objektum majd a tartalom elolvasására nyitható meg.

Íme a végrehajtásának [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) ezt a módszert a szolgáltató.

```csharp
public IContentReader GetContentReader(string path)
{
    string tableName;
    int rowNumber;

    PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

    if (type == PathType.Invalid)
    {
        ThrowTerminatingInvalidPathException(path);
    }
    else if (type == PathType.Row)
    {
        throw new InvalidOperationException("contents can be obtained only for tables");
    }

    return new AccessDBContentReader(path, this);
} // GetContentReader
```

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1829-L1846 "AccessDBProviderSample06.cs")]

#### <a name="things-to-remember-about-implementing-getcontentreader"></a>Megjegyzendő GetContentReader megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader):

- A szolgáltató osztálya meghatározásakor Windows PowerShell a tartalomszolgáltatón a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreader*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReader) metódus biztosítania kell, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott követelményeinek képességek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását nem kell lekérni, kivéve, ha a felhasználó elől rejtett objektumok egy olvasót a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Hiba történt kell írni, ha az elérési utat jelöl egy elemet a felhasználó elől elrejtett és [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) értékre van állítva `false`.

## <a name="attaching-dynamic-parameters-to-the-get-content-cmdlet"></a>A Get-tartalom parancsmag dinamikus paraméterek csatolása

A `Get-Content` parancsmag szükség lehet további paramétereket, amelyeket dinamikusan futásidőben. Ahhoz, hogy ezek a dinamikus paraméterek, a Windows PowerShell tartalomszolgáltató meg kell valósítani a [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentreaderdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentReaderDynamicParameters) metódust. Ez a módszer lekéri az elem elérési útja a jelzett dinamikus paraméterek és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [ System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a parancsmaghoz.

A Windows PowerShell-tároló szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

```csharp
public object GetContentReaderDynamicParameters(string path)
{
    return null;
}
```

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1853-L1856 "AccessDBProviderSample06.cs")]

## <a name="retrieving-the-content-writer"></a>A tartalom író beolvasása

Tartalom írni egy elemet, a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) támogatásához a `Set-Content` és `Add-Content` parancsmagok. Ez a módszer az elem található a megadott elérési úton az content író adja vissza.

Íme a végrehajtásának [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) ezt a módszert.

```csharp
public IContentWriter GetContentWriter(string path)
{
    string tableName;
    int rowNumber;

    PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

    if (type == PathType.Invalid)
    {
        ThrowTerminatingInvalidPathException(path);
    }
    else if (type == PathType.Row)
    {
        throw new InvalidOperationException("contents can be added only to tables");
    }

    return new AccessDBContentWriter(path, this);
}
```

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1863-L1880 "AccessDBProviderSample06.cs")]

#### <a name="things-to-remember-about-implementing-getcontentwriter"></a>Megjegyzendő GetContentWriter megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter):

- A szolgáltató osztálya meghatározásakor Windows PowerShell a tartalomszolgáltatón a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriter*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriter) metódus biztosítania kell, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott követelményeinek képességek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását nem kell lekérni, kivéve, ha a felhasználó elől rejtett objektumok egy író a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Hiba történt kell írni, ha az elérési utat jelöl egy elemet a felhasználó elől elrejtett és [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) értékre van állítva `false`.

## <a name="attaching-dynamic-parameters-to-the-add-content-and-set-content-cmdlets"></a>Dinamikus paraméterek csatolása a tartalom hozzáadása és a Set-tartalom-parancsmagok

A `Add-Content` és `Set-Content` parancsmagok szükség lehet további dinamikus paraméterek, a hozzáadott egy modult. Ahhoz, hogy ezek a dinamikus paraméterek, a Windows PowerShell tartalomszolgáltató meg kell valósítani a [System.Management.Automation.Provider.Icontentcmdletprovider.Getcontentwriterdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.GetContentWriterDynamicParameters) ezek metódust a paraméterek. Ez a módszer lekéri az elem elérési útja a jelzett dinamikus paraméterek és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [ System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a parancsmagokhoz.

A Windows PowerShell-tároló szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1887-L1890 "AccessDBProviderSample06.cs")]

## <a name="clearing-content"></a>Tartalom törlése

A tartalomszolgáltató valósítja meg a [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) módszert támogatja, a `Clear-Content` parancsmagot. Ez a módszer eltávolítja a megadott elérési úton a cikk tartalma, nem érinti a cikk.

Itt van a megvalósítása a [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) metódust a szolgáltató.

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1775-L1812 "AccessDBProviderSample06.cs")]

#### <a name="things-to-remember-about-implementing-clearcontent"></a>Megjegyzendő ClearContent megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent):

- A szolgáltató osztálya meghatározásakor Windows PowerShell a tartalomszolgáltatón a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities)enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) metódus biztosítania kell, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott követelményeinek képességek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását kell szünteti meg, kivéve, ha a felhasználó elől rejtett objektumok tartalmát a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Hiba történt kell írni, ha az elérési utat jelöl egy elemet a felhasználó elől elrejtett és [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) értékre van állítva `false`.

- A megvalósítását az [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) metódus meg kell hívnia [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess* ](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) , és ellenőrizze a visszaadott érték az adattár változtatások előtt. Ez a módszer segítségével amikor módosításakor az adattárolóhoz, például a tartalmak törlésével, győződjön meg arról, hogy egy művelet végrehajtását. A [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) metódus küld a felhasználónak, a Windows PowerShell-futtatókörnyezetben kezelése parancssori beállítást vagy preferencia szerint módosítani az erőforrás neve változók meghatározása, mi megjelenjenek.

  Hívása után [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) adja vissza `true`, a [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontent* ](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContent) metódus meg kell hívnia a [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) metódust. Ez a módszer egy üzenetet küld a felhasználó számára lehetővé teszi a visszajelzés ellenőrizheti, ha a művelet folytatni kell. A hívás [System.Management.Automation.Provider.Cmdletprovider.Shouldcontinue*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) lehetővé teszi, hogy egy potenciálisan veszélyes rendszermódosítások további keresése.

## <a name="attaching-dynamic-parameters-to-the-clear-content-cmdlet"></a>Dinamikus paraméterek csatolása a Clear-tartalom parancsmaghoz

A `Clear-Content` parancsmag szükség lehet további dinamikus paraméterek, a hozzáadott futásidőben. Ahhoz, hogy ezek a dinamikus paraméterek, a Windows PowerShell tartalomszolgáltató meg kell valósítani a [System.Management.Automation.Provider.Icontentcmdletprovider.Clearcontentdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IContentCmdletProvider.ClearContentDynamicParameters) ezek metódust a paraméterek. Ez a módszer a paramétereket, az elem elérési útja a jelzett kérdezi le. Ez a módszer lekéri az elem elérési útja a jelzett dinamikus paraméterek és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [ System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a parancsmaghoz.

A Windows PowerShell-tároló szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

```csharp
public object ClearContentDynamicParameters(string path)
{
    return null;
}
```

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L1819-L1822 "AccessDBProviderSample06.cs")]

## <a name="code-sample"></a>Kódminta

Teljes minta kódja, lásd: [AccessDbProviderSample06 kódminta](./accessdbprovidersample06-code-sample.md).

## <a name="defining-object-types-and-formatting"></a>Objektumtípusok definiálása és formázása

A szolgáltató írásakor tagok hozzáadása a meglévő objektumok vagy új objektumokat megadása szükség lehet. Ha ezzel végzett, létre kell hoznia egy típusok fájlt, amely a Windows PowerShell használatával azonosíthatja az objektum tagjait, és a egy formátumfájlt, amely meghatározza, hogyan jelenjen meg az objektum. További információkért lásd: [objektumtípusok kiterjesztése és formázás](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).

## <a name="building-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltató létrehozása

Lásd: [parancsmagok,-szolgáltatók regisztrálása és alkalmazások üzemeltetése](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltatóban tesztelése

Ha a Windows PowerShell-szolgáltató regisztrálva van a Windows PowerShell-lel, tesztelheti a támogatott parancsmagok futtatásával a parancssorban. Például tesztelje a minta a tartalomszolgáltatón.

Használja a `Get-Content` az adatbázistáblában által megadott elérési útja a megadott elem tartalmának beolvasásához a `Path` paraméter. A `ReadCount` paraméter adja meg a meghatározott tartalom olvasó olvasható (alapértelmezés: 1) elemek száma. A parancsmag a következő parancs bejegyzés (elem) két sor beolvasása a táblából, és megjeleníti azok tartalmát. Vegye figyelembe, hogy az alábbi példa kimenetében használja-e egy fiktív Access-adatbázis.

```powershell
Get-Content -Path mydb:\Customers -ReadCount 2
```

```output
ID        : 1
FirstName : Eric
LastName  : Gruber
Email     : ericgruber@fabrikam.com
Title     : President
Company   : Fabrikam
WorkPhone : (425) 555-0100
Address   : 4567 Main Street
City      : Buffalo
State     : NY
Zip       : 98052
Country   : USA
ID        : 2
FirstName : Eva
LastName  : Corets
Email     : evacorets@cohowinery.com
Title     : Sales Representative
Company   : Coho Winery
WorkPhone : (360) 555-0100
Address   : 8910 Main Street
City      : Cabmerlot
State     : WA
Zip       : 98089
Country   : USA
```

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-szolgáltató létrehozása](./how-to-create-a-windows-powershell-provider.md)

[Terv a Windows PowerShell-szolgáltató](./designing-your-windows-powershell-provider.md)

[Objektumtípusok kiterjesztése és formázása](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[A navigációs Windows PowerShell-szolgáltatóban megvalósítása](./creating-a-windows-powershell-navigation-provider.md)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell SDK](../windows-powershell-reference.md)

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)
