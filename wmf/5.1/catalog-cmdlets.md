---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: Katalógusbeli parancsmagok
ms.openlocfilehash: 7eaca09667af0eb5d719f23e987bb112e8514978
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="catalog-cmdlets"></a><span data-ttu-id="f6ab9-103">Katalógus-parancsmagok</span><span class="sxs-lookup"><span data-stu-id="f6ab9-103">Catalog Cmdlets</span></span>

<span data-ttu-id="f6ab9-104">A két új parancsmagok jelentek meg [Microsoft.Powershell.Secuity](https://technet.microsoft.com/en-us/library/hh847877.aspx) modul hozhatnak létre és a windows katalógusban fájlok érvényesítése.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-104">We have added two new cmdlets in [Microsoft.Powershell.Secuity](https://technet.microsoft.com/en-us/library/hh847877.aspx) module to generate and validate windows catalog files.</span></span>

## <a name="new-filecatalog"></a><span data-ttu-id="f6ab9-105">New-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="f6ab9-105">New-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="f6ab9-106">`New-FileCatalog` létrehoz egy windows catalog mappák és fájlok.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-106">`New-FileCatalog` creates a windows catalog file for set of folders and files.</span></span> <span data-ttu-id="f6ab9-107">A katalógusban az összes fájl megadott elérési utak a kivonatok tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-107">A catalog file contains hashes for all files in specified paths.</span></span> <span data-ttu-id="f6ab9-108">Mappák és a katalógus fájl ezeken a mappákon jelölő megfelelő készletét terjeszthetnek.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-108">Users can distribute the set of folders along with corresponding the catalog file that represents those folders.</span></span> <span data-ttu-id="f6ab9-109">Egy katalógusfájlt segítségével tartalom címzettje ellenőrzi, hogy a módosítások a mappákat a katalógus létrehozása után.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-109">A catalog file can be used by the recipient of content to validate whether any changes were made to the folders after the catalog was created.</span></span>

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
<span data-ttu-id="f6ab9-110">1. és 2 létrehozása katalógus verziója támogatott.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-110">We support creating catalog version 1 and 2.</span></span> <span data-ttu-id="f6ab9-111">1-es verziójú SHA1 kivonatoló algoritmust használ fájlkivonat és 2 használ SHA256 verzió létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-111">Version 1 uses SHA1 hashing algorithm to create file hashes and version 2 uses SHA256.</span></span> <span data-ttu-id="f6ab9-112">Katalógus 2-es verzió nem támogatott a *Windows Server 2008 R2* és *Windows 7*.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-112">Catalog version 2 is not supported on *Windows Server 2008 R2* and *Windows 7*.</span></span> <span data-ttu-id="f6ab9-113">Javasoljuk, hogy a katalógus 2-es verzióját használja, ha platformokat használó *Windows 8*, *Windows Server 2012* vagy újabb verzió.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-113">It is recommended to use catalog version 2 if using platforms *Windows 8*, *Windows Server 2012* and above.</span></span>

<span data-ttu-id="f6ab9-114">Egy meglévő modul ezen parancs használatához adja meg kell egyeznie a moduljegyzékben helyét CatalogFilePath és az elérési utat változókat.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-114">To use this command on an existing module, specify the CatalogFilePath and Path variables to match the location of the module manifest.</span></span> <span data-ttu-id="f6ab9-115">Az alábbi példában a moduljegyzékben C:\Program Files\Windows PowerShell\Modules\Pester van.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-115">In the example below, the module manifest is in C:\Program Files\Windows PowerShell\Modules\Pester.</span></span>

![](../images/NewFileCatalog.jpg)

<span data-ttu-id="f6ab9-116">Ez a katalógus fájlt hoz létre.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-116">This creates the catalog file.</span></span>

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

<span data-ttu-id="f6ab9-117">Egy katalógusfájlt (Pester.cat a fenti exmaple) sértetlenségének ellenőrzése, alá kell írni használatával a [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-117">To verify the integrity of a catalog file (Pester.cat in above exmaple) it should be signed using the [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) cmdlet.</span></span>


## <a name="test-filecatalog"></a><span data-ttu-id="f6ab9-118">Test-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="f6ab9-118">Test-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="f6ab9-119">`Test-FileCatalog` a katalógus képviselő mappákat ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-119">`Test-FileCatalog` validates the catalog representing a set of folders.</span></span>

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

<span data-ttu-id="f6ab9-120">Ez a parancsmag összehasonlítja a kivonatok összes fájl és a relatív elérési utak azokat, lemezre menti a katalógus fájlban található.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-120">This cmdlet compares the hashes of all files and their relative paths found in the catalog file with ones saved to disk.</span></span> <span data-ttu-id="f6ab9-121">Ha a fájlkivonat és elérési utak bármely eltérést észlel állapotot adja vissza `ValidationFailed`.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-121">If it detects any mismatch between file hashes and paths it returns a status of `ValidationFailed`.</span></span>
<span data-ttu-id="f6ab9-122">Felhasználók tudják lekérni az összes ezek az adatokat a a `Detailed` váltani.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-122">Users can retrieve all this information using the `Detailed` switch.</span></span> <span data-ttu-id="f6ab9-123">A katalógus aláírási állapot jelenik meg a `Signature` mező, amely ugyanaz, mint a hívása a [Get-AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) parancsmag a katalógus fájlra.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-123">The signing status of the catalog is displayed as the `Signature` field, which is same as calling the [Get-AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) cmdlet on the catalog file.</span></span>
<span data-ttu-id="f6ab9-124">Felhasználók is hagyhatja a fájl ellenőrzésekor használatával a `FilesToSkip` paraméter.</span><span class="sxs-lookup"><span data-stu-id="f6ab9-124">Users can also skip any file during validation by using the `FilesToSkip` parameter.</span></span>
