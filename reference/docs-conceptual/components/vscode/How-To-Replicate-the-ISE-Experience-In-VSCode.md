---
title: Hogyan replikáljon az ISE élmény, a Visual Studio Code-ban
description: Hogyan replikáljon az ISE élmény, a Visual Studio Code-ban
ms.date: 08/06/2018
ms.openlocfilehash: 0ac38985a842a0dfc6118d0ae7116d12e1579daf
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655519"
---
# <a name="how-to-replicate-the-ise-experience-in-visual-studio-code"></a><span data-ttu-id="c1538-103">Hogyan replikáljon az ISE élmény, a Visual Studio Code-ban</span><span class="sxs-lookup"><span data-stu-id="c1538-103">How to replicate the ISE experience in Visual Studio Code</span></span>

<span data-ttu-id="c1538-104">A PowerShell-bővítmény VSCode-nem keresik a PowerShell ISE-teljes funkcióparitás, amíg nincsenek funkciók a VSCode-élmény több természetes tehet felhasználói számára az ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="c1538-104">While the PowerShell extension for VSCode doesn't seek complete feature parity with the PowerShell ISE, there are features in place to make the VSCode experience more natural for users of the ISE.</span></span>

<span data-ttu-id="c1538-105">Ez a dokumentum próbál konfigurálhatja a vscode-ban, hogy a felhasználói felület az ISE képest egy kicsit több ismerős beállítások.</span><span class="sxs-lookup"><span data-stu-id="c1538-105">This document tries to list settings you can configure in VSCode to make the user experience a bit more familiar compared to the ISE.</span></span>

## <a name="key-bindings"></a><span data-ttu-id="c1538-106">Külsőkulcskötéseinek</span><span class="sxs-lookup"><span data-stu-id="c1538-106">Key bindings</span></span>

| <span data-ttu-id="c1538-107">Függvény</span><span class="sxs-lookup"><span data-stu-id="c1538-107">Function</span></span>                              | <span data-ttu-id="c1538-108">ISE-kötés</span><span class="sxs-lookup"><span data-stu-id="c1538-108">ISE Binding</span></span>                  | <span data-ttu-id="c1538-109">VSCode-kötés</span><span class="sxs-lookup"><span data-stu-id="c1538-109">VSCode Binding</span></span>                              |
| ----------------                      | -----------                  | --------------                              |
| <span data-ttu-id="c1538-110">Megszakítás és break ladicí program</span><span class="sxs-lookup"><span data-stu-id="c1538-110">Interrupt and break debugger</span></span>          | <span data-ttu-id="c1538-111"><kbd>CTRL</kbd>+<kbd>B</kbd></span><span class="sxs-lookup"><span data-stu-id="c1538-111"><kbd>Ctrl</kbd>+<kbd>B</kbd></span></span> | <span data-ttu-id="c1538-112"><kbd>F6</kbd></span><span class="sxs-lookup"><span data-stu-id="c1538-112"><kbd>F6</kbd></span></span>                               |
| <span data-ttu-id="c1538-113">Hajtsa végre az aktuális sor/kiemelt szöveg</span><span class="sxs-lookup"><span data-stu-id="c1538-113">Execute current line/highlighted text</span></span> | <span data-ttu-id="c1538-114"><kbd>F8</kbd></span><span class="sxs-lookup"><span data-stu-id="c1538-114"><kbd>F8</kbd></span></span>                | <span data-ttu-id="c1538-115"><kbd>F8</kbd></span><span class="sxs-lookup"><span data-stu-id="c1538-115"><kbd>F8</kbd></span></span>                               |
| <span data-ttu-id="c1538-116">Lista elérhető kódrészletek</span><span class="sxs-lookup"><span data-stu-id="c1538-116">List available snippets</span></span>               | <span data-ttu-id="c1538-117"><kbd>CTRL</kbd>+<kbd>J</kbd></span><span class="sxs-lookup"><span data-stu-id="c1538-117"><kbd>Ctrl</kbd>+<kbd>J</kbd></span></span> | <span data-ttu-id="c1538-118"><kbd>CTRL</kbd>+<kbd>Alt</kbd>+<kbd>J</kbd></span><span class="sxs-lookup"><span data-stu-id="c1538-118"><kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>J</kbd></span></span> |

