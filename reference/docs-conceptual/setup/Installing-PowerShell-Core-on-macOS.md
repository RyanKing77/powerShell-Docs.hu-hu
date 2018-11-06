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
# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="3654f-103">A PowerShell Core telepítése macOS rendszerre</span><span class="sxs-lookup"><span data-stu-id="3654f-103">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="3654f-104">A PowerShell Core a macOS 10.12 és újabb verzióit támogatja.</span><span class="sxs-lookup"><span data-stu-id="3654f-104">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="3654f-105">A githubon érhető el az összes csomag [kiadások][] lapot.</span><span class="sxs-lookup"><span data-stu-id="3654f-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="3654f-106">A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="3654f-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

## <a name="about-brew"></a><span data-ttu-id="3654f-107">Brew kapcsolatban</span><span class="sxs-lookup"><span data-stu-id="3654f-107">About Brew</span></span>

<span data-ttu-id="3654f-108">[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.</span><span class="sxs-lookup"><span data-stu-id="3654f-108">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="3654f-109">Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].</span><span class="sxs-lookup"><span data-stu-id="3654f-109">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="3654f-110">Legújabb stabil kiadási keresztül Homebrew MacOS 10.12 vagy újabb telepítése</span><span class="sxs-lookup"><span data-stu-id="3654f-110">Installation of latest stable release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="3654f-111">Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="3654f-111">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="3654f-112">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="3654f-112">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="3654f-113">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="3654f-113">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="3654f-114">PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3654f-114">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="3654f-115">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés $PSVersionTable látható értékeket.</span><span class="sxs-lookup"><span data-stu-id="3654f-115">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="3654f-116">MacOS 10.12 vagy újabb rendszeren keresztül Homebrew kiadási legújabb előzetes verziójának telepítése</span><span class="sxs-lookup"><span data-stu-id="3654f-116">Installation of latest preview release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="3654f-117">Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="3654f-117">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="3654f-118">Miután telepítette a homebrew-val, a PowerShell telepítése ördöngösség.</span><span class="sxs-lookup"><span data-stu-id="3654f-118">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="3654f-119">Először telepítse [Cask-verziók] [ cask-versions] , amellyel alternatív verzióit a cask csomagok telepítéséhez:</span><span class="sxs-lookup"><span data-stu-id="3654f-119">First, install [Cask-Versions][cask-versions] which lets you install alternative versions of cask packages:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="3654f-120">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="3654f-120">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="3654f-121">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="3654f-121">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="3654f-122">PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3654f-122">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="3654f-123">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="3654f-123">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="3654f-124">és frissítse a $PSVersionTable látható értékeket.</span><span class="sxs-lookup"><span data-stu-id="3654f-124">and refresh the values shown in $PSVersionTable.</span></span>

## <a name="installation-via-direct-download"></a><span data-ttu-id="3654f-125">Telepítési keresztül közvetlen letöltésére</span><span class="sxs-lookup"><span data-stu-id="3654f-125">Installation via Direct Download</span></span>

