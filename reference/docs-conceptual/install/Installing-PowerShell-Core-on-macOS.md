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
# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="f5c0a-103">A PowerShell Core telepítése macOS rendszerre</span><span class="sxs-lookup"><span data-stu-id="f5c0a-103">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="f5c0a-104">A PowerShell Core a macOS 10.12 és újabb verzióit támogatja.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-104">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="f5c0a-105">A githubon érhető el az összes csomag [kiadások][] lapot.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="f5c0a-106">A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-106">After the package is installed, run `pwsh` from a terminal.</span></span>

## <a name="about-brew"></a><span data-ttu-id="f5c0a-107">Brew kapcsolatban</span><span class="sxs-lookup"><span data-stu-id="f5c0a-107">About Brew</span></span>

<span data-ttu-id="f5c0a-108">[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-108">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="f5c0a-109">Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].</span><span class="sxs-lookup"><span data-stu-id="f5c0a-109">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="f5c0a-110">Legújabb stabil kiadási keresztül Homebrew MacOS 10.12 vagy újabb telepítése</span><span class="sxs-lookup"><span data-stu-id="f5c0a-110">Installation of latest stable release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="f5c0a-111">Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-111">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="f5c0a-112">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="f5c0a-112">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="f5c0a-113">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="f5c0a-113">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="f5c0a-114">PowerShell új verzióinak kiadásakor frissítés a Homebrew-képlet, és a PowerShell frissítése:</span><span class="sxs-lookup"><span data-stu-id="f5c0a-114">When new versions of PowerShell are released, update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="f5c0a-115">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés látható értékeket `$PSVersionTable`.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-115">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in `$PSVersionTable`.</span></span>

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="f5c0a-116">MacOS 10.12 vagy újabb rendszeren keresztül Homebrew kiadási legújabb előzetes verziójának telepítése</span><span class="sxs-lookup"><span data-stu-id="f5c0a-116">Installation of latest preview release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="f5c0a-117">Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-117">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="f5c0a-118">Ha már telepítette a homebrew-val, a PowerShell is telepítheti.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-118">After you've installed Homebrew, you can install PowerShell.</span></span>
<span data-ttu-id="f5c0a-119">Először telepítse a [Cask-verziók] [ cask-versions] csomagot, amely lehetővé teszi a cask csomagok alternatív verzióját telepítse:</span><span class="sxs-lookup"><span data-stu-id="f5c0a-119">First, install the [Cask-Versions][cask-versions] package that lets you install alternative versions of cask packages:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="f5c0a-120">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="f5c0a-120">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="f5c0a-121">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="f5c0a-121">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="f5c0a-122">PowerShell új verzióinak kiadásakor frissítés a Homebrew-képlet, és a PowerShell frissítése:</span><span class="sxs-lookup"><span data-stu-id="f5c0a-122">When new versions of PowerShell are released, update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="f5c0a-123">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-123">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="f5c0a-124">és látható értékeket frissítse `$PSVersionTable`.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-124">and refresh the values shown in `$PSVersionTable`.</span></span>

## <a name="installation-via-direct-download"></a><span data-ttu-id="f5c0a-125">Telepítési keresztül közvetlen letöltésére</span><span class="sxs-lookup"><span data-stu-id="f5c0a-125">Installation via Direct Download</span></span>

<span data-ttu-id="f5c0a-126">A csomag-csomag letöltése `powershell-6.2.0-osx-x64.pkg`</span><span class="sxs-lookup"><span data-stu-id="f5c0a-126">Download the PKG package `powershell-6.2.0-osx-x64.pkg`</span></span>
<span data-ttu-id="f5c0a-127">az a [kiadások][] lap a macOS-számítógépre.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-127">from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="f5c0a-128">Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítheti a terminálról:</span><span class="sxs-lookup"><span data-stu-id="f5c0a-128">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.2.0-osx-x64.pkg -target /
```

<span data-ttu-id="f5c0a-129">Telepítés [OpenSSL](#install-openssl).</span><span class="sxs-lookup"><span data-stu-id="f5c0a-129">Install [OpenSSL](#install-openssl).</span></span> <span data-ttu-id="f5c0a-130">PowerShell távvezérlése és CIM-műveletek OpenSSL van szükség.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-130">OpenSSL is needed for PowerShell remoting and CIM operations.</span></span>

## <a name="binary-archives"></a><span data-ttu-id="f5c0a-131">Bináris archívum</span><span class="sxs-lookup"><span data-stu-id="f5c0a-131">Binary Archives</span></span>

<span data-ttu-id="f5c0a-132">PowerShell bináris `tar.gz` archívumok biztosított speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé, a macOS platformon.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-132">PowerShell binary `tar.gz` archives are provided for the macOS platform to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="f5c0a-133">MacOS rendszeren telepítése bináris archívum</span><span class="sxs-lookup"><span data-stu-id="f5c0a-133">Installing binary archives on macOS</span></span>

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

<span data-ttu-id="f5c0a-134">Telepítés [OpenSSL](#install-openssl).</span><span class="sxs-lookup"><span data-stu-id="f5c0a-134">Install [OpenSSL](#install-openssl).</span></span> <span data-ttu-id="f5c0a-135">PowerShell távvezérlése és CIM-műveletek OpenSSL van szükség.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-135">OpenSSL is needed for PowerShell remoting and CIM operations.</span></span>

## <a name="installing-dependencies"></a><span data-ttu-id="f5c0a-136">Függőségek telepítése</span><span class="sxs-lookup"><span data-stu-id="f5c0a-136">Installing dependencies</span></span>

### <a name="install-xcode-command-line-tools"></a><span data-ttu-id="f5c0a-137">Xcode-ban a parancssori eszközök telepítése</span><span class="sxs-lookup"><span data-stu-id="f5c0a-137">Install XCode command-line tools</span></span>

```sh
xcode-select --install
```

### <a name="install-openssl"></a><span data-ttu-id="f5c0a-138">OpenSSL telepítése</span><span class="sxs-lookup"><span data-stu-id="f5c0a-138">Install OpenSSL</span></span>

<span data-ttu-id="f5c0a-139">PowerShell távvezérlése és CIM-műveletek OpenSSL van szükség.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-139">OpenSSL is needed for PowerShell remoting and CIM operations.</span></span> <span data-ttu-id="f5c0a-140">Telepíthet MacPorts vagy Brew keresztül.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-140">You can install via MacPorts or Brew.</span></span>

#### <a name="install-openssl-via-brew"></a><span data-ttu-id="f5c0a-141">OpenSSL keresztül Brew telepítése</span><span class="sxs-lookup"><span data-stu-id="f5c0a-141">Install OpenSSL via Brew</span></span>

<span data-ttu-id="f5c0a-142">Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-142">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="f5c0a-143">OpenSSL telepítéséhez futtassa `brew install openssl`.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-143">To install OpenSSL, run `brew install openssl`.</span></span>

#### <a name="install-openssl-via-macports"></a><span data-ttu-id="f5c0a-144">OpenSSL keresztül MacPorts telepítése</span><span class="sxs-lookup"><span data-stu-id="f5c0a-144">Install OpenSSL via MacPorts</span></span>

1. <span data-ttu-id="f5c0a-145">Telepítse a [xcode-ban a parancssori eszközök](#install-xcode-command-line-tools).</span><span class="sxs-lookup"><span data-stu-id="f5c0a-145">Install the [XCode command line tools](#install-xcode-command-line-tools).</span></span>
1. <span data-ttu-id="f5c0a-146">Telepítse a MacPorts.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-146">Install MacPorts.</span></span>
   <span data-ttu-id="f5c0a-147">Ha utasításokat van szüksége, tekintse meg a [telepítési útmutató](https://guide.macports.org/chunked/installing.macports.html).</span><span class="sxs-lookup"><span data-stu-id="f5c0a-147">If you need instructions, refer to the [installation guide](https://guide.macports.org/chunked/installing.macports.html).</span></span>
1. <span data-ttu-id="f5c0a-148">Frissítés MacPorts futtatásával `sudo port selfupdate`.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-148">Update MacPorts by running `sudo port selfupdate`.</span></span>
1. <span data-ttu-id="f5c0a-149">MacPorts csomagok frissítése futtatásával `sudo port upgrade outdated`.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-149">Upgrade MacPorts packages by running `sudo port upgrade outdated`.</span></span>
1. <span data-ttu-id="f5c0a-150">Telepítse az OpenSSL futtatásával `sudo port install openssl`.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-150">Install OpenSSL by running `sudo port install openssl`.</span></span>
1. <span data-ttu-id="f5c0a-151">Hivatkozás a kódtárakat, hogy elérhetők legyenek a Powershellbe:</span><span class="sxs-lookup"><span data-stu-id="f5c0a-151">Link the libraries to make them available to PowerShell:</span></span>

```sh
sudo mkdir -p /usr/local/opt/openssl
sudo ln -s /opt/local/lib /usr/local/opt/openssl/lib
```

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="f5c0a-152">A PowerShell Core eltávolítása</span><span class="sxs-lookup"><span data-stu-id="f5c0a-152">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="f5c0a-153">Ha a homebrew-val telepített PowerShell, a következő paranccsal távolíthatja el:</span><span class="sxs-lookup"><span data-stu-id="f5c0a-153">If you installed PowerShell with Homebrew, use the following command to uninstall:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="f5c0a-154">Ha közvetlen letöltésére keresztül telepített, a PowerShell, PowerShell manuálisan kell eltávolítani:</span><span class="sxs-lookup"><span data-stu-id="f5c0a-154">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="f5c0a-155">Távolítsa el a további PowerShell-elérési utak, tekintse meg a [elérési utak](#paths) című rész ebben a dokumentumban, és távolítsa el az elérési utak használata `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-155">To remove the additional PowerShell paths, refer to the [paths](#paths) section in this document and remove the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="f5c0a-156">Ez nem szükséges, ha a telepítést a homebrew-val.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-156">This is not necessary if you installed with Homebrew.</span></span>

## <a name="paths"></a><span data-ttu-id="f5c0a-157">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="f5c0a-157">Paths</span></span>

* <span data-ttu-id="f5c0a-158">`$PSHOME` van `/usr/local/microsoft/powershell/6.2.0/`</span><span class="sxs-lookup"><span data-stu-id="f5c0a-158">`$PSHOME` is `/usr/local/microsoft/powershell/6.2.0/`</span></span>
* <span data-ttu-id="f5c0a-159">Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="f5c0a-159">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="f5c0a-160">Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="f5c0a-160">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="f5c0a-161">Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="f5c0a-161">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="f5c0a-162">Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="f5c0a-162">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="f5c0a-163">Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="f5c0a-163">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="f5c0a-164">PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="f5c0a-164">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="f5c0a-165">A profilok veszik figyelembe a PowerShell a gazdagép konfigurációja.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-165">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="f5c0a-166">Az alapértelmezett gazdagép-specifikus profil létezik így `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-166">So the default host-specific profile exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="f5c0a-167">PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] macOS rendszeren.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-167">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="f5c0a-168">Mivel a macOS BSD, az előtag típusából származtatott `/usr/local` helyett használja `/opt`.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-168">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="f5c0a-169">Tehát `$PSHOME` van `/usr/local/microsoft/powershell/6.2.0/`, és a szimbolikus hivatkozást van elhelyezve `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="f5c0a-169">So, `$PSHOME` is `/usr/local/microsoft/powershell/6.2.0/`, and the symbolic link is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f5c0a-170">Egyéb források</span><span class="sxs-lookup"><span data-stu-id="f5c0a-170">Additional Resources</span></span>

* <span data-ttu-id="f5c0a-171">[Webes homebrew-val][brew]</span><span class="sxs-lookup"><span data-stu-id="f5c0a-171">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="f5c0a-172">[Github-adattár homebrew-val][GitHub]</span><span class="sxs-lookup"><span data-stu-id="f5c0a-172">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="f5c0a-173">[Homebrew-Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="f5c0a-173">[Homebrew-Cask][cask]</span></span>

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[Kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
