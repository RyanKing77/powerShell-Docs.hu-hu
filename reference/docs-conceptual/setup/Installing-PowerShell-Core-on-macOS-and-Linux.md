# <a name="installing-powershell-core-on-macos-and-linux"></a><span data-ttu-id="61418-101">A PowerShell Core telepítése macOS és Linux rendszerre</span><span class="sxs-lookup"><span data-stu-id="61418-101">Installing PowerShell Core on macOS and Linux</span></span>

<span data-ttu-id="61418-102">Támogatja a [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.04] [ u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25 ] [ fed25], [Fedora 26][fed26], [architektúrája Linux][arch], és [macOS 10.12][mac].</span><span class="sxs-lookup"><span data-stu-id="61418-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.04][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25][fed25], [Fedora 26][fed26], [Arch Linux][arch], and [macOS 10.12][mac].</span></span>

<span data-ttu-id="61418-103">A Linux terjesztéseket, amelyek hivatalosan nem támogatottak, próbálkozhat a [PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="61418-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span> <span data-ttu-id="61418-104">Közvetlenül a Linux-használat PowerShell bináris fájljainak telepítéséhez is megpróbálhatja [ `tar.gz` archív][tar], de állítsa be a szükséges függőségek az operációs rendszer, a különálló lépések alapján kell.</span><span class="sxs-lookup"><span data-stu-id="61418-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="61418-105">Minden csomagok érhetők el a githubon [kiadott][] lap.</span><span class="sxs-lookup"><span data-stu-id="61418-105">All packages are available on our GitHub [releases][] page.</span></span> <span data-ttu-id="61418-106">A csomag telepítése után futtassa `pwsh` terminálról.</span><span class="sxs-lookup"><span data-stu-id="61418-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

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

## <a name="ubuntu-1404"></a><span data-ttu-id="61418-107">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="61418-107">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="61418-108">Telepítési csomag tárház - Ubuntu 14.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="61418-108">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="61418-109">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="61418-109">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span> <span data-ttu-id="61418-110">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="61418-110">This is the preferred method.</span></span>

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

<span data-ttu-id="61418-111">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="61418-111">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="61418-112">Közvetlen letöltése – Ubuntu 14.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="61418-112">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="61418-113">A Debian csomag `powershell_6.0.0-1.ubuntu.14.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="61418-113">Download the Debian package `powershell_6.0.0-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.14.04_amd64.deb
```

<span data-ttu-id="61418-114">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="61418-114">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="61418-115">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="61418-115">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="61418-116">Az Eltávolítás - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="61418-116">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="61418-117">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="61418-117">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="61418-118">Telepítési csomag tárház - Ubuntu 16.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="61418-118">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="61418-119">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="61418-119">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="61418-120">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="61418-120">This is the preferred method.</span></span>

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

<span data-ttu-id="61418-121">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="61418-121">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="61418-122">Közvetlen letöltése – Ubuntu 16.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="61418-122">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="61418-123">A Debian csomag `powershell_6.0.0-1.ubuntu.16.04_amd64.deb` a a [kiadott][] az Ubuntu gép oldalon:</span><span class="sxs-lookup"><span data-stu-id="61418-123">Download the Debian package `powershell_6.0.0-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.16.04_amd64.deb
```

<span data-ttu-id="61418-124">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="61418-124">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="61418-125">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="61418-125">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="61418-126">Az Eltávolítás - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="61418-126">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1704"></a><span data-ttu-id="61418-127">Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="61418-127">Ubuntu 17.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1704"></a><span data-ttu-id="61418-128">Telepítési csomag tárház - Ubuntu 17.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="61418-128">Installation via Package Repository - Ubuntu 17.04</span></span>

<span data-ttu-id="61418-129">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="61418-129">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="61418-130">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="61418-130">This is the preferred method.</span></span>

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

<span data-ttu-id="61418-131">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="61418-131">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1704"></a><span data-ttu-id="61418-132">Közvetlen letöltése – Ubuntu 17.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="61418-132">Installation via Direct Download - Ubuntu 17.04</span></span>

<span data-ttu-id="61418-133">A Debian csomag `powershell_6.0.0-1.ubuntu.17.04_amd64.deb` a a [kiadott][] az Ubuntu gép oldalon:</span><span class="sxs-lookup"><span data-stu-id="61418-133">Download the Debian package `powershell_6.0.0-1.ubuntu.17.04_amd64.deb` from the [releases][] page onto the Ubuntu machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.17.04_amd64.deb
```

<span data-ttu-id="61418-134">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="61418-134">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.ubuntu.17.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="61418-135">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="61418-135">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1704"></a><span data-ttu-id="61418-136">Az Eltávolítás - Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="61418-136">Uninstallation - Ubuntu 17.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="61418-137">Debian 8</span><span class="sxs-lookup"><span data-stu-id="61418-137">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="61418-138">Telepítési csomag tárház - Debian 8 keresztül</span><span class="sxs-lookup"><span data-stu-id="61418-138">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="61418-139">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="61418-139">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="61418-140">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="61418-140">This is the preferred method.</span></span>

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

<span data-ttu-id="61418-141">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="61418-141">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="61418-142">Keresztül közvetlen letöltése – Debian 8 telepítése</span><span class="sxs-lookup"><span data-stu-id="61418-142">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="61418-143">A Debian csomag `powershell_6.0.0-1.debian.8_amd64.deb` a a [kiadott][] a Debian gép oldalon:</span><span class="sxs-lookup"><span data-stu-id="61418-143">Download the Debian package `powershell_6.0.0-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.8_amd64.deb
```

<span data-ttu-id="61418-144">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="61418-144">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.debian.8_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="61418-145">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="61418-145">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="61418-146">Az Eltávolítás - Debian 8</span><span class="sxs-lookup"><span data-stu-id="61418-146">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="61418-147">Debian 9</span><span class="sxs-lookup"><span data-stu-id="61418-147">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="61418-148">Telepítési csomag tárház – Debian 9 keresztül</span><span class="sxs-lookup"><span data-stu-id="61418-148">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="61418-149">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="61418-149">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="61418-150">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="61418-150">This is the preferred method.</span></span>

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

<span data-ttu-id="61418-151">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="61418-151">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="61418-152">Közvetlen letöltése – Debian 9 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="61418-152">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="61418-153">A Debian csomag `powershell_6.0.0-1.debian.9_amd64.deb` a a [kiadott][] a Debian gép oldalon:</span><span class="sxs-lookup"><span data-stu-id="61418-153">Download the Debian package `powershell_6.0.0-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.9_amd64.deb
```

<span data-ttu-id="61418-154">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="61418-154">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.0-1.debian.9_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="61418-155">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="61418-155">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-9"></a><span data-ttu-id="61418-156">Az Eltávolítás - Debian 9</span><span class="sxs-lookup"><span data-stu-id="61418-156">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="61418-157">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="61418-157">CentOS 7</span></span>

> <span data-ttu-id="61418-158">Ez a csomag is működik-e az Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="61418-158">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="61418-159">Telepítési csomag tárház (ajánlott) – CentOS 7 keresztül</span><span class="sxs-lookup"><span data-stu-id="61418-159">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="61418-160">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="61418-160">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="61418-161">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="61418-161">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="61418-162">Közvetlen letöltése – CentOS 7 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="61418-162">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="61418-163">Használatával [CentOS 7][], a RPM csomag `powershell-6.0.0-1.rhel.7.x86_64.rpm` a a [kiadott][] a CentOS gép oldalon:</span><span class="sxs-lookup"><span data-stu-id="61418-163">Using [CentOS 7][], download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="61418-164">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="61418-164">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="61418-165">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="61418-165">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="61418-166">Az Eltávolítás - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="61418-166">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="61418-168">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="61418-168">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="61418-169">Telepítési csomag tárház (ajánlott) - Red Hat Enterprise Linux (RHEL) 7 keresztül</span><span class="sxs-lookup"><span data-stu-id="61418-169">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="61418-170">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="61418-170">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="61418-171">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="61418-171">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="61418-172">Közvetlen letöltése – Red Hat Enterprise Linux (RHEL) 7 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="61418-172">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="61418-173">A RPM csomag `powershell-6.0.0-1.rhel.7.x86_64.rpm` a a [kiadott][] a Red Hat Enterprise Linux-gép oldalon:</span><span class="sxs-lookup"><span data-stu-id="61418-173">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.debian.9_amd64.deb
```

<span data-ttu-id="61418-174">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="61418-174">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="61418-175">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="61418-175">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="61418-176">Az Eltávolítás - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="61418-176">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a><span data-ttu-id="61418-177">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="61418-177">OpenSUSE 42.2</span></span>

> <span data-ttu-id="61418-178">**Megjegyzés:** PowerShell Core telepítése esetén a OpenSUSE jelenthet, semmi nem biztosít `libcurl`.</span><span class="sxs-lookup"><span data-stu-id="61418-178">**Note:** When installing PowerShell Core, OpenSUSE may report that nothing provides `libcurl`.</span></span>
<span data-ttu-id="61418-179">`libcurl`már telepíthető OpenSUSE támogatott verzióit.</span><span class="sxs-lookup"><span data-stu-id="61418-179">`libcurl` should already be installed on supported versions of OpenSUSE.</span></span>
<span data-ttu-id="61418-180">Futtatás `zypper search libcurl` megerősítéséhez.</span><span class="sxs-lookup"><span data-stu-id="61418-180">Run `zypper search libcurl` to confirm.</span></span>
<span data-ttu-id="61418-181">A hiba 2 'megoldások"jelent.</span><span class="sxs-lookup"><span data-stu-id="61418-181">The error will present 2 'solutions'.</span></span> <span data-ttu-id="61418-182">Válassza ki a "Megoldás 2" PowerShell Core telepítésének folytatásához.</span><span class="sxs-lookup"><span data-stu-id="61418-182">Choose 'Solution 2' to continue installing PowerShell Core.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-422"></a><span data-ttu-id="61418-183">Telepítési csomag tárház (ajánlott) - OpenSUSE 42.2 keresztül</span><span class="sxs-lookup"><span data-stu-id="61418-183">Installation via Package Repository (preferred) - OpenSUSE 42.2</span></span>

<span data-ttu-id="61418-184">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="61418-184">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---opensuse-422"></a><span data-ttu-id="61418-185">Közvetlen letöltése – OpenSUSE 42.2 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="61418-185">Installation via Direct Download - OpenSUSE 42.2</span></span>

<span data-ttu-id="61418-186">A RPM csomag `powershell-6.0.0-1.rhel.7.x86_64.rpm` a a [kiadott][] a OpenSUSE gép oldalon:</span><span class="sxs-lookup"><span data-stu-id="61418-186">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="61418-187">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="61418-187">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a><span data-ttu-id="61418-188">Az Eltávolítás - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="61418-188">Uninstallation - OpenSUSE 42.2</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora-25"></a><span data-ttu-id="61418-189">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="61418-189">Fedora 25</span></span>

### <a name="installation-via-package-repository-preferred---fedora-25"></a><span data-ttu-id="61418-190">Telepítési csomag tárház (ajánlott) - Fedora 25 keresztül</span><span class="sxs-lookup"><span data-stu-id="61418-190">Installation via Package Repository (preferred) - Fedora 25</span></span>

<span data-ttu-id="61418-191">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="61418-191">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-25"></a><span data-ttu-id="61418-192">Közvetlen letöltése – Fedora 25 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="61418-192">Installation via Direct Download - Fedora 25</span></span>

<span data-ttu-id="61418-193">A RPM csomag `powershell-6.0.0-1.rhel.7.x86_64.rpm` a a [kiadott][] a Fedora gép oldalon:</span><span class="sxs-lookup"><span data-stu-id="61418-193">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="61418-194">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="61418-194">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="61418-195">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="61418-195">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-25"></a><span data-ttu-id="61418-196">Az Eltávolítás - Fedora 25</span><span class="sxs-lookup"><span data-stu-id="61418-196">Uninstallation - Fedora 25</span></span>

```sh
sudo dnf remove powershell
```

## <a name="fedora-26"></a><span data-ttu-id="61418-197">Fedora 26</span><span class="sxs-lookup"><span data-stu-id="61418-197">Fedora 26</span></span>

### <a name="installation-via-package-repository-preferred---fedora-26"></a><span data-ttu-id="61418-198">Telepítési csomag tárház (ajánlott) - Fedora 26 keresztül</span><span class="sxs-lookup"><span data-stu-id="61418-198">Installation via Package Repository (preferred) - Fedora 26</span></span>

<span data-ttu-id="61418-199">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="61418-199">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-26"></a><span data-ttu-id="61418-200">Közvetlen letöltése – Fedora 26 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="61418-200">Installation via Direct Download - Fedora 26</span></span>

<span data-ttu-id="61418-201">A RPM csomag `powershell-6.0.0-1.rhel.7.x86_64.rpm` a a [kiadott][] a Fedora gép oldalon:</span><span class="sxs-lookup"><span data-stu-id="61418-201">Download the RPM package `powershell-6.0.0-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine:</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="61418-202">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="61418-202">Then execute the following in the terminal:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="61418-203">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="61418-203">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-26"></a><span data-ttu-id="61418-204">Az Eltávolítás - Fedora 26</span><span class="sxs-lookup"><span data-stu-id="61418-204">Uninstallation - Fedora 26</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="61418-205">Linux architektúrája</span><span class="sxs-lookup"><span data-stu-id="61418-205">Arch Linux</span></span>

<span data-ttu-id="61418-206">PowerShell érhető el a [architektúrája Linux][] felhasználói tárház (AUR).</span><span class="sxs-lookup"><span data-stu-id="61418-206">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="61418-207">Az összeállítható a [legújabb címkézett kiadás][arch-release]</span><span class="sxs-lookup"><span data-stu-id="61418-207">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="61418-208">Az összeállítható a [fő legújabb véglegesítési][arch-git]</span><span class="sxs-lookup"><span data-stu-id="61418-208">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="61418-209">Használatával telepíthető a [bináris legújabb kiadás][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="61418-209">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="61418-210">A AUR csomagok karbantartása közösségi – nincs hivatalos támogatás.</span><span class="sxs-lookup"><span data-stu-id="61418-210">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="61418-211">A csomagok telepítése a AUR a további információkért lásd: a [architektúrája Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a közösségi [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="61418-211">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[architektúrája Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="61418-213">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="61418-213">Linux AppImage</span></span>

<span data-ttu-id="61418-214">A legutóbbi Linux-eloszlás használatával töltse le a AppImage `powershell-6.0.0-x86_64.AppImage` a a [kiadott][] a Linux-gépek oldalon.</span><span class="sxs-lookup"><span data-stu-id="61418-214">Using a recent Linux distribution, download the AppImage `powershell-6.0.0-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="61418-215">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="61418-215">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.0-x86_64.AppImage
./powershell-6.0.0-x86_64.AppImage
```

<span data-ttu-id="61418-216">A [AppImage][] lehetővé teszi, hogy a telepítés nélküli PowerShell futtatásához.</span><span class="sxs-lookup"><span data-stu-id="61418-216">The [AppImage][] lets you run PowerShell without installing it.</span></span> <span data-ttu-id="61418-217">Egy hordozható alkalmazás, amely a PowerShell és a függőségek (beleértve a .NET Core rendszer függőségeket) bundles egy javul csomagba.</span><span class="sxs-lookup"><span data-stu-id="61418-217">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span> <span data-ttu-id="61418-218">Ez a csomag a felhasználó a Linux-disztribúció függetlenül működik, és egyetlen bináris értékké.</span><span class="sxs-lookup"><span data-stu-id="61418-218">This package works independently of the user's Linux distribution, and is a single binary.</span></span>

[appimage]: http://appimage.org/

## <a name="macos-1012"></a><span data-ttu-id="61418-220">macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="61418-220">macOS 10.12</span></span>

### <a name="installation-via-homebrew-preferred---macos-1012"></a><span data-ttu-id="61418-221">Telepítési Homebrew (ajánlott) - macOS 10.12 keresztül</span><span class="sxs-lookup"><span data-stu-id="61418-221">Installation via Homebrew (preferred) - macOS 10.12</span></span>

<span data-ttu-id="61418-222">[Homebrew] [ brew] a hiányzó Csomagkezelőt a macOS van.</span><span class="sxs-lookup"><span data-stu-id="61418-222">[Homebrew][brew] is the missing package manager for macOS.</span></span> <span data-ttu-id="61418-223">Ha a `brew` parancs nem található, telepítenie kell a következő Homebrew [a utasításaikat][brew].</span><span class="sxs-lookup"><span data-stu-id="61418-223">If the `brew` command is not found, you need to install Homebrew following [their instructions][brew].</span></span>

<span data-ttu-id="61418-224">Homebrew telepítése után is könnyen PowerShell telepítése.</span><span class="sxs-lookup"><span data-stu-id="61418-224">Once you've installed Homebrew, installing PowerShell is easy.</span></span> <span data-ttu-id="61418-225">Először telepítse [Homebrew-Cask][cask], így további csomagok telepítése:</span><span class="sxs-lookup"><span data-stu-id="61418-225">First, install [Homebrew-Cask][cask], so you can install more packages:</span></span>

```sh
brew tap caskroom/cask
```

<span data-ttu-id="61418-226">Most már PowerShell telepíthető:</span><span class="sxs-lookup"><span data-stu-id="61418-226">Now, you can install PowerShell:</span></span>

```sh
brew cask install powershell
```

<span data-ttu-id="61418-227">PowerShell új verzióinak kiadásakor egyszerűen Homebrew tartozó képletek frissítése, és PowerShell frissítése:</span><span class="sxs-lookup"><span data-stu-id="61418-227">When new versions of PowerShell are released, simply update Homebrew's formulae and upgrade PowerShell:</span></span>

```sh
brew update
brew cask reinstall powershell
```

> <span data-ttu-id="61418-228">Megjegyzés: miatt: [ezt a problémát Cask](https://github.com/caskroom/homebrew-cask/issues/29301), jelenleg van, hogy egy reinstall frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="61418-228">Note: because of [this issue in Cask](https://github.com/caskroom/homebrew-cask/issues/29301), you currently have to do a reinstall to upgrade.</span></span>

[brew]: http://brew.sh/
[cask]: https://caskroom.github.io/

### <a name="installation-via-direct-download---macos-1012"></a><span data-ttu-id="61418-229">Közvetlen letöltés - macOS 10.12 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="61418-229">Installation via Direct Download - macOS 10.12</span></span>

<span data-ttu-id="61418-230">MacOS 10.12 használ, töltse le a PKG csomagot `powershell-6.0.0-osx.10.12-x64.pkg` a a [kiadott][] lap települ a macOS gépre.</span><span class="sxs-lookup"><span data-stu-id="61418-230">Using macOS 10.12, download the PKG package `powershell-6.0.0-osx.10.12-x64.pkg` from the [releases][] page onto the macOS machine.</span></span>

<span data-ttu-id="61418-231">Kattintson duplán a fájlra, és kövesse az utasításokat, vagy telepítse azt a Terminálszolgáltatások:</span><span class="sxs-lookup"><span data-stu-id="61418-231">Either double-click the file and follow the prompts, or install it from the terminal:</span></span>

```sh
sudo installer -pkg powershell-6.0.0-osx.10.12-x64.pkg -target /
```

### <a name="uninstallation---macos-1012"></a><span data-ttu-id="61418-232">Az Eltávolítás - macOS 10.12</span><span class="sxs-lookup"><span data-stu-id="61418-232">Uninstallation - macOS 10.12</span></span>

<span data-ttu-id="61418-233">PowerShell Homebrew telepítette, ha az Eltávolítás könnyen:</span><span class="sxs-lookup"><span data-stu-id="61418-233">If you installed PowerShell with Homebrew, uninstallation is easy:</span></span>

```sh
brew cask uninstall powershell
```

<span data-ttu-id="61418-234">Ha telepítette a PowerShell segítségével közvetlen letöltési, PowerShell manuálisan kell eltávolítani:</span><span class="sxs-lookup"><span data-stu-id="61418-234">If you installed PowerShell via direct download, PowerShell must be removed manually:</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

<span data-ttu-id="61418-235">Távolítsa el a további PowerShell útvonalak (például a felhasználói profil elérési útja) tekintse meg a [elérési utak] [ paths] ebben a dokumentumban az alábbi szakaszt, és távolítsa el a kívánt az elérési utak `sudo rm`.</span><span class="sxs-lookup"><span data-stu-id="61418-235">To uninstall the additional PowerShell paths (such as the user profile path) please see the [paths][paths] section below in this document and remove the desired the paths with `sudo rm`.</span></span> <span data-ttu-id="61418-236">(Megjegyzés: Ez nem szükséges, ha telepítette a Homebrew.)</span><span class="sxs-lookup"><span data-stu-id="61418-236">(Note: this is not necessary if you installed with Homebrew.)</span></span>

[paths]:#paths

## <a name="kali"></a><span data-ttu-id="61418-237">Kali</span><span class="sxs-lookup"><span data-stu-id="61418-237">Kali</span></span>

### <a name="installation"></a><span data-ttu-id="61418-238">Telepítés</span><span class="sxs-lookup"><span data-stu-id="61418-238">Installation</span></span>

```sh
# Download & Install prerequisites
sudo apt-get install libunwind8 libicu55
wget http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb
sudo dpkg -i libssl1.0.0_1.0.1t-1+deb8u6_amd64.deb

# Download & Install PowerShell
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell_6.0.0-1.ubuntu.16.04_amd64.deb
sudo dpkg -i powershell_6.0.0-1.ubuntu.16.04_amd64.deb

# Start PowerShell
pwsh
```

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="61418-239">Futtassa a PowerShell legújabb Kali (Kali GNU/Linux folyamatos) a telepítés nélküli</span><span class="sxs-lookup"><span data-stu-id="61418-239">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.0-x86_64.AppImage

# Start PowerShell
./powershell-6.0.0-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="61418-240">Az Eltávolítás - Kali</span><span class="sxs-lookup"><span data-stu-id="61418-240">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell-6.0.0-x86_64.AppImage
```

## <a name="raspbian"></a><span data-ttu-id="61418-241">Raspbian</span><span class="sxs-lookup"><span data-stu-id="61418-241">Raspbian</span></span>

<span data-ttu-id="61418-242">PowerShell jelenleg csak Raspbian Stretch támogatott.</span><span class="sxs-lookup"><span data-stu-id="61418-242">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

### <a name="installation"></a><span data-ttu-id="61418-243">Telepítés</span><span class="sxs-lookup"><span data-stu-id="61418-243">Installation</span></span>

```sh
# Install prerequisites
sudo apt-get install libunwind8

# Grab the latest tar.gz
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-linux-arm32.tar.gz

# Make folder to put powershell
mkdir ~/powershell

# Unpack the tar.gz file
tar -xvf ./powershell-6.0.0-linux-arm32.tar.gz -C ~/powershell

# Start PowerShell
~/powershell/pwsh
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="61418-244">Az Eltávolítás - Raspbian</span><span class="sxs-lookup"><span data-stu-id="61418-244">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="61418-245">Bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="61418-245">Binary Archives</span></span>

<span data-ttu-id="61418-246">PowerShell bináris `tar.gz` archívumokat előírt macOS és Linux platformokat, a központi telepítési forgatókönyvek engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="61418-246">PowerShell binary `tar.gz` archives are provided for macOS and Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="61418-247">Függőségek</span><span class="sxs-lookup"><span data-stu-id="61418-247">Dependencies</span></span>

<span data-ttu-id="61418-248">Linux PowerShell alkot az összes Linux terjesztésekről hordozható bináris fájljait.</span><span class="sxs-lookup"><span data-stu-id="61418-248">For Linux, PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="61418-249">De a .NET Core runtime szükséges a különböző terjesztések átviteli különböző függőségek, és ezért PowerShell szerepe ugyanaz.</span><span class="sxs-lookup"><span data-stu-id="61418-249">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="61418-250">Az alábbi ábra mutatja a .NET Core 2.0 függőségek különböző Linux terjesztések átviteli hivatalosan támogatott.</span><span class="sxs-lookup"><span data-stu-id="61418-250">The following chart shows the .NET Core 2.0 dependencies on different Linux distributions that are officially supported.</span></span>

| <span data-ttu-id="61418-251">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="61418-251">OS</span></span>                 | <span data-ttu-id="61418-252">Függőségek</span><span class="sxs-lookup"><span data-stu-id="61418-252">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="61418-253">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="61418-253">Ubuntu 14.04</span></span>       | <span data-ttu-id="61418-254">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="61418-254">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="61418-255">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="61418-255">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="61418-256">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="61418-256">Ubuntu 16.04</span></span>       | <span data-ttu-id="61418-257">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="61418-257">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="61418-258">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="61418-258">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="61418-259">Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="61418-259">Ubuntu 17.04</span></span>       | <span data-ttu-id="61418-260">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="61418-260">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="61418-261">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="61418-261">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="61418-262">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="61418-262">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="61418-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="61418-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="61418-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="61418-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="61418-265">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="61418-265">Debian 9 (Stretch)</span></span> | <span data-ttu-id="61418-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="61418-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="61418-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="61418-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="61418-268">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="61418-268">CentOS 7</span></span> <br> <span data-ttu-id="61418-269">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="61418-269">Oracle Linux 7</span></span> <br> <span data-ttu-id="61418-270">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="61418-270">RHEL 7</span></span> <br> <span data-ttu-id="61418-271">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="61418-271">OpenSUSE 42.2</span></span> <br> <span data-ttu-id="61418-272">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="61418-272">Fedora 25</span></span> | <span data-ttu-id="61418-273">libunwind, libcurl, openssl-függvénytárak, libicu</span><span class="sxs-lookup"><span data-stu-id="61418-273">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="61418-274">Fedora 26</span><span class="sxs-lookup"><span data-stu-id="61418-274">Fedora 26</span></span>          | <span data-ttu-id="61418-275">libunwind, libcurl, openssl-függvénytárak, libicu, / compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="61418-275">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="61418-276">PowerShell bináris fájljait, a Linux terjesztéseket hivatalosan nem támogatott központi telepítéséhez, akkor kellene telepíteni a szükséges függőségek a cél operációs rendszer a különálló lépések.</span><span class="sxs-lookup"><span data-stu-id="61418-276">In order to deploy PowerShell binaries on Linux distributions that are not officially supported, you would need to install the necessary dependencies for the target OS in separate steps.</span></span> <span data-ttu-id="61418-277">Például a [Amazon Linux dockerfile] [ amazon-dockerfile] függőségek először telepíti, és kinyeri a Linux `tar.gz` archív.</span><span class="sxs-lookup"><span data-stu-id="61418-277">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="61418-278">Telepítés – bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="61418-278">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="61418-279">Linux</span><span class="sxs-lookup"><span data-stu-id="61418-279">Linux</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-linux-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /opt/microsoft/powershell/6.0.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /opt/microsoft/powershell/6.0.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /opt/microsoft/powershell/6.0.0/pwsh /usr/bin/pwsh
```

#### <a name="macos"></a><span data-ttu-id="61418-280">macOS</span><span class="sxs-lookup"><span data-stu-id="61418-280">macOS</span></span>

```sh
# Download the powershell '.tar.gz' archive
curl -L -o /tmp/powershell.tar.gz https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-osx-x64.tar.gz

# Create the target folder where powershell will be placed
sudo mkdir -p /usr/local/microsoft/powershell/6.0.0

# Expand powershell to the target folder
sudo tar zxf /tmp/powershell.tar.gz -C /usr/local/microsoft/powershell/6.0.0

# Set execute permissions
sudo chmod +x /usr/local/microsoft/powershell/6.0.0/pwsh

# Create the symbolic link that points to pwsh
sudo ln -s /usr/local/microsoft/powershell/6.0.0/pwsh /usr/local/bin/pwsh
```

### <a name="uninstallation---binary-archives"></a><span data-ttu-id="61418-281">Az Eltávolítás - bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="61418-281">Uninstallation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="61418-282">Linux</span><span class="sxs-lookup"><span data-stu-id="61418-282">Linux</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

#### <a name="macos"></a><span data-ttu-id="61418-283">macOS</span><span class="sxs-lookup"><span data-stu-id="61418-283">macOS</span></span>

```sh
sudo rm -rf /usr/local/bin/pwsh /usr/local/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="61418-284">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="61418-284">Paths</span></span>

* <span data-ttu-id="61418-285">`$PSHOME`van`/opt/microsoft/powershell/6.0.0/`</span><span class="sxs-lookup"><span data-stu-id="61418-285">`$PSHOME` is `/opt/microsoft/powershell/6.0.0/`</span></span>
* <span data-ttu-id="61418-286">Felhasználói profilok rendszer nem olvas be`~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="61418-286">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="61418-287">Alapértelmezett profilok rendszer nem olvas be`$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="61418-287">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="61418-288">Modulok felhasználói rendszer nem olvas be`~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="61418-288">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="61418-289">Megosztott modulok rendszer nem olvas be`/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="61418-289">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="61418-290">Az alapértelmezett modulokat rendszer nem olvas be`$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="61418-290">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="61418-291">A rögzítendő PSReadline előzmények`~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="61418-291">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="61418-292">A profilok tiszteletben PowerShell gazdagép konfiguráció, így az alapértelmezett gazdagép-specifikus profilok létezik az `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="61418-292">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="61418-293">A Linux és macOS a [XDG Base könyvtár megadása] [ xdg-bds] tiszteletben tartását.</span><span class="sxs-lookup"><span data-stu-id="61418-293">On Linux and macOS, the [XDG Base Directory Specification][xdg-bds] is respected.</span></span>

<span data-ttu-id="61418-294">Vegye figyelembe, hogy mivel macOS BSD, származtatott helyett `/opt`, a használt előtag `/usr/local`.</span><span class="sxs-lookup"><span data-stu-id="61418-294">Note that because macOS is a derivation of BSD, instead of `/opt`, the prefix used is `/usr/local`.</span></span> <span data-ttu-id="61418-295">Ebből kifolyólag `$PSHOME` van `/usr/local/microsoft/powershell/6.0.0/`, és a symlink van elhelyezve `/usr/local/bin/pwsh`.</span><span class="sxs-lookup"><span data-stu-id="61418-295">Thus, `$PSHOME` is `/usr/local/microsoft/powershell/6.0.0/`, and the symlink is placed at `/usr/local/bin/pwsh`.</span></span>

[kiadott]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
