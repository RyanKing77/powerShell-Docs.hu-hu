---
title: A PowerShell Core telepítése Linux rendszerre
description: Információ a különböző Linux-disztribúciókon a PowerShell Core telepítése
ms.date: 08/06/2018
ms.openlocfilehash: a6b0e3003f84ea6dc99cffcc7edf1b5b6963aa21
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587448"
---
# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="f6d31-103">A PowerShell Core telepítése Linux rendszerre</span><span class="sxs-lookup"><span data-stu-id="f6d31-103">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="f6d31-104">Támogatja a [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.10] [ u18], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.3][opensuse], [Fedora 27 ] [ fedora], [Fedora 28][fedora], és [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="f6d31-104">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 18.10][u18], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.3][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="f6d31-105">A hivatalosan nem támogatott Linux-disztribúció, megpróbálhatja használatával a [PowerShell beépülő modul csomag][snap].</span><span class="sxs-lookup"><span data-stu-id="f6d31-105">For Linux distributions that are not officially supported, you can try using the [PowerShell Snap Package][snap].</span></span>
<span data-ttu-id="f6d31-106">Üzembe helyezése a PowerShell bináris fájlokat közvetlenül a a Linux használatával is megpróbálhatja [ `tar.gz` archív][tar], de állítsa be a szükséges függőségek az operációs rendszer a különálló lépések alapján kell.</span><span class="sxs-lookup"><span data-stu-id="f6d31-106">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="f6d31-107">A githubon érhető el az összes csomag [kiadások][] lapot.</span><span class="sxs-lookup"><span data-stu-id="f6d31-107">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="f6d31-108">A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="f6d31-108">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u18]: #ubuntu-1810
[u18]: #ubuntu-1804
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-423
[fedora]: #fedora
[arch]: #arch-linux
[snap]: #snap-package
[tar]: #binary-archives

## <a name="installing-preview-releases"></a><span data-ttu-id="f6d31-109">Előzetes verziók telepítése</span><span class="sxs-lookup"><span data-stu-id="f6d31-109">Installing Preview Releases</span></span>

<span data-ttu-id="f6d31-110">A PowerShell Core előzetes kiadás telepítése Linux rendszeren keresztül egy Csomagtárház esetén a csomag nevét a változik `powershell` való `powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="f6d31-110">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="f6d31-111">Közvetlen letöltésére keresztül telepítése nem változik, a fájl neve eltérő.</span><span class="sxs-lookup"><span data-stu-id="f6d31-111">Installing via direct download does not change, other than the file name.</span></span>

<span data-ttu-id="f6d31-112">Íme egy táblát a parancsokat a különböző csomagkezelőinek használatával stabil és előzetes csomagok telepítéséhez:</span><span class="sxs-lookup"><span data-stu-id="f6d31-112">Here is a table of the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="f6d31-113">Distribution(s)</span><span class="sxs-lookup"><span data-stu-id="f6d31-113">Distribution(s)</span></span>|<span data-ttu-id="f6d31-114">Stabil parancs</span><span class="sxs-lookup"><span data-stu-id="f6d31-114">Stable Command</span></span> | <span data-ttu-id="f6d31-115">A parancs előzetes verzió</span><span class="sxs-lookup"><span data-stu-id="f6d31-115">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="f6d31-116">Ubuntu, a Debian</span><span class="sxs-lookup"><span data-stu-id="f6d31-116">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="f6d31-117">CentOS, a RedHat</span><span class="sxs-lookup"><span data-stu-id="f6d31-117">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="f6d31-118">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="f6d31-118">OpenSUSE</span></span> |`sudo zypper install powershell` | `sudo zypper install powershell-preview`|
| <span data-ttu-id="f6d31-119">Fedora</span><span class="sxs-lookup"><span data-stu-id="f6d31-119">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a><span data-ttu-id="f6d31-120">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="f6d31-120">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="f6d31-121">Telepítési Csomagtárház - Ubuntu 14.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-121">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="f6d31-122">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="f6d31-122">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="f6d31-123">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="f6d31-123">This is the preferred method.</span></span>

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

<span data-ttu-id="f6d31-124">Superuser, mint a Microsoft-tárház regisztrálása.</span><span class="sxs-lookup"><span data-stu-id="f6d31-124">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="f6d31-125">Ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni a telepítés.</span><span class="sxs-lookup"><span data-stu-id="f6d31-125">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="f6d31-126">Telepítési közvetlen letöltése – Ubuntu 14.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-126">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="f6d31-127">A Debian csomag `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` származó a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="f6d31-127">Download the Debian package `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="f6d31-128">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="f6d31-128">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="f6d31-129">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="f6d31-129">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="f6d31-130">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="f6d31-130">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="f6d31-131">Eltávolítás – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="f6d31-131">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="f6d31-132">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f6d31-132">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="f6d31-133">Telepítési csomag tárház - Ubuntu 16.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-133">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="f6d31-134">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="f6d31-134">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="f6d31-135">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="f6d31-135">This is the preferred method.</span></span>

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

