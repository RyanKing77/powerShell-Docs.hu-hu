# <a name="using-visual-studio-code-for-powershell-development"></a><span data-ttu-id="cef8d-101">A Visual Studio Code fejlesztési PowerShell használatával</span><span class="sxs-lookup"><span data-stu-id="cef8d-101">Using Visual Studio Code for PowerShell Development</span></span>

<span data-ttu-id="cef8d-102">Kívül a [PowerShell ISE][ise], PowerShell egyben a Visual Studio Code jól támogatott.</span><span class="sxs-lookup"><span data-stu-id="cef8d-102">In addition to the [PowerShell ISE][ise], PowerShell is also well-supported in Visual Studio Code.</span></span>
<span data-ttu-id="cef8d-103">Ezenkívül az ISE használata nem támogatott PowerShell mag, amíg a Visual Studio Code PowerShell Core támogatott platformon (a Windows, a macOS és a Linux)</span><span class="sxs-lookup"><span data-stu-id="cef8d-103">Furthermore, the ISE is not supported with PowerShell Core, while Visual Studio Code is supported for PowerShell Core on all platforms (Windows, macOS, and Linux)</span></span>

<span data-ttu-id="cef8d-104">Használhatja a Visual Studio Code a Windows PowerShell használatával 5-ös verzióját a Windows 10 vagy telepítésével [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) a régebbi verziójú Windows OSs (Windows 8.1, stb.).</span><span class="sxs-lookup"><span data-stu-id="cef8d-104">You can use Visual Studio Code on Windows with PowerShell version 5 by using Windows 10 or by installing [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) for down-level Windows OSs (e.g. Windows 8.1, etc.).</span></span>

<span data-ttu-id="cef8d-105">Az megkezdése előtt ellenőrizze, hogy PowerShell létezik a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="cef8d-105">Before starting it, please make sure PowerShell exists on your system.</span></span>
<span data-ttu-id="cef8d-106">A Windows, a macOS és a Linux modern munkaterhelések esetén lásd:</span><span class="sxs-lookup"><span data-stu-id="cef8d-106">For modern workloads on Windows, macOS, and Linux, see:</span></span>

- <span data-ttu-id="cef8d-107">[MacOS és Linux PowerShell központi telepítése][install-pscore-linux]</span><span class="sxs-lookup"><span data-stu-id="cef8d-107">[Installing PowerShell Core on macOS and Linux][install-pscore-linux]</span></span>
- <span data-ttu-id="cef8d-108">[A Windows PowerShell központi telepítése][install-pscore-windows]</span><span class="sxs-lookup"><span data-stu-id="cef8d-108">[Installing PowerShell Core on Windows][install-pscore-windows]</span></span>

<span data-ttu-id="cef8d-109">A hagyományos Windows PowerShell-munkaterhelésekhez, lásd: [Windows PowerShell telepítése][install-winps].</span><span class="sxs-lookup"><span data-stu-id="cef8d-109">For traditional Windows PowerShell workloads, see [Installing Windows PowerShell][install-winps].</span></span>

