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
# <a name="the-iseeditor-object"></a>Az ISEEditor objektum

Egy **ISEEditor** objektum a Microsoft.PowerShell.Host.ISE.ISEEditor osztály egy példányát. A konzolablakban van egy **ISEEditor** objektum. Minden egyes [ISEFile](The-ISEFile-Object.md) objektumhoz tartozik egy társított **ISEEditor** objektum. Az alábbi szakaszok tartalmazzák a módszerek és tulajdonságai egy **ISEEditor** objektum.

## <a name="methods"></a>Metódusok

### <a name="clear"></a>Világos\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Törli a szerkesztő szövege.

```powershell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a>EnsureVisible\(int és a lineNumber\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A szerkesztő görgethető, hogy a sort, amely megfelel a megadott **és a lineNumber** paraméter értéke látható. Ezt a kivételt jelez, ha a megadott szám 1, legutóbbi sor száma, amely meghatározza az érvényes sorszámok tartományon kívül esik.

**és a lineNumber** a számát, hogy láthatóvá tenni.

```powershell
# Scrolls the text in the Script pane so that the fifth line is in view.
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a>Fókusz\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A fókusz a szerkesztő állítja be.

```powershell
# Sets focus to the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a>GetLineLength\(int és a lineNumber \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Lekéri a hossza a sort, amelyben a sor száma által meghatározott egész számként.

**és a lineNumber** olvasni a hosszát a sor száma.

**Értéket ad vissza** a hossza, a megadott sorszám a sor.

```powershell
# Gets the length of the first line in the text of the Command pane.
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a>GoToMatch\(\)

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Jel áthelyezi a megfelelő karaktert, ha a **CanGoToMatch** editor objektu tulajdonság **$true**, amely akkor történik, ha a beszúrási jellel közvetlenül egy újabb nyitó zárójelet, zárójel vagy kapcsos zárójel - előtt \(,\[, {– vagy közvetlenül egy záró zárójelet, zárójel vagy kapcsos zárójel után – \),\],}.  A beszúrási jellel kerül egy nyitó karakter előtt vagy után egy záró karakter. Ha a **CanGoToMatch** tulajdonság **$false**, akkor ez a módszer nem csinál semmit.

```powershell
# Goes to the matching character if CanGoToMatch() is $true
$psISE.CurrentPowerShellTab.ConsolePane.GoToMatch()
```

### <a name="inserttext-text-"></a>InsertText\( szöveg \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Lecseréli a kijelölt szöveg, vagy a jelenlegi helyen álló kalap jel beilleszti a szöveget.

**szöveg** – a szöveg beszúrása karakterlánc.

Tekintse meg a [Scripting példa](#scripting-example) jelen témakör későbbi részében.

### <a name="select-startline-startcolumn-endline-endcolumn-"></a>Válassza ki\( startLine, startColumn, endLine, endColumn \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Szöveget kijelöli a **startLine**, **startColumn**, **endLine**, és **endColumn** paramétereket.

**startLine** – egész a sort, ahol a kijelölt kezdődik.

**startColumn** – egész belül a kezdő sorban, ahol a kiválasztása elindítja az oszlop.

**endLine** – egész a sort, ahol a kijelölt véget ér.

**endColumn** – egész szám az oszlop, ahol véget ér a kijelölt sor végén található.

Tekintse meg a [Scripting példa](#scripting-example) jelen témakör későbbi részében.

### <a name="selectcaretline"></a>SelectCaretLine\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A teljes sort jel jelenleg tartalmazó szöveges választja ki.

```powershell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a>SetCaretPosition\( és a lineNumber columnNumber \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Beállítja a kalap pozícióját a sor száma és az oszlop számát. Kivételt jelez, ha a kalap sor számát vagy a kalap oszlopszám kívül esnek a megfelelő érvényes tartományt.

**és a lineNumber** – a billentyűzettel sor számát egész.

**columnNumber** – a billentyűzettel oszlopszám egész.

```powershell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a>ToggleOutliningExpansion\(\)

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Hatására az összes Vázlat szakasz kibontásához vagy összecsukásához.

```powershell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a>Tulajdonságok

### <a name="cangotomatch"></a>CanGoToMatch

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A csak olvasható logikai tulajdonság jelzi, hogy jel melletti egy zárójelet, zárójel vagy kapcsos zárójel - \( \), \[ \], {}. Ha a beszúrási jellel közvetlenül a nyitó karakter előtt, vagy közvetlenül a záró karaktert pár után, akkor ez a tulajdonság értéke **$true**. Egyéb esetben **$false**.

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

### <a name="caretcolumn"></a>CaretColumn

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi az oszlopnak a számát, amely a beszúrási jellel pozícióját felel meg.

```powershell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

### <a name="caretline"></a>CaretLine

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a beszúrási jellel tartalmazó sor száma.

```powershell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

### <a name="caretlinetext"></a>CaretLineText

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a szöveg, amely tartalmazza a jel a teljes sort.

```powershell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

### <a name="linecount"></a>LineCount

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely a sor száma olvas be a szerkesztőt.

```powershell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

### <a name="selectedtext"></a>SelectedText

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely a kijelölt szöveg olvas be a szerkesztőt.

Tekintse meg a [Scripting példa](#scripting-example) jelen témakör későbbi részében.

### <a name="text"></a>Szöveg

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a szöveget a szerkesztőben.

Tekintse meg a [Scripting példa](#scripting-example) jelen témakör későbbi részében.

## <a name="scripting-example"></a>Parancsfájl-kezelési példa

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

## <a name="see-also"></a>Lásd még:

- [Az ISEFile objektum](The-ISEFile-Object.md)
- [Az PowerShellTab objektum](The-PowerShellTab-Object.md)
- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)