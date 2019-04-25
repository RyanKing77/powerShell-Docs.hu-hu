---
title: PowerShell-fejlesztéshez a Visual Studio Code használatával
description: PowerShell-fejlesztéshez a Visual Studio Code használatával
ms.date: 08/06/2018
ms.openlocfilehash: 1e9b9d811a39656327af2810bd6dc8aaf3fde3a4
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086736"
---
# <a name="using-visual-studio-code-for-powershell-development"></a><span data-ttu-id="bea18-103">PowerShell-fejlesztéshez a Visual Studio Code használatával</span><span class="sxs-lookup"><span data-stu-id="bea18-103">Using Visual Studio Code for PowerShell Development</span></span>

<span data-ttu-id="bea18-104">Mellett a [PowerShell ISE-ben][ise], PowerShell egyben a Visual Studio Code jól támogatott.</span><span class="sxs-lookup"><span data-stu-id="bea18-104">In addition to the [PowerShell ISE][ise], PowerShell is also well-supported in Visual Studio Code.</span></span>
<span data-ttu-id="bea18-105">Ezenkívül az ISE-ben nem támogatott a PowerShell Core, a Visual Studio Code-ot minden platformon (Windows, macOS és Linux) a PowerShell Core támogatott</span><span class="sxs-lookup"><span data-stu-id="bea18-105">Furthermore, the ISE is not supported with PowerShell Core, while Visual Studio Code is supported for PowerShell Core on all platforms (Windows, macOS, and Linux)</span></span>

<span data-ttu-id="bea18-106">Használhatja a Visual Studio Code Windows PowerShell 5-ös verzió Windows 10-es vagy telepítésével [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) a régebbi verziójú Windows nyílt forráskódú (pl. Windows 8.1, stb.).</span><span class="sxs-lookup"><span data-stu-id="bea18-106">You can use Visual Studio Code on Windows with PowerShell version 5 by using Windows 10 or by installing [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) for down-level Windows OSs (e.g. Windows 8.1, etc.).</span></span>

<span data-ttu-id="bea18-107">Mielőtt hozzákezdene, ellenőrizze, hogy PowerShell létezik a rendszerben.</span><span class="sxs-lookup"><span data-stu-id="bea18-107">Before starting it, please make sure PowerShell exists on your system.</span></span>
<span data-ttu-id="bea18-108">Számítási feladatok Windows, macOS és Linux rendszereken lásd:</span><span class="sxs-lookup"><span data-stu-id="bea18-108">For modern workloads on Windows, macOS, and Linux, see:</span></span>

- <span data-ttu-id="bea18-109">[A PowerShell Core telepítése Linux rendszeren][install-pscore-linux]</span><span class="sxs-lookup"><span data-stu-id="bea18-109">[Installing PowerShell Core on Linux][install-pscore-linux]</span></span>
- <span data-ttu-id="bea18-110">[A PowerShell Core telepítése macOS rendszeren][install-pscore-macos]</span><span class="sxs-lookup"><span data-stu-id="bea18-110">[Installing PowerShell Core on macOS][install-pscore-macos]</span></span>
- <span data-ttu-id="bea18-111">[Windows PowerShell Core telepítése][install-pscore-windows]</span><span class="sxs-lookup"><span data-stu-id="bea18-111">[Installing PowerShell Core on Windows][install-pscore-windows]</span></span>

<span data-ttu-id="bea18-112">Windows PowerShell hagyományos számítási feladatok esetén tekintse meg a [Windows PowerShell telepítése][install-winps].</span><span class="sxs-lookup"><span data-stu-id="bea18-112">For traditional Windows PowerShell workloads, see [Installing Windows PowerShell][install-winps].</span></span>

