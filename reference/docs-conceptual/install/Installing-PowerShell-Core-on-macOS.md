---
title: A PowerShell Core telepítése macOS rendszerre
description: Információ a PowerShell Core telepítése macOS rendszeren
ms.date: 12/12/2018
ms.openlocfilehash: 70f5d64aa8a697a9011d07fbcb2bb821463827e1
ms.sourcegitcommit: 58fb23c854f5a8b40ad1f952d3323aeeccac7a24
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/07/2019
ms.locfileid: "65229737"
---
# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="ae268-103">A PowerShell Core telepítése macOS rendszerre</span><span class="sxs-lookup"><span data-stu-id="ae268-103">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="ae268-104">A PowerShell Core a macOS 10.12 és újabb verzióit támogatja.</span><span class="sxs-lookup"><span data-stu-id="ae268-104">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="ae268-105">A githubon érhető el az összes csomag [kiadások][] lapot.</span><span class="sxs-lookup"><span data-stu-id="ae268-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="ae268-106">A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="ae268-106">After the package is installed, run `pwsh` from a terminal.</span></span>

## <a name="about-brew"></a><span data-ttu-id="ae268-107">Brew kapcsolatban</span><span class="sxs-lookup"><span data-stu-id="ae268-107">About Brew</span></span>

<span data-ttu-id="ae268-108">[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.</span><span class="sxs-lookup"><span data-stu-id="ae268-108">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="ae268-109">Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].</span><span class="sxs-lookup"><span data-stu-id="ae268-109">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>
<span data-ttu-id="ae268-110">Ellenkező esetben a PowerShell használatával telepítheti [közvetlen letöltése](#installation-via-direct-download) vagy [bináris archívum](#binary-archives).</span><span class="sxs-lookup"><span data-stu-id="ae268-110">Otherwise you may install PowerShell via [Direct Download](#installation-via-direct-download) or from [Binary Archives](#binary-archives).</span></span>

## <a name="installation-of-latest-stable-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="ae268-111">Legújabb stabil kiadási keresztül Homebrew MacOS 10.12 vagy újabb telepítése</span><span class="sxs-lookup"><span data-stu-id="ae268-111">Installation of latest stable release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="ae268-112">Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="ae268-112">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="ae268-113">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="ae268-113">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="ae268-114">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="ae268-114">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="ae268-115">PowerShell új verzióinak kiadásakor frissítés a Homebrew-képlet, és a PowerShell frissítése:</span><span class="sxs-lookup"><span data-stu-id="ae268-115">When new versions of PowerShell are released, update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="ae268-116">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés látható értékeket `$PSVersionTable`.</span><span class="sxs-lookup"><span data-stu-id="ae268-116">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in `$PSVersionTable`.</span></span>

[brew]: http://brew.sh/

## <a name="installation-of-latest-preview-release-via-homebrew-on-macos-1012-or-higher"></a><span data-ttu-id="ae268-117">MacOS 10.12 vagy újabb rendszeren keresztül Homebrew kiadási legújabb előzetes verziójának telepítése</span><span class="sxs-lookup"><span data-stu-id="ae268-117">Installation of latest preview release via Homebrew on macOS 10.12 or higher</span></span>

<span data-ttu-id="ae268-118">Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="ae268-118">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="ae268-119">Ha már telepítette a homebrew-val, a PowerShell is telepítheti.</span><span class="sxs-lookup"><span data-stu-id="ae268-119">After you've installed Homebrew, you can install PowerShell.</span></span>
<span data-ttu-id="ae268-120">Először telepítse a [Cask-verziók] [ cask-versions] csomagot, amely lehetővé teszi a cask csomagok alternatív verzióját telepítse:</span><span class="sxs-lookup"><span data-stu-id="ae268-120">First, install the [Cask-Versions][cask-versions] package that lets you install alternative versions of cask packages:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="ae268-121">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="ae268-121">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="ae268-122">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="ae268-122">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="ae268-123">PowerShell új verzióinak kiadásakor frissítés a Homebrew-képlet, és a PowerShell frissítése:</span><span class="sxs-lookup"><span data-stu-id="ae268-123">When new versions of PowerShell are released, update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="ae268-124">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="ae268-124">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="ae268-125">és látható értékeket frissítse `$PSVersionTable`.</span><span class="sxs-lookup"><span data-stu-id="ae268-125">and refresh the values shown in `$PSVersionTable`.</span></span>

## <a name="installation-via-direct-download"></a><span data-ttu-id="ae268-126">Telepítési keresztül közvetlen letöltésére</span><span class="sxs-lookup"><span data-stu-id="ae268-126">Installation via Direct Download</span></span>

<span data-ttu-id="ae268-127">A csomag-csomag letöltése `powershell-6.2.0-osx-x64.pkg`</span><span class="sxs-lookup"><span data-stu-id="ae268-127">Download the PKG package `powershell-6.2.0-osx-x64.pkg`</span></span>
<span data-ttu-id="ae268-128">az a [kiadások][] lap a macOS-számítógépre.</span><span class="sxs-lookup"><span data-stu-id="ae268-128">from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="ae268-129">Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítheti a terminálról:</span><span class="sxs-lookup"><span data-stu-id="ae268-129">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.2.0-osx-x64.pkg -target /
```

<span data-ttu-id="ae268-130">Telepítés [OpenSSL](#install-openssl).</span><span class="sxs-lookup"><span data-stu-id="ae268-130">Install [OpenSSL](#install-openssl).</span></span> <span data-ttu-id="ae268-131">PowerShell távvezérlése és CIM-műveletek OpenSSL van szükség.</span><span class="sxs-lookup"><span data-stu-id="ae268-131">OpenSSL is needed for PowerShell remoting and CIM operations.</span></span>

## <a name="binary-archives"></a><span data-ttu-id="ae268-132">Bináris archívum</span><span class="sxs-lookup"><span data-stu-id="ae268-132">Binary Archives</span></span>

<span data-ttu-id="ae268-133">PowerShell bináris `tar.gz` archívumok biztosított speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé, a macOS platformon.</span><span class="sxs-lookup"><span data-stu-id="ae268-133">PowerShell binary `tar.gz` archives are provided for the macOS platform to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="ae268-134">MacOS rendszeren telepítése bináris archívum</span><span class="sxs-lookup"><span data-stu-id="ae268-134">Installing binary archives on macOS</span></span>

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

<span data-ttu-id="ae268-135">Telepítés [OpenSSL](#install-openssl).</span><span class="sxs-lookup"><span data-stu-id="ae268-135">Install [OpenSSL](#install-openssl).</span></span> <span data-ttu-id="ae268-136">PowerShell távvezérlése és CIM-műveletek OpenSSL van szükség.</span><span class="sxs-lookup"><span data-stu-id="ae268-136">OpenSSL is needed for PowerShell remoting and CIM operations.</span></span>

## <a name="installing-dependencies"></a><span data-ttu-id="ae268-137">Függőségek telepítése</span><span class="sxs-lookup"><span data-stu-id="ae268-137">Installing dependencies</span></span>

### <a name="install-xcode-command-line-tools"></a><span data-ttu-id="ae268-138">Xcode-ban a parancssori eszközök telepítése</span><span class="sxs-lookup"><span data-stu-id="ae268-138">Install XCode command-line tools</span></span>

```sh
xcode-select --install
```

### <a name="install-openssl"></a><span data-ttu-id="ae268-139">OpenSSL telepítése</span><span class="sxs-lookup"><span data-stu-id="ae268-139">Install OpenSSL</span></span>

<span data-ttu-id="ae268-140">PowerShell távvezérlése és CIM-műveletek OpenSSL van szükség.</span><span class="sxs-lookup"><span data-stu-id="ae268-140">OpenSSL is needed for PowerShell remoting and CIM operations.</span></span> <span data-ttu-id="ae268-141">Telepíthet MacPorts vagy Brew keresztül.</span><span class="sxs-lookup"><span data-stu-id="ae268-141">You can install via MacPorts or Brew.</span></span>

#### <a name="install-openssl-via-brew"></a><span data-ttu-id="ae268-142">OpenSSL keresztül Brew telepítése</span><span class="sxs-lookup"><span data-stu-id="ae268-142">Install OpenSSL via Brew</span></span>

<span data-ttu-id="ae268-143">Lásd: [kapcsolatos Brew](#about-brew) Brew kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="ae268-143">See [About Brew](#about-brew) for information about Brew.</span></span>

<span data-ttu-id="ae268-144">OpenSSL telepítéséhez futtassa `brew install openssl`.</span><span class="sxs-lookup"><span data-stu-id="ae268-144">To install OpenSSL, run `brew install openssl`.</span></span>

#### <a name="install-openssl-via-macports"></a><span data-ttu-id="ae268-145">OpenSSL keresztül MacPorts telepítése</span><span class="sxs-lookup"><span data-stu-id="ae268-145">Install OpenSSL via MacPorts</span></span>

1. <span data-ttu-id="ae268-146">Telepítse a [xcode-ban a parancssori eszközök](#install-xcode-command-line-tools).</span><span class="sxs-lookup"><span data-stu-id="ae268-146">Install the [XCode command line tools](#install-xcode-command-line-tools).</span></span>
1. <span data-ttu-id="ae268-147">Telepítse a MacPorts.</span><span class="sxs-lookup"><span data-stu-id="ae268-147">Install MacPorts.</span></span>
   <span data-ttu-id="ae268-148">Ha utasításokat van szüksége, tekintse meg a [telepítési útmutató](https://guide.macports.org/chunked/installing.macports.html).</span><span class="sxs-lookup"><span data-stu-id="ae268-148">If you need instructions, refer to the [installation guide](https://guide.macports.org/chunked/installing.macports.html).</span></span>
1. <span data-ttu-id="ae268-149">Frissítés MacPorts futtatásával `sudo port selfupdate`.</span><span class="sxs-lookup"><span data-stu-id="ae268-149">Update MacPorts by running `sudo port selfupdate`.</span></span>
1. <span data-ttu-id="ae268-150">MacPorts csomagok frissítése futtatásával `sudo port upgrade outdated`.</span><span class="sxs-lookup"><span data-stu-id="ae268-150">Upgrade MacPorts packages by running `sudo port upgrade outdated`.</span></span>
1. <span data-ttu-id="ae268-151">Telepítse az OpenSSL futtatásával `sudo port install openssl`.</span><span class="sxs-lookup"><span data-stu-id="ae268-151">Install OpenSSL by running `sudo port install openssl`.</span></span>
1. <span data-ttu-id="ae268-152">Hivatkozás a kódtárakat, hogy elérhetők legyenek a Powershellbe:</span><span class="sxs-lookup"><span data-stu-id="ae268-152">Link the libraries to make them available to PowerShell:</span></span>

```sh
sudo mkdir -p /usr/local/opt/openssl
sudo ln -s /opt/local/lib /usr/local/opt/openssl/lib
```

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="ae268-153">A PowerShell Core eltávolítása</span><span class="sxs-lookup"><span data-stu-id="ae268-153">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="ae268-154">Ha a homebrew-val telepített PowerShell, a következő paranccsal távolíthatja el:</span><span class="sxs-lookup"><span data-stu-id="ae268-154">If you installed PowerShell with Homebrew, use the following command to uninstall:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="ae268-155">Ha közvetlen letöltésére keresztül telepített, a PowerShell, PowerShell manuálisan kell eltávolítani:</span><span class="sxs-lookup"><span data-stu-id="ae268-155">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="ae268-156">Távolítsa el a további PowerShell-elérési utak, tekintse meg a [elérési utak](#paths) című rész ebben a dokumentumban, és távolítsa el az elérési utak használata `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="ae268-156">To remove the additional PowerShell paths, refer to the [paths](#paths) section in this document and remove the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="ae268-157">Ez nem szükséges, ha a telepítést a homebrew-val.</span><span class="sxs-lookup"><span data-stu-id="ae268-157">This is not necessary if you installed with Homebrew.</span></span>

## <a name="paths"></a><span data-ttu-id="ae268-158">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="ae268-158">Paths</span></span>

* <span data-ttu-id="ae268-159">`$PSHOME` van `/usr/local/microsoft/powershell/6.2.0/`</span><span class="sxs-lookup"><span data-stu-id="ae268-159">`$PSHOME` is `/usr/local/microsoft/powershell/6.2.0/`</span></span>
* <span data-ttu-id="ae268-160">Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="ae268-160">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="ae268-161">Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="ae268-161">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="ae268-162">Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="ae268-162">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="ae268-163">Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="ae268-163">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="ae268-164">Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="ae268-164">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="ae268-165">PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="ae268-165">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="ae268-166">A profilok veszik figyelembe a PowerShell a gazdagép konfigurációja.</span><span class="sxs-lookup"><span data-stu-id="ae268-166">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="ae268-167">Az alapértelmezett gazdagép-specifikus profil létezik így `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="ae268-167">So the default host-specific profile exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="ae268-168">PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] macOS rendszeren.</span><span class="sxs-lookup"><span data-stu-id="ae268-168">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="ae268-169">Mivel a macOS BSD, az előtag típusából származtatott `/usr/local` helyett használja `/opt`.</span><span class="sxs-lookup"><span data-stu-id="ae268-169">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="ae268-170">Tehát `$PSHOME` van `/usr/local/microsoft/powershell/6.2.0/`, és a szimbolikus hivatkozást van elhelyezve `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="ae268-170">So, `$PSHOME` is `/usr/local/microsoft/powershell/6.2.0/`, and the symbolic link is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae268-171">Egyéb források</span><span class="sxs-lookup"><span data-stu-id="ae268-171">Additional Resources</span></span>

* <span data-ttu-id="ae268-172">[Webes homebrew-val][brew]</span><span class="sxs-lookup"><span data-stu-id="ae268-172">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="ae268-173">[Github-adattár homebrew-val][GitHub]</span><span class="sxs-lookup"><span data-stu-id="ae268-173">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="ae268-174">[Homebrew-Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="ae268-174">[Homebrew-Cask][cask]</span></span>

[brew]: http://brew.sh/
[Cask]: https://github.com/Homebrew/homebrew-cask
[cask-versions]: https://github.com/Homebrew/homebrew-cask-versions
[GitHub]: https://github.com/Homebrew
[Kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
