# <a name="installing-powershell-core-on-macos"></a>A PowerShell Core telepítése macOS rendszerre

A PowerShell Core a macOS 10.12 és újabb verzióit támogatja.
A githubon érhető el az összes csomag [kiadások][] lapot.
A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.

### <a name="installation-via-homebrew-on-macos-1012"></a>A macOS 10.12 + keresztül Homebrew telepítési

[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.
Egy terminálablakban írja be a következőt `brew` futtatásához a homebrew-val.  Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].

> [!NOTE]
> Ha a homebrew-t korábban telepítette, mindig egy célszerű futtatni "frissítés-visszaállítás brew" & & "brew frissítés".
```sh
brew update-reset
brew update
```

> Régebbi verzióit a homebrew-t használja a koppintson "caskroom/cask", amely elavult, és telepítse át a "homebrew/cask".  További információ található [homebrew-val – cask][cask]. Használja a "brew koppintson" parancsot az aktuális TAP-oknak listázásához.  Ha megjelenik "caskroom/cask" "frissítés brew" használhatja a homebrew-val áttelepítése a TAP-oknak kell.

```sh
brew tap
brew update
```

Telepítése vagy frissítése után homebrew-val, a PowerShell telepítése ördöngösség.

PowerShell telepítéséhez:

```sh
brew cask install powershell
```

Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:

```sh
pwsh
```

Lépjen ki a PowerShell, és térjen vissza a bash, használja a 'Kilépés' parancsot. 
```sh
exit
```

PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell:

```sh
brew update
brew cask upgrade powershell
```

> [!NOTE]
> A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés $PSVersionTable látható értékeket.

### <a name="installing-preview-via-homebrew-on-macos-1012"></a>Előzetes keresztül Homebrew macOS 10.12 + telepítése

[Homebrew] [ brew] az előnyben részesített Csomagkezelő macOS-hez.
Egy terminálablakban írja be a következőt `brew` futtatásához a homebrew-val.  Ha a `brew` parancs nem található kell, hogy telepítse a homebrew-val következő [az utasításokat][brew].

> [!NOTE]
> Ha a homebrew-t korábban telepítette, mindig egy célszerű futtatni "frissítés-visszaállítás brew" & & "brew frissítés".
```sh
brew update-reset
brew update
```

Ezután koppintson a `versions` hordó-adattár az előzetes verzió csomag beszerzése:

```sh
brew tap homebrew/cask-versions
```

PowerShell-minta telepítése:

```sh
brew cask install powershell-preview
```

Végül győződjön meg arról, hogy megfelelően működik-e a telepítés:

```sh
pwsh-preview
```

PowerShell új verzióinak kiadásakor egyszerűen frissítés a Homebrew-képlet, és frissítése a PowerShell-előzetes verzió:

```sh
brew update
brew cask upgrade powershell-preview
```

> [!NOTE]
> A fenti parancsok is meghívhassák belül (pwsh) PowerShell-gazdagépet, de majd a PowerShell-héj kell kilépett és újraindítja a frissítés befejezéséhez és a frissítés $PSVersionTable látható értékeket.

### <a name="installation-via-direct-download"></a>Telepítési keresztül közvetlen letöltésére

A csomag csomag `powershell-6.0.2-osx.10.12-x64.pkg` a a [kiadások][] lap a macOS-számítógépre.

Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítheti a terminálról:

```sh
sudo installer -pkg powershell-6.0.2-osx.10.12-x64.pkg -target /
```

## <a name="binary-archives"></a>Bináris archívum

PowerShell bináris `tar.gz` archívumok biztosított macOS és Linux platformokat, a speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé.

### <a name="installing-binary-archives-on-macos"></a>MacOS rendszeren telepítése bináris archívum

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

## <a name="uninstalling-powershell-core"></a>A PowerShell Core eltávolítása

Ha a PowerShell telepítése a homebrew-val, az Eltávolítás ördöngösség:

```sh
brew cask uninstall powershell
```

Ha közvetlen letöltésére keresztül telepített, a PowerShell, PowerShell manuálisan kell eltávolítani:

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

Távolítsa el a további PowerShell-elérési utak, tekintse meg a [elérési utak][] szakaszt ebben a dokumentumban, és távolítsa el a kívánt az elérési utak használata `sudo rm`.

> [!NOTE]
> Ez nem szükséges, ha a telepítést a homebrew-val.

[Elérési utak]:#paths

## <a name="paths"></a>Elérési utak

* `$PSHOME` van `/usr/local/microsoft/powershell/6.0.2/`
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
Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.0.2/`, és a szimbolikus van elhelyezve `/usr/local/bin/pwsh`.

## <a name="additional-resources"></a>További források

* [Webes homebrew-val][brew]
* [Github-adattár homebrew-val][GitHub]
* [Homebrew-val – Cask][cask]


[brew]: http://brew.sh/
[GitHub]: https://github.com/Homebrew
[Cask]: https://github.com/Homebrew/homebrew-cask
[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
