---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISEOptions objektum
ms.assetid: 75e2a76f-f3d1-490b-ad5d-e3829946aabb
ms.openlocfilehash: e756da21aaa5465f7fa6a90563b4180f0c89e87b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953650"
---
# <a name="the-iseoptions-object"></a>Az ISEOptions objektum

A **ISEOptions** objektum által jelképezett Windows PowerShell ISE különböző beállításait. A egy példánya a **Microsoft.PowerShell.Host.ISE.ISEOptions** osztály.

A **ISEOptions** objektumot biztosít a következő módszerek és tulajdonságait.

## <a name="methods"></a>Metódusok

### <a name="restoredefaultconsoletokencolors"></a>RestoreDefaultConsoleTokenColors\(\)

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Visszaállítja a konzol ablaktáblában token színek alapértelmezett értékeit.

```powershell
# Changes the color of the commands in the Console pane to red and then restores it to its default value.
$psISE.Options.ConsoleTokenColors["Command"] = 'red'
$psISE.Options.RestoreDefaultConsoleTokenColors()
```

### <a name="restoredefaults"></a>RestoreDefaults\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az alapértelmezett értékeket, a konzol ablaktáblában beállítások beállításainak visszaállítása. Adja meg a standard jelölőnégyzetet az üzenet ismét megjelenítésének különböző mellőzött figyelmeztető üzenet viselkedése is alaphelyzetbe állítja.

```powershell
# Changes the background color in the Console pane and then restores it to its default value.
$psISE.Options.ConsolePaneBackgroundColor = 'orange'
$psISE.Options.RestoreDefaults()
```

### <a name="restoredefaulttokencolors"></a>RestoreDefaultTokenColors\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Visszaállítja a parancssori panelbe token színek alapértelmezett értékeit.

```powershell
# Changes the color of the comments in the Script pane to red and then restores it to its default value.
$psISE.Options.TokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultTokenColors()
```

