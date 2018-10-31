---
title: PowerShell-fejlesztéshez a Visual Studio Code használatával
description: PowerShell-fejlesztéshez a Visual Studio Code használatával
ms.date: 08/06/2018
ms.openlocfilehash: 9c06ce72c39d08e75fcb7e5cf9d5f92ae5dd8ed9
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/30/2018
ms.locfileid: "50225794"
---
# <a name="using-visual-studio-code-for-powershell-development"></a><span data-ttu-id="b79b6-103">PowerShell-fejlesztéshez a Visual Studio Code használatával</span><span class="sxs-lookup"><span data-stu-id="b79b6-103">Using Visual Studio Code for PowerShell Development</span></span>

<span data-ttu-id="b79b6-104">Mellett a [PowerShell ISE-ben][ise], PowerShell egyben a Visual Studio Code jól támogatott.</span><span class="sxs-lookup"><span data-stu-id="b79b6-104">In addition to the [PowerShell ISE][ise], PowerShell is also well-supported in Visual Studio Code.</span></span>
<span data-ttu-id="b79b6-105">Ezenkívül az ISE-ben nem támogatott a PowerShell Core, a Visual Studio Code-ot minden platformon (Windows, macOS és Linux) a PowerShell Core támogatott</span><span class="sxs-lookup"><span data-stu-id="b79b6-105">Furthermore, the ISE is not supported with PowerShell Core, while Visual Studio Code is supported for PowerShell Core on all platforms (Windows, macOS, and Linux)</span></span>

<span data-ttu-id="b79b6-106">Használhatja a Visual Studio Code Windows PowerShell 5-ös verzió Windows 10-es vagy telepítésével [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) a régebbi verziójú Windows nyílt forráskódú (pl. Windows 8.1, stb.).</span><span class="sxs-lookup"><span data-stu-id="b79b6-106">You can use Visual Studio Code on Windows with PowerShell version 5 by using Windows 10 or by installing [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) for down-level Windows OSs (e.g. Windows 8.1, etc.).</span></span>

<span data-ttu-id="b79b6-107">Mielőtt hozzákezdene, ellenőrizze, hogy PowerShell létezik a rendszerben.</span><span class="sxs-lookup"><span data-stu-id="b79b6-107">Before starting it, please make sure PowerShell exists on your system.</span></span>
<span data-ttu-id="b79b6-108">Számítási feladatok Windows, macOS és Linux rendszereken lásd:</span><span class="sxs-lookup"><span data-stu-id="b79b6-108">For modern workloads on Windows, macOS, and Linux, see:</span></span>

- <span data-ttu-id="b79b6-109">[A PowerShell Core telepítése Linux rendszeren][install-pscore-linux]</span><span class="sxs-lookup"><span data-stu-id="b79b6-109">[Installing PowerShell Core on Linux][install-pscore-linux]</span></span>
- <span data-ttu-id="b79b6-110">[A PowerShell Core telepítése macOS rendszeren][install-pscore-macos]</span><span class="sxs-lookup"><span data-stu-id="b79b6-110">[Installing PowerShell Core on macOS][install-pscore-macos]</span></span>
- <span data-ttu-id="b79b6-111">[Windows PowerShell Core telepítése][install-pscore-windows]</span><span class="sxs-lookup"><span data-stu-id="b79b6-111">[Installing PowerShell Core on Windows][install-pscore-windows]</span></span>

<span data-ttu-id="b79b6-112">Windows PowerShell hagyományos számítási feladatok esetén tekintse meg a [Windows PowerShell telepítése][install-winps].</span><span class="sxs-lookup"><span data-stu-id="b79b6-112">For traditional Windows PowerShell workloads, see [Installing Windows PowerShell][install-winps].</span></span>

