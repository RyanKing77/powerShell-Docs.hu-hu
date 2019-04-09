---
title: A PowerShell Core telepítése Linux rendszerre
description: Információ a különböző Linux-disztribúciókon a PowerShell Core telepítése
ms.date: 08/06/2018
ms.openlocfilehash: 06194550f4e73f9dd38f8cdc25f6c7f698cafce2
ms.sourcegitcommit: 806cf87488b80800b9f50a8af286e8379519a034
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59293333"
---
# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="d2f6d-103">A PowerShell Core telepítése Linux rendszerre</span><span class="sxs-lookup"><span data-stu-id="d2f6d-103">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="d2f6d-104">Támogatja a [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.04] [ u1804], [Ubuntu 18.10][u1810], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42.3][opensuse], [ Leap 15 openSUSE][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], és [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="d2f6d-104">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.04][u1804], [Ubuntu 18.10][u1810],  [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42.3][opensuse], [openSUSE Leap 15][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="d2f6d-105">A hivatalosan nem támogatott Linux-disztribúció, megpróbálhatja használatával a [PowerShell beépülő modul csomag][snap].</span><span class="sxs-lookup"><span data-stu-id="d2f6d-105">For Linux distributions that are not officially supported, you can try using the [PowerShell Snap Package][snap].</span></span>
<span data-ttu-id="d2f6d-106">Üzembe helyezése a PowerShell bináris fájlokat közvetlenül a a Linux használatával is megpróbálhatja [ `tar.gz` archív][tar], de állítsa be a szükséges függőségek az operációs rendszer a különálló lépések alapján kell.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-106">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="d2f6d-107">A githubon érhető el az összes csomag [kiadások][] lapot.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-107">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="d2f6d-108">A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-108">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
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

## <a name="installing-preview-releases"></a><span data-ttu-id="d2f6d-109">Előzetes verziók telepítése</span><span class="sxs-lookup"><span data-stu-id="d2f6d-109">Installing Preview Releases</span></span>