### <a name="restoredefaultxmltokencolors"></a>RestoreDefaultXmlTokenColors\(\)

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Visszaállítja a token XML-elemek Windows PowerShell ISE megjelenő színeinek alapértelmezett értékeit. Lásd még: [XmlTokenColors](#xmltokencolors).

```powershell
# Changes the color of the comments in XML data to red and then restores it to its default value.
$psISE.Options.XmlTokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultXmlTokenColors()
```

## <a name="properties"></a>Tulajdonságok

### <a name="autosaveminuteinterval"></a>AutoSaveMinuteInterval

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

A Windows PowerShell ISE által a fájlok automatikus mentési műveletek között eltelt percek számát adja meg. Az alapértelmezett érték 2 perc. Egész érték.

```powershell
# Changes the number of minutes between automatic save operations to every 3 minutes.
$psISE.Options.AutoSaveMinuteInterval = 3
```

### <a name="commandpanebackgroundcolor"></a>CommandPaneBackgroundColor

Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.  Újabb verzió, lásd: [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

Megadja a parancs panel hátterének színét. A egy példánya a **System.Windows.Media.Color** osztály.

```powershell
# Changes the background color of the Command pane to orange.
$psISE.Options.CommandPaneBackgroundColor = 'orange'
```

### <a name="commandpaneup"></a>CommandPaneUp

Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.

Meghatározza, hogy található-e a parancs ablaktábla fent a Tesztkimenet ablaktáblán.

```powershell
# Moves the Command pane to the top of the screen.
$psISE.Options.CommandPaneUp  = $true
```

### <a name="consolepanebackgroundcolor"></a>ConsolePaneBackgroundColor

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Adja meg a konzol ablaktáblában háttérszínét. A egy példánya a **System.Windows.Media.Color** osztály.

```powershell
# Changes the background color of the Console pane to red.
$psISE.Options.ConsolePaneBackgroundColor = 'red'
```

### <a name="consolepaneforegroundcolor"></a>ConsolePaneForegroundColor

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Megadja a szöveg előterének színét, a konzol ablaktáblában.

```powershell
# Changes the foreground color of the text in the Console pane to yellow.
$psISE.Options.ConsolePaneForegroundColor  = 'yellow'
```

### <a name="consolepanetextbackgroundcolor"></a>ConsolePaneTextBackgroundColor

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Megadja a szöveg hátterének színét a konzol ablaktáblában.

```powershell
# Changes the background color of the Console pane text to pink.
$psISE.Options.ConsolePaneTextBackgroundColor = 'pink'
```

### <a name="consoletokencolors"></a>ConsoleTokenColors

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Adja meg az IntelliSense jogkivonatok színeit a Windows PowerShell ISE konzoljába ablaktáblán. Ez a tulajdonság egy név/érték párok tokentípusokat és a konzol ablaktáblában színeket tartalmazó szótárobjektum. A parancssori panelbe IntelliSense jogkivonatok a színek módosításához lásd [TokenColors](#tokencolors). A színek visszaállítása az alapértelmezett értékeket, lásd: [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors). Token színek állíthat be a következőt: attribútum, parancsot, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, számot, operátor, pozíciója, StatementSeparator, karakterlánc, típusa, Ismeretlen, változó.

```powershell
# Sets the color of commands to green.
$psISE.Options.ConsoleTokenColors["Command"] = 'green'
# Sets the color of keywords to magenta.
$psISE.Options.ConsoleTokenColors["Keyword"] = 'magenta'
```

### <a name="debugbackgroundcolor"></a>DebugBackgroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Határozza meg a konzol ablaktáblában megjelenő hibakeresési szöveg háttérszínét. A egy példánya a **System.Windows.Media.Color** osztály.

```powershell
# Changes the background color for the debug text that appears in the Console pane to blue.
$psISE.Options.DebugBackgroundColor = '#0000FF'
```

### <a name="debugforegroundcolor"></a>DebugForegroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Határozza meg a konzol ablaktáblában megjelenő hibakeresési szöveg előtérszínét. A egy példánya a **System.Windows.Media.Color** osztály.

```powershell
# Changes the foreground color for the debug text that appears in the Console pane to yellow.
$psISE.Options.DebugForegroundColor = 'yellow'
```

### <a name="defaultoptions"></a>DefaultOptions

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az alapértelmezett értékeket kell használni, ha a visszaállítási módszerek használhatók megadó tulajdonságok gyűjteménye.

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

Adja meg a hiba szövegének háttérszínét a konzol ablaktáblában. A egy példánya a **System.Windows.Media.Color** osztály.

```powershell
# Changes the background color for the error text that appears in the Console pane to black.
$psISE.Options.ErrorBackgroundColor = 'black'
```

### <a name="errorforegroundcolor"></a>ErrorForegroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A konzol ablaktáblában határozza meg a hiba szövegének előtérszínét. A egy példánya a **System.Windows.Media.Color** osztály.

```powershell
# Changes the foreground color for the error text that appears in the console pane to green.
$psISE.Options.ErrorForegroundColor = 'green'
```

### <a name="fontname"></a>FontName

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Neve a betűtípus jelenleg használatban lévő mind a parancsfájl és a konzol ablaktábla.

```powershell
# Changes the font used in both panes.
$psISE.Options.FontName = 'Courier New'
```

### <a name="fontsize"></a>FontSize

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A betűtípus méretét adja meg egy egész számot. A parancssori panelbe, a parancs ablaktábla és a kimeneti ablaktábla használatban van. Az érvényes értékek tartománya 8 – 32.

```powershell
# Changes the font size in all panes.
$psISE.Options.FontSize = 20
```

### <a name="intellisensetimeoutinseconds"></a>IntellisenseTimeoutInSeconds

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Adja meg másodpercben, hogy az IntelliSense segítségével oldja fel az éppen gépelt szöveg. A megadott számú másodperc után IntelliSense érvénytelenné válik, és lehetővé teszi a folytatáshoz írja be. Az alapértelmezett érték: 3 másodpercet. Egész érték.

```powershell
# Changes the number of seconds for IntelliSense syntax recognition to 5.
$psISE.Options.IntellisenseTimeoutInSeconds = 5
```

### <a name="mrucount"></a>MruCount

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

A Windows PowerShell ISE nyomon követi, és alján megjeleníti a legutóbb megnyitott fájlok számát adja meg a **fájl megnyitása** menü. Az alapértelmezett értéke 10. Egész érték.

```powershell
# Changes the number of recently used files that appear at the bottom of the File Open menu to 5.
$psISE.Options.MruCount = 5
```

### <a name="outputpanebackgroundcolor"></a>OutputPaneBackgroundColor

Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.  Újabb verzió, lásd: [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).

Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a Tesztkimenet ablaktáblán maga háttérszínét. A egy példánya a **System.Windows.Media.Color** osztály.

```powershell
# Changes the background color of the Output pane to gold.
$psISE.Options.OutputPaneForegroundColor = 'gold'
```

### <a name="outputpanetextforegroundcolor"></a>OutputPaneTextForegroundColor

Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.  Újabb verzió, lásd: [ConsolePaneForegroundColor](#consolepaneforegroundcolor).

Az olvasási/írási tulajdonság, amely módosítja a Windows PowerShell ISE 2.0 kimeneti ablakában a szöveg előterének színét.

```powershell
# Changes the foreground color of the text in the Output Pane to blue.
$psISE.Options.OutputPaneTextForegroundColor  = 'blue'
```

### <a name="outputpanetextbackgroundcolor"></a>OutputPaneTextBackgroundColor

Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.  Újabb verzió, lásd: [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).

Az olvasási/írási tulajdonság, amely megváltoztatja a Tesztkimenet ablaktáblán szöveg háttérszínét.

```powershell
# Changes the background color of the Output pane text to pink.
$psISE.Options.OutputPaneTextBackgroundColor = 'pink'
```

### <a name="scriptpanebackgroundcolor"></a>ScriptPaneBackgroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a fájlok háttérszínét. A egy példánya a **System.Windows.Media.Color** osztály.

```powershell
# Sets the color of the script pane background to yellow.
$psISE.Options.ScriptPaneBackgroundColor = 'yellow'
```

### <a name="scriptpaneforegroundcolor"></a>ScriptPaneForegroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Lekérdezi vagy beállítja a rácsterület előtérszínét, parancsfájl-fájlok esetében parancssori panelbe olvasási/írási tulajdonság.
A parancsfájlok előtérszínét beállításához használja a [TokenColors](#tokencolors).

```powershell
# Sets the foreground to color of non-script files in the script pane to green.
$psISE.Options.ScriptPaneBackgroundColor = 'green'
```

### <a name="selectedscriptpanestate"></a>SelectedScriptPaneState

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a parancsfájl ablak pozícióját az képernyőjén. A karakterlánc lehet "Maximized", "Top" vagy "Jobbra".

```powershell
# Moves the Script Pane to the top.
$psISE.Options.SelectedScriptPaneState = 'Top'
# Moves the Script Pane to the right.
$psISE.Options.SelectedScriptPaneState = 'Right'
# Maximizes the Script Pane
$psISE.Options.SelectedScriptPaneState = 'Maximized'
```

### <a name="showdefaultsnippets"></a>ShowDefaultSnippets

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Megadja, hogy a **CTRL + J** kódtöredékek listáját tartalmazza az alapszintű, amelyek része a Windows PowerShell. Ha beállítása **$false**, csak a felhasználó által definiált kódtöredékek megjelennek a **CTRL + J** listája. Az alapértelmezett érték **$true**.

```powershell
# Hide the default snippets from the CTRL+J list.
$psISE.Options.ShowDefaultSnippets = $false
```

### <a name="showintellisenseinconsolepane"></a>ShowIntellisenseInConsolePane

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Meghatározza, hogy az IntelliSense kínál szintaxis paraméter és érték javaslatok a konzol ablaktáblában. Az alapértelmezett érték **$true**.

```powershell
# Turn off IntelliSense in the console pane.
$psISE.Options.ShowIntellisenseInConsolePane = $false
```

### <a name="showintellisenseinscriptpane"></a>ShowIntellisenseInScriptPane

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Határozza meg, hogy az IntelliSense kínál szintaxis paraméter és érték javaslatok panelbe. Az alapértelmezett érték **$true**.

```powershell
# Turn off IntelliSense in the Script pane.
$psISE.Options.ShowIntellisenseInScriptPane = $false
```

### <a name="showlinenumbers"></a>ShowLineNumbers

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Meghatározza, hogy a parancsfájl ablaktáblán megjelennek-e a bal margón sorok számát. Az alapértelmezett érték **$true**.

```powershell
# Turn off line numbers in the Script pane.
$psISE.Options.ShowLineNumbers = $false
```

### <a name="showoutlining"></a>ShowOutlining

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Meghatározza, hogy a parancsfájl ablaktáblán megjelennek-e a bal margón bővíthető és összecsukható zárójeleket melletti kód szakaszait. Amikor jelennek meg, kattintson a mínusz \( - \) ikonok mellett csukja össze, vagy kattintson a plusz szövegblokk \( + \) ikonra kattintva bontsa ki a szövegblokk. Az alapértelmezett érték **$true**.

```powershell
# Turn off outlining in the Script pane.
$psISE.Options.ShowOutlining = $false
```

### <a name="showtoolbar"></a>EszköztárMegjelenítése

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Megadja, hogy az ISE eszköztár megjelenik-e a Windows PowerShell ISE ablak tetején. Az alapértelmezett érték **$true**.

```powershell
# Show the toolbar.
$psISE.Options.ShowToolBar = $true
```

### <a name="showwarningbeforesavingonrun"></a>ShowWarningBeforeSavingOnRun

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Megadja, hogy egy figyelmeztető üzenet megjelenik-e a parancsfájl mentése automatikusan fut, mielőtt. Az alapértelmezett érték **$true**.

```powershell
# Enable the warning message when an attempt
# is made to run a script without saving it first.
$psISE.Options.ShowWarningBeforeSavingOnRun = $true
```

### <a name="showwarningforduplicatefiles"></a>ShowWarningForDuplicateFiles

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Meghatározza, hogy megjelenik egy figyelmeztető üzenet ugyanazt a fájlt másik PowerShell lapok megnyitása. Ha beállítása **$true**, ugyanazt a fájlt megnyitni több lapokat jeleníti meg ezt az üzenetet: "Ez a fájl másolatát nyitva egy másik Windows PowerShell-lapon. Ez a fájl módosításait hatással lesz az összes nyitott másolatok." Az alapértelmezett érték **$true**.

```powershell
# Enable the warning message when a file is
# opened in multiple PowerShell tabs.
$psISE.Options.ShowWarningForDuplicateFiles = $true
```

### <a name="tokencolors"></a>TokenColors

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Megadja a IntelliSense jogkivonatok színek a Windows PowerShell ISE parancsfájl ablaktáblán. Ez a tulajdonság egy név/érték párok tokentípusokat és a parancssori panelbe színeket tartalmazó szótárobjektum. A konzolpanelen IntelliSense jogkivonatok színek módosításához lásd [ConsoleTokenColors](#consoletokencolors). A színek visszaállítása az alapértelmezett értékeket, lásd: [RestoreDefaultTokenColors](#restoredefaulttokencolors). Token színek állíthat be a következőt: attribútum, parancsot, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, számot, operátor, pozíciója, StatementSeparator, karakterlánc, típusa, Ismeretlen, változó.

```powershell
# Sets the color of commands to green.
$psISE.Options.TokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.TokenColors["Keyword"] = "magenta"
```

### <a name="useentertoselectinconsolepaneintellisense"></a>UseEnterToSelectInConsolePaneIntellisense

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Meghatározza, hogy használhatja az IntelliSense megadott beállítást, a konzol ablaktáblában jelölje be az Enter billentyűt. Az alapértelmezett érték **$true**.

```powershell
# Turn off using the ENTER key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $false
```

### <a name="useentertoselectinscriptpaneintellisense"></a>UseEnterToSelectInScriptPaneIntellisense

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Meghatározza, hogy használhatja a parancssori panelbe IntelliSense által biztosított beállítás kiválasztása az Enter billentyűt. Az alapértelmezett érték **$true**.

```powershell
# Turn on using the Enter key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $true
```

### <a name="uselocalhelp"></a>UseLocalHelp

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Megadja, hogy a helyileg telepített súgó vagy a TechNet Library súgó megjelenik a kurzor kulcsszó elhelyezni az F1 billentyű megnyomásakor. Ha beállítása **$true**, majd a helyileg telepített súgóból előugró ablak látható tartalom. A súgófájlok futtatásával telepíthető a `Update-Help` parancsot. Ha beállítása **$false**, akkor a böngésző nyitja meg a lap a TechNet könyvtárban.

```powershell
# Sets the option for the online help to be displayed.
$psISE.Options.UseLocalHelp = $false
# Sets the option for the local Help to be displayed.
$psISE.Options.UseLocalHelp = $true
```

### <a name="verbosebackgroundcolor"></a>VerboseBackgroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Adja meg a konzol ablaktáblában részletes megjelenő szöveg háttérszínét. Ez egy **System.Windows.Media.Color** objektum.

```powershell
# Changes the background color for verbose text to blue.
$psISE.Options.VerboseBackgroundColor ='#0000FF'
```

### <a name="verboseforegroundcolor"></a>VerboseForegroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A konzol ablaktáblában határozza meg a részletes megjelenő szöveg előterének színét. Ez egy **System.Windows.Media.Color** objektum.

```powershell
# Changes the foreground color for verbose text to yellow.
$psISE.Options.VerboseForegroundColor = 'yellow'
```

### <a name="warningbackgroundcolor"></a>WarningBackgroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Adja meg a konzol ablaktáblában megjelenő figyelmeztető szöveg háttérszínét. Ez egy **System.Windows.Media.Color** objektum.

```powershell
# Changes the background color for warning text to blue.
$psISE.Options.WarningBackgroundColor = '#0000FF'
```

### <a name="warningforegroundcolor"></a>WarningForegroundColor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Adja meg a Tesztkimenet ablaktáblán megjelenő figyelmeztető szöveg előterének színét. Ez egy **System.Windows.Media.Color** objektum.

```powershell
# Changes the foreground color for warning text to yellow.
$psISE.Options.WarningForegroundColor = 'yellow'
```

### <a name="xmltokencolors"></a>XmlTokenColors

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Adja meg a név/érték párok tokentípusokat és XML-tartalom a Windows PowerShell ISE megjelenített színeket tartalmazó szótárobjektum. Token színek állíthat be a következőt: attribútum, parancsot, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, számot, operátor, pozíciója, StatementSeparator, karakterlánc, típusa, Ismeretlen, változó. Lásd még: [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).

```powershell
# Sets the color of XML element names to green.
$psISE.Options.XmlTokenColors["ElementName"] = 'green'
# Sets the color of XML comments to magenta.
$psISE.Options.XmlTokenColors["Comment"] = 'magenta'
```

### <a name="zoom"></a>Nagyítás

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Meghatározza a szöveg relatív méretét a konzol és a parancsfájl ablaktáblán. Az alapértelmezett érték 100. A kisebb értékek miatt a szöveg, a Windows PowerShell ISE kisebb megjelenését, miközben több okozhat nagyobb megjelenítendő szöveget. Az érték egész szám, amely az 20 a 400-as.

```powershell
# Changes the text in the Windows PowerShell ISE to be double its normal size.
$psISE.Options.Zoom = 200
```

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE objektummodell Scripting célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)