<span data-ttu-id="f6d31-136">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="f6d31-136">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="f6d31-137">Telepítési közvetlen letöltése – Ubuntu 16.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-137">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="f6d31-138">A Debian csomag `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` származó a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="f6d31-138">Download the Debian package `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="f6d31-139">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="f6d31-139">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="f6d31-140">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="f6d31-140">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="f6d31-141">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="f6d31-141">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="f6d31-142">Eltávolítás – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f6d31-142">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="f6d31-143">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="f6d31-143">Ubuntu 18.04</span></span>

> [!NOTE]
> <span data-ttu-id="f6d31-144">Miután Ubuntu 18.04 támogatása hozzáadva `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="f6d31-144">Support for Ubuntu 18.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="f6d31-145">Telepítési csomag tárház - Ubuntu 18.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-145">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="f6d31-146">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="f6d31-146">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="f6d31-147">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="f6d31-147">This is the preferred method.</span></span>

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
pwsh-preview
```

<span data-ttu-id="f6d31-148">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="f6d31-148">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="f6d31-149">Telepítési közvetlen letöltése – Ubuntu 18.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-149">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="f6d31-150">A Debian csomag `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` származó a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="f6d31-150">Download the Debian package `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="f6d31-151">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="f6d31-151">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="f6d31-152">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="f6d31-152">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="f6d31-153">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="f6d31-153">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1804"></a><span data-ttu-id="f6d31-154">Eltávolítás – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="f6d31-154">Uninstallation - Ubuntu 18.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a><span data-ttu-id="f6d31-155">Ubuntu 18.10</span><span class="sxs-lookup"><span data-stu-id="f6d31-155">Ubuntu 18.10</span></span>

> [!NOTE]
> <span data-ttu-id="f6d31-156">Ubuntu 18.10 támogatása hozzáadva után `6.1.0-preview.3`.</span><span class="sxs-lookup"><span data-stu-id="f6d31-156">Support for Ubuntu 18.10 was added after `6.1.0-preview.3`.</span></span>
> <span data-ttu-id="f6d31-157">Mivel 18.10 napi build, akkor csak a támogatott közösségi.</span><span class="sxs-lookup"><span data-stu-id="f6d31-157">As 18.10 is a daily build, it is only community supported.</span></span>

<span data-ttu-id="f6d31-158">Keresztül támogatott 18.10 telepítése `snapd`.</span><span class="sxs-lookup"><span data-stu-id="f6d31-158">Installing on 18.10 is supported via `snapd`.</span></span> <span data-ttu-id="f6d31-159">Lásd: [beépülő csomag] [ snap] teljes útmutatás;</span><span class="sxs-lookup"><span data-stu-id="f6d31-159">See [Snap Package][snap] for full instructions;</span></span>