<span data-ttu-id="d2f6d-110">A PowerShell Core előzetes kiadás telepítése Linux rendszeren keresztül egy Csomagtárház esetén a csomag nevét a változik `powershell` való `powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-110">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="d2f6d-111">Közvetlen letöltésére keresztül telepítése nem változik, a fájl neve eltérő.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-111">Installing via direct download does not change, other than the file name.</span></span>

<span data-ttu-id="d2f6d-112">Íme egy táblát a parancsokat a különböző csomagkezelőinek használatával stabil és előzetes csomagok telepítéséhez:</span><span class="sxs-lookup"><span data-stu-id="d2f6d-112">Here is a table of the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="d2f6d-113">Distribution(s)</span><span class="sxs-lookup"><span data-stu-id="d2f6d-113">Distribution(s)</span></span>|<span data-ttu-id="d2f6d-114">Stabil parancs</span><span class="sxs-lookup"><span data-stu-id="d2f6d-114">Stable Command</span></span> | <span data-ttu-id="d2f6d-115">A parancs előzetes verzió</span><span class="sxs-lookup"><span data-stu-id="d2f6d-115">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="d2f6d-116">Ubuntu, a Debian</span><span class="sxs-lookup"><span data-stu-id="d2f6d-116">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="d2f6d-117">CentOS, RedHat</span><span class="sxs-lookup"><span data-stu-id="d2f6d-117">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="d2f6d-118">Fedora</span><span class="sxs-lookup"><span data-stu-id="d2f6d-118">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a><span data-ttu-id="d2f6d-119">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="d2f6d-119">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="d2f6d-120">Telepítési Csomagtárház - Ubuntu 14.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-120">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="d2f6d-121">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-121">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="d2f6d-122">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-122">This is the preferred method.</span></span>

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

<span data-ttu-id="d2f6d-123">Superuser, mint a Microsoft-tárház regisztrálása.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-123">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="d2f6d-124">Ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni a telepítés.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-124">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="d2f6d-125">Telepítési közvetlen letöltése – Ubuntu 14.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-125">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="d2f6d-126">A Debian-csomag letöltése</span><span class="sxs-lookup"><span data-stu-id="d2f6d-126">Download the Debian package</span></span>
`powershell_6.2.0-1.ubuntu.14.04_amd64.deb`
<span data-ttu-id="d2f6d-127">az a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-127">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="d2f6d-128">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="d2f6d-128">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="d2f6d-129">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-129">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="d2f6d-130">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-130">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="d2f6d-131">Eltávolítás – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="d2f6d-131">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="d2f6d-132">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="d2f6d-132">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="d2f6d-133">Telepítési csomag tárház - Ubuntu 16.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-133">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="d2f6d-134">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-134">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="d2f6d-135">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-135">This is the preferred method.</span></span>

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

<span data-ttu-id="d2f6d-136">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-136">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="d2f6d-137">Telepítési közvetlen letöltése – Ubuntu 16.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-137">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="d2f6d-138">A Debian-csomag letöltése</span><span class="sxs-lookup"><span data-stu-id="d2f6d-138">Download the Debian package</span></span>
`powershell_6.2.0-1.ubuntu.16.04_amd64.deb`
<span data-ttu-id="d2f6d-139">az a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-139">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="d2f6d-140">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="d2f6d-140">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="d2f6d-141">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-141">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="d2f6d-142">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-142">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="d2f6d-143">Eltávolítás – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="d2f6d-143">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="d2f6d-144">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="d2f6d-144">Ubuntu 18.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="d2f6d-145">Telepítési csomag tárház - Ubuntu 18.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-145">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="d2f6d-146">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-146">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="d2f6d-147">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-147">This is the preferred method.</span></span>

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

<span data-ttu-id="d2f6d-148">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-148">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="d2f6d-149">Telepítési közvetlen letöltése – Ubuntu 18.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-149">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="d2f6d-150">A Debian-csomag letöltése</span><span class="sxs-lookup"><span data-stu-id="d2f6d-150">Download the Debian package</span></span>
`powershell_6.2.0-1.ubuntu.18.04_amd64.deb`
<span data-ttu-id="d2f6d-151">az a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-151">from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="d2f6d-152">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="d2f6d-152">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="d2f6d-153">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-153">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="d2f6d-154">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-154">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1804"></a><span data-ttu-id="d2f6d-155">Eltávolítás – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="d2f6d-155">Uninstallation - Ubuntu 18.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a><span data-ttu-id="d2f6d-156">Ubuntu 18.10</span><span class="sxs-lookup"><span data-stu-id="d2f6d-156">Ubuntu 18.10</span></span>

> [!NOTE]
> <span data-ttu-id="d2f6d-157">Mivel 18.10 egy [közbenső kiadási](https://www.ubuntu.com/about/release-cycle), csak [támogatott közösségi](https://docs.microsoft.com/en-us/powershell/scripting/powershell-support-lifecycle?view=powershell-6).</span><span class="sxs-lookup"><span data-stu-id="d2f6d-157">As 18.10 is an [interim release](https://www.ubuntu.com/about/release-cycle), it is only [community supported](https://docs.microsoft.com/en-us/powershell/scripting/powershell-support-lifecycle?view=powershell-6).</span></span>

<span data-ttu-id="d2f6d-158">Keresztül támogatott 18.10 telepítése `snapd`.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-158">Installing on 18.10 is supported via `snapd`.</span></span> <span data-ttu-id="d2f6d-159">Lásd: [beépülő csomag] [ snap] teljes útmutatás;</span><span class="sxs-lookup"><span data-stu-id="d2f6d-159">See [Snap Package][snap] for full instructions;</span></span>

## <a name="debian-8"></a><span data-ttu-id="d2f6d-160">Debian 8</span><span class="sxs-lookup"><span data-stu-id="d2f6d-160">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="d2f6d-161">Telepítési Csomagtárház – Debian 8-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-161">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="d2f6d-162">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-162">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="d2f6d-163">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-163">This is the preferred method.</span></span>

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

<span data-ttu-id="d2f6d-164">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-164">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

## <a name="debian-9"></a><span data-ttu-id="d2f6d-165">Debian 9</span><span class="sxs-lookup"><span data-stu-id="d2f6d-165">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="d2f6d-166">Telepítési csomag tárház – Debian 9-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-166">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="d2f6d-167">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-167">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="d2f6d-168">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-168">This is the preferred method.</span></span>

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

<span data-ttu-id="d2f6d-169">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-169">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="d2f6d-170">Telepítési közvetlen letöltése – Debian 9-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-170">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="d2f6d-171">A Debian-csomag letöltése</span><span class="sxs-lookup"><span data-stu-id="d2f6d-171">Download the Debian package</span></span>
`powershell_6.2.0-1.debian.9_amd64.deb`
<span data-ttu-id="d2f6d-172">az a [kiadások][] oldal arra a Debian gépre.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-172">from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="d2f6d-173">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="d2f6d-173">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="d2f6d-174">Eltávolítás – Debian 9</span><span class="sxs-lookup"><span data-stu-id="d2f6d-174">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="d2f6d-175">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="d2f6d-175">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="d2f6d-176">Ez a csomag az Oracle Linux 7 is működik.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-176">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="d2f6d-177">Telepítési csomag tárház (preferált) – CentOS 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-177">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="d2f6d-178">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-178">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="d2f6d-179">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-179">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="d2f6d-180">Keresztül közvetlen letöltése – CentOS 7 telepítése</span><span class="sxs-lookup"><span data-stu-id="d2f6d-180">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="d2f6d-181">Használatával [CentOS 7][], töltse le az RPM-csomagot</span><span class="sxs-lookup"><span data-stu-id="d2f6d-181">Using [CentOS 7][], download the RPM package</span></span>
`powershell-6.2.0-1.rhel.7.x86_64.rpm`
<span data-ttu-id="d2f6d-182">az a [kiadások][] oldal arra a CentOS-gépre.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-182">from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="d2f6d-183">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="d2f6d-183">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="d2f6d-184">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="d2f6d-184">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="d2f6d-185">Eltávolítás – CentOS 7</span><span class="sxs-lookup"><span data-stu-id="d2f6d-185">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[<span data-ttu-id="d2f6d-186">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="d2f6d-186">CentOS 7</span></span>]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="d2f6d-187">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="d2f6d-187">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="d2f6d-188">Telepítési csomag tárház (preferált) – Red Hat Enterprise Linux (RHEL) 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-188">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="d2f6d-189">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-189">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="d2f6d-190">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-190">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="d2f6d-191">Telepítési közvetlen letöltése – Red Hat Enterprise Linux (RHEL) 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-191">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="d2f6d-192">Töltse le az RPM-csomagot</span><span class="sxs-lookup"><span data-stu-id="d2f6d-192">Download the RPM package</span></span>
`powershell-6.2.0-1.rhel.7.x86_64.rpm`
<span data-ttu-id="d2f6d-193">az a [kiadások][] oldal arra a Red Hat Enterprise Linux-gépre.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-193">from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="d2f6d-194">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="d2f6d-194">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="d2f6d-195">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="d2f6d-195">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="d2f6d-196">Eltávolítás – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="d2f6d-196">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse"></a><span data-ttu-id="d2f6d-197">openSUSE</span><span class="sxs-lookup"><span data-stu-id="d2f6d-197">openSUSE</span></span>

### <a name="installation---opensuse-423"></a><span data-ttu-id="d2f6d-198">Telepítés – openSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="d2f6d-198">Installation - openSUSE 42.3</span></span>

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

### <a name="installation---opensuse-leap-15"></a><span data-ttu-id="d2f6d-199">Telepítés – openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="d2f6d-199">Installation - openSUSE Leap 15</span></span>

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

### <a name="uninstallation---opensuse-423-opensuse-leap-15"></a><span data-ttu-id="d2f6d-200">Eltávolítás – openSUSE 42.3, openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="d2f6d-200">Uninstallation - openSUSE 42.3, openSUSE Leap 15</span></span>

```sh
rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="fedora"></a><span data-ttu-id="d2f6d-201">Fedora</span><span class="sxs-lookup"><span data-stu-id="d2f6d-201">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="d2f6d-202">Fedora 28 csak akkor támogatott, a PowerShell Core 6.1-es és újabb.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-202">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="d2f6d-203">Telepítési csomag tárház (preferált) – Fedora 27., Fedora 28-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-203">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="d2f6d-204">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-204">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="d2f6d-205">Telepítési közvetlen letöltése – Fedora 27, Fedora 28-n keresztül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-205">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="d2f6d-206">Töltse le az RPM-csomagot</span><span class="sxs-lookup"><span data-stu-id="d2f6d-206">Download the RPM package</span></span>
`powershell-6.2.0-1.rhel.7.x86_64.rpm`
<span data-ttu-id="d2f6d-207">az a [kiadások][] oldal arra a Fedora gépre.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-207">from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="d2f6d-208">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="d2f6d-208">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="d2f6d-209">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="d2f6d-209">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="d2f6d-210">Eltávolítás – Fedora 27., Fedora 28</span><span class="sxs-lookup"><span data-stu-id="d2f6d-210">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="d2f6d-211">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="d2f6d-211">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="d2f6d-212">A rendszer kísérleti emelőkaros támogatja.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-212">Arch support is experimental.</span></span>

