---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISEEditor objektum
ms.openlocfilehash: 2d4c3d941035384c591ca57e809c0e3a9b852f5c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952613"
---
# <a name="the-iseeditor-object"></a><span data-ttu-id="48bbf-103">Az ISEEditor objektum</span><span class="sxs-lookup"><span data-stu-id="48bbf-103">The ISEEditor Object</span></span>

<span data-ttu-id="48bbf-104">Egy **ISEEditor** célja a Microsoft.PowerShell.Host.ISE.ISEEditor osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="48bbf-104">An **ISEEditor** object is an instance of the Microsoft.PowerShell.Host.ISE.ISEEditor class.</span></span> <span data-ttu-id="48bbf-105">A konzol ablaktáblában van egy **ISEEditor** objektum.</span><span class="sxs-lookup"><span data-stu-id="48bbf-105">The Console pane is an **ISEEditor** object.</span></span> <span data-ttu-id="48bbf-106">Minden egyes [ISEFile](The-ISEFile-Object.md) objektum tartozik egy **ISEEditor** objektum.</span><span class="sxs-lookup"><span data-stu-id="48bbf-106">Each [ISEFile](The-ISEFile-Object.md) object has an associated **ISEEditor** object.</span></span> <span data-ttu-id="48bbf-107">Az alábbi szakaszok tartalmazzák a metódusok és tulajdonságait egy **ISEEditor** objektum.</span><span class="sxs-lookup"><span data-stu-id="48bbf-107">The following sections list the methods and properties of an **ISEEditor** object.</span></span>

## <a name="methods"></a><span data-ttu-id="48bbf-108">Metódusok</span><span class="sxs-lookup"><span data-stu-id="48bbf-108">Methods</span></span>

### <a name="clear"></a><span data-ttu-id="48bbf-109">Törölje a jelet\(\)</span><span class="sxs-lookup"><span data-stu-id="48bbf-109">Clear\(\)</span></span>

<span data-ttu-id="48bbf-110">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-111">Törli a szerkesztő szövege.</span><span class="sxs-lookup"><span data-stu-id="48bbf-111">Clears the text in the editor.</span></span>

```powershell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a><span data-ttu-id="48bbf-112">EnsureVisible\(int és a lineNumber\)</span><span class="sxs-lookup"><span data-stu-id="48bbf-112">EnsureVisible\(int lineNumber\)</span></span>

<span data-ttu-id="48bbf-113">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-113">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-114">A szerkesztő görget, hogy a sor, amely megfelel a megadott **és a lineNumber** paraméter értéke látható.</span><span class="sxs-lookup"><span data-stu-id="48bbf-114">Scrolls the editor so that the line that corresponds to the specified **lineNumber** parameter value is visible.</span></span> <span data-ttu-id="48bbf-115">Az kivételt jelez, ha a megadott sorszámot: 1, utolsó sor száma, amely meghatározza az érvényes sorszámok tartományon kívül esik.</span><span class="sxs-lookup"><span data-stu-id="48bbf-115">It throws an exception if the specified line number is outside the range of 1,last line number, which defines the valid line numbers.</span></span>

<span data-ttu-id="48bbf-116">**és a lineNumber** tehető láthatóvá, hogy a sor számát.</span><span class="sxs-lookup"><span data-stu-id="48bbf-116">**lineNumber** The number of the line that is to be made visible.</span></span>

```powershell
# Scrolls the text in the Script pane so that the fifth line is in view.
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a><span data-ttu-id="48bbf-117">Fókusz\(\)</span><span class="sxs-lookup"><span data-stu-id="48bbf-117">Focus\(\)</span></span>

<span data-ttu-id="48bbf-118">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-119">A fókusz állítja be a szerkesztőt.</span><span class="sxs-lookup"><span data-stu-id="48bbf-119">Sets the focus to the editor.</span></span>

