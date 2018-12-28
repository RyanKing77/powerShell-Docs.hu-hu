---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEEditor objektum
ms.openlocfilehash: 2d4c3d941035384c591ca57e809c0e3a9b852f5c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404539"
---
# <a name="the-iseeditor-object"></a><span data-ttu-id="89013-103">Az ISEEditor objektum</span><span class="sxs-lookup"><span data-stu-id="89013-103">The ISEEditor Object</span></span>

<span data-ttu-id="89013-104">Egy **ISEEditor** objektum a Microsoft.PowerShell.Host.ISE.ISEEditor osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="89013-104">An **ISEEditor** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEEditor class.</span></span> <span data-ttu-id="89013-105">A konzolablakban van egy **ISEEditor** objektum.</span><span class="sxs-lookup"><span data-stu-id="89013-105">The Console pane is an **ISEEditor** object.</span></span> <span data-ttu-id="89013-106">Minden egyes [ISEFile](The-ISEFile-Object.md) objektumhoz tartozik egy társított **ISEEditor** objektum.</span><span class="sxs-lookup"><span data-stu-id="89013-106">Each [ISEFile](The-ISEFile-Object.md) object has an associated **ISEEditor** object.</span></span> <span data-ttu-id="89013-107">Az alábbi szakaszok tartalmazzák a módszerek és tulajdonságai egy **ISEEditor** objektum.</span><span class="sxs-lookup"><span data-stu-id="89013-107">The following sections list the methods and properties of an **ISEEditor** object.</span></span>

## <a name="methods"></a><span data-ttu-id="89013-108">Metódusok</span><span class="sxs-lookup"><span data-stu-id="89013-108">Methods</span></span>

### <a name="clear"></a><span data-ttu-id="89013-109">Világos\(\)</span><span class="sxs-lookup"><span data-stu-id="89013-109">Clear\(\)</span></span>

<span data-ttu-id="89013-110">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-111">Törli a szerkesztő szövege.</span><span class="sxs-lookup"><span data-stu-id="89013-111">Clears the text in the editor.</span></span>

```powershell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a><span data-ttu-id="89013-112">EnsureVisible\(int és a lineNumber\)</span><span class="sxs-lookup"><span data-stu-id="89013-112">EnsureVisible\(int lineNumber\)</span></span>

<span data-ttu-id="89013-113">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-113">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-114">A szerkesztő görgethető, hogy a sort, amely megfelel a megadott **és a lineNumber** paraméter értéke látható.</span><span class="sxs-lookup"><span data-stu-id="89013-114">Scrolls the editor so that the line that corresponds to the specified **lineNumber** parameter value is visible.</span></span> <span data-ttu-id="89013-115">Ezt a kivételt jelez, ha a megadott szám 1, legutóbbi sor száma, amely meghatározza az érvényes sorszámok tartományon kívül esik.</span><span class="sxs-lookup"><span data-stu-id="89013-115">It throws an exception if the specified line number is outside the range of 1,last line number, which defines the valid line numbers.</span></span>

<span data-ttu-id="89013-116">**és a lineNumber** a számát, hogy láthatóvá tenni.</span><span class="sxs-lookup"><span data-stu-id="89013-116">**lineNumber** The number of the line that is to be made visible.</span></span>

```powershell
# Scrolls the text in the Script pane so that the fifth line is in view.
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a><span data-ttu-id="89013-117">Fókusz\(\)</span><span class="sxs-lookup"><span data-stu-id="89013-117">Focus\(\)</span></span>

<span data-ttu-id="89013-118">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-119">A fókusz a szerkesztő állítja be.</span><span class="sxs-lookup"><span data-stu-id="89013-119">Sets the focus to the editor.</span></span>

```powershell
# Sets focus to the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a><span data-ttu-id="89013-120">GetLineLength\(int és a lineNumber \)</span><span class="sxs-lookup"><span data-stu-id="89013-120">GetLineLength\(int lineNumber \)</span></span>

<span data-ttu-id="89013-121">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-121">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-122">Lekéri a hossza a sort, amelyben a sor száma által meghatározott egész számként.</span><span class="sxs-lookup"><span data-stu-id="89013-122">Gets the line length as an integer for the line that is specified by the line number.</span></span>

<span data-ttu-id="89013-123">**és a lineNumber** olvasni a hosszát a sor száma.</span><span class="sxs-lookup"><span data-stu-id="89013-123">**lineNumber** The number of the line of which to get the length.</span></span>

<span data-ttu-id="89013-124">**Értéket ad vissza** a hossza, a megadott sorszám a sor.</span><span class="sxs-lookup"><span data-stu-id="89013-124">**Returns** The line length for the line at the specified line number.</span></span>

```powershell
# Gets the length of the first line in the text of the Command pane.
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a><span data-ttu-id="89013-125">GoToMatch\(\)</span><span class="sxs-lookup"><span data-stu-id="89013-125">GoToMatch\(\)</span></span>

