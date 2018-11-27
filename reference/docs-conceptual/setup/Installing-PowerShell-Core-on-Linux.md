---
title: A PowerShell Core telepítése Linux rendszerre
description: Információ a különböző Linux-disztribúciókon a PowerShell Core telepítése
ms.date: 08/06/2018
ms.openlocfilehash: afb11f053517af592fe42754d543f9f4a9966c5b
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/27/2018
ms.locfileid: "52321111"
---
# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="1758c-103">A PowerShell Core telepítése Linux rendszerre</span><span class="sxs-lookup"><span data-stu-id="1758c-103">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="1758c-104">Támogatja a [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.04] [ u1804], [Ubuntu 18.10][u1810], [Debian 8][deb8], [Debian 9] [ deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42.3][opensuse], [openSUSE Leap 15][opensuse], [Fedora 27][fedora], [ Fedora 28][fedora], és [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="1758c-104">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.04][u1804], [Ubuntu 18.10][u1810], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42.3][opensuse], [openSUSE Leap 15][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="1758c-105">A hivatalosan nem támogatott Linux-disztribúció, megpróbálhatja használatával a [PowerShell beépülő modul csomag][snap].</span><span class="sxs-lookup"><span data-stu-id="1758c-105">For Linux distributions that are not officially supported, you can try using the [PowerShell Snap Package][snap].</span></span>
<span data-ttu-id="1758c-106">Üzembe helyezése a PowerShell bináris fájlokat közvetlenül a a Linux használatával is megpróbálhatja [ `tar.gz` archív][tar], de állítsa be a szükséges függőségek az operációs rendszer a különálló lépések alapján kell.</span><span class="sxs-lookup"><span data-stu-id="1758c-106">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="1758c-107">A githubon érhető el az összes csomag [kiadások][] lapot.</span><span class="sxs-lookup"><span data-stu-id="1758c-107">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="1758c-108">A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="1758c-108">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u1804]: #ubuntu-1804
[u1810]: #ubuntu-1810
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse
[fedora]: #fedora
[arch]: #arch-linux
[snap]: #snap-package
[tar]: #binary-archives

## <a name="installing-preview-releases"></a><span data-ttu-id="1758c-109">Előzetes verziók telepítése</span><span class="sxs-lookup"><span data-stu-id="1758c-109">Installing Preview Releases</span></span>

<span data-ttu-id="1758c-110">A PowerShell Core előzetes kiadás telepítése Linux rendszeren keresztül egy Csomagtárház esetén a csomag nevét a változik `powershell` való `powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="1758c-110">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="1758c-111">Közvetlen letöltésére keresztül telepítése nem változik, a fájl neve eltérő.</span><span class="sxs-lookup"><span data-stu-id="1758c-111">Installing via direct download does not change, other than the file name.</span></span>

<span data-ttu-id="1758c-112">Íme egy táblát a parancsokat a különböző csomagkezelőinek használatával stabil és előzetes csomagok telepítéséhez:</span><span class="sxs-lookup"><span data-stu-id="1758c-112">Here is a table of the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="1758c-113">Distribution(s)</span><span class="sxs-lookup"><span data-stu-id="1758c-113">Distribution(s)</span></span>|<span data-ttu-id="1758c-114">Stabil parancs</span><span class="sxs-lookup"><span data-stu-id="1758c-114">Stable Command</span></span> | <span data-ttu-id="1758c-115">A parancs előzetes verzió</span><span class="sxs-lookup"><span data-stu-id="1758c-115">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="1758c-116">Ubuntu, a Debian</span><span class="sxs-lookup"><span data-stu-id="1758c-116">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="1758c-117">CentOS, a RedHat</span><span class="sxs-lookup"><span data-stu-id="1758c-117">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="1758c-118">Fedora</span><span class="sxs-lookup"><span data-stu-id="1758c-118">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a><span data-ttu-id="1758c-119">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="1758c-119">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="1758c-120">Telepítési Csomagtárház - Ubuntu 14.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-120">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="1758c-121">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="1758c-121">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="1758c-122">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="1758c-122">This is the preferred method.</span></span>

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/14.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="1758c-123">Superuser, mint a Microsoft-tárház regisztrálása.</span><span class="sxs-lookup"><span data-stu-id="1758c-123">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="1758c-124">Ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni a telepítés.</span><span class="sxs-lookup"><span data-stu-id="1758c-124">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="1758c-125">Telepítési közvetlen letöltése – Ubuntu 14.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-125">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="1758c-126">A Debian-csomag letöltése `powershell_6.1.0-1.ubuntu.14.04_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="1758c-126">Download the Debian package `powershell_6.1.0-1.ubuntu.14.04_amd64.deb`</span></span>
<span data-ttu-id="1758c-127">az a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="1758c-127">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="1758c-128">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="1758c-128">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="1758c-129">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="1758c-129">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="1758c-130">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="1758c-130">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="1758c-131">Eltávolítás – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="1758c-131">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="1758c-132">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="1758c-132">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="1758c-133">Telepítési csomag tárház - Ubuntu 16.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-133">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="1758c-134">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="1758c-134">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="1758c-135">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="1758c-135">This is the preferred method.</span></span>

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

