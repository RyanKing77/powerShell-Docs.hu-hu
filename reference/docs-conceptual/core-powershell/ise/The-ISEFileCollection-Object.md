---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISEFileCollection objektum
ms.assetid: 0f86a427-ea38-4bce-85f8-06c98d30d508
ms.openlocfilehash: eb4b2784820cbe51f662fd2fd945d8760ef9dbff
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953089"
---
# <a name="the-isefilecollection-object"></a><span data-ttu-id="3e275-103">Az ISEFileCollection objektum</span><span class="sxs-lookup"><span data-stu-id="3e275-103">The ISEFileCollection Object</span></span>

<span data-ttu-id="3e275-104">A **ISEFileCollection** objektum gyűjteménye **ISEFile** objektumok.</span><span class="sxs-lookup"><span data-stu-id="3e275-104">The **ISEFileCollection** object is a collection of **ISEFile** objects.</span></span> <span data-ttu-id="3e275-105">Példa: a $psISE.CurrentPowerShellTab.Files gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="3e275-105">An example is the $psISE.CurrentPowerShellTab.Files collection.</span></span>

## <a name="methods"></a><span data-ttu-id="3e275-106">Metódusok</span><span class="sxs-lookup"><span data-stu-id="3e275-106">Methods</span></span>

### <a name="add-fullpath-"></a><span data-ttu-id="3e275-107">Add\( \[fullPath\] \)</span><span class="sxs-lookup"><span data-stu-id="3e275-107">Add\( \[fullPath\] \)</span></span>

<span data-ttu-id="3e275-108">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3e275-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3e275-109">Hoz létre, és adja vissza egy új névtelen fájlt, és hozzáadja azt a gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="3e275-109">Creates and returns a new untitled file and adds it to the collection.</span></span> <span data-ttu-id="3e275-110">A **IsUntitled** az újonnan létrehozott fájl tulajdonsága **$true**.</span><span class="sxs-lookup"><span data-stu-id="3e275-110">The **IsUntitled** property of the newly created file is **$true**.</span></span>

<span data-ttu-id="3e275-111">**\[fullPath\]**  – nem kötelező a fájl a teljes mértékben megadott elérési út karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="3e275-111">**\[fullPath\]** - Optional string The fully specified path of the file.</span></span> <span data-ttu-id="3e275-112">Kivétel jön létre, ha megadja a **fullPath** paraméter és egy relatív elérési utat, vagy ha egy fájl neve helyett a teljes elérési útja.</span><span class="sxs-lookup"><span data-stu-id="3e275-112">An exception is generated if you include the **fullPath** parameter and a relative path, or if you use a file name instead of the full path.</span></span>

```powershell
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")
```

### <a name="remove-file-force-"></a><span data-ttu-id="3e275-113">Távolítsa el\( fájl, \[kényszerítése\] \)</span><span class="sxs-lookup"><span data-stu-id="3e275-113">Remove\( File, \[Force\] \)</span></span>

<span data-ttu-id="3e275-114">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3e275-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3e275-115">A megadott fájl eltávolítja a jelenlegi PowerShell fülre.</span><span class="sxs-lookup"><span data-stu-id="3e275-115">Removes a specified file from the current PowerShell tab.</span></span>

<span data-ttu-id="3e275-116">**Fájl** -karakterlánc az ISEFile fájlt, hogy el szeretné távolítani a gyűjteményből.</span><span class="sxs-lookup"><span data-stu-id="3e275-116">**File** - String The ISEFile file that you want to remove from the collection.</span></span> <span data-ttu-id="3e275-117">Ha még nem mentette a fájlt, akkor ez a metódus kivételt jelez.</span><span class="sxs-lookup"><span data-stu-id="3e275-117">If the file has not been saved, this method throws an exception.</span></span> <span data-ttu-id="3e275-118">Használja a **kényszerítése** paraméter a nem mentett fájlok eltávolításának kényszerítése, váltani.</span><span class="sxs-lookup"><span data-stu-id="3e275-118">Use the **Force** switch parameter to force the removal of an unsaved file.</span></span>

<span data-ttu-id="3e275-119">**\[Kényszerített\]**  -választható logikai Ha **$true**, távolítsa el a fájlt, akkor is, ha nem mentette után utolsó használata engedélyt.</span><span class="sxs-lookup"><span data-stu-id="3e275-119">**\[Force\]** - optional Boolean If set to **$true**, grants permission to remove the file even if it has not been saved after last use.</span></span> <span data-ttu-id="3e275-120">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="3e275-120">The default is **$false**.</span></span>

```powershell
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a><span data-ttu-id="3e275-121">SetSelectedFile\( selectedFile \)</span><span class="sxs-lookup"><span data-stu-id="3e275-121">SetSelectedFile\( selectedFile \)</span></span>

<span data-ttu-id="3e275-122">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3e275-122">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3e275-123">A megadott fájl kiválasztja a **selectedFile** paraméter.</span><span class="sxs-lookup"><span data-stu-id="3e275-123">Selects the file that is specified by the **selectedFile** parameter.</span></span>

<span data-ttu-id="3e275-124">**selectedFile** -Microsoft.PowerShell.Host.ISE.ISEFile a ISEFile fájl, amely azt szeretné kiválasztani.</span><span class="sxs-lookup"><span data-stu-id="3e275-124">**selectedFile** - Microsoft.PowerShell.Host.ISE.ISEFile The ISEFile file that you want to select.</span></span>

```powershell
# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)
```

## <a name="see-also"></a><span data-ttu-id="3e275-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3e275-125">See Also</span></span>

- [<span data-ttu-id="3e275-126">A ISEFile objektum</span><span class="sxs-lookup"><span data-stu-id="3e275-126">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="3e275-127">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="3e275-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="3e275-128">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="3e275-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)