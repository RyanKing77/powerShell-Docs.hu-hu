---
title: A Windows PowerShell tároló szolgáltató létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- providers [PowerShell Programmer's Guide], container provider
- container providers [PowerShell Programmer's Guide]
ms.assetid: a7926647-0d18-45b2-967e-b31f92004bc4
caps.latest.revision: 5
ms.openlocfilehash: 9e7da13ff559e802d52df475f2a555baeeeef983
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65855185"
---
# <a name="creating-a-windows-powershell-container-provider"></a>Windows PowerShelles tárolószolgáltató létrehozása

Ez a témakör ismerteti, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, amely többrétegű adattárak dolgozhatnak. Az ilyen típusú adattárat a legfelső szintre a tároló a legfelső szintű elemeket tartalmaz, és minden további szint gyermekelemek csomópont neve. Azáltal, hogy a felhasználót, hogy ezek gyermekcsomópontokat működjön, a felhasználók beavatkozhatnak hierarchikusan keresztül az adattárban.

Több szintű adattárolók dolgozhatnak szolgáltató Windows PowerShell-tároló szolgáltatók nevezzük. Vegye figyelembe, hogy egy Windows PowerShell-tároló szolgáltató csak akkor, ha van egy tároló (nem beágyazott tárolók), a benne lévő elemek használhatók-e. Ha beágyazott tárolókat, majd meg kell valósítani egy Windows PowerShell-navigációs szolgáltató. Windows PowerShell-navigációs szolgáltató megvalósításával kapcsolatos további információkért lásd: [egy Windows PowerShell navigációs szolgáltató létrehozása](./creating-a-windows-powershell-navigation-provider.md).

> [!NOTE]
> Letöltheti a C# forrásfájl (AccessDBSampleProvider04.cs) a szolgáltató a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
>
> A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.
>
> Más Windows PowerShell-szolgáltató esetében kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).

Az itt ismertetett Windows PowerShell tároló-szolgáltató határozza meg az egyetlen tároló, a táblák és sorok definiálva a tároló elemek, az adatbázis az adatbázis.

> [!CAUTION]
> Vegye figyelembe, hogy ez a kialakítás feltételezi, hogy egy adatbázis, amely egy mező neve azonosítóval rendelkezik, és hogy a mező típusát LongInteger.

## <a name="defining-a-windows-powershell-container-provider-class"></a>A Windows PowerShell tároló szolgáltató osztálya meghatározása

A Windows PowerShell-tároló szolgáltató definiálnia kell egy .NET-osztályt, amely az a [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) alaposztály. Ez az osztály definícióját a jelen szakaszban bemutatott Windows PowerShell tároló szolgáltató.

```csharp
   [CmdletProvider("AccessDB", ProviderCapabilities.None)]
   public class AccessDBProvider : ContainerCmdletProvider
```

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L34-L35 "AccessDBProviderSample04.cs")]

Figyelje meg, hogy ez az osztály definícióját, a [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribútum tartalmazza a két paramétert. Az első paraméter adja meg a Windows PowerShell által használt szolgáltató felhasználóbarát nevét. A második paraméter adja meg a Windows PowerShell adott képességeket, amelyek a szolgáltató tesz elérhetővé a Windows PowerShell-modul a parancs feldolgozása közben. A szolgáltató nincsenek nem hozzáadott adott Windows PowerShell-képességekkel.

## <a name="defining-base-functionality"></a>Alapfunkciók meghatározása

Leírtak szerint [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md), a [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) más osztályok megadott származik különböző szolgáltatói funkciót. A Windows PowerShell-tároló szolgáltató, ezért az adott osztályok által biztosított funkciókat által definiált kell.

Munkamenet-specifikus inicializálási információk hozzáadása és a szolgáltató által használt erőforrások felszabadítása funkció megvalósítását, lásd: [alapvető Windows PowerShell-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md). A legtöbb szolgáltatók (beleértve a szolgáltató az itt leírtak szerint) is használják, ez a funkció Windows PowerShell által biztosított alapértelmezett megvalósítása.

Az adattár eléréséhez, a szolgáltatónak tartalmaznia kell a módszereket a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) alaposztály. Ezek a metódusok megvalósításával kapcsolatos további információkért lásd: [egy Windows PowerShell-meghajtó szolgáltató létrehozása](./creating-a-windows-powershell-drive-provider.md).

