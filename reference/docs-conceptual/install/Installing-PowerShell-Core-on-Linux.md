---
title: A PowerShell Core telepítése Linux rendszerre
description: Információk a PowerShell Core különböző Linux-disztribúciókban való telepítéséről
ms.date: 07/19/2019
ms.openlocfilehash: 929b153ef784f3203cd31a0e2fc52e744a07532f
ms.sourcegitcommit: 118eb294d5a84a772e6449d42a9d9324e18ef6b9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/22/2019
ms.locfileid: "68372195"
---
# <a name="installing-powershell-core-on-linux"></a>A PowerShell Core telepítése Linux rendszerre

Támogatja az [Ubuntu 16,04][u16], [Ubuntu 18.04][u1804], [Ubuntu 18,10][u1810], [Debian 9][deb9],
 [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42,3][opensuse], [openSUSE LEAP 15][opensuse] , [Fedora 27][fedora], [Fedora 28][Fedora]és [Arch Linux][arch].

A hivatalosan nem támogatott Linux-disztribúciók esetében a PowerShell [beépülő modullal][snap]próbálhatja meg telepíteni a PowerShellt. A PowerShell bináris fájljait közvetlenül a Linux [ `tar.gz` Archive][tar]használatával is kipróbálhatja, de az operációs rendszertől eltérő lépések alapján kell beállítania a szükséges függőségeket.

Minden csomag elérhető a GitHub- [releases][] oldalán. A csomag telepítése után futtassa `pwsh` a parancsot egy terminálról.

[u16]: #ubuntu-1604
[u1804]: #ubuntu-1804
[u1810]: #ubuntu-1810
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse
[fedora]: #fedora
[arch]: #arch-linux
[snap]: #snap-package
[tar]: #binary-archives

## <a name="installing-preview-releases"></a>Előzetes verziók telepítése

Ha a Linux rendszerhez készült `powershell` `powershell-preview`PowerShell Core Preview kiadását csomag-adattáron keresztül telepíti, a csomag neve a verzióról a verzióra változik.

A közvetlen letöltésen keresztüli telepítés nem változik, a fájlnévtől eltérő módon.

A következő táblázat tartalmazza a stabil és előnézeti csomagok telepítéséhez szükséges parancsokat a különböző csomagkezelő-kezelők használatával:

|Eloszlás (ok)|Stabil parancs | Előnézet parancs |
|---------------|---------------|-----------------|
| Ubuntu, Debian |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| CentOS, RedHat |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| Fedora   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1604"></a>Ubuntu 16.04

### <a name="installation-via-package-repository---ubuntu-1604"></a>Telepítés a Package repository használatával – Ubuntu 16,04

A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében a csomagok tárházában van közzétéve.

Az előnyben részesített módszer a következő:

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat. A regisztrációt követően frissítheti a PowerShellt a `sudo apt-get upgrade powershell`használatával.

### <a name="installation-via-direct-download---ubuntu-1604"></a>Telepítés közvetlen letöltéssel – Ubuntu 16,04

Töltse le a Debian `powershell_6.2.0-1.ubuntu.16.04_amd64.deb` -csomagot a [releases][] lapról az Ubuntu-gépre.