```powershell
# Sets focus to the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a><span data-ttu-id="48bbf-120">GetLineLength\(int és a lineNumber \)</span><span class="sxs-lookup"><span data-stu-id="48bbf-120">GetLineLength\(int lineNumber \)</span></span>

<span data-ttu-id="48bbf-121">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-121">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-122">Lekérdezi a hossza egészként sor száma által meghatározott sor.</span><span class="sxs-lookup"><span data-stu-id="48bbf-122">Gets the line length as an integer for the line that is specified by the line number.</span></span>

<span data-ttu-id="48bbf-123">**és a lineNumber** , amelynek hossza beolvasandó sor.</span><span class="sxs-lookup"><span data-stu-id="48bbf-123">**lineNumber** The number of the line of which to get the length.</span></span>

<span data-ttu-id="48bbf-124">**Vissza** a, a megadott sor: a sor hossza.</span><span class="sxs-lookup"><span data-stu-id="48bbf-124">**Returns** The line length for the line at the specified line number.</span></span>

```powershell
# Gets the length of the first line in the text of the Command pane.
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a><span data-ttu-id="48bbf-125">GoToMatch\(\)</span><span class="sxs-lookup"><span data-stu-id="48bbf-125">GoToMatch\(\)</span></span>

<span data-ttu-id="48bbf-126">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="48bbf-126">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="48bbf-127">A beszúrási jel áthelyezése a megfelelő karaktert, ha a **CanGoToMatch** a szerkesztő objektum tulajdonsága **$true**, amely előtt következik be a billentyűzettel közvetlenül egy nyitó zárójelet, a szögletes zárójel, vagy a zárójel - előtt \(,\[, {- vagy közvetlenül a záró zárójel, a szögletes zárójel, illetve a zárójel után - \),\],}.</span><span class="sxs-lookup"><span data-stu-id="48bbf-127">Moves the caret to the matching character if the **CanGoToMatch** property of the editor object is **$true**, which occurs when the caret is immediately before an opening parenthesis, bracket, or brace - \(,\[,{ - or immediately after a closing parenthesis, bracket, or brace - \),\],}.</span></span>  <span data-ttu-id="48bbf-128">A beszúrási jel kerül egy nyitó karakter előtt vagy után egy záró karakter.</span><span class="sxs-lookup"><span data-stu-id="48bbf-128">The caret is placed before an opening character or after a closing character.</span></span> <span data-ttu-id="48bbf-129">Ha a **CanGoToMatch** tulajdonság **$false**, akkor ez a metódus nincs semmi hatása.</span><span class="sxs-lookup"><span data-stu-id="48bbf-129">If the **CanGoToMatch** property is **$false**, then this method does nothing.</span></span>

```powershell
# Goes to the matching character if CanGoToMatch() is $true
$psISE.CurrentPowerShellTab.ConsolePane.GoToMatch()
```

### <a name="inserttext-text-"></a><span data-ttu-id="48bbf-130">InsertText\( szöveg \)</span><span class="sxs-lookup"><span data-stu-id="48bbf-130">InsertText\( text \)</span></span>

<span data-ttu-id="48bbf-131">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-131">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-132">A kijelölés lecseréli a szöveget, vagy szúrja be a szöveget a jelenlegi pozíciójában álló kalap jel.</span><span class="sxs-lookup"><span data-stu-id="48bbf-132">Replaces the selection with text or inserts text at the current caret position.</span></span>

<span data-ttu-id="48bbf-133">**szöveg** -beszúrása szöveges karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="48bbf-133">**text** - String The text to insert.</span></span>

