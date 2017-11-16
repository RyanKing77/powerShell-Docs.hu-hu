---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISEFile objektum
ms.assetid: 1c6d91f3-c556-42a2-a017-79b6b7b4b7db
ms.openlocfilehash: a1fbd48e872684cc578adb03f52430eabdc54c2c
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="the-isefile-object"></a><span data-ttu-id="ad32f-103">A ISEFile objektum</span><span class="sxs-lookup"><span data-stu-id="ad32f-103">The ISEFile Object</span></span>
  <span data-ttu-id="ad32f-104">Egy **ISEFile** objektum által jelképezett egy fájlt a Windows PowerShell® integrált parancsfájl-kezelési környezet (ISE).</span><span class="sxs-lookup"><span data-stu-id="ad32f-104">An **ISEFile** object represents a file in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="ad32f-105">A Microsoft.PowerShell.Host.ISE.ISEFile osztály példánya.</span><span class="sxs-lookup"><span data-stu-id="ad32f-105">It is an instance of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span> <span data-ttu-id="ad32f-106">Ez a témakör felsorolja a tag módszerek és tagja tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="ad32f-106">This topic lists its member methods and member properties.</span></span> <span data-ttu-id="ad32f-107">A **$psISE.CurrentFile** és a fájlok gyűjtemény PowerShell ablakban fájlok Microsoft.PowerShell.Host.ISE.ISEFile osztály összes példányánál.</span><span class="sxs-lookup"><span data-stu-id="ad32f-107">The **$psISE.CurrentFile** and the files in the Files collection in a PowerShell tab are all instances of the Microsoft.PowerShell.Host.ISE.ISEFile class.</span></span>

## <a name="methods"></a><span data-ttu-id="ad32f-108">Metódusok</span><span class="sxs-lookup"><span data-stu-id="ad32f-108">Methods</span></span>

