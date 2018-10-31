---
title: A PowerShell Core telepítése macOS rendszerre
description: Információ a PowerShell Core telepítése macOS rendszeren
ms.date: 08/06/2018
ms.openlocfilehash: e226cd64f8788ae74dc72fdc0cd219923b7a2cd6
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002359"
---
# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="b9d54-103">A PowerShell Core telepítése macOS rendszerre</span><span class="sxs-lookup"><span data-stu-id="b9d54-103">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="b9d54-104">A PowerShell Core a macOS 10.12 és újabb verzióit támogatja.</span><span class="sxs-lookup"><span data-stu-id="b9d54-104">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="b9d54-105">A githubon érhető el az összes csomag [kiadások][] lapot.</span><span class="sxs-lookup"><span data-stu-id="b9d54-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="b9d54-106">A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="b9d54-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="b9d54-107">Legújabb stabil kiadási keresztül Homebrew MacOS 10.12 vagy újabb telepítése</span><span class="sxs-lookup"><span data-stu-id="b9d54-107">Installation of latest stable release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="b9d54-108">[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.</span><span class="sxs-lookup"><span data-stu-id="b9d54-108">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="b9d54-109">Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].</span><span class="sxs-lookup"><span data-stu-id="b9d54-109">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="b9d54-110">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="b9d54-110">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="b9d54-111">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="b9d54-111">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="b9d54-112">PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b9d54-112">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="b9d54-113">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés $PSVersionTable látható értékeket.</span><span class="sxs-lookup"><span data-stu-id="b9d54-113">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="b9d54-114">MacOS 10.12 vagy újabb rendszeren keresztül Homebrew kiadási legújabb előzetes verziójának telepítése</span><span class="sxs-lookup"><span data-stu-id="b9d54-114">Installation of latest preview release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="b9d54-115">[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.</span><span class="sxs-lookup"><span data-stu-id="b9d54-115">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="b9d54-116">Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].</span><span class="sxs-lookup"><span data-stu-id="b9d54-116">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="b9d54-117">Miután telepítette a homebrew-val, a PowerShell telepítése ördöngösség.</span><span class="sxs-lookup"><span data-stu-id="b9d54-117">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="b9d54-118">Először telepítse [Cask-verziók] [ cask-versions] , amellyel alternatív verzióit a cask csomagok telepítéséhez:</span><span class="sxs-lookup"><span data-stu-id="b9d54-118">First, install [Cask-Versions][cask-versions] which lets you install alternative versions of cask packages:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="b9d54-119">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="b9d54-119">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="b9d54-120">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="b9d54-120">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="b9d54-121">PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b9d54-121">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="b9d54-122">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="b9d54-122">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="b9d54-123">és frissítse a $PSVersionTable látható értékeket.</span><span class="sxs-lookup"><span data-stu-id="b9d54-123">and refresh the values shown in $PSVersionTable.</span></span>

## <a name="installation-via-direct-download"></a><span data-ttu-id="b9d54-124">Telepítési keresztül közvetlen letöltésére</span><span class="sxs-lookup"><span data-stu-id="b9d54-124">Installation via Direct Download</span></span>

<span data-ttu-id="b9d54-125">A csomag-csomag letöltése `powershell-6.1.0-osx-x64.pkg`</span><span class="sxs-lookup"><span data-stu-id="b9d54-125">Download the PKG package `powershell-6.1.0-osx-x64.pkg`</span></span>
<span data-ttu-id="b9d54-126">az a [kiadások][] lap a macOS-számítógépre.</span><span class="sxs-lookup"><span data-stu-id="b9d54-126">from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="b9d54-127">Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítheti a terminálról:</span><span class="sxs-lookup"><span data-stu-id="b9d54-127">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="b9d54-128">Bináris archívum</span><span class="sxs-lookup"><span data-stu-id="b9d54-128">Binary Archives</span></span>

<span data-ttu-id="b9d54-129">PowerShell bináris `tar.gz` archívumok biztosított speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé, a macOS platformon.</span><span class="sxs-lookup"><span data-stu-id="b9d54-129">PowerShell binary `tar.gz` archives are provided for the macOS platform to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="b9d54-130">MacOS rendszeren telepítése bináris archívum</span><span class="sxs-lookup"><span data-stu-id="b9d54-130">Installing binary archives on macOS</span></span>

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

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="b9d54-131">A PowerShell Core eltávolítása</span><span class="sxs-lookup"><span data-stu-id="b9d54-131">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="b9d54-132">Ha a PowerShell telepítése a homebrew-val, az Eltávolítás ördöngösség:</span><span class="sxs-lookup"><span data-stu-id="b9d54-132">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="b9d54-133">Ha közvetlen letöltésére keresztül telepített, a PowerShell, PowerShell manuálisan kell eltávolítani:</span><span class="sxs-lookup"><span data-stu-id="b9d54-133">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="b9d54-134">Távolítsa el a további PowerShell-elérési utak, tekintse meg a [elérési utak](#paths) szakaszt ebben a dokumentumban, és távolítsa el a kívánt az elérési utak használata `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="b9d54-134">To remove the additional PowerShell paths, please see the [paths](#paths) section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="b9d54-135">Ez nem szükséges, ha a telepítést a homebrew-val.</span><span class="sxs-lookup"><span data-stu-id="b9d54-135">This is not necessary if you installed with Homebrew.</span></span>

## <a name="paths"></a><span data-ttu-id="b9d54-136">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="b9d54-136">Paths</span></span>

* <span data-ttu-id="b9d54-137">`$PSHOME` van `/usr/local/microsoft/powershell/6.1.0/`</span><span class="sxs-lookup"><span data-stu-id="b9d54-137">`$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`</span></span>
* <span data-ttu-id="b9d54-138">Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="b9d54-138">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="b9d54-139">Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="b9d54-139">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="b9d54-140">Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="b9d54-140">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="b9d54-141">Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="b9d54-141">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="b9d54-142">Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="b9d54-142">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="b9d54-143">PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="b9d54-143">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="b9d54-144">A profilok veszik figyelembe a PowerShell a gazdagép konfigurációja.</span><span class="sxs-lookup"><span data-stu-id="b9d54-144">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="b9d54-145">Az alapértelmezett gazdagép-specifikus profilok létezik így `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="b9d54-145">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="b9d54-146">PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] macOS rendszeren.</span><span class="sxs-lookup"><span data-stu-id="b9d54-146">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="b9d54-147">Mivel a macOS BSD, az előtag típusából származtatott `/usr/local` helyett használja `/opt`.</span><span class="sxs-lookup"><span data-stu-id="b9d54-147">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="b9d54-148">Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.1.0/`, és a szimbolikus van elhelyezve `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="b9d54-148">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9d54-149">További források</span><span class="sxs-lookup"><span data-stu-id="b9d54-149">Additional Resources</span></span>

* <span data-ttu-id="b9d54-150">[Webes homebrew-val][brew]</span><span class="sxs-lookup"><span data-stu-id="b9d54-150">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="b9d54-151">[Github-adattár homebrew-val][GitHub]</span><span class="sxs-lookup"><span data-stu-id="b9d54-151">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="b9d54-152">[Homebrew-val – Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="b9d54-152">[Homebrew-Cask][cask]</span></span>

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
