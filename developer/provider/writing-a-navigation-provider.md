---
title: A navigációs szolgáltató írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98bcfda0-6ee2-46f5-bbc7-5fab8b780d6a
caps.latest.revision: 5
ms.openlocfilehash: a789b392bddd344ad583c93a1a55302329df9917
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56852086"
---
# <a name="writing-a-navigation-provider"></a><span data-ttu-id="8ebaa-102">Navigációszolgáltató írása</span><span class="sxs-lookup"><span data-stu-id="8ebaa-102">Writing a navigation provider</span></span>

<span data-ttu-id="8ebaa-103">Ez a témakör ismerteti, hogyan valósíthat meg egy Windows PowerShell-szolgáltatóban, amely támogatja a beágyazott tárolók (több szintű adattárolók), cikkek és relatív útvonalak áthelyezése módszerek.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-103">This topic describes how to implement the methods of a Windows PowerShell provider that support nested containers (multi-level data stores), moving items, and relative paths.</span></span> <span data-ttu-id="8ebaa-104">A navigációs szolgáltató származhat a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztály.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-104">A navigation provider must derive from the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class.</span></span>

<span data-ttu-id="8ebaa-105">A szolgáltató a példákban Ez a témakör az Access-adatbázisok a adattárként használja.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-105">The provider in the examples in this topic uses an Access database as its data store.</span></span> <span data-ttu-id="8ebaa-106">Több segédmetódusokat és az adatbázis használt osztályok is van.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-106">There are several helper methods and classes that are used to interact with the database.</span></span> <span data-ttu-id="8ebaa-107">A teljes minta a segédmetódusokat tartalmazó: [AccessDBProviderSample05](./accessdbprovidersample05.md).</span><span class="sxs-lookup"><span data-stu-id="8ebaa-107">For the complete sample that includes the helper methods, see [AccessDBProviderSample05](./accessdbprovidersample05.md).</span></span>

