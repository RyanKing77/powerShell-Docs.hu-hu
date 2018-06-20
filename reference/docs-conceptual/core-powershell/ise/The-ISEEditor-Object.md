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
# <a name="the-iseeditor-object"></a>Az ISEEditor objektum

Egy **ISEEditor** célja a Microsoft.PowerShell.Host.ISE.ISEEditor osztály egy példányát. A konzol ablaktáblában van egy **ISEEditor** objektum. Minden egyes [ISEFile](The-ISEFile-Object.md) objektum tartozik egy **ISEEditor** objektum. Az alábbi szakaszok tartalmazzák a metódusok és tulajdonságait egy **ISEEditor** objektum.

## <a name="methods"></a>Metódusok

### <a name="clear"></a>Törölje a jelet\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Törli a szerkesztő szövege.

```powershell
# Clears the text in the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Clear()
```

### <a name="ensurevisibleint-linenumber"></a>EnsureVisible\(int és a lineNumber\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A szerkesztő görget, hogy a sor, amely megfelel a megadott **és a lineNumber** paraméter értéke látható. Az kivételt jelez, ha a megadott sorszámot: 1, utolsó sor száma, amely meghatározza az érvényes sorszámok tartományon kívül esik.

**és a lineNumber** tehető láthatóvá, hogy a sor számát.

```powershell
# Scrolls the text in the Script pane so that the fifth line is in view.
$psISE.CurrentFile.Editor.EnsureVisible(5)
```

### <a name="focus"></a>Fókusz\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A fókusz állítja be a szerkesztőt.

```powershell
# Sets focus to the Console pane.
$psISE.CurrentPowerShellTab.ConsolePane.Focus()
```

### <a name="getlinelengthint-linenumber-"></a>GetLineLength\(int és a lineNumber \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Lekérdezi a hossza egészként sor száma által meghatározott sor.

**és a lineNumber** , amelynek hossza beolvasandó sor.

**Vissza** a, a megadott sor: a sor hossza.

```powershell
# Gets the length of the first line in the text of the Command pane.
$psISE.CurrentPowerShellTab.ConsolePane.GetLineLength(1)
```

### <a name="gotomatch"></a>GoToMatch\(\)

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

A beszúrási jel áthelyezése a megfelelő karaktert, ha a **CanGoToMatch** a szerkesztő objektum tulajdonsága **$true**, amely előtt következik be a billentyűzettel közvetlenül egy nyitó zárójelet, a szögletes zárójel, vagy a zárójel - előtt \(,\[, {- vagy közvetlenül a záró zárójel, a szögletes zárójel, illetve a zárójel után - \),\],}.  A beszúrási jel kerül egy nyitó karakter előtt vagy után egy záró karakter. Ha a **CanGoToMatch** tulajdonság **$false**, akkor ez a metódus nincs semmi hatása.

```powershell
# Goes to the matching character if CanGoToMatch() is $true
$psISE.CurrentPowerShellTab.ConsolePane.GoToMatch()
```

### <a name="inserttext-text-"></a>InsertText\( szöveg \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A kijelölés lecseréli a szöveget, vagy szúrja be a szöveget a jelenlegi pozíciójában álló kalap jel.

**szöveg** -beszúrása szöveges karakterlánc.

Tekintse meg a [Scripting példa](#scripting-example) a témakör későbbi részében.

### <a name="select-startline-startcolumn-endline-endcolumn-"></a>Válassza ki\( startLine, startColumn, tulajdonság endline értéke, az endcolumn érték \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Kiválasztja a szöveget a **startLine**, **startColumn**, **tulajdonság endline értéke**, és **endcolumn érték** paraméterek.

**startLine** -egész a sor, ha a kijelölt indítja el.

**startColumn** -egész belül a Kezdő sor, ha indítja el a kijelölt oszlop.

**tulajdonság endline értéke** -egész a sort, ahol a kijelölt véget ér.

**az endcolumn érték** -egész az oszlop, ahol véget ér a kijelölt sor végén belül.

Tekintse meg a [Scripting példa](#scripting-example) a témakör későbbi részében.

### <a name="selectcaretline"></a>SelectCaretLine\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Kiválasztja a teljes sor a beszúrási jel jelenleg tartalmazó szöveg.

```powershell
# First, set the caret position on line 5.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
# Now select that entire line of text
$psISE.CurrentFile.Editor.SelectCaretLine()
```

### <a name="setcaretposition-linenumber-columnnumber-"></a>SetCaretPosition\( és a lineNumber, columnNumber \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Beállítja a beszúrási pozíciója a sor számát és az oszlop számát. Az kivételt jelez, ha a beszúrási jel sorszámot vagy a billentyűzettel oszlopszám kívül esnek a a megfelelő, érvényes tartományt.

**és a lineNumber** -egész kalap sor száma.

**columnNumber** -egész a beszúrási jel oszlopszám.

```powershell
# Set the CaretPosition.
$psISE.CurrentFile.Editor.SetCaretPosition(5,1)
```

### <a name="toggleoutliningexpansion"></a>ToggleOutliningExpansion\(\)

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Minden Vázlat szakasz kibontásához vagy összecsukásához okoz.

```powershell
# Toggle the outlining expansion
$psISE.CurrentFile.Editor.ToggleOutliningExpansion()
```

## <a name="properties"></a>Tulajdonságok

### <a name="cangotomatch"></a>CanGoToMatch

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

A csak olvasható logikai tulajdonság jelzi, hogy a beszúrási jel mellett a zárójel, a szögletes zárójel, illetve a zárójel - \( \), \[ \], {}. Ha a beszúrási jel nyitó karakter elé vagy közvetlenül a záró karakter pár után, akkor ez a tulajdonság értéke **$true**. Egyéb esetben **$false**.

```powershell
# Test to see if the caret is next to a parenthesis, bracket, or brace
$psISE.CurrentFile.Editor.CanGoToMatch
```

### <a name="caretcolumn"></a>CaretColumn

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi az oszlopnak a számát, amely megfelel a beszúrási pozíciója.

```powershell
# Get the CaretColumn.
$psISE.CurrentFile.Editor.CaretColumn
```

### <a name="caretline"></a>CaretLine

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a sor számát, amely tartalmazza a beszúrási jel.

```powershell
# Get the CaretLine.
$psISE.CurrentFile.Editor.CaretLine
```

### <a name="caretlinetext"></a>CaretLineText

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a szöveg, amely tartalmazza a billentyűzettel teljes sort.

```powershell
# Get all of the text on the line that contains the caret.
$psISE.CurrentFile.Editor.CaretLineText
```

### <a name="linecount"></a>LineCount

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely a sor számának lekérése a szerkesztőt.

```powershell
# Get the LineCount.
$psISE.CurrentFile.Editor.LineCount
```

### <a name="selectedtext"></a>SelectedText

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a kijelölt szöveg szerkesztő.

Tekintse meg a [Scripting példa](#scripting-example) a témakör későbbi részében.

### <a name="text"></a>Szöveg

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a szöveg a szerkesztőben.

Tekintse meg a [Scripting példa](#scripting-example) a témakör későbbi részében.

## <a name="scripting-example"></a>Parancsfájl-kezelési – példa

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

- [A ISEFile objektum](The-ISEFile-Object.md)
- [The PowerShellTab Object](The-PowerShellTab-Object.md)
- [A Windows PowerShell ISE objektummodell Scripting célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)