Egy adattár, például az első, a beállítás és a elszámolási elemek, a cikkek módosítására a szolgáltató által biztosított metódusokkal meg kell valósítania az [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) alaposztály. Ezek a metódusok megvalósításával kapcsolatos további információkért lásd: [egy Windows PowerShell elem szolgáltató létrehozása](./creating-a-windows-powershell-item-provider.md).

## <a name="retrieving-child-items"></a>Gyermek elemek beolvasása

Gyermekelem lekéréséhez a Windows PowerShell-tároló szolgáltató felül kell írnia a [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) metódus támogatja a hívást a `Get-ChildItem` parancsmagot. Ez a módszer gyermekelemek lekéri az adatokat az adattárból, és objektumként a folyamat írja őket. Ha a `recurse` a parancsmag paraméter meg van adva, a metódus lekér minden gyermek, függetlenül attól, milyen szintű vannak. Ha a `recurse` paraméter nincs megadva, a metódus lekér a gyermekek csak egyetlen szinten.

Itt van a megvalósítása a [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) metódust a szolgáltató. Figyelje meg, hogy a metódus lekér minden adatbázistáblák bejárásához, ha az elérési út azt jelzi, hogy az Access-adatbázissal, és a gyermekelemek kikeresi, hogy a táblázat sorait, ha az elérési út azt jelzi, hogy egy adattábla.

```csharp
protected override void GetChildItems(string path, bool recurse)
{
    // If path represented is a drive then the children in the path are
    // tables. Hence all tables in the drive represented will have to be
    // returned
    if (PathIsDrive(path))
    {
        foreach (DatabaseTableInfo table in GetTables())
        {
            WriteItemObject(table, path, true);

            // if the specified item exists and recurse has been set then
            // all child items within it have to be obtained as well
            if (ItemExists(path) && recurse)
            {
                GetChildItems(path + pathSeparator + table.Name, recurse);
            }
        } // foreach (DatabaseTableInfo...
    } // if (PathIsDrive...
    else
    {
        // Get the table name, row number and type of path from the
        // path specified
        string tableName;
        int rowNumber;

        PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

        if (type == PathType.Table)
        {
            // Obtain all the rows within the table
            foreach (DatabaseRowInfo row in GetRows(tableName))
            {
                WriteItemObject(row, path + pathSeparator + row.RowNumber,
                        false);
            } // foreach (DatabaseRowInfo...
        }
        else if (type == PathType.Row)
        {
            // In this case the user has directly specified a row, hence
            // just give that particular row
            DatabaseRowInfo row = GetRow(tableName, rowNumber);
            WriteItemObject(row, path + pathSeparator + row.RowNumber,
                        false);
        }
        else
        {
            // In this case, the path specified is not valid
            ThrowTerminatingInvalidPathException(path);
        }
    } // else
} // GetChildItems
```

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L311-L362 "AccessDBProviderSample04.cs")]

#### <a name="things-to-remember-about-implementing-getchilditems"></a>Megjegyzendő GetChildItems megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-tároló szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) metódus meg kell győződnie arról, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott követelményeinek képességek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Ez a metódus végrehajtásának figyelembe kell vennie hozzáférés semmilyen formáját, amelyek a cikk a felhasználó számára láthatóvá tehetik az elemre. Például ha egy felhasználónak írási hozzáférése van egy fájlba a fájlrendszer-szolgáltatót (a Windows PowerShell által biztosított), de nem olvasási hozzáférés keresztül, a fájl még létezik és [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) adja vissza `true`. A megvalósítás ellenőrzése során megtekintheti, ha a gyermek számba vehetők egy fölérendelt elemtől lehet szükség.

- Több elem írásakor a [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) metódus a hosszabb ideig is eltarthat. Megtervezheti, hogy a szolgáltató írása az elemekről a [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject) metódus egyszerre. Az ezzel a technikával a felhasználó a stream jelent az elemek.

