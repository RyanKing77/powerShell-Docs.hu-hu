# <a name="using-visual-studio-code-for-powershell-development"></a>A Visual Studio Code fejlesztési PowerShell használatával

Kívül a [PowerShell ISE][ise], PowerShell egyben a Visual Studio Code jól támogatott.
Ezenkívül az ISE használata nem támogatott PowerShell mag, amíg a Visual Studio Code PowerShell Core támogatott platformon (a Windows, a macOS és a Linux)

Használhatja a Visual Studio Code a Windows PowerShell használatával 5-ös verzióját a Windows 10 vagy telepítésével [Windows Management Framework 5.0 RTM](https://www.microsoft.com/en-us/download/details.aspx?id=50395) a régebbi verziójú Windows OSs (Windows 8.1, stb.).

Az megkezdése előtt ellenőrizze, hogy PowerShell létezik a rendszeren.
A Windows, a macOS és a Linux modern munkaterhelések esetén lásd:

- [PowerShell központi telepítése Linux rendszeren][install-pscore-linux]
- [MacOS PowerShell központi telepítése][install-pscore-macos]
- [A Windows PowerShell központi telepítése][install-pscore-windows]

A hagyományos Windows PowerShell-munkaterhelésekhez, lásd: [Windows PowerShell telepítése][install-winps].

## <a name="editing-with-visual-studio-code"></a>Szerkesztés a Visual Studio Code

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[1. A Visual Studio Code telepítése](https://code.visualstudio.com/Docs/setup/setup-overview)

- **Linux**: a telepítési utasításokat kövesse a [VS kódot futtató Linux](https://code.visualstudio.com/docs/setup/linux) lap

- **macOS**: a telepítési utasításokat kövesse a [VS kódot futtató macOS](https://code.visualstudio.com/docs/setup/mac) lap

> [!IMPORTANT]
> MacOS telepítenie kell a PowerShell-bővítmény OpenSSL megfelelő működéséhez.
> Ehhez a legegyszerűbb módja a telepítendő [Homebrew](http://brew.sh/) , majd futtassa `brew install openssl`.
> Visual STUDIO Code most betöltheti az a PowerShell-bővítmény sikeresen megtörtént.

- **Windows**: a telepítési utasításokat kövesse a [VS kódot futtató Windows](https://code.visualstudio.com/docs/setup/windows) lap

### <a name="2-installing-powershell-extension"></a>2. PowerShell-bővítmény telepítése

- A Visual Studio Code-alkalmazások indítása:
    - **Windows**: írja be `code` a PowerShell-munkamenetben
    - **Linux**: írja be `code` a terminálon
    - **macOS**: írja be `code` a terminálon

- Indítsa el **gyors nyitott** billentyűkombináció lenyomásával **Ctrl + P** (**Cmd + P** Mac gépen).
- Írja be a nyitott gyors `ext install powershell` és találati **Enter**.
- A **bővítmények** nézet az oldalsó sáv megnyitása. Jelölje ki a PowerShell-bővítményt a Microsofttól.
  Valami kell megjelennie alatt, például:

  ![VSCode](../../images/vscode.png)

- Kattintson a **telepítése** a PowerShell-bővítmény a Microsoft gombjára.
- A telepítést követően megjelenik az **telepítése** gomb bekapcsolja **Újrabetöltés**.
  Kattintson a **Újrabetöltés**.
- Miután a Visual Studio Code betöltésére tartalmaz, készen áll szerkesztésre.

Például hozzon létre egy új fájlt, kattintson a **fájl -> új**.
Mentse, kattintson a **fájl -> Mentés** és adja meg a fájl nevét, most mondja ki `HelloWorld.ps1`.
Zárja be a fájlt, kattintson a "x" a fájl neve mellett.
A Visual Studio Code kilépéshez **fájl -> kilépési**.

#### <a name="using-a-specific-installed-version-of-powershell"></a>Egy adott telepített verziójához PowerShell használatával

Ha szeretne egy adott telepítés a PowerShell használata a Visual Studio Code, akkor új változó hozzáadása a felhasználói beállítások fájl.

1. Kattintson a **fájl -> Beállítások -> Beállítások**
1. Két szerkesztő ablaktábla jelennek meg.
   A jobb szélső ablaktáblán (`settings.json`), helyezze be az alábbi beállításoknak megfelelő az operációs rendszer, a két kapcsos zárójelek között (`{` és `}`), és cserélje le *<version>* és a telepített PowerShell-verzió:

  ```json
    // On Windows:
    "powershell.powerShellExePath": "c:/Program Files/PowerShell/<version>/pwsh.exe"

    // On Linux:
    "powershell.powerShellExePath": "/opt/microsoft/powershell/<version>/pwsh"

    // On macOS:
    "powershell.powerShellExePath": "/usr/local/microsoft/powershell/<version>/pwsh"
  ```
1. Cserélje le a beállítás a kívánt PowerShell végrehajtható fájl elérési útja
1. A beállítások mentéséhez, és indítsa újra a Visual Studio Code

#### <a name="configuration-settings-for-visual-studio-code"></a>A Visual Studio Code beállításait

Az előző bekezdésben szereplő esetekben lépések segítségével is hozzáadhat konfigurációs beállításai a `settings.json`.

Azt javasoljuk, hogy a Visual Studio Code a következő beállításokat:

```json
{
    "csharp.suppressDotnetRestoreNotification": true,
    "editor.renderWhitespace": "all",
    "editor.renderControlCharacters": true,
    "omnisharp.projectLoadTimeout": 120,
    "files.trimTrailingWhitespace": true
}
```

## <a name="debugging-with-visual-studio-code"></a>A Visual Studio Code-hibakeresés

### <a name="no-workspace-debugging"></a>Nem-munkaterület hibakeresés

1.9 Visual Studio Code verzió frissítésétől a PowerShell-parancsfájlok hibakeresése is a PowerShell-parancsfájlt tartalmazó mappa megnyitása nélkül.
Nyissa meg a PowerShell parancsfájl a **fájl nyissa meg a fájl ->...** , állítson be egy töréspontot a sor (nyomja meg a F9), és nyomja le az F5 billentyűt a hibakeresés elindításához.
Meg kell jelennie a hibakeresési műveletek ablaktáblán jelennek meg, amelyik lehetővé teszi, hogy megszakítással belépjen a hibakeresőbe, lépés, folytatása, állítsa le a hibakeresést.

### <a name="workspace-debugging"></a>Munkaterület-hibakeresés

Munkaterület-hibakeresés hivatkozik egy mappát, a Visual Studio Code használatával megnyitott környezetében hibakeresés **mappa megnyitása...**  a a **fájl** menü.
A megnyitott mappák általában, a PowerShell-projekt mappát és/vagy a Git-tárház gyökérkönyvtárában.

Ebben a módban, még akkor is, megkezdheti a jelenleg kijelölt PowerShell-parancsfájl hibakeresés egyszerűen az F5 billentyű lenyomásával.
Azonban munkaterület hibakeresés lehetővé teszi a jelenleg megnyitott fájl csak hibakeresési eltérő több hibakeresési konfigurációk meghatározását.
Például egy konfigurációt is hozzáadhat:

- Indítsa el a hibakeresőben Pester tesztek
- Egy adott fájlt a hibakeresőben argumentumokkal indítása
- A hibakeresőben egy interaktív munkamenet indítása
- A hibakereső csatolása a PowerShell gazdafolyamatokon

Kövesse az alábbi lépéseket a hibakeresési konfigurációs fájl létrehozása céljából:

1. Nyissa meg a **Debug** billentyűkombináció lenyomásával nézet **Ctrl + Shift + D** (**Cmd + Shift + D** Mac gépen).
1. Nyomja meg a **konfigurálása** fogaskerék ikonra az eszköztárban.
1. A Visual Studio Code kéri, hogy **válasszon környezet**.
   Válasszon **PowerShell**.

   Ha így tesz, a Visual Studio Code a munkaterület mappa gyökeréhez hoz létre a könyvtár és a ".vscode\launch.json" fájl.
   Ez az a hibakeresési konfigurációs tárolására. Ha a fájlok egy Git-tárházban, általában kívánt véglegesíti a launch.json fájl.
   A launch.json fájl tartalma:

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

A hibakeresési szabhatják jelképez.
Azonban a fájl megnyitásakor a szerkesztőben, megjelenik egy **konfigurációs hozzáadása...**  gombra.
A gombra kattintva további PowerShell hibakeresési konfigurációkat. Egy kényelmes konfiguráció hozzáadása **PowerShell: Indítsa el parancsfájl**.
Ezzel a konfigurációval a megadott fájlt nem kötelező argumentum, el kell indítani, amikor lenyomja az F5 függetlenül attól, hogy mely fájl jelenleg aktív, a szerkesztőben is megadhat.

Miután létrejött a hibakeresési konfigurációt, mely egy, a hibakeresési konfigurációból legördülő a hibakeresési munkamenetben használni kívánt konfigurációs kiválaszthatja a **Debug** nézet eszköztár.

Van néhány olyan rendszerek, amelyek segíthetnek az első lépésekhez, a Visual Studio Code PowerShell bővítmény használatával

- A Visual Studio Code: [PowerShell bővítmény][ps-extension]
- [Írási és a Visual Studio Code PowerShell-parancsfájlok hibakeresése][debug]
- [A Visual Studio Code útmutatást hibakeresés][vscode-guide]
- [A Visual Studio Code hibakeresési PowerShell][ps-vscode]
- [Ismerkedés a Visual Studio Code PowerShell-fejlesztésbe.][getting-started]
- [A Visual Studio Code szerkesztési képességeket PowerShell fejlesztési – 1. rész][editing-part1]
- [A Visual Studio Code szerkesztési képességeket PowerShell fejlesztési – 2. rész][editing-part2]
- [Hibakeresési PowerShell-parancsfájlt a Visual Studio Code – 1. rész][debugging-part1]
- [Hibakeresési PowerShell-parancsfájlt a Visual Studio Code – 2. rész][debugging-part2]

[ise]: ../ise-guide.md
[install-pscore-linux]:  ../../setup/Installing-PowerShell-Core-on-Linux.md
[install-pscore-macos]:  ../../setup/Installing-PowerShell-Core-on-macOS.md
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

## <a name="powershell-extension-for-visual-studio-code"></a>A Visual Studio Code PowerShell kiterjesztése

A PowerShell bővítmény forráskód található [GitHub](https://github.com/PowerShell/vscode-powershell).