<span data-ttu-id="89013-126">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="89013-126">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="89013-127">Jel áthelyezi a megfelelő karaktert, ha a **CanGoToMatch** editor objektu tulajdonság **$true**, amely akkor történik, ha a beszúrási jellel közvetlenül egy újabb nyitó zárójelet, zárójel vagy kapcsos zárójel - előtt \(,\[, {– vagy közvetlenül egy záró zárójelet, zárójel vagy kapcsos zárójel után – \),\],}.</span><span class="sxs-lookup"><span data-stu-id="89013-127">Moves the caret to the matching character if the **CanGoToMatch** property of the editor object is **$true**, which occurs when the caret is immediately before an opening parenthesis, bracket, or brace - \(,\[,{ - or immediately after a closing parenthesis, bracket, or brace - \),\],}.</span></span>  <span data-ttu-id="89013-128">A beszúrási jellel kerül egy nyitó karakter előtt vagy után egy záró karakter.</span><span class="sxs-lookup"><span data-stu-id="89013-128">The caret is placed before an opening character or after a closing character.</span></span> <span data-ttu-id="89013-129">Ha a **CanGoToMatch** tulajdonság **$false**, akkor ez a módszer nem csinál semmit.</span><span class="sxs-lookup"><span data-stu-id="89013-129">If the **CanGoToMatch** property is **$false**, then this method does nothing.</span></span>

```powershell
# Goes to the matching character if CanGoToMatch() is $true
$psISE.CurrentPowerShellTab.ConsolePane.GoToMatch()
```

### <a name="inserttext-text-"></a><span data-ttu-id="89013-130">InsertText\( szöveg \)</span><span class="sxs-lookup"><span data-stu-id="89013-130">InsertText\( text \)</span></span>

<span data-ttu-id="89013-131">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-131">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-132">Lecseréli a kijelölt szöveg, vagy a jelenlegi helyen álló kalap jel beilleszti a szöveget.</span><span class="sxs-lookup"><span data-stu-id="89013-132">Replaces the selection with text or inserts text at the current caret position.</span></span>

<span data-ttu-id="89013-133">**szöveg** – a szöveg beszúrása karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="89013-133">**text** - String The text to insert.</span></span>