- Megvalósítását [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) végtelen rekurzió megakadályozza, hogy ha körkörös hivatkozások és a hasonló felelős. Egy megfelelő megszakítást okozó kivétel történt a kell, hogy ilyen feltétel lépett fel.

## <a name="attaching-dynamic-parameters-to-the-get-childitem-cmdlet"></a>A Get-ChildItem parancsmag dinamikus paraméterek csatolása

Egyes esetekben a `Get-ChildItem` parancsmag, amely meghívja ezt [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) van szükség a további paramétereket, amelyeket dinamikusan futásidőben. Ahhoz, hogy ezek a dinamikus paraméterek, a Windows PowerShell tároló a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Containercmdletprovider.Getchilditemsdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItemsDynamicParameters) metódust. Ez a módszer lekéri az elem elérési útja a jelzett dinamikus paraméterek és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [ System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a `Get-ChildItem` parancsmagot.

A Windows PowerShell-tároló szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidergetchilditemsdynamicparameters](Msh_samplestestcmdlets#testprovidergetchilditemsdynamicparameters)]  -->

## <a name="retrieving-child-item-names"></a>Gyermek-elem nevének beolvasása

Gyermekelemek nevei lekéréséhez a Windows PowerShell-tároló szolgáltató felül kell írnia a [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) metódus támogatja a hívásait`Get-ChildItem`parancsmag ha annak `Name` paraméter meg van adva. Ez a módszer beolvassa a megadott elérési útja vagy az alárendelt elem nevek az összes tároló bejárásához nevei, ha a `returnAllContainers` a parancsmag paraméter meg van adva. A gyermek név a levél része egy elérési utat. Például a gyermek az elérési út c:\windows\system32\abc.dll projektneve "abc.dll". A könyvtár c:\windows\system32 gyermek név "system32".

Itt van a megvalósítása a [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) metódust a szolgáltató. Figyelje meg, hogy a metódus táblanevek beolvasása, ha a megadott elérési út jelzi az Access-adatbázis (meghajtó) és a sorok száma, ha az elérési út azt jelzi, hogy egy táblát.

```csharp
protected override void GetChildNames(string path,
                            ReturnContainers returnContainers)
{
    // If the path represented is a drive, then the child items are
    // tables. get the names of all the tables in the drive.
    if (PathIsDrive(path))
    {
        foreach (DatabaseTableInfo table in GetTables())
        {
            WriteItemObject(table.Name, path, true);
        } // foreach (DatabaseTableInfo...
    } // if (PathIsDrive...
    else
    {
        // Get type, table name and row number from path specified
        string tableName;
        int rowNumber;

        PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

        if (type == PathType.Table)
        {
            // Get all the rows in the table and then write out the
            // row numbers.
            foreach (DatabaseRowInfo row in GetRows(tableName))
            {
                WriteItemObject(row.RowNumber, path, false);
            } // foreach (DatabaseRowInfo...
        }
        else if (type == PathType.Row)
        {
            // In this case the user has directly specified a row, hence
            // just give that particular row
            DatabaseRowInfo row = GetRow(tableName, rowNumber);

            WriteItemObject(row.RowNumber, path, false);
        }
        else
        {
            ThrowTerminatingInvalidPathException(path);
        }
    } // else
} // GetChildNames
```

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L369-L411 "AccessDBProviderSample04.cs")]