Ezután a terminálon hajtsa végre a következő parancsokat:

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` parancs nem teljesíti a nem kielégíthető függőségeket. A következő parancs megoldja `apt-get install -f` ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálását.

### <a name="uninstallation---ubuntu-1604"></a>Eltávolítás – Ubuntu 16,04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a>Ubuntu 18.04

### <a name="installation-via-package-repository---ubuntu-1804"></a>Telepítés a Package repository használatával – Ubuntu 18,04

A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében a csomagok tárházában van közzétéve.

Az előnyben részesített módszer a következő:

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Enable the "universe" repositories
sudo add-apt-repository universe

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat. A regisztrációt követően frissítheti a PowerShellt a `sudo apt-get upgrade powershell`használatával.

### <a name="installation-via-direct-download---ubuntu-1804"></a>Telepítés közvetlen letöltéssel – Ubuntu 18,04

Töltse le a Debian `powershell_6.2.0-1.ubuntu.18.04_amd64.deb` -csomagot a [releases][] lapról az Ubuntu-gépre.

Ezután a terminálon hajtsa végre a következő parancsokat:

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> A `dpkg -i` parancs nem teljesíti a nem kielégíthető függőségeket. A következő parancs megoldja `apt-get install -f` ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálását.

### <a name="uninstallation---ubuntu-1804"></a>Eltávolítás – Ubuntu 18,04

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a>Ubuntu 18,10

> [!NOTE]
> Mivel a 18,10 egy [közbenső kiadás](https://www.ubuntu.com/about/release-cycle), csak a [Közösség támogatja](https://docs.microsoft.com/en-us/powershell/scripting/powershell-support-lifecycle?view=powershell-6).

A (z `snapd`) 18,10-es telepítése a rendszeren támogatott. A teljes körű utasításokért lásd a [snap csomag][snap] című témakört.

## <a name="debian-8"></a>Debian 8

### <a name="installation-via-package-repository---debian-8"></a>Telepítés a Package repository használatával – Debian 8

A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében a csomagok tárházában van közzétéve.

Az előnyben részesített módszer a következő:

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

Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat. A regisztrációt követően frissítheti a PowerShellt a `sudo apt-get upgrade powershell`használatával.

## <a name="debian-9"></a>Debian 9

### <a name="installation-via-package-repository---debian-9"></a>Telepítés a Package repository használatával – Debian 9

A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében a csomagok tárházában van közzétéve.

Az előnyben részesített módszer a következő:

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

Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat. A regisztrációt követően frissítheti a PowerShellt a `sudo apt-get upgrade powershell`használatával.

### <a name="installation-via-direct-download---debian-9"></a>Telepítés közvetlen letöltéssel – Debian 9

Töltse le a Debian `powershell_6.2.0-1.debian.9_amd64.deb` -csomagot a [releases][] lapról a Debian rendszerű gépre.

Ezután a terminálon hajtsa végre a következő parancsokat:

```sh
sudo dpkg -i powershell_6.2.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a>Eltávolítás – Debian 9

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a>CentOS 7

> [!NOTE]
> Ez a csomag Oracle Linux 7 rendszeren működik.

### <a name="installation-via-package-repository-preferred---centos-7"></a>Telepítés a Package repository használatával (előnyben részesített) – CentOS 7

A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében közzé van téve a hivatalos Microsoft-Tárházak számára.

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat. A regisztrációt követően frissítheti a PowerShellt a `sudo yum update powershell`használatával.

### <a name="installation-via-direct-download---centos-7"></a>Telepítés közvetlen letöltéssel – CentOS 7

A [CentOS 7][]használatával töltse le az RPM `powershell-6.2.0-1.rhel.7.x86_64.rpm` -csomagot a [releases][] lapról a CentOS gépre.

Ezután a terminálon hajtsa végre a következő parancsokat:

```sh
sudo yum install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

Az RPM a letöltés közbenső lépése nélkül is telepíthető:

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a>Eltávolítás – CentOS 7

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a>Red Hat Enterprise Linux (RHEL) 7

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a>Telepítés a Package repository használatával (előnyben részesített) – Red Hat Enterprise Linux (RHEL) 7

A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében közzé van téve a hivatalos Microsoft-Tárházak számára.

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat. A regisztrációt követően frissítheti a PowerShellt a `sudo yum update powershell`használatával.

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a>Telepítés közvetlen letöltésen keresztül – Red Hat Enterprise Linux (RHEL) 7

Töltse le az RPM `powershell-6.2.0-1.rhel.7.x86_64.rpm` -csomagot a [releases][] lapról a Red Hat Enterprise Linux gépre.

Ezután a terminálon hajtsa végre a következő parancsokat:

```sh
sudo yum install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

Az RPM a letöltés közbenső lépése nélkül is telepíthető:

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a>Eltávolítás – Red Hat Enterprise Linux (RHEL) 7

```sh
sudo yum remove powershell
```

## <a name="opensuse"></a>openSUSE

### <a name="installation---opensuse-423"></a>Telepítés – openSUSE 42,3

```sh
# Install dependencies
zypper update && zypper --non-interactive install curl tar libicu52_1

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-linux-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
mkdir -p /opt/microsoft/powershell/6.2.0

# Expand powershell to the target folder
tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.2.0

# Set execute permissions
chmod +x /opt/microsoft/powershell/6.2.0/pwsh

# Create the symbolic link that points to pwsh
ln -s /opt/microsoft/powershell/6.2.0/pwsh /usr/bin/pwsh

# Start PowerShell
pwsh
```

### <a name="installation---opensuse-leap-15"></a>Telepítés – openSUSE LEAP 15