## <a name="editing-with-visual-studio-code"></a><span data-ttu-id="cef8d-110">Szerkesztés a Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="cef8d-110">Editing with Visual Studio Code</span></span>

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[<span data-ttu-id="cef8d-111">1. A Visual Studio Code telepítése</span><span class="sxs-lookup"><span data-stu-id="cef8d-111">1. Installing Visual Studio Code</span></span>](https://code.visualstudio.com/Docs/setup/setup-overview)

- <span data-ttu-id="cef8d-112">**Linux**: a telepítési utasításokat kövesse a [VS kódot futtató Linux](https://code.visualstudio.com/docs/setup/linux) lap</span><span class="sxs-lookup"><span data-stu-id="cef8d-112">**Linux**: follow the installation instructions on the [Running VS Code on Linux](https://code.visualstudio.com/docs/setup/linux) page</span></span>

- <span data-ttu-id="cef8d-113">**macOS**: a telepítési utasításokat kövesse a [VS kódot futtató macOS](https://code.visualstudio.com/docs/setup/mac) lap</span><span class="sxs-lookup"><span data-stu-id="cef8d-113">**macOS**: follow the installation instructions on the [Running VS Code on macOS](https://code.visualstudio.com/docs/setup/mac) page</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cef8d-114">MacOS telepítenie kell a PowerShell-bővítmény OpenSSL megfelelő működéséhez.</span><span class="sxs-lookup"><span data-stu-id="cef8d-114">On macOS, you must install OpenSSL for the PowerShell extension to work correctly.</span></span>
> <span data-ttu-id="cef8d-115">Ehhez a legegyszerűbb módja a telepítendő [Homebrew](http://brew.sh/) , majd futtassa `brew install openssl`.</span><span class="sxs-lookup"><span data-stu-id="cef8d-115">The easiest way to accomplish this is to install [Homebrew](http://brew.sh/) and then run `brew install openssl`.</span></span>
> <span data-ttu-id="cef8d-116">A PowerShell-bővítmény most már tudnak sikeres betöltése.</span><span class="sxs-lookup"><span data-stu-id="cef8d-116">The PowerShell extension will now be able to load successfully.</span></span>

- <span data-ttu-id="cef8d-117">**Windows**: a telepítési utasításokat kövesse a [VS kódot futtató Windows](https://code.visualstudio.com/docs/setup/windows) lap</span><span class="sxs-lookup"><span data-stu-id="cef8d-117">**Windows**: follow the installation instructions on the [Running VS Code on Windows](https://code.visualstudio.com/docs/setup/windows) page</span></span>

### <a name="2-installing-powershell-extension"></a><span data-ttu-id="cef8d-118">2. PowerShell-bővítmény telepítése</span><span class="sxs-lookup"><span data-stu-id="cef8d-118">2. Installing PowerShell Extension</span></span>

- <span data-ttu-id="cef8d-119">A Visual Studio Code-alkalmazások indítása:</span><span class="sxs-lookup"><span data-stu-id="cef8d-119">Launch the Visual Studio Code app by:</span></span>
    - <span data-ttu-id="cef8d-120">**Windows**: írja be `code` a PowerShell-munkamenetben</span><span class="sxs-lookup"><span data-stu-id="cef8d-120">**Windows**: typing `code` in your PowerShell session</span></span>
    - <span data-ttu-id="cef8d-121">**Linux**: írja be `code` a terminálon</span><span class="sxs-lookup"><span data-stu-id="cef8d-121">**Linux**: typing `code` in your terminal</span></span>
    - <span data-ttu-id="cef8d-122">**macOS**: írja be `code` a terminálon</span><span class="sxs-lookup"><span data-stu-id="cef8d-122">**macOS**: typing `code` in your terminal</span></span>

- <span data-ttu-id="cef8d-123">Indítsa el **gyors nyitott** billentyűkombináció lenyomásával **Ctrl + P** (**Cmd + P** Mac gépen).</span><span class="sxs-lookup"><span data-stu-id="cef8d-123">Launch **Quick Open** by pressing **Ctrl+P** (**Cmd+P** on Mac).</span></span>
- <span data-ttu-id="cef8d-124">Írja be a nyitott gyors `ext install powershell` és találati **Enter**.</span><span class="sxs-lookup"><span data-stu-id="cef8d-124">In Quick Open, type `ext install powershell` and hit **Enter**.</span></span>
- <span data-ttu-id="cef8d-125">A **bővítmények** nézet megnyílik az oldalsó sáv.</span><span class="sxs-lookup"><span data-stu-id="cef8d-125">The **Extensions** view will open on the Side Bar.</span></span> <span data-ttu-id="cef8d-126">Jelölje ki a PowerShell-bővítményt a Microsofttól.</span><span class="sxs-lookup"><span data-stu-id="cef8d-126">Select the PowerShell extension from Microsoft.</span></span>
  <span data-ttu-id="cef8d-127">Valami megjelenik alá, például:</span><span class="sxs-lookup"><span data-stu-id="cef8d-127">You will see something like below:</span></span>

  ![VSCode](../../images/vscode.png)

- <span data-ttu-id="cef8d-129">Kattintson a **telepítése** a PowerShell-bővítmény a Microsoft gombjára.</span><span class="sxs-lookup"><span data-stu-id="cef8d-129">Click the **Install** button on the PowerShell extension from Microsoft.</span></span>
- <span data-ttu-id="cef8d-130">A telepítést követően megjelenik az **telepítése** gomb bekapcsolja **Újrabetöltés**.</span><span class="sxs-lookup"><span data-stu-id="cef8d-130">After the install, you will see the **Install** button turns to **Reload**.</span></span>
  <span data-ttu-id="cef8d-131">Kattintson a **Újrabetöltés**.</span><span class="sxs-lookup"><span data-stu-id="cef8d-131">Click on **Reload**.</span></span>
- <span data-ttu-id="cef8d-132">Miután a Visual Studio Code betöltésére tartalmaz, készen áll szerkesztésre.</span><span class="sxs-lookup"><span data-stu-id="cef8d-132">After Visual Studio Code has reload, you are ready for editing.</span></span>

<span data-ttu-id="cef8d-133">Például hozzon létre egy új fájlt, kattintson a **fájl -> új**.</span><span class="sxs-lookup"><span data-stu-id="cef8d-133">For example, to create a new file, click **File->New**.</span></span>
<span data-ttu-id="cef8d-134">Mentse, kattintson a **fájl -> Mentés** és adja meg a fájl nevét, most mondja ki `HelloWorld.ps1`.</span><span class="sxs-lookup"><span data-stu-id="cef8d-134">To save it, click **File->Save** and then provide a file name, let's say `HelloWorld.ps1`.</span></span>
<span data-ttu-id="cef8d-135">Zárja be a fájlt, kattintson a "x" a fájl neve mellett.</span><span class="sxs-lookup"><span data-stu-id="cef8d-135">To close the file, click on "x" next to the file name.</span></span>
<span data-ttu-id="cef8d-136">A Visual Studio Code kilépéshez **fájl -> kilépési**.</span><span class="sxs-lookup"><span data-stu-id="cef8d-136">To exit Visual Studio Code, **File->Exit**.</span></span>

#### <a name="using-a-specific-installed-version-of-powershell"></a><span data-ttu-id="cef8d-137">Egy adott telepített verziójához PowerShell használatával</span><span class="sxs-lookup"><span data-stu-id="cef8d-137">Using a specific installed version of PowerShell</span></span>

<span data-ttu-id="cef8d-138">Ha szeretne egy adott telepítés a PowerShell használata a Visual Studio Code, szüksége lesz egy új változó hozzáadása a felhasználói beállítások fájlhoz.</span><span class="sxs-lookup"><span data-stu-id="cef8d-138">If you wish to use a specific installation of PowerShell with Visual Studio Code, you will need to add a new variable to your user settings file.</span></span>

1. <span data-ttu-id="cef8d-139">Kattintson a **fájl -> Beállítások -> Beállítások**</span><span class="sxs-lookup"><span data-stu-id="cef8d-139">Click **File -> Preferences -> Settings**</span></span>
1. <span data-ttu-id="cef8d-140">Két szerkesztő ablaktábla jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="cef8d-140">Two editor panes will appear.</span></span>
   <span data-ttu-id="cef8d-141">A jobb szélső ablaktáblán (`settings.json`), helyezze be az alábbi beállításoknak megfelelő az operációs rendszer, a két kapcsos zárójelek között (`{` és `}`), és cserélje le  *<version>*  és a telepített PowerShell-verzió:</span><span class="sxs-lookup"><span data-stu-id="cef8d-141">In the right-most pane (`settings.json`), insert the setting below appropriate for your OS somewhere between the two curly brackets (`{` and `}`) and replace *<version>* with the installed PowerShell version:</span></span>

  ```json
    // On Windows:
    "powershell.powerShellExePath": "c:/Program Files/PowerShell/<version>/pwsh.exe"

    // On Linux:
    "powershell.powerShellExePath": "/opt/microsoft/powershell/<version>/pwsh"

    // On macOS:
    "powershell.powerShellExePath": "/usr/local/microsoft/powershell/<version>/pwsh"
  ```
1. <span data-ttu-id="cef8d-142">Cserélje le a beállítás a kívánt PowerShell végrehajtható fájl elérési útja</span><span class="sxs-lookup"><span data-stu-id="cef8d-142">Replace the setting with the path to the desired PowerShell executable</span></span>
1. <span data-ttu-id="cef8d-143">A beállítások mentéséhez, és indítsa újra a Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="cef8d-143">Save the settings file and restart Visual Studio Code</span></span>

#### <a name="configuration-settings-for-visual-studio-code"></a><span data-ttu-id="cef8d-144">A Visual Studio Code beállításait</span><span class="sxs-lookup"><span data-stu-id="cef8d-144">Configuration settings for Visual Studio Code</span></span>

<span data-ttu-id="cef8d-145">Az előző bekezdésben szereplő esetekben lépések segítségével is hozzáadhat konfigurációs beállításai a `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="cef8d-145">By using the steps in the previous paragraph you can add configuration settings in `settings.json`.</span></span>

<span data-ttu-id="cef8d-146">Azt javasoljuk, hogy a Visual Studio Code a következő beállításokat:</span><span class="sxs-lookup"><span data-stu-id="cef8d-146">We recommend the following configuration settings for Visual Studio Code:</span></span>

```json
{
    "csharp.suppressDotnetRestoreNotification": true,
    "editor.renderWhitespace": "all",
    "editor.renderControlCharacters": true,
    "omnisharp.projectLoadTimeout": 120,
    "files.trimTrailingWhitespace": true
}
```

## <a name="debugging-with-visual-studio-code"></a><span data-ttu-id="cef8d-147">A Visual Studio Code-hibakeresés</span><span class="sxs-lookup"><span data-stu-id="cef8d-147">Debugging with Visual Studio Code</span></span>

### <a name="no-workspace-debugging"></a><span data-ttu-id="cef8d-148">Nem-munkaterület hibakeresés</span><span class="sxs-lookup"><span data-stu-id="cef8d-148">No-workspace debugging</span></span>

<span data-ttu-id="cef8d-149">1.9 Visual Studio Code verzió frissítésétől a PowerShell-parancsfájlok hibakeresése is a PowerShell-parancsfájlt tartalmazó mappa megnyitása nélkül.</span><span class="sxs-lookup"><span data-stu-id="cef8d-149">As of Visual Studio Code version 1.9 you can debug PowerShell scripts without having to open the folder containing the PowerShell script.</span></span>
<span data-ttu-id="cef8d-150">Nyissa meg a PowerShell parancsfájl a **fájl nyissa meg a fájl ->...** , állítson be egy töréspontot a sor (nyomja meg a F9), és nyomja le az F5 billentyűt a hibakeresés elindításához.</span><span class="sxs-lookup"><span data-stu-id="cef8d-150">Simply open the PowerShell script file with **File->Open File...**, set a breakpoint on a line (press F9) and then press F5 to start debugging.</span></span>
<span data-ttu-id="cef8d-151">Látni fogja a hibakeresési műveletek ablaktáblán jelennek meg, amelyik lehetővé teszi, hogy megszakítással belépjen a hibakeresőbe, lépés, folytatása, állítsa le a hibakeresést.</span><span class="sxs-lookup"><span data-stu-id="cef8d-151">You will see the Debug actions pane appear which allows you to break into the debugger, step, resume and stop debugging.</span></span>

### <a name="workspace-debugging"></a><span data-ttu-id="cef8d-152">Munkaterület-hibakeresés</span><span class="sxs-lookup"><span data-stu-id="cef8d-152">Workspace debugging</span></span>

<span data-ttu-id="cef8d-153">Munkaterület-hibakeresés hivatkozik egy mappát, a Visual Studio Code használatával megnyitott környezetében hibakeresés **mappa megnyitása...**  a a **fájl** menü.</span><span class="sxs-lookup"><span data-stu-id="cef8d-153">Workspace debugging refers to debugging in the context of a folder that you have opened in Visual Studio Code using **Open Folder...** from the **File** menu.</span></span>
<span data-ttu-id="cef8d-154">A megnyitott mappák általában, a PowerShell-projekt mappát és/vagy a Git-tárház gyökérkönyvtárában.</span><span class="sxs-lookup"><span data-stu-id="cef8d-154">The folder you open is typically your PowerShell project folder and/or the root of your Git repository.</span></span>

<span data-ttu-id="cef8d-155">Ebben a módban, még akkor is, megkezdheti a jelenleg kijelölt PowerShell-parancsfájl hibakeresés egyszerűen az F5 billentyű lenyomásával.</span><span class="sxs-lookup"><span data-stu-id="cef8d-155">Even in this mode, you can start debugging the currently selected PowerShell script by simply pressing F5.</span></span>
<span data-ttu-id="cef8d-156">Azonban munkaterület hibakeresés lehetővé teszi a jelenleg megnyitott fájl csak hibakeresési eltérő több hibakeresési konfigurációk meghatározását.</span><span class="sxs-lookup"><span data-stu-id="cef8d-156">However, workspace debugging allows you to define multiple debug configurations other than just debugging the currently open file.</span></span>
<span data-ttu-id="cef8d-157">Például egy konfigurációt is hozzáadhat:</span><span class="sxs-lookup"><span data-stu-id="cef8d-157">For instance, you can add a configurations to:</span></span>

- <span data-ttu-id="cef8d-158">Indítsa el a hibakeresőben Pester tesztek</span><span class="sxs-lookup"><span data-stu-id="cef8d-158">Launch Pester tests in the debugger</span></span>
- <span data-ttu-id="cef8d-159">Egy adott fájlt a hibakeresőben argumentumokkal indítása</span><span class="sxs-lookup"><span data-stu-id="cef8d-159">Launch a specific file with arguments in the debugger</span></span>
- <span data-ttu-id="cef8d-160">A hibakeresőben egy interaktív munkamenet indítása</span><span class="sxs-lookup"><span data-stu-id="cef8d-160">Launch an interactive session in the debugger</span></span>
- <span data-ttu-id="cef8d-161">A hibakereső csatolása a PowerShell gazdafolyamatokon</span><span class="sxs-lookup"><span data-stu-id="cef8d-161">Attach the debugger to a PowerShell host process</span></span>

<span data-ttu-id="cef8d-162">Kövesse az alábbi lépéseket a hibakeresési konfigurációs fájl létrehozása céljából:</span><span class="sxs-lookup"><span data-stu-id="cef8d-162">Follow these steps to create your debug configuration file:</span></span>

1. <span data-ttu-id="cef8d-163">Nyissa meg a **Debug** billentyűkombináció lenyomásával nézet **Ctrl + Shift + D** (**Cmd + Shift + D** Mac gépen).</span><span class="sxs-lookup"><span data-stu-id="cef8d-163">Open the **Debug** view by pressing **Ctrl+Shift+D** (**Cmd+Shift+D** on Mac).</span></span>
1. <span data-ttu-id="cef8d-164">Nyomja meg a **konfigurálása** fogaskerék ikonra az eszköztárban.</span><span class="sxs-lookup"><span data-stu-id="cef8d-164">Press the **Configure** gear icon in the toolbar.</span></span>
1. <span data-ttu-id="cef8d-165">A Visual Studio Code felszólítja a **válasszon környezet**.</span><span class="sxs-lookup"><span data-stu-id="cef8d-165">Visual Studio Code will prompt you to **Select Environment**.</span></span>
   <span data-ttu-id="cef8d-166">Válasszon **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="cef8d-166">Choose **PowerShell**.</span></span>

   <span data-ttu-id="cef8d-167">Ha így tesz, a Visual Studio Code a munkaterület mappa gyökeréhez hoz létre a könyvtár és a ".vscode\launch.json" fájl.</span><span class="sxs-lookup"><span data-stu-id="cef8d-167">When you do this, Visual Studio Code creates a directory and a file ".vscode\launch.json" in the root of your workspace folder.</span></span>
   <span data-ttu-id="cef8d-168">Ez az a hibakeresési konfigurációs tárolására.</span><span class="sxs-lookup"><span data-stu-id="cef8d-168">This is where your debug configuration is stored.</span></span> <span data-ttu-id="cef8d-169">Ha a fájlok egy Git-tárházban, általában érdemes a launch.json fájl véglegesítése.</span><span class="sxs-lookup"><span data-stu-id="cef8d-169">If your files are in a Git repository, you will typically want to commit the launch.json file.</span></span>
   <span data-ttu-id="cef8d-170">A launch.json fájl tartalma:</span><span class="sxs-lookup"><span data-stu-id="cef8d-170">The contents of the launch.json file are:</span></span>

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

<span data-ttu-id="cef8d-171">A hibakeresési szabhatják jelképez.</span><span class="sxs-lookup"><span data-stu-id="cef8d-171">This represents the common debug scenarios.</span></span>
<span data-ttu-id="cef8d-172">Azonban a fájl megnyitásakor a szerkesztőben, megjelenik egy **konfigurációs hozzáadása...**  gombra.</span><span class="sxs-lookup"><span data-stu-id="cef8d-172">However, when you open this file in the editor, you will see an **Add Configuration...** button.</span></span>
<span data-ttu-id="cef8d-173">A gombra kattintva további PowerShell hibakeresési konfigurációkat.</span><span class="sxs-lookup"><span data-stu-id="cef8d-173">You can press this button to add more PowerShell debug configurations.</span></span> <span data-ttu-id="cef8d-174">Egy kényelmes konfiguráció hozzáadása **PowerShell: Indítsa el parancsfájl**.</span><span class="sxs-lookup"><span data-stu-id="cef8d-174">One handy configuration to add is **PowerShell: Launch Script**.</span></span>
<span data-ttu-id="cef8d-175">Ezzel a konfigurációval a megadott fájlt nem kötelező argumentum, el kell indítani, amikor lenyomja az F5 függetlenül attól, hogy mely fájl jelenleg aktív, a szerkesztőben is megadhat.</span><span class="sxs-lookup"><span data-stu-id="cef8d-175">With this configuration, you can specify a specific file with optional arguments that should be launched whenever you press F5 no matter which file is currently active in the editor.</span></span>

<span data-ttu-id="cef8d-176">Miután létrejött a hibakeresési konfigurációt, mely egy, a hibakeresési konfigurációból legördülő a hibakeresési munkamenetben használni kívánt konfigurációs kiválaszthatja a **Debug** nézet eszköztár.</span><span class="sxs-lookup"><span data-stu-id="cef8d-176">Once the debug configuration is established, you can select which configuration you want to use during a debug session by selecting one from the debug configuration drop-down in the **Debug** view's toolbar.</span></span>

<span data-ttu-id="cef8d-177">Van néhány olyan rendszerek, amelyek segíthetnek az első lépésekhez, a Visual Studio Code PowerShell bővítmény használatával</span><span class="sxs-lookup"><span data-stu-id="cef8d-177">There are a few blogs that may be helpful to get you started using PowerShell extension for Visual Studio Code</span></span>

- <span data-ttu-id="cef8d-178">A Visual Studio Code: [PowerShell bővítmény][ps-extension]</span><span class="sxs-lookup"><span data-stu-id="cef8d-178">Visual Studio Code: [PowerShell Extension][ps-extension]</span></span>
- <span data-ttu-id="cef8d-179">[Írási és a Visual Studio Code PowerShell-parancsfájlok hibakeresése][debug]</span><span class="sxs-lookup"><span data-stu-id="cef8d-179">[Write and debug PowerShell scripts in Visual Studio Code][debug]</span></span>
- <span data-ttu-id="cef8d-180">[A Visual Studio Code útmutatást hibakeresés][vscode-guide]</span><span class="sxs-lookup"><span data-stu-id="cef8d-180">[Debugging Visual Studio Code Guidance][vscode-guide]</span></span>
- <span data-ttu-id="cef8d-181">[A Visual Studio Code hibakeresési PowerShell][ps-vscode]</span><span class="sxs-lookup"><span data-stu-id="cef8d-181">[Debugging PowerShell in Visual Studio Code][ps-vscode]</span></span>
- <span data-ttu-id="cef8d-182">[Ismerkedés a Visual Studio Code PowerShell-fejlesztésbe.][getting-started]</span><span class="sxs-lookup"><span data-stu-id="cef8d-182">[Get started with PowerShell development in Visual Studio Code][getting-started]</span></span>
- <span data-ttu-id="cef8d-183">[A Visual Studio Code szerkesztési képességeket PowerShell fejlesztési – 1. rész][editing-part1]</span><span class="sxs-lookup"><span data-stu-id="cef8d-183">[Visual Studio Code editing features for PowerShell development – Part 1][editing-part1]</span></span>
- <span data-ttu-id="cef8d-184">[A Visual Studio Code szerkesztési képességeket PowerShell fejlesztési – 2. rész][editing-part2]</span><span class="sxs-lookup"><span data-stu-id="cef8d-184">[Visual Studio Code editing features for PowerShell development – Part 2][editing-part2]</span></span>
- <span data-ttu-id="cef8d-185">[Hibakeresési PowerShell-parancsfájlt a Visual Studio Code – 1. rész][debugging-part1]</span><span class="sxs-lookup"><span data-stu-id="cef8d-185">[Debugging PowerShell script in Visual Studio Code – Part 1][debugging-part1]</span></span>
- <span data-ttu-id="cef8d-186">[Hibakeresési PowerShell-parancsfájlt a Visual Studio Code – 2. rész][debugging-part2]</span><span class="sxs-lookup"><span data-stu-id="cef8d-186">[Debugging PowerShell script in Visual Studio Code – Part 2][debugging-part2]</span></span>

[ise]: ../ise-guide.md
[install-pscore-linux]:  ../../setup/Installing-PowerShell-Core-on-macOS-and-Linux.md
[install-pscore-windows]: ../../setup/Installing-PowerShell-Core-on-Windows.md
[install-winps]: ../../setup/Installing-Windows-PowerShell.md
[ps-extension]:https://blogs.msdn.microsoft.com/cdndevs/2015/12/11/visual-studio-code-powershell-extension/
[debug]:https://blogs.msdn.microsoft.com/powershell/2015/11/16/announcing-powershell-language-support-for-visual-studio-code-and-more/
[vscode-guide]:https://johnpapa.net/debugging-with-visual-studio-code/
[ps-vscode]:https://github.com/PowerShell/vscode-powershell/tree/master/examples
[getting-started]:https://blogs.technet.microsoft.com/heyscriptingguy/2016/12/05/get-started-with-powershell-development-in-visual-studio-code/
[editing-part1]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/11/visual-studio-code-editing-features-for-powershell-development-part-1/
[editing-part2]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/01/12/visual-studio-code-editing-features-for-powershell-development-part-2/
[debugging-part1]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/06/debugging-powershell-script-in-visual-studio-code-part-1/
[debugging-part2]:https://blogs.technet.microsoft.com/heyscriptingguy/2017/02/13/debugging-powershell-script-in-visual-studio-code-part-2/

## <a name="powershell-extension-for-visual-studio-code"></a><span data-ttu-id="cef8d-187">A Visual Studio Code PowerShell kiterjesztése</span><span class="sxs-lookup"><span data-stu-id="cef8d-187">PowerShell Extension for Visual Studio Code</span></span>

<span data-ttu-id="cef8d-188">A PowerShell bővítmény forráskód található [GitHub](https://github.com/PowerShell/vscode-powershell).</span><span class="sxs-lookup"><span data-stu-id="cef8d-188">The PowerShell extension's source code can be found on [GitHub](https://github.com/PowerShell/vscode-powershell).</span></span>