<span data-ttu-id="1758c-136">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="1758c-136">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="1758c-137">Telepítési közvetlen letöltése – Ubuntu 16.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-137">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="1758c-138">A Debian-csomag letöltése `powershell_6.1.0-1.ubuntu.16.04_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="1758c-138">Download the Debian package `powershell_6.1.0-1.ubuntu.16.04_amd64.deb`</span></span>
<span data-ttu-id="1758c-139">az a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="1758c-139">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="1758c-140">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="1758c-140">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="1758c-141">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="1758c-141">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="1758c-142">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="1758c-142">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="1758c-143">Eltávolítás – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="1758c-143">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="1758c-144">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="1758c-144">Ubuntu 18.04</span></span>

> [!NOTE]
> <span data-ttu-id="1758c-145">Miután Ubuntu 18.04 támogatása hozzáadva `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="1758c-145">Support for Ubuntu 18.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="1758c-146">Telepítési csomag tárház - Ubuntu 18.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-146">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="1758c-147">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="1758c-147">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="1758c-148">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="1758c-148">This is the preferred method.</span></span>

```sh
# Download the Microsoft repository GPG keys
wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb

# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="1758c-149">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="1758c-149">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="1758c-150">Telepítési közvetlen letöltése – Ubuntu 18.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-150">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="1758c-151">A Debian-csomag letöltése `powershell_6.1.0-1.ubuntu.18.04_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="1758c-151">Download the Debian package `powershell_6.1.0-1.ubuntu.18.04_amd64.deb`</span></span>
<span data-ttu-id="1758c-152">az a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="1758c-152">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="1758c-153">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="1758c-153">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="1758c-154">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="1758c-154">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="1758c-155">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="1758c-155">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1804"></a><span data-ttu-id="1758c-156">Eltávolítás – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="1758c-156">Uninstallation - Ubuntu 18.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a><span data-ttu-id="1758c-157">Ubuntu 18.10</span><span class="sxs-lookup"><span data-stu-id="1758c-157">Ubuntu 18.10</span></span>

> [!NOTE]
> <span data-ttu-id="1758c-158">Ubuntu 18.10 támogatása hozzáadva után `6.1.0-preview.3`.</span><span class="sxs-lookup"><span data-stu-id="1758c-158">Support for Ubuntu 18.10 was added after `6.1.0-preview.3`.</span></span>
> <span data-ttu-id="1758c-159">Mivel 18.10 napi build, akkor csak a támogatott közösségi.</span><span class="sxs-lookup"><span data-stu-id="1758c-159">As 18.10 is a daily build, it is only community supported.</span></span>