<span data-ttu-id="d2f6d-213">PowerShell érhető el a [Arch Linux][] felhasználói tárház (AUR).</span><span class="sxs-lookup"><span data-stu-id="d2f6d-213">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="d2f6d-214">Az összeállítható a [legújabb címkézett kiadás][arch-release]</span><span class="sxs-lookup"><span data-stu-id="d2f6d-214">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="d2f6d-215">Az összeállítható a [fő a legutóbbi véglegesítést][arch-git]</span><span class="sxs-lookup"><span data-stu-id="d2f6d-215">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="d2f6d-216">Használatával telepíthető a [legújabb kibocsátási bináris][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="d2f6d-216">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="d2f6d-217">A AUR csomagok közösségi kezelt – nem hivatalos támogatott.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-217">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="d2f6d-218">A AUR a csomagok telepítésével kapcsolatos további információkért lásd: a [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a Közösség [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="d2f6d-218">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[<span data-ttu-id="d2f6d-219">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="d2f6d-219">Arch Linux</span></span>]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a><span data-ttu-id="d2f6d-220">Snap Package</span><span class="sxs-lookup"><span data-stu-id="d2f6d-220">Snap Package</span></span>

### <a name="getting-snapd"></a><span data-ttu-id="d2f6d-221">Első snapd</span><span class="sxs-lookup"><span data-stu-id="d2f6d-221">Getting snapd</span></span>

`snapd` <span data-ttu-id="d2f6d-222">Illesztés futtatásához szükség.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-222">is required to run snaps.</span></span>
<span data-ttu-id="d2f6d-223">Használat [ezek az utasítások](https://docs.snapcraft.io/core/install) , ellenőrizze, hogy `snapd` telepítve.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-223">Use [these instructions](https://docs.snapcraft.io/core/install) to make sure you have `snapd` installed.</span></span>

### <a name="installation-via-snap"></a><span data-ttu-id="d2f6d-224">Keresztül beépülő modul telepítése</span><span class="sxs-lookup"><span data-stu-id="d2f6d-224">Installation via Snap</span></span>

<span data-ttu-id="d2f6d-225">A PowerShell Core, Linux esetén a rendszer közzéteszi az [beépülő store](https://snapcraft.io/store) egyszerű telepítéshez (és frissítések).</span><span class="sxs-lookup"><span data-stu-id="d2f6d-225">PowerShell Core, for Linux, is published to the [Snap store](https://snapcraft.io/store) for easy installation (and updates).</span></span>
<span data-ttu-id="d2f6d-226">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-226">This is the preferred method.</span></span>

```sh
# Install PowerShell
sudo snap install powershell --classic

# Start PowerShell
pwsh
```

<span data-ttu-id="d2f6d-227">Ha szeretne az előzetes verzió telepítése, a következő metódust.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-227">If you want to install preview version, use following method.</span></span>

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

<span data-ttu-id="d2f6d-228">Után automatikusan beépülő modul telepítését frissíti, de egy frissítési használatával aktiválhat `sudo snap refresh powershell` vagy `sudo snap refresh powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-228">After installing Snap will automatically upgrade, but you can trigger an upgrade using `sudo snap refresh powershell` or `sudo snap refresh powershell-preview`.</span></span>

### <a name="uninstallation"></a><span data-ttu-id="d2f6d-229">Az Eltávolítás</span><span class="sxs-lookup"><span data-stu-id="d2f6d-229">Uninstallation</span></span>

```sh
sudo snap remove powershell
```

<span data-ttu-id="d2f6d-230">vagy a</span><span class="sxs-lookup"><span data-stu-id="d2f6d-230">or</span></span>

```sh
sudo snap remove powershell-preview
```

## <a name="kali"></a><span data-ttu-id="d2f6d-231">Kali</span><span class="sxs-lookup"><span data-stu-id="d2f6d-231">Kali</span></span>

### <a name="installation---kali"></a><span data-ttu-id="d2f6d-232">Telepítés – Kali</span><span class="sxs-lookup"><span data-stu-id="d2f6d-232">Installation - Kali</span></span>

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

### <a name="uninstallation---kali"></a><span data-ttu-id="d2f6d-233">Eltávolítás – Kali</span><span class="sxs-lookup"><span data-stu-id="d2f6d-233">Uninstallation - Kali</span></span>

```sh
# Uninstall PowerShell package
apt-get remove -y powershell
```

## <a name="raspbian"></a><span data-ttu-id="d2f6d-234">Raspbian</span><span class="sxs-lookup"><span data-stu-id="d2f6d-234">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="d2f6d-235">Raspbian támogatási je experimentální.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-235">Raspbian support is experimental.</span></span>

<span data-ttu-id="d2f6d-236">PowerShell jelenleg csak a Raspbian Stretch támogatott.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-236">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="d2f6d-237">Emellett coreclr-nek (és így a PowerShell Core) csak 2 tartományban és Pi 3 eszközökön módon fog más eszközök, például [Pi nulla](https://github.com/dotnet/coreclr/issues/10605), egy nem támogatott processzorral rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-237">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="d2f6d-238">Töltse le [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) , és kövesse a [telepítési utasításokat](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) a Pi eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-238">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation---raspbian"></a><span data-ttu-id="d2f6d-239">Telepítés – Raspbian</span><span class="sxs-lookup"><span data-stu-id="d2f6d-239">Installation - Raspbian</span></span>

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.2.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

<span data-ttu-id="d2f6d-240">Igény szerint hozhat létre a szimbolikus hivatkozást úgy, hogy tudni indítsa el a Powershellt, a "pwsh" bináris elérési út megadása nélkül</span><span class="sxs-lookup"><span data-stu-id="d2f6d-240">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="d2f6d-241">Eltávolítás – Raspbian</span><span class="sxs-lookup"><span data-stu-id="d2f6d-241">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="d2f6d-242">Bináris archívum</span><span class="sxs-lookup"><span data-stu-id="d2f6d-242">Binary Archives</span></span>

<span data-ttu-id="d2f6d-243">PowerShell bináris `tar.gz` archívumok biztosított Linux-platformokhoz a speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-243">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="d2f6d-244">Függőségek</span><span class="sxs-lookup"><span data-stu-id="d2f6d-244">Dependencies</span></span>

<span data-ttu-id="d2f6d-245">PowerShell az összes Linux-disztribúciókra vonatkozó hordozható bináris épít fel.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-245">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="d2f6d-246">De a .NET Core runtime szükséges különböző disztribúciókon különböző függőségek, és ezért PowerShell pedig ugyanezt.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-246">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="d2f6d-247">A következő diagram a .NET Core 2.0 hivatalosan támogatott különböző Linux-disztribúciókon függőségeit jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-247">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="d2f6d-248">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="d2f6d-248">OS</span></span>                 | <span data-ttu-id="d2f6d-249">Függőségek</span><span class="sxs-lookup"><span data-stu-id="d2f6d-249">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="d2f6d-250">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="d2f6d-250">Ubuntu 14.04</span></span>       | <span data-ttu-id="d2f6d-251">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="d2f6d-251">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="d2f6d-252">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="d2f6d-252">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="d2f6d-253">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="d2f6d-253">Ubuntu 16.04</span></span>       | <span data-ttu-id="d2f6d-254">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="d2f6d-254">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="d2f6d-255">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="d2f6d-255">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="d2f6d-256">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="d2f6d-256">Ubuntu 17.10</span></span>       | <span data-ttu-id="d2f6d-257">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="d2f6d-257">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="d2f6d-258">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="d2f6d-258">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="d2f6d-259">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="d2f6d-259">Ubuntu 18.04</span></span>       | <span data-ttu-id="d2f6d-260">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="d2f6d-260">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="d2f6d-261">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="d2f6d-261">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="d2f6d-262">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="d2f6d-262">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="d2f6d-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="d2f6d-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="d2f6d-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="d2f6d-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="d2f6d-265">Debian 9 (Nyújtás)</span><span class="sxs-lookup"><span data-stu-id="d2f6d-265">Debian 9 (Stretch)</span></span> | <span data-ttu-id="d2f6d-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="d2f6d-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="d2f6d-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="d2f6d-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="d2f6d-268">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="d2f6d-268">CentOS 7</span></span> <br> <span data-ttu-id="d2f6d-269">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="d2f6d-269">Oracle Linux 7</span></span> <br> <span data-ttu-id="d2f6d-270">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="d2f6d-270">RHEL 7</span></span> | <span data-ttu-id="d2f6d-271">libunwind, libcurl, openssl-függvénytárak, libicu</span><span class="sxs-lookup"><span data-stu-id="d2f6d-271">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="d2f6d-272">openSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="d2f6d-272">openSUSE 42.3</span></span> | <span data-ttu-id="d2f6d-273">libcurl4, libopenssl1_0_0, libicu52_1</span><span class="sxs-lookup"><span data-stu-id="d2f6d-273">libcurl4, libopenssl1_0_0, libicu52_1</span></span> |
| <span data-ttu-id="d2f6d-274">openSUSE Leap 15</span><span class="sxs-lookup"><span data-stu-id="d2f6d-274">openSUSE Leap 15</span></span> | <span data-ttu-id="d2f6d-275">libcurl4, libopenssl1_0_0, libicu60_2</span><span class="sxs-lookup"><span data-stu-id="d2f6d-275">libcurl4, libopenssl1_0_0, libicu60_2</span></span> |
| <span data-ttu-id="d2f6d-276">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="d2f6d-276">Fedora 27</span></span> <br> <span data-ttu-id="d2f6d-277">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="d2f6d-277">Fedora 28</span></span> | <span data-ttu-id="d2f6d-278">libunwind, libcurl, openssl-függvénytárak, libicu, a/compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="d2f6d-278">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="d2f6d-279">Nem hivatalosan támogatott Linux-disztribúciókon a PowerShell bináris fájljainak telepítéséhez telepíteni szeretné a cél operációs rendszer szükséges függőséget a különálló lépések.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-279">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="d2f6d-280">Például a [Amazon Linux dockerfile] [ amazon-dockerfile] először telepíti a függőségeket, és ezt követően kiolvassa a Linuxos `tar.gz` archív.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-280">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell-Docker/blob/master/release/community-stable/amazonlinux/docker/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="d2f6d-281">Telepítés – bináris archívum</span><span class="sxs-lookup"><span data-stu-id="d2f6d-281">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="d2f6d-282">Linux</span><span class="sxs-lookup"><span data-stu-id="d2f6d-282">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="d2f6d-283">Bináris archívum eltávolítása</span><span class="sxs-lookup"><span data-stu-id="d2f6d-283">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="d2f6d-284">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="d2f6d-284">Paths</span></span>

* `$PSHOME` <span data-ttu-id="d2f6d-285">van</span><span class="sxs-lookup"><span data-stu-id="d2f6d-285">is</span></span> `/opt/microsoft/powershell/6.2.0/`
* <span data-ttu-id="d2f6d-286">Felhasználói profilokat fog olvasni</span><span class="sxs-lookup"><span data-stu-id="d2f6d-286">User profiles will be read from</span></span> `~/.config/powershell/profile.ps1`
* <span data-ttu-id="d2f6d-287">Alapértelmezett profilokat fog olvasni</span><span class="sxs-lookup"><span data-stu-id="d2f6d-287">Default profiles will be read from</span></span> `$PSHOME/profile.ps1`
* <span data-ttu-id="d2f6d-288">Felhasználói modulok fog olvasni</span><span class="sxs-lookup"><span data-stu-id="d2f6d-288">User modules will be read from</span></span> `~/.local/share/powershell/Modules`
* <span data-ttu-id="d2f6d-289">Megosztott modulok fog olvasni</span><span class="sxs-lookup"><span data-stu-id="d2f6d-289">Shared modules will be read from</span></span> `/usr/local/share/powershell/Modules`
* <span data-ttu-id="d2f6d-290">Az alapértelmezett modulokat fog olvasni</span><span class="sxs-lookup"><span data-stu-id="d2f6d-290">Default modules will be read from</span></span> `$PSHOME/Modules`
* <span data-ttu-id="d2f6d-291">PSReadline előzmények lesz rögzítve a</span><span class="sxs-lookup"><span data-stu-id="d2f6d-291">PSReadline history will be recorded to</span></span> `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`

<span data-ttu-id="d2f6d-292">A profilok tiszteletben PowerShell a gazdagép konfiguráció, így az alapértelmezett gazdagép-specifikus profilok létezik `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-292">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="d2f6d-293">PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="d2f6d-293">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[<span data-ttu-id="d2f6d-294">Kiadások</span><span class="sxs-lookup"><span data-stu-id="d2f6d-294">releases</span></span>]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
