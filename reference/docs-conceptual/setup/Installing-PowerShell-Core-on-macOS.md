---
title: A PowerShell Core telepítése macOS rendszerre
description: Információ a PowerShell Core telepítése macOS rendszeren
ms.date: 08/06/2018
ms.openlocfilehash: 042c933dfa83f3ab52e315036e4f817145116d00
ms.sourcegitcommit: aa41249f153bbc6e11667ade60c878980c15abc6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/14/2018
ms.locfileid: "45611487"
---
# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="4cdef-103">A PowerShell Core telepítése macOS rendszerre</span><span class="sxs-lookup"><span data-stu-id="4cdef-103">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="4cdef-104">A PowerShell Core a macOS 10.12 és újabb verzióit támogatja.</span><span class="sxs-lookup"><span data-stu-id="4cdef-104">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="4cdef-105">A githubon érhető el az összes csomag [kiadások][] lapot.</span><span class="sxs-lookup"><span data-stu-id="4cdef-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="4cdef-106">A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="4cdef-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="4cdef-107">Legújabb stabil kiadási keresztül Homebrew MacOS 10.12 vagy újabb telepítése</span><span class="sxs-lookup"><span data-stu-id="4cdef-107">Installation of latest stable release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="4cdef-108">[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.</span><span class="sxs-lookup"><span data-stu-id="4cdef-108">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="4cdef-109">Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].</span><span class="sxs-lookup"><span data-stu-id="4cdef-109">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="4cdef-110">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="4cdef-110">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="4cdef-111">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="4cdef-111">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="4cdef-112">PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4cdef-112">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="4cdef-113">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="4cdef-113">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="4cdef-114">és frissítse a $PSVersionTable látható értékeket.</span><span class="sxs-lookup"><span data-stu-id="4cdef-114">and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="4cdef-115">MacOS 10.12 vagy újabb rendszeren keresztül Homebrew kiadási legújabb előzetes verziójának telepítése</span><span class="sxs-lookup"><span data-stu-id="4cdef-115">Installation of latest preview release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="4cdef-116">[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.</span><span class="sxs-lookup"><span data-stu-id="4cdef-116">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="4cdef-117">Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].</span><span class="sxs-lookup"><span data-stu-id="4cdef-117">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="4cdef-118">Miután telepítette a homebrew-val, a PowerShell telepítése ördöngösség.</span><span class="sxs-lookup"><span data-stu-id="4cdef-118">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="4cdef-119">Először telepítse [Cask-verziók] [ cask-versions] , amellyel alternatív verzióit a cask csomagok telepítéséhez:</span><span class="sxs-lookup"><span data-stu-id="4cdef-119">First, install [Cask-Versions][cask-versions] which lets you install alternative versions of cask packages:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="4cdef-120">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="4cdef-120">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="4cdef-121">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="4cdef-121">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="4cdef-122">PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4cdef-122">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="4cdef-123">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="4cdef-123">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="4cdef-124">és frissítse a $PSVersionTable látható értékeket.</span><span class="sxs-lookup"><span data-stu-id="4cdef-124">and refresh the values shown in $PSVersionTable.</span></span>

## <a name="installation-via-direct-download"></a><span data-ttu-id="4cdef-125">Telepítési keresztül közvetlen letöltésére</span><span class="sxs-lookup"><span data-stu-id="4cdef-125">Installation via Direct Download</span></span>

<span data-ttu-id="4cdef-126">A csomag-csomag letöltése `powershell-6.1.0-osx-x64.pkg`</span><span class="sxs-lookup"><span data-stu-id="4cdef-126">Download the PKG package `powershell-6.1.0-osx-x64.pkg`</span></span>
<span data-ttu-id="4cdef-127">az a [kiadások][] lap a macOS-számítógépre.</span><span class="sxs-lookup"><span data-stu-id="4cdef-127">from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="4cdef-128">Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítheti a terminálról:</span><span class="sxs-lookup"><span data-stu-id="4cdef-128">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="4cdef-129">Bináris archívum</span><span class="sxs-lookup"><span data-stu-id="4cdef-129">Binary Archives</span></span>

<span data-ttu-id="4cdef-130">PowerShell bináris `tar.gz` archívumok biztosított speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé, a macOS platformon.</span><span class="sxs-lookup"><span data-stu-id="4cdef-130">PowerShell binary `tar.gz` archives are provided for the macOS platform to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="4cdef-131">MacOS rendszeren telepítése bináris archívum</span><span class="sxs-lookup"><span data-stu-id="4cdef-131">Installing binary archives on macOS</span></span>

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

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="4cdef-132">A PowerShell Core eltávolítása</span><span class="sxs-lookup"><span data-stu-id="4cdef-132">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="4cdef-133">Ha a PowerShell telepítése a homebrew-val, az Eltávolítás ördöngösség:</span><span class="sxs-lookup"><span data-stu-id="4cdef-133">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="4cdef-134">Ha közvetlen letöltésére keresztül telepített, a PowerShell, PowerShell manuálisan kell eltávolítani:</span><span class="sxs-lookup"><span data-stu-id="4cdef-134">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="4cdef-135">Távolítsa el a további PowerShell-elérési utak, tekintse meg a [elérési utak](#paths) szakaszt ebben a dokumentumban, és távolítsa el a kívánt az elérési utak használata `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="4cdef-135">To remove the additional PowerShell paths, please see the [paths](#paths) section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="4cdef-136">Ez nem szükséges, ha a telepítést a homebrew-val.</span><span class="sxs-lookup"><span data-stu-id="4cdef-136">This is not necessary if you installed with Homebrew.</span></span>

## <a name="paths"></a><span data-ttu-id="4cdef-137">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="4cdef-137">Paths</span></span>

* <span data-ttu-id="4cdef-138">`$PSHOME` van `/usr/local/microsoft/powershell/6.1.0/`</span><span class="sxs-lookup"><span data-stu-id="4cdef-138">`$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`</span></span>
* <span data-ttu-id="4cdef-139">Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="4cdef-139">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="4cdef-140">Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="4cdef-140">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="4cdef-141">Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="4cdef-141">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="4cdef-142">Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="4cdef-142">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="4cdef-143">Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="4cdef-143">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="4cdef-144">PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="4cdef-144">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="4cdef-145">A profilok veszik figyelembe a PowerShell a gazdagép konfigurációja.</span><span class="sxs-lookup"><span data-stu-id="4cdef-145">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="4cdef-146">Az alapértelmezett gazdagép-specifikus profilok létezik így `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="4cdef-146">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="4cdef-147">PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] macOS rendszeren.</span><span class="sxs-lookup"><span data-stu-id="4cdef-147">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="4cdef-148">Mivel a macOS BSD, az előtag típusából származtatott `/usr/local` helyett használja `/opt`.</span><span class="sxs-lookup"><span data-stu-id="4cdef-148">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="4cdef-149">Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.1.0/`, és a szimbolikus van elhelyezve `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="4cdef-149">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4cdef-150">További források</span><span class="sxs-lookup"><span data-stu-id="4cdef-150">Additional Resources</span></span>

* <span data-ttu-id="4cdef-151">[Webes homebrew-val][brew]</span><span class="sxs-lookup"><span data-stu-id="4cdef-151">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="4cdef-152">[Github-adattár homebrew-val][GitHub]</span><span class="sxs-lookup"><span data-stu-id="4cdef-152">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="4cdef-153">[Homebrew-val – Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="4cdef-153">[Homebrew-Cask][cask]</span></span>

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