#### <a name="things-to-remember-about-implementing-getchildnames"></a>Megjegyzendő GetChildNames megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-tároló szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) metódus meg kell győződnie arról, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott követelményeinek képességek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

  > [!NOTE]
  > Kivételt képez ez a szabály akkor fordul elő, amikor a `returnAllContainers` a parancsmag paraméter meg van adva. Ebben az esetben a módszert érdemes lekérni egy tárolóban, bármilyen gyermek nevet akkor is, ha nem felel meg az értékét a [System.Management.Automation.Provider.Cmdletprovider.Filter*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Filter), [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include), vagy [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását nem kell lekérni az objektumneveknek, amely általában a felhasználó elől rejtve vannak, kivéve, ha a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonság meg van adva. Ha a megadott elérési út azt jelzi, hogy egy tárolóban, a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonság nem kötelező.

- Megvalósítását [System.Management.Automation.Provider.Containercmdletprovider.Getchildnames*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNames) végtelen rekurzió megakadályozza, hogy ha körkörös hivatkozások és a hasonló felelős. Egy megfelelő megszakítást okozó kivétel történt a kell, hogy ilyen feltétel lépett fel.

## <a name="attaching-dynamic-parameters-to-the-get-childitem-cmdlet-name"></a>Dinamikus paraméterek csatolása a Get-ChildItem parancsmag (név)

Egyes esetekben a `Get-ChildItem` parancsmag (az a `Name` paraméter) van szükség a további paramétereket, amelyeket dinamikusan futásidőben. Ahhoz, hogy ezek a dinamikus paraméterek, a Windows PowerShell tároló a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Containercmdletprovider.Getchildnamesdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildNamesDynamicParameters) metódust. Ez a módszer lekéri a dinamikus paraméterek az elem elérési útja a jelzett és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [ System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a `Get-ChildItem` parancsmagot.

Ez a szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidergetchildnamesdynamicparameters](Msh_samplestestcmdlets#testprovidergetchildnamesdynamicparameters)]  -->

## <a name="renaming-items"></a>Cikkek átnevezése

Egy elem átnevezése, egy Windows PowerShell-tároló szolgáltató felül kell írnia a [System.Management.Automation.Provider.Containercmdletprovider.Renameitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) metódus támogatja a hívást a `Rename-Item` parancsmag. Ez a módszer a megadott elérési úton az elem nevét az új neve változik. Az új név mindig képest a fölérendelt elemtől (tároló) kell lennie.

Ez a szolgáltató nem bírálja felül a [System.Management.Automation.Provider.Containercmdletprovider.Renameitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) metódust. Azonban az alábbi, az alapértelmezett implementációja.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderrenameitem](Msh_samplestestcmdlets#testproviderrenameitem)]  -->

#### <a name="things-to-remember-about-implementing-renameitem"></a>Megjegyzendő RenameItem megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Containercmdletprovider.Renameitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-tároló szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) metódus meg kell győződnie arról, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott követelményeinek képességek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- A [System.Management.Automation.Provider.Containercmdletprovider.Renameitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) metódus célja, a módosítás csak egy elem nevét, és nem a áthelyezési műveleteket. A metódus megvalósítása kell írási hiba, ha a `newName` paraméter elérési út elválasztók tartalmaz, vagy ellenkező esetben előfordulhat, hogy a cikk a fölérendelt helyének megváltoztatásához.

- Alapértelmezés szerint ez a metódus felülbírálását kell nem nevezhető át objektumokat, kivéve, ha a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonság meg van adva. Ha a megadott elérési út azt jelzi, hogy egy tárolóban, a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonság nem kötelező.

- A megvalósítását az [System.Management.Automation.Provider.Containercmdletprovider.Renameitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) metódus meg kell hívnia [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) , és ellenőrizze a visszaadott érték az adattár változtatások előtt. Ez a módszer segítségével amikor módosításakor a rendszer állapotáról, például fájlok átnevezésével, győződjön meg arról, hogy egy művelet végrehajtását. [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) küld a felhasználó a Windows PowerShell-futtatókörnyezetben, figyelembe véve parancssori beállítást vagy a preferenciaváltozók módosítani az erőforrás neve annak meghatározása, mi megjelenjenek.

  Hívása után [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) adja vissza `true`, a [System.Management.Automation.Provider.Containercmdletprovider.Renameitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItem) metódus meg kell hívnia a [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) metódust. Ez a módszer egy üzenetet küld egy megerősítő üzenetet a felhasználó számára lehetővé tegyük fel, ha a művelet folytatni kell további visszajelzéseket. Meg kell hívnia a szolgáltató [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) , egy potenciálisan veszélyes rendszermódosítások további keresése.

## <a name="attaching-dynamic-parameters-to-the-rename-item-cmdlet"></a>Dinamikus paraméterek csatolása a Rename-cikk parancsmaghoz

Egyes esetekben a `Rename-Item` parancsmaghoz szükséges további paramétereket, amelyeket dinamikusan futásidőben. Ezek a dinamikus paraméterek megadásához Windows PowerShell tároló a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Containercmdletprovider.Renameitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RenameItemDynamicParameters) metódust. Ez a módszer kérdezi le a paramétereket, az elem elérési útja a jelzett és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [System.Management.Automation.Runtimedefinedparameterdictionary ](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a `Rename-Item` parancsmagot.

Ez a tároló-szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderrenameitemdynamicparameters](Msh_samplestestcmdlets#testproviderrenameitemdynamicparameters)]  -->

## <a name="creating-new-items"></a>Új elem létrehozása

Új cikkek létrehozásához, egy tárolót a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) metódus támogatja a hívást a `New-Item` parancsmagot. Ezzel a módszerrel hoz létre a megadott elérési úton található adatelemet. A `type` a parancsmag tartalmazza az új elem a szolgáltató által meghatározott típus. Ha például a fájlrendszer-szolgáltatót használ egy `type` paraméter "fájl" vagy "könyvtár" értékkel. A `newItemValue` a parancsmag az új elem szolgáltatóhoz tartozó értéket határoz meg.

