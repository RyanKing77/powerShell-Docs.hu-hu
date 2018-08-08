---
title: A PowerShell Core telepítése macOS rendszerre
description: Információ a PowerShell Core telepítése macOS rendszeren
ms.date: 08/06/2018
ms.openlocfilehash: ff1814d95b3ca3fa8497069dff249fd2ad5576ef
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587465"
---
# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="12de1-103">A PowerShell Core telepítése macOS rendszerre</span><span class="sxs-lookup"><span data-stu-id="12de1-103">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="12de1-104">A PowerShell Core a macOS 10.12 és újabb verzióit támogatja.</span><span class="sxs-lookup"><span data-stu-id="12de1-104">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="12de1-105">A githubon érhető el az összes csomag [kiadások][] lapot.</span><span class="sxs-lookup"><span data-stu-id="12de1-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="12de1-106">A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="12de1-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

### <a name="installation-via-homebrew-on-macos-1012"></a><span data-ttu-id="12de1-107">A macOS 10.12 + keresztül Homebrew telepítési</span><span class="sxs-lookup"><span data-stu-id="12de1-107">Installation via Homebrew on macOS 10.12+</span></span>

<span data-ttu-id="12de1-108">[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.</span><span class="sxs-lookup"><span data-stu-id="12de1-108">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="12de1-109">Egy terminálablakban írja be a következőt `brew` futtatásához a homebrew-val.</span><span class="sxs-lookup"><span data-stu-id="12de1-109">From a terminal window, type `brew` to run Homebrew.</span></span>  <span data-ttu-id="12de1-110">Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].</span><span class="sxs-lookup"><span data-stu-id="12de1-110">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

> [!NOTE]
> <span data-ttu-id="12de1-111">Ha a homebrew-t korábban telepítette, mindig egy célszerű futtatni "frissítés-visszaállítás brew" & & "brew frissítés".</span><span class="sxs-lookup"><span data-stu-id="12de1-111">If you installed Homebrew in the past, it's always a good idea to run 'brew update-reset' && 'brew update'.</span></span>
```sh
brew update-reset
brew update
```

> <span data-ttu-id="12de1-112">Régebbi verzióit a homebrew-t használja a koppintson "caskroom/cask", amely elavult, és telepítse át a "homebrew/cask".</span><span class="sxs-lookup"><span data-stu-id="12de1-112">Older versions of Homebrew used the tap 'caskroom/cask', which has been deprecated, and migrated into 'homebrew/cask'.</span></span>  <span data-ttu-id="12de1-113">További információ található [homebrew-val – cask][cask].</span><span class="sxs-lookup"><span data-stu-id="12de1-113">More information can be found at [Homebrew-cask][cask].</span></span> <span data-ttu-id="12de1-114">Használja a "brew koppintson" parancsot az aktuális TAP-oknak listázásához.</span><span class="sxs-lookup"><span data-stu-id="12de1-114">Use the 'brew tap' command to list your current taps.</span></span>  <span data-ttu-id="12de1-115">Ha megjelenik "caskroom/cask" "frissítés brew" használhatja a homebrew-val áttelepítése a TAP-oknak kell.</span><span class="sxs-lookup"><span data-stu-id="12de1-115">If you see 'caskroom/cask' you can use 'brew update' to have Homebrew migrate the taps.</span></span>

```sh
brew tap
brew update
```

<span data-ttu-id="12de1-116">Telepítése vagy frissítése után homebrew-val, a PowerShell telepítése ördöngösség.</span><span class="sxs-lookup"><span data-stu-id="12de1-116">Once you've installed/updated Homebrew, installing PowerShell is easy.</span></span>

<span data-ttu-id="12de1-117">PowerShell telepítéséhez:</span><span class="sxs-lookup"><span data-stu-id="12de1-117">To install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="12de1-118">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="12de1-118">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="12de1-119">Lépjen ki a PowerShell, és térjen vissza a bash, használja a 'Kilépés' parancsot.</span><span class="sxs-lookup"><span data-stu-id="12de1-119">To exit PowerShell, and return to bash, use the 'exit' command.</span></span>
```sh
exit
```

<span data-ttu-id="12de1-120">PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:</span><span class="sxs-lookup"><span data-stu-id="12de1-120">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="12de1-121">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés $PSVersionTable látható értékeket.</span><span class="sxs-lookup"><span data-stu-id="12de1-121">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

### <a name="installing-preview-via-homebrew-on-macos-1012"></a><span data-ttu-id="12de1-122">Előzetes keresztül Homebrew macOS 10.12 + telepítése</span><span class="sxs-lookup"><span data-stu-id="12de1-122">Installing Preview via Homebrew on macOS 10.12+</span></span>

<span data-ttu-id="12de1-123">[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.</span><span class="sxs-lookup"><span data-stu-id="12de1-123">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="12de1-124">Egy terminálablakban írja be a következőt `brew` futtatásához a homebrew-val.</span><span class="sxs-lookup"><span data-stu-id="12de1-124">From a terminal window, type `brew` to run Homebrew.</span></span>  <span data-ttu-id="12de1-125">Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].</span><span class="sxs-lookup"><span data-stu-id="12de1-125">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