## <a name="editing-with-visual-studio-code"></a><span data-ttu-id="bea18-113">A Visual Studio Code-dal szerkesztése</span><span class="sxs-lookup"><span data-stu-id="bea18-113">Editing with Visual Studio Code</span></span>

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[<span data-ttu-id="bea18-114">1. A Visual Studio Code telepítése</span><span class="sxs-lookup"><span data-stu-id="bea18-114">1. Installing Visual Studio Code</span></span>](https://code.visualstudio.com/Docs/setup/setup-overview)

- <span data-ttu-id="bea18-115">**Linux**: kövesse a telepítési utasításokat a [Linux rendszeren futó VS Code](https://code.visualstudio.com/docs/setup/linux) lap</span><span class="sxs-lookup"><span data-stu-id="bea18-115">**Linux**: follow the installation instructions on the [Running VS Code on Linux](https://code.visualstudio.com/docs/setup/linux) page</span></span>

- <span data-ttu-id="bea18-116">**macOS**: kövesse a telepítési utasításokat a [macOS rendszeren futó VS Code](https://code.visualstudio.com/docs/setup/mac) lap</span><span class="sxs-lookup"><span data-stu-id="bea18-116">**macOS**: follow the installation instructions on the [Running VS Code on macOS](https://code.visualstudio.com/docs/setup/mac) page</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="bea18-117">MacOS-gépeken telepítenie kell a PowerShell-bővítmény OpenSSL megfelelő működéséhez.</span><span class="sxs-lookup"><span data-stu-id="bea18-117">On macOS, you must install OpenSSL for the PowerShell extension to work correctly.</span></span>
  > <span data-ttu-id="bea18-118">Ennek legegyszerűbb módja az, hogy telepítése [Homebrew](https://brew.sh/) , majd futtassa `brew install openssl`.</span><span class="sxs-lookup"><span data-stu-id="bea18-118">The easiest way to accomplish this is to install [Homebrew](https://brew.sh/) and then run `brew install openssl`.</span></span>
  > <span data-ttu-id="bea18-119">A VS Code most már betöltheti a PowerShell-bővítmény sikeresen megtörtént.</span><span class="sxs-lookup"><span data-stu-id="bea18-119">VS Code can now load the PowerShell extension successfully.</span></span>

- <span data-ttu-id="bea18-120">**Windows**: kövesse a telepítési utasításokat a [VS Code fut a Windows](https://code.visualstudio.com/docs/setup/windows) lap</span><span class="sxs-lookup"><span data-stu-id="bea18-120">**Windows**: follow the installation instructions on the [Running VS Code on Windows](https://code.visualstudio.com/docs/setup/windows) page</span></span>

### <a name="2-installing-powershell-extension"></a><span data-ttu-id="bea18-121">2. PowerShell-bővítmény telepítése</span><span class="sxs-lookup"><span data-stu-id="bea18-121">2. Installing PowerShell Extension</span></span>

- <span data-ttu-id="bea18-122">Indítsa el a Visual Studio Code az alkalmazás által:</span><span class="sxs-lookup"><span data-stu-id="bea18-122">Launch the Visual Studio Code app by:</span></span>
  - <span data-ttu-id="bea18-123">**Windows**: beírni `code` a PowerShell-munkamenetben</span><span class="sxs-lookup"><span data-stu-id="bea18-123">**Windows**: typing `code` in your PowerShell session</span></span>
  - <span data-ttu-id="bea18-124">**Linux**: beírni `code` a terminálban</span><span class="sxs-lookup"><span data-stu-id="bea18-124">**Linux**: typing `code` in your terminal</span></span>
  - <span data-ttu-id="bea18-125">**macOS**: beírni `code` a terminálban</span><span class="sxs-lookup"><span data-stu-id="bea18-125">**macOS**: typing `code` in your terminal</span></span>

- <span data-ttu-id="bea18-126">Indítsa el a **jelenítse meg a Gyorsmegnyitási** lenyomásával **Ctrl + P** (**Cmd + P** Mac gépen).</span><span class="sxs-lookup"><span data-stu-id="bea18-126">Launch **Quick Open** by pressing **Ctrl+P** (**Cmd+P** on Mac).</span></span>
- <span data-ttu-id="bea18-127">Írja be a Megnyitás gyors `ext install powershell` kattintok **Enter**.</span><span class="sxs-lookup"><span data-stu-id="bea18-127">In Quick Open, type `ext install powershell` and hit **Enter**.</span></span>
- <span data-ttu-id="bea18-128">A **bővítmények** nézet nyílik az oldalsó sáv.</span><span class="sxs-lookup"><span data-stu-id="bea18-128">The **Extensions** view opens on the Side Bar.</span></span> <span data-ttu-id="bea18-129">Válassza ki a PowerShell-bővítmény a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bea18-129">Select the PowerShell extension from Microsoft.</span></span>
  <span data-ttu-id="bea18-130">Megjelennie alábbi módon:</span><span class="sxs-lookup"><span data-stu-id="bea18-130">You should see something like below:</span></span>

  ![VSCode](../../images/vscode.png)

- <span data-ttu-id="bea18-132">Kattintson a **telepítése** a PowerShell-bővítmény a Microsoft gombjára.</span><span class="sxs-lookup"><span data-stu-id="bea18-132">Click the **Install** button on the PowerShell extension from Microsoft.</span></span>
- <span data-ttu-id="bea18-133">A telepítést követően megjelenik a **telepítése** gomb kerül, **Újrabetöltés**.</span><span class="sxs-lookup"><span data-stu-id="bea18-133">After the install, you see the **Install** button turns to **Reload**.</span></span>
  <span data-ttu-id="bea18-134">Kattintson a **Újrabetöltés**.</span><span class="sxs-lookup"><span data-stu-id="bea18-134">Click on **Reload**.</span></span>
- <span data-ttu-id="bea18-135">Miután a Visual Studio Code újbóli betöltése rendelkezik, készen áll szerkesztésre.</span><span class="sxs-lookup"><span data-stu-id="bea18-135">After Visual Studio Code has reload, you are ready for editing.</span></span>

<span data-ttu-id="bea18-136">Például hozzon létre egy új fájlt, kattintson a **fájl -> új**.</span><span class="sxs-lookup"><span data-stu-id="bea18-136">For example, to create a new file, click **File->New**.</span></span>
<span data-ttu-id="bea18-137">A mentéshez kattintson **File -> Mentés** adja meg a fájl nevét, most tegyük fel, és `HelloWorld.ps1`.</span><span class="sxs-lookup"><span data-stu-id="bea18-137">To save it, click **File->Save** and then provide a file name, let's say `HelloWorld.ps1`.</span></span>
<span data-ttu-id="bea18-138">Zárja be a fájlt, kattintson a "x", a fájl neve mellett.</span><span class="sxs-lookup"><span data-stu-id="bea18-138">To close the file, click on "x" next to the file name.</span></span>
<span data-ttu-id="bea18-139">Lépjen ki a Visual Studio Code-ban való **File -> kilépési**.</span><span class="sxs-lookup"><span data-stu-id="bea18-139">To exit Visual Studio Code, **File->Exit**.</span></span>

### <a name="installing-the-powershell-extension-on-restricted-systems"></a><span data-ttu-id="bea18-140">Korlátozott rendszereken a PowerShell-bővítmény telepítése</span><span class="sxs-lookup"><span data-stu-id="bea18-140">Installing the PowerShell Extension on Restricted Systems</span></span>

<span data-ttu-id="bea18-141">Egyes rendszerek állítsa be úgy, hogy az összes kód aláírása ellenőrizendő igényel, és megköveteli, PowerShell-szerkesztő szolgáltatások manuálisan kell jóváhagyni a rendszeren való futtatásához.</span><span class="sxs-lookup"><span data-stu-id="bea18-141">Some systems are set up in a way that requires all code signatures to be checked and thus requires PowerShell Editor Services to be manually approved to run on the system.</span></span>
<span data-ttu-id="bea18-142">Egy csoportházirend-frissítés, amely módosítja a végrehajtási házirend ennek valószínű oka, ha a PowerShell-bővítmény telepítve van, de az elérni próbált hasonló hibával:</span><span class="sxs-lookup"><span data-stu-id="bea18-142">A Group Policy update that changes execution policy is a likely cause if you have installed the PowerShell extension but are reaching an error like:</span></span>

```
Language server startup failed.
```

<span data-ttu-id="bea18-143">Manuális jóváhagyásáról PowerShell szerkesztő szolgáltatásokat, és így a PowerShell-bővítmény VSCode-nyisson meg egy PowerShell parancssort és futtassa:</span><span class="sxs-lookup"><span data-stu-id="bea18-143">To manually approve PowerShell Editor Services and thus the PowerShell extension for VSCode open a PowerShell prompt and run:</span></span>

```powershell
Import-Module $HOME\.vscode\extensions\ms-vscode.powershell*\modules\PowerShellEditorServices\PowerShellEditorServices.psd1
```

<span data-ttu-id="bea18-144">A program "Szeretné futtatni a szoftvert a nem megbízható közzétételi?"</span><span class="sxs-lookup"><span data-stu-id="bea18-144">You are prompted with "Do you want to run software from this untrusted publisher?"</span></span>
<span data-ttu-id="bea18-145">Típus `R` , futtassa a fájlt.</span><span class="sxs-lookup"><span data-stu-id="bea18-145">Type `R` to run the file.</span></span> <span data-ttu-id="bea18-146">Ezután nyissa meg a Visual Studio Code-ot, és ellenőrizze, hogy a PowerShell-bővítmény megfelelően működik-e.</span><span class="sxs-lookup"><span data-stu-id="bea18-146">Then, open Visual Studio Code and check that the PowerShell extension is functioning properly.</span></span> <span data-ttu-id="bea18-147">Ha továbbra is problémákba ütközik bevezetés, ossza meg velünk az [GitHub](https://github.com/PowerShell/vscode-powershell/issues).</span><span class="sxs-lookup"><span data-stu-id="bea18-147">If you still have issues getting started, let us know on [GitHub](https://github.com/PowerShell/vscode-powershell/issues).</span></span>

#### <a name="using-a-specific-installed-version-of-powershell"></a><span data-ttu-id="bea18-148">Egy adott PowerShell telepített verziójának használatával</span><span class="sxs-lookup"><span data-stu-id="bea18-148">Using a specific installed version of PowerShell</span></span>

<span data-ttu-id="bea18-149">Ha szeretne egy adott telepítési PowerShell használata a Visual Studio Code, kell új változó hozzáadása a felhasználói beállításokat fájlt.</span><span class="sxs-lookup"><span data-stu-id="bea18-149">If you wish to use a specific installation of PowerShell with Visual Studio Code, you need to add a new variable to your user settings file.</span></span>

1. <span data-ttu-id="bea18-150">Kattintson a **fájl -> Beállítások -> Beállítások**</span><span class="sxs-lookup"><span data-stu-id="bea18-150">Click **File -> Preferences -> Settings**</span></span>
1. <span data-ttu-id="bea18-151">Két Jelentésszerkesztő paneljei jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="bea18-151">Two editor panes appear.</span></span>
   <span data-ttu-id="bea18-152">A jobb szélső ablaktáblán (`settings.json`), helyezze be az alábbi beállítást az operációs rendszer, a két kapcsos zárójelek között megfelelő (`{` és `}`), és cserélje le **\<verzió\>** a PowerShell telepített verziója:</span><span class="sxs-lookup"><span data-stu-id="bea18-152">In the right-most pane (`settings.json`), insert the setting below appropriate for your OS somewhere between the two curly brackets (`{` and `}`) and replace **\<version\>** with the installed PowerShell version:</span></span>

   ```json
    // On Windows:
    "powershell.powerShellExePath": "c:/Program Files/PowerShell/<version>/pwsh.exe"

    // On Linux:
    "powershell.powerShellExePath": "/opt/microsoft/powershell/<version>/pwsh"

    // On macOS:
    "powershell.powerShellExePath": "/usr/local/microsoft/powershell/<version>/pwsh"
   ```

1. <span data-ttu-id="bea18-153">Cserélje le a beállítás a kívánt PowerShell végrehajtható fájl elérési útja</span><span class="sxs-lookup"><span data-stu-id="bea18-153">Replace the setting with the path to the desired PowerShell executable</span></span>
1. <span data-ttu-id="bea18-154">Mentse a beállításokat fájlt, és indítsa újra a Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bea18-154">Save the settings file and restart Visual Studio Code</span></span>

#### <a name="configuration-settings-for-visual-studio-code"></a><span data-ttu-id="bea18-155">A Visual Studio Code-konfigurációs beállítások</span><span class="sxs-lookup"><span data-stu-id="bea18-155">Configuration settings for Visual Studio Code</span></span>

<span data-ttu-id="bea18-156">Az előző bekezdésben leírt lépések végrehajtásával adja hozzá a konfigurációs beállítások `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="bea18-156">By using the steps in the previous paragraph you can add configuration settings in `settings.json`.</span></span>

<span data-ttu-id="bea18-157">Azt javasoljuk, hogy a Visual Studio Code a következő beállításokat:</span><span class="sxs-lookup"><span data-stu-id="bea18-157">We recommend the following configuration settings for Visual Studio Code:</span></span>

```json
{
    "csharp.suppressDotnetRestoreNotification": true,
    "editor.renderWhitespace": "all",
    "editor.renderControlCharacters": true,
    "omnisharp.projectLoadTimeout": 120,
    "files.trimTrailingWhitespace": true,
    "files.encoding": "utf8bom",
    "files.autoGuessEncoding": true
}
```

<span data-ttu-id="bea18-158">Ha nem szeretné ezeket a beállításokat az összes fájltípus hatással, VSCode is lehetővé teszi, hogy nyelvenkénti konfigurációkat.</span><span class="sxs-lookup"><span data-stu-id="bea18-158">If you don't want these settings to affect all files types, VSCode also allows per-language configurations.</span></span> <span data-ttu-id="bea18-159">Hozzon létre egy adott nyelvi beállítás beállításait írja a `[<language-name>]` mező.</span><span class="sxs-lookup"><span data-stu-id="bea18-159">Create a language specific setting by putting settings in a `[<language-name>]` field.</span></span> <span data-ttu-id="bea18-160">Például:</span><span class="sxs-lookup"><span data-stu-id="bea18-160">For example:</span></span>

```json
"[powershell]": {
    "files.encoding": "utf8bom",
    "files.autoGuessEncoding": true
}
```

<span data-ttu-id="bea18-161">Fájllal kapcsolatos további információk a VS Code-ban kódolási: [ismertetése fájlkódolás](understanding-file-encoding.md).</span><span class="sxs-lookup"><span data-stu-id="bea18-161">For more information about file encoding in VS Code, see [Understanding file encoding](understanding-file-encoding.md).</span></span>

## <a name="debugging-with-visual-studio-code"></a><span data-ttu-id="bea18-162">Hibakeresés a Visual Studio Code-dal</span><span class="sxs-lookup"><span data-stu-id="bea18-162">Debugging with Visual Studio Code</span></span>

### <a name="no-workspace-debugging"></a><span data-ttu-id="bea18-163">Nem-munkaterület-hibakeresés</span><span class="sxs-lookup"><span data-stu-id="bea18-163">No-workspace debugging</span></span>

<span data-ttu-id="bea18-164">1.9-es verziója a Visual Studio Code-tól a PowerShell-parancsfájlok hibakeresése is a PowerShell-parancsfájlt tartalmazó mappa megnyitása nélkül.</span><span class="sxs-lookup"><span data-stu-id="bea18-164">As of Visual Studio Code version 1.9 you can debug PowerShell scripts without having to open the folder containing the PowerShell script.</span></span> <span data-ttu-id="bea18-165">Nyissa meg a PowerShell-parancsfájl tárolásához a **File -> fájl megnyitása...** , állítson be egy töréspontot sorban (F9 lenyomás), és nyomja le az F5 billentyűt a hibakeresés elindításához.</span><span class="sxs-lookup"><span data-stu-id="bea18-165">Open the PowerShell script file with **File->Open File...**, set a breakpoint on a line (press F9) and then press F5 to start debugging.</span></span> <span data-ttu-id="bea18-166">A hibakeresési műveletek panelen jelennek meg, amely lehetővé teszi, hogy a hibakeresőt, lépés, folytatása és stop-hibakeresés felosztása kell megjelennie.</span><span class="sxs-lookup"><span data-stu-id="bea18-166">You should see the Debug actions pane appear which allows you to break into the debugger, step, resume and stop debugging.</span></span>

### <a name="workspace-debugging"></a><span data-ttu-id="bea18-167">Munkaterület-hibakeresés</span><span class="sxs-lookup"><span data-stu-id="bea18-167">Workspace debugging</span></span>

<span data-ttu-id="bea18-168">Munkaterület hibakeresés hivatkozik egy mappát a Visual Studio Code használatával megnyitott kontextusában hibakeresés **mappa megnyitása...**  származó a **fájl** menü.</span><span class="sxs-lookup"><span data-stu-id="bea18-168">Workspace debugging refers to debugging in the context of a folder that you have opened in Visual Studio Code using **Open Folder...** from the **File** menu.</span></span>
<span data-ttu-id="bea18-169">A mappát, nyissa meg a PowerShell projektmappába és/vagy a Git-tárház gyökérkönyvtárában általában.</span><span class="sxs-lookup"><span data-stu-id="bea18-169">The folder you open is typically your PowerShell project folder and/or the root of your Git repository.</span></span>

<span data-ttu-id="bea18-170">Ebben a módban, még akkor is, elindíthatja a jelenleg kijelölt PowerShell-parancsprogram-hibakeresés egyszerűen az F5 billentyű lenyomásával.</span><span class="sxs-lookup"><span data-stu-id="bea18-170">Even in this mode, you can start debugging the currently selected PowerShell script by simply pressing F5.</span></span>
<span data-ttu-id="bea18-171">Azonban munkaterület hibakeresés lehetővé teszi több hibakeresési konfiguráció eltérő csak hibakeresés a jelenleg megnyitott fájl határozza meg.</span><span class="sxs-lookup"><span data-stu-id="bea18-171">However, workspace debugging allows you to define multiple debug configurations other than just debugging the currently open file.</span></span>
<span data-ttu-id="bea18-172">Például egy konfigurációkat adhat hozzá:</span><span class="sxs-lookup"><span data-stu-id="bea18-172">For instance, you can add a configurations to:</span></span>

- <span data-ttu-id="bea18-173">Indítsa el a hibakeresőt a Pester tesztek</span><span class="sxs-lookup"><span data-stu-id="bea18-173">Launch Pester tests in the debugger</span></span>
- <span data-ttu-id="bea18-174">Indítsa el egy adott fájlra a hibakeresőt a argumentumokkal</span><span class="sxs-lookup"><span data-stu-id="bea18-174">Launch a specific file with arguments in the debugger</span></span>
- <span data-ttu-id="bea18-175">A hibakereső egy interaktív munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="bea18-175">Launch an interactive session in the debugger</span></span>
- <span data-ttu-id="bea18-176">Csatolja a hibakeresőt a PowerShell gazdafolyamatokon</span><span class="sxs-lookup"><span data-stu-id="bea18-176">Attach the debugger to a PowerShell host process</span></span>

<span data-ttu-id="bea18-177">Kövesse az alábbi lépéseket a hibakeresési konfigurációs fájl létrehozása céljából:</span><span class="sxs-lookup"><span data-stu-id="bea18-177">Follow these steps to create your debug configuration file:</span></span>

  1. <span data-ttu-id="bea18-178">Nyissa meg a **Debug** lenyomásával nézet **Ctrl + Shift + D** (**Cmd + Shift + D** Mac gépen).</span><span class="sxs-lookup"><span data-stu-id="bea18-178">Open the **Debug** view by pressing **Ctrl+Shift+D** (**Cmd+Shift+D** on Mac).</span></span>
  2. <span data-ttu-id="bea18-179">Nyomja le az **konfigurálása** fogaskerék ikont, az eszköztáron.</span><span class="sxs-lookup"><span data-stu-id="bea18-179">Press the **Configure** gear icon in the toolbar.</span></span>
  3. <span data-ttu-id="bea18-180">A Visual Studio Code felszólítja, hogy **környezet kiválasztása**.</span><span class="sxs-lookup"><span data-stu-id="bea18-180">Visual Studio Code prompts you to **Select Environment**.</span></span> <span data-ttu-id="bea18-181">Válasszon **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="bea18-181">Choose **PowerShell**.</span></span>

  <span data-ttu-id="bea18-182">Ha így tesz, a Visual Studio Code létrehoz egy könyvtárat és a egy ".vscode\launch.json" fájlt a munkaterület gyökérkönyvtárába.</span><span class="sxs-lookup"><span data-stu-id="bea18-182">When you do this, Visual Studio Code creates a directory and a file ".vscode\launch.json" in the root of your workspace folder.</span></span>
  <span data-ttu-id="bea18-183">Ez az a hibakeresési konfigurációs tárolására.</span><span class="sxs-lookup"><span data-stu-id="bea18-183">This is where your debug configuration is stored.</span></span> <span data-ttu-id="bea18-184">Ha a fájlok egy Git-tárházban, általában a launch.json fájl véglegesíteni kívánja.</span><span class="sxs-lookup"><span data-stu-id="bea18-184">If your files are in a Git repository, you typically want to commit the launch.json file.</span></span>
  <span data-ttu-id="bea18-185">A launch.json fájl tartalma:</span><span class="sxs-lookup"><span data-stu-id="bea18-185">The contents of the launch.json file are:</span></span>

  ```json
  {
    "version": "0.2.0",
    "configurations": [
        {
            "type": "PowerShell",
            "request": "launch",
            "name": "PowerShell Launch (current file)",
            "script": "${file}",
            "args": [],
            "cwd": "${file}"
        },
        {
            "type": "PowerShell",
            "request": "attach",
            "name": "PowerShell Attach to Host Process",
            "processId": "${command.PickPSHostProcess}",
            "runspaceId": 1
        },
        {
            "type": "PowerShell",
            "request": "launch",
            "name": "PowerShell Interactive Session",
            "cwd": "${workspaceRoot}"
        }
    ]
  }
  ```

  <span data-ttu-id="bea18-186">Ez a hibakeresési gyakori helyzetek jelöli.</span><span class="sxs-lookup"><span data-stu-id="bea18-186">This represents the common debug scenarios.</span></span>
  <span data-ttu-id="bea18-187">Azonban ez a fájl megnyitásakor a szerkesztőben megjelenik egy **konfiguráció hozzáadása...**  gombra.</span><span class="sxs-lookup"><span data-stu-id="bea18-187">However, when you open this file in the editor, you see an **Add Configuration...** button.</span></span>
  <span data-ttu-id="bea18-188">A gombra kattintva további PowerShell hibakeresési konfigurációk hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="bea18-188">You can press this button to add more PowerShell debug configurations.</span></span> <span data-ttu-id="bea18-189">Hozzáadása egy praktikus konfigurációs van **PowerShell: Indítsa el a szkript**.</span><span class="sxs-lookup"><span data-stu-id="bea18-189">One handy configuration to add is **PowerShell: Launch Script**.</span></span>
  <span data-ttu-id="bea18-190">Ebben a konfigurációban is megadhat egy adott fájlt, amikor, nyomja le az F5 nincs függetlenül attól, hogy melyik fájlt a szerkesztőben a jelenleg aktív indítható választható argumentumokat.</span><span class="sxs-lookup"><span data-stu-id="bea18-190">With this configuration, you can specify a specific file with optional arguments that should be launched whenever you press F5 no matter which file is currently active in the editor.</span></span>

  <span data-ttu-id="bea18-191">Ha a hibakeresési konfigurációs létrejött, melyik konfiguráció, ha kiválaszt egy, a hibakeresési konfigurációjából legördülő a hibakeresési munkamenet során használni kívánt kiválaszthatja a **Debug** nézet eszköztárán.</span><span class="sxs-lookup"><span data-stu-id="bea18-191">Once the debug configuration is established, you can select which configuration you want to use during a debug session by selecting one from the debug configuration drop-down in the **Debug** view's toolbar.</span></span>

<span data-ttu-id="bea18-192">Van néhány hasznos az első lépésekhez a PowerShell-bővítmény használata a Visual Studio Code-blogok:</span><span class="sxs-lookup"><span data-stu-id="bea18-192">There are a few blogs that may be helpful to get you started using PowerShell extension for Visual Studio Code:</span></span>

- <span data-ttu-id="bea18-193">[PowerShell-bővítmény][ps-extension]</span><span class="sxs-lookup"><span data-stu-id="bea18-193">[PowerShell Extension][ps-extension]</span></span>
- <span data-ttu-id="bea18-194">[Írási és hibakeresése a Visual Studio Code-ban a PowerShell-parancsprogramok][debug]</span><span class="sxs-lookup"><span data-stu-id="bea18-194">[Write and debug PowerShell scripts in Visual Studio Code][debug]</span></span>
- <span data-ttu-id="bea18-195">[Hibakeresés a Visual Studio Code-útmutató][vscode-guide]</span><span class="sxs-lookup"><span data-stu-id="bea18-195">[Debugging Visual Studio Code Guidance][vscode-guide]</span></span>
- <span data-ttu-id="bea18-196">[Hibakeresés a PowerShell, a Visual Studio Code-ban][ps-vscode]</span><span class="sxs-lookup"><span data-stu-id="bea18-196">[Debugging PowerShell in Visual Studio Code][ps-vscode]</span></span>
- <span data-ttu-id="bea18-197">[PowerShell-fejlesztés a Visual Studio Code-ban – első lépések][getting-started]</span><span class="sxs-lookup"><span data-stu-id="bea18-197">[Get started with PowerShell development in Visual Studio Code][getting-started]</span></span>
- <span data-ttu-id="bea18-198">[PowerShell-fejlesztéshez – 1. rész funkciók szerkesztése a Visual Studio Code][editing-part1]</span><span class="sxs-lookup"><span data-stu-id="bea18-198">[Visual Studio Code editing features for PowerShell development – Part 1][editing-part1]</span></span>
- <span data-ttu-id="bea18-199">[PowerShell-fejlesztéshez – 2. rész funkciók szerkesztése a Visual Studio Code][editing-part2]</span><span class="sxs-lookup"><span data-stu-id="bea18-199">[Visual Studio Code editing features for PowerShell development – Part 2][editing-part2]</span></span>
- <span data-ttu-id="bea18-200">[Hibakeresés a PowerShell-parancsfájlt a Visual Studio Code – 1. rész][debugging-part1]</span><span class="sxs-lookup"><span data-stu-id="bea18-200">[Debugging PowerShell script in Visual Studio Code – Part 1][debugging-part1]</span></span>
- <span data-ttu-id="bea18-201">[Hibakeresés a PowerShell-parancsfájlt a Visual Studio Code – 2. rész][debugging-part2]</span><span class="sxs-lookup"><span data-stu-id="bea18-201">[Debugging PowerShell script in Visual Studio Code – Part 2][debugging-part2]</span></span>

[ise]: ../ise/Introducing-the-Windows-PowerShell-ISE.md
[install-pscore-linux]:  ../../setup/Installing-PowerShell-Core-on-Linux.md
[install-pscore-macos]:  ../../setup/Installing-PowerShell-Core-on-macOS.md
[install-pscore-windows]: ../../setup/Installing-PowerShell-Core-on-Windows.md
[install-winps]: ../../setup/Installing-Windows-PowerShell.md
[ps-extension]: https://blogs.msdn.microsoft.com/cdndevs/2015/12/11/visual-studio-code-powershell-extension/
[debug]: https://blogs.msdn.microsoft.com/powershell/2015/11/16/announcing-powershell-language-support-for-visual-studio-code-and-more/
[vscode-guide]: https://johnpapa.net/debugging-with-visual-studio-code/
[ps-vscode]: https://github.com/PowerShell/vscode-powershell/tree/master/examples
[getting-started]: https://blogs.technet.microsoft.com/heyscriptingguy/2016/12/05/get-started-with-powershell-development-in-visual-studio-code/
[editing-part1]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/11/visual-studio-code-editing-features-for-powershell-development-part-1/
[editing-part2]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/12/visual-studio-code-editing-features-for-powershell-development-part-2/
[debugging-part1]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/06/debugging-powershell-script-in-visual-studio-code-part-1/
[debugging-part2]: https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/13/debugging-powershell-script-in-visual-studio-code-part-2/

## <a name="powershell-extension-for-visual-studio-code"></a><span data-ttu-id="bea18-202">PowerShell-bővítmény a Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bea18-202">PowerShell Extension for Visual Studio Code</span></span>

<span data-ttu-id="bea18-203">A PowerShell-bővítmény forráskód találhatók [GitHub](https://github.com/PowerShell/vscode-powershell).</span><span class="sxs-lookup"><span data-stu-id="bea18-203">The PowerShell extension's source code can be found on [GitHub](https://github.com/PowerShell/vscode-powershell).</span></span>
