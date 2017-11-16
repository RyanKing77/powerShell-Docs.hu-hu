---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISEOptions objektum
ms.assetid: 75e2a76f-f3d1-490b-ad5d-e3829946aabb
ms.openlocfilehash: 5e04adeebacfb9214bf39d9ec9c5f0e01f5729ee
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="the-iseoptions-object"></a><span data-ttu-id="e1825-103">A ISEOptions objektum</span><span class="sxs-lookup"><span data-stu-id="e1825-103">The ISEOptions Object</span></span>
  <span data-ttu-id="e1825-104">A **ISEOptions** objektum által jelképezett Windows PowerShell ISE különböző beállításait.</span><span class="sxs-lookup"><span data-stu-id="e1825-104">The **ISEOptions** object represents various settings for Windows PowerShell ISE.</span></span> <span data-ttu-id="e1825-105">A egy példánya a **Microsoft.PowerShell.Host.ISE.ISEOptions** osztály.</span><span class="sxs-lookup"><span data-stu-id="e1825-105">It is an instance of the **Microsoft.PowerShell.Host.ISE.ISEOptions** class.</span></span>

 <span data-ttu-id="e1825-106">A **ISEOptions** objektumot biztosít a következő módszerek és tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="e1825-106">The **ISEOptions** object provides the following methods and properties.</span></span>

## <a name="methods"></a><span data-ttu-id="e1825-107">Metódusok</span><span class="sxs-lookup"><span data-stu-id="e1825-107">Methods</span></span>

### <a name="restoredefaultconsoletokencolors"></a><span data-ttu-id="e1825-108">RestoreDefaultConsoleTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="e1825-108">RestoreDefaultConsoleTokenColors\(\)</span></span>
  <span data-ttu-id="e1825-109">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-110">Visszaállítja a konzol ablaktáblában token színek alapértelmezett értékeit.</span><span class="sxs-lookup"><span data-stu-id="e1825-110">Restores the default values of the token colors in the Console pane.</span></span>

```
# Changes the color of the commands in the Console pane to red and then restores it to its default value.
$psISE.Options.ConsoleTokenColors["Command"] = "red"
$psISE.Options.RestoreDefaultConsoleTokenColors()
```

### <a name="restoredefaults"></a><span data-ttu-id="e1825-111">RestoreDefaults\(\)</span><span class="sxs-lookup"><span data-stu-id="e1825-111">RestoreDefaults\(\)</span></span>
  <span data-ttu-id="e1825-112">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-112">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-113">Az alapértelmezett értékeket, a konzol ablaktáblában beállítások beállításainak visszaállítása.</span><span class="sxs-lookup"><span data-stu-id="e1825-113">Restores the default values of all options settings in the Console pane.</span></span> <span data-ttu-id="e1825-114">Adja meg a standard jelölőnégyzetet az üzenet ismét megjelenítésének különböző mellőzött figyelmeztető üzenet viselkedése is alaphelyzetbe állítja.</span><span class="sxs-lookup"><span data-stu-id="e1825-114">It also resets the behavior of various warning messages that provide the standard check box to prevent the message from being shown again.</span></span>

```
# Changes the background color in the Console pane and then restores it to its default value.
$psISE.Options.ConsolePaneBackgroundColor = "orange"
$psISE.Options.RestoreDefaults()
```

### <a name="restoredefaulttokencolors"></a><span data-ttu-id="e1825-115">RestoreDefaultTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="e1825-115">RestoreDefaultTokenColors\(\)</span></span>
  <span data-ttu-id="e1825-116">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-116">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-117">Visszaállítja a parancssori panelbe token színek alapértelmezett értékeit.</span><span class="sxs-lookup"><span data-stu-id="e1825-117">Restores the default values of the token colors in the Script pane.</span></span>

```
# Changes the color of the comments in the Script pane to red and then restores it to its default value.
$psISE.Options.TokenColors["Comment"]="red"
$psISE.Options.RestoreDefaultTokenColors()
```

