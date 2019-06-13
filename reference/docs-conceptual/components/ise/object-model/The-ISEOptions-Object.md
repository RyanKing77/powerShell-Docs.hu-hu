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
# <a name="the-iseoptions-object"></a><span data-ttu-id="3bf0d-103">Az ISEOptions objektum</span><span class="sxs-lookup"><span data-stu-id="3bf0d-103">The ISEOptions Object</span></span>

<span data-ttu-id="3bf0d-104">A **ISEOptions** objektum képviseli a Windows PowerShell ISE-ben különböző beállításait.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-104">The **ISEOptions** object represents various settings for Windows PowerShell ISE.</span></span> <span data-ttu-id="3bf0d-105">Egy példányát a **Microsoft.PowerShell.Host.ISE.ISEOptions** osztály.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-105">It is an instance of the **Microsoft.PowerShell.Host.ISE.ISEOptions** class.</span></span>

<span data-ttu-id="3bf0d-106">A **ISEOptions** objektum tartalmazza a következő metódusokat és tulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-106">The **ISEOptions** object provides the following methods and properties.</span></span>

## <a name="methods"></a><span data-ttu-id="3bf0d-107">Metódusok</span><span class="sxs-lookup"><span data-stu-id="3bf0d-107">Methods</span></span>

### <a name="restoredefaultconsoletokencolors"></a><span data-ttu-id="3bf0d-108">RestoreDefaultConsoleTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="3bf0d-108">RestoreDefaultConsoleTokenColors\(\)</span></span>

<span data-ttu-id="3bf0d-109">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-110">Visszaállítja a konzolablakban a token színek alapértelmezett értékeit.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-110">Restores the default values of the token colors in the Console pane.</span></span>

```powershell
# Changes the color of the commands in the Console pane to red and then restores it to its default value.
$psISE.Options.ConsoleTokenColors["Command"] = 'red'
$psISE.Options.RestoreDefaultConsoleTokenColors()
```

### <a name="restoredefaults"></a><span data-ttu-id="3bf0d-111">RestoreDefaults\(\)</span><span class="sxs-lookup"><span data-stu-id="3bf0d-111">RestoreDefaults\(\)</span></span>

<span data-ttu-id="3bf0d-112">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-112">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-113">Visszaállítja a konzol ablaktáblában összes beállítások alapértelmezett értékeit.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-113">Restores the default values of all options settings in the Console pane.</span></span> <span data-ttu-id="3bf0d-114">Adja meg a standard szintű jelölőnégyzetet, hogy az üzenet nem jelenik meg újra különböző figyelmeztető üzeneteket viselkedését is alaphelyzetbe állítja.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-114">It also resets the behavior of various warning messages that provide the standard check box to prevent the message from being shown again.</span></span>

```powershell
# Changes the background color in the Console pane and then restores it to its default value.
$psISE.Options.ConsolePaneBackgroundColor = 'orange'
$psISE.Options.RestoreDefaults()
```

### <a name="restoredefaulttokencolors"></a><span data-ttu-id="3bf0d-115">RestoreDefaultTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="3bf0d-115">RestoreDefaultTokenColors\(\)</span></span>

<span data-ttu-id="3bf0d-116">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-116">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-117">Visszaállítja az alapértelmezett értékeket, a parancsfájl panelen tokent színeit.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-117">Restores the default values of the token colors in the Script pane.</span></span>

```powershell
# Changes the color of the comments in the Script pane to red and then restores it to its default value.
$psISE.Options.TokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultTokenColors()
```

### <a name="restoredefaultxmltokencolors"></a><span data-ttu-id="3bf0d-118">RestoreDefaultXmlTokenColors\(\)</span><span class="sxs-lookup"><span data-stu-id="3bf0d-118">RestoreDefaultXmlTokenColors\(\)</span></span>

<span data-ttu-id="3bf0d-119">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-119">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-120">Visszaállítja az alapértelmezett értékeket, az XML-elemeket, amelyek jelennek meg a Windows PowerShell ISE-ben a jogkivonat színe.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-120">Restores the default values of the token colors for XML elements that are displayed in Windows PowerShell ISE.</span></span> <span data-ttu-id="3bf0d-121">További tájékoztatás [XmlTokenColors](#xmltokencolors).</span><span class="sxs-lookup"><span data-stu-id="3bf0d-121">Also see [XmlTokenColors](#xmltokencolors).</span></span>

```powershell
# Changes the color of the comments in XML data to red and then restores it to its default value.
$psISE.Options.XmlTokenColors["Comment"] = 'red'
$psISE.Options.RestoreDefaultXmlTokenColors()
```

## <a name="properties"></a><span data-ttu-id="3bf0d-122">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="3bf0d-122">Properties</span></span>

### <a name="autosaveminuteinterval"></a><span data-ttu-id="3bf0d-123">AutoSaveMinuteInterval</span><span class="sxs-lookup"><span data-stu-id="3bf0d-123">AutoSaveMinuteInterval</span></span>

