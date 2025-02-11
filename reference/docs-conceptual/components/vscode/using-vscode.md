---
title: PowerShell-fejlesztéshez a Visual Studio Code használatával
description: PowerShell-fejlesztéshez a Visual Studio Code használatával
ms.date: 08/06/2018
ms.openlocfilehash: 6a0da6e060693dc7cfc08d40fd658414dc23d660
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67733876"
---
# <a name="using-visual-studio-code-for-powershell-development"></a>PowerShell-fejlesztéshez a Visual Studio Code használatával

Mellett a [PowerShell ISE-ben][ise], PowerShell egyben a Visual Studio Code jól támogatott.
Ezenkívül az ISE-ben nem támogatott a PowerShell Core, a Visual Studio Code-ot minden platformon (Windows, macOS és Linux) a PowerShell Core támogatott

Használhatja a Visual Studio Code Windows PowerShell 5-ös verzió Windows 10-es vagy telepítésével [Windows Management Framework 5.0 RTM](https://devblogs.microsoft.com/powershell/windows-management-framework-wmf-5-0-rtm-is-now-available-via-the-microsoft-update-catalog/) a régebbi verziójú Windows nyílt forráskódú (pl. Windows 8.1, stb.).

Mielőtt hozzákezdene, ellenőrizze, hogy PowerShell létezik a rendszerben.
Számítási feladatok Windows, macOS és Linux rendszereken lásd:

- [A PowerShell Core telepítése Linux rendszeren][install-pscore-linux]
- [A PowerShell Core telepítése macOS rendszeren][install-pscore-macos]
- [Windows PowerShell Core telepítése][install-pscore-windows]

Windows PowerShell hagyományos számítási feladatok esetén tekintse meg a [Windows PowerShell telepítése][install-winps].

## <a name="editing-with-visual-studio-code"></a>A Visual Studio Code-dal szerkesztése

### <a name="1-installing-visual-studio-codehttpscodevisualstudiocomdocssetupsetup-overview"></a>[1. A Visual Studio Code telepítése](https://code.visualstudio.com/Docs/setup/setup-overview)

- **Linux**: kövesse a telepítési utasításokat a [Linux rendszeren futó VS Code](https://code.visualstudio.com/docs/setup/linux) lap

- **macOS**: kövesse a telepítési utasításokat a [macOS rendszeren futó VS Code](https://code.visualstudio.com/docs/setup/mac) lap

  > [!IMPORTANT]
  > MacOS-gépeken telepítenie kell a PowerShell-bővítmény OpenSSL megfelelő működéséhez.
  > Ennek legegyszerűbb módja az, hogy telepítése [Homebrew](https://brew.sh/) , majd futtassa `brew install openssl`.
  > A VS Code most már betöltheti a PowerShell-bővítmény sikeresen megtörtént.

- **Windows**: kövesse a telepítési utasításokat a [VS Code fut a Windows](https://code.visualstudio.com/docs/setup/windows) lap

### <a name="2-installing-powershell-extension"></a>2. PowerShell-bővítmény telepítése

- Indítsa el a Visual Studio Code az alkalmazás által:
  - **Windows**: beírni `code` a PowerShell-munkamenetben
  - **Linux**: beírni `code` a terminálban
  - **macOS**: beírni `code` a terminálban

- Indítsa el a **jelenítse meg a Gyorsmegnyitási** lenyomásával **Ctrl + P** (**Cmd + P** Mac gépen).
- Írja be a Megnyitás gyors `ext install powershell` kattintok **Enter**.
- A **bővítmények** nézet nyílik az oldalsó sáv. Válassza ki a PowerShell-bővítmény a Microsoft.
  Megjelennie alábbi módon:

  ![VSCode](../../images/vscode.png)

- Kattintson a **telepítése** a PowerShell-bővítmény a Microsoft gombjára.
- A telepítést követően megjelenik a **telepítése** gomb kerül, **Újrabetöltés**.
  Kattintson a **Újrabetöltés**.
- Miután a Visual Studio Code újbóli betöltése rendelkezik, készen áll szerkesztésre.

Például hozzon létre egy új fájlt, kattintson a **fájl -> új**.
A mentéshez kattintson **File -> Mentés** adja meg a fájl nevét, most tegyük fel, és `HelloWorld.ps1`.
Zárja be a fájlt, kattintson a "x", a fájl neve mellett.
Lépjen ki a Visual Studio Code-ban való **File -> kilépési**.

### <a name="installing-the-powershell-extension-on-restricted-systems"></a>Korlátozott rendszereken a PowerShell-bővítmény telepítése

Egyes rendszerek állítsa be úgy, hogy az összes kód aláírása ellenőrizendő igényel, és megköveteli, PowerShell-szerkesztő szolgáltatások manuálisan kell jóváhagyni a rendszeren való futtatásához.
Egy csoportházirend-frissítés, amely módosítja a végrehajtási házirend ennek valószínű oka, ha a PowerShell-bővítmény telepítve van, de az elérni próbált hasonló hibával:

```
Language server startup failed.
```

Manuális jóváhagyásáról PowerShell szerkesztő szolgáltatásokat, és így a PowerShell-bővítmény VSCode-nyisson meg egy PowerShell parancssort és futtassa:

```powershell
Import-Module $HOME\.vscode\extensions\ms-vscode.powershell*\modules\PowerShellEditorServices\PowerShellEditorServices.psd1
```

A program "Szeretné futtatni a szoftvert a nem megbízható közzétételi?"
Típus `R` , futtassa a fájlt. Ezután nyissa meg a Visual Studio Code-ot, és ellenőrizze, hogy a PowerShell-bővítmény megfelelően működik-e. Ha továbbra is problémákba ütközik bevezetés, ossza meg velünk az [GitHub](https://github.com/PowerShell/vscode-powershell/issues).

#### <a name="choosing-a-version-of-powershell-to-use-with-the-extension"></a>A kiterjesztéssel használandó PowerShell-verzió kiválasztása

A PowerShell Core egymás mellett telepíti a Windows PowerShell-lel azt most már lehetőség van a PowerShell-bővítmény használata a PowerShell egy adott verzióját. Használja az alábbi lépéseket a verzió kiválasztása:

1. Nyissa meg a parancs raklap (<kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> a Windows és Linux-alapú <kbd>Cmd</kbd> + <kbd>Shift</kbd>+<kbd>P</kbd> macOS rendszeren).
1. Keresse meg "Munkamenet".
1. Kattintson a "PowerShell: Munkamenet menü megjelenítése".
1. Válassza ki a listából – például "a PowerShell Core" használni kívánt PowerShell verzióját.

>[!IMPORTANT]
> Ez a szolgáltatás néhány jól ismert elérési utak megvizsgálja a különböző operációs rendszerek felderítéséhez PowerShell telepítési helyét. Ha PowerShell-jellemző helyre telepítette, akkor előfordulhat, hogy nem jelennek kezdetben a munkamenet menü. A munkamenet menü által bővítése [hozzáadása a saját egyéni útvonalak](#adding-your-own-powershell-paths-to-the-session-menu) alább leírtak szerint.

>[!NOTE]
> A munkamenet menüből való másik módja is van. Egy PowerShell-fájlra a szerkesztőben megnyitott, megjelenik egy zöld verziószámot jobb alsó. Ez a verziószám kattintva irányítja a munkamenet menüben.

##### <a name="adding-your-own-powershell-paths-to-the-session-menu"></a>A saját PowerShell-elérési út hozzáadása a munkamenet menü

A munkamenet menü a VS Code beállításnál is hozzáadhat más PowerShell végrehajtható elérési utak.

Vegyen fel egy elemet a listában `powershell.powerShellAdditionalExePaths` lista létrehozása, ha az nem létezik, vagy a `settings.json`:

```json
{
    // other settings...

    "powershell.powerShellAdditionalExePaths": [
        {
            "exePath": "C:\\Users\\tyler\\Downloads\\PowerShell\\pwsh.exe",
            "versionName": "Downloaded PowerShell"
        }
    ],
    
    // other settings...
}
```

Minden elem kell rendelkeznie:

* `exePath`: Az elérési útját a `pwsh` vagy `powershell` végrehajtható.
* `versionName`: A szöveg, amely a munkamenet menü fog megjelenni.

Beállíthatja az alapértelmezett PowerShell-verzió használatához használja a `powershell.powerShellDefaultVersion` beállítás szerint a beállítás Ez a szöveg jelenik meg a munkamenet menü (más néven a `versionName` az utolsó beállításai):

```json
{
    // other settings...

    "powershell.powerShellAdditionalExePaths": [
        {
            "exePath": "C:\\Users\\tyler\\Downloads\\PowerShell\\pwsh.exe",
            "versionName": "Downloaded PowerShell"
        }
    ],
    
    "powershell.powerShellDefaultVersion": "Downloaded PowerShell",
    
    // other settings...
}
```

Miután beállította ezt a beállítást, indítsa újra a Visual Studio Code, vagy használja a a "fejlesztői: Töltse be újra az ablakban"parancs raklap művelet az aktuális vscode-ablak.

Ha a munkamenet menü megnyitásához, ekkor megjelenik a további PowerShell-verzió!

> [!NOTE]
> Forrás PowerShell hoz létre, ez-e a PowerShell helyi build kipróbálásához nagyszerű lehetőséget.

#### <a name="configuration-settings-for-visual-studio-code"></a>A Visual Studio Code-konfigurációs beállítások

Az előző bekezdésben leírt lépések végrehajtásával adja hozzá a konfigurációs beállítások `settings.json`.

Azt javasoljuk, hogy a Visual Studio Code a következő beállításokat:

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

Ha nem szeretné ezeket a beállításokat az összes fájltípus hatással, VSCode is lehetővé teszi, hogy nyelvenkénti konfigurációkat. Hozzon létre egy adott nyelvi beállítás beállításait írja a `[<language-name>]` mező. Például:

```json
"[powershell]": {
    "files.encoding": "utf8bom",
    "files.autoGuessEncoding": true
}
```

Fájllal kapcsolatos további információk a VS Code-ban kódolási: [ismertetése fájlkódolás](understanding-file-encoding.md).

## <a name="debugging-with-visual-studio-code"></a>Hibakeresés a Visual Studio Code-dal

### <a name="no-workspace-debugging"></a>Nem-munkaterület-hibakeresés

1\.9-es verziója a Visual Studio Code-tól a PowerShell-parancsfájlok hibakeresése is a PowerShell-parancsfájlt tartalmazó mappa megnyitása nélkül. Nyissa meg a PowerShell-parancsfájl tárolásához a **File -> fájl megnyitása...** , állítson be egy töréspontot sorban (F9 lenyomás), és nyomja le az F5 billentyűt a hibakeresés elindításához. A hibakeresési műveletek panelen jelennek meg, amely lehetővé teszi, hogy a hibakeresőt, lépés, folytatása és stop-hibakeresés felosztása kell megjelennie.

### <a name="workspace-debugging"></a>Munkaterület-hibakeresés

Munkaterület hibakeresés hivatkozik egy mappát a Visual Studio Code használatával megnyitott kontextusában hibakeresés **mappa megnyitása...**  származó a **fájl** menü.
A mappát, nyissa meg a PowerShell projektmappába és/vagy a Git-tárház gyökérkönyvtárában általában.

Ebben a módban, még akkor is, elindíthatja a jelenleg kijelölt PowerShell-parancsprogram-hibakeresés egyszerűen az F5 billentyű lenyomásával.
Azonban munkaterület hibakeresés lehetővé teszi több hibakeresési konfiguráció eltérő csak hibakeresés a jelenleg megnyitott fájl határozza meg.
Például egy konfigurációkat adhat hozzá:

- Indítsa el a hibakeresőt a Pester tesztek
- Indítsa el egy adott fájlra a hibakeresőt a argumentumokkal
- A hibakereső egy interaktív munkamenet indítása
- Csatolja a hibakeresőt a PowerShell gazdafolyamatokon

Kövesse az alábbi lépéseket a hibakeresési konfigurációs fájl létrehozása céljából:

  1. Nyissa meg a **Debug** lenyomásával nézet **Ctrl + Shift + D** (**Cmd + Shift + D** Mac gépen).
  2. Nyomja le az **konfigurálása** fogaskerék ikont, az eszköztáron.
  3. A Visual Studio Code felszólítja, hogy **környezet kiválasztása**. Válasszon **PowerShell**.

  Ha így tesz, a Visual Studio Code létrehoz egy könyvtárat és a egy ".vscode\launch.json" fájlt a munkaterület gyökérkönyvtárába.
  Ez az a hibakeresési konfigurációs tárolására. Ha a fájlok egy Git-tárházban, általában a launch.json fájl véglegesíteni kívánja.
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

  Ez a hibakeresési gyakori helyzetek jelöli.
  Azonban ez a fájl megnyitásakor a szerkesztőben megjelenik egy **konfiguráció hozzáadása...**  gombra.
  A gombra kattintva további PowerShell hibakeresési konfigurációk hozzáadása. Hozzáadása egy praktikus konfigurációs van **PowerShell: Indítsa el a szkript**.
  Ebben a konfigurációban is megadhat egy adott fájlt, amikor, nyomja le az F5 nincs függetlenül attól, hogy melyik fájlt a szerkesztőben a jelenleg aktív indítható választható argumentumokat.

  Ha a hibakeresési konfigurációs létrejött, melyik konfiguráció, ha kiválaszt egy, a hibakeresési konfigurációjából legördülő a hibakeresési munkamenet során használni kívánt kiválaszthatja a **Debug** nézet eszköztárán.

Van néhány hasznos az első lépésekhez a PowerShell-bővítmény használata a Visual Studio Code-blogok:

- [PowerShell-bővítmény][ps-extension]
- [Írási és hibakeresése a Visual Studio Code-ban a PowerShell-parancsprogramok][debug]
- [Hibakeresés a Visual Studio Code-útmutató][vscode-guide]
- [Hibakeresés a PowerShell, a Visual Studio Code-ban][ps-vscode]
- [PowerShell-fejlesztés a Visual Studio Code-ban – első lépések][getting-started]
- [PowerShell-fejlesztéshez – 1. rész funkciók szerkesztése a Visual Studio Code][editing-part1]
- [PowerShell-fejlesztéshez – 2. rész funkciók szerkesztése a Visual Studio Code][editing-part2]
- [Hibakeresés a PowerShell-parancsfájlt a Visual Studio Code – 1. rész][debugging-part1]
- [Hibakeresés a PowerShell-parancsfájlt a Visual Studio Code – 2. rész][debugging-part2]

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

## <a name="powershell-extension-for-visual-studio-code"></a>PowerShell-bővítmény a Visual Studio Code

A PowerShell-bővítmény forráskód találhatók [GitHub](https://github.com/PowerShell/vscode-powershell).
