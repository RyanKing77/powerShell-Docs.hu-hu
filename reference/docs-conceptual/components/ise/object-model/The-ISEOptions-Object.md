---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEOptions objektum
ms.openlocfilehash: e9dcb13c14212ec4aec40a7f163e2ed56ceea6f9
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67028926"
---
# <a name="the-iseoptions-object"></a>Az ISEOptions objektum

A **ISEOptions** objektum képviseli a Windows PowerShell ISE-ben különböző beállításait. Egy példányát a **Microsoft.PowerShell.Host.ISE.ISEOptions** osztály.

A **ISEOptions** objektum tartalmazza a következő metódusokat és tulajdonságokat.

## <a name="methods"></a>Metódusok

### <a name="restoredefaultconsoletokencolors"></a>RestoreDefaultConsoleTokenColors\(\)

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Visszaállítja a konzolablakban a token színek alapértelmezett értékeit.

```powershell
# Changes the color of the commands in the Console pane to red and then restores it to its default value.
$psISE.Options.ConsoleTokenColors["Command"] = 'red'
$psISE.Options.RestoreDefaultConsoleTokenColors()
```

### <a name="restoredefaults"></a>RestoreDefaults\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Visszaállítja a konzol ablaktáblában összes beállítások alapértelmezett értékeit. Adja meg a standard szintű jelölőnégyzetet, hogy az üzenet nem jelenik meg újra különböző figyelmeztető üzeneteket viselkedését is alaphelyzetbe állítja.

```powershell
# Changes the background color in the Console pane and then restores it to its default value.
$psISE.Options.ConsolePaneBackgroundColor = 'orange'
$psISE.Options.RestoreDefaults()
```

### <a name="restoredefaulttokencolors"></a>RestoreDefaultTokenColors\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Visszaállítja az alapértelmezett értékeket, a parancsfájl panelen tokent színeit.

```powershell
# Changes the color of the comments in the Script pane to red and then restores it to its default value.
$psISE.Options.TokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultTokenColors()
```