Itt van a megvalósítása a [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) metódust a szolgáltató.

```csharp
protected override void NewItem( string path, string type,
                                 object newItemValue )
{
    // Create the new item here after
    // performing necessary validations
    //
    // WriteItemObject(newItemValue, path, false);

    // Example
    //
    // if (ShouldProcess(path, "new item"))
    // {
    //      // Create a new item and then call WriteObject
    //      WriteObject(newItemValue, path, false);
    // }

} // NewItem
```

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L939-L955 "AccessDBProviderSample04.cs")]

#### <a name="things-to-remember-about-implementing-newitem"></a>Megjegyzendő új elem bevezetésével kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem):

- A [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) metódus végre kell hajtania az átadott karakterlánc kis-és összehasonlítása a `type` paraméter. Azt is lehetővé teszi az egyezések legalább egyértelműek. Például a típusok "file" és "directory", csak az első betűje szükséges elem egyértelműségének biztosításához. Ha a `type` paraméter azt jelzi, hogy a szolgáltató nem hozható létre, a típus a [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) metódust kell írnia egy üzenetet ArgumentException a típusok jelzi a szolgáltató hozhat létre.

- Az a `newItemValue` paraméter, a megvalósítása a [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) módszer ajánlott minimális karakterláncok fogadására. Azt is elfogadjon által beolvasott objektum típusa a [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) módszer ugyanazt az útvonalat. A [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) módszer használható a [System.Management.Automation.Languageprimitives.Convertto*](/dotnet/api/System.Management.Automation.LanguagePrimitives.ConvertTo) típust konvertálása metódus a kívánt típust.

- A megvalósítását az [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) metódus meg kell hívnia [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) , és ellenőrizze a visszaadott érték az adattár változtatások előtt. Hívása után [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) ad vissza IGAZ, a [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem) módszer meg kell hívnia a [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) potenciálisan veszélyes rendszermódosítások, egy további ellenőrzési módszert.

## <a name="attaching-dynamic-parameters-to-the-new-item-cmdlet"></a>Az új elem parancsmag dinamikus paraméterek csatolása

