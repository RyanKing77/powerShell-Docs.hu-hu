---
title: A PowerShell Core telepítése Linux rendszerre
description: Információk a PowerShell Core különböző Linux-disztribúciókban való telepítéséről
ms.date: 07/19/2019
ms.openlocfilehash: 7d7c9a9f915f0a6e735a7baec1ec56e9c205a155
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848185"
---
# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="7a794-103">A PowerShell Core telepítése Linux rendszerre</span><span class="sxs-lookup"><span data-stu-id="7a794-103">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="7a794-104">Támogatja az [ubuntu 16,04][u16], [Ubuntu 18,04][u1804], [Ubuntu 18,10][u1810], [Ubuntu 19,04][u1904], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42,3][opensuse], [openSUSE LEAP 15][opensuse], [Fedora 27 ][fedora], [Fedora 28][fedora]és [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="7a794-104">Supports [Ubuntu 16.04][u16], [Ubuntu 18.04][u1804], [Ubuntu 18.10][u1810], [Ubuntu 19.04][u1904], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [openSUSE 42.3][opensuse], [openSUSE Leap 15][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="7a794-105">A hivatalosan nem támogatott Linux-disztribúciók esetében a PowerShell [beépülő modullal][snap]próbálhatja meg telepíteni a PowerShellt.</span><span class="sxs-lookup"><span data-stu-id="7a794-105">For Linux distributions that aren't officially supported, you can try to install PowerShell using the [PowerShell Snap Package][snap].</span></span> <span data-ttu-id="7a794-106">A PowerShell bináris fájljait közvetlenül a Linux [ `tar.gz` Archive][tar]használatával is kipróbálhatja, de az operációs rendszertől eltérő lépések alapján kell beállítania a szükséges függőségeket.</span><span class="sxs-lookup"><span data-stu-id="7a794-106">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="7a794-107">Minden csomag elérhető a GitHub- [releases][] oldalán.</span><span class="sxs-lookup"><span data-stu-id="7a794-107">All packages are available on our GitHub [releases][] page.</span></span> <span data-ttu-id="7a794-108">A csomag telepítése után futtassa `pwsh` a parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="7a794-108">After the package is installed, run `pwsh` from a terminal.</span></span>

[u16]: #ubuntu-1604
[u1804]: #ubuntu-1804
[u1810]: #ubuntu-1810
[u1904]: #ubuntu-1904
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse
[fedora]: #fedora
[arch]: #arch-linux
[snap]: #snap-package
[tar]: #binary-archives

## <a name="installing-preview-releases"></a><span data-ttu-id="7a794-109">Előzetes verziók telepítése</span><span class="sxs-lookup"><span data-stu-id="7a794-109">Installing Preview Releases</span></span>

<span data-ttu-id="7a794-110">Ha a Linux rendszerhez készült `powershell` `powershell-preview`PowerShell Core Preview kiadását csomag-adattáron keresztül telepíti, a csomag neve a verzióról a verzióra változik.</span><span class="sxs-lookup"><span data-stu-id="7a794-110">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="7a794-111">A közvetlen letöltésen keresztüli telepítés nem változik, a fájlnévtől eltérő módon.</span><span class="sxs-lookup"><span data-stu-id="7a794-111">Installing via direct download doesn't change, other than the file name.</span></span>

<span data-ttu-id="7a794-112">A következő táblázat tartalmazza a stabil és előnézeti csomagok telepítéséhez szükséges parancsokat a különböző csomagkezelő-kezelők használatával:</span><span class="sxs-lookup"><span data-stu-id="7a794-112">The following table contains the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="7a794-113">Eloszlás (ok)</span><span class="sxs-lookup"><span data-stu-id="7a794-113">Distribution(s)</span></span>|<span data-ttu-id="7a794-114">Stabil parancs</span><span class="sxs-lookup"><span data-stu-id="7a794-114">Stable Command</span></span> | <span data-ttu-id="7a794-115">Előnézet parancs</span><span class="sxs-lookup"><span data-stu-id="7a794-115">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="7a794-116">Ubuntu, Debian</span><span class="sxs-lookup"><span data-stu-id="7a794-116">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="7a794-117">CentOS, RedHat</span><span class="sxs-lookup"><span data-stu-id="7a794-117">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="7a794-118">Fedora</span><span class="sxs-lookup"><span data-stu-id="7a794-118">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1604"></a><span data-ttu-id="7a794-119">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="7a794-119">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="7a794-120">Telepítés a Package repository használatával – Ubuntu 16,04</span><span class="sxs-lookup"><span data-stu-id="7a794-120">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="7a794-121">A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében a csomagok tárházában van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="7a794-121">PowerShell Core for Linux is published to package repositories for easy installation and updates.</span></span>

