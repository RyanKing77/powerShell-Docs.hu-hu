# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="57a22-101">A PowerShell Core telepítése Linux rendszerre</span><span class="sxs-lookup"><span data-stu-id="57a22-101">Installing PowerShell Core on Linux</span></span>

Supports <bpt id="p1">[</bpt>Ubuntu 14.04<ept id="p1">]</ept><bpt id="p2">[</bpt><ept id="p2">u14]</ept>, <bpt id="p3">[</bpt>Ubuntu 16.04<ept id="p3">]</ept><bpt id="p4">[</bpt><ept id="p4">u16]</ept>, <bpt id="p5">[</bpt>Ubuntu 17.04<ept id="p5">]</ept><bpt id="p6">[</bpt><ept id="p6">u17]</ept>, <bpt id="p7">[</bpt>Debian 8<ept id="p7">]</ept><bpt id="p8">[</bpt><ept id="p8">deb8]</ept>, <bpt id="p9">[</bpt>Debian 9<ept id="p9">]</ept><bpt id="p10">[</bpt><ept id="p10">deb9]</ept>, <bpt id="p11">[</bpt>CentOS 7<ept id="p11">]</ept><bpt id="p12">[</bpt><ept id="p12">cos]</ept>, <bpt id="p13">[</bpt>Red Hat Enterprise Linux (RHEL) 7<ept id="p13">]</ept><bpt id="p14">[</bpt><ept id="p14">rhel7]</ept>, <bpt id="p15">[</bpt>OpenSUSE 42.2<ept id="p15">]</ept><bpt id="p16">[</bpt><ept id="p16">opensuse]</ept>, <bpt id="p17">[</bpt>Fedora 27<ept id="p17">]</ept><bpt id="p18">[</bpt><ept id="p18">fedora]</ept>, <bpt id="p19">[</bpt>Fedora 28<ept id="p19">]</ept><bpt id="p20">[</bpt><ept id="p20">fedora]</ept>, and <bpt id="p21">[</bpt>Arch Linux<ept id="p21">]</ept><bpt id="p22">[</bpt><ept id="p22">arch]</ept>.