<span data-ttu-id="3bf0d-124">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-125">Automatikus mentés műveletek Windows PowerShell ISE által a fájlok között eltelt percek számát adja meg.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-125">Specifies the number of minutes between automatic save operations of your files by Windows PowerShell ISE.</span></span> <span data-ttu-id="3bf0d-126">Az alapértelmezett érték 2 perc.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-126">The default value is 2 minutes.</span></span> <span data-ttu-id="3bf0d-127">Egész érték.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-127">The value is an integer.</span></span>

```powershell
# Changes the number of minutes between automatic save operations to every 3 minutes.
$psISE.Options.AutoSaveMinuteInterval = 3
```

### <a name="commandpanebackgroundcolor"></a><span data-ttu-id="3bf0d-128">CommandPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-128">CommandPaneBackgroundColor</span></span>

<span data-ttu-id="3bf0d-129">Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-129">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="3bf0d-130">A későbbi verziókhoz, lásd: [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span><span class="sxs-lookup"><span data-stu-id="3bf0d-130">For later versions, see [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span></span>

<span data-ttu-id="3bf0d-131">Meghatározza a parancs panelen háttérszíne.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-131">Specifies the background color for the Command pane.</span></span> <span data-ttu-id="3bf0d-132">Egy példányát a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-132">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the background color of the Command pane to orange.
$psISE.Options.CommandPaneBackgroundColor = 'orange'
```

### <a name="commandpaneup"></a><span data-ttu-id="3bf0d-133">CommandPaneUp</span><span class="sxs-lookup"><span data-stu-id="3bf0d-133">CommandPaneUp</span></span>

<span data-ttu-id="3bf0d-134">Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-134">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>

<span data-ttu-id="3bf0d-135">Itt adhatja meg, hogy található-e a parancs panelen fent a Tesztkimenet ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-135">Specifies whether the Command pane is located above the Output pane.</span></span>

```powershell
# Moves the Command pane to the top of the screen.
$psISE.Options.CommandPaneUp  = $true
```

### <a name="consolepanebackgroundcolor"></a><span data-ttu-id="3bf0d-136">ConsolePaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-136">ConsolePaneBackgroundColor</span></span>

<span data-ttu-id="3bf0d-137">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-137">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-138">Adja meg a konzol ablaktáblában háttérszíne.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-138">Specifies the background color for the Console pane.</span></span> <span data-ttu-id="3bf0d-139">Egy példányát a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-139">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the background color of the Console pane to red.
$psISE.Options.ConsolePaneBackgroundColor = 'red'
```

### <a name="consolepaneforegroundcolor"></a><span data-ttu-id="3bf0d-140">ConsolePaneForegroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-140">ConsolePaneForegroundColor</span></span>

<span data-ttu-id="3bf0d-141">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-141">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-142">Megadja a szöveg előterének színe a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-142">Specifies the foreground color of the text in the Console pane.</span></span>

```powershell
# Changes the foreground color of the text in the Console pane to yellow.
$psISE.Options.ConsolePaneForegroundColor  = 'yellow'
```

### <a name="consolepanetextbackgroundcolor"></a><span data-ttu-id="3bf0d-143">ConsolePaneTextBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-143">ConsolePaneTextBackgroundColor</span></span>

<span data-ttu-id="3bf0d-144">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-144">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-145">A szöveg háttérszínét adja meg a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-145">Specifies the background color of the text in the Console pane.</span></span>

```powershell
# Changes the background color of the Console pane text to pink.
$psISE.Options.ConsolePaneTextBackgroundColor = 'pink'
```

### <a name="consoletokencolors"></a><span data-ttu-id="3bf0d-146">ConsoleTokenColors</span><span class="sxs-lookup"><span data-stu-id="3bf0d-146">ConsoleTokenColors</span></span>