<span data-ttu-id="7a794-122">Az előnyben részesített módszer a következő:</span><span class="sxs-lookup"><span data-stu-id="7a794-122">The preferred method is as follows:</span></span>

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

<span data-ttu-id="7a794-123">Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat.</span><span class="sxs-lookup"><span data-stu-id="7a794-123">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="7a794-124">A regisztrációt követően frissítheti a PowerShellt a `sudo apt-get upgrade powershell`használatával.</span><span class="sxs-lookup"><span data-stu-id="7a794-124">After registration, you can update PowerShell with `sudo apt-get upgrade powershell`.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="7a794-125">Telepítés közvetlen letöltéssel – Ubuntu 16,04</span><span class="sxs-lookup"><span data-stu-id="7a794-125">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="7a794-126">Töltse le a Debian `powershell_6.2.0-1.ubuntu.16.04_amd64.deb` -csomagot a [releases][] lapról az Ubuntu-gépre.</span><span class="sxs-lookup"><span data-stu-id="7a794-126">Download the Debian package `powershell_6.2.0-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="7a794-127">Ezután a terminálon hajtsa végre a következő parancsokat:</span><span class="sxs-lookup"><span data-stu-id="7a794-127">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="7a794-128">A `dpkg -i` parancs nem teljesíti a nem kielégíthető függőségeket.</span><span class="sxs-lookup"><span data-stu-id="7a794-128">The `dpkg -i` command fails with unmet dependencies.</span></span> <span data-ttu-id="7a794-129">A következő parancs megoldja `apt-get install -f` ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálását.</span><span class="sxs-lookup"><span data-stu-id="7a794-129">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="7a794-130">Eltávolítás – Ubuntu 16,04</span><span class="sxs-lookup"><span data-stu-id="7a794-130">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="7a794-131">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="7a794-131">Ubuntu 18.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="7a794-132">Telepítés a Package repository használatával – Ubuntu 18,04</span><span class="sxs-lookup"><span data-stu-id="7a794-132">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="7a794-133">A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében a csomagok tárházában van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="7a794-133">PowerShell Core for Linux is published to package repositories for easy installation and updates.</span></span>

<span data-ttu-id="7a794-134">Az előnyben részesített módszer a következő:</span><span class="sxs-lookup"><span data-stu-id="7a794-134">The preferred method is as follows:</span></span>

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

<span data-ttu-id="7a794-135">Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat.</span><span class="sxs-lookup"><span data-stu-id="7a794-135">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="7a794-136">A regisztrációt követően frissítheti a PowerShellt a `sudo apt-get upgrade powershell`használatával.</span><span class="sxs-lookup"><span data-stu-id="7a794-136">After registration, you can update PowerShell with `sudo apt-get upgrade powershell`.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="7a794-137">Telepítés közvetlen letöltéssel – Ubuntu 18,04</span><span class="sxs-lookup"><span data-stu-id="7a794-137">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="7a794-138">Töltse le a Debian `powershell_6.2.0-1.ubuntu.18.04_amd64.deb` -csomagot a [releases][] lapról az Ubuntu-gépre.</span><span class="sxs-lookup"><span data-stu-id="7a794-138">Download the Debian package `powershell_6.2.0-1.ubuntu.18.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="7a794-139">Ezután a terminálon hajtsa végre a következő parancsokat:</span><span class="sxs-lookup"><span data-stu-id="7a794-139">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="7a794-140">A `dpkg -i` parancs nem teljesíti a nem kielégíthető függőségeket.</span><span class="sxs-lookup"><span data-stu-id="7a794-140">The `dpkg -i` command fails with unmet dependencies.</span></span> <span data-ttu-id="7a794-141">A következő parancs megoldja `apt-get install -f` ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálását.</span><span class="sxs-lookup"><span data-stu-id="7a794-141">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1804"></a><span data-ttu-id="7a794-142">Eltávolítás – Ubuntu 18,04</span><span class="sxs-lookup"><span data-stu-id="7a794-142">Uninstallation - Ubuntu 18.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1810"></a><span data-ttu-id="7a794-143">Ubuntu 18,10</span><span class="sxs-lookup"><span data-stu-id="7a794-143">Ubuntu 18.10</span></span>

