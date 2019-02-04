---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEFile objektum
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: 24549720b8bc35435882533b0eb138de432ede65
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685136"
---
# <a name="the-isefile-object"></a><span data-ttu-id="32543-103">Az ISEFile objektum</span><span class="sxs-lookup"><span data-stu-id="32543-103">The ISEFile Object</span></span>

<span data-ttu-id="32543-104">Egy **ISEFile** objektum egy fájlt a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE) jelöl.</span><span class="sxs-lookup"><span data-stu-id="32543-104">An **ISEFile** object represents a file in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="32543-105">Fontos a Microsoft.PowerShell.Host.ISE.ISEFile osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="32543-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span> <span data-ttu-id="32543-106">Ez a témakör felsorolja a tag módszerek és a tag tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="32543-106">This topic lists its member methods and member properties.</span></span> <span data-ttu-id="32543-107">A **$psISE.CurrentFile** , és a fájlok a fájlok gyűjteményben, a PowerShell-lap Microsoft.PowerShell.Host.ISE.ISEFile osztály összes példányánál.</span><span class="sxs-lookup"><span data-stu-id="32543-107">The **$psISE.CurrentFile** and the files in the Files collection in a PowerShell tab are all instances of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span>

## <a name="methods"></a><span data-ttu-id="32543-108">Metódusok</span><span class="sxs-lookup"><span data-stu-id="32543-108">Methods</span></span>

### <a name="save-saveencoding-"></a><span data-ttu-id="32543-109">Mentés\( \[saveEncoding\] \)</span><span class="sxs-lookup"><span data-stu-id="32543-109">Save\( \[saveEncoding\] \)</span></span>

<span data-ttu-id="32543-110">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="32543-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="32543-111">Lemezre menti a fájlt.</span><span class="sxs-lookup"><span data-stu-id="32543-111">Saves the file to disk.</span></span>

