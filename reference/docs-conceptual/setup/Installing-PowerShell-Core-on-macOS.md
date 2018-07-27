# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="0863e-101">A PowerShell Core telepítése macOS rendszerre</span><span class="sxs-lookup"><span data-stu-id="0863e-101">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="0863e-102">A PowerShell Core a macOS 10.12 és újabb verzióit támogatja.</span><span class="sxs-lookup"><span data-stu-id="0863e-102">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="0863e-103">A githubon érhető el az összes csomag [kiadások][] lapot.</span><span class="sxs-lookup"><span data-stu-id="0863e-103">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="0863e-104">A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="0863e-104">Once the package is installed, run `pwsh` from a terminal.</span></span>

### <a name="installation-via-homebrew-on-macos-1012"></a><span data-ttu-id="0863e-105">A macOS 10.12 + keresztül Homebrew telepítési</span><span class="sxs-lookup"><span data-stu-id="0863e-105">Installation via Homebrew on macOS 10.12+</span></span>

<span data-ttu-id="0863e-106">[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.</span><span class="sxs-lookup"><span data-stu-id="0863e-106">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="0863e-107">Egy terminálablakban írja be a következőt `brew` futtatásához a homebrew-val.</span><span class="sxs-lookup"><span data-stu-id="0863e-107">From a terminal window, type `brew` to run Homebrew.</span></span>  <span data-ttu-id="0863e-108">Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].</span><span class="sxs-lookup"><span data-stu-id="0863e-108">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

> [!NOTE]
> <span data-ttu-id="0863e-109">Ha a homebrew-t korábban telepítette, mindig egy célszerű futtatni "frissítés-visszaállítás brew" & & "brew frissítés".</span><span class="sxs-lookup"><span data-stu-id="0863e-109">If you installed Homebrew in the past, it's always a good idea to run 'brew update-reset' && 'brew update'.</span></span>
```sh
brew update-reset
brew update
```

> <span data-ttu-id="0863e-110">Régebbi verzióit a homebrew-t használja a koppintson "caskroom/cask", amely elavult, és telepítse át a "homebrew/cask".</span><span class="sxs-lookup"><span data-stu-id="0863e-110">Older versions of Homebrew used the tap 'caskroom/cask', which has been deprecated, and migrated into 'homebrew/cask'.</span></span>  <span data-ttu-id="0863e-111">További információ található [homebrew-val – cask][cask].</span><span class="sxs-lookup"><span data-stu-id="0863e-111">More information can be found at [Homebrew-cask][cask].</span></span> <span data-ttu-id="0863e-112">Használja a "brew koppintson" parancsot az aktuális TAP-oknak listázásához.</span><span class="sxs-lookup"><span data-stu-id="0863e-112">Use the 'brew tap' command to list your current taps.</span></span>  <span data-ttu-id="0863e-113">Ha megjelenik "caskroom/cask" "frissítés brew" használhatja a homebrew-val áttelepítése a TAP-oknak kell.</span><span class="sxs-lookup"><span data-stu-id="0863e-113">If you see 'caskroom/cask' you can use 'brew update' to have Homebrew migrate the taps.</span></span>

```sh
brew tap
brew update
```

<span data-ttu-id="0863e-114">Telepítése vagy frissítése után homebrew-val, a PowerShell telepítése ördöngösség.</span><span class="sxs-lookup"><span data-stu-id="0863e-114">Once you've installed/updated Homebrew, installing PowerShell is easy.</span></span>

<span data-ttu-id="0863e-115">PowerShell telepítéséhez:</span><span class="sxs-lookup"><span data-stu-id="0863e-115">To install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="0863e-116">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="0863e-116">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="0863e-117">Lépjen ki a PowerShell, és térjen vissza a bash, használja a 'Kilépés' parancsot.</span><span class="sxs-lookup"><span data-stu-id="0863e-117">To exit PowerShell, and return to bash, use the 'exit' command.</span></span> 
```sh
exit
```

<span data-ttu-id="0863e-118">PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0863e-118">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="0863e-119">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés $PSVersionTable látható értékeket.</span><span class="sxs-lookup"><span data-stu-id="0863e-119">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

### <a name="installing-preview-via-homebrew-on-macos-1012"></a><span data-ttu-id="0863e-120">Előzetes keresztül Homebrew macOS 10.12 + telepítése</span><span class="sxs-lookup"><span data-stu-id="0863e-120">Installing Preview via Homebrew on macOS 10.12+</span></span>

<span data-ttu-id="0863e-121">[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.</span><span class="sxs-lookup"><span data-stu-id="0863e-121">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="0863e-122">Egy terminálablakban írja be a következőt `brew` futtatásához a homebrew-val.</span><span class="sxs-lookup"><span data-stu-id="0863e-122">From a terminal window, type `brew` to run Homebrew.</span></span>  <span data-ttu-id="0863e-123">Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].</span><span class="sxs-lookup"><span data-stu-id="0863e-123">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

> [!NOTE]
> <span data-ttu-id="0863e-124">Ha a homebrew-t korábban telepítette, mindig egy célszerű futtatni "frissítés-visszaállítás brew" & & "brew frissítés".</span><span class="sxs-lookup"><span data-stu-id="0863e-124">If you installed Homebrew in the past, it's always a good idea to run 'brew update-reset' && 'brew update'.</span></span>
```sh
brew update-reset
brew update
```

