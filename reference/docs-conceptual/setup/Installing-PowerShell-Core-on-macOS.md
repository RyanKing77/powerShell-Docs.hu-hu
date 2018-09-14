---
title: A PowerShell Core telepítése macOS rendszerre
description: Információ a PowerShell Core telepítése macOS rendszeren
ms.date: 08/06/2018
ms.openlocfilehash: 50b8dbbf26f02580e4be45978c926d5337da6b63
ms.sourcegitcommit: b235c58b34d23317076540631f5cf83f1f309c0d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45557160"
---
# <a name="installing-powershell-core-on-macos"></a>A PowerShell Core telepítése macOS rendszerre

A PowerShell Core a macOS 10.12 és újabb verzióit támogatja.
A githubon érhető el az összes csomag [kiadások][] lapot.
A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.

### <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a>MacOS 10.12 vagy újabb rendszeren keresztül Homebrew kiadási legújabb előzetes verziójának telepítése

[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.
Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].

Miután telepítette a homebrew-val, a PowerShell telepítése ördöngösség.
Először telepítse [homebrew-val – Cask][cask], így további csomagok telepítése és telepítése [Cask-verziók] [cask-verzió], amely lehetővé teszi csomagok alternatív verzióját telepítse:

```sh
brew tap caskroom/cask
brew tap caskroom/versions
```

Most már PowerShell telepíthető:

```sh
brew cask install powershell-preview
```

Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:

```sh
pwsh-preview
```

PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez.
> és frissítse a $PSVersionTable látható értékeket.

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions

### <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a>MacOS 10.12 vagy újabb rendszeren keresztül Homebrew kiadási legújabb előzetes verziójának telepítése

[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.
Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].

Miután telepítette a homebrew-val, a PowerShell telepítése ördöngösség.
Először telepítse [homebrew-val – Cask][cask], így további csomagok telepítése és telepítése [Cask-verziók] [cask-verzió], amely lehetővé teszi csomagok alternatív verzióját telepítse:

```sh
brew tap caskroom/cask
brew tap caskroom/versions
```

Most már PowerShell telepíthető:

```sh
brew cask install powershell-preview
```

Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:

```sh
pwsh-preview
```

PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez.
> és frissítse a $PSVersionTable látható értékeket.

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions

### <a name="installation-via-direct-download"></a>Telepítési keresztül közvetlen letöltésére

A csomag-csomag letöltése `powershell-6.1.0-osx-x64.pkg`
az a [kiadások][] lap a macOS-számítógépre.

Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítheti a terminálról:

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

## <a name="binary-archives"></a>Bináris archívum

PowerShell bináris `tar.gz` archívumok biztosított macOS és Linux platformokat, a speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé.

### <a name="installing-binary-archives-on-macos"></a>MacOS rendszeren telepítése bináris archívum

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.1.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.1.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.1.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.1.0/pwsh /usr/local/bin/pwsh
```

## <a name="uninstalling-powershell-core"></a>A PowerShell Core eltávolítása

Ha a PowerShell telepítése a homebrew-val, az Eltávolítás ördöngösség:

```sh
brew cask uninstall powershell
```

Ha közvetlen letöltésére keresztül telepített, a PowerShell, PowerShell manuálisan kell eltávolítani:

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

Távolítsa el a további PowerShell-elérési utak, tekintse meg a [elérési utak][] szakaszt ebben a dokumentumban, és távolítsa el a kívánt az elérési utak használata `sudo rm`.

> [!NOTE]
> Ez nem szükséges, ha a telepítést a homebrew-val.

[Elérési utak]:#paths

## <a name="paths"></a>Elérési utak

* `$PSHOME` van `/usr/local/microsoft/powershell/6.1.0/`
* Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`
* Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`
* Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`
* Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`
* Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`
* PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

A profilok veszik figyelembe a PowerShell a gazdagép konfigurációja.
Az alapértelmezett gazdagép-specifikus profilok létezik így `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.

PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] macOS rendszeren.

Mivel a macOS BSD, az előtag típusából származtatott `/usr/local` helyett használja `/opt`.
Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.1.0/`, és a szimbolikus van elhelyezve `/usr/local/bin/pwsh`.

## <a name="additional-resources"></a>További források

* [Webes homebrew-val][brew]
* [Github-adattár homebrew-val][GitHub]
* [Homebrew-val – Cask][cask]

[brew]: http://brew.sh/
[GitHub]: https://github.com/Homebrew
[Cask]: https://github.com/Homebrew/homebrew-cask
[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