<span data-ttu-id="1758c-160">Keresztül támogatott 18.10 telepítése `snapd`.</span><span class="sxs-lookup"><span data-stu-id="1758c-160">Installing on 18.10 is supported via `snapd`.</span></span> <span data-ttu-id="1758c-161">Lásd: [beépülő csomag] [ snap] teljes útmutatás;</span><span class="sxs-lookup"><span data-stu-id="1758c-161">See [Snap Package][snap] for full instructions;</span></span>

## <a name="debian-8"></a><span data-ttu-id="1758c-162">Debian 8</span><span class="sxs-lookup"><span data-stu-id="1758c-162">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="1758c-163">Telepítési Csomagtárház – Debian 8-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-163">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="1758c-164">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="1758c-164">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="1758c-165">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="1758c-165">This is the preferred method.</span></span>

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

<span data-ttu-id="1758c-166">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="1758c-166">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="1758c-167">Keresztül közvetlen letöltése – Debian 8 telepítés</span><span class="sxs-lookup"><span data-stu-id="1758c-167">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="1758c-168">A Debian-csomag letöltése `powershell_6.1.0-1.debian.8_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="1758c-168">Download the Debian package `powershell_6.1.0-1.debian.8_amd64.deb`</span></span>
<span data-ttu-id="1758c-169">az a [kiadások][] oldal arra a Debian gépre.</span><span class="sxs-lookup"><span data-stu-id="1758c-169">from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="1758c-170">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="1758c-170">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="1758c-171">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="1758c-171">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="1758c-172">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="1758c-172">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="1758c-173">Eltávolítás – Debian 8</span><span class="sxs-lookup"><span data-stu-id="1758c-173">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="1758c-174">Debian 9</span><span class="sxs-lookup"><span data-stu-id="1758c-174">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="1758c-175">Telepítési csomag tárház – Debian 9-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-175">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="1758c-176">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="1758c-176">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="1758c-177">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="1758c-177">This is the preferred method.</span></span>

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

<span data-ttu-id="1758c-178">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="1758c-178">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="1758c-179">Telepítési közvetlen letöltése – Debian 9-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-179">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="1758c-180">A Debian-csomag letöltése `powershell_6.1.0-1.debian.9_amd64.deb`</span><span class="sxs-lookup"><span data-stu-id="1758c-180">Download the Debian package `powershell_6.1.0-1.debian.9_amd64.deb`</span></span>
<span data-ttu-id="1758c-181">az a [kiadások][] oldal arra a Debian gépre.</span><span class="sxs-lookup"><span data-stu-id="1758c-181">from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="1758c-182">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="1758c-182">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="1758c-183">Eltávolítás – Debian 9</span><span class="sxs-lookup"><span data-stu-id="1758c-183">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="1758c-184">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="1758c-184">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="1758c-185">Ez a csomag az Oracle Linux 7 is működik.</span><span class="sxs-lookup"><span data-stu-id="1758c-185">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="1758c-186">Telepítési csomag tárház (preferált) – CentOS 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-186">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="1758c-187">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="1758c-187">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="1758c-188">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="1758c-188">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="1758c-189">Keresztül közvetlen letöltése – CentOS 7 telepítése</span><span class="sxs-lookup"><span data-stu-id="1758c-189">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="1758c-190">Használatával [CentOS 7][], töltse le az RPM-csomagot `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span><span class="sxs-lookup"><span data-stu-id="1758c-190">Using [CentOS 7][], download the RPM package `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span></span>
<span data-ttu-id="1758c-191">az a [kiadások][] oldal arra a CentOS-gépre.</span><span class="sxs-lookup"><span data-stu-id="1758c-191">from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="1758c-192">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="1758c-192">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="1758c-193">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="1758c-193">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="1758c-194">Eltávolítás – CentOS 7</span><span class="sxs-lookup"><span data-stu-id="1758c-194">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="1758c-196">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="1758c-196">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="1758c-197">Telepítési csomag tárház (preferált) – Red Hat Enterprise Linux (RHEL) 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-197">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="1758c-198">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="1758c-198">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="1758c-199">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="1758c-199">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="1758c-200">Telepítési közvetlen letöltése – Red Hat Enterprise Linux (RHEL) 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-200">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="1758c-201">Töltse le az RPM-csomagot `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span><span class="sxs-lookup"><span data-stu-id="1758c-201">Download the RPM package `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span></span>
<span data-ttu-id="1758c-202">az a [kiadások][] oldal arra a Red Hat Enterprise Linux-gépre.</span><span class="sxs-lookup"><span data-stu-id="1758c-202">from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="1758c-203">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="1758c-203">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="1758c-204">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="1758c-204">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="1758c-205">Eltávolítás – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="1758c-205">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse"></a><span data-ttu-id="1758c-206">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="1758c-206">openSUSE</span></span>

### <a name="installation---opensuse-423"></a><span data-ttu-id="1758c-207">Telepítés – openSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="1758c-207">Installation - openSUSE 42.3</span></span>

```sh
# Install dependencies
zypper update && zypper --non-interactive install curl tar libicu52_1

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-linux-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
mkdir -p /opt/microsoft/powershell/6.1.0

