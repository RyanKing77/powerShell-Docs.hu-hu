# <a name="installing-powershell-core-on-macos-and-linux"></a><span data-ttu-id="2fd21-101">MacOS és Linux PowerShell központi telepítése</span><span class="sxs-lookup"><span data-stu-id="2fd21-101">Installing PowerShell Core on macOS and Linux</span></span>

<span data-ttu-id="2fd21-102">Támogatja a [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.04] [ u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25 ] [ fed25], [Fedora 26][fed26], [architektúrája Linux][arch], és [macOS 10.12][mac].</span><span class="sxs-lookup"><span data-stu-id="2fd21-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.04][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25][fed25], [Fedora 26][fed26], [Arch Linux][arch], and [macOS 10.12][mac].</span></span>

<span data-ttu-id="2fd21-103">A Linux terjesztéseket, amelyek hivatalosan nem támogatottak, próbálkozhat a [PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="2fd21-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span>
<span data-ttu-id="2fd21-104">Közvetlenül a Linux-használat PowerShell bináris fájljainak telepítéséhez is megpróbálhatja [ `tar.gz` archív][tar], de állítsa be a szükséges függőségek az operációs rendszer, a különálló lépések alapján kell.</span><span class="sxs-lookup"><span data-stu-id="2fd21-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="2fd21-105">Minden csomagok érhetők el a githubon [kiadott][] lap.</span><span class="sxs-lookup"><span data-stu-id="2fd21-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="2fd21-106">A csomag telepítése után futtassa `pwsh` terminálról.</span><span class="sxs-lookup"><span data-stu-id="2fd21-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u17]: #ubuntu-1704
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-422
[fed25]: #fedora-25
[fed26]: #fedora-26
[arch]: #arch-linux
[lai]: #linux-appimage
[mac]: #macos-1012
[tar]: #binary-archives

## <a name="ubuntu-1404"></a><span data-ttu-id="2fd21-107">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="2fd21-107">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="2fd21-108">Telepítési csomag tárház - Ubuntu 14.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="2fd21-108">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="2fd21-109">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="2fd21-109">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="2fd21-110">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="2fd21-110">This is the preferred method.</span></span>

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

<span data-ttu-id="2fd21-111">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="2fd21-111">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="2fd21-112">Közvetlen letöltése – Ubuntu 14.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="2fd21-112">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="2fd21-113">A Debian csomag `powershell_6.0.0-rc-1.ubuntu.14.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="2fd21-113">Download the Debian package `powershell_6.0.0-rc-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="2fd21-114">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="2fd21-114">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-rc-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="2fd21-115">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="2fd21-115">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="2fd21-116">Az Eltávolítás - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="2fd21-116">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="2fd21-117">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="2fd21-117">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="2fd21-118">Telepítési csomag tárház - Ubuntu 16.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="2fd21-118">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="2fd21-119">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="2fd21-119">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="2fd21-120">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="2fd21-120">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="2fd21-121">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="2fd21-121">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="2fd21-122">Közvetlen letöltése – Ubuntu 16.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="2fd21-122">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="2fd21-123">A Debian csomag `powershell_6.0.0-rc-1.ubuntu.16.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="2fd21-123">Download the Debian package `powershell_6.0.0-rc-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="2fd21-124">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="2fd21-124">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-rc-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="2fd21-125">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="2fd21-125">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="2fd21-126">Az Eltávolítás - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="2fd21-126">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1704"></a><span data-ttu-id="2fd21-127">Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="2fd21-127">Ubuntu 17.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1704"></a><span data-ttu-id="2fd21-128">Telepítési csomag tárház - Ubuntu 17.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="2fd21-128">Installation via Package Repository - Ubuntu 17.04</span></span>

<span data-ttu-id="2fd21-129">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="2fd21-129">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="2fd21-130">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="2fd21-130">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
curl https://packages.microsoft.com/config/ubuntu/17.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="2fd21-131">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="2fd21-131">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1704"></a><span data-ttu-id="2fd21-132">Közvetlen letöltése – Ubuntu 17.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="2fd21-132">Installation via Direct Download - Ubuntu 17.04</span></span>

<span data-ttu-id="2fd21-133">A Debian csomag `powershell_6.0.0-rc-1.ubuntu.17.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="2fd21-133">Download the Debian package `powershell_6.0.0-rc-1.ubuntu.17.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="2fd21-134">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="2fd21-134">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-rc-1.ubuntu.17.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="2fd21-135">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="2fd21-135">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1704"></a><span data-ttu-id="2fd21-136">Az Eltávolítás - Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="2fd21-136">Uninstallation - Ubuntu 17.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="2fd21-137">Debian 8</span><span class="sxs-lookup"><span data-stu-id="2fd21-137">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="2fd21-138">Telepítési csomag tárház - Debian 8 keresztül</span><span class="sxs-lookup"><span data-stu-id="2fd21-138">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="2fd21-139">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="2fd21-139">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="2fd21-140">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="2fd21-140">This is the preferred method.</span></span>

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

<span data-ttu-id="2fd21-141">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="2fd21-141">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="2fd21-142">Keresztül közvetlen letöltése – Debian 8 telepítése</span><span class="sxs-lookup"><span data-stu-id="2fd21-142">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="2fd21-143">A Debian csomag `powershell_6.0.0-rc-1.debian.8_amd64.deb` a a [kiadott][] a Debian gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="2fd21-143">Download the Debian package `powershell_6.0.0-rc-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="2fd21-144">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="2fd21-144">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-rc-1.debian.8_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="2fd21-145">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="2fd21-145">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="2fd21-146">Az Eltávolítás - Debian 8</span><span class="sxs-lookup"><span data-stu-id="2fd21-146">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="2fd21-147">Debian 9</span><span class="sxs-lookup"><span data-stu-id="2fd21-147">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="2fd21-148">Telepítési csomag tárház – Debian 9 keresztül</span><span class="sxs-lookup"><span data-stu-id="2fd21-148">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="2fd21-149">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="2fd21-149">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="2fd21-150">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="2fd21-150">This is the preferred method.</span></span>

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

<span data-ttu-id="2fd21-151">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="2fd21-151">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="2fd21-152">Közvetlen letöltése – Debian 9 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="2fd21-152">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="2fd21-153">A Debian csomag `powershell_6.0.0-rc-1.debian.9_amd64.deb` a a [kiadott][] a Debian gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="2fd21-153">Download the Debian package `powershell_6.0.0-rc-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="2fd21-154">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="2fd21-154">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-rc-1.debian.9_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="2fd21-155">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="2fd21-155">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-9"></a><span data-ttu-id="2fd21-156">Az Eltávolítás - Debian 9</span><span class="sxs-lookup"><span data-stu-id="2fd21-156">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="2fd21-157">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="2fd21-157">CentOS 7</span></span>

> <span data-ttu-id="2fd21-158">Ez a csomag is működik-e az Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="2fd21-158">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="2fd21-159">Telepítési csomag tárház (ajánlott) – CentOS 7 keresztül</span><span class="sxs-lookup"><span data-stu-id="2fd21-159">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="2fd21-160">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="2fd21-160">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="2fd21-161">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="2fd21-161">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="2fd21-162">Közvetlen letöltése – CentOS 7 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="2fd21-162">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="2fd21-163">Használatával [CentOS 7][], a RPM csomag `powershell-6.0.0_rc-1.rhel.7.x86_64.rpm` a a [kiadott][] a CentOS gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="2fd21-163">Using [CentOS 7][], download the RPM package `powershell-6.0.0_rc-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="2fd21-164">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="2fd21-164">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.0_rc-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="2fd21-165">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="2fd21-165">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-rc/powershell-6.0.0_rc-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="2fd21-166">Az Eltávolítás - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="2fd21-166">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="2fd21-168">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="2fd21-168">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="2fd21-169">Telepítési csomag tárház (ajánlott) - Red Hat Enterprise Linux (RHEL) 7 keresztül</span><span class="sxs-lookup"><span data-stu-id="2fd21-169">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="2fd21-170">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="2fd21-170">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="2fd21-171">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="2fd21-171">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="2fd21-172">Közvetlen letöltése – Red Hat Enterprise Linux (RHEL) 7 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="2fd21-172">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="2fd21-173">A RPM csomag `powershell-6.0.0_rc-1.rhel.7.x86_64.rpm` a a [kiadott][] a Red Hat Enterprise Linux-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="2fd21-173">Download the RPM package `powershell-6.0.0_rc-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="2fd21-174">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="2fd21-174">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.0_rc-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="2fd21-175">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="2fd21-175">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-rc/powershell-6.0.0_rc-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="2fd21-176">Az Eltávolítás - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="2fd21-176">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a><span data-ttu-id="2fd21-177">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="2fd21-177">OpenSUSE 42.2</span></span>

> <span data-ttu-id="2fd21-178">**Megjegyzés:** PowerShell Core telepítése esetén a OpenSUSE jelenthet, semmi nem biztosít `libcurl`.</span><span class="sxs-lookup"><span data-stu-id="2fd21-178">**Note:** When installing PowerShell Core, OpenSUSE may report that nothing provides `libcurl`.</span></span>
<span data-ttu-id="2fd21-179">`libcurl`már telepíthető OpenSUSE támogatott verzióit.</span><span class="sxs-lookup"><span data-stu-id="2fd21-179">`libcurl` should already be installed on supported versions of OpenSUSE.</span></span>
<span data-ttu-id="2fd21-180">Futtatás `zypper search libcurl` megerősítéséhez.</span><span class="sxs-lookup"><span data-stu-id="2fd21-180">Run `zypper search libcurl` to confirm.</span></span>
<span data-ttu-id="2fd21-181">A hiba 2 'megoldások"jelent.</span><span class="sxs-lookup"><span data-stu-id="2fd21-181">The error will present 2 'solutions'.</span></span> <span data-ttu-id="2fd21-182">Válassza ki a "Megoldás 2" PowerShell Core telepítésének folytatásához.</span><span class="sxs-lookup"><span data-stu-id="2fd21-182">Choose 'Solution 2' to continue installing PowerShell Core.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-422"></a><span data-ttu-id="2fd21-183">Telepítési csomag tárház (ajánlott) - OpenSUSE 42.2 keresztül</span><span class="sxs-lookup"><span data-stu-id="2fd21-183">Installation via Package Repository (preferred) - OpenSUSE 42.2</span></span>

<span data-ttu-id="2fd21-184">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="2fd21-184">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---opensuse-422"></a><span data-ttu-id="2fd21-185">Közvetlen letöltése – OpenSUSE 42.2 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="2fd21-185">Installation via Direct Download - OpenSUSE 42.2</span></span>

<span data-ttu-id="2fd21-186">A RPM csomag `powershell-6.0.0_rc-1.rhel.7.x86_64.rpm` a a [kiadott][] a OpenSUSE gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="2fd21-186">Download the RPM package `powershell-6.0.0_rc-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.0_rc-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="2fd21-187">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="2fd21-187">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-rc/powershell-6.0.0_rc-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a><span data-ttu-id="2fd21-188">Az Eltávolítás - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="2fd21-188">Uninstallation - OpenSUSE 42.2</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora-25"></a><span data-ttu-id="2fd21-189">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="2fd21-189">Fedora 25</span></span>

### <a name="installation-via-package-repository-preferred---fedora-25"></a><span data-ttu-id="2fd21-190">Telepítési csomag tárház (ajánlott) - Fedora 25 keresztül</span><span class="sxs-lookup"><span data-stu-id="2fd21-190">Installation via Package Repository (preferred) - Fedora 25</span></span>

<span data-ttu-id="2fd21-191">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="2fd21-191">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft signature key
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Update the list of products
sudo dnf update

# Install PowerShell
sudo dnf install -y powershell

# Start PowerShell
pwsh
```

### <a name="installation-via-direct-download---fedora-25"></a><span data-ttu-id="2fd21-192">Közvetlen letöltése – Fedora 25 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="2fd21-192">Installation via Direct Download - Fedora 25</span></span>

<span data-ttu-id="2fd21-193">A RPM csomag `powershell-6.0.0_rc-1.rhel.7.x86_64.rpm` a a [kiadott][] a Fedora gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="2fd21-193">Download the RPM package `powershell-6.0.0_rc-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="2fd21-194">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="2fd21-194">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install powershell-6.0.0_rc-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="2fd21-195">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="2fd21-195">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-rc/powershell-6.0.0_rc-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-25"></a><span data-ttu-id="2fd21-196">Az Eltávolítás - Fedora 25</span><span class="sxs-lookup"><span data-stu-id="2fd21-196">Uninstallation - Fedora 25</span></span>

```sh
sudo dnf remove powershell
```

## <a name="fedora-26"></a><span data-ttu-id="2fd21-197">26 Fedora</span><span class="sxs-lookup"><span data-stu-id="2fd21-197">Fedora 26</span></span>

### <a name="installation-via-package-repository-preferred---fedora-26"></a><span data-ttu-id="2fd21-198">Telepítési csomag tárház (ajánlott) - Fedora 26 keresztül</span><span class="sxs-lookup"><span data-stu-id="2fd21-198">Installation via Package Repository (preferred) - Fedora 26</span></span>

<span data-ttu-id="2fd21-199">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="2fd21-199">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-26"></a><span data-ttu-id="2fd21-200">Közvetlen letöltése – Fedora 26 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="2fd21-200">Installation via Direct Download - Fedora 26</span></span>

<span data-ttu-id="2fd21-201">A RPM csomag `powershell-6.0.0_rc-1.rhel.7.x86_64.rpm` a a [kiadott][] a Fedora gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="2fd21-201">Download the RPM package `powershell-6.0.0_rc-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="2fd21-202">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="2fd21-202">Then execute the following in the terminal:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.0_rc-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="2fd21-203">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="2fd21-203">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-rc/powershell-6.0.0_rc-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-26"></a><span data-ttu-id="2fd21-204">Az Eltávolítás - Fedora 26</span><span class="sxs-lookup"><span data-stu-id="2fd21-204">Uninstallation - Fedora 26</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="2fd21-205">Linux architektúrája</span><span class="sxs-lookup"><span data-stu-id="2fd21-205">Arch Linux</span></span>

<span data-ttu-id="2fd21-206">PowerShell érhető el a [architektúrája Linux][] felhasználói tárház (AUR).</span><span class="sxs-lookup"><span data-stu-id="2fd21-206">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="2fd21-207">Az összeállítható a [legújabb címkézett kiadás][arch-release]</span><span class="sxs-lookup"><span data-stu-id="2fd21-207">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="2fd21-208">Az összeállítható a [fő legújabb véglegesítési][arch-git]</span><span class="sxs-lookup"><span data-stu-id="2fd21-208">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="2fd21-209">Használatával telepíthető a [bináris legújabb kiadás][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="2fd21-209">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="2fd21-210">A AUR csomagok karbantartása közösségi – nincs hivatalos támogatás.</span><span class="sxs-lookup"><span data-stu-id="2fd21-210">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="2fd21-211">A csomagok telepítése a AUR a további információkért lásd: a [architektúrája Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a közösségi [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="2fd21-211">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[architektúrája Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="2fd21-213">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="2fd21-213">Linux AppImage</span></span>

<span data-ttu-id="2fd21-214">A legutóbbi Linux-eloszlás használatával töltse le a AppImage `powershell-6.0.0-rc-x86_64.AppImage` a a [kiadott][] a Linux-gépek oldalon.</span><span class="sxs-lookup"><span data-stu-id="2fd21-214">Using a recent Linux distribution, download the AppImage `powershell-6.0.0-rc-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="2fd21-215">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="2fd21-215">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.0-rc-x86_64.AppImage
./powershell-6.0.0-rc-x86_64.AppImage
```

<span data-ttu-id="2fd21-216">A [AppImage][] lehetővé teszi, hogy a telepítés nélküli PowerShell futtatásához.</span><span class="sxs-lookup"><span data-stu-id="2fd21-216">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="2fd21-217">Egy hordozható alkalmazás, amely a PowerShell és a függőségek (beleértve a .NET Core rendszer függőségeket) bundles egy javul csomagba.</span><span class="sxs-lookup"><span data-stu-id="2fd21-217">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="2fd21-218">Ez a csomag a felhasználó a Linux-disztribúció függetlenül működik, és egyetlen bináris értékké.</span><span class="sxs-lookup"><span data-stu-id="2fd21-218">This package works independently of the user's Linux distribution, and is a single binary.</span></span>

[appimage]: http://appimage.org/

## <a name="macos-1012"></a><span data-ttu-id="2fd21-220">macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="2fd21-220">macOS 10.12</span></span>

### <a name="installation-via-homebrew-preferred---macos-1012"></a><span data-ttu-id="2fd21-221">Telepítési Homebrew (ajánlott) - macOS 10.12 keresztül</span><span class="sxs-lookup"><span data-stu-id="2fd21-221">Installation via Homebrew (preferred) - macOS 10.12</span></span>

<span data-ttu-id="2fd21-222">[Homebrew] [ brew] a hiányzó Csomagkezelőt a macOS van.</span><span class="sxs-lookup"><span data-stu-id="2fd21-222">[Homebrew][brew] is the missing package manager for macOS.</span></span>
<span data-ttu-id="2fd21-223">Ha a `brew` parancs nem található, telepítenie kell a következő Homebrew [a utasításaikat][brew].</span><span class="sxs-lookup"><span data-stu-id="2fd21-223">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="2fd21-224">Homebrew telepítése után is könnyen PowerShell telepítése.</span><span class="sxs-lookup"><span data-stu-id="2fd21-224">Once you've installed Homebrew, installing PowerShell is easy.</span></span>
<span data-ttu-id="2fd21-225">Először telepítse [Homebrew-Cask][cask], így további csomagok telepítése:</span><span class="sxs-lookup"><span data-stu-id="2fd21-225">First, install [Homebrew-Cask][cask], so you can install more packages:</span></span>

```sh
brew tap caskroom/cask
```

<span data-ttu-id="2fd21-226">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="2fd21-226">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="2fd21-227">PowerShell új verzióinak kiadásakor egyszerűen Homebrew tartozó képletek frissítése, és PowerShell frissítése:</span><span class="sxs-lookup"><span data-stu-id="2fd21-227">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask reinstall powershell
```

> <span data-ttu-id="2fd21-228">Megjegyzés: miatt: [ezt a problémát Cask](https://github.com/caskroom/homebrew-cask/issues/29301), jelenleg van, hogy egy reinstall frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="2fd21-228">Note: because of [this issue in Cask](https://github.com/caskroom/homebrew-cask/issues/29301), you currently have to do a reinstall to upgrade.</span></span>

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/

### <a name="installation-via-direct-download---macos-1012"></a><span data-ttu-id="2fd21-229">Közvetlen letöltés - macOS 10.12 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="2fd21-229">Installation via Direct Download - macOS 10.12</span></span>

<span data-ttu-id="2fd21-230">MacOS 10.12 használ, töltse le a PKG csomagot `powershell-6.0.0-rc-osx.10.12-x64.pkg` a a [kiadott][] lap települ a macOS gépre.</span><span class="sxs-lookup"><span data-stu-id="2fd21-230">Using macOS 10.12, download the PKG package `powershell-6.0.0-rc-osx.10.12-x64.pkg` from the [releases][] page onto the macOS machine.</span></span>

<span data-ttu-id="2fd21-231">Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítse azt a Terminálszolgáltatások:</span><span class="sxs-lookup"><span data-stu-id="2fd21-231">Either double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.0-rc-osx.10.12-x64.pkg -target /
```

### <a name="uninstallation---macos-1012"></a><span data-ttu-id="2fd21-232">Az Eltávolítás - macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="2fd21-232">Uninstallation - macOS 10.12</span></span>

<span data-ttu-id="2fd21-233">PowerShell Homebrew telepítette, ha az Eltávolítás könnyen:</span><span class="sxs-lookup"><span data-stu-id="2fd21-233">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="2fd21-234">Ha telepítette a PowerShell segítségével közvetlen letöltési, PowerShell manuálisan kell eltávolítani:</span><span class="sxs-lookup"><span data-stu-id="2fd21-234">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="2fd21-235">Távolítsa el a további PowerShell útvonalak (például a felhasználói profil elérési útja) tekintse meg a [elérési utak] [ paths] ebben a dokumentumban az alábbi szakaszt, és távolítsa el a kívánt az elérési utak `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="2fd21-235">To uninstall the additional PowerShell paths (such as the user profile path) please see the [paths][paths] section below in this document and remove the desired the paths with `sudo rm`.</span></span>
<span data-ttu-id="2fd21-236">(Megjegyzés: Ez nem szükséges, ha telepítette a Homebrew.)</span><span class="sxs-lookup"><span data-stu-id="2fd21-236">(Note: this is not necessary if you installed with Homebrew.)</span></span>

[paths]:#paths

## <a name="kali"></a><span data-ttu-id="2fd21-237">Kali</span><span class="sxs-lookup"><span data-stu-id="2fd21-237">Kali</span></span>

### <a name="installation"></a><span data-ttu-id="2fd21-238">Telepítés</span><span class="sxs-lookup"><span data-stu-id="2fd21-238">Installation</span></span>

```sh
# Install prerequisites
apt-get install libunwind8 libicu55
wget http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb
dpkg -i libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb

# Install PowerShell
dpkg -i powershell_6.0.0-rc-1.ubuntu.16.04_amd64.deb

# Start PowerShell
pwsh
```

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="2fd21-239">Futtassa a PowerShell legújabb Kali (Kali GNU/Linux folyamatos) a telepítés nélküli</span><span class="sxs-lookup"><span data-stu-id="2fd21-239">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-rc/powershell-6.0.0-rc-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.0-rc-x86_64.AppImage

# Start PowerShell
./powershell-6.0.0-rc-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="2fd21-240">Az Eltávolítás - Kali</span><span class="sxs-lookup"><span data-stu-id="2fd21-240">Uninstallation - Kali</span></span>

```sh
dpkg -r powershell_6.0.0-rc-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="2fd21-241">Raspbian</span><span class="sxs-lookup"><span data-stu-id="2fd21-241">Raspbian</span></span>

<span data-ttu-id="2fd21-242">PowerShell jelenleg csak Raspbian Stretch támogatott.</span><span class="sxs-lookup"><span data-stu-id="2fd21-242">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

### <a name="installation"></a><span data-ttu-id="2fd21-243">Telepítés</span><span class="sxs-lookup"><span data-stu-id="2fd21-243">Installation</span></span>

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-rc/powershell-6.0.0-rc-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.0.0-rc-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="2fd21-244">Az Eltávolítás - Raspbian</span><span class="sxs-lookup"><span data-stu-id="2fd21-244">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="2fd21-245">Bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="2fd21-245">Binary Archives</span></span>

<span data-ttu-id="2fd21-246">PowerShell bináris `tar.gz` archívumokat előírt macOS és Linux platformokat, a központi telepítési forgatókönyvek engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="2fd21-246">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="2fd21-247">Függőségek</span><span class="sxs-lookup"><span data-stu-id="2fd21-247">Dependencies</span></span>

<span data-ttu-id="2fd21-248">Linux PowerShell alkot az összes Linux terjesztésekről hordozható bináris fájljait.</span><span class="sxs-lookup"><span data-stu-id="2fd21-248">For Linux, PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="2fd21-249">De a .NET Core runtime szükséges a különböző terjesztések átviteli különböző függőségek, és ezért PowerShell szerepe ugyanaz.</span><span class="sxs-lookup"><span data-stu-id="2fd21-249">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="2fd21-250">Az alábbi ábra mutatja a .NET Core 2.0 függőségek különböző Linux terjesztések átviteli hivatalosan támogatott.</span><span class="sxs-lookup"><span data-stu-id="2fd21-250">The following chart shows the .NET Core 2.0 dependencies on different Linux distributions that are officially supported.</span></span>

| <span data-ttu-id="2fd21-251">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="2fd21-251">OS</span></span>                 | <span data-ttu-id="2fd21-252">Függőségek</span><span class="sxs-lookup"><span data-stu-id="2fd21-252">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="2fd21-253">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="2fd21-253">Ubuntu 14.04</span></span>       | <span data-ttu-id="2fd21-254">libc6, libgcc1, libgssapi-krb5-2 liblttng-ust0, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="2fd21-254">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="2fd21-255">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="2fd21-255">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="2fd21-256">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="2fd21-256">Ubuntu 16.04</span></span>       | <span data-ttu-id="2fd21-257">libc6, libgcc1, libgssapi-krb5-2 liblttng-ust0, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="2fd21-257">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="2fd21-258">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="2fd21-258">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="2fd21-259">Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="2fd21-259">Ubuntu 17.04</span></span>       | <span data-ttu-id="2fd21-260">libc6, libgcc1, libgssapi-krb5-2 liblttng-ust0, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="2fd21-260">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="2fd21-261">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="2fd21-261">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="2fd21-262">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="2fd21-262">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="2fd21-263">libc6, libgcc1, libgssapi-krb5-2 liblttng-ust0, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="2fd21-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="2fd21-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="2fd21-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="2fd21-265">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="2fd21-265">Debian 9 (Stretch)</span></span> | <span data-ttu-id="2fd21-266">libc6, libgcc1, libgssapi-krb5-2 liblttng-ust0, libstdc ++ 6,</span><span class="sxs-lookup"><span data-stu-id="2fd21-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="2fd21-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="2fd21-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="2fd21-268">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="2fd21-268">CentOS 7</span></span> <br> <span data-ttu-id="2fd21-269">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="2fd21-269">Oracle Linux 7</span></span> <br> <span data-ttu-id="2fd21-270">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="2fd21-270">RHEL 7</span></span> <br> <span data-ttu-id="2fd21-271">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="2fd21-271">OpenSUSE 42.2</span></span> <br> <span data-ttu-id="2fd21-272">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="2fd21-272">Fedora 25</span></span> | <span data-ttu-id="2fd21-273">libunwind, libcurl, openssl-függvénytárak, libicu</span><span class="sxs-lookup"><span data-stu-id="2fd21-273">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="2fd21-274">26 Fedora</span><span class="sxs-lookup"><span data-stu-id="2fd21-274">Fedora 26</span></span>          | <span data-ttu-id="2fd21-275">libunwind, libcurl, openssl-függvénytárak, libicu, / compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="2fd21-275">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="2fd21-276">PowerShell bináris fájljait, a Linux terjesztéseket hivatalosan nem támogatott központi telepítéséhez, akkor kellene telepíteni a szükséges függőségek a cél operációs rendszer a különálló lépések.</span><span class="sxs-lookup"><span data-stu-id="2fd21-276">In order to deploy PowerShell binaries on Linux distributions that are not officially supported, you would need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="2fd21-277">Például a [Amazon Linux dockerfile] [ amazon-dockerfile] függőségek először telepíti, és kinyeri a Linux `tar.gz` archív.</span><span class="sxs-lookup"><span data-stu-id="2fd21-277">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="2fd21-278">Telepítés – bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="2fd21-278">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="2fd21-279">Linux</span><span class="sxs-lookup"><span data-stu-id="2fd21-279">Linux</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-rc/powershell-6.0.0-rc-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.0.0-rc

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.0.0-rc

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.0-rc/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.0.0-rc/pwsh /usr/bin/pwsh
```

#### <a name="macos"></a><span data-ttu-id="2fd21-280">macOS</span><span class="sxs-lookup"><span data-stu-id="2fd21-280">macOS</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.0-rc/powershell-6.0.0-rc-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.0.0-rc

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.0.0-rc

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.0-rc/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.0.0-rc/pwsh /usr/local/bin/pwsh
```

### <a name="uninstallation---binary-archives"></a><span data-ttu-id="2fd21-281">Az Eltávolítás - bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="2fd21-281">Uninstallation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="2fd21-282">Linux</span><span class="sxs-lookup"><span data-stu-id="2fd21-282">Linux</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

#### <a name="macos"></a><span data-ttu-id="2fd21-283">macOS</span><span class="sxs-lookup"><span data-stu-id="2fd21-283">macOS</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="2fd21-284">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="2fd21-284">Paths</span></span>

* <span data-ttu-id="2fd21-285">`$PSHOME`van`/opt/microsoft/powershell/6.0.0-rc/`</span><span class="sxs-lookup"><span data-stu-id="2fd21-285">`$PSHOME` is `/opt/microsoft/powershell/6.0.0-rc/`</span></span>
* <span data-ttu-id="2fd21-286">Felhasználói profilok rendszer nem olvas be`~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="2fd21-286">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="2fd21-287">Alapértelmezett profilok rendszer nem olvas be`$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="2fd21-287">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="2fd21-288">Modulok felhasználói rendszer nem olvas be`~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="2fd21-288">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="2fd21-289">Megosztott modulok rendszer nem olvas be`/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="2fd21-289">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="2fd21-290">Az alapértelmezett modulokat rendszer nem olvas be`$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="2fd21-290">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="2fd21-291">A rögzítendő PSReadline előzmények`~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="2fd21-291">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="2fd21-292">A profilok tiszteletben PowerShell gazdagép konfiguráció, így az alapértelmezett gazdagép-specifikus profilok létezik az `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="2fd21-292">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="2fd21-293">A Linux és macOS a [XDG Base könyvtár megadása] [ xdg-bds] tiszteletben tartását.</span><span class="sxs-lookup"><span data-stu-id="2fd21-293">On Linux and macOS, the [XDG Base Directory Specification][xdg-bds] is respected.</span></span>

<span data-ttu-id="2fd21-294">Vegye figyelembe, hogy mivel macOS BSD, származtatott helyett `/opt`, a használt előtag `/usr/local`.</span><span class="sxs-lookup"><span data-stu-id="2fd21-294">Note that because macOS is a derivation of BSD, instead of `/opt`, the prefix used is `/usr/local`.</span></span>
<span data-ttu-id="2fd21-295">Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.0.0-rc/`, és a symlink van elhelyezve `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="2fd21-295">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.0-rc/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

[kiadott]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