<span data-ttu-id="7a794-144">A telepítés a- `snapd`on keresztül támogatott.</span><span class="sxs-lookup"><span data-stu-id="7a794-144">Installation is supported via `snapd`.</span></span> <span data-ttu-id="7a794-145">Útmutatásért lásd: [snap csomag][snap].</span><span class="sxs-lookup"><span data-stu-id="7a794-145">For instructions, see [Snap Package][snap].</span></span>

> [!NOTE]
> <span data-ttu-id="7a794-146">Az Ubuntu 18,10 egy [átmeneti kiadás](https://www.ubuntu.com/about/release-cycle) , amelyet a [Közösség támogat](../powershell-support-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="7a794-146">Ubuntu 18.10 is an [interim release](https://www.ubuntu.com/about/release-cycle) that's [community supported](../powershell-support-lifecycle.md).</span></span>

## <a name="ubuntu-1904"></a><span data-ttu-id="7a794-147">Ubuntu 19,04</span><span class="sxs-lookup"><span data-stu-id="7a794-147">Ubuntu 19.04</span></span>

<span data-ttu-id="7a794-148">A telepítés a- `snapd`on keresztül támogatott.</span><span class="sxs-lookup"><span data-stu-id="7a794-148">Installation is supported via `snapd`.</span></span> <span data-ttu-id="7a794-149">Útmutatásért lásd: [snap csomag][snap].</span><span class="sxs-lookup"><span data-stu-id="7a794-149">For instructions, see [Snap Package][snap].</span></span>

> [!NOTE]
> <span data-ttu-id="7a794-150">Az Ubuntu 19,04 egy [átmeneti kiadás](https://www.ubuntu.com/about/release-cycle) , amelyet a [Közösség támogat](../powershell-support-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="7a794-150">Ubuntu 19.04 is an [interim release](https://www.ubuntu.com/about/release-cycle) that's [community supported](../powershell-support-lifecycle.md).</span></span>

## <a name="debian-8"></a><span data-ttu-id="7a794-151">Debian 8</span><span class="sxs-lookup"><span data-stu-id="7a794-151">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="7a794-152">Telepítés a Package repository használatával – Debian 8</span><span class="sxs-lookup"><span data-stu-id="7a794-152">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="7a794-153">A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében a csomagok tárházában van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="7a794-153">PowerShell Core for Linux is published to package repositories for easy installation and updates.</span></span>

<span data-ttu-id="7a794-154">Az előnyben részesített módszer a következő:</span><span class="sxs-lookup"><span data-stu-id="7a794-154">The preferred method is as follows:</span></span>

```sh
# Install system components
sudo apt-get update
sudo apt-get install -y curl apt-transport-https

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

<span data-ttu-id="7a794-155">Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat.</span><span class="sxs-lookup"><span data-stu-id="7a794-155">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="7a794-156">A regisztrációt követően frissítheti a PowerShellt a `sudo apt-get upgrade powershell`használatával.</span><span class="sxs-lookup"><span data-stu-id="7a794-156">After registration, you can update PowerShell with `sudo apt-get upgrade powershell`.</span></span>

## <a name="debian-9"></a><span data-ttu-id="7a794-157">Debian 9</span><span class="sxs-lookup"><span data-stu-id="7a794-157">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="7a794-158">Telepítés a Package repository használatával – Debian 9</span><span class="sxs-lookup"><span data-stu-id="7a794-158">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="7a794-159">A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében a csomagok tárházában van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="7a794-159">PowerShell Core for Linux is published to package repositories for easy installation and updates.</span></span>

<span data-ttu-id="7a794-160">Az előnyben részesített módszer a következő:</span><span class="sxs-lookup"><span data-stu-id="7a794-160">The preferred method is as follows:</span></span>

```sh
# Install system components
sudo apt-get update
sudo apt-get install -y curl gnupg apt-transport-https

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

<span data-ttu-id="7a794-161">Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat.</span><span class="sxs-lookup"><span data-stu-id="7a794-161">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="7a794-162">A regisztrációt követően frissítheti a PowerShellt a `sudo apt-get upgrade powershell`használatával.</span><span class="sxs-lookup"><span data-stu-id="7a794-162">After registration, you can update PowerShell with `sudo apt-get upgrade powershell`.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="7a794-163">Telepítés közvetlen letöltéssel – Debian 9</span><span class="sxs-lookup"><span data-stu-id="7a794-163">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="7a794-164">Töltse le a Debian `powershell_6.2.0-1.debian.9_amd64.deb` -csomagot a [releases][] lapról a Debian rendszerű gépre.</span><span class="sxs-lookup"><span data-stu-id="7a794-164">Download the Debian package `powershell_6.2.0-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="7a794-165">Ezután a terminálon hajtsa végre a következő parancsokat:</span><span class="sxs-lookup"><span data-stu-id="7a794-165">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo dpkg -i powershell_6.2.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="7a794-166">Eltávolítás – Debian 9</span><span class="sxs-lookup"><span data-stu-id="7a794-166">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="7a794-167">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="7a794-167">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="7a794-168">Ez a csomag Oracle Linux 7 rendszeren működik.</span><span class="sxs-lookup"><span data-stu-id="7a794-168">This package works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="7a794-169">Telepítés a Package repository használatával (előnyben részesített) – CentOS 7</span><span class="sxs-lookup"><span data-stu-id="7a794-169">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="7a794-170">A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében közzé van téve a hivatalos Microsoft-Tárházak számára.</span><span class="sxs-lookup"><span data-stu-id="7a794-170">PowerShell Core for Linux is published to official Microsoft repositories for easy installation and updates.</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="7a794-171">Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat.</span><span class="sxs-lookup"><span data-stu-id="7a794-171">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="7a794-172">A regisztrációt követően frissítheti a PowerShellt a `sudo yum update powershell`használatával.</span><span class="sxs-lookup"><span data-stu-id="7a794-172">After registration, you can update PowerShell with `sudo yum update powershell`.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="7a794-173">Telepítés közvetlen letöltéssel – CentOS 7</span><span class="sxs-lookup"><span data-stu-id="7a794-173">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="7a794-174">A [CentOS 7][]használatával töltse le az RPM `powershell-6.2.0-1.rhel.7.x86_64.rpm` -csomagot a [releases][] lapról a CentOS gépre.</span><span class="sxs-lookup"><span data-stu-id="7a794-174">Using [CentOS 7][], download the RPM package `powershell-6.2.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="7a794-175">Ezután a terminálon hajtsa végre a következő parancsokat:</span><span class="sxs-lookup"><span data-stu-id="7a794-175">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo yum install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="7a794-176">Az RPM a letöltés közbenső lépése nélkül is telepíthető:</span><span class="sxs-lookup"><span data-stu-id="7a794-176">You can install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="7a794-177">Eltávolítás – CentOS 7</span><span class="sxs-lookup"><span data-stu-id="7a794-177">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="7a794-179">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="7a794-179">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="7a794-180">Telepítés a Package repository használatával (előnyben részesített) – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="7a794-180">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="7a794-181">A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében közzé van téve a hivatalos Microsoft-Tárházak számára.</span><span class="sxs-lookup"><span data-stu-id="7a794-181">PowerShell Core for Linux is published to official Microsoft repositories for easy installation and updates.</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="7a794-182">Rendszergazdaként csak egyszer regisztrálja a Microsoft-tárházat.</span><span class="sxs-lookup"><span data-stu-id="7a794-182">As superuser, register the Microsoft repository once.</span></span> <span data-ttu-id="7a794-183">A regisztrációt követően frissítheti a PowerShellt a `sudo yum update powershell`használatával.</span><span class="sxs-lookup"><span data-stu-id="7a794-183">After registration, you can update PowerShell with `sudo yum update powershell`.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="7a794-184">Telepítés közvetlen letöltésen keresztül – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="7a794-184">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="7a794-185">Töltse le az RPM `powershell-6.2.0-1.rhel.7.x86_64.rpm` -csomagot a [releases][] lapról a Red Hat Enterprise Linux gépre.</span><span class="sxs-lookup"><span data-stu-id="7a794-185">Download the RPM package `powershell-6.2.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="7a794-186">Ezután a terminálon hajtsa végre a következő parancsokat:</span><span class="sxs-lookup"><span data-stu-id="7a794-186">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo yum install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="7a794-187">Az RPM a letöltés közbenső lépése nélkül is telepíthető:</span><span class="sxs-lookup"><span data-stu-id="7a794-187">You can install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="7a794-188">Eltávolítás – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="7a794-188">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse"></a><span data-ttu-id="7a794-189">openSUSE</span><span class="sxs-lookup"><span data-stu-id="7a794-189">openSUSE</span></span>

### <a name="installation---opensuse-423"></a><span data-ttu-id="7a794-190">Telepítés – openSUSE 42,3</span><span class="sxs-lookup"><span data-stu-id="7a794-190">Installation - openSUSE 42.3</span></span>

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

### <a name="installation---opensuse-leap-15"></a><span data-ttu-id="7a794-191">Telepítés – openSUSE LEAP 15</span><span class="sxs-lookup"><span data-stu-id="7a794-191">Installation - openSUSE Leap 15</span></span>

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

### <a name="uninstallation---opensuse-423-opensuse-leap-15"></a><span data-ttu-id="7a794-192">Eltávolítás – openSUSE 42,3, openSUSE – 15. Ugrás</span><span class="sxs-lookup"><span data-stu-id="7a794-192">Uninstallation - openSUSE 42.3, openSUSE Leap 15</span></span>

```sh
rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="fedora"></a><span data-ttu-id="7a794-193">Fedora</span><span class="sxs-lookup"><span data-stu-id="7a794-193">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="7a794-194">A Fedora 28 csak a PowerShell Core 6,1-es és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7a794-194">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="7a794-195">Telepítés a Package repository használatával (preferált) – Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="7a794-195">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="7a794-196">A Linux rendszerhez készült PowerShell Core az egyszerű telepítés és frissítés érdekében közzé van téve a hivatalos Microsoft-Tárházak számára.</span><span class="sxs-lookup"><span data-stu-id="7a794-196">PowerShell Core for Linux is published to official Microsoft repositories for easy installation and updates.</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="7a794-197">Telepítés közvetlen letöltésen keresztül – Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="7a794-197">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="7a794-198">Töltse le az RPM `powershell-6.2.0-1.rhel.7.x86_64.rpm` -csomagot a [releases][] lapról a Fedora gépre.</span><span class="sxs-lookup"><span data-stu-id="7a794-198">Download the RPM package `powershell-6.2.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="7a794-199">Ezután a terminálon hajtsa végre a következő parancsokat:</span><span class="sxs-lookup"><span data-stu-id="7a794-199">Then, in the terminal, execute the following commands:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.2.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="7a794-200">Az RPM a letöltés közbenső lépése nélkül is telepíthető:</span><span class="sxs-lookup"><span data-stu-id="7a794-200">You can install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.2.0/powershell-6.2.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="7a794-201">Eltávolítás – Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="7a794-201">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="7a794-202">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="7a794-202">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="7a794-203">Az Arch-támogatás kísérleti jellegű.</span><span class="sxs-lookup"><span data-stu-id="7a794-203">Arch support is experimental.</span></span>

<span data-ttu-id="7a794-204">A PowerShell az [Arch Linux][] User adattárból (Aur) érhető el.</span><span class="sxs-lookup"><span data-stu-id="7a794-204">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="7a794-205">A [legújabb címkézett kiadással][arch-release] állítható össze</span><span class="sxs-lookup"><span data-stu-id="7a794-205">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="7a794-206">A [legutóbbi véglegesítés a főkiszolgálóról][arch-git] lefordítható</span><span class="sxs-lookup"><span data-stu-id="7a794-206">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="7a794-207">A [legújabb kiadási bináris][arch-bin] fájl használatával telepíthető.</span><span class="sxs-lookup"><span data-stu-id="7a794-207">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="7a794-208">A rendszer karbantartja a csomagokat az AUR-ban; nincs hivatalos támogatás.</span><span class="sxs-lookup"><span data-stu-id="7a794-208">Packages in the AUR are community maintained; there's no official support.</span></span>

<span data-ttu-id="7a794-209">A csomagok az AUR-ból való telepítésével kapcsolatos további információkért tekintse meg az [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a közösségi [Docker](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile)című témakört.</span><span class="sxs-lookup"><span data-stu-id="7a794-209">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="snap-package"></a><span data-ttu-id="7a794-211">Csomag igazítása</span><span class="sxs-lookup"><span data-stu-id="7a794-211">Snap Package</span></span>

### <a name="getting-snapd"></a><span data-ttu-id="7a794-212">Beépülő modul beolvasása</span><span class="sxs-lookup"><span data-stu-id="7a794-212">Getting snapd</span></span>

<span data-ttu-id="7a794-213">`snapd`a illesztések futtatásához szükséges.</span><span class="sxs-lookup"><span data-stu-id="7a794-213">`snapd` is required to run snaps.</span></span> <span data-ttu-id="7a794-214">[Ezeket az utasításokat követve](https://docs.snapcraft.io/core/install) ellenőrizze, hogy `snapd` telepítve van-e.</span><span class="sxs-lookup"><span data-stu-id="7a794-214">Use [these instructions](https://docs.snapcraft.io/core/install) to make sure you have `snapd` installed.</span></span>

### <a name="installation-via-snap"></a><span data-ttu-id="7a794-215">Telepítés snap használatával</span><span class="sxs-lookup"><span data-stu-id="7a794-215">Installation via Snap</span></span>

<span data-ttu-id="7a794-216">A Linux rendszerhez készült PowerShell Core a könnyű telepítés és frissítés érdekében a [snap áruházban](https://snapcraft.io/store) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="7a794-216">PowerShell Core for Linux is published to the [Snap store](https://snapcraft.io/store) for easy installation and updates.</span></span>

<span data-ttu-id="7a794-217">Az előnyben részesített módszer a következő:</span><span class="sxs-lookup"><span data-stu-id="7a794-217">The preferred method is as follows:</span></span>

```sh
# Install PowerShell
sudo snap install powershell --classic

# Start PowerShell
pwsh
```

<span data-ttu-id="7a794-218">Az előzetes verzió telepítéséhez használja a következő metódust:</span><span class="sxs-lookup"><span data-stu-id="7a794-218">To install a preview version, use the following method:</span></span>

```sh
# Install PowerShell
sudo snap install powershell-preview --classic

# Start PowerShell
pwsh-preview
```

<span data-ttu-id="7a794-219">A telepítés után a Snap automatikusan frissül.</span><span class="sxs-lookup"><span data-stu-id="7a794-219">After installation, Snap will automatically upgrade.</span></span> <span data-ttu-id="7a794-220">A frissítést a vagy `sudo snap refresh powershell` `sudo snap refresh powershell-preview`a használatával aktiválhatja.</span><span class="sxs-lookup"><span data-stu-id="7a794-220">You can trigger an upgrade using `sudo snap refresh powershell` or `sudo snap refresh powershell-preview`.</span></span>

### <a name="uninstallation"></a><span data-ttu-id="7a794-221">Uninstallation</span><span class="sxs-lookup"><span data-stu-id="7a794-221">Uninstallation</span></span>

```sh
sudo snap remove powershell
```

<span data-ttu-id="7a794-222">vagy a</span><span class="sxs-lookup"><span data-stu-id="7a794-222">or</span></span>

```sh
sudo snap remove powershell-preview
```

## <a name="kali"></a><span data-ttu-id="7a794-223">Kali</span><span class="sxs-lookup"><span data-stu-id="7a794-223">Kali</span></span>

### <a name="installation---kali"></a><span data-ttu-id="7a794-224">Telepítés – Kali</span><span class="sxs-lookup"><span data-stu-id="7a794-224">Installation - Kali</span></span>

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

### <a name="uninstallation---kali"></a><span data-ttu-id="7a794-225">Eltávolítás – Kali</span><span class="sxs-lookup"><span data-stu-id="7a794-225">Uninstallation - Kali</span></span>

```sh
# Uninstall PowerShell package
apt-get remove -y powershell
```

## <a name="raspbian"></a><span data-ttu-id="7a794-226">Raspbian</span><span class="sxs-lookup"><span data-stu-id="7a794-226">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="7a794-227">A Raspbian-támogatás kísérleti jellegű.</span><span class="sxs-lookup"><span data-stu-id="7a794-227">Raspbian support is experimental.</span></span>

<span data-ttu-id="7a794-228">Jelenleg a PowerShell csak a Raspbian stretch esetében támogatott.</span><span class="sxs-lookup"><span data-stu-id="7a794-228">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="7a794-229">A CoreCLR és a PowerShell Core csak a pi 2 és a PI 3 rendszerű eszközökön működik, mint például a [PI Zero](https://github.com/dotnet/coreclr/issues/10605), nem támogatott processzorral rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="7a794-229">CoreCLR and PowerShell Core will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="7a794-230">Töltse le a [Raspbian stretch](https://www.raspberrypi.org/downloads/raspbian/) -t, és kövesse a [telepítési utasításokat](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) a PI-re való lekéréséhez.</span><span class="sxs-lookup"><span data-stu-id="7a794-230">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation---raspbian"></a><span data-ttu-id="7a794-231">Telepítés – Raspbian</span><span class="sxs-lookup"><span data-stu-id="7a794-231">Installation - Raspbian</span></span>

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

<span data-ttu-id="7a794-232">A PowerShell indításához a `pwsh` bináris elérési út megadása nélkül is létrehozhat egy szimbolikus hivatkozást.</span><span class="sxs-lookup"><span data-stu-id="7a794-232">Optionally, you can create a symbolic link to start PowerShell without specifying the path to the `pwsh` binary.</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="7a794-233">Eltávolítás – Raspbian</span><span class="sxs-lookup"><span data-stu-id="7a794-233">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="7a794-234">Bináris archívumok</span><span class="sxs-lookup"><span data-stu-id="7a794-234">Binary Archives</span></span>

<span data-ttu-id="7a794-235">A speciális `tar.gz` üzembe helyezési forgatókönyvek lehetővé tétele érdekében a PowerShell bináris archívumokat a linuxos platformokhoz biztosítjuk.</span><span class="sxs-lookup"><span data-stu-id="7a794-235">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="7a794-236">Függőségek</span><span class="sxs-lookup"><span data-stu-id="7a794-236">Dependencies</span></span>

<span data-ttu-id="7a794-237">A PowerShell hordozható bináris fájlokat hoz létre az összes Linux-disztribúcióhoz.</span><span class="sxs-lookup"><span data-stu-id="7a794-237">PowerShell builds portable binaries for all Linux distributions.</span></span> <span data-ttu-id="7a794-238">A .NET Core-futtatókörnyezet azonban eltérő függőségeket igényel a különböző disztribúciók esetében, és a PowerShell is.</span><span class="sxs-lookup"><span data-stu-id="7a794-238">But, .NET Core runtime requires different dependencies on different distributions, and PowerShell does too.</span></span>

<span data-ttu-id="7a794-239">A következő diagram a .NET Core 2,0-függőségeket mutatja be, amelyek a különböző Linux-disztribúciókban hivatalosan támogatottak.</span><span class="sxs-lookup"><span data-stu-id="7a794-239">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="7a794-240">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="7a794-240">OS</span></span>                 | <span data-ttu-id="7a794-241">Függőségek</span><span class="sxs-lookup"><span data-stu-id="7a794-241">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="7a794-242">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="7a794-242">Ubuntu 16.04</span></span>       | <span data-ttu-id="7a794-243">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="7a794-243">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="7a794-244">libcurl3, libunwind8, libuuid1, zlib1g, libssl 1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="7a794-244">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="7a794-245">Ubuntu 17,10</span><span class="sxs-lookup"><span data-stu-id="7a794-245">Ubuntu 17.10</span></span>       | <span data-ttu-id="7a794-246">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="7a794-246">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="7a794-247">libcurl3, libunwind8, libuuid1, zlib1g, libssl 1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="7a794-247">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="7a794-248">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="7a794-248">Ubuntu 18.04</span></span>       | <span data-ttu-id="7a794-249">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="7a794-249">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="7a794-250">libcurl3, libunwind8, libuuid1, zlib1g, libssl 1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="7a794-250">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="7a794-251">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="7a794-251">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="7a794-252">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="7a794-252">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="7a794-253">libcurl3, libunwind8, libuuid1, zlib1g, libssl 1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="7a794-253">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="7a794-254">Debian 9 (stretch)</span><span class="sxs-lookup"><span data-stu-id="7a794-254">Debian 9 (Stretch)</span></span> | <span data-ttu-id="7a794-255">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="7a794-255">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="7a794-256">libcurl3, libunwind8, libuuid1, zlib1g, libssl 1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="7a794-256">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="7a794-257">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="7a794-257">CentOS 7</span></span> <br> <span data-ttu-id="7a794-258">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="7a794-258">Oracle Linux 7</span></span> <br> <span data-ttu-id="7a794-259">7\. RHEL</span><span class="sxs-lookup"><span data-stu-id="7a794-259">RHEL 7</span></span> | <span data-ttu-id="7a794-260">libunwind, libcurl, OpenSSL-libs, libicu</span><span class="sxs-lookup"><span data-stu-id="7a794-260">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="7a794-261">openSUSE 42,3</span><span class="sxs-lookup"><span data-stu-id="7a794-261">openSUSE 42.3</span></span> | <span data-ttu-id="7a794-262">libcurl4, libopenssl1_0_0, libicu52_1</span><span class="sxs-lookup"><span data-stu-id="7a794-262">libcurl4, libopenssl1_0_0, libicu52_1</span></span> |
| <span data-ttu-id="7a794-263">openSUSE – 15. Ugrás</span><span class="sxs-lookup"><span data-stu-id="7a794-263">openSUSE Leap 15</span></span> | <span data-ttu-id="7a794-264">libcurl4, libopenssl1_0_0, libicu60_2</span><span class="sxs-lookup"><span data-stu-id="7a794-264">libcurl4, libopenssl1_0_0, libicu60_2</span></span> |
| <span data-ttu-id="7a794-265">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="7a794-265">Fedora 27</span></span> <br> <span data-ttu-id="7a794-266">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="7a794-266">Fedora 28</span></span> | <span data-ttu-id="7a794-267">libunwind, libcurl, OpenSSL-libs, libicu, kompatibilitás – openssl10</span><span class="sxs-lookup"><span data-stu-id="7a794-267">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="7a794-268">A nem hivatalosan támogatott Linux-disztribúciók PowerShell-bináris fájljainak telepítéséhez külön lépésben kell telepítenie a cél operációs rendszerhez szükséges függőségeket.</span><span class="sxs-lookup"><span data-stu-id="7a794-268">To deploy PowerShell binaries on Linux distributions that aren't officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span> <span data-ttu-id="7a794-269">Például az [Amazon Linux-Docker][amazon-dockerfile] először telepíti a függőségeket, majd kibontja `tar.gz` a Linux-archívumot.</span><span class="sxs-lookup"><span data-stu-id="7a794-269">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell-Docker/blob/master/release/community-stable/amazonlinux/docker/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="7a794-270">Telepítés – bináris archívumok</span><span class="sxs-lookup"><span data-stu-id="7a794-270">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="7a794-271">Linux</span><span class="sxs-lookup"><span data-stu-id="7a794-271">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="7a794-272">Bináris archívumok eltávolítása</span><span class="sxs-lookup"><span data-stu-id="7a794-272">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="7a794-273">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="7a794-273">Paths</span></span>

* <span data-ttu-id="7a794-274">`$PSHOME`van`/opt/microsoft/powershell/6.2.0/`</span><span class="sxs-lookup"><span data-stu-id="7a794-274">`$PSHOME` is `/opt/microsoft/powershell/6.2.0/`</span></span>
* <span data-ttu-id="7a794-275">A rendszer beolvassa a felhasználói profilokat`~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="7a794-275">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="7a794-276">Az alapértelmezett profilok a következő címről lesznek beolvasva:`$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="7a794-276">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="7a794-277">A felhasználói modulok a következő címről lesznek beolvasva:`~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="7a794-277">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="7a794-278">A megosztott modulok a következő címről lesznek beolvasva:`/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="7a794-278">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="7a794-279">Az alapértelmezett modulok a következő címről lesznek beolvasva:`$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="7a794-279">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="7a794-280">A PSReadline előzményei a következőre lesznek rögzítve`~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="7a794-280">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="7a794-281">A profilok figyelembe veszik a PowerShell gazdagép-konfigurációját, így az alapértelmezett gazdagép-specifikus profilok `Microsoft.PowerShell_profile.ps1` ugyanabban a helyen találhatók.</span><span class="sxs-lookup"><span data-stu-id="7a794-281">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="7a794-282">A PowerShell tiszteletben tartja a [XDG alap könyvtár specifikációját][xdg-bds] a Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="7a794-282">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