Egyes esetekben a `New-Item` parancsmaghoz szükséges további paramétereket, amelyeket dinamikusan futásidőben. Ezek a dinamikus paraméterek megadásához a tárolót a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Containercmdletprovider.Newitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItemDynamicParameters) metódust. Ez a módszer kérdezi le a paramétereket, az elem elérési útja a jelzett és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [System.Management.Automation.Runtimedefinedparameterdictionary ](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a `New-Item` parancsmagot.

Ez a szolgáltató nem valósítja meg ezt a módszert. Viszont a következő kódot, ez a módszer alapértelmezett megvalósítása.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidernewitemdynamicparameters](Msh_samplestestcmdlets#testprovidernewitemdynamicparameters)]  -->

## <a name="removing-items"></a>Elemek eltávolítása

Elem eltávolításához a Windows PowerShell-szolgáltatóban felül kell írnia a [System.Management.Automation.Provider.Containercmdletprovider.Removeitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) metódus támogatja a hívást a `Remove-Item` parancsmagot. Ez a módszer egy elem törlése az adatokat az adattárból a megadott elérési úton. Ha a `recurse` paraméterében a `Remove-Item` parancsmag értékre van állítva `true`, a módszer eltávolítja az összes alárendelt elem, függetlenül a szintet. Ha a paraméter értéke `false`, a módszer eltávolítja a megadott elérési úton csak egy elemet.

Ez a szolgáltató nem támogatja az elem eltávolítása. Azonban az alábbi kód-e az alapértelmezett megvalósítása [System.Management.Automation.Provider.Containercmdletprovider.Removeitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem).

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderremoveitem](Msh_samplestestcmdlets#testproviderremoveitem)]  -->

#### <a name="things-to-remember-about-implementing-removeitem"></a>Megjegyzendő RemoveItem megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Containercmdletprovider.Newitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.NewItem):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-tároló szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) metódus meg kell győződnie arról, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott követelményeinek képességek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását sem érdemes eltávolítani objektumok, kivéve, ha a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonság értéke igaz. Ha a megadott elérési út azt jelzi, hogy egy tárolóban, a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonság nem kötelező.

- Megvalósítását [System.Management.Automation.Provider.Containercmdletprovider.Removeitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) végtelen rekurzió megakadályozza, hogy ha körkörös hivatkozások és a hasonló felelős. Egy megfelelő megszakítást okozó kivétel történt a kell, hogy ilyen feltétel lépett fel.

- A megvalósítását az [System.Management.Automation.Provider.Containercmdletprovider.Removeitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) metódus meg kell hívnia [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) , és ellenőrizze a visszaadott érték az adattár változtatások előtt. Hívása után [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) adja vissza `true`, a [System.Management.Automation.Provider.Containercmdletprovider.Removeitem*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItem) metódus meg kell hívnia a [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) potenciálisan veszélyes rendszermódosítások, egy további ellenőrzési módszert.

## <a name="attaching-dynamic-parameters-to-the-remove-item-cmdlet"></a>A Remove-cikk parancsmag dinamikus paraméterek csatolása

Egyes esetekben a `Remove-Item` parancsmaghoz szükséges további paramétereket, amelyeket dinamikusan futásidőben. Ezek a dinamikus paraméterek megadásához a tárolót a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Containercmdletprovider.Removeitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItemDynamicParameters) metódust ezeket a paramétereket. Ez a módszer lekéri a dinamikus paraméterek az elem elérési útja a jelzett és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [ System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a `Remove-Item` parancsmagot.

Ez a tároló-szolgáltató nem valósítja meg ezt a módszert. Azonban az alábbi kód-e az alapértelmezett megvalósítása [System.Management.Automation.Provider.Containercmdletprovider.Removeitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.RemoveItemDynamicParameters).

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderremoveitemdynamicparameters](Msh_samplestestcmdlets#testproviderremoveitemdynamicparameters)]  -->

## <a name="querying-for-child-items"></a>Gyermekelemek lekérdezése

Ellenőrizze, hogy ha gyermekelemek létezik-e a megadott elérési úton, hogy a Windows PowerShell-tároló szolgáltató felül kell írnia a [System.Management.Automation.Provider.Containercmdletprovider.Haschilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems) metódust. A metódus visszatérése `true` Ha az elem típusú gyermekei, és `false` más módon. Egy NULL értékű vagy üres elérési útjához, a metódus egyetlen elem sem a gyermekek lennie az adattár is figyelembe veszi, és adja vissza `true`.

Íme a felülbírálást a [System.Management.Automation.Provider.Containercmdletprovider.Haschilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems) metódust. Ha több mint két elérési út részből áll ChunkPath segédmetódus által létrehozott, a metódus adja vissza `false`, mivel csak egy adatbázist tároló és a egy table-tároló meg van határozva. A segítő módszerrel kapcsolatos további információkért lásd: a ChunkPath módszer a következő cikkben [egy Windows PowerShell elem szolgáltató létrehozása](./creating-a-windows-powershell-item-provider.md).

```csharp
protected override bool HasChildItems( string path )
{
    return false;
} // HasChildItems
```

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L1094-L1097 "AccessDBProviderSample04.cs")]