## <a name="debian-8"></a><span data-ttu-id="f6d31-160">Debian 8</span><span class="sxs-lookup"><span data-stu-id="f6d31-160">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="f6d31-161">Telepítési Csomagtárház – Debian 8-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-161">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="f6d31-162">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="f6d31-162">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="f6d31-163">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="f6d31-163">This is the preferred method.</span></span>

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

<span data-ttu-id="f6d31-164">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="f6d31-164">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="f6d31-165">Keresztül közvetlen letöltése – Debian 8 telepítés</span><span class="sxs-lookup"><span data-stu-id="f6d31-165">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="f6d31-166">A Debian csomag `powershell_6.0.2-1.debian.8_amd64.deb` származó a [kiadások][] oldal arra a Debian gépre.</span><span class="sxs-lookup"><span data-stu-id="f6d31-166">Download the Debian package `powershell_6.0.2-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="f6d31-167">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="f6d31-167">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="f6d31-168">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="f6d31-168">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="f6d31-169">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="f6d31-169">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="f6d31-170">Eltávolítás – Debian 8</span><span class="sxs-lookup"><span data-stu-id="f6d31-170">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="f6d31-171">Debian 9</span><span class="sxs-lookup"><span data-stu-id="f6d31-171">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="f6d31-172">Telepítési csomag tárház – Debian 9-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-172">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="f6d31-173">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="f6d31-173">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="f6d31-174">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="f6d31-174">This is the preferred method.</span></span>

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

<span data-ttu-id="f6d31-175">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="f6d31-175">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="f6d31-176">Telepítési közvetlen letöltése – Debian 9-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-176">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="f6d31-177">A Debian csomag `powershell_6.0.2-1.debian.9_amd64.deb` származó a [kiadások][] oldal arra a Debian gépre.</span><span class="sxs-lookup"><span data-stu-id="f6d31-177">Download the Debian package `powershell_6.0.2-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="f6d31-178">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="f6d31-178">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="f6d31-179">Eltávolítás – Debian 9</span><span class="sxs-lookup"><span data-stu-id="f6d31-179">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="f6d31-180">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="f6d31-180">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="f6d31-181">Ez a csomag az Oracle Linux 7 is működik.</span><span class="sxs-lookup"><span data-stu-id="f6d31-181">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="f6d31-182">Telepítési csomag tárház (preferált) – CentOS 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-182">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="f6d31-183">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="f6d31-183">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="f6d31-184">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="f6d31-184">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="f6d31-185">Keresztül közvetlen letöltése – CentOS 7 telepítése</span><span class="sxs-lookup"><span data-stu-id="f6d31-185">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="f6d31-186">Használatával [CentOS 7][], töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadások][] oldal arra a CentOS-gépre.</span><span class="sxs-lookup"><span data-stu-id="f6d31-186">Using [CentOS 7][], download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="f6d31-187">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="f6d31-187">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="f6d31-188">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="f6d31-188">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="f6d31-189">Eltávolítás – CentOS 7</span><span class="sxs-lookup"><span data-stu-id="f6d31-189">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="f6d31-191">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="f6d31-191">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="f6d31-192">Telepítési csomag tárház (preferált) – Red Hat Enterprise Linux (RHEL) 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-192">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="f6d31-193">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="f6d31-193">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="f6d31-194">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="f6d31-194">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="f6d31-195">Telepítési közvetlen letöltése – Red Hat Enterprise Linux (RHEL) 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-195">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="f6d31-196">Töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` származó a [kiadások][] oldal arra a Red Hat Enterprise Linux-gépre.</span><span class="sxs-lookup"><span data-stu-id="f6d31-196">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="f6d31-197">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="f6d31-197">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="f6d31-198">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="f6d31-198">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="f6d31-199">Eltávolítás – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="f6d31-199">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-423"></a><span data-ttu-id="f6d31-200">OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="f6d31-200">OpenSUSE 42.3</span></span>