<span data-ttu-id="57a22-103">A Linux terjesztéseket, amelyek hivatalosan nem támogatottak, próbálkozhat a [PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="57a22-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span>
<span data-ttu-id="57a22-104">Közvetlenül a Linux-használat PowerShell bináris fájljainak telepítéséhez is megpróbálhatja [ `tar.gz` archív][tar], de állítsa be a szükséges függőségek az operációs rendszer, a különálló lépések alapján kell.</span><span class="sxs-lookup"><span data-stu-id="57a22-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="57a22-105">Minden csomagok érhetők el a githubon [Kiadások][] lap.</span><span class="sxs-lookup"><span data-stu-id="57a22-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="57a22-106">A csomag telepítése után futtassa `pwsh` terminálról.</span><span class="sxs-lookup"><span data-stu-id="57a22-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u17]: #ubuntu-1704
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-422
[fedora]: #fedora
[arch]: #arch-linux
[lai]: #linux-appimage
[tar]: #binary-archives

## <a name="ubuntu-1404"></a><span data-ttu-id="57a22-107">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="57a22-107">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="57a22-108">Telepítési csomag tárház - Ubuntu 14.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="57a22-108">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="57a22-109">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="57a22-109">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="57a22-110">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="57a22-110">This is the preferred method.</span></span>

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

<span data-ttu-id="57a22-111">Felügyelő, mint a Microsoft-tárház regisztrálni.</span><span class="sxs-lookup"><span data-stu-id="57a22-111">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="57a22-112">Ettől kezdve csak kell használnia `sudo apt-get upgrade powershell` a telepítés frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="57a22-112">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="57a22-113">Közvetlen letöltése – Ubuntu 14.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="57a22-113">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="57a22-114">A Debian csomag `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` a a [Kiadások][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="57a22-114">Download the Debian package `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="57a22-115">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="57a22-115">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="57a22-116">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="57a22-116">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="57a22-117">Az Eltávolítás - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="57a22-117">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="57a22-118">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="57a22-118">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="57a22-119">Telepítési csomag tárház - Ubuntu 16.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="57a22-119">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="57a22-120">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="57a22-120">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="57a22-121">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="57a22-121">This is the preferred method.</span></span>

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

<span data-ttu-id="57a22-122">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="57a22-122">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="57a22-123">Közvetlen letöltése – Ubuntu 16.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="57a22-123">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="57a22-124">A Debian csomag `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` a a [Kiadások][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="57a22-124">Download the Debian package `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="57a22-125">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="57a22-125">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="57a22-126">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="57a22-126">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="57a22-127">Az Eltávolítás - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="57a22-127">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1704"></a><span data-ttu-id="57a22-128">Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="57a22-128">Ubuntu 17.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1704"></a><span data-ttu-id="57a22-129">Telepítési csomag tárház - Ubuntu 17.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="57a22-129">Installation via Package Repository - Ubuntu 17.04</span></span>

<span data-ttu-id="57a22-130">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="57a22-130">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="57a22-131">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="57a22-131">This is the preferred method.</span></span>

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

<span data-ttu-id="57a22-132">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="57a22-132">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1704"></a><span data-ttu-id="57a22-133">Közvetlen letöltése – Ubuntu 17.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="57a22-133">Installation via Direct Download - Ubuntu 17.04</span></span>

<span data-ttu-id="57a22-134">A Debian csomag `powershell_6.0.2-1.ubuntu.17.04_amd64.deb` a a [Kiadások][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="57a22-134">Download the Debian package `powershell_6.0.2-1.ubuntu.17.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="57a22-135">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="57a22-135">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.17.04_amd64.deb
sudo apt-get install -f
```

> <span data-ttu-id="57a22-136">Ne feledje, hogy `dpkg -i` sikertelen lesz, és unmet függőségek; a következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="57a22-136">Please note that `dpkg -i` will fail with unmet dependencies; the next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1704"></a><span data-ttu-id="57a22-137">Az Eltávolítás - Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="57a22-137">Uninstallation - Ubuntu 17.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="57a22-138">Debian 8</span><span class="sxs-lookup"><span data-stu-id="57a22-138">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="57a22-139">Telepítési csomag tárház - Debian 8 keresztül</span><span class="sxs-lookup"><span data-stu-id="57a22-139">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="57a22-140">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="57a22-140">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="57a22-141">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="57a22-141">This is the preferred method.</span></span>

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

<span data-ttu-id="57a22-142">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="57a22-142">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="57a22-143">Keresztül közvetlen letöltése – Debian 8 telepítése</span><span class="sxs-lookup"><span data-stu-id="57a22-143">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="57a22-144">A Debian csomag `powershell_6.0.2-1.debian.8_amd64.deb` a a [Kiadások][] a Debian gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="57a22-144">Download the Debian package `powershell_6.0.2-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="57a22-145">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="57a22-145">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="57a22-146">Ne feledje, hogy `dpkg -i` unmet függőségekkel rendelkező sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="57a22-146">Please note that `dpkg -i` will fail with unmet dependencies.</span></span>
> <span data-ttu-id="57a22-147">A következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="57a22-147">The next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="57a22-148">Az Eltávolítás - Debian 8</span><span class="sxs-lookup"><span data-stu-id="57a22-148">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="57a22-149">Debian 9</span><span class="sxs-lookup"><span data-stu-id="57a22-149">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="57a22-150">Telepítési csomag tárház – Debian 9 keresztül</span><span class="sxs-lookup"><span data-stu-id="57a22-150">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="57a22-151">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="57a22-151">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="57a22-152">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="57a22-152">This is the preferred method.</span></span>

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

<span data-ttu-id="57a22-153">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="57a22-153">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="57a22-154">Közvetlen letöltése – Debian 9 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="57a22-154">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="57a22-155">A Debian csomag `powershell_6.0.2-1.debian.9_amd64.deb` a a [Kiadások][] a Debian gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="57a22-155">Download the Debian package `powershell_6.0.2-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="57a22-156">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="57a22-156">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="57a22-157">Ne feledje, hogy `dpkg -i` unmet függőségekkel rendelkező sikertelen lesz.</span><span class="sxs-lookup"><span data-stu-id="57a22-157">Please note that `dpkg -i` will fail with unmet dependencies.</span></span>
> <span data-ttu-id="57a22-158">A következő parancs `apt-get install -f` megoldja-e, és majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="57a22-158">The next command, `apt-get install -f` resolves these and then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-9"></a><span data-ttu-id="57a22-159">Az Eltávolítás - Debian 9</span><span class="sxs-lookup"><span data-stu-id="57a22-159">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="57a22-160">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="57a22-160">CentOS 7</span></span>

> <span data-ttu-id="57a22-161">Ez a csomag is működik-e az Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="57a22-161">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="57a22-162">Telepítési csomag tárház (ajánlott) – CentOS 7 keresztül</span><span class="sxs-lookup"><span data-stu-id="57a22-162">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="57a22-163">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="57a22-163">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="57a22-164">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="57a22-164">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="57a22-165">Közvetlen letöltése – CentOS 7 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="57a22-165">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="57a22-166">Használatával [CentOS 7][], a RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [Kiadások][] a CentOS gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="57a22-166">Using [CentOS 7][], download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="57a22-167">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="57a22-167">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="57a22-168">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="57a22-168">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="57a22-169">Az Eltávolítás - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="57a22-169">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="57a22-171">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="57a22-171">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="57a22-172">Telepítési csomag tárház (ajánlott) - Red Hat Enterprise Linux (RHEL) 7 keresztül</span><span class="sxs-lookup"><span data-stu-id="57a22-172">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="57a22-173">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="57a22-173">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="57a22-174">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="57a22-174">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="57a22-175">Közvetlen letöltése – Red Hat Enterprise Linux (RHEL) 7 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="57a22-175">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="57a22-176">A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [Kiadások][] a Red Hat Enterprise Linux-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="57a22-176">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="57a22-177">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="57a22-177">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="57a22-178">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="57a22-178">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="57a22-179">Az Eltávolítás - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="57a22-179">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a><span data-ttu-id="57a22-180">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="57a22-180">OpenSUSE 42.2</span></span>

> [!NOTE]
> <span data-ttu-id="57a22-181">PowerShell központ telepítésekor `zypper` előfordulhat, hogy a következő hiba jelentését:</span><span class="sxs-lookup"><span data-stu-id="57a22-181">When installing PowerShell Core, `zypper` may report the following error:</span></span>
>
> ```Output
> Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
>  Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
>  Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
> ```
>
> <span data-ttu-id="57a22-182">Ebben az esetben ellenőrizze, hogy a kompatibilis `libcurl` könyvtár megtalálható úgy, hogy a következő parancsot a jeleníti meg a `libcurl4` csomag telepítve:</span><span class="sxs-lookup"><span data-stu-id="57a22-182">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>
>
> ```sh
> zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
> ```
>
> <span data-ttu-id="57a22-183">Válassza ki a `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` megoldás a PowerShell csomag telepítésekor.</span><span class="sxs-lookup"><span data-stu-id="57a22-183">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the PowerShell package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-422"></a><span data-ttu-id="57a22-184">Telepítési csomag tárház (ajánlott) - OpenSUSE 42.2 keresztül</span><span class="sxs-lookup"><span data-stu-id="57a22-184">Installation via Package Repository (preferred) - OpenSUSE 42.2</span></span>

<span data-ttu-id="57a22-185">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="57a22-185">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---opensuse-422"></a><span data-ttu-id="57a22-186">Közvetlen letöltése – OpenSUSE 42.2 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="57a22-186">Installation via Direct Download - OpenSUSE 42.2</span></span>

<span data-ttu-id="57a22-187">A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [Kiadások][] a OpenSUSE gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="57a22-187">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="57a22-188">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="57a22-188">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a><span data-ttu-id="57a22-189">Az Eltávolítás - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="57a22-189">Uninstallation - OpenSUSE 42.2</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a><span data-ttu-id="57a22-190">Fedora</span><span class="sxs-lookup"><span data-stu-id="57a22-190">Fedora</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="57a22-191">Telepítési csomag tárház (ajánlott) - Fedora 27 Fedora 28 keresztül</span><span class="sxs-lookup"><span data-stu-id="57a22-191">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="57a22-192">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="57a22-192">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="57a22-193">Közvetlen letöltése – Fedora 27, Fedora 28 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="57a22-193">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="57a22-194">A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [Kiadások][] a Fedora gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="57a22-194">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="57a22-195">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="57a22-195">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="57a22-196">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="57a22-196">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="57a22-197">Az Eltávolítás - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="57a22-197">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="57a22-198">Linux architektúrája</span><span class="sxs-lookup"><span data-stu-id="57a22-198">Arch Linux</span></span>

<span data-ttu-id="57a22-199">PowerShell érhető el a [Linux architektúrája][] felhasználói tárház (AUR).</span><span class="sxs-lookup"><span data-stu-id="57a22-199">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="57a22-200">Az összeállítható a [legújabb címkézett kiadás][arch-release]</span><span class="sxs-lookup"><span data-stu-id="57a22-200">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="57a22-201">Az összeállítható a [fő legújabb véglegesítési][arch-git]</span><span class="sxs-lookup"><span data-stu-id="57a22-201">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="57a22-202">Használatával telepíthető a [bináris legújabb kiadás][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="57a22-202">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="57a22-203">A AUR csomagok karbantartása közösségi – nincs hivatalos támogatás.</span><span class="sxs-lookup"><span data-stu-id="57a22-203">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="57a22-204">A csomagok telepítése a AUR a további információkért lásd: a [architektúrája Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a közösségi [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="57a22-204">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Linux architektúrája]: https://www.archlinux.org/download/
[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="57a22-206">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="57a22-206">Linux AppImage</span></span>

<span data-ttu-id="57a22-207">A legutóbbi Linux-eloszlás használatával töltse le a AppImage `powershell-6.0.1-x86_64.AppImage` a a [Kiadások][] a Linux-gépek oldalon.</span><span class="sxs-lookup"><span data-stu-id="57a22-207">Using a recent Linux distribution, download the AppImage `powershell-6.0.1-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="57a22-208">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="57a22-208">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

<span data-ttu-id="57a22-209">A [AppImage][] lehetővé teszi, hogy a telepítés nélküli PowerShell futtatásához.</span><span class="sxs-lookup"><span data-stu-id="57a22-209">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="57a22-210">Egy hordozható alkalmazás, amely a PowerShell és a függőségek (beleértve a .NET Core rendszer függőségeket) bundles egy javul csomagba.</span><span class="sxs-lookup"><span data-stu-id="57a22-210">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="57a22-211">Ez a csomag, amely a felhasználó a Linux-disztribúció függetlenül működik egy bináris.</span><span class="sxs-lookup"><span data-stu-id="57a22-211">This package  is a single binary that works independently of the user's Linux distribution.</span></span>

[appimage]: http://appimage.org/

## <a name="kali"></a><span data-ttu-id="57a22-213">Kali</span><span class="sxs-lookup"><span data-stu-id="57a22-213">Kali</span></span>

### <a name="installation"></a><span data-ttu-id="57a22-214">Telepítés</span><span class="sxs-lookup"><span data-stu-id="57a22-214">Installation</span></span>

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

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="57a22-215">Futtassa a PowerShell legújabb Kali (Kali GNU/Linux folyamatos) a telepítés nélküli</span><span class="sxs-lookup"><span data-stu-id="57a22-215">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="57a22-216">Az Eltávolítás - Kali</span><span class="sxs-lookup"><span data-stu-id="57a22-216">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="57a22-217">Raspbian</span><span class="sxs-lookup"><span data-stu-id="57a22-217">Raspbian</span></span>

<span data-ttu-id="57a22-218">PowerShell jelenleg csak Raspbian Stretch támogatott.</span><span class="sxs-lookup"><span data-stu-id="57a22-218">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="57a22-219">Is CoreCLR (és így PowerShell Core) csak Pi 2 és Pi 3 eszközökön módon fog más eszközök, például [Pi nulla](https://github.com/dotnet/coreclr/issues/10605), egy nem támogatott processzorral rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="57a22-219">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="57a22-220">Töltse le [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) , és kövesse a [telepítési utasításokat](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) a Pi eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="57a22-220">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation"></a><span data-ttu-id="57a22-221">Telepítés</span><span class="sxs-lookup"><span data-stu-id="57a22-221">Installation</span></span>

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

<span data-ttu-id="57a22-222">Nem kötelező elérési út megadását a "pwsh" bináris nélkül indítsa el a Powershellt szeretné szimbolikus hivatkozást hozhat létre</span><span class="sxs-lookup"><span data-stu-id="57a22-222">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="57a22-223">Az Eltávolítás - Raspbian</span><span class="sxs-lookup"><span data-stu-id="57a22-223">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="57a22-224">Bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="57a22-224">Binary Archives</span></span>

<span data-ttu-id="57a22-225">PowerShell bináris `tar.gz` archívumokat biztosított Linux-platformokhoz lehetővé központi telepítési forgatókönyveket.</span><span class="sxs-lookup"><span data-stu-id="57a22-225">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="57a22-226">Függőségek</span><span class="sxs-lookup"><span data-stu-id="57a22-226">Dependencies</span></span>

<span data-ttu-id="57a22-227">PowerShell alkot az összes Linux terjesztésekről hordozható bináris fájljait.</span><span class="sxs-lookup"><span data-stu-id="57a22-227">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="57a22-228">De a .NET Core runtime szükséges a különböző terjesztések átviteli különböző függőségek, és ezért PowerShell szerepe ugyanaz.</span><span class="sxs-lookup"><span data-stu-id="57a22-228">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="57a22-229">Az alábbi ábra mutatja a .NET Core 2.0 függőségek hivatalosan által támogatott különböző Linux terjesztéseket.</span><span class="sxs-lookup"><span data-stu-id="57a22-229">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="57a22-230">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="57a22-230">OS</span></span>                 | <span data-ttu-id="57a22-231">Függőségek</span><span class="sxs-lookup"><span data-stu-id="57a22-231">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="57a22-232">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="57a22-232">Ubuntu 14.04</span></span>       | <span data-ttu-id="57a22-233">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="57a22-233">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="57a22-234">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="57a22-234">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="57a22-235">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="57a22-235">Ubuntu 16.04</span></span>       | <span data-ttu-id="57a22-236">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="57a22-236">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="57a22-237">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="57a22-237">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="57a22-238">Ubuntu 17.04</span><span class="sxs-lookup"><span data-stu-id="57a22-238">Ubuntu 17.04</span></span>       | <span data-ttu-id="57a22-239">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="57a22-239">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="57a22-240">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="57a22-240">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="57a22-241">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="57a22-241">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="57a22-242">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="57a22-242">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="57a22-243">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="57a22-243">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="57a22-244">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="57a22-244">Debian 9 (Stretch)</span></span> | <span data-ttu-id="57a22-245">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="57a22-245">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="57a22-246">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="57a22-246">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="57a22-247">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="57a22-247">CentOS 7</span></span> <br> <span data-ttu-id="57a22-248">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="57a22-248">Oracle Linux 7</span></span> <br> <span data-ttu-id="57a22-249">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="57a22-249">RHEL 7</span></span> <br> <span data-ttu-id="57a22-250">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="57a22-250">OpenSUSE 42.2</span></span> | <span data-ttu-id="57a22-251">libunwind, libcurl, openssl-függvénytárak, libicu</span><span class="sxs-lookup"><span data-stu-id="57a22-251">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="57a22-252">27 Fedora</span><span class="sxs-lookup"><span data-stu-id="57a22-252">Fedora 27</span></span> <br> <span data-ttu-id="57a22-253">28 Fedora</span><span class="sxs-lookup"><span data-stu-id="57a22-253">Fedora 28</span></span> | <span data-ttu-id="57a22-254">libunwind, libcurl, openssl-függvénytárak, libicu, / compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="57a22-254">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="57a22-255">Az telepítéséhez PowerShell bináris fájljait, a Linux terjesztéseket, amelyek hivatalosan nem támogatottak, kell telepíteni a cél operációs rendszer szükséges függőségek külön lépéseket.</span><span class="sxs-lookup"><span data-stu-id="57a22-255">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="57a22-256">Például a [Amazon Linux dockerfile] [ amazon-dockerfile] függőségek először telepíti, és kinyeri a Linux `tar.gz` archív.</span><span class="sxs-lookup"><span data-stu-id="57a22-256">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="57a22-257">Telepítés – bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="57a22-257">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="57a22-258">Linux</span><span class="sxs-lookup"><span data-stu-id="57a22-258">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="57a22-259">Bináris archívumokat eltávolítása</span><span class="sxs-lookup"><span data-stu-id="57a22-259">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="57a22-260">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="57a22-260">Paths</span></span>

* <span data-ttu-id="57a22-261">`$PSHOME` van `/opt/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="57a22-261">`$PSHOME` is `/opt/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="57a22-262">Felhasználói profilok rendszer nem olvas be `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="57a22-262">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="57a22-263">Alapértelmezett profilok rendszer nem olvas be `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="57a22-263">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="57a22-264">Modulok felhasználói rendszer nem olvas be `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="57a22-264">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="57a22-265">Megosztott modulok rendszer nem olvas be `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="57a22-265">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="57a22-266">Az alapértelmezett modulokat rendszer nem olvas be `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="57a22-266">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="57a22-267">A rögzítendő PSReadline előzmények `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="57a22-267">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="57a22-268">A profilok tiszteletben PowerShell gazdagép konfiguráció, így az alapértelmezett gazdagép-specifikus profilok létezik az `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="57a22-268">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="57a22-269">PowerShell tiszteletben tartja a [XDG Base könyvtár megadása] [ xdg-bds] Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="57a22-269">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[Kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