### <a name="restoredefaultxmltokencolors"></a><span data-ttu-id="e1825-118">RestoreDefaultXmlTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="e1825-118">RestoreDefaultXmlTokenColors\(\)</span></span>
  <span data-ttu-id="e1825-119">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-119">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-120">Visszaállítja a token XML-elemek Windows PowerShell ISE megjelenő színeinek alapértelmezett értékeit.</span><span class="sxs-lookup"><span data-stu-id="e1825-120">Restores the default values of the token colors for XML elements that are displayed in Windows PowerShell ISE.</span></span> <span data-ttu-id="e1825-121">Lásd még: [XmlTokenColors](#xmltokencolors).</span><span class="sxs-lookup"><span data-stu-id="e1825-121">Also see [XmlTokenColors](#xmltokencolors).</span></span>

```
# Changes the color of the comments in XML data to red and then restores it to its default value.
$psISE.Options.XmlTokenColors["Comment"]="red"
$psISE.Options.RestoreDefaultXmlTokenColors()
```

## <a name="properties"></a><span data-ttu-id="e1825-122">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="e1825-122">Properties</span></span>

### <a name="autosaveminuteinterval"></a><span data-ttu-id="e1825-123">AutoSaveMinuteInterval</span><span class="sxs-lookup"><span data-stu-id="e1825-123">AutoSaveMinuteInterval</span></span>
  <span data-ttu-id="e1825-124">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-125">A Windows PowerShell ISE által a fájlok automatikus mentési műveletek között eltelt percek számát adja meg.</span><span class="sxs-lookup"><span data-stu-id="e1825-125">Specifies the number of minutes between automatic save operations of your files by Windows PowerShell ISE.</span></span> <span data-ttu-id="e1825-126">Az alapértelmezett érték 2 perc.</span><span class="sxs-lookup"><span data-stu-id="e1825-126">The default value is 2 minutes.</span></span> <span data-ttu-id="e1825-127">Egész érték.</span><span class="sxs-lookup"><span data-stu-id="e1825-127">The value is an integer.</span></span>

```
# Changes the number of minutes between automatic save operations to every 3 minutes.
$psISE.Options.AutoSaveMinuteInterval = 3
```

### <a name="commandpanebackgroundcolor"></a><span data-ttu-id="e1825-128">CommandPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-128">CommandPaneBackgroundColor</span></span>
  <span data-ttu-id="e1825-129">Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="e1825-129">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="e1825-130">Újabb verzió, lásd: [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span><span class="sxs-lookup"><span data-stu-id="e1825-130">For later versions, see [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span></span>

 <span data-ttu-id="e1825-131">Megadja a parancs panel hátterének színét.</span><span class="sxs-lookup"><span data-stu-id="e1825-131">Specifies the background color for the Command pane.</span></span> <span data-ttu-id="e1825-132">A egy példánya a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="e1825-132">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the background color of the Command pane to orange.
$psISE.Options.CommandPaneBackgroundColor = "orange"
```

### <a name="commandpaneup"></a><span data-ttu-id="e1825-133">CommandPaneUp</span><span class="sxs-lookup"><span data-stu-id="e1825-133">CommandPaneUp</span></span>
  <span data-ttu-id="e1825-134">Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="e1825-134">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>

 <span data-ttu-id="e1825-135">Meghatározza, hogy található-e a parancs ablaktábla fent a Tesztkimenet ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="e1825-135">Specifies whether the Command pane is located above the Output pane.</span></span>

```
# Moves the Command pane to the top of the screen.
$psISE.Options.CommandPaneUp  = $true

```

### <a name="consolepanebackgroundcolor"></a><span data-ttu-id="e1825-136">ConsolePaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-136">ConsolePaneBackgroundColor</span></span>
  <span data-ttu-id="e1825-137">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-137">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-138">Adja meg a konzol ablaktáblában háttérszínét.</span><span class="sxs-lookup"><span data-stu-id="e1825-138">Specifies the background color for the Console pane.</span></span> <span data-ttu-id="e1825-139">A egy példánya a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="e1825-139">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the background color of the Console pane to red.
$psISE.Options.ConsolePaneBackgroundColor = "red"
```

### <a name="consolepaneforegroundcolor"></a><span data-ttu-id="e1825-140">ConsolePaneForegroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-140">ConsolePaneForegroundColor</span></span>
  <span data-ttu-id="e1825-141">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-141">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-142">Megadja a szöveg előterének színét, a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="e1825-142">Specifies the foreground color of the text in the Console pane.</span></span>

```
# Changes the foreground color of the text in the Console pane to yellow.
$psISE.Options.ConsolePaneForegroundColor  = "yellow"

```

### <a name="consolepanetextbackgroundcolor"></a><span data-ttu-id="e1825-143">ConsolePaneTextBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-143">ConsolePaneTextBackgroundColor</span></span>
  <span data-ttu-id="e1825-144">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-144">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-145">Megadja a szöveg hátterének színét a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="e1825-145">Specifies the background color of the text in the Console pane.</span></span>

```
# Changes the background color of the Console pane text to pink.
$psISE.Options.ConsolePaneTextBackgroundColor = "pink"
```

### <a name="consoletokencolors"></a><span data-ttu-id="e1825-146">ConsoleTokenColors</span><span class="sxs-lookup"><span data-stu-id="e1825-146">ConsoleTokenColors</span></span>
  <span data-ttu-id="e1825-147">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-147">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-148">Adja meg az IntelliSense jogkivonatok színeit a Windows PowerShell ISE konzoljába ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="e1825-148">Specifies the colors of the IntelliSense tokens in the Windows PowerShell ISE Console pane.</span></span> <span data-ttu-id="e1825-149">Ez a tulajdonság egy név/érték párok tokentípusokat és a konzol ablaktáblában színeket tartalmazó szótárobjektum.</span><span class="sxs-lookup"><span data-stu-id="e1825-149">This property is a dictionary object that contains name/value pairs of token types and colors for the Console pane.</span></span> <span data-ttu-id="e1825-150">A parancssori panelbe IntelliSense jogkivonatok a színek módosításához lásd [TokenColors](#tokencolors).</span><span class="sxs-lookup"><span data-stu-id="e1825-150">To change the colors of the IntelliSense tokens in the Script pane, see [TokenColors](#tokencolors).</span></span> <span data-ttu-id="e1825-151">A színek visszaállítása az alapértelmezett értékeket, lásd: [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors).</span><span class="sxs-lookup"><span data-stu-id="e1825-151">To reset the colors to the default values, see [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors).</span></span> <span data-ttu-id="e1825-152">Token színek állíthat be a következőt: attribútum, parancsot, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, számot, operátor, pozíciója, StatementSeparator, karakterlánc, típusa, Ismeretlen, változó.</span><span class="sxs-lookup"><span data-stu-id="e1825-152">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span>

```
# Sets the color of commands to green.
$psISE.Options.ConsoleTokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.ConsoleTokenColors["Keyword"] = "magenta"

```

### <a name="debugbackgroundcolor"></a><span data-ttu-id="e1825-153">DebugBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-153">DebugBackgroundColor</span></span>
  <span data-ttu-id="e1825-154">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-154">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-155">Határozza meg a konzol ablaktáblában megjelenő hibakeresési szöveg háttérszínét.</span><span class="sxs-lookup"><span data-stu-id="e1825-155">Specifies the background color for the debug text that appears in the Console pane.</span></span> <span data-ttu-id="e1825-156">A egy példánya a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="e1825-156">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the background color for the debug text that appears in the Console pane to blue.
$psISE.Options.DebugBackgroundColor ='#0000FF'
```

### <a name="debugforegroundcolor"></a><span data-ttu-id="e1825-157">DebugForegroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-157">DebugForegroundColor</span></span>
  <span data-ttu-id="e1825-158">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-158">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-159">Határozza meg a konzol ablaktáblában megjelenő hibakeresési szöveg előtérszínét.</span><span class="sxs-lookup"><span data-stu-id="e1825-159">Specifies the foreground color for the debug text that appears in the Console pane.</span></span> <span data-ttu-id="e1825-160">A egy példánya a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="e1825-160">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the foreground color for the debug text that appears in the Console pane to yellow.
$psISE.Options.DebugForegroundColor ="yellow"
```

### <a name="defaultoptions"></a><span data-ttu-id="e1825-161">DefaultOptions</span><span class="sxs-lookup"><span data-stu-id="e1825-161">DefaultOptions</span></span>
  <span data-ttu-id="e1825-162">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-162">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-163">Az alapértelmezett értékeket kell használni, ha a visszaállítási módszerek használhatók megadó tulajdonságok gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="e1825-163">A collection of properties that specify the default values to be used when the Reset methods are used.</span></span>

```
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

### <a name="errorbackgroundcolor"></a><span data-ttu-id="e1825-164">ErrorBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-164">ErrorBackgroundColor</span></span>
  <span data-ttu-id="e1825-165">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-165">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-166">Adja meg a hiba szövegének háttérszínét a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="e1825-166">Specifies the background color for error text that appears in the Console pane.</span></span> <span data-ttu-id="e1825-167">A egy példánya a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="e1825-167">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the background color for the error text that appears in the Console pane to black.
$psISE.Options.ErrorBackgroundColor="black"
```

### <a name="errorforegroundcolor"></a><span data-ttu-id="e1825-168">ErrorForegroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-168">ErrorForegroundColor</span></span>
  <span data-ttu-id="e1825-169">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-169">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-170">A konzol ablaktáblában határozza meg a hiba szövegének előtérszínét.</span><span class="sxs-lookup"><span data-stu-id="e1825-170">Specifies the foreground color for error text that appears in the Console pane.</span></span> <span data-ttu-id="e1825-171">A egy példánya a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="e1825-171">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the foreground color for the error text that appears in the console pane to green.
$psISE.Options.ErrorForegroundColor ="green"
```

### <a name="fontname"></a><span data-ttu-id="e1825-172">FontName</span><span class="sxs-lookup"><span data-stu-id="e1825-172">FontName</span></span>
  <span data-ttu-id="e1825-173">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-173">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-174">Neve a betűtípus jelenleg használatban lévő mind a parancsfájl és a konzol ablaktábla.</span><span class="sxs-lookup"><span data-stu-id="e1825-174">Specifies the font name currently in use in both the Script pane and the Console pane.</span></span>

```
# Changes the font used in both panes.
$psISE.Options.FontName = "courier new"
```

### <a name="fontsize"></a><span data-ttu-id="e1825-175">FontSize</span><span class="sxs-lookup"><span data-stu-id="e1825-175">FontSize</span></span>
  <span data-ttu-id="e1825-176">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-176">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-177">A betűtípus méretét adja meg egy egész számot.</span><span class="sxs-lookup"><span data-stu-id="e1825-177">Specifies the font size as an integer.</span></span> <span data-ttu-id="e1825-178">A parancssori panelbe, a parancs ablaktábla és a kimeneti ablaktábla használatban van.</span><span class="sxs-lookup"><span data-stu-id="e1825-178">It is used in the Script pane, the Command pane, and the Output pane.</span></span> <span data-ttu-id="e1825-179">Az érvényes értékek tartománya 8 – 32.</span><span class="sxs-lookup"><span data-stu-id="e1825-179">The valid range of values is 8 through 32.</span></span>

```
# Changes the font size in all panes.
$psISE.Options.FontSize = 20

```

### <a name="intellisensetimeoutinseconds"></a><span data-ttu-id="e1825-180">IntellisenseTimeoutInSeconds</span><span class="sxs-lookup"><span data-stu-id="e1825-180">IntellisenseTimeoutInSeconds</span></span>
  <span data-ttu-id="e1825-181">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-181">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-182">Adja meg másodpercben, hogy az IntelliSense segítségével oldja fel az éppen gépelt szöveg.</span><span class="sxs-lookup"><span data-stu-id="e1825-182">Specifies the number of seconds that IntelliSense uses to try to resolve the currently typed text.</span></span> <span data-ttu-id="e1825-183">A megadott számú másodperc után IntelliSense érvénytelenné válik, és lehetővé teszi a folytatáshoz írja be.</span><span class="sxs-lookup"><span data-stu-id="e1825-183">After this number of seconds, IntelliSense times out and enables you to continue typing.</span></span> <span data-ttu-id="e1825-184">Az alapértelmezett érték: 3 másodpercet.</span><span class="sxs-lookup"><span data-stu-id="e1825-184">The default value is 3 seconds.</span></span> <span data-ttu-id="e1825-185">Egész érték.</span><span class="sxs-lookup"><span data-stu-id="e1825-185">The value is an integer.</span></span>

```
# Changes the number of seconds for IntelliSense syntax recognition to 5.
$psISE.Options.IntellisenseTimeoutInSeconds = 5
```

### <a name="mrucount"></a><span data-ttu-id="e1825-186">MruCount</span><span class="sxs-lookup"><span data-stu-id="e1825-186">MruCount</span></span>
  <span data-ttu-id="e1825-187">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-187">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-188">A Windows PowerShell ISE nyomon követi, és alján megjeleníti a legutóbb megnyitott fájlok számát adja meg a **fájl megnyitása** menü.</span><span class="sxs-lookup"><span data-stu-id="e1825-188">Specifies the number of recently opened files that Windows PowerShell ISE tracks and displays at the bottom of the **File Open** menu.</span></span> <span data-ttu-id="e1825-189">Az alapértelmezett értéke 10.</span><span class="sxs-lookup"><span data-stu-id="e1825-189">The default value is 10.</span></span> <span data-ttu-id="e1825-190">Egész érték.</span><span class="sxs-lookup"><span data-stu-id="e1825-190">The value is an integer.</span></span>

```
# Changes the number of recently used files that appear at the bottom of the File Open menu to 5.
$psISE.Options.MruCount = 5
```

### <a name="outputpanebackgroundcolor"></a><span data-ttu-id="e1825-191">OutputPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-191">OutputPaneBackgroundColor</span></span>
  <span data-ttu-id="e1825-192">Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="e1825-192">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="e1825-193">Újabb verzió, lásd: [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span><span class="sxs-lookup"><span data-stu-id="e1825-193">For later versions, see [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span></span>

 <span data-ttu-id="e1825-194">Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a Tesztkimenet ablaktáblán maga háttérszínét.</span><span class="sxs-lookup"><span data-stu-id="e1825-194">The read/write property that gets or sets the background color for the Output pane itself.</span></span> <span data-ttu-id="e1825-195">A egy példánya a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="e1825-195">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```
# Changes the background color of the Output pane to gold.
$psISE.Options.OutputPaneForegroundColor = "gold"

```

### <a name="outputpanetextforegroundcolor"></a><span data-ttu-id="e1825-196">OutputPaneTextForegroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-196">OutputPaneTextForegroundColor</span></span>
  <span data-ttu-id="e1825-197">Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="e1825-197">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="e1825-198">Újabb verzió, lásd: [ConsolePaneForegroundColor](#consolepaneforegroundcolor).</span><span class="sxs-lookup"><span data-stu-id="e1825-198">For later versions, see [ConsolePaneForegroundColor](#consolepaneforegroundcolor).</span></span>

 <span data-ttu-id="e1825-199">Az olvasási/írási tulajdonság, amely módosítja a Windows PowerShell ISE 2.0 kimeneti ablakában a szöveg előterének színét.</span><span class="sxs-lookup"><span data-stu-id="e1825-199">The read/write property that changes the foreground color of the text in the Output pane in Windows PowerShell ISE 2.0.</span></span>

```
# Changes the foreground color of the text in the Output Pane to blue.
$psISE.Options.OutputPaneTextForegroundColor  = "blue"

```

### <a name="outputpanetextbackgroundcolor"></a><span data-ttu-id="e1825-200">OutputPaneTextBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-200">OutputPaneTextBackgroundColor</span></span>
  <span data-ttu-id="e1825-201">Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="e1825-201">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="e1825-202">Újabb verzió, lásd: [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).</span><span class="sxs-lookup"><span data-stu-id="e1825-202">For later versions, see [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).</span></span>

 <span data-ttu-id="e1825-203">Az olvasási/írási tulajdonság, amely megváltoztatja a Tesztkimenet ablaktáblán szöveg háttérszínét.</span><span class="sxs-lookup"><span data-stu-id="e1825-203">The read/write property that changes the background color of the text in the Output pane.</span></span>

```
# Changes the background color of the Output pane text to pink.
$psISE.Options.OutputPaneTextBackgroundColor = "pink"
```

### <a name="scriptpanebackgroundcolor"></a><span data-ttu-id="e1825-204">ScriptPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-204">ScriptPaneBackgroundColor</span></span>
  <span data-ttu-id="e1825-205">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-205">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-206">Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a fájlok háttérszínét.</span><span class="sxs-lookup"><span data-stu-id="e1825-206">The read/write property that gets or sets the background color for files.</span></span> <span data-ttu-id="e1825-207">A egy példánya a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="e1825-207">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```

# Sets the color of the script pane background to yellow.
$psISE.Options.ScriptPaneBackgroundColor = 'yellow'

```

### <a name="scriptpaneforegroundcolor"></a><span data-ttu-id="e1825-208">ScriptPaneForegroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-208">ScriptPaneForegroundColor</span></span>
  <span data-ttu-id="e1825-209">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-209">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-210">Lekérdezi vagy beállítja a rácsterület előtérszínét, parancsfájl-fájlok esetében parancssori panelbe olvasási/írási tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="e1825-210">The read/write property that gets or sets the foreground color for non-script files in the Script pane.</span></span>
<span data-ttu-id="e1825-211">A parancsfájlok előtérszínét beállításához használja a [TokenColors](#tokencolors).</span><span class="sxs-lookup"><span data-stu-id="e1825-211">To set the foreground color for script files, use the [TokenColors](#tokencolors).</span></span>

```
# Sets the foreground to color of non-script files in the script pane to green.
$psISE.Options.ScriptPaneBackgroundColor = "green"

```

### <a name="selectedscriptpanestate"></a><span data-ttu-id="e1825-212">SelectedScriptPaneState</span><span class="sxs-lookup"><span data-stu-id="e1825-212">SelectedScriptPaneState</span></span>
  <span data-ttu-id="e1825-213">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-213">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-214">Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a parancsfájl ablak pozícióját az képernyőjén.</span><span class="sxs-lookup"><span data-stu-id="e1825-214">The read/write property that gets or sets the position of the Script pane on the display.</span></span> <span data-ttu-id="e1825-215">A karakterlánc lehet "Maximized", "Top" vagy "Jobbra".</span><span class="sxs-lookup"><span data-stu-id="e1825-215">The string can be either "Maximized", "Top", or "Right".</span></span>

```
# Moves the Script Pane to the top.
$psISE.Options.SelectedScriptPaneState = "Top"
# Moves the Script Pane to the right.
$psISE.Options.SelectedScriptPaneState = "Right"
# Maximizes the Script Pane
$psISE.Options.SelectedScriptPaneState = "Maximized"

```

### <a name="showdefaultsnippets"></a><span data-ttu-id="e1825-216">ShowDefaultSnippets</span><span class="sxs-lookup"><span data-stu-id="e1825-216">ShowDefaultSnippets</span></span>
  <span data-ttu-id="e1825-217">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-217">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-218">Megadja, hogy a **CTRL + J** kódtöredékek listáját tartalmazza az alapszintű, amelyek része a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1825-218">Specifies whether the **CTRL+J** list of snippets includes the starter set that is included in Windows PowerShell.</span></span> <span data-ttu-id="e1825-219">Ha beállítása **$false**, csak a felhasználó által definiált kódtöredékek megjelennek a **CTRL + J** listája.</span><span class="sxs-lookup"><span data-stu-id="e1825-219">When set to **$false**, only user-defined snippets appear in the **CTRL+J** list.</span></span> <span data-ttu-id="e1825-220">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="e1825-220">The default value is **$true**.</span></span>

```
# Hide the default snippets from the CTRL+J list.
$psISe.Options.ShowDefaultSnippets = $false
```

### <a name="showintellisenseinconsolepane"></a><span data-ttu-id="e1825-221">ShowIntellisenseInConsolePane</span><span class="sxs-lookup"><span data-stu-id="e1825-221">ShowIntellisenseInConsolePane</span></span>
  <span data-ttu-id="e1825-222">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-222">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-223">Meghatározza, hogy az IntelliSense kínál szintaxis paraméter és érték javaslatok a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="e1825-223">Specifies whether IntelliSense offers syntax, parameter, and value suggestions in the Console pane.</span></span> <span data-ttu-id="e1825-224">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="e1825-224">The default value is **$true**.</span></span>

```
# Turn off IntelliSense in the console pane.
$psISe.Options.ShowIntellisenseInConsolePane = $false
```

### <a name="showintellisenseinscriptpane"></a><span data-ttu-id="e1825-225">ShowIntellisenseInScriptPane</span><span class="sxs-lookup"><span data-stu-id="e1825-225">ShowIntellisenseInScriptPane</span></span>
  <span data-ttu-id="e1825-226">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-226">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-227">Határozza meg, hogy az IntelliSense kínál szintaxis paraméter és érték javaslatok panelbe.</span><span class="sxs-lookup"><span data-stu-id="e1825-227">Specifies whether IntelliSense offers syntax, parameter, and value suggestions in the Script pane.</span></span> <span data-ttu-id="e1825-228">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="e1825-228">The default value is **$true**.</span></span>

```
# Turn off IntelliSense in the Script pane.
$psISe.Options.ShowIntellisenseInScriptPane = $false
```

### <a name="showlinenumbers"></a><span data-ttu-id="e1825-229">ShowLineNumbers</span><span class="sxs-lookup"><span data-stu-id="e1825-229">ShowLineNumbers</span></span>
  <span data-ttu-id="e1825-230">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-230">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-231">Meghatározza, hogy a parancsfájl ablaktáblán megjelennek-e a bal margón sorok számát.</span><span class="sxs-lookup"><span data-stu-id="e1825-231">Specifies whether the Script pane displays line numbers in the left margin.</span></span> <span data-ttu-id="e1825-232">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="e1825-232">The default value is **$true**.</span></span>

```
# Turn off line numbers in the Script pane.
$psISe.Options.ShowLineNumbers = $false
```

### <a name="showoutlining"></a><span data-ttu-id="e1825-233">ShowOutlining</span><span class="sxs-lookup"><span data-stu-id="e1825-233">ShowOutlining</span></span>
  <span data-ttu-id="e1825-234">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-234">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-235">Meghatározza, hogy a parancsfájl ablaktáblán megjelennek-e a bal margón bővíthető és összecsukható zárójeleket melletti kód szakaszait.</span><span class="sxs-lookup"><span data-stu-id="e1825-235">Specifies whether the Script pane displays expandable and collapsible brackets next to sections of code in the left margin.</span></span> <span data-ttu-id="e1825-236">Amikor jelennek meg, kattintson a mínusz \( - \) ikonok mellett csukja össze, vagy kattintson a plusz szövegblokk \( + \) ikonra kattintva bontsa ki a szövegblokk.</span><span class="sxs-lookup"><span data-stu-id="e1825-236">When they are displayed, you can click the minus \(-\) icons next to a block of text to collapse it or click the plus \(+\) icon to expand a block of text.</span></span> <span data-ttu-id="e1825-237">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="e1825-237">The default value is **$true**.</span></span>

```
# Turn off outlining in the Script pane.
$psISe.Options.ShowOutlining = $false
```

### <a name="showtoolbar"></a><span data-ttu-id="e1825-238">EszköztárMegjelenítése</span><span class="sxs-lookup"><span data-stu-id="e1825-238">ShowToolBar</span></span>
  <span data-ttu-id="e1825-239">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-239">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-240">Megadja, hogy az ISE eszköztár megjelenik-e a Windows PowerShell ISE ablak tetején.</span><span class="sxs-lookup"><span data-stu-id="e1825-240">Specifies whether the ISE toolbar appears at the top of the Windows PowerShell ISE window.</span></span> <span data-ttu-id="e1825-241">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="e1825-241">The default value is **$true**.</span></span>

```
# Show the toolbar.
$psISe.Options.ShowToolBar = $true
```

### <a name="showwarningbeforesavingonrun"></a><span data-ttu-id="e1825-242">ShowWarningBeforeSavingOnRun</span><span class="sxs-lookup"><span data-stu-id="e1825-242">ShowWarningBeforeSavingOnRun</span></span>
  <span data-ttu-id="e1825-243">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-243">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-244">Megadja, hogy egy figyelmeztető üzenet megjelenik-e a parancsfájl mentése automatikusan fut, mielőtt.</span><span class="sxs-lookup"><span data-stu-id="e1825-244">Specifies whether a warning message appears when a script is saved automatically before it is run.</span></span> <span data-ttu-id="e1825-245">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="e1825-245">The default value is **$true**.</span></span>

```
# Enable the warning message when an attempt
# is made to run a script without saving it first.
$psISE.Options.ShowWarningBeforeSavingOnRun=$true

```

### <a name="showwarningforduplicatefiles"></a><span data-ttu-id="e1825-246">ShowWarningForDuplicateFiles</span><span class="sxs-lookup"><span data-stu-id="e1825-246">ShowWarningForDuplicateFiles</span></span>
  <span data-ttu-id="e1825-247">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-247">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-248">Meghatározza, hogy megjelenik egy figyelmeztető üzenet ugyanazt a fájlt másik PowerShell lapok megnyitása.</span><span class="sxs-lookup"><span data-stu-id="e1825-248">Specifies whether a warning message appears when the same file is opened in different PowerShell tabs.</span></span> <span data-ttu-id="e1825-249">Ha beállítása **$true**, ugyanazt a fájlt megnyitni több lapokat jeleníti meg ezt az üzenetet: "Ez a fájl másolatát nyitva egy másik Windows PowerShell-lapon. Ez a fájl módosításait hatással lesz az összes nyitott másolatok."</span><span class="sxs-lookup"><span data-stu-id="e1825-249">If set to **$true**, to open the same file in multiple tabs displays this message: "A copy of this file is open in another Windows PowerShell tab. Changes made to this file will affect all open copies."</span></span> <span data-ttu-id="e1825-250">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="e1825-250">The default value is **$true**.</span></span>

```
# Enable the warning message when a file is
# opened in multiple PowerShell tabs.
$psISE.Options.ShowWarningForDuplicateFiles = $true

```

### <a name="tokencolors"></a><span data-ttu-id="e1825-251">TokenColors</span><span class="sxs-lookup"><span data-stu-id="e1825-251">TokenColors</span></span>
  <span data-ttu-id="e1825-252">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-252">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-253">Megadja a IntelliSense jogkivonatok színek a Windows PowerShell ISE parancsfájl ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="e1825-253">Specifies the colors of the IntelliSense tokens in the Windows PowerShell ISE Script pane.</span></span> <span data-ttu-id="e1825-254">Ez a tulajdonság egy név/érték párok tokentípusokat és a parancssori panelbe színeket tartalmazó szótárobjektum.</span><span class="sxs-lookup"><span data-stu-id="e1825-254">This property is a dictionary object that contains name/value pairs of token types and colors for the Script pane.</span></span> <span data-ttu-id="e1825-255">A konzolpanelen IntelliSense jogkivonatok színek módosításához lásd [ConsoleTokenColors](#consoletokencolors).</span><span class="sxs-lookup"><span data-stu-id="e1825-255">To change the colors of the IntelliSense tokens in the Console pane, see [ConsoleTokenColors](#consoletokencolors).</span></span> <span data-ttu-id="e1825-256">A színek visszaállítása az alapértelmezett értékeket, lásd: [RestoreDefaultTokenColors](#restoredefaulttokencolors).</span><span class="sxs-lookup"><span data-stu-id="e1825-256">To reset the colors to the default values, see [RestoreDefaultTokenColors](#restoredefaulttokencolors).</span></span> <span data-ttu-id="e1825-257">Token színek állíthat be a következőt: attribútum, parancsot, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, számot, operátor, pozíciója, StatementSeparator, karakterlánc, típusa, Ismeretlen, változó.</span><span class="sxs-lookup"><span data-stu-id="e1825-257">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span>

```
# Sets the color of commands to green.
$psISE.Options.TokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.TokenColors["Keyword"] = "magenta"

```

### <a name="useentertoselectinconsolepaneintellisense"></a><span data-ttu-id="e1825-258">UseEnterToSelectInConsolePaneIntellisense</span><span class="sxs-lookup"><span data-stu-id="e1825-258">UseEnterToSelectInConsolePaneIntellisense</span></span>
  <span data-ttu-id="e1825-259">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-259">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-260">Meghatározza, hogy használhatja az IntelliSense megadott beállítást, a konzol ablaktáblában jelölje be az Enter billentyűt.</span><span class="sxs-lookup"><span data-stu-id="e1825-260">Specifies whether you can use the Enter key to select an IntelliSense provided option in the Console pane.</span></span> <span data-ttu-id="e1825-261">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="e1825-261">The default value is **$true**.</span></span>

```
# Turn off using the ENTER key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense=$false

```

### <a name="useentertoselectinscriptpaneintellisense"></a><span data-ttu-id="e1825-262">UseEnterToSelectInScriptPaneIntellisense</span><span class="sxs-lookup"><span data-stu-id="e1825-262">UseEnterToSelectInScriptPaneIntellisense</span></span>
  <span data-ttu-id="e1825-263">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-263">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-264">Meghatározza, hogy használhatja a parancssori panelbe IntelliSense által biztosított beállítás kiválasztása az Enter billentyűt.</span><span class="sxs-lookup"><span data-stu-id="e1825-264">Specifies whether you can use the Enter key to select an IntelliSense-provided option in the Script pane.</span></span> <span data-ttu-id="e1825-265">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="e1825-265">The default value is **$true**.</span></span>

```
# Turn on using the Enter key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense=$true

```

### <a name="uselocalhelp"></a><span data-ttu-id="e1825-266">UseLocalHelp</span><span class="sxs-lookup"><span data-stu-id="e1825-266">UseLocalHelp</span></span>
  <span data-ttu-id="e1825-267">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-267">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-268">Megadja, hogy a helyileg telepített súgó vagy a TechNet Library súgó megjelenik a kurzor kulcsszó elhelyezni az F1 billentyű megnyomásakor.</span><span class="sxs-lookup"><span data-stu-id="e1825-268">Specifies whether the locally installed Help or the online TechNet Library Help appears when you press F1 with the cursor positioned in a keyword.</span></span> <span data-ttu-id="e1825-269">Ha beállítása **$true**, majd a helyileg telepített súgóból előugró ablak látható tartalom.</span><span class="sxs-lookup"><span data-stu-id="e1825-269">If set to **$true**, then a pop-up window shows content from the locally installed Help.</span></span> <span data-ttu-id="e1825-270">A súgófájlok futtatásával telepíthető a `Update-Help` parancsot.</span><span class="sxs-lookup"><span data-stu-id="e1825-270">You can install the Help files by running the `Update-Help` command.</span></span> <span data-ttu-id="e1825-271">Ha beállítása **$false**, akkor a böngésző nyitja meg a lap a TechNet könyvtárban.</span><span class="sxs-lookup"><span data-stu-id="e1825-271">If set to **$false**, then your browser opens to a page in the TechNet Library.</span></span>

```
# Sets the option for the online help to be displayed.
$psISE.Options.UseLocalHelp=$false
# Sets the option for the local Help to be displayed.
$psISE.Options.UseLocalHelp=$true

```

### <a name="verbosebackgroundcolor"></a><span data-ttu-id="e1825-272">VerboseBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-272">VerboseBackgroundColor</span></span>
  <span data-ttu-id="e1825-273">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-273">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-274">Adja meg a konzol ablaktáblában részletes megjelenő szöveg háttérszínét.</span><span class="sxs-lookup"><span data-stu-id="e1825-274">Specifies the background color for verbose text that appears in the Console pane.</span></span> <span data-ttu-id="e1825-275">Ez egy **System.Windows.Media.Color** objektum.</span><span class="sxs-lookup"><span data-stu-id="e1825-275">It is a **System.Windows.Media.Color** object.</span></span>

```
# Changes the background color for verbose text to blue.
$psISE.Options.VerboseBackgroundColor ='#0000FF'
```

### <a name="verboseforegroundcolor"></a><span data-ttu-id="e1825-276">VerboseForegroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-276">VerboseForegroundColor</span></span>
  <span data-ttu-id="e1825-277">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-277">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-278">A konzol ablaktáblában határozza meg a részletes megjelenő szöveg előterének színét.</span><span class="sxs-lookup"><span data-stu-id="e1825-278">Specifies the foreground color for verbose text that appears in the Console pane.</span></span> <span data-ttu-id="e1825-279">Ez egy **System.Windows.Media.Color** objektum.</span><span class="sxs-lookup"><span data-stu-id="e1825-279">It is a **System.Windows.Media.Color** object.</span></span>

```
# Changes the foreground color for verbose text to yellow.
$psISE.Options.VerboseForegroundColor ='yellow'
```

### <a name="warningbackgroundcolor"></a><span data-ttu-id="e1825-280">WarningBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-280">WarningBackgroundColor</span></span>
  <span data-ttu-id="e1825-281">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-281">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-282">Adja meg a konzol ablaktáblában megjelenő figyelmeztető szöveg háttérszínét.</span><span class="sxs-lookup"><span data-stu-id="e1825-282">Specifies the background color for warning text that appears in the Console pane.</span></span> <span data-ttu-id="e1825-283">Ez egy **System.Windows.Media.Color** objektum.</span><span class="sxs-lookup"><span data-stu-id="e1825-283">It is a **System.Windows.Media.Color** object.</span></span>

```
# Changes the background color for warning text to blue.
$psISE.Options.WarningBackgroundColor ='#0000FF'
```

### <a name="warningforegroundcolor"></a><span data-ttu-id="e1825-284">WarningForegroundColor</span><span class="sxs-lookup"><span data-stu-id="e1825-284">WarningForegroundColor</span></span>
  <span data-ttu-id="e1825-285">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="e1825-285">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

 <span data-ttu-id="e1825-286">Adja meg a Tesztkimenet ablaktáblán megjelenő figyelmeztető szöveg előterének színét.</span><span class="sxs-lookup"><span data-stu-id="e1825-286">Specifies the foreground color for warning text that appears in the Output pane.</span></span> <span data-ttu-id="e1825-287">Ez egy **System.Windows.Media.Color** objektum.</span><span class="sxs-lookup"><span data-stu-id="e1825-287">It is a **System.Windows.Media.Color** object.</span></span>

```
# Changes the foreground color for warning text to yellow.
$psISE.Options.WarningForegroundColor ='yellow'
```

### <a name="xmltokencolors"></a><span data-ttu-id="e1825-288">XmlTokenColors</span><span class="sxs-lookup"><span data-stu-id="e1825-288">XmlTokenColors</span></span>
  <span data-ttu-id="e1825-289">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-289">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-290">Adja meg a név/érték párok tokentípusokat és XML-tartalom a Windows PowerShell ISE megjelenített színeket tartalmazó szótárobjektum.</span><span class="sxs-lookup"><span data-stu-id="e1825-290">Specifies a dictionary object that contains name/value pairs of token types and colors for XML content that is displayed in Windows PowerShell ISE.</span></span> <span data-ttu-id="e1825-291">Token színek állíthat be a következőt: attribútum, parancsot, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, számot, operátor, pozíciója, StatementSeparator, karakterlánc, típusa, Ismeretlen, változó.</span><span class="sxs-lookup"><span data-stu-id="e1825-291">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span> <span data-ttu-id="e1825-292">Lásd még: [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).</span><span class="sxs-lookup"><span data-stu-id="e1825-292">Also see [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).</span></span>

```
# Sets the color of XML element names to green.
$psISE.Options.XmlTokenColors["ElementName"] = "green"
# Sets the color of XML comments to magenta.
$psISE.Options.XmlTokenColors["Comment"] = "magenta"

```

### <a name="zoom"></a><span data-ttu-id="e1825-293">Nagyítás</span><span class="sxs-lookup"><span data-stu-id="e1825-293">Zoom</span></span>
  <span data-ttu-id="e1825-294">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="e1825-294">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="e1825-295">Meghatározza a szöveg relatív méretét a konzol és a parancsfájl ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="e1825-295">Specifies the relative size of text in both the Console and Script panes.</span></span> <span data-ttu-id="e1825-296">Az alapértelmezett érték 100.</span><span class="sxs-lookup"><span data-stu-id="e1825-296">The default value is 100.</span></span> <span data-ttu-id="e1825-297">A kisebb értékek miatt a szöveg, a Windows PowerShell ISE kisebb megjelenését, miközben több okozhat nagyobb megjelenítendő szöveget.</span><span class="sxs-lookup"><span data-stu-id="e1825-297">Smaller values cause the text in Windows PowerShell ISE to appear smaller while larger numbers cause text to appear larger.</span></span> <span data-ttu-id="e1825-298">Az érték egész szám, amely az 20 a 400-as.</span><span class="sxs-lookup"><span data-stu-id="e1825-298">The value is an integer that ranges from 20 to 400.</span></span>

```
# Changes the text in the Windows PowerShell ISE to be double its normal size.
$psISE.Options.Zoom = 200
```

## <a name="see-also"></a><span data-ttu-id="e1825-299">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e1825-299">See Also</span></span>
- [<span data-ttu-id="e1825-300">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="e1825-300">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="e1825-301">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="e1825-301">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md)