```sh
# Install dependencies
zypper update && zypper --non-interactive install curl tar gzip libopenssl1_0_0 libicu60_2

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-linux-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
mkdir -p /opt/microsoft/powershell/6.2.0

# Expand powershell to the target folder
tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.2.0

# Set execute permissions
chmod +x /opt/microsoft/powershell/6.2.0/pwsh

# Create the symbolic link that points to pwsh
ln -s /opt/microsoft/powershell/6.2.0/pwsh /usr/bin/pwsh

# Start PowerShell
pwsh
```

### <a name="uninstallation---opensuse-423-opensuse-leap-15"></a>Eltávolítás – openSUSE 42,3, openSUSE – 15. Ugrás

```sh
rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="fedora"></a>Fedora

> [!NOTE]
> A Fedora 28 csak a PowerShell Core 6,1-es és újabb verzióiban támogatott.

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a>Telepítés a Package repository használatával (preferált) – Fedora 27, Fedora 28

A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében közzé van téve a hivatalos Microsoft-Tárházak számára.

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a>Telepítés közvetlen letöltésen keresztül – Fedora 27, Fedora 28

Töltse le az RPM `powershell-6.2.0-1.rhel.7.x86_64.rpm` -csomagot a [releases][] lapról a Fedora gépre.

Ezután a terminálon hajtsa végre a következő parancsokat:

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

Az RPM a letöltés közbenső lépése nélkül is telepíthető:

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a>Eltávolítás – Fedora 27, Fedora 28

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a>Arch Linux

> [!NOTE]
> Az Arch-támogatás kísérleti jellegű.

A PowerShell az [Arch Linux][] User adattárból (Aur) érhető el.

* A [legújabb címkézett kiadással][arch-release] állítható össze
* A [legutóbbi véglegesítés][arch-git] a főkiszolgálóról lefordítható
* A [legújabb kiadási bináris][arch-bin] fájl használatával telepíthető.

A rendszer karbantartja a csomagokat az AUR-ban; nincs hivatalos támogatás.

A csomagok az AUR-ból való telepítésével kapcsolatos további információkért tekintse meg az [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a közösségi [Docker](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile)című témakört.

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a>Csomag igazítása

### <a name="getting-snapd"></a>Beépülő modul beolvasása

`snapd`a illesztések futtatásához szükséges. [Ezeket az utasításokat követve](https://docs.snapcraft.io/core/install) ellenőrizze, hogy `snapd` telepítve van-e.

### <a name="installation-via-snap"></a>Telepítés snap használatával

A Linux rendszerhez készült PowerShell Core a könnyű telepítés és frissítés érdekében a [snap áruházban](https://snapcraft.io/store) van közzétéve.

Az előnyben részesített módszer a következő:

```sh
# Install PowerShell
sudo snap install powershell --classic

# Start PowerShell
pwsh
```

Az előzetes verzió telepítéséhez használja a következő metódust:

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

A telepítés után a Snap automatikusan frissül. A frissítést a vagy `sudo snap refresh powershell` `sudo snap refresh powershell-preview`a használatával aktiválhatja.

### <a name="uninstallation"></a>Uninstallation

```sh
sudo snap remove powershell
```

vagy a

```sh
sudo snap remove powershell-preview
```

## <a name="kali"></a>Kali

### <a name="installation---kali"></a>Telepítés – Kali

```sh
# Download & Install prerequisites
wget http://ftp.us.debian.org/debian/pool/main/i/icu/libicu57_57.1-6+deb9u2_amd64.deb
dpkg -i libicu57_57.1-6+deb9u2_amd64.deb
apt-get update && apt-get install -y curl gnupg apt-transport-https

# Add Microsoft public repository key to APT
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -

# Add Microsoft package repository to the source list
echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" | tee /etc/apt/sources.list.d/powershell.list

# Install PowerShell package
apt-get update && apt-get install -y powershell

# Start PowerShell
pwsh
```

### <a name="uninstallation---kali"></a>Eltávolítás – Kali

```sh
# Uninstall PowerShell package
apt-get remove -y powershell
```

## <a name="raspbian"></a>Raspbian

> [!NOTE]
> A Raspbian-támogatás kísérleti jellegű.

Jelenleg a PowerShell csak a Raspbian stretch esetében támogatott.

A CoreCLR és a PowerShell Core csak a pi 2 és a PI 3 rendszerű eszközökön működik, mint például a [PI Zero](https://github.com/dotnet/coreclr/issues/10605), nem támogatott processzorral rendelkezik.

Töltse le a [Raspbian stretch](https://www.raspberrypi.org/downloads/raspbian/) -t, és kövesse a [telepítési utasításokat](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) a PI-re való lekéréséhez.

### <a name="installation---raspbian"></a>Telepítés – Raspbian

```sh
###################################
# Prerequisites