<span data-ttu-id="89013-134">Tekintse meg a [Scripting példa](#scripting-example) jelen témakör későbbi részében.</span><span class="sxs-lookup"><span data-stu-id="89013-134">See the [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="select-startline-startcolumn-endline-endcolumn-"></a><span data-ttu-id="89013-135">Válassza ki\( startLine, startColumn, endLine, endColumn \)</span><span class="sxs-lookup"><span data-stu-id="89013-135">Select\( startLine, startColumn, endLine, endColumn \)</span></span>

<span data-ttu-id="89013-136">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-137">Szöveget kijelöli a **startLine**, **startColumn**, **endLine**, és **endColumn** paramétereket.</span><span class="sxs-lookup"><span data-stu-id="89013-137">Selects the text from the **startLine**, **startColumn**, **endLine**, and **endColumn** parameters.</span></span>

<span data-ttu-id="89013-138">**startLine** – egész a sort, ahol a kijelölt kezdődik.</span><span class="sxs-lookup"><span data-stu-id="89013-138">**startLine** - Integer The line where the selection starts.</span></span>

<span data-ttu-id="89013-139">**startColumn** – egész belül a kezdő sorban, ahol a kiválasztása elindítja az oszlop.</span><span class="sxs-lookup"><span data-stu-id="89013-139">**startColumn** - Integer The column within the start line where the selection starts.</span></span>

<span data-ttu-id="89013-140">**endLine** – egész a sort, ahol a kijelölt véget ér.</span><span class="sxs-lookup"><span data-stu-id="89013-140">**endLine** - Integer The line where the selection ends.</span></span>

<span data-ttu-id="89013-141">**endColumn** – egész szám az oszlop, ahol véget ér a kijelölt sor végén található.</span><span class="sxs-lookup"><span data-stu-id="89013-141">**endColumn** - Integer The column within the end line where the selection ends.</span></span>

<span data-ttu-id="89013-142">Tekintse meg a [Scripting példa](#scripting-example) jelen témakör későbbi részében.</span><span class="sxs-lookup"><span data-stu-id="89013-142">See the  [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="selectcaretline"></a><span data-ttu-id="89013-143">SelectCaretLine\(\)</span><span class="sxs-lookup"><span data-stu-id="89013-143">SelectCaretLine\(\)</span></span>

<span data-ttu-id="89013-144">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-144">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-145">A teljes sort jel jelenleg tartalmazó szöveges választja ki.</span><span class="sxs-lookup"><span data-stu-id="89013-145">Selects the entire line of text that currently contains the caret.</span></span>

```powershell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a><span data-ttu-id="89013-146">SetCaretPosition\( és a lineNumber columnNumber \)</span><span class="sxs-lookup"><span data-stu-id="89013-146">SetCaretPosition\( lineNumber, columnNumber \)</span></span>

<span data-ttu-id="89013-147">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-147">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-148">Beállítja a kalap pozícióját a sor száma és az oszlop számát.</span><span class="sxs-lookup"><span data-stu-id="89013-148">Sets the caret position at the line number and the column number.</span></span> <span data-ttu-id="89013-149">Kivételt jelez, ha a kalap sor számát vagy a kalap oszlopszám kívül esnek a megfelelő érvényes tartományt.</span><span class="sxs-lookup"><span data-stu-id="89013-149">It throws an exception if either the caret line number  or the caret column number  are out of their respective valid ranges.</span></span>

<span data-ttu-id="89013-150">**és a lineNumber** – a billentyűzettel sor számát egész.</span><span class="sxs-lookup"><span data-stu-id="89013-150">**lineNumber** - Integer The caret line number.</span></span>

<span data-ttu-id="89013-151">**columnNumber** – a billentyűzettel oszlopszám egész.</span><span class="sxs-lookup"><span data-stu-id="89013-151">**columnNumber** - Integer The caret column number.</span></span>

```powershell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a><span data-ttu-id="89013-152">ToggleOutliningExpansion\(\)</span><span class="sxs-lookup"><span data-stu-id="89013-152">ToggleOutliningExpansion\(\)</span></span>

<span data-ttu-id="89013-153">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="89013-153">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="89013-154">Hatására az összes Vázlat szakasz kibontásához vagy összecsukásához.</span><span class="sxs-lookup"><span data-stu-id="89013-154">Causes all the outline sections to expand or collapse.</span></span>

```powershell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a><span data-ttu-id="89013-155">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="89013-155">Properties</span></span>

### <a name="cangotomatch"></a><span data-ttu-id="89013-156">CanGoToMatch</span><span class="sxs-lookup"><span data-stu-id="89013-156">CanGoToMatch</span></span>

<span data-ttu-id="89013-157">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="89013-157">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="89013-158">A csak olvasható logikai tulajdonság jelzi, hogy jel melletti egy zárójelet, zárójel vagy kapcsos zárójel - \( \), \[ \], {}.</span><span class="sxs-lookup"><span data-stu-id="89013-158">The read-only Boolean property to indicate whether the caret is next to a parenthesis, bracket, or brace - \(\), \[\], {}.</span></span> <span data-ttu-id="89013-159">Ha a beszúrási jellel közvetlenül a nyitó karakter előtt, vagy közvetlenül a záró karaktert pár után, akkor ez a tulajdonság értéke **$true**.</span><span class="sxs-lookup"><span data-stu-id="89013-159">If the caret is immediately before the opening character or immediately after the closing character of a pair, then this property value is **$true**.</span></span> <span data-ttu-id="89013-160">Egyéb esetben **$false**.</span><span class="sxs-lookup"><span data-stu-id="89013-160">Otherwise, it is **$false**.</span></span>

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

### <a name="caretcolumn"></a><span data-ttu-id="89013-161">CaretColumn</span><span class="sxs-lookup"><span data-stu-id="89013-161">CaretColumn</span></span>

<span data-ttu-id="89013-162">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-162">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-163">A csak olvasható tulajdonság, amely lekérdezi az oszlopnak a számát, amely a beszúrási jellel pozícióját felel meg.</span><span class="sxs-lookup"><span data-stu-id="89013-163">The read-only property that gets the column number that corresponds to the position of the caret.</span></span>

```powershell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

### <a name="caretline"></a><span data-ttu-id="89013-164">CaretLine</span><span class="sxs-lookup"><span data-stu-id="89013-164">CaretLine</span></span>

<span data-ttu-id="89013-165">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-165">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-166">A csak olvasható tulajdonság, amely lekérdezi a beszúrási jellel tartalmazó sor száma.</span><span class="sxs-lookup"><span data-stu-id="89013-166">The read-only property that gets the number of the line that contains the caret.</span></span>

```powershell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

### <a name="caretlinetext"></a><span data-ttu-id="89013-167">CaretLineText</span><span class="sxs-lookup"><span data-stu-id="89013-167">CaretLineText</span></span>

<span data-ttu-id="89013-168">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-168">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-169">A csak olvasható tulajdonság, amely lekérdezi a szöveg, amely tartalmazza a jel a teljes sort.</span><span class="sxs-lookup"><span data-stu-id="89013-169">The read-only property that gets the complete line of text that contains the caret.</span></span>

```powershell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

### <a name="linecount"></a><span data-ttu-id="89013-170">LineCount</span><span class="sxs-lookup"><span data-stu-id="89013-170">LineCount</span></span>

<span data-ttu-id="89013-171">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-171">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-172">A csak olvasható tulajdonság, amely a sor száma olvas be a szerkesztőt.</span><span class="sxs-lookup"><span data-stu-id="89013-172">The read-only property that gets the line count from the editor.</span></span>

```powershell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

### <a name="selectedtext"></a><span data-ttu-id="89013-173">SelectedText</span><span class="sxs-lookup"><span data-stu-id="89013-173">SelectedText</span></span>

<span data-ttu-id="89013-174">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-174">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-175">A csak olvasható tulajdonság, amely a kijelölt szöveg olvas be a szerkesztőt.</span><span class="sxs-lookup"><span data-stu-id="89013-175">The read-only property that gets the selected text from the editor.</span></span>

<span data-ttu-id="89013-176">Tekintse meg a [Scripting példa](#scripting-example) jelen témakör későbbi részében.</span><span class="sxs-lookup"><span data-stu-id="89013-176">See the  [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="text"></a><span data-ttu-id="89013-177">Szöveg</span><span class="sxs-lookup"><span data-stu-id="89013-177">Text</span></span>

<span data-ttu-id="89013-178">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="89013-178">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="89013-179">Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a szöveget a szerkesztőben.</span><span class="sxs-lookup"><span data-stu-id="89013-179">The read/write property that gets or sets the text in the editor.</span></span>

<span data-ttu-id="89013-180">Tekintse meg a [Scripting példa](#scripting-example) jelen témakör későbbi részében.</span><span class="sxs-lookup"><span data-stu-id="89013-180">See the [Scripting Example](#scripting-example) later in this topic.</span></span>

## <a name="scripting-example"></a><span data-ttu-id="89013-181">Parancsfájl-kezelési példa</span><span class="sxs-lookup"><span data-stu-id="89013-181">Scripting Example</span></span>

```powershell
# This illustrates how you can use the length of a line to
# select the entire line and shows how you can make it lowercase.
# You must run this in the Console pane. It will not run in the Script pane.
# Begin by getting a variable that points to the editor.
$myEditor = $psISE.CurrentFile.Editor
# Clear the text in the current file editor.
$myEditor.Clear()

# Make sure the file has five lines of text.
$myEditor.InsertText("LINE1 `n")
$myEditor.InsertText("LINE2 `n")
$myEditor.InsertText("LINE3 `n")
$myEditor.InsertText("LINE4 `n")
$myEditor.InsertText("LINE5 `n")

# Use the GetLineLength method to get the length of the third line.
$endColumn = $myEditor.GetLineLength(3)
# Select the text in the first three lines.
$myEditor.Select(1, 1, 3, $endColumn + 1)
$selection = $myEditor.SelectedText
# Clear all the text in the editor.
$myEditor.Clear()
# Add the selected text back, but in lower case.
$myEditor.InsertText($selection.ToLower())
```

## <a name="see-also"></a><span data-ttu-id="89013-182">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="89013-182">See Also</span></span>

- [<span data-ttu-id="89013-183">Az ISEFile objektum</span><span class="sxs-lookup"><span data-stu-id="89013-183">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="89013-184">Az PowerShellTab objektum</span><span class="sxs-lookup"><span data-stu-id="89013-184">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="89013-185">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="89013-185">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="89013-186">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="89013-186">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)