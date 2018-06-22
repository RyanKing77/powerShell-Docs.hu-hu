# <a name="installing-powershell-core-on-macos"></a>A PowerShell Core telepítése macOS rendszerre

PowerShell Core macOS 10.12 vagy újabb verziókat támogatja.
Minden csomagok érhetők el a githubon [Kiadások][] lap.
A csomag telepítése után futtassa `pwsh` terminálról.

### <a name="installation-via-homebrew-on-macos-1012"></a>MacOS 10.12 keresztül Homebrew telepítése

[Homebrew] [ brew] az előnyben részesített Csomagkezelőt a macOS van.
Ha a `brew` parancs nem található, telepítenie kell a következő Homebrew [a utasításaikat][brew].

Homebrew telepítése után is könnyen PowerShell telepítése.
Először telepítse [Homebrew-Cask][cask], így további csomagok telepítése:

```sh
brew tap caskroom/cask
```

Most már PowerShell telepíthető:

```sh
brew cask install powershell
```

Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:

```sh
pwsh
```

PowerShell új verzióinak kiadásakor egyszerűen Homebrew tartozó képletek frissítése, és PowerShell frissítése:

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> A fenti parancsokat is hívható meg egy PowerShell (pwsh) állomás, de majd a PowerShell rendszerhéjban kell kilépett és indítani, hogy végezze el a frissítést, és frissítse a $PSVersionTable megjelenő értékeket.

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/

### <a name="installation-via-direct-download"></a>Telepítési keresztül közvetlen letöltése

A PKG csomag `powershell-6.0.2-osx.10.12-x64.pkg` a a [Kiadások][] lap a macOS számítógépre.

Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítse azt a Terminálszolgáltatások:

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a>Bináris archívumokat

PowerShell bináris `tar.gz` archívumokat előírt macOS és Linux platformokat, a központi telepítési forgatókönyvek engedélyezése.

### <a name="installing-binary-archives-on-macos"></a>A macOS telepítése bináris archívumokat

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

## <a name="uninstalling-powershell-core"></a>PowerShell Core eltávolítása

PowerShell Homebrew telepítette, ha az Eltávolítás könnyen:

```sh
brew cask uninstall powershell
```

Ha telepítette a PowerShell segítségével közvetlen letöltési, PowerShell manuálisan kell eltávolítani:

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

Távolítsa el a további PowerShell elérési utak, tekintse meg a [elérési utak][] szakasz ebben a dokumentumban, és távolítsa el a kívánt elérési utak használata `sudo rm`.

> [!NOTE]
> Erre nincs szükség, ha Homebrew telepítette.

[elérési utak]:#paths

## <a name="paths"></a>Elérési utak

* `$PSHOME` van `/usr/local/microsoft/powershell/6.0.2/`
* Felhasználói profilok rendszer nem olvas be `~/.config/powershell/profile.ps1`
* Alapértelmezett profilok rendszer nem olvas be `$PSHOME/profile.ps1`
* Modulok felhasználói rendszer nem olvas be `~/.local/share/powershell/Modules`
* Megosztott modulok rendszer nem olvas be `/usr/local/share/powershell/Modules`
* Az alapértelmezett modulokat rendszer nem olvas be `$PSHOME/Modules`
* A rögzítendő PSReadline előzmények `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

A profilok tiszteletben PowerShell gazdagép konfiguráció.
Így az alapértelmezett gazdagép-specifikus profilok létezik az `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.

PowerShell tiszteletben tartja a [XDG Base könyvtár megadása] [ xdg-bds] macOS meg.

Mivel macOS BSD, az előtag származtatott `/usr/local` helyett használt `/opt`.
Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.0.2/`, és a symlink van elhelyezve `/usr/local/bin/pwsh`.

[Kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