### <a name="custom-key-bindings"></a><span data-ttu-id="c1538-119">Egyéni kulcs kötések használata</span><span class="sxs-lookup"><span data-stu-id="c1538-119">Custom Key bindings</span></span>

<span data-ttu-id="c1538-120">Is [konfigurálása saját külsőkulcskötéseinek](https://code.visualstudio.com/docs/getstarted/keybindings#_custom-keybindings-for-refactorings) a vscode-ban is.</span><span class="sxs-lookup"><span data-stu-id="c1538-120">You can [configure your own key bindings](https://code.visualstudio.com/docs/getstarted/keybindings#_custom-keybindings-for-refactorings) in VSCode as well.</span></span>

## <a name="tab-completion"></a><span data-ttu-id="c1538-121">Kiegészítés</span><span class="sxs-lookup"><span data-stu-id="c1538-121">Tab completion</span></span>

<span data-ttu-id="c1538-122">Ahhoz, hogy több ISE-szerű kiegészítés, adja hozzá ezt a beállítást:</span><span class="sxs-lookup"><span data-stu-id="c1538-122">To enable more ISE-like tab completion, add this setting:</span></span>

```json
"editor.tabCompletion": "on"
```

> [!NOTE]
> <span data-ttu-id="c1538-123">Ez a beállítás lett hozzáadva, közvetlenül a VSCode (nem a bővítmény).</span><span class="sxs-lookup"><span data-stu-id="c1538-123">This setting was added directly to VSCode (rather than in the extension).</span></span> <span data-ttu-id="c1538-124">Annak viselkedését határozza meg VSCode közvetlenül, és a bővítmény által nem módosítható.</span><span class="sxs-lookup"><span data-stu-id="c1538-124">Its behavior is determined by VSCode directly and cannot be changed by the extension.</span></span>

## <a name="no-focus-on-console-when-executing"></a><span data-ttu-id="c1538-125">A konzolon végrehajtásakor nincs fókusz</span><span class="sxs-lookup"><span data-stu-id="c1538-125">No focus on console when executing</span></span>

<span data-ttu-id="c1538-126">Tartani a fókusz a szerkesztőben a végrehajtásakor <kbd>F8</kbd>:</span><span class="sxs-lookup"><span data-stu-id="c1538-126">To keep the focus in the editor when you execute with <kbd>F8</kbd>:</span></span>

```json
"powershell.integratedConsole.focusConsoleOnExecute": false
```

<span data-ttu-id="c1538-127">Az alapértelmezett érték `true` kisegítő célokra.</span><span class="sxs-lookup"><span data-stu-id="c1538-127">The default is `true` for accessibility purposes.</span></span>

## <a name="dont-start-integrated-console-on-startup"></a><span data-ttu-id="c1538-128">Indításkor nem integrált konzol elindítása</span><span class="sxs-lookup"><span data-stu-id="c1538-128">Don't start integrated console on startup</span></span>

<span data-ttu-id="c1538-129">Állítsa le a integrált konzol az indítási, állítsa be:</span><span class="sxs-lookup"><span data-stu-id="c1538-129">To stop the integrated console on startup, set:</span></span>

```json
"powershell.integratedConsole.showOnStartup": false
```

> [!NOTE]
> <span data-ttu-id="c1538-130">A háttérben PowerShell folyamat továbbra is indul el, mivel biztosítja az intellisense, a parancsfájl elemzés, a szimbólum navigációs, stb. De a konzol nem jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="c1538-130">The background PowerShell process will still start since that provides intellisense, script analysis, symbol navigation, etc. But the console won't be shown.</span></span>

## <a name="assume-files-are-powershell-by-default"></a><span data-ttu-id="c1538-131">Tegyük fel, fájlok PowerShell alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="c1538-131">Assume files are PowerShell by default</span></span>

<span data-ttu-id="c1538-132">Ahhoz, hogy új/cím nélküli fájlokat, regisztrálja, a PowerShell alapértelmezés szerint:</span><span class="sxs-lookup"><span data-stu-id="c1538-132">To make new/untitled files, register as PowerShell by default:</span></span>

```json
"files.defaultLanguage": "powershell"
```

## <a name="color-scheme"></a><span data-ttu-id="c1538-133">Színsémát</span><span class="sxs-lookup"><span data-stu-id="c1538-133">Color scheme</span></span>

<span data-ttu-id="c1538-134">Nincsenek elérhető, hogy a keresés sokkal több, mint például az ISE-szerkesztő VSCode-számos ISE téma.</span><span class="sxs-lookup"><span data-stu-id="c1538-134">There are a number of ISE themes available for VSCode to make the editor look much more like the ISE.</span></span>

<span data-ttu-id="c1538-135">Az a [Parancskatalógus] típus `theme` beolvasni `Preferences: Color Theme` nyomja le az ENTER <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="c1538-135">In the [Command Palette] type `theme` to get `Preferences: Color Theme` and press <kbd>Enter</kbd>.</span></span>
<span data-ttu-id="c1538-136">Válassza ki a legördülő listából `PowerShell ISE`.</span><span class="sxs-lookup"><span data-stu-id="c1538-136">In the drop-down list, select `PowerShell ISE`.</span></span>

<span data-ttu-id="c1538-137">Ez a téma a-beállításokat adhatja meg:</span><span class="sxs-lookup"><span data-stu-id="c1538-137">You can set this theme in the settings with:</span></span>

```json
"workbench.colorTheme": "PowerShell ISE"
```

## <a name="powershell-command-explorer"></a><span data-ttu-id="c1538-138">PowerShell-paranccsal Explorer</span><span class="sxs-lookup"><span data-stu-id="c1538-138">PowerShell Command Explorer</span></span>

<span data-ttu-id="c1538-139">Munkájának köszönhetően [ @corbob ](https://github.com/corbob), a PowerShell-bővítmény rendelkezik a saját parancs explorer alapjait.</span><span class="sxs-lookup"><span data-stu-id="c1538-139">Thanks to the work of [@corbob](https://github.com/corbob), the PowerShell extension has the beginnings of its own command explorer.</span></span>

<span data-ttu-id="c1538-140">Az a [Parancskatalógus], adja meg `PowerShell Command Explorer` nyomja le az ENTER <kbd>Enter</kbd>.</span><span class="sxs-lookup"><span data-stu-id="c1538-140">In the [Command Palette], enter `PowerShell Command Explorer` and press <kbd>Enter</kbd>.</span></span>

## <a name="open-in-the-ise"></a><span data-ttu-id="c1538-141">Nyissa meg az ISE-ben</span><span class="sxs-lookup"><span data-stu-id="c1538-141">Open in the ISE</span></span>

<span data-ttu-id="c1538-142">Ha Ön megtörténhet, aki a ennek ellenére az ISE-ben nyisson meg egy fájlt, akkor használhatja <kbd>Shift</kbd>+<kbd>Alt</kbd>+<kbd>P</kbd>.</span><span class="sxs-lookup"><span data-stu-id="c1538-142">If you end up wanting to open a file in the ISE anyway, you can use <kbd>Shift</kbd>+<kbd>Alt</kbd>+<kbd>P</kbd>.</span></span>

## <a name="other-resources"></a><span data-ttu-id="c1538-143">Egyéb erőforrások</span><span class="sxs-lookup"><span data-stu-id="c1538-143">Other resources</span></span>

- <span data-ttu-id="c1538-144">4sysops rendelkezik [egy remek cikket](https://4sysops.com/archives/make-visual-studio-code-look-and-behave-like-powershell-ise/) VSCode lehet több, mint például az ISE-ben való konfigurálásával kapcsolatban.</span><span class="sxs-lookup"><span data-stu-id="c1538-144">4sysops has [a great article](https://4sysops.com/archives/make-visual-studio-code-look-and-behave-like-powershell-ise/) on configuring VSCode to be more like the ISE.</span></span>
- <span data-ttu-id="c1538-145">Mike F Robbins rendelkezik [nagyszerű hozzászólás](https://mikefrobbins.com/2017/08/24/how-to-install-visual-studio-code-and-configure-it-as-a-replacement-for-the-powershell-ise/) VSCode beállításával.</span><span class="sxs-lookup"><span data-stu-id="c1538-145">Mike F Robbins has [a great post](https://mikefrobbins.com/2017/08/24/how-to-install-visual-studio-code-and-configure-it-as-a-replacement-for-the-powershell-ise/) on setting up VSCode.</span></span>
- <span data-ttu-id="c1538-146">Ismerje meg a PowerShell rendelkezik [fel egy kiváló írási](https://www.learnpwsh.com/setup-vs-code-for-powershell/) PowerShell beállítása a VSCode beolvasása.</span><span class="sxs-lookup"><span data-stu-id="c1538-146">Learn PowerShell has [an excellent write up](https://www.learnpwsh.com/setup-vs-code-for-powershell/) on getting VSCode setup for PowerShell.</span></span>

## <a name="more-settings"></a><span data-ttu-id="c1538-147">További beállítások</span><span class="sxs-lookup"><span data-stu-id="c1538-147">More settings</span></span>

<span data-ttu-id="c1538-148">Ha több módon teheti a VSCode megszokottabb ISE felhasználók úgy ismeri, járul hozzá ezt a dokumentumot. Ha a keresett kompatibilitási konfigurációs van, de nem találja az engedélyezéshez, bármilyen módon [nyissa meg a probléma](https://github.com/PowerShell/vscode-powershell/issues/new/choose) és kérdezzen!</span><span class="sxs-lookup"><span data-stu-id="c1538-148">If you know of more ways to make VSCode feel more familiar for ISE users, contribute to this doc. If there's a compatibility configuration you're looking for, but you can't find any way to enable it, [open an issue](https://github.com/PowerShell/vscode-powershell/issues/new/choose) and ask away!</span></span>

<span data-ttu-id="c1538-149">Mindig örömmel fogadja el a lekéréses kérelmek és a hozzájárulások is!</span><span class="sxs-lookup"><span data-stu-id="c1538-149">We're always happy to accept PRs and contributions as well!</span></span>

## <a name="vscode-tips"></a><span data-ttu-id="c1538-150">VSCode-tippek</span><span class="sxs-lookup"><span data-stu-id="c1538-150">VSCode Tips</span></span>

### <a name="command-palette"></a><span data-ttu-id="c1538-151">Parancskatalógus</span><span class="sxs-lookup"><span data-stu-id="c1538-151">Command Palette</span></span>

<span data-ttu-id="c1538-152"><kbd>F1</kbd> vagy <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> (<kbd>Cmd</kbd> + <kbd> SHIFT</kbd>+<kbd>P</kbd> macOS rendszeren)</span><span class="sxs-lookup"><span data-stu-id="c1538-152"><kbd>F1</kbd> OR <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> (<kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> on macOS)</span></span>

<span data-ttu-id="c1538-153">Sablonszolgáltatása segítségével kényelmesen parancsok végrehajtása a vscode-ban.</span><span class="sxs-lookup"><span data-stu-id="c1538-153">A handy way of executing commands in VSCode.</span></span>
<span data-ttu-id="c1538-154">További információkért lásd: [a VSCode-docs](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette).</span><span class="sxs-lookup"><span data-stu-id="c1538-154">For more information, see [the VSCode docs](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette).</span></span>

[Parancskatalógus]: #command-palette
[Command Palette]: #command-palette