<span data-ttu-id="f6d31-201">A PowerShell Core, telepítésekor `zypper` feltétlenül jelentik a következő hibával:</span><span class="sxs-lookup"><span data-stu-id="f6d31-201">When installing PowerShell Core, `zypper` may report the following error:</span></span>

```Output
Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
 Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
 Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
```

<span data-ttu-id="f6d31-202">Ebben az esetben ellenőrizze, hogy a kompatibilis `libcurl` könyvtár megtalálható úgy, hogy a következő parancsot a látható a `libcurl4` csomag telepítve vannak:</span><span class="sxs-lookup"><span data-stu-id="f6d31-202">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>

```sh
zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
```

<span data-ttu-id="f6d31-203">Majd válassza ki a `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` megoldáshoz, amikor a PowerShell-csomag telepítése.</span><span class="sxs-lookup"><span data-stu-id="f6d31-203">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the PowerShell package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-423"></a><span data-ttu-id="f6d31-204">Telepítés (preferált) – Csomagtárház OpenSUSE 42.3 keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-204">Installation via Package Repository (preferred) - OpenSUSE 42.3</span></span>

<span data-ttu-id="f6d31-205">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="f6d31-205">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Add the Microsoft Repository
zypper ar https://packages.microsoft.com/rhel/7/prod/

# Update the list of products
sudo zypper update

# Install PowerShell
sudo zypper install powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---opensuse-423"></a><span data-ttu-id="f6d31-206">Telepítési közvetlen letöltése – OpenSUSE 42.3-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-206">Installation via Direct Download - OpenSUSE 42.3</span></span>

<span data-ttu-id="f6d31-207">Töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` származó a [kiadások][] lap arra az opensuse-alapú gépre.</span><span class="sxs-lookup"><span data-stu-id="f6d31-207">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="f6d31-208">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="f6d31-208">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-423"></a><span data-ttu-id="f6d31-209">Eltávolítás – OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="f6d31-209">Uninstallation - OpenSUSE 42.3</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a><span data-ttu-id="f6d31-210">Fedora</span><span class="sxs-lookup"><span data-stu-id="f6d31-210">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="f6d31-211">Fedora 28 csak akkor támogatott, a PowerShell Core 6.1-es és újabb.</span><span class="sxs-lookup"><span data-stu-id="f6d31-211">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="f6d31-212">Telepítési csomag tárház (preferált) – Fedora 27., Fedora 28-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-212">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="f6d31-213">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="f6d31-213">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="f6d31-214">Telepítési közvetlen letöltése – Fedora 27, Fedora 28-n keresztül</span><span class="sxs-lookup"><span data-stu-id="f6d31-214">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="f6d31-215">Töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` származó a [kiadások][] oldal arra a Fedora gépre.</span><span class="sxs-lookup"><span data-stu-id="f6d31-215">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="f6d31-216">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="f6d31-216">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="f6d31-217">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="f6d31-217">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="f6d31-218">Eltávolítás – Fedora 27., Fedora 28</span><span class="sxs-lookup"><span data-stu-id="f6d31-218">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="f6d31-219">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="f6d31-219">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="f6d31-220">A rendszer kísérleti emelőkaros támogatja.</span><span class="sxs-lookup"><span data-stu-id="f6d31-220">Arch support is experimental.</span></span>

