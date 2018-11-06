---
title: A PowerShell Core telepítése macOS rendszerre
description: Információ a PowerShell Core telepítése macOS rendszeren
ms.date: 11/02/2018
ms.openlocfilehash: 162e841bf71d708e9db84ea1bb2dbef13924783b
ms.sourcegitcommit: f4247d3f91d06ec392c4cd66921ce7d0456a2bd9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/05/2018
ms.locfileid: "50998503"
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

PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés $PSVersionTable látható értékeket.

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a>MacOS 10.12 vagy újabb rendszeren keresztül Homebrew kiadási legújabb előzetes verziójának telepítése

Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.

Miután telepítette a homebrew-val, a PowerShell telepítése ördöngösség.
Először telepítse [Cask-verziók] [ cask-versions] , amellyel alternatív verzióit a cask csomagok telepítéséhez:

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

PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez.
> és frissítse a $PSVersionTable látható értékeket.

## <a name="installation-via-direct-download"></a>Telepítési keresztül közvetlen letöltésére

A csomag-csomag letöltése `powershell-6.1.0-osx-x64.pkg`
az a [kiadások][] lap a macOS-számítógépre.

Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítheti a terminálról:

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

Telepítés [OpenSSL](#install-openssl) , erre azért van szükség a PowerShell távvezérlése és CIM-műveleteket.

## <a name="binary-archives"></a>Bináris archívum

PowerShell bináris `tar.gz` archívumok biztosított speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé, a macOS platformon.

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

Telepítés [OpenSSL](#install-openssl) , erre azért van szükség a PowerShell távvezérlése és CIM-műveleteket.

## <a name="installing-dependencies"></a>Függőségek telepítése

### <a name="install-xcode-command-line-tools"></a>Telepítse az xcode-ban a parancssori eszközök

```shell
xcode-select -install
```

### <a name="install-openssl"></a>OpenSSL telepítése

PowerShell távvezérlése és CIM-műveletek OpenSSL van szükség.  Telepíthet MacPorts vagy Brew keresztül.

#### <a name="install-openssl-via-brew"></a>OpenSSL keresztül Brew telepítése

Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.

Futtatás `brew install openssl` OpenSSL telepítéséhez.

#### <a name="install-openssl-via-macports"></a>OpenSSL keresztül MacPorts telepítése

1. Telepít a [xcode-ban a parancssori eszközök](#install-xcode-command-line-tools)
1. Telepítse a MacPorts.
   Tekintse meg a [telepítési útmutató](https://guide.macports.org/chunked/installing.macports.html) Ha utasításokat kell.
1. A futó MacPorts frissítése `sudo port selfupdate`
1. A futó MacPorts csomagok frissítése `sudo port upgrade outdated`
1. OpenSSL futtatásával futtatásával telepítse: `sudo port instal openssl`
1. Hivatkozás a kódtárakat, így PowerShell használhatják azt.

```shell
sudo mkdir -p /usr/local/opt/openssl
sudo ln -s /opt/local/lib /usr/local/opt/openssl/lib
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

Távolítsa el a további PowerShell-elérési utak, tekintse meg a [elérési utak](#paths) szakaszt ebben a dokumentumban, és távolítsa el a kívánt az elérési utak használata `sudo rm`.

> [!NOTE]
> Ez nem szükséges, ha a telepítést a homebrew-val.

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
Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.1.0/`, és a szimbolikus hivatkozást van elhelyezve `/usr/local/bin/pwsh`.

## <a name="additional-resources"></a>További források

* [Webes homebrew-val][brew]
* [Github-adattár homebrew-val][GitHub]
* [Homebrew-val – Cask][cask]

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