# Expand powershell to the target folder
tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.1.0

# Set execute permissions
chmod +x /opt/microsoft/powershell/6.1.0/pwsh

# Create the symbolic link that points to pwsh
ln -s /opt/microsoft/powershell/6.1.0/pwsh /usr/bin/pwsh

# Start PowerShell
pwsh
```

### <a name="installation---opensuse-leap-15"></a><span data-ttu-id="1758c-208">Telepítés – openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="1758c-208">Installation - openSUSE Leap 15</span></span>

```sh
# Install dependencies
zypper update && zypper --non-interactive install curl tar gzip libopenssl1_0_0 libicu60_2

# Download the powershell '.tar.gz' archive
curl -L https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-linux-x64.tar.gz -o /tmp/powershell.tar.gz

# Create the target folder where powershell will be placed
mkdir -p /opt/microsoft/powershell/6.1.0

# Expand powershell to the target folder
tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.1.0

# Set execute permissions
chmod +x /opt/microsoft/powershell/6.1.0/pwsh

# Create the symbolic link that points to pwsh
ln -s /opt/microsoft/powershell/6.1.0/pwsh /usr/bin/pwsh

# Start PowerShell
pwsh
```

### <a name="uninstallation---opensuse-423-opensuse-leap-15"></a><span data-ttu-id="1758c-209">Eltávolítás – openSUSE 42.3, openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="1758c-209">Uninstallation - openSUSE 42.3, openSUSE Leap 15</span></span>

```sh
rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="fedora"></a><span data-ttu-id="1758c-210">Fedora</span><span class="sxs-lookup"><span data-stu-id="1758c-210">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="1758c-211">Fedora 28 csak akkor támogatott, a PowerShell Core 6.1-es és újabb.</span><span class="sxs-lookup"><span data-stu-id="1758c-211">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="1758c-212">Telepítési csomag tárház (preferált) – Fedora 27., Fedora 28-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-212">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="1758c-213">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="1758c-213">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="1758c-214">Telepítési közvetlen letöltése – Fedora 27, Fedora 28-n keresztül</span><span class="sxs-lookup"><span data-stu-id="1758c-214">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="1758c-215">Töltse le az RPM-csomagot `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span><span class="sxs-lookup"><span data-stu-id="1758c-215">Download the RPM package `powershell-6.1.0-1.rhel.7.x86_64.rpm`</span></span>
<span data-ttu-id="1758c-216">az a [kiadások][] oldal arra a Fedora gépre.</span><span class="sxs-lookup"><span data-stu-id="1758c-216">from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="1758c-217">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="1758c-217">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.1.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="1758c-218">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="1758c-218">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="1758c-219">Eltávolítás – Fedora 27., Fedora 28</span><span class="sxs-lookup"><span data-stu-id="1758c-219">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="1758c-220">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="1758c-220">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="1758c-221">A rendszer kísérleti emelőkaros támogatja.</span><span class="sxs-lookup"><span data-stu-id="1758c-221">Arch support is experimental.</span></span>