<span data-ttu-id="0863e-125">Ezután koppintson a `versions` hordó-adattár az előzetes verzió csomag beszerzése:</span><span class="sxs-lookup"><span data-stu-id="0863e-125">Then, you must tap the `versions` casks repository to get the preview package:</span></span>

```sh
brew tap homebrew/cask-versions
```

<span data-ttu-id="0863e-126">PowerShell-minta telepítése:</span><span class="sxs-lookup"><span data-stu-id="0863e-126">To install PowerShell Preview:</span></span>

```sh
brew cask install powershell-preview
```

<span data-ttu-id="0863e-127">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="0863e-127">Finally, verify that your install is working properly:</span></span>

```sh
pwsh-preview
```

<span data-ttu-id="0863e-128">PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell-előzetes verzió:</span><span class="sxs-lookup"><span data-stu-id="0863e-128">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell Preview:</span></span>

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> <span data-ttu-id="0863e-129">A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés $PSVersionTable látható értékeket.</span><span class="sxs-lookup"><span data-stu-id="0863e-129">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade and refresh the values shown in $PSVersionTable.</span></span>

### <a name="installation-via-direct-download"></a><span data-ttu-id="0863e-130">Telepítési keresztül közvetlen letöltésére</span><span class="sxs-lookup"><span data-stu-id="0863e-130">Installation via Direct Download</span></span>

<span data-ttu-id="0863e-131">A csomag csomag `powershell-6.0.2-osx.10.12-x64.pkg` a a [kiadások][] lap a macOS-számítógépre.</span><span class="sxs-lookup"><span data-stu-id="0863e-131">Download the PKG package `powershell-6.0.2-osx.10.12-x64.pkg` from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="0863e-132">Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítheti a terminálról:</span><span class="sxs-lookup"><span data-stu-id="0863e-132">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="0863e-133">Bináris archívum</span><span class="sxs-lookup"><span data-stu-id="0863e-133">Binary Archives</span></span>

<span data-ttu-id="0863e-134">PowerShell bináris `tar.gz` archívumok biztosított macOS és Linux platformokat, a speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé.</span><span class="sxs-lookup"><span data-stu-id="0863e-134">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="0863e-135">MacOS rendszeren telepítése bináris archívum</span><span class="sxs-lookup"><span data-stu-id="0863e-135">Installing binary archives on macOS</span></span>

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

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="0863e-136">A PowerShell Core eltávolítása</span><span class="sxs-lookup"><span data-stu-id="0863e-136">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="0863e-137">Ha a PowerShell telepítése a homebrew-val, az Eltávolítás ördöngösség:</span><span class="sxs-lookup"><span data-stu-id="0863e-137">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="0863e-138">Ha közvetlen letöltésére keresztül telepített, a PowerShell, PowerShell manuálisan kell eltávolítani:</span><span class="sxs-lookup"><span data-stu-id="0863e-138">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="0863e-139">Távolítsa el a további PowerShell-elérési utak, tekintse meg a [elérési utak][] szakaszt ebben a dokumentumban, és távolítsa el a kívánt az elérési utak használata `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="0863e-139">To remove the additional PowerShell paths, please see the [paths][] section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="0863e-140">Ez nem szükséges, ha a telepítést a homebrew-val.</span><span class="sxs-lookup"><span data-stu-id="0863e-140">This is not necessary if you installed with Homebrew.</span></span>

[Elérési utak]:#paths
[paths]:#paths

## <a name="paths"></a><span data-ttu-id="0863e-142">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="0863e-142">Paths</span></span>

* <span data-ttu-id="0863e-143">`$PSHOME` van `/usr/local/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="0863e-143">`$PSHOME` is `/usr/local/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="0863e-144">Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="0863e-144">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="0863e-145">Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="0863e-145">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="0863e-146">Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="0863e-146">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="0863e-147">Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="0863e-147">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="0863e-148">Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="0863e-148">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="0863e-149">PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="0863e-149">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="0863e-150">A profilok veszik figyelembe a PowerShell a gazdagép konfigurációja.</span><span class="sxs-lookup"><span data-stu-id="0863e-150">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="0863e-151">Az alapértelmezett gazdagép-specifikus profilok létezik így `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="0863e-151">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="0863e-152">PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] macOS rendszeren.</span><span class="sxs-lookup"><span data-stu-id="0863e-152">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="0863e-153">Mivel a macOS BSD, az előtag típusából származtatott `/usr/local` helyett használja `/opt`.</span><span class="sxs-lookup"><span data-stu-id="0863e-153">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="0863e-154">Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.0.2/`, és a szimbolikus van elhelyezve `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="0863e-154">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.2/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0863e-155">További források</span><span class="sxs-lookup"><span data-stu-id="0863e-155">Additional Resources</span></span>

* <span data-ttu-id="0863e-156">[Webes homebrew-val][brew]</span><span class="sxs-lookup"><span data-stu-id="0863e-156">[Homebrew Web][brew]</span></span>
* <span data-ttu-id="0863e-157">[Github-adattár homebrew-val][GitHub]</span><span class="sxs-lookup"><span data-stu-id="0863e-157">[Homebrew Github Repository][GitHub]</span></span>
* <span data-ttu-id="0863e-158">[Homebrew-val – Cask][cask]</span><span class="sxs-lookup"><span data-stu-id="0863e-158">[Homebrew-Cask][cask]</span></span>


[brew]: http://brew.sh/
[GitHub]: https://github.com/Homebrew
[Cask]: https://github.com/Homebrew/homebrew-cask
[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
