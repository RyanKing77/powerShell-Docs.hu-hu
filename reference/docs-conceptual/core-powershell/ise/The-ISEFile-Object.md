---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISEFile objektum
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: 276e8f04a827e18999b5b3ecb08f47de4f4b23b1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="the-isefile-object"></a><span data-ttu-id="5b920-103">Az ISEFile objektum</span><span class="sxs-lookup"><span data-stu-id="5b920-103">The ISEFile Object</span></span>

<span data-ttu-id="5b920-104">Egy **ISEFile** objektum által jelképezett egy fájlt a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE).</span><span class="sxs-lookup"><span data-stu-id="5b920-104">An **ISEFile** object represents a file in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="5b920-105">A Microsoft.PowerShell.Host.ISE.ISEFile osztály példánya.</span><span class="sxs-lookup"><span data-stu-id="5b920-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span> <span data-ttu-id="5b920-106">Ez a témakör felsorolja a tag módszerek és tagja tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="5b920-106">This topic lists its member methods and member properties.</span></span> <span data-ttu-id="5b920-107">A **$psISE.CurrentFile** és a fájlok gyűjtemény PowerShell ablakban fájlok Microsoft.PowerShell.Host.ISE.ISEFile osztály összes példányánál.</span><span class="sxs-lookup"><span data-stu-id="5b920-107">The **$psISE.CurrentFile** and the files in the Files collection in a PowerShell tab are all instances of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span>

## <a name="methods"></a><span data-ttu-id="5b920-108">Metódusok</span><span class="sxs-lookup"><span data-stu-id="5b920-108">Methods</span></span>

### <a name="save-saveencoding-"></a><span data-ttu-id="5b920-109">Mentés\( \[saveEncoding\] \)</span><span class="sxs-lookup"><span data-stu-id="5b920-109">Save\( \[saveEncoding\] \)</span></span>

<span data-ttu-id="5b920-110">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5b920-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5b920-111">Lemezre menti a fájlt.</span><span class="sxs-lookup"><span data-stu-id="5b920-111">Saves the file to disk.</span></span>

