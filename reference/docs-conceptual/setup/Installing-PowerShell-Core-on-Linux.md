# <a name="installing-powershell-core-on-linux"></a>A PowerShell Core telepítése Linux rendszerre

Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.10][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].

A Linux terjesztéseket, amelyek hivatalosan nem támogatottak, próbálkozhat a [PowerShell AppImage][lai].
Közvetlenül a Linux-használat PowerShell bináris fájljainak telepítéséhez is megpróbálhatja [ `tar.gz` archív][tar], de állítsa be a szükséges függőségek az operációs rendszer, a különálló lépések alapján kell.

Minden csomagok érhetők el a githubon [kiadott][] lap.
A csomag telepítése után futtassa `pwsh` terminálról.

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u17]: #ubuntu-1710
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-422
[fedora]: #fedora
[arch]: #arch-linux
[lai]: #linux-appimage
[tar]: #binary-archives

## <a name="installing-preview-releases"></a>Előzetes kiadások telepítése

PowerShell Core előzetes kiadás egy csomag tárház keresztül Linux telepítésekor a csomag nevét a változik `powershell` való `powershell-preview`.

Közvetlen letöltési keresztül telepítése nem változik, a fájl neve eltérő.

Íme egy tábla a parancsok a különböző csomag-kezelők használatával stabil és preview-csomagok:

|Distrobution(s)|Stabil parancs | Előzetes parancs |
|---------------|---------------|-----------------|
| Ubuntu, Debian |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| CentOS, RedHat |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| openSUSE |`sudo zypper install powershell` | `sudo zypper install powershell-preview`|
| Fedora   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a>Ubuntu 14.04

### <a name="installation-via-package-repository---ubuntu-1404"></a>Telepítési csomag tárház - Ubuntu 14.04 keresztül

PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).
Ez az elsődleges módszer.

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/14.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Felügyelő, mint a Microsoft-tárház regisztrálni.
Ettől kezdve csak kell használnia `sudo apt-get upgrade powershell` a telepítés frissítéséhez.

### <a name="installation-via-direct-download---ubuntu-1404"></a>Közvetlen letöltése – Ubuntu 14.04 történő telepítést

A Debian csomag `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.

A terminálban majd hajtsa végre az alábbiakat:

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` unmet függőségekkel rendelkező parancs meghiúsul.
> A következő parancs `apt-get install -f` megoldja a problémát, majd a PowerShell-csomag konfigurálása befejeződik.

### <a name="uninstallation---ubuntu-1404"></a>Az Eltávolítás - Ubuntu 14.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a>Ubuntu 16.04

### <a name="installation-via-package-repository---ubuntu-1604"></a>Telepítési csomag tárház - Ubuntu 16.04 keresztül

PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).
Ez az elsődleges módszer.

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/16.04/prod.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.

### <a name="installation-via-direct-download---ubuntu-1604"></a>Közvetlen letöltése – Ubuntu 16.04 történő telepítést

A Debian csomag `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.

A terminálban majd hajtsa végre az alábbiakat:

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` unmet függőségekkel rendelkező parancs meghiúsul.
> A következő parancs `apt-get install -f` megoldja a problémát, majd a PowerShell-csomag konfigurálása befejeződik.

### <a name="uninstallation---ubuntu-1604"></a>Az Eltávolítás - Ubuntu 16.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1710"></a>Ubuntu 17.10

> [!NOTE]
> Ubuntu 17.04 támogatása után lett hozzáadva. `6.1.0-preview.2`

### <a name="installation-via-package-repository---ubuntu-1710"></a>Telepítési csomag tárház - Ubuntu 17.10 keresztül

PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).
Ez az elsődleges módszer.

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/17.10/prod.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.

### <a name="installation-via-direct-download---ubuntu-1710"></a>Közvetlen letöltése – Ubuntu 17.10 történő telepítést

A Debian csomag `powershell_6.0.2-1.ubuntu.17.10_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.

A terminálban majd hajtsa végre az alábbiakat:

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.17.10_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` unmet függőségekkel rendelkező parancs meghiúsul.
> A következő parancs `apt-get install -f` megoldja a problémát, majd a PowerShell-csomag konfigurálása befejeződik.

### <a name="uninstallation---ubuntu-1710"></a>Az Eltávolítás - Ubuntu 17.10

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a>Ubuntu 18.04

> [!NOTE]
> Ubuntu 18.04 támogatása után lett hozzáadva. `6.1.0-preview.2`

### <a name="installation-via-package-repository---ubuntu-1804"></a>Telepítési csomag tárház - Ubuntu 18.04 keresztül

PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).
Ez az elsődleges módszer.

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.

### <a name="installation-via-direct-download---ubuntu-1804"></a>Közvetlen letöltése – Ubuntu 18.04 történő telepítést

