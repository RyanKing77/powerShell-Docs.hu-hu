# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="6501a-101">PowerShell központi telepítése Linux rendszeren</span><span class="sxs-lookup"><span data-stu-id="6501a-101">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="6501a-102">Támogatja a [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.04] [ u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25 ] [ fed25], [Fedora 26][fed26], és [architektúrája Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="6501a-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.04][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 25][fed25], [Fedora 26][fed26], and [Arch Linux][arch].</span></span>

<span data-ttu-id="6501a-103">A Linux terjesztéseket, amelyek hivatalosan nem támogatottak, próbálkozhat a [PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="6501a-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span>
<span data-ttu-id="6501a-104">Közvetlenül a Linux-használat PowerShell bináris fájljainak telepítéséhez is megpróbálhatja [ `tar.gz` archív][tar], de állítsa be a szükséges függőségek az operációs rendszer, a különálló lépések alapján kell.</span><span class="sxs-lookup"><span data-stu-id="6501a-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="6501a-105">Minden csomagok érhetők el a githubon [kiadott][] lap.</span><span class="sxs-lookup"><span data-stu-id="6501a-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="6501a-106">A csomag telepítése után futtassa `pwsh` terminálról.</span><span class="sxs-lookup"><span data-stu-id="6501a-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

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
[tar]: #binary-archives

## <a name="ubuntu-1404"></a><span data-ttu-id="6501a-107">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6501a-107">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="6501a-108">Telepítési csomag tárház - Ubuntu 14.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="6501a-108">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="6501a-109">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="6501a-109">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="6501a-110">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="6501a-110">This is the preferred method.</span></span>

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

<span data-ttu-id="6501a-111">Felügyelő, mint a Microsoft-tárház regisztrálni.</span><span class="sxs-lookup"><span data-stu-id="6501a-111">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="6501a-112">Ettől kezdve csak kell használnia `sudo apt-get upgrade powershell` a telepítés frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="6501a-112">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="6501a-113">Közvetlen letöltése – Ubuntu 14.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="6501a-113">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="6501a-114">A Debian csomag `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="6501a-114">Download the Debian package `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="6501a-115">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="6501a-115">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="6501a-116">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="6501a-116">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="6501a-117">Az Eltávolítás - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6501a-117">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="6501a-118">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6501a-118">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="6501a-119">Telepítési csomag tárház - Ubuntu 16.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="6501a-119">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="6501a-120">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="6501a-120">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="6501a-121">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="6501a-121">This is the preferred method.</span></span>

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

<span data-ttu-id="6501a-122">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="6501a-122">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="6501a-123">Közvetlen letöltése – Ubuntu 16.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="6501a-123">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="6501a-124">A Debian csomag `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="6501a-124">Download the Debian package `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="6501a-125">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="6501a-125">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="6501a-126">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="6501a-126">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="6501a-127">Az Eltávolítás - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6501a-127">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1704"></a><span data-ttu-id="6501a-128">Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="6501a-128">Ubuntu 17.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1704"></a><span data-ttu-id="6501a-129">Telepítési csomag tárház - Ubuntu 17.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="6501a-129">Installation via Package Repository - Ubuntu 17.04</span></span>

<span data-ttu-id="6501a-130">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="6501a-130">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="6501a-131">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="6501a-131">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/17.04/prod.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="6501a-132">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="6501a-132">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1704"></a><span data-ttu-id="6501a-133">Közvetlen letöltése – Ubuntu 17.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="6501a-133">Installation via Direct Download - Ubuntu 17.04</span></span>

<span data-ttu-id="6501a-134">A Debian csomag `powershell_6.0.2-1.ubuntu.17.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="6501a-134">Download the Debian package `powershell_6.0.2-1.ubuntu.17.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="6501a-135">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="6501a-135">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.17.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="6501a-136">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="6501a-136">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1704"></a><span data-ttu-id="6501a-137">Az Eltávolítás - Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="6501a-137">Uninstallation - Ubuntu 17.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="6501a-138">Debian 8</span><span class="sxs-lookup"><span data-stu-id="6501a-138">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="6501a-139">Telepítési csomag tárház - Debian 8 keresztül</span><span class="sxs-lookup"><span data-stu-id="6501a-139">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="6501a-140">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="6501a-140">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="6501a-141">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="6501a-141">This is the preferred method.</span></span>

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

<span data-ttu-id="6501a-142">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="6501a-142">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="6501a-143">Keresztül közvetlen letöltése – Debian 8 telepítése</span><span class="sxs-lookup"><span data-stu-id="6501a-143">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="6501a-144">A Debian csomag `powershell_6.0.2-1.debian.8_amd64.deb` a a [kiadott][] a Debian gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="6501a-144">Download the Debian package `powershell_6.0.2-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="6501a-145">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="6501a-145">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="6501a-146">Ne feledje, hogy `dpkg -i` unmet függőségekkel rendelkező sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="6501a-146">Please note that `dpkg -i` will fail with unmet dependencies.</span></span>
> <span data-ttu-id="6501a-147">A következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="6501a-147">The next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="6501a-148">Az Eltávolítás - Debian 8</span><span class="sxs-lookup"><span data-stu-id="6501a-148">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="6501a-149">Debian 9</span><span class="sxs-lookup"><span data-stu-id="6501a-149">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="6501a-150">Telepítési csomag tárház – Debian 9 keresztül</span><span class="sxs-lookup"><span data-stu-id="6501a-150">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="6501a-151">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="6501a-151">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="6501a-152">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="6501a-152">This is the preferred method.</span></span>

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

<span data-ttu-id="6501a-153">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="6501a-153">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="6501a-154">Közvetlen letöltése – Debian 9 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="6501a-154">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="6501a-155">A Debian csomag `powershell_6.0.2-1.debian.9_amd64.deb` a a [kiadott][] a Debian gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="6501a-155">Download the Debian package `powershell_6.0.2-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="6501a-156">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="6501a-156">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="6501a-157">Ne feledje, hogy `dpkg -i` unmet függőségekkel rendelkező sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="6501a-157">Please note that `dpkg -i` will fail with unmet dependencies.</span></span>
> <span data-ttu-id="6501a-158">A következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="6501a-158">The next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-9"></a><span data-ttu-id="6501a-159">Az Eltávolítás - Debian 9</span><span class="sxs-lookup"><span data-stu-id="6501a-159">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="6501a-160">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6501a-160">CentOS 7</span></span>

> <span data-ttu-id="6501a-161">Ez a csomag is működik-e az Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="6501a-161">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="6501a-162">Telepítési csomag tárház (ajánlott) – CentOS 7 keresztül</span><span class="sxs-lookup"><span data-stu-id="6501a-162">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="6501a-163">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="6501a-163">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="6501a-164">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="6501a-164">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="6501a-165">Közvetlen letöltése – CentOS 7 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="6501a-165">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="6501a-166">Használatával [CentOS 7][], a RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a CentOS gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="6501a-166">Using [CentOS 7][], download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="6501a-167">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="6501a-167">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6501a-168">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="6501a-168">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="6501a-169">Az Eltávolítás - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6501a-169">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6501a-171">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="6501a-171">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6501a-172">Telepítési csomag tárház (ajánlott) - Red Hat Enterprise Linux (RHEL) 7 keresztül</span><span class="sxs-lookup"><span data-stu-id="6501a-172">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="6501a-173">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="6501a-173">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="6501a-174">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="6501a-174">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6501a-175">Közvetlen letöltése – Red Hat Enterprise Linux (RHEL) 7 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="6501a-175">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="6501a-176">A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a Red Hat Enterprise Linux-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="6501a-176">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="6501a-177">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="6501a-177">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6501a-178">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="6501a-178">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="6501a-179">Az Eltávolítás - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="6501a-179">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a><span data-ttu-id="6501a-180">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="6501a-180">OpenSUSE 42.2</span></span>

> [!NOTE]
> <span data-ttu-id="6501a-181">PowerShell központ telepítésekor `zypper` előfordulhat, hogy a következő hiba jelentését:</span><span class="sxs-lookup"><span data-stu-id="6501a-181">When installing PowerShell Core, `zypper` may report the following error:</span></span>
>
> ```Output
> Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
>  Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
>  Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
> ```
>
> <span data-ttu-id="6501a-182">Ebben az esetben ellenőrizze, hogy a kompatibilis `libcurl` könyvtár megtalálható úgy, hogy a következő parancsot a jeleníti meg a `libcurl4` csomag telepítve:</span><span class="sxs-lookup"><span data-stu-id="6501a-182">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>
>
> ```sh
> zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
> ```
>
> <span data-ttu-id="6501a-183">Válassza ki a `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` megoldás a PowerShell csomag telepítésekor.</span><span class="sxs-lookup"><span data-stu-id="6501a-183">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the PowerShell package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-422"></a><span data-ttu-id="6501a-184">Telepítési csomag tárház (ajánlott) - OpenSUSE 42.2 keresztül</span><span class="sxs-lookup"><span data-stu-id="6501a-184">Installation via Package Repository (preferred) - OpenSUSE 42.2</span></span>

<span data-ttu-id="6501a-185">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="6501a-185">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---opensuse-422"></a><span data-ttu-id="6501a-186">Közvetlen letöltése – OpenSUSE 42.2 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="6501a-186">Installation via Direct Download - OpenSUSE 42.2</span></span>

<span data-ttu-id="6501a-187">A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a OpenSUSE gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="6501a-187">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6501a-188">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="6501a-188">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a><span data-ttu-id="6501a-189">Az Eltávolítás - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="6501a-189">Uninstallation - OpenSUSE 42.2</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora-25"></a><span data-ttu-id="6501a-190">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="6501a-190">Fedora 25</span></span>

### <a name="installation-via-package-repository-preferred---fedora-25"></a><span data-ttu-id="6501a-191">Telepítési csomag tárház (ajánlott) - Fedora 25 keresztül</span><span class="sxs-lookup"><span data-stu-id="6501a-191">Installation via Package Repository (preferred) - Fedora 25</span></span>

<span data-ttu-id="6501a-192">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="6501a-192">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-25"></a><span data-ttu-id="6501a-193">Közvetlen letöltése – Fedora 25 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="6501a-193">Installation via Direct Download - Fedora 25</span></span>

<span data-ttu-id="6501a-194">A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a Fedora gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="6501a-194">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

```sh
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.0/powershell-6.0.0-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6501a-195">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="6501a-195">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6501a-196">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="6501a-196">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-25"></a><span data-ttu-id="6501a-197">Az Eltávolítás - Fedora 25</span><span class="sxs-lookup"><span data-stu-id="6501a-197">Uninstallation - Fedora 25</span></span>

```sh
sudo dnf remove powershell
```

## <a name="fedora-26"></a><span data-ttu-id="6501a-198">Fedora 26</span><span class="sxs-lookup"><span data-stu-id="6501a-198">Fedora 26</span></span>

### <a name="installation-via-package-repository-preferred---fedora-26"></a><span data-ttu-id="6501a-199">Telepítési csomag tárház (ajánlott) - Fedora 26 keresztül</span><span class="sxs-lookup"><span data-stu-id="6501a-199">Installation via Package Repository (preferred) - Fedora 26</span></span>

<span data-ttu-id="6501a-200">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="6501a-200">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-26"></a><span data-ttu-id="6501a-201">Közvetlen letöltése – Fedora 26 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="6501a-201">Installation via Direct Download - Fedora 26</span></span>

<span data-ttu-id="6501a-202">A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a Fedora gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="6501a-202">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="6501a-203">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="6501a-203">Then execute the following in the terminal:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="6501a-204">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="6501a-204">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf update
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-26"></a><span data-ttu-id="6501a-205">Az Eltávolítás - Fedora 26</span><span class="sxs-lookup"><span data-stu-id="6501a-205">Uninstallation - Fedora 26</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="6501a-206">Linux architektúrája</span><span class="sxs-lookup"><span data-stu-id="6501a-206">Arch Linux</span></span>

<span data-ttu-id="6501a-207">PowerShell érhető el a [architektúrája Linux][] felhasználói tárház (AUR).</span><span class="sxs-lookup"><span data-stu-id="6501a-207">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="6501a-208">Az összeállítható a [legújabb címkézett kiadás][arch-release]</span><span class="sxs-lookup"><span data-stu-id="6501a-208">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="6501a-209">Az összeállítható a [fő legújabb véglegesítési][arch-git]</span><span class="sxs-lookup"><span data-stu-id="6501a-209">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="6501a-210">Használatával telepíthető a [bináris legújabb kiadás][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="6501a-210">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="6501a-211">A AUR csomagok karbantartása közösségi – nincs hivatalos támogatás.</span><span class="sxs-lookup"><span data-stu-id="6501a-211">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="6501a-212">A csomagok telepítése a AUR a további információkért lásd: a [architektúrája Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a közösségi [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="6501a-212">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[architektúrája Linux]: https://www.archlinux.org/download/
[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="6501a-214">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="6501a-214">Linux AppImage</span></span>

<span data-ttu-id="6501a-215">A legutóbbi Linux-eloszlás használatával töltse le a AppImage `powershell-6.0.1-x86_64.AppImage` a a [kiadott][] a Linux-gépek oldalon.</span><span class="sxs-lookup"><span data-stu-id="6501a-215">Using a recent Linux distribution, download the AppImage `powershell-6.0.1-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="6501a-216">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="6501a-216">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

<span data-ttu-id="6501a-217">A [AppImage][] lehetővé teszi, hogy a telepítés nélküli PowerShell futtatásához.</span><span class="sxs-lookup"><span data-stu-id="6501a-217">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="6501a-218">Egy hordozható alkalmazás, amely a PowerShell és a függőségek (beleértve a .NET Core rendszer függőségeket) bundles egy javul csomagba.</span><span class="sxs-lookup"><span data-stu-id="6501a-218">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="6501a-219">Ez a csomag, amely a felhasználó a Linux-disztribúció függetlenül működik egy bináris.</span><span class="sxs-lookup"><span data-stu-id="6501a-219">This package  is a single binary that works independently of the user's Linux distribution.</span></span>

[appimage]: http://appimage.org/

## <a name="kali"></a><span data-ttu-id="6501a-221">Kali</span><span class="sxs-lookup"><span data-stu-id="6501a-221">Kali</span></span>

### <a name="installation"></a><span data-ttu-id="6501a-222">Telepítés</span><span class="sxs-lookup"><span data-stu-id="6501a-222">Installation</span></span>

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

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="6501a-223">Futtassa a PowerShell legújabb Kali (Kali GNU/Linux folyamatos) a telepítés nélküli</span><span class="sxs-lookup"><span data-stu-id="6501a-223">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="6501a-224">Az Eltávolítás - Kali</span><span class="sxs-lookup"><span data-stu-id="6501a-224">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="6501a-225">Raspbian</span><span class="sxs-lookup"><span data-stu-id="6501a-225">Raspbian</span></span>

<span data-ttu-id="6501a-226">PowerShell jelenleg csak Raspbian Stretch támogatott.</span><span class="sxs-lookup"><span data-stu-id="6501a-226">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="6501a-227">Is CoreCLR (és így PowerShell Core) csak Pi 2 és Pi 3 eszközökön módon fog más eszközök, például [Pi nulla](https://github.com/dotnet/coreclr/issues/10605), egy nem támogatott processzorral rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="6501a-227">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="6501a-228">Töltse le [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) , és kövesse a [telepítési utasításokat](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) a Pi eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="6501a-228">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation"></a><span data-ttu-id="6501a-229">Telepítés</span><span class="sxs-lookup"><span data-stu-id="6501a-229">Installation</span></span>

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

<span data-ttu-id="6501a-230">Nem kötelező elérési út megadását a "pwsh" bináris nélkül indítsa el a Powershellt szeretné szimbolikus hivatkozást hozhat létre</span><span class="sxs-lookup"><span data-stu-id="6501a-230">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="6501a-231">Az Eltávolítás - Raspbian</span><span class="sxs-lookup"><span data-stu-id="6501a-231">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="6501a-232">Bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="6501a-232">Binary Archives</span></span>

<span data-ttu-id="6501a-233">PowerShell bináris `tar.gz` archívumokat biztosított Linux-platformokhoz lehetővé központi telepítési forgatókönyveket.</span><span class="sxs-lookup"><span data-stu-id="6501a-233">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="6501a-234">Függőségek</span><span class="sxs-lookup"><span data-stu-id="6501a-234">Dependencies</span></span>

<span data-ttu-id="6501a-235">PowerShell alkot az összes Linux terjesztésekről hordozható bináris fájljait.</span><span class="sxs-lookup"><span data-stu-id="6501a-235">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="6501a-236">De a .NET Core runtime szükséges a különböző terjesztések átviteli különböző függőségek, és ezért PowerShell szerepe ugyanaz.</span><span class="sxs-lookup"><span data-stu-id="6501a-236">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="6501a-237">Az alábbi ábra mutatja a .NET Core 2.0 függőségek hivatalosan által támogatott különböző Linux terjesztéseket.</span><span class="sxs-lookup"><span data-stu-id="6501a-237">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="6501a-238">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="6501a-238">OS</span></span>                 | <span data-ttu-id="6501a-239">Függőségek</span><span class="sxs-lookup"><span data-stu-id="6501a-239">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="6501a-240">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="6501a-240">Ubuntu 14.04</span></span>       | <span data-ttu-id="6501a-241">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="6501a-241">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6501a-242">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="6501a-242">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="6501a-243">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="6501a-243">Ubuntu 16.04</span></span>       | <span data-ttu-id="6501a-244">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="6501a-244">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6501a-245">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="6501a-245">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="6501a-246">Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="6501a-246">Ubuntu 17.04</span></span>       | <span data-ttu-id="6501a-247">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="6501a-247">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6501a-248">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="6501a-248">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="6501a-249">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="6501a-249">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="6501a-250">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="6501a-250">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6501a-251">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="6501a-251">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="6501a-252">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="6501a-252">Debian 9 (Stretch)</span></span> | <span data-ttu-id="6501a-253">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="6501a-253">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="6501a-254">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="6501a-254">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="6501a-255">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6501a-255">CentOS 7</span></span> <br> <span data-ttu-id="6501a-256">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="6501a-256">Oracle Linux 7</span></span> <br> <span data-ttu-id="6501a-257">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="6501a-257">RHEL 7</span></span> <br> <span data-ttu-id="6501a-258">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="6501a-258">OpenSUSE 42.2</span></span> <br> <span data-ttu-id="6501a-259">Fedora 25</span><span class="sxs-lookup"><span data-stu-id="6501a-259">Fedora 25</span></span> | <span data-ttu-id="6501a-260">libunwind, libcurl, openssl-függvénytárak, libicu</span><span class="sxs-lookup"><span data-stu-id="6501a-260">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="6501a-261">Fedora 26</span><span class="sxs-lookup"><span data-stu-id="6501a-261">Fedora 26</span></span>          | <span data-ttu-id="6501a-262">libunwind, libcurl, openssl-függvénytárak, libicu, / compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="6501a-262">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="6501a-263">Az telepítéséhez PowerShell bináris fájljait, a Linux terjesztéseket, amelyek hivatalosan nem támogatottak, kell telepíteni a cél operációs rendszer szükséges függőségek külön lépéseket.</span><span class="sxs-lookup"><span data-stu-id="6501a-263">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="6501a-264">Például a [Amazon Linux dockerfile] [ amazon-dockerfile] függőségek először telepíti, és kinyeri a Linux `tar.gz` archív.</span><span class="sxs-lookup"><span data-stu-id="6501a-264">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="6501a-265">Telepítés – bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="6501a-265">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="6501a-266">Linux</span><span class="sxs-lookup"><span data-stu-id="6501a-266">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="6501a-267">Bináris archívumokat eltávolítása</span><span class="sxs-lookup"><span data-stu-id="6501a-267">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="6501a-268">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="6501a-268">Paths</span></span>

* <span data-ttu-id="6501a-269">`$PSHOME` van `/opt/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="6501a-269">`$PSHOME` is `/opt/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="6501a-270">Felhasználói profilok rendszer nem olvas be `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="6501a-270">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="6501a-271">Alapértelmezett profilok rendszer nem olvas be `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="6501a-271">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="6501a-272">Modulok felhasználói rendszer nem olvas be `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="6501a-272">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="6501a-273">Megosztott modulok rendszer nem olvas be `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="6501a-273">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="6501a-274">Az alapértelmezett modulokat rendszer nem olvas be `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="6501a-274">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="6501a-275">A rögzítendő PSReadline előzmények `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="6501a-275">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="6501a-276">A profilok tiszteletben PowerShell gazdagép konfiguráció, így az alapértelmezett gazdagép-specifikus profilok létezik az `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="6501a-276">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="6501a-277">PowerShell tiszteletben tartja a [XDG Base könyvtár megadása] [ xdg-bds] Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="6501a-277">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[kiadott]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