### <a name="save-saveencoding-"></a><span data-ttu-id="ad32f-109">Mentés\( \[saveEncoding\]\)</span><span class="sxs-lookup"><span data-stu-id="ad32f-109">Save\( \[saveEncoding\] \)</span></span>
  <span data-ttu-id="ad32f-110">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="ad32f-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="ad32f-111">Lemezre menti a fájlt.</span><span class="sxs-lookup"><span data-stu-id="ad32f-111">Saves the file to disk.</span></span>

 <span data-ttu-id="ad32f-112">**\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező paraméter, a mentett fájlt használandó kódolás karakter.</span><span class="sxs-lookup"><span data-stu-id="ad32f-112">**\[saveEncoding\]** - optional [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="ad32f-113">Az alapértelmezett érték **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="ad32f-113">The default value is **UTF8**.</span></span>

 <span data-ttu-id="ad32f-114">**Kivételek**</span><span class="sxs-lookup"><span data-stu-id="ad32f-114">**Exceptions**</span></span>
 -   <span data-ttu-id="ad32f-115">**System.IO.IOException**: nem sikerült menteni a fájlt.</span><span class="sxs-lookup"><span data-stu-id="ad32f-115">**System.IO.IOException**: The file could not be saved.</span></span>

```
# Save the file using the default encoding (UTF8)
$psIse.CurrentFile.Save()

# Save the file as ASCII.
$psIse.CurrentFile.Save( [System.Text.Encoding]::ASCII )

# Gets the current encoding.
$myfile=$psIse.CurrentFile
$myfile.Encoding

```

### <a name="saveasfilename-saveencoding"></a><span data-ttu-id="ad32f-116">A SaveAs\(fájlnév, \[saveEncoding\]\)</span><span class="sxs-lookup"><span data-stu-id="ad32f-116">SaveAs\(filename, \[saveEncoding\]\)</span></span>
  <span data-ttu-id="ad32f-117">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="ad32f-117">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="ad32f-118">Menti a fájlt a megadott fájlnévvel és kódolását.</span><span class="sxs-lookup"><span data-stu-id="ad32f-118">Saves the file with the specified file name and encoding.</span></span>

 <span data-ttu-id="ad32f-119">**Fájlnév** -karakterlánc fájl mentéséhez használandó neve.</span><span class="sxs-lookup"><span data-stu-id="ad32f-119">**filename** - String The name to be used to save the file.</span></span>

 <span data-ttu-id="ad32f-120">**\[saveEncoding\]**  – nem kötelező [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) egy nem kötelező paraméter, a mentett fájlt használandó kódolás karakter.</span><span class="sxs-lookup"><span data-stu-id="ad32f-120">**\[saveEncoding\]** - optional [System.Text.Encoding](http://msdn.microsoft.com/library/system.text.encoding.aspx) An optional character encoding parameter to be used for the saved file.</span></span> <span data-ttu-id="ad32f-121">Az alapértelmezett érték **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="ad32f-121">The default value is **UTF8**.</span></span>

 <span data-ttu-id="ad32f-122">**Kivételek**</span><span class="sxs-lookup"><span data-stu-id="ad32f-122">**Exceptions**</span></span>
 -   <span data-ttu-id="ad32f-123">**System.ArgumentNullException**: A **Fájlnév** paraméterek egyike null értékű.</span><span class="sxs-lookup"><span data-stu-id="ad32f-123">**System.ArgumentNullException**: The **filename** parameter is null.</span></span>

- <span data-ttu-id="ad32f-124">**System.ArgumentException**: A **Fájlnév** paraméter üres.</span><span class="sxs-lookup"><span data-stu-id="ad32f-124">**System.ArgumentException**: The **filename** parameter is empty.</span></span>

- <span data-ttu-id="ad32f-125">**System.IO.IOException**: nem sikerült menteni a fájlt.</span><span class="sxs-lookup"><span data-stu-id="ad32f-125">**System.IO.IOException**: The file could not be saved.</span></span>

```
# Save the file with a full path and name. 
$fullpath = "c:\temp\newname.txt"
$psIse.CurrentFile.SaveAs($fullPath) 
# Save the file with a full path and name and explicitly as UTF8. 
$psIse.CurrentFile.SaveAs( $fullPath, [System.Text.Encoding]::UTF8 )

```

## <a name="properties"></a><span data-ttu-id="ad32f-126">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="ad32f-126">Properties</span></span>

### <a name="displayname"></a><span data-ttu-id="ad32f-127">DisplayName</span><span class="sxs-lookup"><span data-stu-id="ad32f-127">DisplayName</span></span>
  <span data-ttu-id="ad32f-128">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="ad32f-128">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="ad32f-129">A csak olvasható tulajdonság, amely lekérdezi az megjelenített neve ezt a fájlt tartalmazó karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="ad32f-129">The read-only property that gets the string that contains the display name of this file.</span></span> <span data-ttu-id="ad32f-130">A név jelenik meg a **fájl** szerkesztő felső fülre.</span><span class="sxs-lookup"><span data-stu-id="ad32f-130">The name is shown on the **File** tab at the top of the editor.</span></span> <span data-ttu-id="ad32f-131">A csillag jelenlétét \( \* \) a név végén azt jelzi, hogy a fájl rendelkezik-e a nem mentett módosításokat.</span><span class="sxs-lookup"><span data-stu-id="ad32f-131">The presence of an asterisk \(\*\) at the end of the name indicates that the file has changes that have not been saved.</span></span>

```
# Shows the display name of the file.
$psIse.CurrentFile.DisplayName

```

### <a name="editor"></a><span data-ttu-id="ad32f-132">Szerkesztő</span><span class="sxs-lookup"><span data-stu-id="ad32f-132">Editor</span></span>
  <span data-ttu-id="ad32f-133">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="ad32f-133">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="ad32f-134">A csak olvasható tulajdonság, amely lekérdezi a [szerkesztő objektum](The-ISEEditor-Object.md) , amely a megadott fájl szolgál.</span><span class="sxs-lookup"><span data-stu-id="ad32f-134">The read-only property that gets the [editor object](The-ISEEditor-Object.md) that is used for the specified file.</span></span>

```
# Gets the editor and the text.
$psIse.CurrentFile.Editor.Text

```

### <a name="encoding"></a><span data-ttu-id="ad32f-135">Kódolás</span><span class="sxs-lookup"><span data-stu-id="ad32f-135">Encoding</span></span>
  <span data-ttu-id="ad32f-136">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="ad32f-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="ad32f-137">A csak olvasható tulajdonság, amely lekérdezi az eredeti fájl kódolást.</span><span class="sxs-lookup"><span data-stu-id="ad32f-137">The read-only property that gets the original file encoding.</span></span> <span data-ttu-id="ad32f-138">Ez egy **System.Text.Encoding** objektum.</span><span class="sxs-lookup"><span data-stu-id="ad32f-138">This is a **System.Text.Encoding** object.</span></span>

```
# Shows the encoding for the file. 
$psIse.CurrentFile.Encoding

```

### <a name="fullpath"></a><span data-ttu-id="ad32f-139">FullPath</span><span class="sxs-lookup"><span data-stu-id="ad32f-139">FullPath</span></span>
  <span data-ttu-id="ad32f-140">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="ad32f-140">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="ad32f-141">A csak olvasható tulajdonság, amely lekérdezi a karakterláncot, amely a megnyitott fájlt a teljes elérési útját adja meg.</span><span class="sxs-lookup"><span data-stu-id="ad32f-141">The read-only property that gets the string that specifies the full path of the opened file.</span></span>

```
# Shows the full path for the file. 
$psIse.CurrentFile.FullPath

```

### <a name="issaved"></a><span data-ttu-id="ad32f-142">IsSaved</span><span class="sxs-lookup"><span data-stu-id="ad32f-142">IsSaved</span></span>
  <span data-ttu-id="ad32f-143">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="ad32f-143">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="ad32f-144">A csak olvasható logikai visszaadó tulajdonság **$true** Ha a fájl mentését után utolsó módosításának.</span><span class="sxs-lookup"><span data-stu-id="ad32f-144">The read-only Boolean property that returns **$true** if the file has been saved after it was last modified.</span></span>

```
# Determines whether the file has been saved since it was last modified.
$myfile=$psIse.CurrentFile
$myfile.IsSaved

```

### <a name="isuntitled"></a><span data-ttu-id="ad32f-145">IsUntitled</span><span class="sxs-lookup"><span data-stu-id="ad32f-145">IsUntitled</span></span>
  <span data-ttu-id="ad32f-146">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="ad32f-146">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="ad32f-147">A csak olvasható tulajdonság, amely visszaadja **$true** Ha a fájl soha nem adtak címét.</span><span class="sxs-lookup"><span data-stu-id="ad32f-147">The read-only property that returns **$true** if the file has never been given a title.</span></span>

```
# Determines whether the file has never been given a title.
$psISE.CurrentFile.IsUntitled
$psISE.CurrentFile.SaveAs("temp.txt")
$psISE.CurrentFile.IsUntitled

```

## <a name="see-also"></a><span data-ttu-id="ad32f-148">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ad32f-148">See Also</span></span>
- [<span data-ttu-id="ad32f-149">A ISEFileCollectionObject</span><span class="sxs-lookup"><span data-stu-id="ad32f-149">The ISEFileCollectionObject</span></span>](The-ISEFileCollection-Object.md) 
- [<span data-ttu-id="ad32f-150">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="ad32f-150">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="ad32f-151">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="ad32f-151">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [<span data-ttu-id="ad32f-152">A ISE objektum modell hierarchia</span><span class="sxs-lookup"><span data-stu-id="ad32f-152">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
