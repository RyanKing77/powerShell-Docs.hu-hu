---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISEFileCollection objektum
ms.assetid: 0f86a427-ea38-4bce-85f8-06c98d30d508
ms.openlocfilehash: 60bf4dae33f3a71c31e7fdbed0f4fd6ab27a8bd1
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="the-isefilecollection-object"></a><span data-ttu-id="2cbdb-103">A ISEFileCollection objektum</span><span class="sxs-lookup"><span data-stu-id="2cbdb-103">The ISEFileCollection Object</span></span>
  <span data-ttu-id="2cbdb-104">A **ISEFileCollection** objektum gyűjteménye **ISEFile** objektumok.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-104">The **ISEFileCollection** object is a collection of **ISEFile** objects.</span></span> <span data-ttu-id="2cbdb-105">Példa: a $psISE.CurrentPowerShellTab.Files gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-105">An example is the $psISE.CurrentPowerShellTab.Files collection.</span></span>

## <a name="methods"></a><span data-ttu-id="2cbdb-106">Metódusok</span><span class="sxs-lookup"><span data-stu-id="2cbdb-106">Methods</span></span>

### <a name="add-fullpath-"></a><span data-ttu-id="2cbdb-107">Adja hozzá\( \[fullPath\]\)</span><span class="sxs-lookup"><span data-stu-id="2cbdb-107">Add\( \[fullPath\] \)</span></span>
  <span data-ttu-id="2cbdb-108">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="2cbdb-109">Hoz létre, és adja vissza egy új névtelen fájlt, és hozzáadja azt a gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-109">Creates and returns a new untitled file and adds it to the collection.</span></span> <span data-ttu-id="2cbdb-110">A **IsUntitled** az újonnan létrehozott fájl tulajdonsága **$true**.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-110">The **IsUntitled** property of the newly created file is **$true**.</span></span>

 <span data-ttu-id="2cbdb-111">**\[fullPath\]**  – nem kötelező a fájl a teljes mértékben megadott elérési út karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-111">**\[fullPath\]** - Optional string The fully specified path of the file.</span></span> <span data-ttu-id="2cbdb-112">Kivétel jön létre, ha megadja a **fullPath** paraméter és egy relatív elérési utat, vagy ha egy fájl neve helyett a teljes elérési útja.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-112">An exception is generated if you include the **fullPath** parameter and a relative path, or if you use a file name instead of the full path.</span></span>

```
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")

```

### <a name="remove-file-force-"></a><span data-ttu-id="2cbdb-113">Távolítsa el\( fájl, \[kényszerített\]\)</span><span class="sxs-lookup"><span data-stu-id="2cbdb-113">Remove\( File, \[Force\] \)</span></span>
  <span data-ttu-id="2cbdb-114">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="2cbdb-115">A megadott fájl eltávolítja a jelenlegi PowerShell fülre.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-115">Removes a specified file from the current PowerShell tab.</span></span>

 <span data-ttu-id="2cbdb-116">**Fájl** -karakterlánc az ISEFile fájlt, hogy el szeretné távolítani a gyűjteményből.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-116">**File** - String The ISEFile file that you want to remove from the collection.</span></span> <span data-ttu-id="2cbdb-117">Ha még nem mentette a fájlt, akkor ez a metódus kivételt jelez.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-117">If the file has not been saved, this method throws an exception.</span></span> <span data-ttu-id="2cbdb-118">Használja a **kényszerítése** paraméter a nem mentett fájlok eltávolításának kényszerítése, váltani.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-118">Use the **Force** switch parameter to force the removal of an unsaved file.</span></span>

 <span data-ttu-id="2cbdb-119">**\[Kényszerített\]**  -választható logikai Ha **$true**, távolítsa el a fájlt, akkor is, ha nem mentette után utolsó használata engedélyt.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-119">**\[Force\]** - optional Boolean If set to **$true**, grants permission to remove the file even if it has not been saved after last use.</span></span> <span data-ttu-id="2cbdb-120">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-120">The default is **$false**.</span></span>

```
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a><span data-ttu-id="2cbdb-121">SetSelectedFile\( selectedFile\)</span><span class="sxs-lookup"><span data-stu-id="2cbdb-121">SetSelectedFile\( selectedFile \)</span></span>
  <span data-ttu-id="2cbdb-122">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-122">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="2cbdb-123">A megadott fájl kiválasztja a **selectedFile** paraméter.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-123">Selects the file that is specified by the **selectedFile** parameter.</span></span>

 <span data-ttu-id="2cbdb-124">**selectedFile** -Microsoft.PowerShell.Host.ISE.ISEFile a ISEFile fájl, amely azt szeretné kiválasztani.</span><span class="sxs-lookup"><span data-stu-id="2cbdb-124">**selectedFile** - Microsoft.PowerShell.Host.ISE.ISEFile The ISEFile file that you want to select.</span></span>

```

# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)

```

## <a name="see-also"></a><span data-ttu-id="2cbdb-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2cbdb-125">See Also</span></span>
- [<span data-ttu-id="2cbdb-126">A ISEFile objektum</span><span class="sxs-lookup"><span data-stu-id="2cbdb-126">The ISEFile Object</span></span>](The-ISEFile-Object.md) 
- [<span data-ttu-id="2cbdb-127">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="2cbdb-127">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="2cbdb-128">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="2cbdb-128">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="2cbdb-129">A ISE objektum modell hierarchia</span><span class="sxs-lookup"><span data-stu-id="2cbdb-129">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