> [!NOTE]
> <span data-ttu-id="12de1-126">Ha a homebrew-t korábban telepítette, mindig egy célszerű futtatni "frissítés-visszaállítás brew" & & "brew frissítés".</span><span class="sxs-lookup"><span data-stu-id="12de1-126">If you installed Homebrew in the past, it's always a good idea to run 'brew update-reset' && 'brew update'.</span></span>
```sh
brew update-reset
brew update
```

<span data-ttu-id="12de1-127">Ezután koppintson a `versions` hordó-adattár az előzetes verzió csomag beszerzése:</span><span class="sxs-lookup"><span data-stu-id="12de1-127">Then, you must tap the `versions` casks repository to get the preview package:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="12de1-128">PowerShell-minta telepítése:</span><span class="sxs-lookup"><span data-stu-id="12de1-128">To install PowerShell Preview:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="12de1-129">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="12de1-129">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="12de1-130">PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell-előzetes verzió:</span><span class="sxs-lookup"><span data-stu-id="12de1-130">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell Preview:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="12de1-131">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés $PSVersionTable látható értékeket.</span><span class="sxs-lookup"><span data-stu-id="12de1-131">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

### <a name="installation-via-direct-download"></a><span data-ttu-id="12de1-132">Telepítési keresztül közvetlen letöltésére</span><span class="sxs-lookup"><span data-stu-id="12de1-132">Installation via Direct Download</span></span>

<span data-ttu-id="12de1-133">A csomag csomag `powershell-6.0.2-osx.10.12-x64.pkg` a a [kiadások][] lap a macOS-számítógépre.</span><span class="sxs-lookup"><span data-stu-id="12de1-133">Download the PKG package `powershell-6.0.2-osx.10.12-x64.pkg` from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="12de1-134">Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítheti a terminálról:</span><span class="sxs-lookup"><span data-stu-id="12de1-134">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="12de1-135">Bináris archívum</span><span class="sxs-lookup"><span data-stu-id="12de1-135">Binary Archives</span></span>

<span data-ttu-id="12de1-136">PowerShell bináris `tar.gz` archívumok biztosított macOS és Linux platformokat, a speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé.</span><span class="sxs-lookup"><span data-stu-id="12de1-136">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="12de1-137">MacOS rendszeren telepítése bináris archívum</span><span class="sxs-lookup"><span data-stu-id="12de1-137">Installing binary archives on macOS</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.0.2

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.0.2

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.2/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.0.2/pwsh /usr/local/bin/pwsh
```

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="12de1-138">A PowerShell Core eltávolítása</span><span class="sxs-lookup"><span data-stu-id="12de1-138">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="12de1-139">Ha a PowerShell telepítése a homebrew-val, az Eltávolítás ördöngösség:</span><span class="sxs-lookup"><span data-stu-id="12de1-139">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="12de1-140">Ha közvetlen letöltésére keresztül telepített, a PowerShell, PowerShell manuálisan kell eltávolítani:</span><span class="sxs-lookup"><span data-stu-id="12de1-140">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="12de1-141">Távolítsa el a további PowerShell-elérési utak, tekintse meg a [elérési utak][] szakaszt ebben a dokumentumban, és távolítsa el a kívánt az elérési utak használata `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="12de1-141">To remove the additional PowerShell paths, please see the [paths][] section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="12de1-142">Ez nem szükséges, ha a telepítést a homebrew-val.</span><span class="sxs-lookup"><span data-stu-id="12de1-142">This is not necessary if you installed with Homebrew.</span></span>

[Elérési utak]:#paths
[paths]:#paths

## <a name="paths"></a><span data-ttu-id="12de1-144">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="12de1-144">Paths</span></span>

* <span data-ttu-id="12de1-145">`$PSHOME` van `/usr/local/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="12de1-145">`$PSHOME` is `/usr/local/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="12de1-146">Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="12de1-146">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="12de1-147">Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="12de1-147">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="12de1-148">Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="12de1-148">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="12de1-149">Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="12de1-149">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="12de1-150">Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="12de1-150">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="12de1-151">PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="12de1-151">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="12de1-152">A profilok veszik figyelembe a PowerShell a gazdagép konfigurációja.</span><span class="sxs-lookup"><span data-stu-id="12de1-152">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="12de1-153">Az alapértelmezett gazdagép-specifikus profilok létezik így `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="12de1-153">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="12de1-154">PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] macOS rendszeren.</span><span class="sxs-lookup"><span data-stu-id="12de1-154">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="12de1-155">Mivel a macOS BSD, az előtag típusából származtatott `/usr/local` helyett használja `/opt`.</span><span class="sxs-lookup"><span data-stu-id="12de1-155">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="12de1-156">Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.0.2/`, és a szimbolikus van elhelyezve `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="12de1-156">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.2/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12de1-157">További források</span><span class="sxs-lookup"><span data-stu-id="12de1-157">Additional Resources</span></span>

* <span data-ttu-id="12de1-158">[Webes homebrew-val][brew]</span><span class="sxs-lookup"><span data-stu-id="12de1-158">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="12de1-159">[Github-adattár homebrew-val][GitHub]</span><span class="sxs-lookup"><span data-stu-id="12de1-159">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="12de1-160">[Homebrew-val – Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="12de1-160">[Homebrew-Cask][cask]</span></span>


[brew]: http://brew.sh/
[GitHub]: https://github.com/Homebrew
[Cask]: https://github.com/Homebrew/homebrew-cask
[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