<span data-ttu-id="5b920-112">**\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező paraméter, a mentett fájlt használandó kódolás karakter.</span><span class="sxs-lookup"><span data-stu-id="5b920-112">**\[saveEncoding\]** - optional [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="5b920-113">Az alapértelmezett érték **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="5b920-113">The default value is **UTF8**.</span></span>

### <a name="exceptions"></a><span data-ttu-id="5b920-114">Kivételek</span><span class="sxs-lookup"><span data-stu-id="5b920-114">Exceptions</span></span>

- <span data-ttu-id="5b920-115">**System.IO.IOException**: nem sikerült menteni a fájlt.</span><span class="sxs-lookup"><span data-stu-id="5b920-115">**System.IO.IOException**: The file could not be saved.</span></span>

```powershell
# Save the file using the default encoding (UTF8)
$psISE.CurrentFile.Save()

# Save the file as ASCII.
$psISE.CurrentFile.Save([System.Text.Encoding]::ASCII)

# Gets the current encoding.
$myfile = $psISE.CurrentFile
$myfile.Encoding
```

### <a name="saveasfilename-saveencoding"></a><span data-ttu-id="5b920-116">A SaveAs\(fájlnév, \[saveEncoding\]\)</span><span class="sxs-lookup"><span data-stu-id="5b920-116">SaveAs\(filename, \[saveEncoding\]\)</span></span>

<span data-ttu-id="5b920-117">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5b920-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5b920-118">Menti a fájlt a megadott fájlnévvel és kódolását.</span><span class="sxs-lookup"><span data-stu-id="5b920-118">Saves the file with the specified file name and encoding.</span></span>

<span data-ttu-id="5b920-119">**Fájlnév** -karakterlánc fájl mentéséhez használandó neve.</span><span class="sxs-lookup"><span data-stu-id="5b920-119">**filename** - String The name to be used to save the file.</span></span>

<span data-ttu-id="5b920-120">**\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező paraméter, a mentett fájlt használandó kódolás karakter.</span><span class="sxs-lookup"><span data-stu-id="5b920-120">**\[saveEncoding\]** - optional [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="5b920-121">Az alapértelmezett érték **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="5b920-121">The default value is **UTF8**.</span></span>

### <a name="exceptions"></a><span data-ttu-id="5b920-122">Kivételek</span><span class="sxs-lookup"><span data-stu-id="5b920-122">Exceptions</span></span>

- <span data-ttu-id="5b920-123">**System.ArgumentNullException**: A **Fájlnév** paraméterek egyike null értékű.</span><span class="sxs-lookup"><span data-stu-id="5b920-123">**System.ArgumentNullException**: The **filename** parameter is null.</span></span>
- <span data-ttu-id="5b920-124">**System.ArgumentException**: A **Fájlnév** paraméter üres.</span><span class="sxs-lookup"><span data-stu-id="5b920-124">**System.ArgumentException**: The **filename** parameter is empty.</span></span>
- <span data-ttu-id="5b920-125">**System.IO.IOException**: nem sikerült menteni a fájlt.</span><span class="sxs-lookup"><span data-stu-id="5b920-125">**System.IO.IOException**: The file could not be saved.</span></span>

```powershell
# Save the file with a full path and name.
$fullpath = "c:\temp\newname.txt"
$psISE.CurrentFile.SaveAs($fullPath)
# Save the file with a full path and name and explicitly as UTF8.
$psISE.CurrentFile.SaveAs($fullPath, [System.Text.Encoding]::UTF8)
```

## <a name="properties"></a><span data-ttu-id="5b920-126">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="5b920-126">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="5b920-127">DisplayName</span><span class="sxs-lookup"><span data-stu-id="5b920-127">DisplayName</span></span>

<span data-ttu-id="5b920-128">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5b920-128">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5b920-129">A csak olvasható tulajdonság, amely lekérdezi az megjelenített neve ezt a fájlt tartalmazó karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="5b920-129">The read-only property that gets the string that contains the display name of this file.</span></span> <span data-ttu-id="5b920-130">A név jelenik meg a **fájl** szerkesztő felső fülre.</span><span class="sxs-lookup"><span data-stu-id="5b920-130">The name is shown on the **File** tab at the top of the editor.</span></span> <span data-ttu-id="5b920-131">A csillag jelenlétét \( \* \) a név végén azt jelzi, hogy a fájl rendelkezik-e a nem mentett módosításokat.</span><span class="sxs-lookup"><span data-stu-id="5b920-131">The presence of an asterisk \(\*\) at the end of the name indicates that the file has changes that have not been saved.</span></span>

```powershell
# Shows the display name of the file.
$psISE.CurrentFile.DisplayName
```

### <a name="editor"></a><span data-ttu-id="5b920-132">Szerkesztő</span><span class="sxs-lookup"><span data-stu-id="5b920-132">Editor</span></span>

<span data-ttu-id="5b920-133">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5b920-133">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5b920-134">A csak olvasható tulajdonság, amely lekérdezi a [szerkesztő objektum](The-ISEEditor-Object.md) , amely a megadott fájl szolgál.</span><span class="sxs-lookup"><span data-stu-id="5b920-134">The read-only property that gets the [editor object](The-ISEEditor-Object.md) that is used for the specified file.</span></span>

```powershell
# Gets the editor and the text.
$psISE.CurrentFile.Editor.Text
```

### <a name="encoding"></a><span data-ttu-id="5b920-135">Kódolás</span><span class="sxs-lookup"><span data-stu-id="5b920-135">Encoding</span></span>

<span data-ttu-id="5b920-136">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5b920-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5b920-137">A csak olvasható tulajdonság, amely lekérdezi az eredeti fájl kódolást.</span><span class="sxs-lookup"><span data-stu-id="5b920-137">The read-only property that gets the original file encoding.</span></span> <span data-ttu-id="5b920-138">Ez egy **System.Text.Encoding** objektum.</span><span class="sxs-lookup"><span data-stu-id="5b920-138">This is a **System.Text.Encoding** object.</span></span>

```powershell
# Shows the encoding for the file.
$psISE.CurrentFile.Encoding
```

### <a name="fullpath"></a><span data-ttu-id="5b920-139">FullPath</span><span class="sxs-lookup"><span data-stu-id="5b920-139">FullPath</span></span>

<span data-ttu-id="5b920-140">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5b920-140">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5b920-141">A csak olvasható tulajdonság, amely lekérdezi a karakterláncot, amely a megnyitott fájlt a teljes elérési útját adja meg.</span><span class="sxs-lookup"><span data-stu-id="5b920-141">The read-only property that gets the string that specifies the full path of the opened file.</span></span>

```powershell
# Shows the full path for the file.
$psISE.CurrentFile.FullPath
```

### <a name="issaved"></a><span data-ttu-id="5b920-142">IsSaved</span><span class="sxs-lookup"><span data-stu-id="5b920-142">IsSaved</span></span>

<span data-ttu-id="5b920-143">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5b920-143">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5b920-144">A csak olvasható logikai visszaadó tulajdonság **$true** Ha a fájl mentését után utolsó módosításának.</span><span class="sxs-lookup"><span data-stu-id="5b920-144">The read-only Boolean property that returns **$true** if the file has been saved after it was last modified.</span></span>

```powershell
# Determines whether the file has been saved since it was last modified.
$myfile = $psISE.CurrentFile
$myfile.IsSaved
```

### <a name="isuntitled"></a><span data-ttu-id="5b920-145">IsUntitled</span><span class="sxs-lookup"><span data-stu-id="5b920-145">IsUntitled</span></span>

<span data-ttu-id="5b920-146">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="5b920-146">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="5b920-147">A csak olvasható tulajdonság, amely visszaadja **$true** Ha a fájl soha nem adtak címét.</span><span class="sxs-lookup"><span data-stu-id="5b920-147">The read-only property that returns **$true** if the file has never been given a title.</span></span>

```powershell
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled
```

## <a name="see-also"></a><span data-ttu-id="5b920-148">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5b920-148">See Also</span></span>

- [<span data-ttu-id="5b920-149">The ISEFileCollectionObject</span><span class="sxs-lookup"><span data-stu-id="5b920-149">The ISEFileCollectionObject</span></span>](The-ISEFileCollection-Object.md)
- [<span data-ttu-id="5b920-150">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="5b920-150">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="5b920-151">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="5b920-151">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)