<span data-ttu-id="8ebaa-108">További információ a Windows PowerShell-szolgáltatók: [Windows PowerShell-szolgáltató áttekintése](./windows-powershell-provider-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ebaa-108">For more information about Windows PowerShell providers, see [Windows PowerShell Provider Overview](./windows-powershell-provider-overview.md).</span></span>

## <a name="implementing-navigation-methods"></a><span data-ttu-id="8ebaa-109">Navigációs módszereket megvalósítása</span><span class="sxs-lookup"><span data-stu-id="8ebaa-109">Implementing navigation methods</span></span>

<span data-ttu-id="8ebaa-110">A [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztálya határozza meg, amely támogatja a beágyazott tárolók, relatív útvonalakat és a cikkek mozgatása módszerek.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-110">The [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class implements methods that support nested containers, relative paths, and moving items.</span></span> <span data-ttu-id="8ebaa-111">Ezek a metódusok teljes listáját lásd: [NavigationCmdletProvider módszerek](http://msdn.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider_methods\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="8ebaa-111">For a complete list of these methods, see [NavigationCmdletProvider Methods](http://msdn.microsoft.com/library/system.management.automation.provider.navigationcmdletprovider_methods\(v=vs.85\).aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="8ebaa-112">Ebben a témakörben található információk épül [Windows PowerShell szolgáltató a rövid útmutató](./windows-powershell-provider-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="8ebaa-112">This topic builds on the information in [Windows PowerShell Provider QuickStart](./windows-powershell-provider-quickstart.md).</span></span> <span data-ttu-id="8ebaa-113">Ez a témakör nem terjed ki a szolgáltató projekt beállítása alapjait, vagy a módszerek megvalósításának öröklődés forrása a [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztály létrehozása, és távolítsa el a meghajtókat.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-113">This topic does not cover the basics of how to set up a provider project, or how to implement the methods inherited from the [System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) class that create and remove drives.</span></span> <span data-ttu-id="8ebaa-114">Ez a témakör nem fedi módszerek által elérhetővé tett megvalósítása a [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) vagy [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) osztályokat.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-114">This topic also does not cover how to implement methods exposed by the [System.Management.Automation.Provider.Itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) or [System.Management.Automation.Provider.Containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) classes.</span></span> <span data-ttu-id="8ebaa-115">Példa bemutatja, hogyan valósíthat meg az item-parancsmagokkal, lásd: [egy elem szolgáltató írása](./writing-an-item-provider.md).</span><span class="sxs-lookup"><span data-stu-id="8ebaa-115">For an example that shows how to implement item cmdlets, see [Writing an item provider](./writing-an-item-provider.md).</span></span> <span data-ttu-id="8ebaa-116">Példa bemutatja, hogyan valósíthat meg a tároló-parancsmagok, lásd: [egy tároló-szolgáltató írása](./writing-a-container-provider.md).</span><span class="sxs-lookup"><span data-stu-id="8ebaa-116">For an example that shows how to implement container cmdlets, see [Writing a container provider](./writing-a-container-provider.md).</span></span>

### <a name="declaring-the-provider-class"></a><span data-ttu-id="8ebaa-117">A szolgáltató osztálya deklaráló</span><span class="sxs-lookup"><span data-stu-id="8ebaa-117">Declaring the provider class</span></span>

<span data-ttu-id="8ebaa-118">A szolgáltató származtassa deklarálja a [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) osztályt, és megadhat hozzá a [System.Management.Automation.Provider.Cmdletproviderattribute ](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute).</span><span class="sxs-lookup"><span data-stu-id="8ebaa-118">Declare the provider to derive from the [System.Management.Automation.Provider.Navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) class, and decorate it with the [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute).</span></span>

```
[CmdletProvider("AccessDB", ProviderCapabilities.None)]
   public class AccessDBProvider : NavigationCmdletProvider
   {

   }
```

### <a name="implementing-isitemcontainer"></a><span data-ttu-id="8ebaa-119">Végrehajtási IsItemContainer</span><span class="sxs-lookup"><span data-stu-id="8ebaa-119">Implementing IsItemContainer</span></span>

<span data-ttu-id="8ebaa-120">A [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) metódus ellenőrzi, hogy a megadott elérési úton a elem egy tárolót.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-120">The [System.Management.Automation.Provider.Navigationcmdletprovider.Isitemcontainer\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.IsItemContainer) method checks whether the item at the specified path is a container.</span></span>

```csharp
protected override bool IsItemContainer(string path)
      {
         if (PathIsDrive(path))
         {
             return true;
         }

         string[] pathChunks = ChunkPath(path);
         string tableName;
         int rowNumber;

         PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

         if (type == PathType.Table)
         {
            foreach (DatabaseTableInfo ti in GetTables())
            {
                if (string.Equals(ti.Name, tableName, StringComparison.OrdinalIgnoreCase))
                {
                    return true;
                }
            } // foreach (DatabaseTableInfo...
         } // if (pathChunks...

         return false;
      }
```

### <a name="implementing-getchildname"></a><span data-ttu-id="8ebaa-121">Végrehajtási GetChildName</span><span class="sxs-lookup"><span data-stu-id="8ebaa-121">Implementing GetChildName</span></span>

<span data-ttu-id="8ebaa-122">A [System.Management.Automation.Provider.Navigationcmdletprovider.Getchildname\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetChildName) metódus lekéri az alárendelt elem a name tulajdonság a megadott elérési úton.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-122">The [System.Management.Automation.Provider.Navigationcmdletprovider.Getchildname\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetChildName) method gets the name property of the child item at the specified path.</span></span> <span data-ttu-id="8ebaa-123">Ha a megadott elérési úton elem nem egy adott tároló gyermek, akkor ezt a módszert az elérési utat kell visszaadnia.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-123">If the item at the specified path is not a child of a container, then this method should return the path.</span></span>

```csharp
protected override string GetChildName(string path)
       {
           if (PathIsDrive(path))
           {
               return path;
           }

           string tableName;
           int rowNumber;

           PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

           if (type == PathType.Table)
           {
               return tableName;
           }
           else if (type == PathType.Row)
           {
               return rowNumber.ToString(CultureInfo.CurrentCulture);
           }
           else
           {
               ThrowTerminatingInvalidPathException(path);
           }

           return null;
       }
```

### <a name="implementing-getparentpath"></a><span data-ttu-id="8ebaa-124">Végrehajtási GetParentPath</span><span class="sxs-lookup"><span data-stu-id="8ebaa-124">Implementing GetParentPath</span></span>

<span data-ttu-id="8ebaa-125">A [System.Management.Automation.Provider.Navigationcmdletprovider.Getparentpath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetParentPath) metódus lekéri az elem a szülő elérési útját a megadott elérési úton.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-125">The [System.Management.Automation.Provider.Navigationcmdletprovider.Getparentpath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.GetParentPath) method gets the path of the parent of the item at the specified path.</span></span> <span data-ttu-id="8ebaa-126">Ha a cikk a megadott elérési úton (tehát nem a szülő rendelkezik) az adattár gyökérkönyvtárában, akkor ez a módszer a gyökér elérési útját kell visszaadnia.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-126">If the item at the specified path is the root of the data store (so it has no parent), then this method should return the root path.</span></span>

```csharp
protected override string GetParentPath(string path, string root)
       {
           // If root is specified then the path has to contain
           // the root. If not nothing should be returned
           if (!String.IsNullOrEmpty(root))
           {
               if (!path.Contains(root))
               {
                   return null;
               }
           }

           return path.Substring(0, path.LastIndexOf(pathSeparator, StringComparison.OrdinalIgnoreCase));
       }
```

### <a name="implementing-makepath"></a><span data-ttu-id="8ebaa-127">Végrehajtási MakePath</span><span class="sxs-lookup"><span data-stu-id="8ebaa-127">Implementing MakePath</span></span>

<span data-ttu-id="8ebaa-128">A [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) metódus csatlakozik a megadott szülő elérési útját és a provider – belső elérési utat határozza meg (az elérési út információ típusokat, amelyeket ebbe hoz létre a megadott gyermek elérési útja szolgáltatók is támogatják, lásd: [Windows PowerShell-szolgáltató áttekintése](./windows-powershell-provider-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ebaa-128">The [System.Management.Automation.Provider.Navigationcmdletprovider.Makepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MakePath) method joins a specified parent path and a specified child path to create a provider-internal path (for information about path types that providers can support, see [Windows PowerShell Provider Overview](./windows-powershell-provider-overview.md).</span></span> <span data-ttu-id="8ebaa-129">A PowerShell motor meghívja ezt a metódust, amikor egy felhasználó meghívja a [Microsoft.Powershell.Commands.Join-Path](/dotnet/api/Microsoft.PowerShell.Commands.Join-Path) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-129">The PowerShell engine calls this method when a user calls the [Microsoft.Powershell.Commands.Join-Path](/dotnet/api/Microsoft.PowerShell.Commands.Join-Path) cmdlet.</span></span>

```csharp
protected override string MakePath(string parent, string child)
       {
           string result;

           string normalParent = NormalizePath(parent);
           normalParent = RemoveDriveFromPath(normalParent);
           string normalChild = NormalizePath(child);
           normalChild = RemoveDriveFromPath(normalChild);

           if (String.IsNullOrEmpty(normalParent) && String.IsNullOrEmpty(normalChild))
           {
               result = String.Empty;
           }
           else if (String.IsNullOrEmpty(normalParent) && !String.IsNullOrEmpty(normalChild))
           {
               result = normalChild;
           }
           else if (!String.IsNullOrEmpty(normalParent) && String.IsNullOrEmpty(normalChild))
           {
               if (normalParent.EndsWith(pathSeparator, StringComparison.OrdinalIgnoreCase))
               {
                   result = normalParent;
               }
               else
               {
                   result = normalParent + pathSeparator;
               }
           } // else if (!String...
           else
           {
               if (!normalParent.Equals(String.Empty) &&
                   !normalParent.EndsWith(pathSeparator, StringComparison.OrdinalIgnoreCase))
               {
                   result = normalParent + pathSeparator;
               }
               else
               {
                   result = normalParent;
               }

               if (normalChild.StartsWith(pathSeparator, StringComparison.OrdinalIgnoreCase))
               {
                   result += normalChild.Substring(1);
               }
               else
               {
                   result += normalChild;
               }
           } // else

           return result;
       }
```

### <a name="implementing-normalizerelativepath"></a><span data-ttu-id="8ebaa-130">Implementing NormalizeRelativePath</span><span class="sxs-lookup"><span data-stu-id="8ebaa-130">Implementing NormalizeRelativePath</span></span>

<span data-ttu-id="8ebaa-131">A [System.Management.Automation.Provider.Navigationcmdletprovider.Normalizerelativepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.NormalizeRelativePath) módszer `path` és `basepath` paramétereket, és adja vissza, amely megegyezik a Normalizáltelérési`path`paraméter és a viszonyítva a `basepath` paraméter.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-131">The [System.Management.Automation.Provider.Navigationcmdletprovider.Normalizerelativepath\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.NormalizeRelativePath) method takes `path` and `basepath` parameters, and returns a normalized path that is equivalent to the `path` parameter and relative to the `basepath` parameter.</span></span>

```csharp
protected override string NormalizeRelativePath(string path,
                                                            string basepath)
       {
           // Normalize the paths first
           string normalPath = NormalizePath(path);
           normalPath = RemoveDriveFromPath(normalPath);
           string normalBasePath = NormalizePath(basepath);
           normalBasePath = RemoveDriveFromPath(normalBasePath);

           if (String.IsNullOrEmpty(normalBasePath))
           {
               return normalPath;
           }
           else
           {
               if (!normalPath.Contains(normalBasePath))
               {
                   return null;
               }

               return normalPath.Substring(normalBasePath.Length + pathSeparator.Length);
           }
       }
```

### <a name="implementing-moveitem"></a><span data-ttu-id="8ebaa-132">Végrehajtási MoveItem</span><span class="sxs-lookup"><span data-stu-id="8ebaa-132">Implementing MoveItem</span></span>

<span data-ttu-id="8ebaa-133">A [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) metódus a megadott elérési út egy elem helyez át a megadott célhely elérési útja.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-133">The [System.Management.Automation.Provider.Navigationcmdletprovider.Moveitem\*](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider.MoveItem) method moves an item from the specified path to the specified destination path.</span></span> <span data-ttu-id="8ebaa-134">A PowerShell motor meghívja ezt a metódust, amikor egy felhasználó meghívja a [Microsoft.Powershell.Commands.Move-cikk](/dotnet/api/Microsoft.PowerShell.Commands.Move-Item) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="8ebaa-134">The PowerShell engine calls this method when a user calls the [Microsoft.Powershell.Commands.Move-Item](/dotnet/api/Microsoft.PowerShell.Commands.Move-Item) cmdlet.</span></span>

```csharp
protected override void MoveItem(string path, string destination)
       {
           // Get type, table name and rowNumber from the path
           string tableName, destTableName;
           int rowNumber, destRowNumber;

           PathType type = GetNamesFromPath(path, out tableName, out rowNumber);

           PathType destType = GetNamesFromPath(destination, out destTableName,
                                    out destRowNumber);

           if (type == PathType.Invalid)
           {
               ThrowTerminatingInvalidPathException(path);
           }

           if (destType == PathType.Invalid)
           {
               ThrowTerminatingInvalidPathException(destination);
           }

           if (type == PathType.Table)
           {
               ArgumentException e = new ArgumentException("Move not supported for tables");

               WriteError(new ErrorRecord(e, "MoveNotSupported",
                   ErrorCategory.InvalidArgument, path));

               throw e;
           }
           else
           {
               OdbcDataAdapter da = GetAdapterForTable(tableName);
               if (da == null)
               {
                   return;
               }

               DataSet ds = GetDataSetForTable(da, tableName);
               DataTable table = GetDataTable(ds, tableName);

               OdbcDataAdapter dda = GetAdapterForTable(destTableName);
               if (dda == null)
               {
                   return;
               }

               DataSet dds = GetDataSetForTable(dda, destTableName);
               DataTable destTable = GetDataTable(dds, destTableName);
               DataRow row = table.Rows[rowNumber];

               if (destType == PathType.Table)
               {
                   DataRow destRow = destTable.NewRow();

                   destRow.ItemArray = row.ItemArray;
               }
               else
               {
                   DataRow destRow = destTable.Rows[destRowNumber];

                   destRow.ItemArray = row.ItemArray;
               }

               // Update the changes
               if (ShouldProcess(path, "MoveItem"))
               {
                   WriteItemObject(row, path, false);
                   dda.Update(dds, destTableName);
               }
           }
       }
```

## <a name="see-also"></a><span data-ttu-id="8ebaa-135">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8ebaa-135">See Also</span></span>

[<span data-ttu-id="8ebaa-136">Egy tároló-szolgáltató írása</span><span class="sxs-lookup"><span data-stu-id="8ebaa-136">Writing a container provider</span></span>](./writing-a-container-provider.md)

[<span data-ttu-id="8ebaa-137">Windows PowerShell-szolgáltató áttekintése</span><span class="sxs-lookup"><span data-stu-id="8ebaa-137">Windows PowerShell Provider Overview</span></span>](./windows-powershell-provider-overview.md)