<span data-ttu-id="3bf0d-147">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-147">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-148">Megadja a színeket az IntelliSense jogkivonatokat a Windows PowerShell ISE-konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-148">Specifies the colors of the IntelliSense tokens in the Windows PowerShell ISE Console pane.</span></span> <span data-ttu-id="3bf0d-149">Ez a tulajdonság egy szótárobjektum, amely tartalmazza a név/érték párok tokentípusokat és a konzol ablaktáblában színe.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-149">This property is a dictionary object that contains name/value pairs of token types and colors for the Console pane.</span></span> <span data-ttu-id="3bf0d-150">A parancsfájl panelen IntelliSense jogkivonatok a színek módosításához lásd [TokenColors](#tokencolors).</span><span class="sxs-lookup"><span data-stu-id="3bf0d-150">To change the colors of the IntelliSense tokens in the Script pane, see [TokenColors](#tokencolors).</span></span> <span data-ttu-id="3bf0d-151">A színek visszaáll az alapértelmezett értékeket, lásd: [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors).</span><span class="sxs-lookup"><span data-stu-id="3bf0d-151">To reset the colors to the default values, see [RestoreDefaultConsoleTokenColors](#restoredefaultconsoletokencolors).</span></span> <span data-ttu-id="3bf0d-152">Token színek állíthat be a következőket: Attribútum parancs, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, szám, operátor, pozíciója, StatementSeparator, karakterlánc, típus, ismeretlen, változó.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-152">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span>

```powershell
# Sets the color of commands to green.
$psISE.Options.ConsoleTokenColors["Command"] = 'green'
# Sets the color of keywords to magenta.
$psISE.Options.ConsoleTokenColors["Keyword"] = 'magenta'
```

### <a name="debugbackgroundcolor"></a><span data-ttu-id="3bf0d-153">DebugBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-153">DebugBackgroundColor</span></span>

<span data-ttu-id="3bf0d-154">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-154">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-155">Megadja a háttér színét, a hibakeresési szöveg, amely akkor jelenik meg a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-155">Specifies the background color for the debug text that appears in the Console pane.</span></span> <span data-ttu-id="3bf0d-156">Egy példányát a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-156">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the background color for the debug text that appears in the Console pane to blue.
$psISE.Options.DebugBackgroundColor = '#0000FF'
```

### <a name="debugforegroundcolor"></a><span data-ttu-id="3bf0d-157">DebugForegroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-157">DebugForegroundColor</span></span>

<span data-ttu-id="3bf0d-158">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-158">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-159">Megadja az előtér színe a hibakeresési szöveg, amely megjelenik a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-159">Specifies the foreground color for the debug text that appears in the Console pane.</span></span> <span data-ttu-id="3bf0d-160">Egy példányát a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-160">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the foreground color for the debug text that appears in the Console pane to yellow.
$psISE.Options.DebugForegroundColor = 'yellow'
```

### <a name="defaultoptions"></a><span data-ttu-id="3bf0d-161">DefaultOptions</span><span class="sxs-lookup"><span data-stu-id="3bf0d-161">DefaultOptions</span></span>

<span data-ttu-id="3bf0d-162">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-162">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-163">Adja meg az alapértelmezett értékekkel használható, ha a visszaállítás módszerek használhatók a Tulajdonságok gyűjteménye.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-163">A collection of properties that specify the default values to be used when the Reset methods are used.</span></span>

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

### <a name="errorbackgroundcolor"></a><span data-ttu-id="3bf0d-164">ErrorBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-164">ErrorBackgroundColor</span></span>

<span data-ttu-id="3bf0d-165">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-165">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-166">Adja meg a konzol ablaktáblában megjelenő hibaüzenet-szöveg háttérszíne.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-166">Specifies the background color for error text that appears in the Console pane.</span></span> <span data-ttu-id="3bf0d-167">Egy példányát a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-167">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the background color for the error text that appears in the Console pane to black.
$psISE.Options.ErrorBackgroundColor = 'black'
```

### <a name="errorforegroundcolor"></a><span data-ttu-id="3bf0d-168">ErrorForegroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-168">ErrorForegroundColor</span></span>

<span data-ttu-id="3bf0d-169">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-169">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-170">Adja meg az előtér színe hiba szöveg jelenik meg a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-170">Specifies the foreground color for error text that appears in the Console pane.</span></span> <span data-ttu-id="3bf0d-171">Egy példányát a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-171">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the foreground color for the error text that appears in the console pane to green.
$psISE.Options.ErrorForegroundColor = 'green'
```

### <a name="fontname"></a><span data-ttu-id="3bf0d-172">FontName</span><span class="sxs-lookup"><span data-stu-id="3bf0d-172">FontName</span></span>

<span data-ttu-id="3bf0d-173">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-173">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-174">Megadja a betűtípus neve jelenleg használja a parancsfájl panelen és a konzol panelen is.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-174">Specifies the font name currently in use in both the Script pane and the Console pane.</span></span>

```powershell
# Changes the font used in both panes.
$psISE.Options.FontName = 'Courier New'
```

### <a name="fontsize"></a><span data-ttu-id="3bf0d-175">FontSize</span><span class="sxs-lookup"><span data-stu-id="3bf0d-175">FontSize</span></span>

<span data-ttu-id="3bf0d-176">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-176">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-177">Egy egész számot határozza meg a betűméretet.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-177">Specifies the font size as an integer.</span></span> <span data-ttu-id="3bf0d-178">A parancsfájl panelen, a parancs ablaktábla és a kimeneti ablaktábla használatban van.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-178">It is used in the Script pane, the Command pane, and the Output pane.</span></span> <span data-ttu-id="3bf0d-179">Az érvényes értékek tartománya 8 – 32.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-179">The valid range of values is 8 through 32.</span></span>

```powershell
# Changes the font size in all panes.
$psISE.Options.FontSize = 20
```

### <a name="intellisensetimeoutinseconds"></a><span data-ttu-id="3bf0d-180">IntellisenseTimeoutInSeconds</span><span class="sxs-lookup"><span data-stu-id="3bf0d-180">IntellisenseTimeoutInSeconds</span></span>

<span data-ttu-id="3bf0d-181">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-181">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-182">Adja meg másodpercben, az IntelliSense használatával oldja fel az aktuálisan beírt szöveget.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-182">Specifies the number of seconds that IntelliSense uses to try to resolve the currently typed text.</span></span> <span data-ttu-id="3bf0d-183">Másodpercek számát az IntelliSense túllépi az időkorlátot, és lehetővé teszi, írja be a folytatáshoz.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-183">After this number of seconds, IntelliSense times out and enables you to continue typing.</span></span> <span data-ttu-id="3bf0d-184">Az alapértelmezett értéke 3 másodperc.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-184">The default value is 3 seconds.</span></span> <span data-ttu-id="3bf0d-185">Egész érték.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-185">The value is an integer.</span></span>

```powershell
# Changes the number of seconds for IntelliSense syntax recognition to 5.
$psISE.Options.IntellisenseTimeoutInSeconds = 5
```

### <a name="mrucount"></a><span data-ttu-id="3bf0d-186">MruCount</span><span class="sxs-lookup"><span data-stu-id="3bf0d-186">MruCount</span></span>

<span data-ttu-id="3bf0d-187">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-187">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-188">A Windows PowerShell ISE-ben nyomon követi és alján megjeleníti a legutóbb megnyitott fájlok számát adja meg a **fájl megnyitása** menü.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-188">Specifies the number of recently opened files that Windows PowerShell ISE tracks and displays at the bottom of the **File Open** menu.</span></span> <span data-ttu-id="3bf0d-189">Az alapértelmezett értéke 10.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-189">The default value is 10.</span></span> <span data-ttu-id="3bf0d-190">Egész érték.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-190">The value is an integer.</span></span>

```powershell
# Changes the number of recently used files that appear at the bottom of the File Open menu to 5.
$psISE.Options.MruCount = 5
```

### <a name="outputpanebackgroundcolor"></a><span data-ttu-id="3bf0d-191">OutputPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-191">OutputPaneBackgroundColor</span></span>

<span data-ttu-id="3bf0d-192">Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-192">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="3bf0d-193">A későbbi verziókhoz, lásd: [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span><span class="sxs-lookup"><span data-stu-id="3bf0d-193">For later versions, see [ConsolePaneBackgroundColor](#consolepanebackgroundcolor).</span></span>

<span data-ttu-id="3bf0d-194">Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a Tesztkimenet ablaktáblán maga háttérszíne.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-194">The read/write property that gets or sets the background color for the Output pane itself.</span></span> <span data-ttu-id="3bf0d-195">Egy példányát a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-195">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Changes the background color of the Output pane to gold.
$psISE.Options.OutputPaneForegroundColor = 'gold'
```

### <a name="outputpanetextforegroundcolor"></a><span data-ttu-id="3bf0d-196">OutputPaneTextForegroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-196">OutputPaneTextForegroundColor</span></span>

<span data-ttu-id="3bf0d-197">Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-197">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="3bf0d-198">A későbbi verziókhoz, lásd: [ConsolePaneForegroundColor](#consolepaneforegroundcolor).</span><span class="sxs-lookup"><span data-stu-id="3bf0d-198">For later versions, see [ConsolePaneForegroundColor](#consolepaneforegroundcolor).</span></span>

<span data-ttu-id="3bf0d-199">Az olvasási/írási tulajdonság, amely a szöveget a Tesztkimenet ablaktáblán, a Windows PowerShell ISE 2.0 előterének színe megváltozik.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-199">The read/write property that changes the foreground color of the text in the Output pane in Windows PowerShell ISE 2.0.</span></span>

```powershell
# Changes the foreground color of the text in the Output Pane to blue.
$psISE.Options.OutputPaneTextForegroundColor  = 'blue'
```

### <a name="outputpanetextbackgroundcolor"></a><span data-ttu-id="3bf0d-200">OutputPaneTextBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-200">OutputPaneTextBackgroundColor</span></span>

<span data-ttu-id="3bf0d-201">Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-201">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="3bf0d-202">A későbbi verziókhoz, lásd: [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).</span><span class="sxs-lookup"><span data-stu-id="3bf0d-202">For later versions, see [ConsolePaneTextBackgroundColor](#consolepanetextbackgroundcolor).</span></span>

<span data-ttu-id="3bf0d-203">Az olvasási/írási tulajdonság, amely módosítja a Tesztkimenet ablaktáblán a szöveg háttérszíne.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-203">The read/write property that changes the background color of the text in the Output pane.</span></span>

```powershell
# Changes the background color of the Output pane text to pink.
$psISE.Options.OutputPaneTextBackgroundColor = 'pink'
```

### <a name="scriptpanebackgroundcolor"></a><span data-ttu-id="3bf0d-204">ScriptPaneBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-204">ScriptPaneBackgroundColor</span></span>

<span data-ttu-id="3bf0d-205">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-205">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-206">Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a fájlokat a háttér színe.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-206">The read/write property that gets or sets the background color for files.</span></span> <span data-ttu-id="3bf0d-207">Egy példányát a **System.Windows.Media.Color** osztály.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-207">It is an instance of the **System.Windows.Media.Color** class.</span></span>

```powershell
# Sets the color of the script pane background to yellow.
$psISE.Options.ScriptPaneBackgroundColor = 'yellow'
```

### <a name="scriptpaneforegroundcolor"></a><span data-ttu-id="3bf0d-208">ScriptPaneForegroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-208">ScriptPaneForegroundColor</span></span>

<span data-ttu-id="3bf0d-209">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-209">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-210">Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a előtérszíne parancsfájl-fájlok esetében a parancsfájl panelen.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-210">The read/write property that gets or sets the foreground color for non-script files in the Script pane.</span></span>
<span data-ttu-id="3bf0d-211">A parancsfájlokban előtérszíne beállításához használja a [TokenColors](#tokencolors).</span><span class="sxs-lookup"><span data-stu-id="3bf0d-211">To set the foreground color for script files, use the [TokenColors](#tokencolors).</span></span>

```powershell
# Sets the foreground to color of non-script files in the script pane to green.
$psISE.Options.ScriptPaneBackgroundColor = 'green'
```

### <a name="selectedscriptpanestate"></a><span data-ttu-id="3bf0d-212">SelectedScriptPaneState</span><span class="sxs-lookup"><span data-stu-id="3bf0d-212">SelectedScriptPaneState</span></span>

<span data-ttu-id="3bf0d-213">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-213">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-214">Az olvasási/írási tulajdonság, amely lekérdezi vagy beállítja a parancsfájl panelen pozícióját megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-214">The read/write property that gets or sets the position of the Script pane on the display.</span></span> <span data-ttu-id="3bf0d-215">A karakterlánc lehet "Maximized", "Top" vagy 'Jobbról'.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-215">The string can be either 'Maximized', 'Top', or 'Right'.</span></span>

```powershell
# Moves the Script Pane to the top.
$psISE.Options.SelectedScriptPaneState = 'Top'
# Moves the Script Pane to the right.
$psISE.Options.SelectedScriptPaneState = 'Right'
# Maximizes the Script Pane
$psISE.Options.SelectedScriptPaneState = 'Maximized'
```

### <a name="showdefaultsnippets"></a><span data-ttu-id="3bf0d-216">ShowDefaultSnippets</span><span class="sxs-lookup"><span data-stu-id="3bf0d-216">ShowDefaultSnippets</span></span>

<span data-ttu-id="3bf0d-217">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-217">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-218">Megadja, hogy a **CTRL + J** kódrészletek listája tartalmazza az alapszintű készlet, amely része a Windows PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-218">Specifies whether the **CTRL+J** list of snippets includes the starter set that is included in Windows PowerShell.</span></span> <span data-ttu-id="3bf0d-219">Ha a beállítása **$false**, csak a felhasználói kódrészletek jelennek meg a **CTRL + J** listája.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-219">When set to **$false**, only user-defined snippets appear in the **CTRL+J** list.</span></span> <span data-ttu-id="3bf0d-220">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-220">The default value is **$true**.</span></span>

```powershell
# Hide the default snippets from the CTRL+J list.
$psISE.Options.ShowDefaultSnippets = $false
```

### <a name="showintellisenseinconsolepane"></a><span data-ttu-id="3bf0d-221">ShowIntellisenseInConsolePane</span><span class="sxs-lookup"><span data-stu-id="3bf0d-221">ShowIntellisenseInConsolePane</span></span>

<span data-ttu-id="3bf0d-222">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-222">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-223">Itt adhatja meg, hogy IntelliSense kínál szintaxis paraméter és érték javaslatok a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-223">Specifies whether IntelliSense offers syntax, parameter, and value suggestions in the Console pane.</span></span> <span data-ttu-id="3bf0d-224">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-224">The default value is **$true**.</span></span>

```powershell
# Turn off IntelliSense in the console pane.
$psISE.Options.ShowIntellisenseInConsolePane = $false
```

### <a name="showintellisenseinscriptpane"></a><span data-ttu-id="3bf0d-225">ShowIntellisenseInScriptPane</span><span class="sxs-lookup"><span data-stu-id="3bf0d-225">ShowIntellisenseInScriptPane</span></span>

<span data-ttu-id="3bf0d-226">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-226">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-227">Itt adhatja meg, hogy IntelliSense kínál szintaxis paraméter és érték javaslatok a parancsfájl panelen.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-227">Specifies whether IntelliSense offers syntax, parameter, and value suggestions in the Script pane.</span></span> <span data-ttu-id="3bf0d-228">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-228">The default value is **$true**.</span></span>

```powershell
# Turn off IntelliSense in the Script pane.
$psISE.Options.ShowIntellisenseInScriptPane = $false
```

### <a name="showlinenumbers"></a><span data-ttu-id="3bf0d-229">ShowLineNumbers</span><span class="sxs-lookup"><span data-stu-id="3bf0d-229">ShowLineNumbers</span></span>

<span data-ttu-id="3bf0d-230">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-230">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-231">Megadja, hogy e a parancsfájl panelen a bal margón sorszámok megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-231">Specifies whether the Script pane displays line numbers in the left margin.</span></span> <span data-ttu-id="3bf0d-232">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-232">The default value is **$true**.</span></span>

```powershell
# Turn off line numbers in the Script pane.
$psISE.Options.ShowLineNumbers = $false
```

### <a name="showoutlining"></a><span data-ttu-id="3bf0d-233">ShowOutlining</span><span class="sxs-lookup"><span data-stu-id="3bf0d-233">ShowOutlining</span></span>

<span data-ttu-id="3bf0d-234">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-234">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-235">Megadja, hogy e megjeleníti-e a parancsfájl panelen bővíthető és összecsukható zárójelben mellett szabályzat szakaszok bal szélén.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-235">Specifies whether the Script pane displays expandable and collapsible brackets next to sections of code in the left margin.</span></span> <span data-ttu-id="3bf0d-236">Amikor megjelennek, kattintson a mínusz \( - \) ikonok mellett kattintson a plusz kibonthatja vagy összecsukhatja, szövegblokk \( + \) ikonra kattintva bontsa ki a szöveget egy kódblokkot.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-236">When they are displayed, you can click the minus \(-\) icons next to a block of text to collapse it or click the plus \(+\) icon to expand a block of text.</span></span> <span data-ttu-id="3bf0d-237">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-237">The default value is **$true**.</span></span>

```powershell
# Turn off outlining in the Script pane.
$psISE.Options.ShowOutlining = $false
```

### <a name="showtoolbar"></a><span data-ttu-id="3bf0d-238">EszköztárMegjelenítése</span><span class="sxs-lookup"><span data-stu-id="3bf0d-238">ShowToolBar</span></span>

<span data-ttu-id="3bf0d-239">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-239">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-240">Megadja, hogy az ISE eszköztár megjelenik-e a Windows PowerShell ISE-ablak tetején.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-240">Specifies whether the ISE toolbar appears at the top of the Windows PowerShell ISE window.</span></span> <span data-ttu-id="3bf0d-241">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-241">The default value is **$true**.</span></span>

```powershell
# Show the toolbar.
$psISE.Options.ShowToolBar = $true
```

### <a name="showwarningbeforesavingonrun"></a><span data-ttu-id="3bf0d-242">ShowWarningBeforeSavingOnRun</span><span class="sxs-lookup"><span data-stu-id="3bf0d-242">ShowWarningBeforeSavingOnRun</span></span>

<span data-ttu-id="3bf0d-243">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-243">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-244">Megadja, hogy egy figyelmeztető üzenet megjelenik-e a parancsfájl mentése automatikusan azt futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-244">Specifies whether a warning message appears when a script is saved automatically before it is run.</span></span> <span data-ttu-id="3bf0d-245">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-245">The default value is **$true**.</span></span>

```powershell
# Enable the warning message when an attempt
# is made to run a script without saving it first.
$psISE.Options.ShowWarningBeforeSavingOnRun = $true
```

### <a name="showwarningforduplicatefiles"></a><span data-ttu-id="3bf0d-246">ShowWarningForDuplicateFiles</span><span class="sxs-lookup"><span data-stu-id="3bf0d-246">ShowWarningForDuplicateFiles</span></span>

<span data-ttu-id="3bf0d-247">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-247">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-248">Megadja, hogy egy figyelmeztető üzenet megjelenik-e ugyanabban a fájlban külön PowerShell-lapokon megnyitásakor.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-248">Specifies whether a warning message appears when the same file is opened in different PowerShell tabs.</span></span> <span data-ttu-id="3bf0d-249">Ha beállítása **$true**, több lapokat jeleníti meg ugyanazt a fájlt megnyitni ezt az üzenetet: "Ez a fájl másolatát nyitva egy másik Windows PowerShell-lapon. Ez a fájl módosításait hatással lesz összes megnyitott másolatokat."</span><span class="sxs-lookup"><span data-stu-id="3bf0d-249">If set to **$true**, to open the same file in multiple tabs displays this message: "A copy of this file is open in another Windows PowerShell tab. Changes made to this file will affect all open copies."</span></span> <span data-ttu-id="3bf0d-250">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-250">The default value is **$true**.</span></span>

```powershell
# Enable the warning message when a file is
# opened in multiple PowerShell tabs.
$psISE.Options.ShowWarningForDuplicateFiles = $true
```

### <a name="tokencolors"></a><span data-ttu-id="3bf0d-251">TokenColors</span><span class="sxs-lookup"><span data-stu-id="3bf0d-251">TokenColors</span></span>

<span data-ttu-id="3bf0d-252">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-252">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-253">A Windows PowerShell ISE parancsfájl panelen adja meg a színeket az IntelliSense jogkivonatokat.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-253">Specifies the colors of the IntelliSense tokens in the Windows PowerShell ISE Script pane.</span></span> <span data-ttu-id="3bf0d-254">Ez a tulajdonság egy szótárobjektum, amely tartalmazza a név/érték párok tokentípusokat és a parancsfájl panelen színe.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-254">This property is a dictionary object that contains name/value pairs of token types and colors for the Script pane.</span></span> <span data-ttu-id="3bf0d-255">A konzolablakban az IntelliSense jogkivonatokat a színek módosításához lásd [ConsoleTokenColors](#consoletokencolors).</span><span class="sxs-lookup"><span data-stu-id="3bf0d-255">To change the colors of the IntelliSense tokens in the Console pane, see [ConsoleTokenColors](#consoletokencolors).</span></span> <span data-ttu-id="3bf0d-256">A színek visszaáll az alapértelmezett értékeket, lásd: [RestoreDefaultTokenColors](#restoredefaulttokencolors).</span><span class="sxs-lookup"><span data-stu-id="3bf0d-256">To reset the colors to the default values, see [RestoreDefaultTokenColors](#restoredefaulttokencolors).</span></span> <span data-ttu-id="3bf0d-257">Token színek állíthat be a következőket: Attribútum parancs, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, szám, operátor, pozíciója, StatementSeparator, karakterlánc, típus, ismeretlen, változó.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-257">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span>

```powershell
# Sets the color of commands to green.
$psISE.Options.TokenColors["Command"] = "green"
# Sets the color of keywords to magenta.
$psISE.Options.TokenColors["Keyword"] = "magenta"
```

### <a name="useentertoselectinconsolepaneintellisense"></a><span data-ttu-id="3bf0d-258">UseEnterToSelectInConsolePaneIntellisense</span><span class="sxs-lookup"><span data-stu-id="3bf0d-258">UseEnterToSelectInConsolePaneIntellisense</span></span>

<span data-ttu-id="3bf0d-259">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-259">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-260">Itt adhatja meg, hogy használhatja az IntelliSense megadott beállítást, a konzol ablaktáblában válassza ki az Enter billentyűt.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-260">Specifies whether you can use the Enter key to select an IntelliSense provided option in the Console pane.</span></span> <span data-ttu-id="3bf0d-261">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-261">The default value is **$true**.</span></span>

```powershell
# Turn off using the ENTER key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $false
```

### <a name="useentertoselectinscriptpaneintellisense"></a><span data-ttu-id="3bf0d-262">UseEnterToSelectInScriptPaneIntellisense</span><span class="sxs-lookup"><span data-stu-id="3bf0d-262">UseEnterToSelectInScriptPaneIntellisense</span></span>

<span data-ttu-id="3bf0d-263">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-263">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-264">Itt adhatja meg, e segítségével az Enter billentyűt a parancsfájl panelen válassza ki az IntelliSense által biztosított lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-264">Specifies whether you can use the Enter key to select an IntelliSense-provided option in the Script pane.</span></span> <span data-ttu-id="3bf0d-265">Az alapértelmezett érték **$true**.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-265">The default value is **$true**.</span></span>

```powershell
# Turn on using the Enter key to select an IntelliSense provided option in the Console pane.
$psISE.Options.UseEnterToSelectInConsolePaneIntellisense = $true
```

### <a name="uselocalhelp"></a><span data-ttu-id="3bf0d-266">UseLocalHelp</span><span class="sxs-lookup"><span data-stu-id="3bf0d-266">UseLocalHelp</span></span>

<span data-ttu-id="3bf0d-267">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-267">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-268">Megadja, hogy a helyileg telepített súgó vagy az online TechNet könyvtár súgója megjelenik F1 kulcsszó elhelyezni a kurzor megnyomásakor.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-268">Specifies whether the locally installed Help or the online TechNet Library Help appears when you press F1 with the cursor positioned in a keyword.</span></span> <span data-ttu-id="3bf0d-269">Ha beállítása **$true**, majd az előugró ablakban látható tartalom a helyileg telepített súgóból.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-269">If set to **$true**, then a pop-up window shows content from the locally installed Help.</span></span> <span data-ttu-id="3bf0d-270">A súgófájlok futtatásával telepítheti a `Update-Help` parancsot.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-270">You can install the Help files by running the `Update-Help` command.</span></span> <span data-ttu-id="3bf0d-271">Ha beállítása **$false**, akkor a böngészőben megnyílik egy lap a TechNet könyvtárban.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-271">If set to **$false**, then your browser opens to a page in the TechNet Library.</span></span>

```powershell
# Sets the option for the online help to be displayed.
$psISE.Options.UseLocalHelp = $false
# Sets the option for the local Help to be displayed.
$psISE.Options.UseLocalHelp = $true
```

### <a name="verbosebackgroundcolor"></a><span data-ttu-id="3bf0d-272">VerboseBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-272">VerboseBackgroundColor</span></span>

<span data-ttu-id="3bf0d-273">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-273">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-274">Adja meg a konzol ablaktáblában megjelenő részletes szöveg háttérszíne.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-274">Specifies the background color for verbose text that appears in the Console pane.</span></span> <span data-ttu-id="3bf0d-275">Ez egy **System.Windows.Media.Color** objektum.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-275">It is a **System.Windows.Media.Color** object.</span></span>

```powershell
# Changes the background color for verbose text to blue.
$psISE.Options.VerboseBackgroundColor ='#0000FF'
```

### <a name="verboseforegroundcolor"></a><span data-ttu-id="3bf0d-276">VerboseForegroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-276">VerboseForegroundColor</span></span>

<span data-ttu-id="3bf0d-277">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-277">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-278">Adja meg a részletes megjelenő szöveg előtérszínét a konzol ablaktáblában.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-278">Specifies the foreground color for verbose text that appears in the Console pane.</span></span> <span data-ttu-id="3bf0d-279">Ez egy **System.Windows.Media.Color** objektum.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-279">It is a **System.Windows.Media.Color** object.</span></span>

```powershell
# Changes the foreground color for verbose text to yellow.
$psISE.Options.VerboseForegroundColor = 'yellow'
```

### <a name="warningbackgroundcolor"></a><span data-ttu-id="3bf0d-280">WarningBackgroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-280">WarningBackgroundColor</span></span>

<span data-ttu-id="3bf0d-281">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-281">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-282">Adja meg a konzol ablaktáblában megjelenő figyelmeztető szöveg háttérszíne.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-282">Specifies the background color for warning text that appears in the Console pane.</span></span> <span data-ttu-id="3bf0d-283">Ez egy **System.Windows.Media.Color** objektum.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-283">It is a **System.Windows.Media.Color** object.</span></span>

```powershell
# Changes the background color for warning text to blue.
$psISE.Options.WarningBackgroundColor = '#0000FF'
```

### <a name="warningforegroundcolor"></a><span data-ttu-id="3bf0d-284">WarningForegroundColor</span><span class="sxs-lookup"><span data-stu-id="3bf0d-284">WarningForegroundColor</span></span>

<span data-ttu-id="3bf0d-285">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-285">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="3bf0d-286">A megjelenő figyelmeztető szöveg előtérszínét megadja a Tesztkimenet ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-286">Specifies the foreground color for warning text that appears in the Output pane.</span></span> <span data-ttu-id="3bf0d-287">Ez egy **System.Windows.Media.Color** objektum.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-287">It is a **System.Windows.Media.Color** object.</span></span>

```powershell
# Changes the foreground color for warning text to yellow.
$psISE.Options.WarningForegroundColor = 'yellow'
```

### <a name="xmltokencolors"></a><span data-ttu-id="3bf0d-288">XmlTokenColors</span><span class="sxs-lookup"><span data-stu-id="3bf0d-288">XmlTokenColors</span></span>

<span data-ttu-id="3bf0d-289">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-289">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-290">Megadja a szótárobjektum, amely tokentípusokat és az XML-tartalom a Windows PowerShell ISE-ben megjelenő színeket név/érték párt tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-290">Specifies a dictionary object that contains name/value pairs of token types and colors for XML content that is displayed in Windows PowerShell ISE.</span></span> <span data-ttu-id="3bf0d-291">Token színek állíthat be a következőket: Attribútum parancs, CommandArgument, CommandParameter, Megjegyzés, GroupEnd, GroupStart, kulcsszó, LineContinuation, LoopLabel, tag, soremelés, szám, operátor, pozíciója, StatementSeparator, karakterlánc, típus, ismeretlen, változó.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-291">Token colors can be set for the following: Attribute, Command, CommandArgument, CommandParameter, Comment, GroupEnd, GroupStart, Keyword, LineContinuation, LoopLabel, Member, NewLine, Number, Operator, Position, StatementSeparator, String, Type, Unknown, Variable.</span></span> <span data-ttu-id="3bf0d-292">További tájékoztatás [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).</span><span class="sxs-lookup"><span data-stu-id="3bf0d-292">Also see [RestoreDefaultXmlTokenColors](#restoredefaultxmltokencolors).</span></span>

```powershell
# Sets the color of XML element names to green.
$psISE.Options.XmlTokenColors["ElementName"] = 'green'
# Sets the color of XML comments to magenta.
$psISE.Options.XmlTokenColors["Comment"] = 'magenta'
```

### <a name="zoom"></a><span data-ttu-id="3bf0d-293">Nagyítás</span><span class="sxs-lookup"><span data-stu-id="3bf0d-293">Zoom</span></span>

<span data-ttu-id="3bf0d-294">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-294">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="3bf0d-295">Megadja a szöveg relatív méretét a konzol és a parancsfájl ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-295">Specifies the relative size of text in both the Console and Script panes.</span></span> <span data-ttu-id="3bf0d-296">Az alapértelmezett érték 100.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-296">The default value is 100.</span></span> <span data-ttu-id="3bf0d-297">A kisebb értékek miatt a szöveg jelenik meg, míg a nagyobb számot miatt szöveg jelenik meg a nagyobb kisebb Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-297">Smaller values cause the text in Windows PowerShell ISE to appear smaller while larger numbers cause text to appear larger.</span></span> <span data-ttu-id="3bf0d-298">Az érték: egész szám, amely 20-ról a 400-as címtartományok.</span><span class="sxs-lookup"><span data-stu-id="3bf0d-298">The value is an integer that ranges from 20 to 400.</span></span>

```powershell
# Changes the text in the Windows PowerShell ISE to be double its normal size.
$psISE.Options.Zoom = 200
```

## <a name="see-also"></a><span data-ttu-id="3bf0d-299">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3bf0d-299">See Also</span></span>

- [<span data-ttu-id="3bf0d-300">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="3bf0d-300">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="3bf0d-301">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="3bf0d-301">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
