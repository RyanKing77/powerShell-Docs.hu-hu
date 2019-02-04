---
title: Az ISE-élmény replikálása a Visual Studio Code-ban
description: Az ISE-élmény replikálása a Visual Studio Code-ban
ms.date: 08/06/2018
ms.openlocfilehash: 983da850c13d72bcdc7b2d33970c6e9e06b3d869
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687376"
---
# <a name="how-to-replicate-the-ise-experience-in-visual-studio-code"></a>Az ISE-élmény replikálása a Visual Studio Code-ban

A PowerShell-bővítmény VSCode-nem keresik a PowerShell ISE-teljes funkcióparitás, amíg nincsenek funkciók a VSCode-élmény több természetes tehet felhasználói számára az ISE-ben.

Ez a dokumentum próbál konfigurálhatja a vscode-ban, hogy a felhasználói felület az ISE képest egy kicsit több ismerős beállítások.

## <a name="key-bindings"></a>Külsőkulcskötéseinek

| Függvény                              | ISE-kötés                  | VSCode-kötés                              |
| ----------------                      | -----------                  | --------------                              |
| Megszakítás és break ladicí program          | <kbd>Ctrl</kbd>+<kbd>B</kbd> | <kbd>F6</kbd>                               |
| Hajtsa végre az aktuális sor/kiemelt szöveg | <kbd>F8</kbd>                | <kbd>F8</kbd>                               |
| Lista elérhető kódrészletek               | <kbd>Ctrl</kbd>+<kbd>J</kbd> | <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>J</kbd> |

### <a name="custom-key-bindings"></a>Egyéni kulcs kötések használata

Is [konfigurálása saját külsőkulcskötéseinek](https://code.visualstudio.com/docs/getstarted/keybindings#_custom-keybindings-for-refactorings) a vscode-ban is.

## <a name="tab-completion"></a>Kiegészítés

Ahhoz, hogy több ISE-szerű kiegészítés, adja hozzá ezt a beállítást:

```json
"editor.tabCompletion": "on"
```

> [!NOTE]
> Ez a beállítás lett hozzáadva, közvetlenül a VSCode (nem a bővítmény). Annak viselkedését határozza meg VSCode közvetlenül, és a bővítmény által nem módosítható.

## <a name="no-focus-on-console-when-executing"></a>A konzolon végrehajtásakor nincs fókusz

Tartani a fókusz a szerkesztőben a végrehajtásakor <kbd>F8</kbd>:

```json
"powershell.integratedConsole.focusConsoleOnExecute": false
```

Az alapértelmezett érték `true` kisegítő célokra.

## <a name="dont-start-integrated-console-on-startup"></a>Indításkor nem integrált konzol elindítása

Állítsa le a integrált konzol az indítási, állítsa be:

```json
"powershell.integratedConsole.showOnStartup": false
```

> [!NOTE]
> A háttérben PowerShell folyamat továbbra is indul el, mivel biztosítja az IntelliSense, parancsfájl-elemző, szimbólum navigációs stb. De a konzol nem jelennek meg.

## <a name="assume-files-are-powershell-by-default"></a>Tegyük fel, fájlok PowerShell alapértelmezés szerint.

Ahhoz, hogy új/cím nélküli fájlokat, regisztrálja, a PowerShell alapértelmezés szerint:

```json
"files.defaultLanguage": "powershell"
```

## <a name="color-scheme"></a>Színsémát

Nincsenek elérhető, hogy a keresés sokkal több, mint például az ISE-szerkesztő VSCode-számos ISE téma.

Az a [Parancskatalógus] típus `theme` beolvasni `Preferences: Color Theme` nyomja le az ENTER <kbd>Enter</kbd>.
Válassza ki a legördülő listából `PowerShell ISE`.

Ez a téma a-beállításokat adhatja meg:

```json
"workbench.colorTheme": "PowerShell ISE"
```

## <a name="powershell-command-explorer"></a>PowerShell-paranccsal Explorer

Munkájának köszönhetően [ @corbob ](https://github.com/corbob), a PowerShell-bővítmény rendelkezik a saját parancs explorer alapjait.

Az a [Parancskatalógus], adja meg `PowerShell Command Explorer` nyomja le az ENTER <kbd>Enter</kbd>.

## <a name="open-in-the-ise"></a>Nyissa meg az ISE-ben

Ha Ön megtörténhet, aki a ennek ellenére az ISE-ben nyisson meg egy fájlt, akkor használhatja <kbd>Shift</kbd>+<kbd>Alt</kbd>+<kbd>P</kbd>.

## <a name="other-resources"></a>Egyéb erőforrások

- 4sysops rendelkezik [egy remek cikket](https://4sysops.com/archives/make-visual-studio-code-look-and-behave-like-powershell-ise/) VSCode lehet több, mint például az ISE-ben való konfigurálásával kapcsolatban.
- Mike F Robbins rendelkezik [nagyszerű hozzászólás](https://mikefrobbins.com/2017/08/24/how-to-install-visual-studio-code-and-configure-it-as-a-replacement-for-the-powershell-ise/) VSCode beállításával.
- Ismerje meg a PowerShell rendelkezik [fel egy kiváló írási](https://www.learnpwsh.com/setup-vs-code-for-powershell/) PowerShell beállítása a VSCode beolvasása.

## <a name="more-settings"></a>További beállítások

Ha több módon teheti a VSCode megszokottabb ISE felhasználók úgy ismeri, járul hozzá ezt a dokumentumot. Ha a keresett kompatibilitási konfigurációs van, de nem találja az engedélyezéshez, bármilyen módon [nyissa meg a probléma](https://github.com/PowerShell/vscode-powershell/issues/new/choose) és kérdezzen!

Mindig örömmel fogadja el a lekéréses kérelmek és a hozzájárulások is!

## <a name="vscode-tips"></a>VSCode-tippek

### <a name="command-palette"></a>Parancskatalógus

<kbd>F1</kbd> vagy <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> (<kbd>Cmd</kbd> + <kbd> SHIFT</kbd>+<kbd>P</kbd> macOS rendszeren)

Sablonszolgáltatása segítségével kényelmesen parancsok végrehajtása a vscode-ban.
További információkért lásd: [a VSCode-docs](https://code.visualstudio.com/docs/getstarted/userinterface#_command-palette).

[Parancskatalógus]: #command-palette