<span data-ttu-id="1758c-222">PowerShell érhető el a [Arch Linux][] felhasználói tárház (AUR).</span><span class="sxs-lookup"><span data-stu-id="1758c-222">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="1758c-223">Az összeállítható a [legújabb címkézett kiadás][arch-release]</span><span class="sxs-lookup"><span data-stu-id="1758c-223">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="1758c-224">Az összeállítható a [fő a legutóbbi véglegesítést][arch-git]</span><span class="sxs-lookup"><span data-stu-id="1758c-224">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="1758c-225">Használatával telepíthető a [legújabb kibocsátási bináris][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="1758c-225">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="1758c-226">A AUR csomagok közösségi kezelt – nem hivatalos támogatott.</span><span class="sxs-lookup"><span data-stu-id="1758c-226">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="1758c-227">A AUR a csomagok telepítésével kapcsolatos további információkért lásd: a [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a Közösség [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="1758c-227">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a><span data-ttu-id="1758c-229">Oszlopokhoz illesztés csomag</span><span class="sxs-lookup"><span data-stu-id="1758c-229">Snap Package</span></span>

### <a name="getting-snapd"></a><span data-ttu-id="1758c-230">Első snapd</span><span class="sxs-lookup"><span data-stu-id="1758c-230">Getting snapd</span></span>

<span data-ttu-id="1758c-231">`snapd` Illesztés futtatásához szükség.</span><span class="sxs-lookup"><span data-stu-id="1758c-231">`snapd` is required to run snaps.</span></span>
<span data-ttu-id="1758c-232">Használat [ezek az utasítások](https://docs.snapcraft.io/core/install) , ellenőrizze, hogy `snapd` telepítve.</span><span class="sxs-lookup"><span data-stu-id="1758c-232">Use [these instructions](https://docs.snapcraft.io/core/install) to make sure you have `snapd` installed.</span></span>

### <a name="installation-via-snap"></a><span data-ttu-id="1758c-233">Keresztül beépülő modul telepítése</span><span class="sxs-lookup"><span data-stu-id="1758c-233">Installation via Snap</span></span>

<span data-ttu-id="1758c-234">A PowerShell Core, Linux esetén a rendszer közzéteszi az [beépülő store](https://snapcraft.io/store) egyszerű telepítéshez (és frissítések).</span><span class="sxs-lookup"><span data-stu-id="1758c-234">PowerShell Core, for Linux, is published to the [Snap store](https://snapcraft.io/store) for easy installation (and updates).</span></span>
<span data-ttu-id="1758c-235">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="1758c-235">This is the preferred method.</span></span>

```sh
# Install PowerShell
sudo snap install powershell --classic

# Start PowerShell
pwsh
```

<span data-ttu-id="1758c-236">Ha szeretne az előzetes verzió telepítése, a következő metódust.</span><span class="sxs-lookup"><span data-stu-id="1758c-236">If you want to install preview version, use following method.</span></span>

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

<span data-ttu-id="1758c-237">Után automatikusan beépülő modul telepítését frissíti, de egy frissítési használatával aktiválhat `sudo snap refresh powershell` vagy `sudo snap refresh powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="1758c-237">After installing Snap will automatically upgrade, but you can trigger an upgrade using `sudo snap refresh powershell` or `sudo snap refresh powershell-preview`.</span></span>

### <a name="uninstallation"></a><span data-ttu-id="1758c-238">Az Eltávolítás</span><span class="sxs-lookup"><span data-stu-id="1758c-238">Uninstallation</span></span>

```sh
sudo snap remove powershell
```

<span data-ttu-id="1758c-239">vagy a</span><span class="sxs-lookup"><span data-stu-id="1758c-239">or</span></span>

```sh
sudo snap remove powershell-preview
```

## <a name="kali"></a><span data-ttu-id="1758c-240">Kali</span><span class="sxs-lookup"><span data-stu-id="1758c-240">Kali</span></span>

### <a name="installation---kali"></a><span data-ttu-id="1758c-241">Telepítés – Kali</span><span class="sxs-lookup"><span data-stu-id="1758c-241">Installation - Kali</span></span>

```sh
# Download & Install prerequisites
wget http://ftp.us.debian.org/debian/pool/main/i/icu/libicu57_57.1-9_amd64.deb
dpkg -i libicu57_57.1-9_amd64.deb
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

### <a name="uninstallation---kali"></a><span data-ttu-id="1758c-242">Eltávolítás – Kali</span><span class="sxs-lookup"><span data-stu-id="1758c-242">Uninstallation - Kali</span></span>

```sh
# Uninstall PowerShell package
apt-get remove -y powershell
```

## <a name="raspbian"></a><span data-ttu-id="1758c-243">Raspbian</span><span class="sxs-lookup"><span data-stu-id="1758c-243">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="1758c-244">Raspbian támogatási je experimentální.</span><span class="sxs-lookup"><span data-stu-id="1758c-244">Raspbian support is experimental.</span></span>

<span data-ttu-id="1758c-245">PowerShell jelenleg csak a Raspbian Stretch támogatott.</span><span class="sxs-lookup"><span data-stu-id="1758c-245">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="1758c-246">Emellett coreclr-nek (és így a PowerShell Core) csak 2 tartományban és Pi 3 eszközökön módon fog más eszközök, például [Pi nulla](https://github.com/dotnet/coreclr/issues/10605), egy nem támogatott processzorral rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="1758c-246">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="1758c-247">Töltse le [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) , és kövesse a [telepítési utasításokat](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) a Pi eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="1758c-247">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation---raspbian"></a><span data-ttu-id="1758c-248">Telepítés – Raspbian</span><span class="sxs-lookup"><span data-stu-id="1758c-248">Installation - Raspbian</span></span>

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.1.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

<span data-ttu-id="1758c-249">Igény szerint hozhat létre a szimbolikus hivatkozást úgy, hogy tudni indítsa el a Powershellt, a "pwsh" bináris elérési út megadása nélkül</span><span class="sxs-lookup"><span data-stu-id="1758c-249">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="1758c-250">Eltávolítás – Raspbian</span><span class="sxs-lookup"><span data-stu-id="1758c-250">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="1758c-251">Bináris archívum</span><span class="sxs-lookup"><span data-stu-id="1758c-251">Binary Archives</span></span>

<span data-ttu-id="1758c-252">PowerShell bináris `tar.gz` archívumok biztosított Linux-platformokhoz a speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé.</span><span class="sxs-lookup"><span data-stu-id="1758c-252">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="1758c-253">Függőségek</span><span class="sxs-lookup"><span data-stu-id="1758c-253">Dependencies</span></span>

<span data-ttu-id="1758c-254">PowerShell az összes Linux-disztribúciókra vonatkozó hordozható bináris épít fel.</span><span class="sxs-lookup"><span data-stu-id="1758c-254">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="1758c-255">De a .NET Core runtime szükséges különböző disztribúciókon különböző függőségek, és ezért PowerShell pedig ugyanezt.</span><span class="sxs-lookup"><span data-stu-id="1758c-255">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="1758c-256">A következő diagram a .NET Core 2.0 hivatalosan támogatott különböző Linux-disztribúciókon függőségeit jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="1758c-256">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="1758c-257">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="1758c-257">OS</span></span>                 | <span data-ttu-id="1758c-258">Függőségek</span><span class="sxs-lookup"><span data-stu-id="1758c-258">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="1758c-259">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="1758c-259">Ubuntu 14.04</span></span>       | <span data-ttu-id="1758c-260">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="1758c-260">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="1758c-261">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="1758c-261">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="1758c-262">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="1758c-262">Ubuntu 16.04</span></span>       | <span data-ttu-id="1758c-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="1758c-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="1758c-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="1758c-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="1758c-265">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="1758c-265">Ubuntu 17.10</span></span>       | <span data-ttu-id="1758c-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="1758c-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="1758c-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="1758c-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="1758c-268">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="1758c-268">Ubuntu 18.04</span></span>       | <span data-ttu-id="1758c-269">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="1758c-269">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="1758c-270">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="1758c-270">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="1758c-271">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="1758c-271">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="1758c-272">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="1758c-272">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="1758c-273">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="1758c-273">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="1758c-274">Debian 9 (Nyújtás)</span><span class="sxs-lookup"><span data-stu-id="1758c-274">Debian 9 (Stretch)</span></span> | <span data-ttu-id="1758c-275">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="1758c-275">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="1758c-276">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="1758c-276">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="1758c-277">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="1758c-277">CentOS 7</span></span> <br> <span data-ttu-id="1758c-278">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="1758c-278">Oracle Linux 7</span></span> <br> <span data-ttu-id="1758c-279">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="1758c-279">RHEL 7</span></span> | <span data-ttu-id="1758c-280">libunwind, libcurl, openssl-függvénytárak, libicu</span><span class="sxs-lookup"><span data-stu-id="1758c-280">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="1758c-281">OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="1758c-281">openSUSE 42.3</span></span> | <span data-ttu-id="1758c-282">libcurl4, libopenssl1_0_0, libicu52_1</span><span class="sxs-lookup"><span data-stu-id="1758c-282">libcurl4, libopenssl1_0_0, libicu52_1</span></span> |
| <span data-ttu-id="1758c-283">openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="1758c-283">openSUSE Leap 15</span></span> | <span data-ttu-id="1758c-284">libcurl4, libopenssl1_0_0, libicu60_2</span><span class="sxs-lookup"><span data-stu-id="1758c-284">libcurl4, libopenssl1_0_0, libicu60_2</span></span> |
| <span data-ttu-id="1758c-285">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="1758c-285">Fedora 27</span></span> <br> <span data-ttu-id="1758c-286">28 Fedora</span><span class="sxs-lookup"><span data-stu-id="1758c-286">Fedora 28</span></span> | <span data-ttu-id="1758c-287">libunwind, libcurl, openssl-függvénytárak, libicu, a/compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="1758c-287">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="1758c-288">Nem hivatalosan támogatott Linux-disztribúciókon a PowerShell bináris fájljainak telepítéséhez telepíteni szeretné a cél operációs rendszer szükséges függőséget a különálló lépések.</span><span class="sxs-lookup"><span data-stu-id="1758c-288">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="1758c-289">Például a [Amazon Linux dockerfile] [ amazon-dockerfile] először telepíti a függőségeket, és ezt követően kiolvassa a Linuxos `tar.gz` archív.</span><span class="sxs-lookup"><span data-stu-id="1758c-289">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="1758c-290">Telepítés – bináris archívum</span><span class="sxs-lookup"><span data-stu-id="1758c-290">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="1758c-291">Linux</span><span class="sxs-lookup"><span data-stu-id="1758c-291">Linux</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.1.0/powershell-6.1.0-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.1.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.1.0

# Set execute permissions
sudo chmod +x /opt/microsoft/powershell/6.1.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.1.0/pwsh /usr/bin/pwsh
```

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="1758c-292">Bináris archívum eltávolítása</span><span class="sxs-lookup"><span data-stu-id="1758c-292">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="1758c-293">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="1758c-293">Paths</span></span>

* <span data-ttu-id="1758c-294">`$PSHOME` van `/opt/microsoft/powershell/6.1.0/`</span><span class="sxs-lookup"><span data-stu-id="1758c-294">`$PSHOME` is `/opt/microsoft/powershell/6.1.0/`</span></span>
* <span data-ttu-id="1758c-295">Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="1758c-295">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="1758c-296">Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="1758c-296">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="1758c-297">Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="1758c-297">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="1758c-298">Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="1758c-298">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="1758c-299">Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="1758c-299">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="1758c-300">PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="1758c-300">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="1758c-301">A profilok tiszteletben PowerShell a gazdagép konfiguráció, így az alapértelmezett gazdagép-specifikus profilok létezik `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="1758c-301">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="1758c-302">PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="1758c-302">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