<span data-ttu-id="48bbf-134">Tekintse meg a [Scripting példa](#scripting-example) a témakör későbbi részében.</span><span class="sxs-lookup"><span data-stu-id="48bbf-134">See the [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="select-startline-startcolumn-endline-endcolumn-"></a><span data-ttu-id="48bbf-135">Válassza ki\( startLine, startColumn, tulajdonság endline értéke, az endcolumn érték \)</span><span class="sxs-lookup"><span data-stu-id="48bbf-135">Select\( startLine, startColumn, endLine, endColumn \)</span></span>

<span data-ttu-id="48bbf-136">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-137">Kiválasztja a szöveget a **startLine**, **startColumn**, **tulajdonság endline értéke**, és **endcolumn érték** paraméterek.</span><span class="sxs-lookup"><span data-stu-id="48bbf-137">Selects the text from the **startLine**, **startColumn**, **endLine**, and **endColumn** parameters.</span></span>

<span data-ttu-id="48bbf-138">**startLine** -egész a sor, ha a kijelölt indítja el.</span><span class="sxs-lookup"><span data-stu-id="48bbf-138">**startLine** - Integer The line where the selection starts.</span></span>

<span data-ttu-id="48bbf-139">**startColumn** -egész belül a Kezdő sor, ha indítja el a kijelölt oszlop.</span><span class="sxs-lookup"><span data-stu-id="48bbf-139">**startColumn** - Integer The column within the start line where the selection starts.</span></span>

<span data-ttu-id="48bbf-140">**tulajdonság endline értéke** -egész a sort, ahol a kijelölt véget ér.</span><span class="sxs-lookup"><span data-stu-id="48bbf-140">**endLine** - Integer The line where the selection ends.</span></span>

<span data-ttu-id="48bbf-141">**az endcolumn érték** -egész az oszlop, ahol véget ér a kijelölt sor végén belül.</span><span class="sxs-lookup"><span data-stu-id="48bbf-141">**endColumn** - Integer The column within the end line where the selection ends.</span></span>

<span data-ttu-id="48bbf-142">Tekintse meg a [Scripting példa](#scripting-example) a témakör későbbi részében.</span><span class="sxs-lookup"><span data-stu-id="48bbf-142">See the  [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="selectcaretline"></a><span data-ttu-id="48bbf-143">SelectCaretLine\(\)</span><span class="sxs-lookup"><span data-stu-id="48bbf-143">SelectCaretLine\(\)</span></span>

<span data-ttu-id="48bbf-144">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-144">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-145">Kiválasztja a teljes sor a beszúrási jel jelenleg tartalmazó szöveg.</span><span class="sxs-lookup"><span data-stu-id="48bbf-145">Selects the entire line of text that currently contains the caret.</span></span>

```powershell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a><span data-ttu-id="48bbf-146">SetCaretPosition\( és a lineNumber, columnNumber \)</span><span class="sxs-lookup"><span data-stu-id="48bbf-146">SetCaretPosition\( lineNumber, columnNumber \)</span></span>

<span data-ttu-id="48bbf-147">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-147">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-148">Beállítja a beszúrási pozíciója a sor számát és az oszlop számát.</span><span class="sxs-lookup"><span data-stu-id="48bbf-148">Sets the caret position at the line number and the column number.</span></span> <span data-ttu-id="48bbf-149">Az kivételt jelez, ha a beszúrási jel sorszámot vagy a billentyűzettel oszlopszám kívül esnek a a megfelelő, érvényes tartományt.</span><span class="sxs-lookup"><span data-stu-id="48bbf-149">It throws an exception if either the caret line number  or the caret column number  are out of their respective valid ranges.</span></span>

<span data-ttu-id="48bbf-150">**és a lineNumber** -egész kalap sor száma.</span><span class="sxs-lookup"><span data-stu-id="48bbf-150">**lineNumber** - Integer The caret line number.</span></span>

<span data-ttu-id="48bbf-151">**columnNumber** -egész a beszúrási jel oszlopszám.</span><span class="sxs-lookup"><span data-stu-id="48bbf-151">**columnNumber** - Integer The caret column number.</span></span>

```powershell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a><span data-ttu-id="48bbf-152">ToggleOutliningExpansion\(\)</span><span class="sxs-lookup"><span data-stu-id="48bbf-152">ToggleOutliningExpansion\(\)</span></span>

<span data-ttu-id="48bbf-153">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="48bbf-153">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="48bbf-154">Minden Vázlat szakasz kibontásához vagy összecsukásához okoz.</span><span class="sxs-lookup"><span data-stu-id="48bbf-154">Causes all the outline sections to expand or collapse.</span></span>

```powershell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a><span data-ttu-id="48bbf-155">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="48bbf-155">Properties</span></span>

### <a name="cangotomatch"></a><span data-ttu-id="48bbf-156">CanGoToMatch</span><span class="sxs-lookup"><span data-stu-id="48bbf-156">CanGoToMatch</span></span>

<span data-ttu-id="48bbf-157">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="48bbf-157">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="48bbf-158">A csak olvasható logikai tulajdonság jelzi, hogy a beszúrási jel mellett a zárójel, a szögletes zárójel, illetve a zárójel - \( \), \[ \], {}.</span><span class="sxs-lookup"><span data-stu-id="48bbf-158">The read-only Boolean property to indicate whether the caret is next to a parenthesis, bracket, or brace - \(\), \[\], {}.</span></span> <span data-ttu-id="48bbf-159">Ha a beszúrási jel nyitó karakter elé vagy közvetlenül a záró karakter pár után, akkor ez a tulajdonság értéke **$true**.</span><span class="sxs-lookup"><span data-stu-id="48bbf-159">If the caret is immediately before the opening character or immediately after the closing character of a pair, then this property value is **$true**.</span></span> <span data-ttu-id="48bbf-160">Egyéb esetben **$false**.</span><span class="sxs-lookup"><span data-stu-id="48bbf-160">Otherwise, it is **$false**.</span></span>

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

### <a name="caretcolumn"></a><span data-ttu-id="48bbf-161">CaretColumn</span><span class="sxs-lookup"><span data-stu-id="48bbf-161">CaretColumn</span></span>

<span data-ttu-id="48bbf-162">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-162">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-163">A csak olvasható tulajdonság, amely lekérdezi az oszlopnak a számát, amely megfelel a beszúrási pozíciója.</span><span class="sxs-lookup"><span data-stu-id="48bbf-163">The read-only property that gets the column number that corresponds to the position of the caret.</span></span>

```powershell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

### <a name="caretline"></a><span data-ttu-id="48bbf-164">CaretLine</span><span class="sxs-lookup"><span data-stu-id="48bbf-164">CaretLine</span></span>

<span data-ttu-id="48bbf-165">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-165">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-166">A csak olvasható tulajdonság, amely lekérdezi a sor számát, amely tartalmazza a beszúrási jel.</span><span class="sxs-lookup"><span data-stu-id="48bbf-166">The read-only property that gets the number of the line that contains the caret.</span></span>

```powershell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

### <a name="caretlinetext"></a><span data-ttu-id="48bbf-167">CaretLineText</span><span class="sxs-lookup"><span data-stu-id="48bbf-167">CaretLineText</span></span>

<span data-ttu-id="48bbf-168">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-168">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-169">A csak olvasható tulajdonság, amely lekérdezi a szöveg, amely tartalmazza a billentyűzettel teljes sort.</span><span class="sxs-lookup"><span data-stu-id="48bbf-169">The read-only property that gets the complete line of text that contains the caret.</span></span>

```powershell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

### <a name="linecount"></a><span data-ttu-id="48bbf-170">LineCount</span><span class="sxs-lookup"><span data-stu-id="48bbf-170">LineCount</span></span>

<span data-ttu-id="48bbf-171">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-171">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-172">A csak olvasható tulajdonság, amely a sor számának lekérése a szerkesztőt.</span><span class="sxs-lookup"><span data-stu-id="48bbf-172">The read-only property that gets the line count from the editor.</span></span>

```powershell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

### <a name="selectedtext"></a><span data-ttu-id="48bbf-173">SelectedText</span><span class="sxs-lookup"><span data-stu-id="48bbf-173">SelectedText</span></span>

<span data-ttu-id="48bbf-174">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-174">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-175">A csak olvasható tulajdonság, amely lekérdezi a kijelölt szöveg szerkesztő.</span><span class="sxs-lookup"><span data-stu-id="48bbf-175">The read-only property that gets the selected text from the editor.</span></span>

<span data-ttu-id="48bbf-176">Tekintse meg a [Scripting példa](#scripting-example) a témakör későbbi részében.</span><span class="sxs-lookup"><span data-stu-id="48bbf-176">See the  [Scripting Example](#scripting-example) later in this topic.</span></span>

### <a name="text"></a><span data-ttu-id="48bbf-177">Szöveg</span><span class="sxs-lookup"><span data-stu-id="48bbf-177">Text</span></span>

<span data-ttu-id="48bbf-178">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="48bbf-178">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="48bbf-179">Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a szöveg a szerkesztőben.</span><span class="sxs-lookup"><span data-stu-id="48bbf-179">The read/write property that gets or sets the text in the editor.</span></span>

<span data-ttu-id="48bbf-180">Tekintse meg a [Scripting példa](#scripting-example) a témakör későbbi részében.</span><span class="sxs-lookup"><span data-stu-id="48bbf-180">See the [Scripting Example](#scripting-example) later in this topic.</span></span>

## <a name="scripting-example"></a><span data-ttu-id="48bbf-181">Parancsfájl-kezelési – példa</span><span class="sxs-lookup"><span data-stu-id="48bbf-181">Scripting Example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="48bbf-182">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="48bbf-182">See Also</span></span>

- [<span data-ttu-id="48bbf-183">A ISEFile objektum</span><span class="sxs-lookup"><span data-stu-id="48bbf-183">The ISEFile Object</span></span>](The-ISEFile-Object.md)
- [<span data-ttu-id="48bbf-184">The PowerShellTab Object</span><span class="sxs-lookup"><span data-stu-id="48bbf-184">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="48bbf-185">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="48bbf-185">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="48bbf-186">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="48bbf-186">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)