A Debian csomag `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.

A terminálban majd hajtsa végre az alábbiakat:

```sh
sudo dpkg -i powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` unmet függőségekkel rendelkező parancs meghiúsul.
> A következő parancs `apt-get install -f` megoldja a problémát, majd a PowerShell-csomag konfigurálása befejeződik.

### <a name="uninstallation---ubuntu-1710"></a>Az Eltávolítás - Ubuntu 17.10

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a>Debian 8

### <a name="installation-via-package-repository---debian-8"></a>Telepítési csomag tárház - Debian 8 keresztül

PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).
Ez az elsődleges módszer.

```sh
# Install system components
sudo apt-get update
sudo apt-get install curl apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-jessie-prod jessie main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.

### <a name="installation-via-direct-download---debian-8"></a>Keresztül közvetlen letöltése – Debian 8 telepítése

A Debian csomag `powershell_6.0.2-1.debian.8_amd64.deb` a a [kiadott][] a Debian gép oldalon.

A terminálban majd hajtsa végre az alábbiakat:

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` unmet függőségekkel rendelkező parancs meghiúsul.
> A következő parancs `apt-get install -f` megoldja a problémát, majd a PowerShell-csomag konfigurálása befejeződik.

### <a name="uninstallation---debian-8"></a>Az Eltávolítás - Debian 8

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a>Debian 9

### <a name="installation-via-package-repository---debian-9"></a>Telepítési csomag tárház – Debian 9 keresztül

PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).
Ez az elsődleges módszer.

```sh
# Install system components
sudo apt-get update
sudo apt-get install curl gnupg apt-transport-https

# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Product feed
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/microsoft.list'

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.

### <a name="installation-via-direct-download---debian-9"></a>Közvetlen letöltése – Debian 9 történő telepítést

A Debian csomag `powershell_6.0.2-1.debian.9_amd64.deb` a a [kiadott][] a Debian gép oldalon.

A terminálban majd hajtsa végre az alábbiakat:

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a>Az Eltávolítás - Debian 9

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a>CentOS 7

> [!NOTE]
> Ez a csomag is működik-e az Oracle Linux 7.

### <a name="installation-via-package-repository-preferred---centos-7"></a>Telepítési csomag tárház (ajánlott) – CentOS 7 keresztül

Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.

### <a name="installation-via-direct-download---centos-7"></a>Közvetlen letöltése – CentOS 7 történő telepítést

Használatával [CentOS 7][], a RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a CentOS gép oldalon.

A terminálban majd hajtsa végre az alábbiakat:

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

A RPM nélkül letölti a köztes lépés is telepíthet:

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a>Az Eltávolítás - CentOS 7

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a>Red Hat Enterprise Linux (RHEL) 7

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a>Telepítési csomag tárház (ajánlott) - Red Hat Enterprise Linux (RHEL) 7 keresztül

Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a>Közvetlen letöltése – Red Hat Enterprise Linux (RHEL) 7 történő telepítést

A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a Red Hat Enterprise Linux-gép oldalon.

A terminálban majd hajtsa végre az alábbiakat:

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

A RPM nélkül letölti a köztes lépés is telepíthet:

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a>Az Eltávolítás - Red Hat Enterprise Linux (RHEL) 7

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a>OpenSUSE 42.2

PowerShell központ telepítésekor `zypper` előfordulhat, hogy a következő hiba jelentését:

```Output
Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
 Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
 Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
```

Ebben az esetben ellenőrizze, hogy a kompatibilis `libcurl` könyvtár megtalálható úgy, hogy a következő parancsot a jeleníti meg a `libcurl4` csomag telepítve:

```sh
zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
```

Válassza ki a `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` megoldás a PowerShell csomag telepítésekor.

### <a name="installation-via-package-repository-preferred---opensuse-422"></a>Telepítési csomag tárház (ajánlott) - OpenSUSE 42.2 keresztül

Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Add the Microsoft Product feed
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/zypp/repos.d/microsoft.repo

# Update the list of products
sudo zypper update

# Install PowerShell
sudo zypper install powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---opensuse-422"></a>Közvetlen letöltése – OpenSUSE 42.2 történő telepítést

A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a OpenSUSE gép oldalon.

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

A RPM nélkül letölti a köztes lépés is telepíthet:

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a>Az Eltávolítás - OpenSUSE 42.2

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a>Fedora

> [!NOTE]
> Fedora 28 csak akkor támogatott, a PowerShell Core 6.1 vagy újabb.

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a>Telepítési csomag tárház (ajánlott) - Fedora 27 Fedora 28 keresztül

Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Update the list of products
sudo dnf update

# Install a system component
sudo dnf install compat-openssl10

# Install PowerShell
sudo dnf install -y powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a>Közvetlen letöltése – Fedora 27, Fedora 28 történő telepítést

A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a Fedora gép oldalon.

A terminálban majd hajtsa végre az alábbiakat:

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

A RPM nélkül letölti a köztes lépés is telepíthet:

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a>Az Eltávolítás - Fedora 27, Fedora 28

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a>Linux architektúrája

> [!NOTE]
> Emelőkaros funkció kísérleti.

PowerShell érhető el a [architektúrája Linux][] felhasználói tárház (AUR).

* Az összeállítható a [legújabb címkézett kiadás][arch-release]
* Az összeállítható a [fő legújabb véglegesítési][arch-git]
* Használatával telepíthető a [bináris legújabb kiadás][arch-bin]