#### <a name="things-to-remember-about-implementing-haschilditems"></a>Megjegyzendő HasChildItems megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Containercmdletprovider.Haschilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems):

- Ha a tároló szolgáltató tesz közzé egy érdekes csatlakoztatási pontok, a megvalósítása tartalmazó gyökér a [System.Management.Automation.Provider.Containercmdletprovider.Haschilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.HasChildItems) módszert kell visszaadnia `true`amikor null értékű vagy üres karakterlánc átadott elérési úthoz.

## <a name="copying-items"></a>Elemek másolása

Elemek másolása, a tároló a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) metódus támogatja a hívást a `Copy-Item` parancsmagot. Ez a módszer egy adatelem jelzett helyre másolja át a `path` jelzi a helyet a parancsmag a `copyPath` paraméter. Ha a `recurse` paraméter meg van adva, a metódus az összes alárendelt tároló másolja. Ha a paraméter nincs megadva, a metódus csak egyszintű elemek másolja át.

Ez a szolgáltató nem valósítja meg ezt a módszert. Azonban az alábbi kód-e az alapértelmezett megvalósítása [System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem).

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidercopyitem](Msh_samplestestcmdlets#testprovidercopyitem)]  -->

#### <a name="things-to-remember-about-implementing-copyitem"></a>Megjegyzendő CopyItem megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-tároló szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Containercmdletprovider.Getchilditems*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.GetChildItems) metódus meg kell győződnie arról, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott követelményeinek képességek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását ne próbálja átmásolni objektumok keresztül a meglévő objektumok, kivéve, ha a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Ha például a fájlrendszer-szolgáltatót nem másolja c:\temp\abc.txt egy már létező c:\abc.txt fájl, kivéve, ha a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Ha a megadott elérési útja a `copyPath` paraméter létezik, és azt jelzi, hogy egy tárolóban, a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonság nem kötelező. Ebben az esetben [System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) át kell másolnia az elem jelzi a `path` által megadott a tárolóhoz a paraméter a `copyPath` gyermek paraméter.

- Megvalósítását [System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) végtelen rekurzió megakadályozza, hogy ha körkörös hivatkozások és a hasonló felelős. Egy megfelelő megszakítást okozó kivétel történt a kell, hogy ilyen feltétel lépett fel.

- A megvalósítását az [System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) metódus meg kell hívnia [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) , és ellenőrizze a visszaadott érték az adattár változtatások előtt. Hívása után [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) ad vissza IGAZ, a [System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItem) módszer meg kell hívnia a [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) potenciálisan veszélyes rendszermódosítások, egy további ellenőrzési módszert. Ezek a metódusok meghívásával kapcsolatos további információkért lásd: [cikkek átnevezése](#renaming-items).

## <a name="attaching-dynamic-parameters-to-the-copy-item-cmdlet"></a>Dinamikus paraméterek csatolása a Copy-Item parancsmaghoz

Egyes esetekben a `Copy-Item` parancsmaghoz szükséges további paramétereket, amelyeket dinamikusan futásidőben. Ahhoz, hogy ezek a dinamikus paraméterek, a Windows PowerShell tároló a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Containercmdletprovider.Copyitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItemDynamicParameters) ezek metódust a paraméterek. Ez a módszer kérdezi le a paramétereket, az elem elérési útja a jelzett és tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés rendelkező objektumot adja vissza vagy egy [System.Management.Automation.Runtimedefinedparameterdictionary ](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a `Copy-Item` parancsmagot.

Ez a szolgáltató nem valósítja meg ezt a módszert. Azonban az alábbi kód-e az alapértelmezett megvalósítása [System.Management.Automation.Provider.Containercmdletprovider.Copyitemdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider.CopyItemDynamicParameters).

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidercopyitemdynamicparameters](Msh_samplestestcmdlets#testprovidercopyitemdynamicparameters)]  -->

## <a name="code-sample"></a>Kódminta

Teljes minta kódja, lásd: [AccessDbProviderSample04 kódminta](./accessdbprovidersample04-code-sample.md).

## <a name="building-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltató létrehozása

Lásd: [parancsmagok,-szolgáltatók regisztrálása és alkalmazások üzemeltetése](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="testing-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltatóban tesztelése

Ha a Windows PowerShell-szolgáltató regisztrálva van a Windows PowerShell-lel, tesztelheti a támogatott parancsmagok futtatásával a parancssorban. Vegye figyelembe, hogy az alábbi példa kimenetében használ egy fiktív Access-adatbázis.

1. Futtassa a `Get-ChildItem` az Access-adatbázis ügyfelek táblájában az alárendelt elemek listájának beolvasásához.

   ```powershell
   Get-ChildItem mydb:customers
   ```

   A következő eredmény jelenik meg.

   ```output
   PSPath        : AccessDB::customers
   PSDrive       : mydb
   PSProvider    : System.Management.Automation.ProviderInfo
   PSIsContainer : True
   Data          : System.Data.DataRow
   Name          : Customers
   RowCount      : 91
   Columns       :
   ```

2. Futtassa a `Get-ChildItem` parancsmag újra az adatokat egy tábla lekéréséhez.

   ```powershell
   (Get-ChildItem mydb:customers).data
   ```

   A következő eredmény jelenik meg.

   ```output
   TABLE_CAT   : c:\PS\northwind
   TABLE_SCHEM :
   TABLE_NAME  : Customers
   TABLE_TYPE  : TABLE
   REMARKS     :
   ```

3. Mostantól használhatja a `Get-Item` adattábla 0 sort elemek beolvasásához.

   ```powershell
   Get-Item mydb:\customers\0
   ```

   A következő eredmény jelenik meg.

   ```output
   PSPath        : AccessDB::customers\0
   PSDrive       : mydb
   PSProvider    : System.Management.Automation.ProviderInfo
   PSIsContainer : False
   Data          : System.Data.DataRow
   RowNumber     : 0
   ```

4. Újból felhasználhatja `Get-Item` sor 0 elemeinek adatok lekéréséhez.

   ```powershell
   (Get-Item mydb:\customers\0).data
   ```

   A következő eredmény jelenik meg.

   ```output
   CustomerID   : 1234
   CompanyName  : Fabrikam
   ContactName  : Eric Gruber
   ContactTitle : President
   Address      : 4567 Main Street
   City         : Buffalo
   Region       : NY
   PostalCode   : 98052
   Country      : USA
   Phone        : (425) 555-0100
   Fax          : (425) 555-0101
   ```

5. Mostantól használhatja a `New-Item` parancsmag segítségével adjon hozzá egy sort egy meglévő táblába. A `Path` paraméter megadja a sor teljes elérési útja, és tartalmaznia kell egy sorszám nagyobb, mint a meglévő a tábla sorainak száma. A `Type` paraméter azt jelzi, hogy az adott típusú elem hozzáadásához adja meg a "sor". Végül a `Value` paraméter megadja a sor oszlop értékek egy vesszővel tagolt listája.

   ```powershell
   New-Item -Path mydb:\Customers\3 -ItemType "row" -Value "3,CustomerFirstName,CustomerLastName,CustomerEmailAddress,CustomerTitle,CustomerCompany,CustomerPhone, CustomerAddress,CustomerCity,CustomerState,CustomerZip,CustomerCountry"
   ```

6. Ellenőrizze, hogy az új elem művelet a következő.

   ```none
   PS mydb:\> cd Customers
   PS mydb:\Customers> (Get-Item 3).data
   ```

   A következő eredmény jelenik meg.

   ```output
   ID        : 3
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
   ```

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-szolgáltató létrehozása](./how-to-create-a-windows-powershell-provider.md)

[A Windows PowerShell-szolgáltató tervezése](./designing-your-windows-powershell-provider.md)

[Egy elem Windows PowerShell-szolgáltatóban megvalósítása](./creating-a-windows-powershell-item-provider.md)

[A navigációs Windows PowerShell-szolgáltatóban megvalósítása](./creating-a-windows-powershell-navigation-provider.md)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell SDK](../windows-powershell-reference.md)

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)