<span data-ttu-id="f6d31-221">PowerShell érhető el a [Arch Linux][] felhasználói tárház (AUR).</span><span class="sxs-lookup"><span data-stu-id="f6d31-221">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="f6d31-222">Az összeállítható a [legújabb címkézett kiadás][arch-release]</span><span class="sxs-lookup"><span data-stu-id="f6d31-222">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="f6d31-223">Az összeállítható a [fő a legutóbbi véglegesítést][arch-git]</span><span class="sxs-lookup"><span data-stu-id="f6d31-223">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="f6d31-224">Használatával telepíthető a [legújabb kibocsátási bináris][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="f6d31-224">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="f6d31-225">A AUR csomagok közösségi kezelt – nem hivatalos támogatott.</span><span class="sxs-lookup"><span data-stu-id="f6d31-225">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="f6d31-226">A AUR a csomagok telepítésével kapcsolatos további információkért lásd: a [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a Közösség [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="f6d31-226">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a><span data-ttu-id="f6d31-228">Oszlopokhoz illesztés csomag</span><span class="sxs-lookup"><span data-stu-id="f6d31-228">Snap Package</span></span>

### <a name="getting-snapd"></a><span data-ttu-id="f6d31-229">Első snapd</span><span class="sxs-lookup"><span data-stu-id="f6d31-229">Getting snapd</span></span>

<span data-ttu-id="f6d31-230">`snapd` Illesztés futtatásához szükség.</span><span class="sxs-lookup"><span data-stu-id="f6d31-230">`snapd` is required to run snaps.</span></span>  <span data-ttu-id="f6d31-231">Használat [ezek az utasítások](https://docs.snapcraft.io/core/install) , ellenőrizze, hogy `snapd` telepítve.</span><span class="sxs-lookup"><span data-stu-id="f6d31-231">Use [these instructions](https://docs.snapcraft.io/core/install) to make sure you have `snapd` installed.</span></span>

### <a name="installation-via-snap"></a><span data-ttu-id="f6d31-232">Keresztül beépülő modul telepítése</span><span class="sxs-lookup"><span data-stu-id="f6d31-232">Installation via Snap</span></span>

<span data-ttu-id="f6d31-233">A PowerShell Core, Linux esetén a rendszer közzéteszi az [beépülő store](https://snapcraft.io/store) egyszerű telepítéshez (és frissítések).</span><span class="sxs-lookup"><span data-stu-id="f6d31-233">PowerShell Core, for Linux, is published to the [Snap store](https://snapcraft.io/store) for easy installation (and updates).</span></span>
<span data-ttu-id="f6d31-234">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="f6d31-234">This is the preferred method.</span></span>

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

<span data-ttu-id="f6d31-235">Után automatikusan beépülő modul telepítését frissíti, de egy frissítési használatával aktiválhat `sudo snap refresh powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="f6d31-235">After installing Snap will automatically upgrade, but you can trigger an upgrade using `sudo snap refresh powershell-preview`.</span></span>

### <a name="uninstallation"></a><span data-ttu-id="f6d31-236">Az Eltávolítás</span><span class="sxs-lookup"><span data-stu-id="f6d31-236">Uninstallation</span></span>

```sh
sudo snap remove powershell-preview
```

## <a name="linux-appimage"></a><span data-ttu-id="f6d31-237">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="f6d31-237">Linux AppImage</span></span>

> [!NOTE]
> <span data-ttu-id="f6d31-238">AppImage támogatási je experimentální.</span><span class="sxs-lookup"><span data-stu-id="f6d31-238">AppImage support is experimental</span></span>

<span data-ttu-id="f6d31-239">Legutóbbi Linux-disztribúció használatával töltse le a AppImage `powershell-6.0.1-x86_64.AppImage` származó a [kiadások][] oldal arra a Linux-gépre.</span><span class="sxs-lookup"><span data-stu-id="f6d31-239">Using a recent Linux distribution, download the AppImage `powershell-6.0.1-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="f6d31-240">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="f6d31-240">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

<span data-ttu-id="f6d31-241">A [AppImage][] teszi lehetővé a PowerShell futtatása nélkül telepíti azt.</span><span class="sxs-lookup"><span data-stu-id="f6d31-241">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="f6d31-242">Egy hordozható alkalmazást, amely a PowerShell és annak függőségeit, (beleértve a .NET Core rendszerfüggőségekben) bundles javul csomagba.</span><span class="sxs-lookup"><span data-stu-id="f6d31-242">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="f6d31-243">A csomag nincs egyetlen bináris, amely a felhasználó Linux-disztribúció függetlenül működik.</span><span class="sxs-lookup"><span data-stu-id="f6d31-243">This package is a single binary that works independently of the user's Linux distribution.</span></span>

[appimage]: http://appimage.org/

## <a name="kali"></a><span data-ttu-id="f6d31-245">Kali</span><span class="sxs-lookup"><span data-stu-id="f6d31-245">Kali</span></span>

> [!NOTE]
> <span data-ttu-id="f6d31-246">Kali támogatási je experimentální.</span><span class="sxs-lookup"><span data-stu-id="f6d31-246">Kali support is experimental.</span></span>

### <a name="installation"></a><span data-ttu-id="f6d31-247">Telepítés</span><span class="sxs-lookup"><span data-stu-id="f6d31-247">Installation</span></span>

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

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="f6d31-248">Futtassa a Powershellt a legújabb Kali (GNU/Linux folyamatos Kali) azt telepítése nélkül</span><span class="sxs-lookup"><span data-stu-id="f6d31-248">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="f6d31-249">Eltávolítás – Kali</span><span class="sxs-lookup"><span data-stu-id="f6d31-249">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="f6d31-250">Raspbian</span><span class="sxs-lookup"><span data-stu-id="f6d31-250">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="f6d31-251">Raspbian támogatási je experimentální.</span><span class="sxs-lookup"><span data-stu-id="f6d31-251">Raspbian support is experimental.</span></span>

<span data-ttu-id="f6d31-252">PowerShell jelenleg csak a Raspbian Stretch támogatott.</span><span class="sxs-lookup"><span data-stu-id="f6d31-252">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="f6d31-253">Emellett coreclr-nek (és így a PowerShell Core) csak 2 tartományban és Pi 3 eszközökön módon fog más eszközök, például [Pi nulla](https://github.com/dotnet/coreclr/issues/10605), egy nem támogatott processzorral rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="f6d31-253">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="f6d31-254">Töltse le [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) , és kövesse a [telepítési utasításokat](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) a Pi eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="f6d31-254">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation"></a><span data-ttu-id="f6d31-255">Telepítés</span><span class="sxs-lookup"><span data-stu-id="f6d31-255">Installation</span></span>

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

<span data-ttu-id="f6d31-256">Igény szerint hozhat létre a szimbolikus hivatkozást úgy, hogy tudni indítsa el a Powershellt, a "pwsh" bináris elérési út megadása nélkül</span><span class="sxs-lookup"><span data-stu-id="f6d31-256">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="f6d31-257">Eltávolítás – Raspbian</span><span class="sxs-lookup"><span data-stu-id="f6d31-257">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="f6d31-258">Bináris archívum</span><span class="sxs-lookup"><span data-stu-id="f6d31-258">Binary Archives</span></span>

<span data-ttu-id="f6d31-259">PowerShell bináris `tar.gz` archívumok biztosított Linux-platformokhoz a speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé.</span><span class="sxs-lookup"><span data-stu-id="f6d31-259">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="f6d31-260">Függőségek</span><span class="sxs-lookup"><span data-stu-id="f6d31-260">Dependencies</span></span>

<span data-ttu-id="f6d31-261">PowerShell az összes Linux-disztribúciókra vonatkozó hordozható bináris épít fel.</span><span class="sxs-lookup"><span data-stu-id="f6d31-261">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="f6d31-262">De a .NET Core runtime szükséges különböző disztribúciókon különböző függőségek, és ezért PowerShell pedig ugyanezt.</span><span class="sxs-lookup"><span data-stu-id="f6d31-262">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="f6d31-263">A következő diagram a .NET Core 2.0 hivatalosan támogatott különböző Linux-disztribúciókon függőségeit jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="f6d31-263">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="f6d31-264">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="f6d31-264">OS</span></span>                 | <span data-ttu-id="f6d31-265">Függőségek</span><span class="sxs-lookup"><span data-stu-id="f6d31-265">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="f6d31-266">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="f6d31-266">Ubuntu 14.04</span></span>       | <span data-ttu-id="f6d31-267">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="f6d31-267">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="f6d31-268">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="f6d31-268">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="f6d31-269">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="f6d31-269">Ubuntu 16.04</span></span>       | <span data-ttu-id="f6d31-270">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="f6d31-270">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="f6d31-271">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="f6d31-271">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="f6d31-272">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="f6d31-272">Ubuntu 17.10</span></span>       | <span data-ttu-id="f6d31-273">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="f6d31-273">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="f6d31-274">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="f6d31-274">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="f6d31-275">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="f6d31-275">Ubuntu 18.04</span></span>       | <span data-ttu-id="f6d31-276">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="f6d31-276">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="f6d31-277">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="f6d31-277">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="f6d31-278">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="f6d31-278">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="f6d31-279">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="f6d31-279">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="f6d31-280">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="f6d31-280">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="f6d31-281">Debian 9 (Nyújtás)</span><span class="sxs-lookup"><span data-stu-id="f6d31-281">Debian 9 (Stretch)</span></span> | <span data-ttu-id="f6d31-282">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="f6d31-282">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="f6d31-283">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="f6d31-283">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="f6d31-284">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="f6d31-284">CentOS 7</span></span> <br> <span data-ttu-id="f6d31-285">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="f6d31-285">Oracle Linux 7</span></span> <br> <span data-ttu-id="f6d31-286">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="f6d31-286">RHEL 7</span></span> <br> <span data-ttu-id="f6d31-287">OpenSUSE OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="f6d31-287">OpenSUSE OpenSUSE 42.3</span></span> | <span data-ttu-id="f6d31-288">libunwind, libcurl, openssl-függvénytárak, libicu</span><span class="sxs-lookup"><span data-stu-id="f6d31-288">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="f6d31-289">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="f6d31-289">Fedora 27</span></span> <br> <span data-ttu-id="f6d31-290">28 Fedora</span><span class="sxs-lookup"><span data-stu-id="f6d31-290">Fedora 28</span></span> | <span data-ttu-id="f6d31-291">libunwind, libcurl, openssl-függvénytárak, libicu, a/compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="f6d31-291">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="f6d31-292">Nem hivatalosan támogatott Linux-disztribúciókon a PowerShell bináris fájljainak telepítéséhez telepíteni szeretné a cél operációs rendszer szükséges függőséget a különálló lépések.</span><span class="sxs-lookup"><span data-stu-id="f6d31-292">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="f6d31-293">Például a [Amazon Linux dockerfile] [ amazon-dockerfile] először telepíti a függőségeket, és ezt követően kiolvassa a Linuxos `tar.gz` archív.</span><span class="sxs-lookup"><span data-stu-id="f6d31-293">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="f6d31-294">Telepítés – bináris archívum</span><span class="sxs-lookup"><span data-stu-id="f6d31-294">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="f6d31-295">Linux</span><span class="sxs-lookup"><span data-stu-id="f6d31-295">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="f6d31-296">Bináris archívum eltávolítása</span><span class="sxs-lookup"><span data-stu-id="f6d31-296">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="f6d31-297">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="f6d31-297">Paths</span></span>

* <span data-ttu-id="f6d31-298">`$PSHOME` van `/opt/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="f6d31-298">`$PSHOME` is `/opt/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="f6d31-299">Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="f6d31-299">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="f6d31-300">Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="f6d31-300">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="f6d31-301">Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="f6d31-301">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="f6d31-302">Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="f6d31-302">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="f6d31-303">Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="f6d31-303">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="f6d31-304">PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="f6d31-304">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="f6d31-305">A profilok tiszteletben PowerShell a gazdagép konfiguráció, így az alapértelmezett gazdagép-specifikus profilok létezik `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="f6d31-305">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="f6d31-306">PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="f6d31-306">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
