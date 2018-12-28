---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEFileCollection objektum
ms.assetid: 0f86a427-ea38-4bce-85f8-06c98d30d508
ms.openlocfilehash: eb4b2784820cbe51f662fd2fd945d8760ef9dbff
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53405589"
---
# <a name="the-isefilecollection-object"></a><span data-ttu-id="0f9ee-103">Az ISEFileCollection objektum</span><span class="sxs-lookup"><span data-stu-id="0f9ee-103">The ISEFileCollection Object</span></span>

<span data-ttu-id="0f9ee-104">A **ISEFileCollection** objektum olyan gyűjteménye, **ISEFile** objektumokat.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-104">The **ISEFileCollection** object is a collection of **ISEFile** objects.</span></span> <span data-ttu-id="0f9ee-105">Például az a $psISE.CurrentPowerShellTab.Files gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-105">An example is the $psISE.CurrentPowerShellTab.Files collection.</span></span>

## <a name="methods"></a><span data-ttu-id="0f9ee-106">Metódusok</span><span class="sxs-lookup"><span data-stu-id="0f9ee-106">Methods</span></span>

### <a name="add-fullpath-"></a><span data-ttu-id="0f9ee-107">Adjon hozzá\( \[fullPath\] \)</span><span class="sxs-lookup"><span data-stu-id="0f9ee-107">Add\( \[fullPath\] \)</span></span>

<span data-ttu-id="0f9ee-108">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0f9ee-109">Hoz létre, és adja vissza egy új cím nélküli fájl, és hozzáadja azt a gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-109">Creates and returns a new untitled file and adds it to the collection.</span></span> <span data-ttu-id="0f9ee-110">A **IsUntitled** tulajdonság az újonnan létrehozott fájl **$true**.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-110">The **IsUntitled** property of the newly created file is **$true**.</span></span>

<span data-ttu-id="0f9ee-111">**\[fullPath\]**  – nem kötelező a megadott teljes mértékben a fájl elérési útját karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-111">**\[fullPath\]** - Optional string The fully specified path of the file.</span></span> <span data-ttu-id="0f9ee-112">Kivétel akkor jön létre, ha a **fullPath** paraméter és a egy relatív elérési utat, vagy ha egy fájl neve helyett a teljes elérési útja.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-112">An exception is generated if you include the **fullPath** parameter and a relative path, or if you use a file name instead of the full path.</span></span>

```powershell
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")
```

### <a name="remove-file-force-"></a><span data-ttu-id="0f9ee-113">Távolítsa el\( fájl \[kényszerítése\] \)</span><span class="sxs-lookup"><span data-stu-id="0f9ee-113">Remove\( File, \[Force\] \)</span></span>

<span data-ttu-id="0f9ee-114">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0f9ee-115">Eltávolítja a megadott fájl az aktuális PowerShell-lapon.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-115">Removes a specified file from the current PowerShell tab.</span></span>

<span data-ttu-id="0f9ee-116">**Fájl** -karakterlánc az ISEFile fájlt, amelyet szeretne eltávolítása a gyűjteményből.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-116">**File** - String The ISEFile file that you want to remove from the collection.</span></span> <span data-ttu-id="0f9ee-117">Ha a fájl nem lett mentve, ez a metódus kivételt jelez.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-117">If the file has not been saved, this method throws an exception.</span></span> <span data-ttu-id="0f9ee-118">Használja a **kényszerítése** váltson paraméter egy nem mentett fájlt, az Eltávolítás kényszerítése.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-118">Use the **Force** switch parameter to force the removal of an unsaved file.</span></span>

<span data-ttu-id="0f9ee-119">**\[Kényszerített\]**  – nem kötelező logikai Ha **$true**, engedélyt ad a fájl eltávolítása, még akkor is, ha azt nem lett mentve utolsó használat után.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-119">**\[Force\]** - optional Boolean If set to **$true**, grants permission to remove the file even if it has not been saved after last use.</span></span> <span data-ttu-id="0f9ee-120">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-120">The default is **$false**.</span></span>

```powershell
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a><span data-ttu-id="0f9ee-121">SetSelectedFile\( selectedFile \)</span><span class="sxs-lookup"><span data-stu-id="0f9ee-121">SetSelectedFile\( selectedFile \)</span></span>

<span data-ttu-id="0f9ee-122">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-122">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="0f9ee-123">A megadott fájlt választja ki a **selectedFile** paraméter.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-123">Selects the file that is specified by the **selectedFile** parameter.</span></span>

<span data-ttu-id="0f9ee-124">**selectedFile** -Microsoft.PowerShell.Host.ISE.ISEFile az ISEFile fájlt, amely azt szeretné kiválasztani.</span><span class="sxs-lookup"><span data-stu-id="0f9ee-124">**selectedFile** - Microsoft.PowerShell.Host.ISE.ISEFile The ISEFile file that you want to select.</span></span>

```powershell
# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)
```

## <a name="see-also"></a><span data-ttu-id="0f9ee-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0f9ee-125">See Also</span></span>

- [<span data-ttu-id="0f9ee-126">Az ISEFile objektum</span><span class="sxs-lookup"><span data-stu-id="0f9ee-126">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="0f9ee-127">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="0f9ee-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="0f9ee-128">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="0f9ee-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)