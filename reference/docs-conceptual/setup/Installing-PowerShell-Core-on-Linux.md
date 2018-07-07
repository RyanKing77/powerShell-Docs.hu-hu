# <a name="installing-powershell-core-on-linux"></a>A PowerShell Core telepítése Linux rendszerre

Támogatja a [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.10] [ u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 27 ] [ fedora], [Fedora 28][fedora], és [Arch Linux][arch].

A hivatalosan nem támogatott Linux-disztribúció, megpróbálhatja használatával a [PowerShell AppImage][lai].
Üzembe helyezése a PowerShell bináris fájlokat közvetlenül a a Linux használatával is megpróbálhatja [ `tar.gz` archív][tar], de állítsa be a szükséges függőségek az operációs rendszer a különálló lépések alapján kell.

A githubon érhető el az összes csomag [kiadások][] lapot.
A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.

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

## <a name="installing-preview-releases"></a>Előzetes verziók telepítése

A PowerShell Core előzetes kiadás telepítése Linux rendszeren keresztül egy Csomagtárház esetén a csomag nevét a változik `powershell` való `powershell-preview`.

Közvetlen letöltésére keresztül telepítése nem változik, a fájl neve eltérő.

Íme egy táblát a parancsokat a különböző csomagkezelőinek használatával stabil és előzetes csomagok telepítéséhez:

|Distrobution(s)|Stabil parancs | A parancs előzetes verzió |
|---------------|---------------|-----------------|
| Ubuntu, a Debian |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| CentOS, a RedHat |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| OpenSUSE |`sudo zypper install powershell` | `sudo zypper install powershell-preview`|
| Fedora   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a>Ubuntu 14.04

### <a name="installation-via-package-repository---ubuntu-1404"></a>Telepítési Csomagtárház - Ubuntu 14.04-n keresztül

A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.
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

Superuser, mint a Microsoft-tárház regisztrálása.
Ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni a telepítés.

### <a name="installation-via-direct-download---ubuntu-1404"></a>Telepítési közvetlen letöltése – Ubuntu 14.04-n keresztül

A Debian csomag `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` származó a [kiadások][] az Ubuntu-gép oldalon.

Ezután hajtsa végre a következő billentyűparancsot a terminálon:

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.
> A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.

### <a name="uninstallation---ubuntu-1404"></a>Eltávolítás – Ubuntu 14.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a>Ubuntu 16.04

### <a name="installation-via-package-repository---ubuntu-1604"></a>Telepítési csomag tárház - Ubuntu 16.04-n keresztül

A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.
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

A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.

### <a name="installation-via-direct-download---ubuntu-1604"></a>Telepítési közvetlen letöltése – Ubuntu 16.04-n keresztül

A Debian csomag `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` származó a [kiadások][] az Ubuntu-gép oldalon.

Ezután hajtsa végre a következő billentyűparancsot a terminálon:

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.
> A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.

### <a name="uninstallation---ubuntu-1604"></a>Eltávolítás – Ubuntu 16.04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1710"></a>Ubuntu 17.10

> [!NOTE]
> Miután Ubuntu 17.04 támogatása hozzáadva `6.1.0-preview.2`

### <a name="installation-via-package-repository---ubuntu-1710"></a>Telepítési csomag tárház - Ubuntu 17.10-n keresztül

A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.
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

A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.

### <a name="installation-via-direct-download---ubuntu-1710"></a>Telepítési közvetlen letöltése – Ubuntu 17.10-n keresztül

A Debian csomag `powershell_6.0.2-1.ubuntu.17.10_amd64.deb` származó a [kiadások][] az Ubuntu-gép oldalon.

Ezután hajtsa végre a következő billentyűparancsot a terminálon:

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.17.10_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.
> A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.

### <a name="uninstallation---ubuntu-1710"></a>Eltávolítás – Ubuntu 17.10

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a>Ubuntu 18.04

> [!NOTE]
> Miután Ubuntu 18.04 támogatása hozzáadva `6.1.0-preview.2`

### <a name="installation-via-package-repository---ubuntu-1804"></a>Telepítési csomag tárház - Ubuntu 18.04-n keresztül

A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.
Ez az elsődleges módszer.

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell-preview

