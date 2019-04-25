---
title: Egy elem szolgáltató írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 606c880c-6cf1-4ea6-8730-dbf137bfabff
caps.latest.revision: 5
ms.openlocfilehash: 9285a2f0e673de8b86084157423512bdeeda109d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080815"
---
# <a name="writing-an-item-provider"></a>Elemszolgáltató írása

Ez a témakör ismerteti, hogyan valósíthat meg a Windows PowerShell-szolgáltató a módszereket, amelyekkel elérheti és módosíthatja az adattár elemeit. Az, hogy elemek eléréséhez, egy szolgáltató származhat a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály.

A szolgáltató a példákban Ez a témakör az Access-adatbázisok a adattárként használja. Több segédmetódusokat és az adatbázis használt osztályok is van. A teljes minta a segédmetódusokat tartalmazó: [AccessDBProviderSample03](./accessdbprovidersample03.md)

További információ a Windows PowerShell-szolgáltatók: [Windows PowerShell-szolgáltató áttekintése](./windows-powershell-provider-overview.md).

## <a name="implementing-item-methods"></a>Elem-metódusokat megvalósítása

A [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály többféle módszer is használható a tárolóban található elemek érje el vagy tesz elérhetővé. Ezek a metódusok teljes listáját lásd: [ItemCmdletProvider módszerek](http://msdn.microsoft.com/library/system.management.automation.provider.itemcmdletprovider_methods\(v=vs.85\).aspx). Ebben a példában fog megvalósítása négy ezen metódusok közül. [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) egy elem beolvasása a megadott elérési úton. [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) a megadott elem értékét. [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) ellenőrzi, hogy létezik-e egy elemet a megadott elérési úton. [System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) ellenőrzi a elérési útját, tekintse meg, ha vannak leképezve az adattár egy helyre.

> [!NOTE]
> Ebben a témakörben található információk épül [Windows PowerShell szolgáltató a rövid útmutató](./windows-powershell-provider-quickstart.md). Ez a témakör nem terjed ki a szolgáltató projekt beállítása alapjait, vagy a módszerek megvalósításának öröklődés forrása a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztály létrehozása, és távolítsa el a meghajtókat.

### <a name="declaring-the-provider-class"></a>A szolgáltató osztálya deklaráló

A szolgáltató származtassa deklarálja a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztályt, és megadhat hozzá a [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute).

```csharp
[CmdletProvider("AccessDB", ProviderCapabilities.None)]

   public class AccessDBProvider : ItemCmdletProvider
   {

  }

```

### <a name="implementing-getitem"></a>Végrehajtási GetItem

A [System.Management.Automation.Provider.Itemcmdletprovider.Getitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) nevezzük a PowerShell motor, amikor egy felhasználó meghívja a [Microsoft.PowerShell.Commands.Get-cikk](/dotnet/api/Microsoft.PowerShell.Commands.Get-Item) parancsmagot a szolgáltató. A metódus a megadott elérési úton elemét adja vissza. A hozzáférés adatbázis példában a metódus ellenőrzi, hogy a cikk a meghajtó, egy táblát az adatbázisban, vagy egy sor az adatbázisban. A metódus az elem küldi a PowerShell motor meghívásával a [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject) metódust.

```csharp
protected override void GetItem(string path)
      {
          // check if the path represented is a drive
          if (PathIsDrive(path))
          {
              WriteItemObject(this.PSDriveInfo, path, true);
              return;
          }// if (PathIsDrive...

           // Get table name and row information from the path and do
           // necessary actions
           string tableName;
           int rowNumber;

           PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

           if (type == PathType.Table)
           {
               DatabaseTableInfo table = GetTable(tableName);
               WriteItemObject(table, path, true);
           }
           else if (type == PathType.Row)
           {
               DatabaseRowInfo row = GetRow(tableName, rowNumber);
               WriteItemObject(row, path, false);
           }
           else
           {
               ThrowTerminatingInvalidPathException(path);
           }

       }
```

### <a name="implementing-setitem"></a>Végrehajtási SetItem

A [System.Management.Automation.Provider.Itemcmdletprovider.Setitem*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) metódust hívja meg, a PowerShell motor hívások amikor egy felhasználó meghívja a [Microsoft.PowerShell.Commands.Set-cikk](/dotnet/api/Microsoft.PowerShell.Commands.Set-Item) parancsmag . A megadott elérési úton, beállítja az elem értékét.

A hozzáférés adatbázis példában logikus elem értéke állítható be, csak ha a elem egy sort, a metódus jelez [NotSupportedException](http://msdn.microsoft.com/library/system.notsupportedexception\(v=vs.110\).aspx) Ha ez az elem nem egy sort.

```csharp
protected override void SetItem(string path, object values)
       {
           // Get type, table name and row number from the path specified
           string tableName;
           int rowNumber;

           PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

           if (type != PathType.Row)
           {
               WriteError(new ErrorRecord(new NotSupportedException(
                     "SetNotSupported"), "",
                  ErrorCategory.InvalidOperation, path));

               return;
           }

           // Get in-memory representation of table
           OdbcDataAdapter da = GetAdapterForTable(tableName);

           if (da == null)
           {
               return;
           }
           DataSet ds = GetDataSetForTable(da, tableName);
           DataTable table = GetDataTable(ds, tableName);

           if (rowNumber >= table.Rows.Count)
           {
               // The specified row number has to be available. If not
               // NewItem has to be used to add a new row
               throw new ArgumentException("Row specified is not available");
           } // if (rowNum...

           string[] colValues = (values as string).Split(',');

           // set the specified row
           DataRow row = table.Rows[rowNumber];

           for (int i = 0; i < colValues.Length; i++)
           {
               row[i] = colValues[i];
           }

           // Update the table
           if (ShouldProcess(path, "SetItem"))
           {
               da.Update(ds, tableName);
           }

       }
```

### <a name="implementing-itemexists"></a>Végrehajtási ItemExists

A [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) metódus a PowerShell motor nevezzük, amikor egy felhasználó meghívja a [Microsoft.PowerShell.Commands.Test-Path](/dotnet/api/Microsoft.PowerShell.Commands.Test-Path) parancsmagot. A módszer határozza meg, hogy van-e egy elemet a megadott elérési úton. Ha az elem létezik, a metódus továbbítja azt vissza a PowerShell motor meghívásával [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject).

```csharp
protected override bool ItemExists(string path)
       {
           // check if the path represented is a drive
           if (PathIsDrive(path))
           {
               return true;
           }

           // Obtain type, table name and row number from path
           string tableName;
           int rowNumber;

           PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

           DatabaseTableInfo table = GetTable(tableName);

           if (type == PathType.Table)
           {
               // if specified path represents a table then DatabaseTableInfo
               // object for the same should exist
               if (table != null)
               {
                   return true;
               }
           }
           else if (type == PathType.Row)
           {
               // if specified path represents a row then DatabaseTableInfo should
               // exist for the table and then specified row number must be within
               // the maximum row count in the table
               if (table != null && rowNumber < table.RowCount)
               {
                   return true;
               }
           }

           return false;

       }
```

### <a name="implementing-isvalidpath"></a>Végrehajtási IsValidPath

A [System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) metódus ellenőrzi, hogy a megadott elérési út a jelenlegi szolgáltató szintaktikailag érvényes. Azt nem ellenőrzi, hogy létezik-e egy elem az elérési úton.

```csharp
protected override bool IsValidPath(string path)
       {
           bool result = true;

           // check if the path is null or empty
           if (String.IsNullOrEmpty(path))
           {
               result = false;
           }

           // convert all separators in the path to a uniform one
           path = NormalizePath(path);

           // split the path into individual chunks
           string[] pathChunks = path.Split(pathSeparator.ToCharArray());

           foreach (string pathChunk in pathChunks)
           {
               if (pathChunk.Length == 0)
               {
                   result = false;
               }
           }
           return result;
       }
```

## <a name="next-steps"></a>További lépések

Egy tipikus valós szolgáltató az képes támogató más elemeket tartalmazó elemeket, és az elemek áthelyezését egy elérési utat egy másik, a meghajtó belül. A szolgáltató, amely támogatja a tárolók egy példa: [egy tároló-szolgáltató írása](./writing-a-container-provider.md). A szolgáltató, amely támogatja az elemek áthelyezése egy példa: [navigációs szolgáltató írása](./writing-a-navigation-provider.md).

## <a name="see-also"></a>Lásd még:

[Egy tároló-szolgáltató írása](./writing-a-container-provider.md)

[A navigációs szolgáltató írása](./writing-a-navigation-provider.md)

[Windows PowerShell-szolgáltató áttekintése](./windows-powershell-provider-overview.md)