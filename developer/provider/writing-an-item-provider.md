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
# <a name="writing-an-item-provider"></a><span data-ttu-id="557ac-102">Elemszolgáltató írása</span><span class="sxs-lookup"><span data-stu-id="557ac-102">Writing an item provider</span></span>

<span data-ttu-id="557ac-103">Ez a témakör ismerteti, hogyan valósíthat meg a Windows PowerShell-szolgáltató a módszereket, amelyekkel elérheti és módosíthatja az adattár elemeit.</span><span class="sxs-lookup"><span data-stu-id="557ac-103">This topic describes how to implement the methods of a Windows PowerShell provider that access and manipulate items in the data store.</span></span> <span data-ttu-id="557ac-104">Az, hogy elemek eléréséhez, egy szolgáltató származhat a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály.</span><span class="sxs-lookup"><span data-stu-id="557ac-104">To be able to access items, a provider must derive from the [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class.</span></span>

<span data-ttu-id="557ac-105">A szolgáltató a példákban Ez a témakör az Access-adatbázisok a adattárként használja.</span><span class="sxs-lookup"><span data-stu-id="557ac-105">The provider in the examples in this topic uses an Access database as its data store.</span></span> <span data-ttu-id="557ac-106">Több segédmetódusokat és az adatbázis használt osztályok is van.</span><span class="sxs-lookup"><span data-stu-id="557ac-106">There are several helper methods and classes that are used to interact with the database.</span></span> <span data-ttu-id="557ac-107">A teljes minta a segédmetódusokat tartalmazó: [AccessDBProviderSample03](./accessdbprovidersample03.md)</span><span class="sxs-lookup"><span data-stu-id="557ac-107">For the complete sample that includes the helper methods, see [AccessDBProviderSample03](./accessdbprovidersample03.md)</span></span>

<span data-ttu-id="557ac-108">További információ a Windows PowerShell-szolgáltatók: [Windows PowerShell-szolgáltató áttekintése](./windows-powershell-provider-overview.md).</span><span class="sxs-lookup"><span data-stu-id="557ac-108">For more information about Windows PowerShell providers, see [Windows PowerShell Provider Overview](./windows-powershell-provider-overview.md).</span></span>

## <a name="implementing-item-methods"></a><span data-ttu-id="557ac-109">Elem-metódusokat megvalósítása</span><span class="sxs-lookup"><span data-stu-id="557ac-109">Implementing item methods</span></span>

<span data-ttu-id="557ac-110">A [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztály többféle módszer is használható a tárolóban található elemek érje el vagy tesz elérhetővé.</span><span class="sxs-lookup"><span data-stu-id="557ac-110">The [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class exposes several methods that can be used to access and manipulate the items in a data store.</span></span> <span data-ttu-id="557ac-111">Ezek a metódusok teljes listáját lásd: [ItemCmdletProvider módszerek](http://msdn.microsoft.com/library/system.management.automation.provider.itemcmdletprovider_methods\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="557ac-111">For a complete list of these methods, see [ItemCmdletProvider Methods](http://msdn.microsoft.com/library/system.management.automation.provider.itemcmdletprovider_methods\(v=vs.85\).aspx).</span></span> <span data-ttu-id="557ac-112">Ebben a példában fog megvalósítása négy ezen metódusok közül.</span><span class="sxs-lookup"><span data-stu-id="557ac-112">In this example, we will implement four of these methods.</span></span> <span data-ttu-id="557ac-113">[System.Management.Automation.Provider.Itemcmdletprovider.Getitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) egy elem beolvasása a megadott elérési úton.</span><span class="sxs-lookup"><span data-stu-id="557ac-113">[System.Management.Automation.Provider.Itemcmdletprovider.Getitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) gets an item at a specified path.</span></span> <span data-ttu-id="557ac-114">[System.Management.Automation.Provider.Itemcmdletprovider.Setitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) a megadott elem értékét.</span><span class="sxs-lookup"><span data-stu-id="557ac-114">[System.Management.Automation.Provider.Itemcmdletprovider.Setitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) sets the value of the specified item.</span></span> <span data-ttu-id="557ac-115">[System.Management.Automation.Provider.Itemcmdletprovider.Itemexists\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) ellenőrzi, hogy létezik-e egy elemet a megadott elérési úton.</span><span class="sxs-lookup"><span data-stu-id="557ac-115">[System.Management.Automation.Provider.Itemcmdletprovider.Itemexists\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) checks whether an item exists at the specified path.</span></span> <span data-ttu-id="557ac-116">[System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) ellenőrzi a elérési útját, tekintse meg, ha vannak leképezve az adattár egy helyre.</span><span class="sxs-lookup"><span data-stu-id="557ac-116">[System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) checks a path to see if it maps to a location in the data store.</span></span>

> [!NOTE]
> <span data-ttu-id="557ac-117">Ebben a témakörben található információk épül [Windows PowerShell szolgáltató a rövid útmutató](./windows-powershell-provider-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="557ac-117">This topic builds on the information in [Windows PowerShell Provider QuickStart](./windows-powershell-provider-quickstart.md).</span></span> <span data-ttu-id="557ac-118">Ez a témakör nem terjed ki a szolgáltató projekt beállítása alapjait, vagy a módszerek megvalósításának öröklődés forrása a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztály létrehozása, és távolítsa el a meghajtókat.</span><span class="sxs-lookup"><span data-stu-id="557ac-118">This topic does not cover the basics of how to set up a provider project, or how to implement the methods inherited from the [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) class that create and remove drives.</span></span>

### <a name="declaring-the-provider-class"></a><span data-ttu-id="557ac-119">A szolgáltató osztálya deklaráló</span><span class="sxs-lookup"><span data-stu-id="557ac-119">Declaring the provider class</span></span>

<span data-ttu-id="557ac-120">A szolgáltató származtassa deklarálja a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) osztályt, és megadhat hozzá a [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute).</span><span class="sxs-lookup"><span data-stu-id="557ac-120">Declare the provider to derive from the [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) class, and decorate it with the [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute).</span></span>

```csharp
[CmdletProvider("AccessDB", ProviderCapabilities.None)]

   public class AccessDBProvider : ItemCmdletProvider
   {

  }

```

### <a name="implementing-getitem"></a><span data-ttu-id="557ac-121">Végrehajtási GetItem</span><span class="sxs-lookup"><span data-stu-id="557ac-121">Implementing GetItem</span></span>

<span data-ttu-id="557ac-122">A [System.Management.Automation.Provider.Itemcmdletprovider.Getitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) nevezzük a PowerShell motor, amikor egy felhasználó meghívja a [Microsoft.PowerShell.Commands.Get-cikk](/dotnet/api/Microsoft.PowerShell.Commands.Get-Item) parancsmagot a szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="557ac-122">The [System.Management.Automation.Provider.Itemcmdletprovider.Getitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.GetItem) is called by the PowerShell engine when a user calls the [Microsoft.PowerShell.Commands.Get-Item](/dotnet/api/Microsoft.PowerShell.Commands.Get-Item) cmdlet on your provider.</span></span> <span data-ttu-id="557ac-123">A metódus a megadott elérési úton elemét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="557ac-123">The method returns the item at the specified path.</span></span> <span data-ttu-id="557ac-124">A hozzáférés adatbázis példában a metódus ellenőrzi, hogy a cikk a meghajtó, egy táblát az adatbázisban, vagy egy sor az adatbázisban.</span><span class="sxs-lookup"><span data-stu-id="557ac-124">In the Access database example, the method checks whether the item is the drive itself, a table in the database, or a row in the database.</span></span> <span data-ttu-id="557ac-125">A metódus az elem küldi a PowerShell motor meghívásával a [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject) metódust.</span><span class="sxs-lookup"><span data-stu-id="557ac-125">The method sends the item to the PowerShell engine by calling the [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject) method.</span></span>

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

### <a name="implementing-setitem"></a><span data-ttu-id="557ac-126">Végrehajtási SetItem</span><span class="sxs-lookup"><span data-stu-id="557ac-126">Implementing SetItem</span></span>

<span data-ttu-id="557ac-127">A [System.Management.Automation.Provider.Itemcmdletprovider.Setitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) metódust hívja meg, a PowerShell motor hívások amikor egy felhasználó meghívja a [Microsoft.PowerShell.Commands.Set-cikk](/dotnet/api/Microsoft.PowerShell.Commands.Set-Item) parancsmag .</span><span class="sxs-lookup"><span data-stu-id="557ac-127">The [System.Management.Automation.Provider.Itemcmdletprovider.Setitem\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.SetItem) method is called by the PowerShell engine calls when a user calls the [Microsoft.PowerShell.Commands.Set-Item](/dotnet/api/Microsoft.PowerShell.Commands.Set-Item) cmdlet.</span></span> <span data-ttu-id="557ac-128">A megadott elérési úton, beállítja az elem értékét.</span><span class="sxs-lookup"><span data-stu-id="557ac-128">It sets the value of the item at the specified path.</span></span>

<span data-ttu-id="557ac-129">A hozzáférés adatbázis példában logikus elem értéke állítható be, csak ha a elem egy sort, a metódus jelez [NotSupportedException](http://msdn.microsoft.com/library/system.notsupportedexception\(v=vs.110\).aspx) Ha ez az elem nem egy sort.</span><span class="sxs-lookup"><span data-stu-id="557ac-129">In the Access database example, it makes sense to set the value of an item only if that item is a row, so the method throws [NotSupportedException](http://msdn.microsoft.com/library/system.notsupportedexception\(v=vs.110\).aspx) when the item is not a row.</span></span>

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

### <a name="implementing-itemexists"></a><span data-ttu-id="557ac-130">Végrehajtási ItemExists</span><span class="sxs-lookup"><span data-stu-id="557ac-130">Implementing ItemExists</span></span>

<span data-ttu-id="557ac-131">A [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) metódus a PowerShell motor nevezzük, amikor egy felhasználó meghívja a [Microsoft.PowerShell.Commands.Test-Path](/dotnet/api/Microsoft.PowerShell.Commands.Test-Path) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="557ac-131">The [System.Management.Automation.Provider.Itemcmdletprovider.Itemexists\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.ItemExists) method is called by the PowerShell engine when a user calls the [Microsoft.PowerShell.Commands.Test-Path](/dotnet/api/Microsoft.PowerShell.Commands.Test-Path) cmdlet.</span></span> <span data-ttu-id="557ac-132">A módszer határozza meg, hogy van-e egy elemet a megadott elérési úton.</span><span class="sxs-lookup"><span data-stu-id="557ac-132">The method determines whether there is an item at the specified path.</span></span> <span data-ttu-id="557ac-133">Ha az elem létezik, a metódus továbbítja azt vissza a PowerShell motor meghívásával [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject).</span><span class="sxs-lookup"><span data-stu-id="557ac-133">If the item does exist, the method passes it back to the PowerShell engine by calling [System.Management.Automation.Provider.Cmdletprovider.Writeitemobject\*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteItemObject).</span></span>

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

### <a name="implementing-isvalidpath"></a><span data-ttu-id="557ac-134">Végrehajtási IsValidPath</span><span class="sxs-lookup"><span data-stu-id="557ac-134">Implementing IsValidPath</span></span>

<span data-ttu-id="557ac-135">A [System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) metódus ellenőrzi, hogy a megadott elérési út a jelenlegi szolgáltató szintaktikailag érvényes.</span><span class="sxs-lookup"><span data-stu-id="557ac-135">The [System.Management.Automation.Provider.Itemcmdletprovider.Isvalidpath\*](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider.IsValidPath) method checks whether the specified path is syntactically valid for the current provider.</span></span> <span data-ttu-id="557ac-136">Azt nem ellenőrzi, hogy létezik-e egy elem az elérési úton.</span><span class="sxs-lookup"><span data-stu-id="557ac-136">It does not check whether an item exists at the path.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="557ac-137">További lépések</span><span class="sxs-lookup"><span data-stu-id="557ac-137">Next steps</span></span>

<span data-ttu-id="557ac-138">Egy tipikus valós szolgáltató az képes támogató más elemeket tartalmazó elemeket, és az elemek áthelyezését egy elérési utat egy másik, a meghajtó belül.</span><span class="sxs-lookup"><span data-stu-id="557ac-138">A typical real-world provider is capable of supporting items that contain other items, and of moving items from one path to another within the drive.</span></span> <span data-ttu-id="557ac-139">A szolgáltató, amely támogatja a tárolók egy példa: [egy tároló-szolgáltató írása](./writing-a-container-provider.md).</span><span class="sxs-lookup"><span data-stu-id="557ac-139">For an example of a provider that supports containers, see [Writing a container provider](./writing-a-container-provider.md).</span></span> <span data-ttu-id="557ac-140">A szolgáltató, amely támogatja az elemek áthelyezése egy példa: [navigációs szolgáltató írása](./writing-a-navigation-provider.md).</span><span class="sxs-lookup"><span data-stu-id="557ac-140">For an example of a provider that supports moving items, see [Writing a navigation provider](./writing-a-navigation-provider.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="557ac-141">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="557ac-141">See Also</span></span>

[<span data-ttu-id="557ac-142">Egy tároló-szolgáltató írása</span><span class="sxs-lookup"><span data-stu-id="557ac-142">Writing a container provider</span></span>](./writing-a-container-provider.md)

[<span data-ttu-id="557ac-143">A navigációs szolgáltató írása</span><span class="sxs-lookup"><span data-stu-id="557ac-143">Writing a navigation provider</span></span>](./writing-a-navigation-provider.md)

[<span data-ttu-id="557ac-144">Windows PowerShell-szolgáltató áttekintése</span><span class="sxs-lookup"><span data-stu-id="557ac-144">Windows PowerShell Provider Overview</span></span>](./windows-powershell-provider-overview.md)