A AUR csomagok karbantartása közösségi – nincs hivatalos támogatás.

A csomagok telepítése a AUR a további információkért lásd: a [architektúrája Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a közösségi [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).

[architektúrája Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a>Linux AppImage

> [!NOTE]
> AppImage funkció kísérleti

A legutóbbi Linux-eloszlás használatával töltse le a AppImage `powershell-6.0.1-x86_64.AppImage` a a [kiadott][] a Linux-gépek oldalon.

A terminálban majd hajtsa végre az alábbiakat:

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

A [AppImage][] lehetővé teszi, hogy a telepítés nélküli PowerShell futtatásához.
Egy hordozható alkalmazás, amely a PowerShell és a függőségek (beleértve a .NET Core rendszer függőségeket) bundles egy javul csomagba.
Ez a csomag, amely a felhasználó a Linux-disztribúció függetlenül működik egy bináris.

[appimage]: http://appimage.org/

## <a name="kali"></a>Kali

> [!NOTE]
> Kali funkció kísérleti.

### <a name="installation"></a>Telepítés

```sh
# Download & Install prerequisites
sudo apt-get install libunwind8 libicu55
wget http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb
sudo dpkg -i libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb

# Install PowerShell
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb

# Start PowerShell
pwsh
```

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a>Futtassa a PowerShell legújabb Kali (Kali GNU/Linux folyamatos) a telepítés nélküli

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a>Az Eltávolítás - Kali

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a>Raspbian

> [!NOTE]
> Raspbian funkció kísérleti.

PowerShell jelenleg csak Raspbian Stretch támogatott.

Is CoreCLR (és így PowerShell Core) csak Pi 2 és Pi 3 eszközökön módon fog más eszközök, például [Pi nulla](https://github.com/dotnet/coreclr/issues/10605), egy nem támogatott processzorral rendelkezik.

Töltse le [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) , és kövesse a [telepítési utasításokat](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) a Pi eléréséhez.

### <a name="installation"></a>Telepítés

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.0.2-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

Nem kötelező elérési út megadását a "pwsh" bináris nélkül indítsa el a Powershellt szeretné szimbolikus hivatkozást hozhat létre

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a>Az Eltávolítás - Raspbian

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a>Bináris archívumokat

PowerShell bináris `tar.gz` archívumokat biztosított Linux-platformokhoz lehetővé központi telepítési forgatókönyveket.

### <a name="dependencies"></a>Függőségek

PowerShell alkot az összes Linux terjesztésekről hordozható bináris fájljait.
De a .NET Core runtime szükséges a különböző terjesztések átviteli különböző függőségek, és ezért PowerShell szerepe ugyanaz.

Az alábbi ábra mutatja a .NET Core 2.0 függőségek hivatalosan által támogatott különböző Linux terjesztéseket.

| Operációs rendszer                 | Függőségek |
| ------------------ | ------------ |
| Ubuntu 14.04       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52 |
| Ubuntu 16.04       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55 |
| Ubuntu 17.10       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57 |
| Ubuntu 18.04       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60 |
| Debian 8 (Jessie)  | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52 |
| Debian 9 (Stretch) | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57 |
| CentOS 7 <br> Oracle Linux 7 <br> RHEL 7 <br> OpenSUSE 42.2 | libunwind, libcurl, openssl-függvénytárak, libicu |
| 27 Fedora <br> 28 Fedora | libunwind, libcurl, openssl-függvénytárak, libicu, / compat-openssl10 |

Az telepítéséhez PowerShell bináris fájljait, a Linux terjesztéseket, amelyek hivatalosan nem támogatottak, kell telepíteni a cél operációs rendszer szükséges függőségek külön lépéseket.
Például a [Amazon Linux dockerfile] [ amazon-dockerfile] függőségek először telepíti, és kinyeri a Linux `tar.gz` archív.

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a>Telepítés – bináris archívumokat

#### <a name="linux"></a>Linux

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.0.2

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.0.2

# Set execute permissions
sudo chmod +x /opt/microsoft/powershell/6.0.2/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.0.2/pwsh /usr/bin/pwsh
```

### <a name="uninstalling-binary-archives"></a>Bináris archívumokat eltávolítása

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a>Elérési utak

* `$PSHOME` van `/opt/microsoft/powershell/6.0.2/`
* Felhasználói profilok rendszer nem olvas be `~/.config/powershell/profile.ps1`
* Alapértelmezett profilok rendszer nem olvas be `$PSHOME/profile.ps1`
* Modulok felhasználói rendszer nem olvas be `~/.local/share/powershell/Modules`
* Megosztott modulok rendszer nem olvas be `/usr/local/share/powershell/Modules`
* Az alapértelmezett modulokat rendszer nem olvas be `$PSHOME/Modules`
* A rögzítendő PSReadline előzmények `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

A profilok tiszteletben PowerShell gazdagép konfiguráció, így az alapértelmezett gazdagép-specifikus profilok létezik az `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.

PowerShell tiszteletben tartja a [XDG Base könyvtár megadása] [ xdg-bds] Linux rendszeren.

[kiadott]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
