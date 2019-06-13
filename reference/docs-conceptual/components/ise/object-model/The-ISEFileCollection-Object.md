---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEFileCollection objektum
ms.openlocfilehash: 96db51ee921cc0fa34803091d563bc6e118643b6
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030513"
---
# <a name="the-isefilecollection-object"></a><span data-ttu-id="21f16-103">Az ISEFileCollection objektum</span><span class="sxs-lookup"><span data-stu-id="21f16-103">The ISEFileCollection Object</span></span>

<span data-ttu-id="21f16-104">A **ISEFileCollection** objektum olyan gyűjteménye, **ISEFile** objektumokat.</span><span class="sxs-lookup"><span data-stu-id="21f16-104">The **ISEFileCollection** object is a collection of **ISEFile** objects.</span></span> <span data-ttu-id="21f16-105">An example is the $psISE.CurrentPowerShellTab.Files collection.</span><span class="sxs-lookup"><span data-stu-id="21f16-105">An example is the $psISE.CurrentPowerShellTab.Files collection.</span></span>

## <a name="methods"></a><span data-ttu-id="21f16-106">Metódusok</span><span class="sxs-lookup"><span data-stu-id="21f16-106">Methods</span></span>

### <a name="add-fullpath-"></a><span data-ttu-id="21f16-107">Adjon hozzá\( \[fullPath\] \)</span><span class="sxs-lookup"><span data-stu-id="21f16-107">Add\( \[fullPath\] \)</span></span>

<span data-ttu-id="21f16-108">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="21f16-108">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="21f16-109">Hoz létre, és adja vissza egy új cím nélküli fájl, és hozzáadja azt a gyűjteményt.</span><span class="sxs-lookup"><span data-stu-id="21f16-109">Creates and returns a new untitled file and adds it to the collection.</span></span> <span data-ttu-id="21f16-110">A **IsUntitled** tulajdonság az újonnan létrehozott fájl **$true**.</span><span class="sxs-lookup"><span data-stu-id="21f16-110">The **IsUntitled** property of the newly created file is **$true**.</span></span>

<span data-ttu-id="21f16-111">**\[fullPath\]**  – nem kötelező a megadott teljes mértékben a fájl elérési útját karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="21f16-111">**\[fullPath\]** - Optional string The fully specified path of the file.</span></span> <span data-ttu-id="21f16-112">Kivétel akkor jön létre, ha a **fullPath** paraméter és a egy relatív elérési utat, vagy ha egy fájl neve helyett a teljes elérési útja.</span><span class="sxs-lookup"><span data-stu-id="21f16-112">An exception is generated if you include the **fullPath** parameter and a relative path, or if you use a file name instead of the full path.</span></span>

```powershell
# Adds a new untitled file to the collection of files in the current PowerShell tab.
$newFile = $psISE.CurrentPowerShellTab.Files.Add()

# Adds a file specified by its full path to the collection of files in the current PowerShell tab.
$psISE.CurrentPowerShellTab.Files.Add("$pshome\Examples\profile.ps1")
```

### <a name="remove-file-force-"></a><span data-ttu-id="21f16-113">Távolítsa el\( fájl \[kényszerítése\] \)</span><span class="sxs-lookup"><span data-stu-id="21f16-113">Remove\( File, \[Force\] \)</span></span>

<span data-ttu-id="21f16-114">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="21f16-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="21f16-115">Eltávolítja a megadott fájl az aktuális PowerShell-lapon.</span><span class="sxs-lookup"><span data-stu-id="21f16-115">Removes a specified file from the current PowerShell tab.</span></span>

<span data-ttu-id="21f16-116">**Fájl** -karakterlánc az ISEFile fájlt, amelyet szeretne eltávolítása a gyűjteményből.</span><span class="sxs-lookup"><span data-stu-id="21f16-116">**File** - String The ISEFile file that you want to remove from the collection.</span></span> <span data-ttu-id="21f16-117">Ha a fájl nem lett mentve, ez a metódus kivételt jelez.</span><span class="sxs-lookup"><span data-stu-id="21f16-117">If the file has not been saved, this method throws an exception.</span></span> <span data-ttu-id="21f16-118">Használja a **kényszerítése** váltson paraméter egy nem mentett fájlt, az Eltávolítás kényszerítése.</span><span class="sxs-lookup"><span data-stu-id="21f16-118">Use the **Force** switch parameter to force the removal of an unsaved file.</span></span>

<span data-ttu-id="21f16-119">**\[Kényszerített\]**  – nem kötelező logikai Ha **$true**, engedélyt ad a fájl eltávolítása, még akkor is, ha azt nem lett mentve utolsó használat után.</span><span class="sxs-lookup"><span data-stu-id="21f16-119">**\[Force\]** - optional Boolean If set to **$true**, grants permission to remove the file even if it has not been saved after last use.</span></span> <span data-ttu-id="21f16-120">Az alapértelmezett érték **$false**.</span><span class="sxs-lookup"><span data-stu-id="21f16-120">The default is **$false**.</span></span>

```powershell
# Removes the first opened file from the file collection associated with the current PowerShell tab.
# If the file has not yet been saved, then an exception is generated.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile)

# Removes the first opened file from the file collection associated with the current PowerShell tab, even if it has not been saved.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.Remove($firstfile, $true)
```

### <a name="setselectedfile-selectedfile-"></a><span data-ttu-id="21f16-121">SetSelectedFile\( selectedFile \)</span><span class="sxs-lookup"><span data-stu-id="21f16-121">SetSelectedFile\( selectedFile \)</span></span>

<span data-ttu-id="21f16-122">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="21f16-122">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="21f16-123">A megadott fájlt választja ki a **selectedFile** paraméter.</span><span class="sxs-lookup"><span data-stu-id="21f16-123">Selects the file that is specified by the **selectedFile** parameter.</span></span>

<span data-ttu-id="21f16-124">**selectedFile** -Microsoft.PowerShell.Host.ISE.ISEFile az ISEFile fájlt, amely azt szeretné kiválasztani.</span><span class="sxs-lookup"><span data-stu-id="21f16-124">**selectedFile** - Microsoft.PowerShell.Host.ISE.ISEFile The ISEFile file that you want to select.</span></span>

```powershell
# Selects the specified file.
$firstfile = $psISE.CurrentPowerShellTab.Files[0]
$psISE.CurrentPowerShellTab.Files.SetSelectedFile($firstfile)
```

## <a name="see-also"></a><span data-ttu-id="21f16-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="21f16-125">See Also</span></span>

- [<span data-ttu-id="21f16-126">Az ISEFile objektum</span><span class="sxs-lookup"><span data-stu-id="21f16-126">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="21f16-127">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="21f16-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="21f16-128">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="21f16-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