## <a name="editing-with-visual-studio-code"></a><span data-ttu-id="b79b6-113">A Visual Studio Code-dal szerkesztése</span><span class="sxs-lookup"><span data-stu-id="b79b6-113">Editing with Visual Studio Code</span></span>

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[<span data-ttu-id="b79b6-114">1. A Visual Studio Code telepítése</span><span class="sxs-lookup"><span data-stu-id="b79b6-114">1. Installing Visual Studio Code</span></span>](https://code.visualstudio.com/Docs/setup/setup-overview)

- <span data-ttu-id="b79b6-115">**Linux**: kövesse a telepítési utasításokat a [Linux rendszeren futó VS Code](https://code.visualstudio.com/docs/setup/linux) lap</span><span class="sxs-lookup"><span data-stu-id="b79b6-115">**Linux**: follow the installation instructions on the [Running VS Code on Linux](https://code.visualstudio.com/docs/setup/linux) page</span></span>

- <span data-ttu-id="b79b6-116">**macOS**: kövesse a telepítési utasításokat a [macOS rendszeren futó VS Code](https://code.visualstudio.com/docs/setup/mac) lap</span><span class="sxs-lookup"><span data-stu-id="b79b6-116">**macOS**: follow the installation instructions on the [Running VS Code on macOS](https://code.visualstudio.com/docs/setup/mac) page</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b79b6-117">MacOS-gépeken telepítenie kell a PowerShell-bővítmény OpenSSL megfelelő működéséhez.</span><span class="sxs-lookup"><span data-stu-id="b79b6-117">On macOS, you must install OpenSSL for the PowerShell extension to work correctly.</span></span>
  > <span data-ttu-id="b79b6-118">Ennek legegyszerűbb módja az, hogy telepítése [Homebrew](http://brew.sh/) , majd futtassa `brew install openssl`.</span><span class="sxs-lookup"><span data-stu-id="b79b6-118">The easiest way to accomplish this is to install [Homebrew](http://brew.sh/) and then run `brew install openssl`.</span></span>
  > <span data-ttu-id="b79b6-119">A VS Code most már betöltheti a PowerShell-bővítmény sikeresen megtörtént.</span><span class="sxs-lookup"><span data-stu-id="b79b6-119">VS Code can now load the PowerShell extension successfully.</span></span>

- <span data-ttu-id="b79b6-120">**Windows**: kövesse a telepítési utasításokat a [VS Code fut a Windows](https://code.visualstudio.com/docs/setup/windows) lap</span><span class="sxs-lookup"><span data-stu-id="b79b6-120">**Windows**: follow the installation instructions on the [Running VS Code on Windows](https://code.visualstudio.com/docs/setup/windows) page</span></span>

### <a name="2-installing-powershell-extension"></a><span data-ttu-id="b79b6-121">2. PowerShell-bővítmény telepítése</span><span class="sxs-lookup"><span data-stu-id="b79b6-121">2. Installing PowerShell Extension</span></span>

- <span data-ttu-id="b79b6-122">Indítsa el a Visual Studio Code az alkalmazás által:</span><span class="sxs-lookup"><span data-stu-id="b79b6-122">Launch the Visual Studio Code app by:</span></span>
  - <span data-ttu-id="b79b6-123">**Windows**: beírni `code` a PowerShell-munkamenetben</span><span class="sxs-lookup"><span data-stu-id="b79b6-123">**Windows**: typing `code` in your PowerShell session</span></span>
  - <span data-ttu-id="b79b6-124">**Linux**: beírni `code` a terminálban</span><span class="sxs-lookup"><span data-stu-id="b79b6-124">**Linux**: typing `code` in your terminal</span></span>
  - <span data-ttu-id="b79b6-125">**macOS**: beírni `code` a terminálban</span><span class="sxs-lookup"><span data-stu-id="b79b6-125">**macOS**: typing `code` in your terminal</span></span>

- <span data-ttu-id="b79b6-126">Indítsa el a **jelenítse meg a Gyorsmegnyitási** lenyomásával **Ctrl + P** (**Cmd + P** Mac gépen).</span><span class="sxs-lookup"><span data-stu-id="b79b6-126">Launch **Quick Open** by pressing **Ctrl+P** (**Cmd+P** on Mac).</span></span>
- <span data-ttu-id="b79b6-127">Írja be a Megnyitás gyors `ext install powershell` kattintok **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b79b6-127">In Quick Open, type `ext install powershell` and hit **Enter**.</span></span>
- <span data-ttu-id="b79b6-128">A **bővítmények** nézet nyílik az oldalsó sáv.</span><span class="sxs-lookup"><span data-stu-id="b79b6-128">The **Extensions** view opens on the Side Bar.</span></span> <span data-ttu-id="b79b6-129">Válassza ki a PowerShell-bővítmény a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b79b6-129">Select the PowerShell extension from Microsoft.</span></span>
  <span data-ttu-id="b79b6-130">Megjelennie alábbi módon:</span><span class="sxs-lookup"><span data-stu-id="b79b6-130">You should see something like below:</span></span>

  ![VSCode](../../images/vscode.png)

- <span data-ttu-id="b79b6-132">Kattintson a **telepítése** a PowerShell-bővítmény a Microsoft gombjára.</span><span class="sxs-lookup"><span data-stu-id="b79b6-132">Click the **Install** button on the PowerShell extension from Microsoft.</span></span>
- <span data-ttu-id="b79b6-133">A telepítést követően megjelenik a **telepítése** gomb kerül, **Újrabetöltés**.</span><span class="sxs-lookup"><span data-stu-id="b79b6-133">After the install, you see the **Install** button turns to **Reload**.</span></span>
  <span data-ttu-id="b79b6-134">Kattintson a **Újrabetöltés**.</span><span class="sxs-lookup"><span data-stu-id="b79b6-134">Click on **Reload**.</span></span>
- <span data-ttu-id="b79b6-135">Miután a Visual Studio Code újbóli betöltése rendelkezik, készen áll szerkesztésre.</span><span class="sxs-lookup"><span data-stu-id="b79b6-135">After Visual Studio Code has reload, you are ready for editing.</span></span>

<span data-ttu-id="b79b6-136">Például hozzon létre egy új fájlt, kattintson a **fájl -> új**.</span><span class="sxs-lookup"><span data-stu-id="b79b6-136">For example, to create a new file, click **File->New**.</span></span>
<span data-ttu-id="b79b6-137">A mentéshez kattintson **File -> Mentés** adja meg a fájl nevét, most tegyük fel, és `HelloWorld.ps1`.</span><span class="sxs-lookup"><span data-stu-id="b79b6-137">To save it, click **File->Save** and then provide a file name, let's say `HelloWorld.ps1`.</span></span>
<span data-ttu-id="b79b6-138">Zárja be a fájlt, kattintson a "x", a fájl neve mellett.</span><span class="sxs-lookup"><span data-stu-id="b79b6-138">To close the file, click on "x" next to the file name.</span></span>
<span data-ttu-id="b79b6-139">Lépjen ki a Visual Studio Code-ban való **File -> kilépési**.</span><span class="sxs-lookup"><span data-stu-id="b79b6-139">To exit Visual Studio Code, **File->Exit**.</span></span>

#### <a name="using-a-specific-installed-version-of-powershell"></a><span data-ttu-id="b79b6-140">Egy adott PowerShell telepített verziójának használatával</span><span class="sxs-lookup"><span data-stu-id="b79b6-140">Using a specific installed version of PowerShell</span></span>

<span data-ttu-id="b79b6-141">Ha szeretne egy adott telepítési PowerShell használata a Visual Studio Code, kell új változó hozzáadása a felhasználói beállításokat fájlt.</span><span class="sxs-lookup"><span data-stu-id="b79b6-141">If you wish to use a specific installation of PowerShell with Visual Studio Code, you need to add a new variable to your user settings file.</span></span>

1. <span data-ttu-id="b79b6-142">Kattintson a **fájl -> Beállítások -> Beállítások**</span><span class="sxs-lookup"><span data-stu-id="b79b6-142">Click **File -> Preferences -> Settings**</span></span>
1. <span data-ttu-id="b79b6-143">Két Jelentésszerkesztő paneljei jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="b79b6-143">Two editor panes appear.</span></span>
   <span data-ttu-id="b79b6-144">A jobb szélső ablaktáblán (`settings.json`), helyezze be az alábbi beállítást az operációs rendszer, a két kapcsos zárójelek között megfelelő (`{` és `}`), és cserélje le **\<verzió\>** a PowerShell telepített verziója:</span><span class="sxs-lookup"><span data-stu-id="b79b6-144">In the right-most pane (`settings.json`), insert the setting below appropriate for your OS somewhere between the two curly brackets (`{` and `}`) and replace **\<version\>** with the installed PowerShell version:</span></span>

   ```json
    // On Windows:
    "powershell.powerShellExePath": "c:/Program Files/PowerShell/<version>/pwsh.exe"

    // On Linux:
    "powershell.powerShellExePath": "/opt/microsoft/powershell/<version>/pwsh"

    // On macOS:
    "powershell.powerShellExePath": "/usr/local/microsoft/powershell/<version>/pwsh"
   ```

1. <span data-ttu-id="b79b6-145">Cserélje le a beállítás a kívánt PowerShell végrehajtható fájl elérési útja</span><span class="sxs-lookup"><span data-stu-id="b79b6-145">Replace the setting with the path to the desired PowerShell executable</span></span>
1. <span data-ttu-id="b79b6-146">Mentse a beállításokat fájlt, és indítsa újra a Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b79b6-146">Save the settings file and restart Visual Studio Code</span></span>

#### <a name="configuration-settings-for-visual-studio-code"></a><span data-ttu-id="b79b6-147">A Visual Studio Code-konfigurációs beállítások</span><span class="sxs-lookup"><span data-stu-id="b79b6-147">Configuration settings for Visual Studio Code</span></span>

<span data-ttu-id="b79b6-148">Az előző bekezdésben leírt lépések végrehajtásával adja hozzá a konfigurációs beállítások `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="b79b6-148">By using the steps in the previous paragraph you can add configuration settings in `settings.json`.</span></span>

<span data-ttu-id="b79b6-149">Azt javasoljuk, hogy a Visual Studio Code a következő beállításokat:</span><span class="sxs-lookup"><span data-stu-id="b79b6-149">We recommend the following configuration settings for Visual Studio Code:</span></span>

```json
{
    "csharp.suppressDotnetRestoreNotification": true,
    "editor.renderWhitespace": "all",
    "editor.renderControlCharacters": true,
    "omnisharp.projectLoadTimeout": 120,
    "files.trimTrailingWhitespace": true
}
```

## <a name="debugging-with-visual-studio-code"></a><span data-ttu-id="b79b6-150">Hibakeresés a Visual Studio Code-dal</span><span class="sxs-lookup"><span data-stu-id="b79b6-150">Debugging with Visual Studio Code</span></span>

### <a name="no-workspace-debugging"></a><span data-ttu-id="b79b6-151">Nem-munkaterület-hibakeresés</span><span class="sxs-lookup"><span data-stu-id="b79b6-151">No-workspace debugging</span></span>

<span data-ttu-id="b79b6-152">1.9-es verziója a Visual Studio Code-tól a PowerShell-parancsfájlok hibakeresése is a PowerShell-parancsfájlt tartalmazó mappa megnyitása nélkül.</span><span class="sxs-lookup"><span data-stu-id="b79b6-152">As of Visual Studio Code version 1.9 you can debug PowerShell scripts without having to open the folder containing the PowerShell script.</span></span>
<span data-ttu-id="b79b6-153">Nyissa meg a PowerShell-parancsfájl tárolásához a **File -> fájl megnyitása...** , állítson be egy töréspontot sorban (F9 lenyomás), és nyomja le az F5 billentyűt a hibakeresés elindításához.</span><span class="sxs-lookup"><span data-stu-id="b79b6-153">Simply open the PowerShell script file with **File->Open File...**, set a breakpoint on a line (press F9) and then press F5 to start debugging.</span></span>
<span data-ttu-id="b79b6-154">A hibakeresési műveletek panelen jelennek meg, amely lehetővé teszi, hogy a hibakeresőt, lépés, folytatása és stop-hibakeresés felosztása kell megjelennie.</span><span class="sxs-lookup"><span data-stu-id="b79b6-154">You should see the Debug actions pane appear which allows you to break into the debugger, step, resume and stop debugging.</span></span>

### <a name="workspace-debugging"></a><span data-ttu-id="b79b6-155">Munkaterület-hibakeresés</span><span class="sxs-lookup"><span data-stu-id="b79b6-155">Workspace debugging</span></span>

<span data-ttu-id="b79b6-156">Munkaterület hibakeresés hivatkozik egy mappát a Visual Studio Code használatával megnyitott kontextusában hibakeresés **mappa megnyitása...**  származó a **fájl** menü.</span><span class="sxs-lookup"><span data-stu-id="b79b6-156">Workspace debugging refers to debugging in the context of a folder that you have opened in Visual Studio Code using **Open Folder...** from the **File** menu.</span></span>
<span data-ttu-id="b79b6-157">A mappát, nyissa meg a PowerShell projektmappába és/vagy a Git-tárház gyökérkönyvtárában általában.</span><span class="sxs-lookup"><span data-stu-id="b79b6-157">The folder you open is typically your PowerShell project folder and/or the root of your Git repository.</span></span>

<span data-ttu-id="b79b6-158">Ebben a módban, még akkor is, elindíthatja a jelenleg kijelölt PowerShell-parancsprogram-hibakeresés egyszerűen az F5 billentyű lenyomásával.</span><span class="sxs-lookup"><span data-stu-id="b79b6-158">Even in this mode, you can start debugging the currently selected PowerShell script by simply pressing F5.</span></span>
<span data-ttu-id="b79b6-159">Azonban munkaterület hibakeresés lehetővé teszi több hibakeresési konfiguráció eltérő csak hibakeresés a jelenleg megnyitott fájl határozza meg.</span><span class="sxs-lookup"><span data-stu-id="b79b6-159">However, workspace debugging allows you to define multiple debug configurations other than just debugging the currently open file.</span></span>
<span data-ttu-id="b79b6-160">Például egy konfigurációkat adhat hozzá:</span><span class="sxs-lookup"><span data-stu-id="b79b6-160">For instance, you can add a configurations to:</span></span>

- <span data-ttu-id="b79b6-161">Indítsa el a hibakeresőt a Pester tesztek</span><span class="sxs-lookup"><span data-stu-id="b79b6-161">Launch Pester tests in the debugger</span></span>
- <span data-ttu-id="b79b6-162">Indítsa el egy adott fájlra a hibakeresőt a argumentumokkal</span><span class="sxs-lookup"><span data-stu-id="b79b6-162">Launch a specific file with arguments in the debugger</span></span>
- <span data-ttu-id="b79b6-163">A hibakereső egy interaktív munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="b79b6-163">Launch an interactive session in the debugger</span></span>
- <span data-ttu-id="b79b6-164">Csatolja a hibakeresőt a PowerShell gazdafolyamatokon</span><span class="sxs-lookup"><span data-stu-id="b79b6-164">Attach the debugger to a PowerShell host process</span></span>

<span data-ttu-id="b79b6-165">Kövesse az alábbi lépéseket a hibakeresési konfigurációs fájl létrehozása céljából:</span><span class="sxs-lookup"><span data-stu-id="b79b6-165">Follow these steps to create your debug configuration file:</span></span>

  1. <span data-ttu-id="b79b6-166">Nyissa meg a **Debug** lenyomásával nézet **Ctrl + Shift + D** (**Cmd + Shift + D** Mac gépen).</span><span class="sxs-lookup"><span data-stu-id="b79b6-166">Open the **Debug** view by pressing **Ctrl+Shift+D** (**Cmd+Shift+D** on Mac).</span></span>
  2. <span data-ttu-id="b79b6-167">Nyomja le az **konfigurálása** fogaskerék ikont, az eszköztáron.</span><span class="sxs-lookup"><span data-stu-id="b79b6-167">Press the **Configure** gear icon in the toolbar.</span></span>
  3. <span data-ttu-id="b79b6-168">A Visual Studio Code felszólítja, hogy **környezet kiválasztása**.</span><span class="sxs-lookup"><span data-stu-id="b79b6-168">Visual Studio Code prompts you to **Select Environment**.</span></span> <span data-ttu-id="b79b6-169">Válasszon **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b79b6-169">Choose **PowerShell**.</span></span>

  <span data-ttu-id="b79b6-170">Ha így tesz, a Visual Studio Code létrehoz egy könyvtárat és a egy ".vscode\launch.json" fájlt a munkaterület gyökérkönyvtárába.</span><span class="sxs-lookup"><span data-stu-id="b79b6-170">When you do this, Visual Studio Code creates a directory and a file ".vscode\launch.json" in the root of your workspace folder.</span></span>
  <span data-ttu-id="b79b6-171">Ez az a hibakeresési konfigurációs tárolására.</span><span class="sxs-lookup"><span data-stu-id="b79b6-171">This is where your debug configuration is stored.</span></span> <span data-ttu-id="b79b6-172">Ha a fájlok egy Git-tárházban, általában a launch.json fájl véglegesíteni kívánja.</span><span class="sxs-lookup"><span data-stu-id="b79b6-172">If your files are in a Git repository, you typically want to commit the launch.json file.</span></span>
  <span data-ttu-id="b79b6-173">A launch.json fájl tartalma:</span><span class="sxs-lookup"><span data-stu-id="b79b6-173">The contents of the launch.json file are:</span></span>

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

  <span data-ttu-id="b79b6-174">Ez a hibakeresési gyakori helyzetek jelöli.</span><span class="sxs-lookup"><span data-stu-id="b79b6-174">This represents the common debug scenarios.</span></span>
  <span data-ttu-id="b79b6-175">Azonban ez a fájl megnyitásakor a szerkesztőben megjelenik egy **konfiguráció hozzáadása...**  gombra.</span><span class="sxs-lookup"><span data-stu-id="b79b6-175">However, when you open this file in the editor, you see an **Add Configuration...** button.</span></span>
  <span data-ttu-id="b79b6-176">A gombra kattintva további PowerShell hibakeresési konfigurációk hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="b79b6-176">You can press this button to add more PowerShell debug configurations.</span></span> <span data-ttu-id="b79b6-177">Hozzáadása egy praktikus konfigurációs van **PowerShell: Indítsa el a szkript**.</span><span class="sxs-lookup"><span data-stu-id="b79b6-177">One handy configuration to add is **PowerShell: Launch Script**.</span></span>
  <span data-ttu-id="b79b6-178">Ebben a konfigurációban is megadhat egy adott fájlt, amikor, nyomja le az F5 nincs függetlenül attól, hogy melyik fájlt a szerkesztőben a jelenleg aktív indítható választható argumentumokat.</span><span class="sxs-lookup"><span data-stu-id="b79b6-178">With this configuration, you can specify a specific file with optional arguments that should be launched whenever you press F5 no matter which file is currently active in the editor.</span></span>

  <span data-ttu-id="b79b6-179">Ha a hibakeresési konfigurációs létrejött, melyik konfiguráció, ha kiválaszt egy, a hibakeresési konfigurációjából legördülő a hibakeresési munkamenet során használni kívánt kiválaszthatja a **Debug** nézet eszköztárán.</span><span class="sxs-lookup"><span data-stu-id="b79b6-179">Once the debug configuration is established, you can select which configuration you want to use during a debug session by selecting one from the debug configuration drop-down in the **Debug** view's toolbar.</span></span>

<span data-ttu-id="b79b6-180">Van néhány hasznos az első lépésekhez a PowerShell-bővítmény használata a Visual Studio Code-blogok:</span><span class="sxs-lookup"><span data-stu-id="b79b6-180">There are a few blogs that may be helpful to get you started using PowerShell extension for Visual Studio Code:</span></span>

- <span data-ttu-id="b79b6-181">[PowerShell-bővítmény][ps-extension]</span><span class="sxs-lookup"><span data-stu-id="b79b6-181">[PowerShell Extension][ps-extension]</span></span>
- <span data-ttu-id="b79b6-182">[Írási és hibakeresése a Visual Studio Code-ban a PowerShell-parancsprogramok][debug]</span><span class="sxs-lookup"><span data-stu-id="b79b6-182">[Write and debug PowerShell scripts in Visual Studio Code][debug]</span></span>
- <span data-ttu-id="b79b6-183">[Hibakeresés a Visual Studio Code-útmutató][vscode-guide]</span><span class="sxs-lookup"><span data-stu-id="b79b6-183">[Debugging Visual Studio Code Guidance][vscode-guide]</span></span>
- <span data-ttu-id="b79b6-184">[Hibakeresés a PowerShell, a Visual Studio Code-ban][ps-vscode]</span><span class="sxs-lookup"><span data-stu-id="b79b6-184">[Debugging PowerShell in Visual Studio Code][ps-vscode]</span></span>
- <span data-ttu-id="b79b6-185">[PowerShell-fejlesztés a Visual Studio Code-ban – első lépések][getting-started]</span><span class="sxs-lookup"><span data-stu-id="b79b6-185">[Get started with PowerShell development in Visual Studio Code][getting-started]</span></span>
- <span data-ttu-id="b79b6-186">[PowerShell-fejlesztéshez – 1. rész funkciók szerkesztése a Visual Studio Code][editing-part1]</span><span class="sxs-lookup"><span data-stu-id="b79b6-186">[Visual Studio Code editing features for PowerShell development – Part 1][editing-part1]</span></span>
- <span data-ttu-id="b79b6-187">[PowerShell-fejlesztéshez – 2. rész funkciók szerkesztése a Visual Studio Code][editing-part2]</span><span class="sxs-lookup"><span data-stu-id="b79b6-187">[Visual Studio Code editing features for PowerShell development – Part 2][editing-part2]</span></span>
- <span data-ttu-id="b79b6-188">[Hibakeresés a PowerShell-parancsfájlt a Visual Studio Code – 1. rész][debugging-part1]</span><span class="sxs-lookup"><span data-stu-id="b79b6-188">[Debugging PowerShell script in Visual Studio Code – Part 1][debugging-part1]</span></span>
- <span data-ttu-id="b79b6-189">[Hibakeresés a PowerShell-parancsfájlt a Visual Studio Code – 2. rész][debugging-part2]</span><span class="sxs-lookup"><span data-stu-id="b79b6-189">[Debugging PowerShell script in Visual Studio Code – Part 2][debugging-part2]</span></span>

[ise]: ../ise-guide.md
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

## <a name="powershell-extension-for-visual-studio-code"></a><span data-ttu-id="b79b6-190">PowerShell-bővítmény a Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b79b6-190">PowerShell Extension for Visual Studio Code</span></span>

<span data-ttu-id="b79b6-191">A PowerShell-bővítmény forráskód találhatók [GitHub](https://github.com/PowerShell/vscode-powershell).</span><span class="sxs-lookup"><span data-stu-id="b79b6-191">The PowerShell extension's source code can be found on [GitHub](https://github.com/PowerShell/vscode-powershell).</span></span>
