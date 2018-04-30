# <a name="installing-powershell-core-on-macos"></a><span data-ttu-id="954da-101">MacOS PowerShell központi telepítése</span><span class="sxs-lookup"><span data-stu-id="954da-101">Installing PowerShell Core on macOS</span></span>

<span data-ttu-id="954da-102">PowerShell Core macOS 10.12 vagy újabb verziókat támogatja.</span><span class="sxs-lookup"><span data-stu-id="954da-102">PowerShell Core supports macOS 10.12 and higher.</span></span>
<span data-ttu-id="954da-103">Minden csomagok érhetők el a githubon [kiadott][] lap.</span><span class="sxs-lookup"><span data-stu-id="954da-103">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="954da-104">A csomag telepítése után futtassa `pwsh` terminálról.</span><span class="sxs-lookup"><span data-stu-id="954da-104">Once the package is installed, run `pwsh` from a terminal.</span></span>

### <a name="installation-via-homebrew-on-macos-1012"></a><span data-ttu-id="954da-105">MacOS 10.12 keresztül Homebrew telepítése</span><span class="sxs-lookup"><span data-stu-id="954da-105">Installation via Homebrew on macOS 10.12</span></span>

<span data-ttu-id="954da-106">[Homebrew] [ brew] az előnyben részesített Csomagkezelőt a macOS van.</span><span class="sxs-lookup"><span data-stu-id="954da-106">[Homebrew][brew] is the preferred package manager for macOS.</span></span>
<span data-ttu-id="954da-107">Ha a `brew` parancs nem található, telepítenie kell a következő Homebrew [a utasításaikat][brew].</span><span class="sxs-lookup"><span data-stu-id="954da-107">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="954da-108">Homebrew telepítése után is könnyen PowerShell telepítése.</span><span class="sxs-lookup"><span data-stu-id="954da-108">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="954da-109">Először telepítse [Homebrew-Cask][cask], így további csomagok telepítése:</span><span class="sxs-lookup"><span data-stu-id="954da-109">First, install [Homebrew-Cask][cask], so you can install more packages:</span></span>

```sh
brew tap caskroom/cask
```

<span data-ttu-id="954da-110">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="954da-110">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="954da-111">Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:</span><span class="sxs-lookup"><span data-stu-id="954da-111">Finally, verify that your install is working properly:</span></span>

```sh
pwsh
```

<span data-ttu-id="954da-112">PowerShell új verzióinak kiadásakor egyszerűen Homebrew tartozó képletek frissítése, és PowerShell frissítése:</span><span class="sxs-lookup"><span data-stu-id="954da-112">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> <span data-ttu-id="954da-113">A fenti parancsokat is hívható meg egy PowerShell (pwsh) állomás, de majd a PowerShell rendszerhéjban kell kilépett és újraindul a frissítés befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="954da-113">The commands above can be called from within a PowerShell (pwsh) host, but then the PowerShell shell must be exited and restarted to complete the upgrade.</span></span>
> <span data-ttu-id="954da-114">és frissítse a $PSVersionTable megjelenő értékeket.</span><span class="sxs-lookup"><span data-stu-id="954da-114">and refresh the values shown in $PSVersionTable.</span></span>

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/

### <a name="installation-via-direct-download"></a><span data-ttu-id="954da-115">Telepítési keresztül közvetlen letöltése</span><span class="sxs-lookup"><span data-stu-id="954da-115">Installation via Direct Download</span></span>

<span data-ttu-id="954da-116">A PKG csomag `powershell-6.0.2-osx.10.12-x64.pkg` a a [kiadott][] lap a macOS számítógépre.</span><span class="sxs-lookup"><span data-stu-id="954da-116">Download the PKG package `powershell-6.0.2-osx.10.12-x64.pkg` from the [releases][] page onto your macOS machine.</span></span>

<span data-ttu-id="954da-117">Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítse azt a Terminálszolgáltatások:</span><span class="sxs-lookup"><span data-stu-id="954da-117">You can double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a><span data-ttu-id="954da-118">Bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="954da-118">Binary Archives</span></span>

<span data-ttu-id="954da-119">PowerShell bináris `tar.gz` archívumokat előírt macOS és Linux platformokat, a központi telepítési forgatókönyvek engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="954da-119">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="installing-binary-archives-on-macos"></a><span data-ttu-id="954da-120">A macOS telepítése bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="954da-120">Installing binary archives on macOS</span></span>

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

## <a name="uninstalling-powershell-core"></a><span data-ttu-id="954da-121">PowerShell Core eltávolítása</span><span class="sxs-lookup"><span data-stu-id="954da-121">Uninstalling PowerShell Core</span></span>

<span data-ttu-id="954da-122">PowerShell Homebrew telepítette, ha az Eltávolítás könnyen:</span><span class="sxs-lookup"><span data-stu-id="954da-122">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="954da-123">Ha telepítette a PowerShell segítségével közvetlen letöltési, PowerShell manuálisan kell eltávolítani:</span><span class="sxs-lookup"><span data-stu-id="954da-123">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="954da-124">Távolítsa el a további PowerShell elérési utak, tekintse meg a [elérési utak][] szakasz ebben a dokumentumban, és távolítsa el a kívánt elérési utak használata `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="954da-124">To remove the additional PowerShell paths, please see the [paths][] section in this document and remove the desired the paths using `sudo rm`.</span></span>

> [!NOTE]
> <span data-ttu-id="954da-125">Erre nincs szükség, ha Homebrew telepítette.</span><span class="sxs-lookup"><span data-stu-id="954da-125">This is not necessary if you installed with Homebrew.</span></span>

[elérési utak]:#paths
[paths]:#paths

## <a name="paths"></a><span data-ttu-id="954da-127">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="954da-127">Paths</span></span>

* <span data-ttu-id="954da-128">`$PSHOME` van `/opt/microsoft/powershell/6.0.0/`</span><span class="sxs-lookup"><span data-stu-id="954da-128">`$PSHOME` is `/opt/microsoft/powershell/6.0.0/`</span></span>
* <span data-ttu-id="954da-129">Felhasználói profilok rendszer nem olvas be `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="954da-129">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="954da-130">Alapértelmezett profilok rendszer nem olvas be `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="954da-130">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="954da-131">Modulok felhasználói rendszer nem olvas be `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="954da-131">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="954da-132">Megosztott modulok rendszer nem olvas be `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="954da-132">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="954da-133">Az alapértelmezett modulokat rendszer nem olvas be `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="954da-133">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="954da-134">A rögzítendő PSReadline előzmények `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="954da-134">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="954da-135">A profilok tiszteletben PowerShell gazdagép konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="954da-135">The profiles respect PowerShell's per-host configuration.</span></span>
<span data-ttu-id="954da-136">Így az alapértelmezett gazdagép-specifikus profilok létezik az `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="954da-136">So the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="954da-137">PowerShell tiszteletben tartja a [XDG Base könyvtár megadása] [ xdg-bds] macOS meg.</span><span class="sxs-lookup"><span data-stu-id="954da-137">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on macOS.</span></span>

<span data-ttu-id="954da-138">Mivel macOS BSD, az előtag származtatott `/usr/local` helyett használt `/opt`.</span><span class="sxs-lookup"><span data-stu-id="954da-138">Because macOS is a derivation of BSD, the prefix `/usr/local` is used instead of `/opt`.</span></span>
<span data-ttu-id="954da-139">Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.0.0/`, és a symlink van elhelyezve `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="954da-139">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.0/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

[kiadott]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