# Start PowerShell
pwsh
```

A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.

### <a name="installation-via-direct-download---ubuntu-1804"></a>Telepítési közvetlen letöltése – Ubuntu 18.04-n keresztül

A Debian csomag `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` származó a [kiadások][] az Ubuntu-gép oldalon.

Ezután hajtsa végre a következő billentyűparancsot a terminálon:

```sh
sudo dpkg -i powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.
> A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.

### <a name="uninstallation---ubuntu-1710"></a>Eltávolítás – Ubuntu 17.10

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a>Debian 8

### <a name="installation-via-package-repository---debian-8"></a>Telepítési Csomagtárház – Debian 8-n keresztül

A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.
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

A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.

### <a name="installation-via-direct-download---debian-8"></a>Keresztül közvetlen letöltése – Debian 8 telepítés

A Debian csomag `powershell_6.0.2-1.debian.8_amd64.deb` származó a [kiadások][] oldal arra a Debian gépre.

Ezután hajtsa végre a következő billentyűparancsot a terminálon:

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.
> A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.

### <a name="uninstallation---debian-8"></a>Eltávolítás – Debian 8

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a>Debian 9

### <a name="installation-via-package-repository---debian-9"></a>Telepítési csomag tárház – Debian 9-n keresztül

A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.
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

A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.

### <a name="installation-via-direct-download---debian-9"></a>Telepítési közvetlen letöltése – Debian 9-n keresztül

A Debian csomag `powershell_6.0.2-1.debian.9_amd64.deb` származó a [kiadások][] oldal arra a Debian gépre.

Ezután hajtsa végre a következő billentyűparancsot a terminálon:

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a>Eltávolítás – Debian 9

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a>CentOS 7

> [!NOTE]
> Ez a csomag az Oracle Linux 7 is működik.

### <a name="installation-via-package-repository-preferred---centos-7"></a>Telepítési csomag tárház (preferált) – CentOS 7-n keresztül

A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissíteni.

### <a name="installation-via-direct-download---centos-7"></a>Keresztül közvetlen letöltése – CentOS 7 telepítése

Használatával [CentOS 7][], töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadások][] oldal arra a CentOS-gépre.

Ezután hajtsa végre a következő billentyűparancsot a terminálon:

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a>Eltávolítás – CentOS 7

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a>Red Hat Enterprise Linux (RHEL) 7

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a>Telepítési csomag tárház (preferált) – Red Hat Enterprise Linux (RHEL) 7-n keresztül

A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissíteni.

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a>Telepítési közvetlen letöltése – Red Hat Enterprise Linux (RHEL) 7-n keresztül

Töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` származó a [kiadások][] oldal arra a Red Hat Enterprise Linux-gépre.

Ezután hajtsa végre a következő billentyűparancsot a terminálon:

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a>Eltávolítás – Red Hat Enterprise Linux (RHEL) 7

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a>OpenSUSE 42.2

A PowerShell Core, telepítésekor `zypper` feltétlenül jelentik a következő hibával:

```Output
Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
 Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
 Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
```

Ebben az esetben ellenőrizze, hogy a kompatibilis `libcurl` könyvtár megtalálható úgy, hogy a következő parancsot a látható a `libcurl4` csomag telepítve vannak:

```sh
zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
```

Majd válassza ki a `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` megoldáshoz, amikor a PowerShell-csomag telepítése.

### <a name="installation-via-package-repository-preferred---opensuse-422"></a>Telepítés (preferált) – Csomagtárház OpenSUSE 42.2 keresztül

A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.

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

### <a name="installation-via-direct-download---opensuse-422"></a>Telepítési közvetlen letöltése – OpenSUSE 42.2-n keresztül

Töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` származó a [kiadások][] lap arra az opensuse-alapú gépre.

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a>Eltávolítás – OpenSUSE 42.2

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a>Fedora

> [!NOTE]
> Fedora 28 csak akkor támogatott, a PowerShell Core 6.1-es és újabb.

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a>Telepítési csomag tárház (preferált) – Fedora 27., Fedora 28-n keresztül

A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a>Telepítési közvetlen letöltése – Fedora 27, Fedora 28-n keresztül

Töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` származó a [kiadások][] oldal arra a Fedora gépre.

Ezután hajtsa végre a következő billentyűparancsot a terminálon:

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a>Eltávolítás – Fedora 27., Fedora 28

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a>Arch Linux

> [!NOTE]
> A rendszer kísérleti emelőkaros támogatja.

PowerShell érhető el a [Arch Linux][] felhasználói tárház (AUR).

* Az összeállítható a [legújabb címkézett kiadás][arch-release]
* Az összeállítható a [fő a legutóbbi véglegesítést][arch-git]
* Használatával telepíthető a [legújabb kibocsátási bináris][arch-bin]

A AUR csomagok közösségi kezelt – nem hivatalos támogatott.

A AUR a csomagok telepítésével kapcsolatos további információkért lásd: a [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a Közösség [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a>Linux AppImage

> [!NOTE]
> AppImage támogatási je experimentální.

Legutóbbi Linux-disztribúció használatával töltse le a AppImage `powershell-6.0.1-x86_64.AppImage` származó a [kiadások][] oldal arra a Linux-gépre.

Ezután hajtsa végre a következő billentyűparancsot a terminálon:

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

A [AppImage][] teszi lehetővé a PowerShell futtatása nélkül telepíti azt.
Egy hordozható alkalmazást, amely a PowerShell és annak függőségeit, (beleértve a .NET Core rendszerfüggőségekben) bundles javul csomagba.
A csomag nincs egyetlen bináris, amely a felhasználó Linux-disztribúció függetlenül működik.

[appimage]: http://appimage.org/

## <a name="kali"></a>Kali

> [!NOTE]
> Kali támogatási je experimentální.

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

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a>Futtassa a Powershellt a legújabb Kali (GNU/Linux folyamatos Kali) azt telepítése nélkül

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a>Eltávolítás – Kali

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a>Raspbian

> [!NOTE]
> Raspbian támogatási je experimentální.

PowerShell jelenleg csak a Raspbian Stretch támogatott.

Emellett coreclr-nek (és így a PowerShell Core) csak 2 tartományban és Pi 3 eszközökön módon fog más eszközök, például [Pi nulla](https://github.com/dotnet/coreclr/issues/10605), egy nem támogatott processzorral rendelkezik.

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

Igény szerint hozhat létre a szimbolikus hivatkozást úgy, hogy tudni indítsa el a Powershellt, a "pwsh" bináris elérési út megadása nélkül

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a>Eltávolítás – Raspbian

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a>Bináris archívum

PowerShell bináris `tar.gz` archívumok biztosított Linux-platformokhoz a speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé.

### <a name="dependencies"></a>Függőségek

PowerShell az összes Linux-disztribúciókra vonatkozó hordozható bináris épít fel.
De a .NET Core runtime szükséges különböző disztribúciókon különböző függőségek, és ezért PowerShell pedig ugyanezt.

A következő diagram a .NET Core 2.0 hivatalosan támogatott különböző Linux-disztribúciókon függőségeit jeleníti meg.

| Operációs rendszer                 | Függőségek |
| ------------------ | ------------ |
| Ubuntu 14.04       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52 |
| Ubuntu 16.04       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55 |
| Ubuntu 17.10       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57 |
| Ubuntu 18.04       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60 |
| Debian 8 (Jessie)  | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52 |
| Debian 9 (Nyújtás) | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57 |
| CentOS 7 <br> Oracle Linux 7 <br> RHEL 7 <br> OpenSUSE 42.2 | libunwind, libcurl, openssl-függvénytárak, libicu |
| Fedora 27 <br> 28 Fedora | libunwind, libcurl, openssl-függvénytárak, libicu, a/compat-openssl10 |

Nem hivatalosan támogatott Linux-disztribúciókon a PowerShell bináris fájljainak telepítéséhez telepíteni szeretné a cél operációs rendszer szükséges függőséget a különálló lépések.
Például a [Amazon Linux dockerfile] [ amazon-dockerfile] először telepíti a függőségeket, és ezt követően kiolvassa a Linuxos `tar.gz` archív.

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a>Telepítés – bináris archívum

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

### <a name="uninstalling-binary-archives"></a>Bináris archívum eltávolítása

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a>Elérési utak

* `$PSHOME` van `/opt/microsoft/powershell/6.0.2/`
* Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`
* Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`
* Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`
* Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`
* Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`
* PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

A profilok tiszteletben PowerShell a gazdagép konfiguráció, így az alapértelmezett gazdagép-specifikus profilok létezik `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.

PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] Linux rendszeren.

[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