# Update package lists
sudo apt-get update

# Install libunwind8 and libssl1.0
# Regex is used to ensure that we do not install libssl1.0-dev, as it is a variant that is not required
sudo apt-get install '^libssl1.0.[0-9]$' libunwind8 -y

###################################
# Download and extract PowerShell

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.2.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

A PowerShell indításához a `pwsh` bináris elérési út megadása nélkül is létrehozhat egy szimbolikus hivatkozást.

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

## <a name="binary-archives"></a>Bináris archívumok

A speciális `tar.gz` üzembe helyezési forgatókönyvek lehetővé tétele érdekében a PowerShell bináris archívumokat a linuxos platformokhoz biztosítjuk.

### <a name="dependencies"></a>Függőségek

A PowerShell hordozható bináris fájlokat hoz létre az összes Linux-disztribúcióhoz. A .NET Core-futtatókörnyezet azonban eltérő függőségeket igényel a különböző disztribúciók esetében, és a PowerShell is.

A következő diagram a .NET Core 2,0-függőségeket mutatja be, amelyek a különböző Linux-disztribúciókban hivatalosan támogatottak.

| Operációs rendszer                 | Függőségek |
| ------------------ | ------------ |
| Ubuntu 16.04       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl 1.0.0, libicu55 |
| Ubuntu 17,10       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl 1.0.0, libicu57 |
| Ubuntu 18.04       | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl 1.0.0, libicu60 |
| Debian 8 (Jessie)  | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl 1.0.0, libicu52 |
| Debian 9 (stretch) | libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6, <br> libcurl3, libunwind8, libuuid1, zlib1g, libssl 1.0.2, libicu57 |
| CentOS 7 <br> Oracle Linux 7 <br> 7\. RHEL | libunwind, libcurl, OpenSSL-libs, libicu |
| openSUSE 42,3 | libcurl4, libopenssl1_0_0, libicu52_1 |
| openSUSE – 15. Ugrás | libcurl4, libopenssl1_0_0, libicu60_2 |
| Fedora 27 <br> Fedora 28 | libunwind, libcurl, OpenSSL-libs, libicu, kompatibilitás – openssl10 |

A nem hivatalosan támogatott Linux-disztribúciók PowerShell-bináris fájljainak telepítéséhez külön lépésben kell telepítenie a cél operációs rendszerhez szükséges függőségeket. Például az [Amazon Linux-Docker][amazon-dockerfile] először telepíti a függőségeket, majd kibontja `tar.gz` a Linux-archívumot.

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell-Docker/blob/master/release/community-stable/amazonlinux/docker/Dockerfile

### <a name="installation---binary-archives"></a>Telepítés – bináris archívumok

#### <a name="linux"></a>Linux

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.2.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.2.0

# Set execute permissions
sudo chmod +x /opt/microsoft/powershell/6.2.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.2.0/pwsh /usr/bin/pwsh
```

### <a name="uninstalling-binary-archives"></a>Bináris archívumok eltávolítása

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a>Elérési utak

* `$PSHOME`van`/opt/microsoft/powershell/6.2.0/`
* A rendszer beolvassa a felhasználói profilokat`~/.config/powershell/profile.ps1`
* Az alapértelmezett profilok a következő címről lesznek beolvasva:`$PSHOME/profile.ps1`
* A felhasználói modulok a következő címről lesznek beolvasva:`~/.local/share/powershell/Modules`
* A megosztott modulok a következő címről lesznek beolvasva:`/usr/local/share/powershell/Modules`
* Az alapértelmezett modulok a következő címről lesznek beolvasva:`$PSHOME/Modules`
* A PSReadline előzményei a következőre lesznek rögzítve`~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

A profilok figyelembe veszik a PowerShell gazdagép-konfigurációját, így az alapértelmezett gazdagép-specifikus profilok `Microsoft.PowerShell_profile.ps1` ugyanabban a helyen találhatók.

A PowerShell tiszteletben tartja a [XDG alap könyvtár specifikációját][xdg-bds] a Linux rendszeren.

[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