### <a name="restoredefaultxmltokencolors"></a>RestoreDefaultXmlTokenColors\(\)

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Visszaállítja az alapértelmezett értékeket, az XML-elemeket, amelyek jelennek meg a Windows PowerShell ISE-ben a jogkivonat színe. További tájékoztatás [XmlTokenColors](#xmltokencolors).

```powershell
# Changes the color of the comments in XML data to red and then restores it to its default value.
$psISE.Options.XmlTokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultXmlTokenColors()
```

## <a name="properties"></a>Tulajdonságok

### <a name="autosaveminuteinterval"></a>AutoSaveMinuteInterval

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Automatikus mentés műveletek Windows PowerShell ISE által a fájlok között eltelt percek számát adja meg. Az alapértelmezett érték 2 perc. Egész érték.

```powershell
# Changes the number of minutes between automatic save operations to every 3 minutes.
$psISE.Options.AutoSaveMinuteInterval = 3
```

### <a name="commandpanebackgroundcolor"></a>CommandPaneBackgroundColor

Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.  A későbbi verziókhoz, lásd: [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

Meghatározza a parancs panelen háttérszíne. Egy példányát a **System.Windows.Media.Color** osztály.

```powershell
# Changes the background color of the Command pane to orange.
$psISE.Options.CommandPaneBackgroundColor = 'orange'
```

### <a name="commandpaneup"></a>CommandPaneUp

Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.

Itt adhatja meg, hogy található-e a parancs panelen fent a Tesztkimenet ablaktáblán.

```powershell
# Moves the Command pane to the top of the screen.
$psISE.Options.CommandPaneUp  = $true
```

### <a name="consolepanebackgroundcolor"></a>ConsolePaneBackgroundColor

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Adja meg a konzol ablaktáblában háttérszíne. Egy példányát a **System.Windows.Media.Color** osztály.

```powershell
# Changes the background color of the Console pane to red.
$psISE.Options.ConsolePaneBackgroundColor = 'red'
```

### <a name="consolepaneforegroundcolor"></a>ConsolePaneForegroundColor

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Megadja a szöveg előterének színe a konzol ablaktáblában.

```powershell
# Changes the foreground color of the text in the Console pane to yellow.
$psISE.Options.ConsolePaneForegroundColor  = 'yellow'
```

### <a name="consolepanetextbackgroundcolor"></a>ConsolePaneTextBackgroundColor

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A szöveg háttérszínét adja meg a konzol ablaktáblában.

```powershell
# Changes the background color of the Console pane text to pink.
$psISE.Options.ConsolePaneTextBackgroundColor = 'pink'
```

### <a name="consoletokencolors"></a>ConsoleTokenColors

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Megadja a színeket az IntelliSense jogkivonatokat a Windows PowerShell ISE-konzol ablaktáblában. Ez a tulajdonság egy szótárobjektum, amely tartalmazza a név/érték párok tokentípusokat és a konzol ablaktáblában színe. A parancsfájl panelen IntelliSense jogkivonatok a színek módosításához lásd [TokenColors](#tokencolors). A színek visszaáll az alapértelmezett értékeket, lásd: [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors). Token színek állíthat be a következőket: Attribútum parancs, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, szám, operátor, pozíciója, StatementSeparator, karakterlánc, típus, ismeretlen, változó.

```powershell
# Sets the color of commands to green.
$psISE.Options.ConsoleTokenColors["Command"] = 'green'
# Sets the color of keywords to magenta.
$psISE.Options.ConsoleTokenColors["Keyword"] = 'magenta'
```

### <a name="debugbackgroundcolor"></a>DebugBackgroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Megadja a háttér színét, a hibakeresési szöveg, amely akkor jelenik meg a konzol ablaktáblában. Egy példányát a **System.Windows.Media.Color** osztály.

```powershell
# Changes the background color for the debug text that appears in the Console pane to blue.
$psISE.Options.DebugBackgroundColor = '#0000FF'
```

### <a name="debugforegroundcolor"></a>DebugForegroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Megadja az előtér színe a hibakeresési szöveg, amely megjelenik a konzol ablaktáblában. Egy példányát a **System.Windows.Media.Color** osztály.

```powershell
# Changes the foreground color for the debug text that appears in the Console pane to yellow.
$psISE.Options.DebugForegroundColor = 'yellow'
```

### <a name="defaultoptions"></a>DefaultOptions

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Adja meg az alapértelmezett értékekkel használható, ha a visszaállítás módszerek használhatók a Tulajdonságok gyűjteménye.

```powershell
# Displays the name of the default options. This example is from ISE 4.0.
$psISE.Options.DefaultOptions

SelectedScriptPaneState                   : Top
ShowDefaultSnippets                       : True
ShowToolBar                               : True
ShowOutlining                             : True
ShowLineNumbers                           : True
TokenColors                               : {[Attribute, #FF00BFFF], [Command, #FF0000FF], [CommandArgument, #FF8A2BE2], [CommandParameter, #FF000080]...}
ConsoleTokenColors                        : {[Attribute, #FFB0C4DE], [Command, #FFE0FFFF], [CommandArgument, #FFEE82EE], [CommandParameter, #FFFFE4B5]...}
XmlTokenColors                            : {[Comment, #FF006400], [CommentDelimiter, #FF008000], [ElementName, #FF8B0000], [MarkupExtension, #FFFF8C00]...}
DefaultOptions                            : Microsoft.PowerShell.Host.ISE.ISEOptions
FontSize                                  : 9
Zoom                                      : 100
FontName                                  : Lucida Console
ErrorForegroundColor                      : #FFFF0000
ErrorBackgroundColor                      : #00FFFFFF
WarningForegroundColor                    : #FFFF8C00
WarningBackgroundColor                    : #00FFFFFF
VerboseForegroundColor                    : #FF00FFFF
VerboseBackgroundColor                    : #00FFFFFF
DebugForegroundColor                      : #FF00FFFF
DebugBackgroundColor                      : #00FFFFFF
ConsolePaneBackgroundColor                : #FF012456
ConsolePaneTextBackgroundColor            : #FF012456
ConsolePaneForegroundColor                : #FFF5F5F5
ScriptPaneBackgroundColor                 : #FFFFFFFF
ScriptPaneForegroundColor                 : #FF000000
ShowWarningForDuplicateFiles              : True
ShowWarningBeforeSavingOnRun              : True
UseLocalHelp                              : True
AutoSaveMinuteInterval                    : 2
MruCount                                  : 10
ShowIntellisenseInConsolePane             : True
ShowIntellisenseInScriptPane              : True
UseEnterToSelectInConsolePaneIntellisense : True
UseEnterToSelectInScriptPaneIntellisense  : True
IntellisenseTimeoutInSeconds              : 3
```

### <a name="errorbackgroundcolor"></a>ErrorBackgroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Adja meg a konzol ablaktáblában megjelenő hibaüzenet-szöveg háttérszíne. Egy példányát a **System.Windows.Media.Color** osztály.

```powershell
# Changes the background color for the error text that appears in the Console pane to black.
$psISE.Options.ErrorBackgroundColor = 'black'
```

### <a name="errorforegroundcolor"></a>ErrorForegroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Adja meg az előtér színe hiba szöveg jelenik meg a konzol ablaktáblában. Egy példányát a **System.Windows.Media.Color** osztály.

```powershell
# Changes the foreground color for the error text that appears in the console pane to green.
$psISE.Options.ErrorForegroundColor = 'green'
```

### <a name="fontname"></a>FontName

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Megadja a betűtípus neve jelenleg használja a parancsfájl panelen és a konzol panelen is.

```powershell
# Changes the font used in both panes.
$psISE.Options.FontName = 'Courier New'
```

### <a name="fontsize"></a>FontSize

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Egy egész számot határozza meg a betűméretet. A parancsfájl panelen, a parancs ablaktábla és a kimeneti ablaktábla használatban van. Az érvényes értékek tartománya 8 – 32.

```powershell
# Changes the font size in all panes.
$psISE.Options.FontSize = 20
```

### <a name="intellisensetimeoutinseconds"></a>IntellisenseTimeoutInSeconds

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Adja meg másodpercben, az IntelliSense használatával oldja fel az aktuálisan beírt szöveget. Másodpercek számát az IntelliSense túllépi az időkorlátot, és lehetővé teszi, írja be a folytatáshoz. Az alapértelmezett értéke 3 másodperc. Egész érték.

```powershell
# Changes the number of seconds for IntelliSense syntax recognition to 5.
$psISE.Options.IntellisenseTimeoutInSeconds = 5
```

### <a name="mrucount"></a>MruCount

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A Windows PowerShell ISE-ben nyomon követi és alján megjeleníti a legutóbb megnyitott fájlok számát adja meg a **fájl megnyitása** menü. Az alapértelmezett értéke 10. Egész érték.

```powershell
# Changes the number of recently used files that appear at the bottom of the File Open menu to 5.
$psISE.Options.MruCount = 5
```

### <a name="outputpanebackgroundcolor"></a>OutputPaneBackgroundColor

Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.  A későbbi verziókhoz, lásd: [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a Tesztkimenet ablaktáblán maga háttérszíne. Egy példányát a **System.Windows.Media.Color** osztály.

```powershell
# Changes the background color of the Output pane to gold.
$psISE.Options.OutputPaneForegroundColor = 'gold'
```

### <a name="outputpanetextforegroundcolor"></a>OutputPaneTextForegroundColor

Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.  A későbbi verziókhoz, lásd: [ConsolePaneForegroundColor](#consolepaneforegroundcolor).

Az olvasási/írási tulajdonság, amely a szöveget a Tesztkimenet ablaktáblán, a Windows PowerShell ISE 2.0 előterének színe megváltozik.

```powershell
# Changes the foreground color of the text in the Output Pane to blue.
$psISE.Options.OutputPaneTextForegroundColor  = 'blue'
```

### <a name="outputpanetextbackgroundcolor"></a>OutputPaneTextBackgroundColor

Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.  A későbbi verziókhoz, lásd: [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).

Az olvasási/írási tulajdonság, amely módosítja a Tesztkimenet ablaktáblán a szöveg háttérszíne.

```powershell
# Changes the background color of the Output pane text to pink.
$psISE.Options.OutputPaneTextBackgroundColor = 'pink'
```

### <a name="scriptpanebackgroundcolor"></a>ScriptPaneBackgroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a fájlokat a háttér színe. Egy példányát a **System.Windows.Media.Color** osztály.

```powershell
# Sets the color of the script pane background to yellow.
$psISE.Options.ScriptPaneBackgroundColor = 'yellow'
```

### <a name="scriptpaneforegroundcolor"></a>ScriptPaneForegroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a előtérszíne parancsfájl-fájlok esetében a parancsfájl panelen.
A parancsfájlokban előtérszíne beállításához használja a [TokenColors](#tokencolors).

```powershell
# Sets the foreground to color of non-script files in the script pane to green.
$psISE.Options.ScriptPaneBackgroundColor = 'green'
```

### <a name="selectedscriptpanestate"></a>SelectedScriptPaneState

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a parancsfájl panelen pozícióját megjelenítéséhez. A karakterlánc lehet "Maximized", "Top" vagy 'Jobbról'.

```powershell
# Moves the Script Pane to the top.
$psISE.Options.SelectedScriptPaneState = 'Top'
# Moves the Script Pane to the right.
$psISE.Options.SelectedScriptPaneState = 'Right'
# Maximizes the Script Pane
$psISE.Options.SelectedScriptPaneState = 'Maximized'
```

### <a name="showdefaultsnippets"></a>ShowDefaultSnippets

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Megadja, hogy a **CTRL + J** kódrészletek listája tartalmazza az alapszintű készlet, amely része a Windows PowerShellben. Ha a beállítása **$false**, csak a felhasználói kódrészletek jelennek meg a **CTRL + J** listája. Az alapértelmezett érték **$true**.

```powershell
# Hide the default snippets from the CTRL+J list.
$psISE.Options.ShowDefaultSnippets = $false
```

### <a name="showintellisenseinconsolepane"></a>ShowIntellisenseInConsolePane

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Itt adhatja meg, hogy IntelliSense kínál szintaxis paraméter és érték javaslatok a konzol ablaktáblában. Az alapértelmezett érték **$true**.

```powershell
# Turn off IntelliSense in the console pane.
$psISE.Options.ShowIntellisenseInConsolePane = $false
```

### <a name="showintellisenseinscriptpane"></a>ShowIntellisenseInScriptPane

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Itt adhatja meg, hogy IntelliSense kínál szintaxis paraméter és érték javaslatok a parancsfájl panelen. Az alapértelmezett érték **$true**.

```powershell
# Turn off IntelliSense in the Script pane.
$psISE.Options.ShowIntellisenseInScriptPane = $false
```

### <a name="showlinenumbers"></a>ShowLineNumbers

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Megadja, hogy e a parancsfájl panelen a bal margón sorszámok megjelenítése. Az alapértelmezett érték **$true**.

```powershell
# Turn off line numbers in the Script pane.
$psISE.Options.ShowLineNumbers = $false
```

### <a name="showoutlining"></a>ShowOutlining

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Megadja, hogy e megjeleníti-e a parancsfájl panelen bővíthető és összecsukható zárójelben mellett szabályzat szakaszok bal szélén. Amikor megjelennek, kattintson a mínusz \( - \) ikonok mellett kattintson a plusz kibonthatja vagy összecsukhatja, szövegblokk \( + \) ikonra kattintva bontsa ki a szöveget egy kódblokkot. Az alapértelmezett érték **$true**.

```powershell
# Turn off outlining in the Script pane.
$psISE.Options.ShowOutlining = $false
```

### <a name="showtoolbar"></a>EszköztárMegjelenítése

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Megadja, hogy az ISE eszköztár megjelenik-e a Windows PowerShell ISE-ablak tetején. Az alapértelmezett érték **$true**.

```powershell
# Show the toolbar.
$psISE.Options.ShowToolBar = $true
```

### <a name="showwarningbeforesavingonrun"></a>ShowWarningBeforeSavingOnRun

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Megadja, hogy egy figyelmeztető üzenet megjelenik-e a parancsfájl mentése automatikusan azt futtatása előtt. Az alapértelmezett érték **$true**.

```powershell
# Enable the warning message when an attempt
# is made to run a script without saving it first.
$psISE.Options.ShowWarningBeforeSavingOnRun = $true
```

### <a name="showwarningforduplicatefiles"></a>ShowWarningForDuplicateFiles

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Megadja, hogy egy figyelmeztető üzenet megjelenik-e ugyanabban a fájlban külön PowerShell-lapokon megnyitásakor. Ha beállítása **$true**, több lapokat jeleníti meg ugyanazt a fájlt megnyitni ezt az üzenetet: "Ez a fájl másolatát nyitva egy másik Windows PowerShell-lapon. Ez a fájl módosításait hatással lesz összes megnyitott másolatokat." Az alapértelmezett érték **$true**.

```powershell
# Enable the warning message when a file is
# opened in multiple PowerShell tabs.
$psISE.Options.ShowWarningForDuplicateFiles = $true
```

### <a name="tokencolors"></a>TokenColors

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A Windows PowerShell ISE parancsfájl panelen adja meg a színeket az IntelliSense jogkivonatokat. Ez a tulajdonság egy szótárobjektum, amely tartalmazza a név/érték párok tokentípusokat és a parancsfájl panelen színe. A konzolablakban az IntelliSense jogkivonatokat a színek módosításához lásd [ConsoleTokenColors](#consoletokencolors). A színek visszaáll az alapértelmezett értékeket, lásd: [RestoreDefaultTokenColors](#restoredefaulttokencolors). Token színek állíthat be a következőket: Attribútum parancs, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, szám, operátor, pozíciója, StatementSeparator, karakterlánc, típus, ismeretlen, változó.

```powershell
# Sets the color of commands to green.
$psISE.Options.TokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.TokenColors["Keyword"] = "magenta"
```

### <a name="useentertoselectinconsolepaneintellisense"></a>UseEnterToSelectInConsolePaneIntellisense

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Itt adhatja meg, hogy használhatja az IntelliSense megadott beállítást, a konzol ablaktáblában válassza ki az Enter billentyűt. Az alapértelmezett érték **$true**.

```powershell
# Turn off using the ENTER key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $false
```

### <a name="useentertoselectinscriptpaneintellisense"></a>UseEnterToSelectInScriptPaneIntellisense

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Itt adhatja meg, e segítségével az Enter billentyűt a parancsfájl panelen válassza ki az IntelliSense által biztosított lehetőséget. Az alapértelmezett érték **$true**.

```powershell
# Turn on using the Enter key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $true
```

### <a name="uselocalhelp"></a>UseLocalHelp

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Megadja, hogy a helyileg telepített súgó vagy az online TechNet könyvtár súgója megjelenik F1 kulcsszó elhelyezni a kurzor megnyomásakor. Ha beállítása **$true**, majd az előugró ablakban látható tartalom a helyileg telepített súgóból. A súgófájlok futtatásával telepítheti a `Update-Help` parancsot. Ha beállítása **$false**, akkor a böngészőben megnyílik egy lap a TechNet könyvtárban.

```powershell
# Sets the option for the online help to be displayed.
$psISE.Options.UseLocalHelp = $false
# Sets the option for the local Help to be displayed.
$psISE.Options.UseLocalHelp = $true
```

### <a name="verbosebackgroundcolor"></a>VerboseBackgroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Adja meg a konzol ablaktáblában megjelenő részletes szöveg háttérszíne. Ez egy **System.Windows.Media.Color** objektum.

```powershell
# Changes the background color for verbose text to blue.
$psISE.Options.VerboseBackgroundColor ='#0000FF'
```

### <a name="verboseforegroundcolor"></a>VerboseForegroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Adja meg a részletes megjelenő szöveg előtérszínét a konzol ablaktáblában. Ez egy **System.Windows.Media.Color** objektum.

```powershell
# Changes the foreground color for verbose text to yellow.
$psISE.Options.VerboseForegroundColor = 'yellow'
```

### <a name="warningbackgroundcolor"></a>WarningBackgroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Adja meg a konzol ablaktáblában megjelenő figyelmeztető szöveg háttérszíne. Ez egy **System.Windows.Media.Color** objektum.

```powershell
# Changes the background color for warning text to blue.
$psISE.Options.WarningBackgroundColor = '#0000FF'
```

### <a name="warningforegroundcolor"></a>WarningForegroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A megjelenő figyelmeztető szöveg előtérszínét megadja a Tesztkimenet ablaktáblán. Ez egy **System.Windows.Media.Color** objektum.

```powershell
# Changes the foreground color for warning text to yellow.
$psISE.Options.WarningForegroundColor = 'yellow'
```

### <a name="xmltokencolors"></a>XmlTokenColors

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Megadja a szótárobjektum, amely tokentípusokat és az XML-tartalom a Windows PowerShell ISE-ben megjelenő színeket név/érték párt tartalmaz. Token színek állíthat be a következőket: Attribútum parancs, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, szám, operátor, pozíciója, StatementSeparator, karakterlánc, típus, ismeretlen, változó. További tájékoztatás [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).

```powershell
# Sets the color of XML element names to green.
$psISE.Options.XmlTokenColors["ElementName"] = 'green'
# Sets the color of XML comments to magenta.
$psISE.Options.XmlTokenColors["Comment"] = 'magenta'
```

### <a name="zoom"></a>Nagyítás

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Megadja a szöveg relatív méretét a konzol és a parancsfájl ablaktáblán. Az alapértelmezett érték 100. A kisebb értékek miatt a szöveg jelenik meg, míg a nagyobb számot miatt szöveg jelenik meg a nagyobb kisebb Windows PowerShell ISE-ben. Az érték: egész szám, amely 20-ról a 400-as címtartományok.

```powershell
# Changes the text in the Windows PowerShell ISE to be double its normal size.
$psISE.Options.Zoom = 200
```

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)