<span data-ttu-id="3654f-126">A csomag-csomag letöltése `powershell-6.1.0-osx-x64.pkg`</span><span class="sxs-lookup"><span data-stu-id="3654f-126">Download the PKG package `powershell-6.1.0-osx-x64.pkg`</span></span>
<span data-ttu-id="3654f-127">az a [kiadások][] lap a macOS-számítógépre.</span><span class="sxs-lookup"><span data-stu-id="3654f-127">from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="3654f-128">Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítheti a terminálról:</span><span class="sxs-lookup"><span data-stu-id="3654f-128">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.1.0-osx-x64.pkg -target /
```

<span data-ttu-id="3654f-129">Telepítés [OpenSSL](#install-openssl) , erre azért van szükség a PowerShell távvezérlése és CIM-műveleteket.</span><span class="sxs-lookup"><span data-stu-id="3654f-129">Install [OpenSSL](#install-openssl) as this is needed for PowerShell remoting and CIM operations.</span></span>

## <a name="binary-archives"></a><span data-ttu-id="3654f-130">Bináris archívum</span><span class="sxs-lookup"><span data-stu-id="3654f-130">Binary Archives</span></span>

<span data-ttu-id="3654f-131">PowerShell bináris `tar.gz` archívumok biztosított speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé, a macOS platformon.</span><span class="sxs-lookup"><span data-stu-id="3654f-131">PowerShell binary `tar.gz` archives are provided for the macOS platform to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="3654f-132">MacOS rendszeren telepítése bináris archívum</span><span class="sxs-lookup"><span data-stu-id="3654f-132">Installing binary archives on macOS</span></span>

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

<span data-ttu-id="3654f-133">Telepítés [OpenSSL](#install-openssl) , erre azért van szükség a PowerShell távvezérlése és CIM-műveleteket.</span><span class="sxs-lookup"><span data-stu-id="3654f-133">Install [OpenSSL](#install-openssl) as this is needed for PowerShell remoting and CIM operations.</span></span>

## <a name="installing-dependencies"></a><span data-ttu-id="3654f-134">Függőségek telepítése</span><span class="sxs-lookup"><span data-stu-id="3654f-134">Installing dependencies</span></span>

### <a name="install-xcode-command-line-tools"></a><span data-ttu-id="3654f-135">Telepítse az xcode-ban a parancssori eszközök</span><span class="sxs-lookup"><span data-stu-id="3654f-135">Install XCode command line tools</span></span>

```shell
xcode-select -install
```

### <a name="install-openssl"></a><span data-ttu-id="3654f-136">OpenSSL telepítése</span><span class="sxs-lookup"><span data-stu-id="3654f-136">Install OpenSSL</span></span>

<span data-ttu-id="3654f-137">PowerShell távvezérlése és CIM-műveletek OpenSSL van szükség.</span><span class="sxs-lookup"><span data-stu-id="3654f-137">OpenSSL is needed for PowerShell remoting and CIM operations.</span></span>  <span data-ttu-id="3654f-138">Telepíthet MacPorts vagy Brew keresztül.</span><span class="sxs-lookup"><span data-stu-id="3654f-138">You can install via MacPorts or Brew.</span></span>

#### <a name="install-openssl-via-brew"></a><span data-ttu-id="3654f-139">OpenSSL keresztül Brew telepítése</span><span class="sxs-lookup"><span data-stu-id="3654f-139">Install OpenSSL via Brew</span></span>

<span data-ttu-id="3654f-140">Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="3654f-140">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="3654f-141">Futtatás `brew install openssl` OpenSSL telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="3654f-141">Run `brew install openssl` to install OpenSSL.</span></span>

#### <a name="install-openssl-via-macports"></a><span data-ttu-id="3654f-142">OpenSSL keresztül MacPorts telepítése</span><span class="sxs-lookup"><span data-stu-id="3654f-142">Install OpenSSL via MacPorts</span></span>

1. <span data-ttu-id="3654f-143">Telepít a [xcode-ban a parancssori eszközök](#install-xcode-command-line-tools)</span><span class="sxs-lookup"><span data-stu-id="3654f-143">Instal the [XCode command line tools](#install-xcode-command-line-tools)</span></span>
1. <span data-ttu-id="3654f-144">Telepítse a MacPorts.</span><span class="sxs-lookup"><span data-stu-id="3654f-144">Install MacPorts.</span></span>
   <span data-ttu-id="3654f-145">Tekintse meg a [telepítési útmutató](https://guide.macports.org/chunked/installing.macports.html) Ha utasításokat kell.</span><span class="sxs-lookup"><span data-stu-id="3654f-145">See the [installation guide](https://guide.macports.org/chunked/installing.macports.html) if you need instructions.</span></span>
1. <span data-ttu-id="3654f-146">A futó MacPorts frissítése `sudo port selfupdate`</span><span class="sxs-lookup"><span data-stu-id="3654f-146">Update MacPorts by running `sudo port selfupdate`</span></span>
1. <span data-ttu-id="3654f-147">A futó MacPorts csomagok frissítése `sudo port upgrade outdated`</span><span class="sxs-lookup"><span data-stu-id="3654f-147">Upgrade MacPorts packages by running `sudo port upgrade outdated`</span></span>
1. <span data-ttu-id="3654f-148">OpenSSL futtatásával futtatásával telepítse: `sudo port instal openssl`</span><span class="sxs-lookup"><span data-stu-id="3654f-148">Install OpenSSL by running by running `sudo port instal openssl`</span></span>
1. <span data-ttu-id="3654f-149">Hivatkozás a kódtárakat, így PowerShell használhatják azt.</span><span class="sxs-lookup"><span data-stu-id="3654f-149">Link the libraries so that PowerShell can use it.</span></span>

```shell
sudo mkdir -p /usr/local/opt/openssl
sudo ln -s /opt/local/lib /usr/local/opt/openssl/lib
```

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="3654f-150">A PowerShell Core eltávolítása</span><span class="sxs-lookup"><span data-stu-id="3654f-150">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="3654f-151">Ha a PowerShell telepítése a homebrew-val, az Eltávolítás ördöngösség:</span><span class="sxs-lookup"><span data-stu-id="3654f-151">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="3654f-152">Ha közvetlen letöltésére keresztül telepített, a PowerShell, PowerShell manuálisan kell eltávolítani:</span><span class="sxs-lookup"><span data-stu-id="3654f-152">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="3654f-153">Távolítsa el a további PowerShell-elérési utak, tekintse meg a [elérési utak](#paths) szakaszt ebben a dokumentumban, és távolítsa el a kívánt az elérési utak használata `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="3654f-153">To remove the additional PowerShell paths, please see the [paths](#paths) section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="3654f-154">Ez nem szükséges, ha a telepítést a homebrew-val.</span><span class="sxs-lookup"><span data-stu-id="3654f-154">This is not necessary if you installed with Homebrew.</span></span>

## <a name="paths"></a><span data-ttu-id="3654f-155">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="3654f-155">Paths</span></span>

* <span data-ttu-id="3654f-156">`$PSHOME` van `/usr/local/microsoft/powershell/6.1.0/`</span><span class="sxs-lookup"><span data-stu-id="3654f-156">`$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`</span></span>
* <span data-ttu-id="3654f-157">Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="3654f-157">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="3654f-158">Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="3654f-158">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="3654f-159">Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="3654f-159">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="3654f-160">Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="3654f-160">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="3654f-161">Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="3654f-161">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="3654f-162">PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="3654f-162">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="3654f-163">A profilok veszik figyelembe a PowerShell a gazdagép konfigurációja.</span><span class="sxs-lookup"><span data-stu-id="3654f-163">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="3654f-164">Az alapértelmezett gazdagép-specifikus profilok létezik így `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="3654f-164">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="3654f-165">PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] macOS rendszeren.</span><span class="sxs-lookup"><span data-stu-id="3654f-165">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="3654f-166">Mivel a macOS BSD, az előtag típusából származtatott `/usr/local` helyett használja `/opt`.</span><span class="sxs-lookup"><span data-stu-id="3654f-166">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="3654f-167">Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.1.0/`, és a szimbolikus hivatkozást van elhelyezve `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="3654f-167">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.1.0/`, and the symbolic link is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3654f-168">További források</span><span class="sxs-lookup"><span data-stu-id="3654f-168">Additional Resources</span></span>

* <span data-ttu-id="3654f-169">[Webes homebrew-val][brew]</span><span class="sxs-lookup"><span data-stu-id="3654f-169">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="3654f-170">[Github-adattár homebrew-val][GitHub]</span><span class="sxs-lookup"><span data-stu-id="3654f-170">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="3654f-171">[Homebrew-val – Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="3654f-171">[Homebrew-Cask][cask]</span></span>

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
