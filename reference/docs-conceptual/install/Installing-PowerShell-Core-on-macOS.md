---
title: A PowerShell Core telepítése macOS rendszerre
description: Információ a PowerShell Core telepítése macOS rendszeren
ms.date: 12/12/2018
ms.openlocfilehash: 7db8ca0cb6d13db8ce7f11b4a4b03b7d3f9b6feb
ms.sourcegitcommit: 17ce42f97e13e8b3286779dc3f583474b0357023
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/18/2019
ms.locfileid: "59293401"
---
# <a name="installing-powershell-core-on-macos"></a>A PowerShell Core telepítése macOS rendszerre

A PowerShell Core a macOS 10.12 és újabb verzióit támogatja.
A githubon érhető el az összes csomag [kiadások][] lapot.
A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.

## <a name="about-brew"></a>Brew kapcsolatban

[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.
Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a>Legújabb stabil kiadási keresztül Homebrew MacOS 10.12 vagy újabb telepítése

Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.

Most már PowerShell telepíthető:

```sh
brew cask install powershell
```

Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:

```sh
pwsh
```

PowerShell új verzióinak kiadásakor frissítés a Homebrew-képlet, és a PowerShell frissítése:

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés látható értékeket `$PSVersionTable`.

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a>MacOS 10.12 vagy újabb rendszeren keresztül Homebrew kiadási legújabb előzetes verziójának telepítése

Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.

Ha már telepítette a homebrew-val, a PowerShell is telepítheti.
Először telepítse a [Cask-verziók] [ cask-versions] csomagot, amely lehetővé teszi a cask csomagok alternatív verzióját telepítse:

```sh
brew tap homebrew/cask-versions
```

Most már PowerShell telepíthető:

```sh
brew cask install powershell-preview
```

Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:

```sh
pwsh-preview
```

PowerShell új verzióinak kiadásakor frissítés a Homebrew-képlet, és a PowerShell frissítése:

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez.
> és látható értékeket frissítse `$PSVersionTable`.

## <a name="installation-via-direct-download"></a>Telepítési keresztül közvetlen letöltésére

A csomag-csomag letöltése `powershell-6.2.0-osx-x64.pkg`
az a [kiadások][] lap a macOS-számítógépre.

Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítheti a terminálról:

```sh
sudo installer -pkg powershell-6.2.0-osx-x64.pkg -target /
```

Telepítés [OpenSSL](#install-openssl). PowerShell távvezérlése és CIM-műveletek OpenSSL van szükség.

## <a name="binary-archives"></a>Bináris archívum

PowerShell bináris `tar.gz` archívumok biztosított speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé, a macOS platformon.

### <a name="installing-binary-archives-on-macos"></a>MacOS rendszeren telepítése bináris archívum

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.2.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.2.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.2.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.2.0/pwsh /usr/local/bin/pwsh
```

Telepítés [OpenSSL](#install-openssl). PowerShell távvezérlése és CIM-műveletek OpenSSL van szükség.

## <a name="installing-dependencies"></a>Függőségek telepítése

### <a name="install-xcode-command-line-tools"></a>Xcode-ban a parancssori eszközök telepítése

```sh
xcode-select --install
```

### <a name="install-openssl"></a>OpenSSL telepítése

PowerShell távvezérlése és CIM-műveletek OpenSSL van szükség. Telepíthet MacPorts vagy Brew keresztül.

#### <a name="install-openssl-via-brew"></a>OpenSSL keresztül Brew telepítése

Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.

OpenSSL telepítéséhez futtassa `brew install openssl`.

#### <a name="install-openssl-via-macports"></a>OpenSSL keresztül MacPorts telepítése

1. Telepítse a [xcode-ban a parancssori eszközök](#install-xcode-command-line-tools).
1. Telepítse a MacPorts.
   Ha utasításokat van szüksége, tekintse meg a [telepítési útmutató](https://guide.macports.org/chunked/installing.macports.html).
1. Frissítés MacPorts futtatásával `sudo port selfupdate`.
1. MacPorts csomagok frissítése futtatásával `sudo port upgrade outdated`.
1. Telepítse az OpenSSL futtatásával `sudo port install openssl`.
1. Hivatkozás a kódtárakat, hogy elérhetők legyenek a Powershellbe:

```sh
sudo mkdir -p /usr/local/opt/openssl
sudo ln -s /opt/local/lib /usr/local/opt/openssl/lib
```

## <a name="uninstalling-powershell-core"></a>A PowerShell Core eltávolítása

Ha a homebrew-val telepített PowerShell, a következő paranccsal távolíthatja el:

```sh
brew cask uninstall powershell
```

Ha közvetlen letöltésére keresztül telepített, a PowerShell, PowerShell manuálisan kell eltávolítani:

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

Távolítsa el a további PowerShell-elérési utak, tekintse meg a [elérési utak](#paths) című rész ebben a dokumentumban, és távolítsa el az elérési utak használata `sudo rm`.

> [!NOTE]
> Ez nem szükséges, ha a telepítést a homebrew-val.

## <a name="paths"></a>Elérési utak

* `$PSHOME` van `/usr/local/microsoft/powershell/6.2.0/`
* Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`
* Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`
* Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`
* Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`
* Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`
* PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

A profilok veszik figyelembe a PowerShell a gazdagép konfigurációja.
Az alapértelmezett gazdagép-specifikus profil létezik így `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.

PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] macOS rendszeren.

Mivel a macOS BSD, az előtag típusából származtatott `/usr/local` helyett használja `/opt`.
Tehát `$PSHOME` van `/usr/local/microsoft/powershell/6.2.0/`, és a szimbolikus hivatkozást van elhelyezve `/usr/local/bin/pwsh`.

## <a name="additional-resources"></a>Egyéb források

* [Webes homebrew-val][brew]
* [Github-adattár homebrew-val][GitHub]
* [Homebrew-Cask][cask]

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[Kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