<span data-ttu-id="32543-112">**\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező karakterkódolást a mentett fájlt használható paraméter azonosítására.</span><span class="sxs-lookup"><span data-stu-id="32543-112">**\[saveEncoding\]** - optional [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="32543-113">Az alapértelmezett érték **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="32543-113">The default value is **UTF8**.</span></span>

### <a name="exceptions"></a><span data-ttu-id="32543-114">Kivételek</span><span class="sxs-lookup"><span data-stu-id="32543-114">Exceptions</span></span>

- <span data-ttu-id="32543-115">**System.IO.IOException**: A fájl nem menthető.</span><span class="sxs-lookup"><span data-stu-id="32543-115">**System.IO.IOException**: The file could not be saved.</span></span>

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a><span data-ttu-id="32543-116">SaveAs\(filename, \[saveEncoding\]\)</span><span class="sxs-lookup"><span data-stu-id="32543-116">SaveAs\(filename, \[saveEncoding\]\)</span></span>

<span data-ttu-id="32543-117">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="32543-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="32543-118">Menti a fájlt a megadott fájlnévvel és a kódolást.</span><span class="sxs-lookup"><span data-stu-id="32543-118">Saves the file with the specified file name and encoding.</span></span>

<span data-ttu-id="32543-119">**Fájlnév** -karakterlánc, a fájl mentéséhez használni kívánt nevét.</span><span class="sxs-lookup"><span data-stu-id="32543-119">**filename** - String The name to be used to save the file.</span></span>

<span data-ttu-id="32543-120">**\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező karakterkódolást a mentett fájlt használható paraméter azonosítására.</span><span class="sxs-lookup"><span data-stu-id="32543-120">**\[saveEncoding\]** - optional [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="32543-121">Az alapértelmezett érték **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="32543-121">The default value is **UTF8**.</span></span>

### <a name="exceptions"></a><span data-ttu-id="32543-122">Kivételek</span><span class="sxs-lookup"><span data-stu-id="32543-122">Exceptions</span></span>

- <span data-ttu-id="32543-123">**System.ArgumentNullException**: A **filename** paraméter null értékű.</span><span class="sxs-lookup"><span data-stu-id="32543-123">**System.ArgumentNullException**: The **filename** parameter is null.</span></span>
- <span data-ttu-id="32543-124">**System.ArgumentException**: A **filename** paraméter értéke üres.</span><span class="sxs-lookup"><span data-stu-id="32543-124">**System.ArgumentException**: The **filename** parameter is empty.</span></span>
- <span data-ttu-id="32543-125">**System.IO.IOException**: A fájl nem menthető.</span><span class="sxs-lookup"><span data-stu-id="32543-125">**System.IO.IOException**: The file could not be saved.</span></span>

```powershell
# Save the file with a full path and name.
$fullpath = "c:\temp\newname.txt"
$psISE.CurrentFile.SaveAs($fullPath)
# Save the file with a full path and name and explicitly as UTF8.
$psISE.CurrentFile.SaveAs($fullPath, [System.Text.Encoding]::UTF8)
```

## <a name="properties"></a><span data-ttu-id="32543-126">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="32543-126">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="32543-127">DisplayName</span><span class="sxs-lookup"><span data-stu-id="32543-127">DisplayName</span></span>

<span data-ttu-id="32543-128">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="32543-128">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="32543-129">A csak olvasható tulajdonság, amely lekérdezi a karakterlánc, amely tartalmazza ezt a fájlt a megjelenítendő nevét.</span><span class="sxs-lookup"><span data-stu-id="32543-129">The read-only property that gets the string that contains the display name of this file.</span></span> <span data-ttu-id="32543-130">A név jelenik meg a **fájl** szerkesztő a felső fülön.</span><span class="sxs-lookup"><span data-stu-id="32543-130">The name is shown on the **File** tab at the top of the editor.</span></span> <span data-ttu-id="32543-131">A csillag jelenléte \( \* \) a név végén azt jelzi, hogy a fájl rendelkezik-e a nem mentett módosításokat.</span><span class="sxs-lookup"><span data-stu-id="32543-131">The presence of an asterisk \(\*\) at the end of the name indicates that the file has changes that have not been saved.</span></span>

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a><span data-ttu-id="32543-132">Szerkesztő</span><span class="sxs-lookup"><span data-stu-id="32543-132">Editor</span></span>

<span data-ttu-id="32543-133">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="32543-133">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="32543-134">A csak olvasható tulajdonság, amely lekérdezi a [objektum](The-ISEEditor-Object.md) szolgál, amely a megadott fájlt.</span><span class="sxs-lookup"><span data-stu-id="32543-134">The read-only property that gets the [editor object](The-ISEEditor-Object.md) that is used for the specified file.</span></span>

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a><span data-ttu-id="32543-135">Kódolás</span><span class="sxs-lookup"><span data-stu-id="32543-135">Encoding</span></span>

<span data-ttu-id="32543-136">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="32543-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="32543-137">A csak olvasható tulajdonság, amely lekérdezi az eredeti fájl kódolása.</span><span class="sxs-lookup"><span data-stu-id="32543-137">The read-only property that gets the original file encoding.</span></span> <span data-ttu-id="32543-138">Ez egy **System.Text.Encoding** objektum.</span><span class="sxs-lookup"><span data-stu-id="32543-138">This is a **System.Text.Encoding** object.</span></span>

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a><span data-ttu-id="32543-139">FullPath</span><span class="sxs-lookup"><span data-stu-id="32543-139">FullPath</span></span>

<span data-ttu-id="32543-140">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="32543-140">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="32543-141">A csak olvasható tulajdonság, amely lekérdezi a teljes elérési útját a megnyitott fájlt megadó karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="32543-141">The read-only property that gets the string that specifies the full path of the opened file.</span></span>

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a><span data-ttu-id="32543-142">IsSaved</span><span class="sxs-lookup"><span data-stu-id="32543-142">IsSaved</span></span>

<span data-ttu-id="32543-143">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="32543-143">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="32543-144">A csak olvasható logikai tulajdonság által visszaadott **$true** , ha a fájl mentése után történt utolsó módosításának.</span><span class="sxs-lookup"><span data-stu-id="32543-144">The read-only Boolean property that returns **$true** if the file has been saved after it was last modified.</span></span>

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a><span data-ttu-id="32543-145">IsUntitled</span><span class="sxs-lookup"><span data-stu-id="32543-145">IsUntitled</span></span>

<span data-ttu-id="32543-146">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="32543-146">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="32543-147">A csak olvasható tulajdonság által visszaadott **$true** , ha a fájl soha nem adtak ki egy címet.</span><span class="sxs-lookup"><span data-stu-id="32543-147">The read-only property that returns **$true** if the file has never been given a title.</span></span>

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a><span data-ttu-id="32543-148">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="32543-148">See Also</span></span>

- [<span data-ttu-id="32543-149">A ISEFileCollectionObject</span><span class="sxs-lookup"><span data-stu-id="32543-149">The ISEFileCollectionObject</span></span>](The-ISEFileCollection-Object.md)
- [<span data-ttu-id="32543-150">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="32543-150">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="32543-151">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="32543-151">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)