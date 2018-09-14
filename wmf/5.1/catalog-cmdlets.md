---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: Katalógusbeli parancsmagok
ms.openlocfilehash: ec5fc866fe27a894b23b93d3ea46ad9c0cba288e
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522888"
---
# <a name="catalog-cmdlets"></a><span data-ttu-id="ad12b-103">Katalógusbeli parancsmagok</span><span class="sxs-lookup"><span data-stu-id="ad12b-103">Catalog Cmdlets</span></span>

<span data-ttu-id="ad12b-104">A két új parancsmag új verziója [Microsoft.Powershell.Secuity](https://technet.microsoft.com/library/hh847877.aspx) modul hozza létre, és a windows katalógusban fájlok érvényesítése.</span><span class="sxs-lookup"><span data-stu-id="ad12b-104">We have added two new cmdlets in [Microsoft.Powershell.Secuity](https://technet.microsoft.com/library/hh847877.aspx) module to generate and validate windows catalog files.</span></span>

## <a name="new-filecatalog"></a><span data-ttu-id="ad12b-105">New-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="ad12b-105">New-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="ad12b-106">`New-FileCatalog` létrehoz egy windows katalógusfájlt az tartozó fájlok és mappák.</span><span class="sxs-lookup"><span data-stu-id="ad12b-106">`New-FileCatalog` creates a windows catalog file for set of folders and files.</span></span> <span data-ttu-id="ad12b-107">A katalógus-kivonat a megadott elérési utak lévő összes fájlt tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="ad12b-107">A catalog file contains hashes for all files in specified paths.</span></span> <span data-ttu-id="ad12b-108">A katalógus fájl mappákat jelölő megfelelő együtt mappakészlet terjeszthetnek.</span><span class="sxs-lookup"><span data-stu-id="ad12b-108">Users can distribute the set of folders along with corresponding the catalog file that represents those folders.</span></span> <span data-ttu-id="ad12b-109">Egy katalógusfájlt megállapítani, hogy e módosítások történtek a mappákat a katalógus létrehozása után használhatják a címzett tartalom.</span><span class="sxs-lookup"><span data-stu-id="ad12b-109">A catalog file can be used by the recipient of content to validate whether any changes were made to the folders after the catalog was created.</span></span>

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
<span data-ttu-id="ad12b-110">1. és 2 létrehozása katalógus-verzió is támogatott.</span><span class="sxs-lookup"><span data-stu-id="ad12b-110">We support creating catalog version 1 and 2.</span></span> <span data-ttu-id="ad12b-111">1. verziójának SHA1 kivonatoló algoritmust használja fájlkivonatokkal és verzió 2 használja SHA256 létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="ad12b-111">Version 1 uses SHA1 hashing algorithm to create file hashes and version 2 uses SHA256.</span></span> <span data-ttu-id="ad12b-112">Katalógus 2-es verzió nem támogatott az *Windows Server 2008 R2* és *Windows 7*.</span><span class="sxs-lookup"><span data-stu-id="ad12b-112">Catalog version 2 is not supported on *Windows Server 2008 R2* and *Windows 7*.</span></span> <span data-ttu-id="ad12b-113">Javasoljuk, hogy ha platformok használja a katalógus 2-es verziójú *Windows 8*, *Windows Server 2012* vagy újabb verzió.</span><span class="sxs-lookup"><span data-stu-id="ad12b-113">It is recommended to use catalog version 2 if using platforms *Windows 8*, *Windows Server 2012* and above.</span></span>

<span data-ttu-id="ad12b-114">Ezzel a paranccsal egy meglévő modulon használatához adja meg a moduljegyzékben helyének megfelelően CatalogFilePath és az elérési út változókat.</span><span class="sxs-lookup"><span data-stu-id="ad12b-114">To use this command on an existing module, specify the CatalogFilePath and Path variables to match the location of the module manifest.</span></span> <span data-ttu-id="ad12b-115">Az alábbi példában a moduljegyzékben C:\Program Files\Windows PowerShell\Modules\Pester szerepel.</span><span class="sxs-lookup"><span data-stu-id="ad12b-115">In the example below, the module manifest is in C:\Program Files\Windows PowerShell\Modules\Pester.</span></span>

![](../images/NewFileCatalog.jpg)

<span data-ttu-id="ad12b-116">Ez a katalógus fájlt hoz létre.</span><span class="sxs-lookup"><span data-stu-id="ad12b-116">This creates the catalog file.</span></span>

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

<span data-ttu-id="ad12b-117">Egy katalógusfájlt (Pester.cat a fenti példában) sértetlenségének ellenőrzése, alá kell írni használatával a [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="ad12b-117">To verify the integrity of a catalog file (Pester.cat in above exmaple) it should be signed using the [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) cmdlet.</span></span>


## <a name="test-filecatalog"></a><span data-ttu-id="ad12b-118">Test-FileCatalog</span><span class="sxs-lookup"><span data-stu-id="ad12b-118">Test-FileCatalog</span></span>
--------------------------------

<span data-ttu-id="ad12b-119">`Test-FileCatalog` a katalógus jelölő mappákat ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="ad12b-119">`Test-FileCatalog` validates the catalog representing a set of folders.</span></span>

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

<span data-ttu-id="ad12b-120">Ez a parancsmag összehasonlítja a kivonatok, és azok relatív elérési utakat azokról, lemezre menti a katalógus fájlban található összes fájlt.</span><span class="sxs-lookup"><span data-stu-id="ad12b-120">This cmdlet compares the hashes of all files and their relative paths found in the catalog file with ones saved to disk.</span></span> <span data-ttu-id="ad12b-121">Ha azt észleli, hogy bármely fájlkivonatokkal és elérési utak nem egyezik a állapotát adja vissza `ValidationFailed`.</span><span class="sxs-lookup"><span data-stu-id="ad12b-121">If it detects any mismatch between file hashes and paths it returns a status of `ValidationFailed`.</span></span>
<span data-ttu-id="ad12b-122">Felhasználók kérheti le az összes ezen információk használatával a `Detailed` váltani.</span><span class="sxs-lookup"><span data-stu-id="ad12b-122">Users can retrieve all this information using the `Detailed` switch.</span></span> <span data-ttu-id="ad12b-123">Aláíró állapotát, a katalógusban elemnél a `Signature` mező, amely ugyanaz, mint a hívása a [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx) katalógusfájl parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="ad12b-123">The signing status of the catalog is displayed as the `Signature` field, which is same as calling the [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx) cmdlet on the catalog file.</span></span>
<span data-ttu-id="ad12b-124">Felhasználók ki is hagyhatja bármely fájl ellenőrzésekor használatával a `FilesToSkip` paraméter.</span><span class="sxs-lookup"><span data-stu-id="ad12b-124">Users can also skip any file during validation by using the `FilesToSkip` parameter.</span></span>
