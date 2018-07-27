# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="83750-101">A PowerShell Core telepítése Linux rendszerre</span><span class="sxs-lookup"><span data-stu-id="83750-101">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="83750-102">Támogatja a [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.10] [ u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7] [ cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.3][opensuse], [Fedora 27 ] [ fedora], [Fedora 28][fedora], és [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="83750-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.10][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.3][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="83750-103">A hivatalosan nem támogatott Linux-disztribúció, megpróbálhatja használatával a [PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="83750-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span>
<span data-ttu-id="83750-104">Üzembe helyezése a PowerShell bináris fájlokat közvetlenül a a Linux használatával is megpróbálhatja [ `tar.gz` archív][tar], de állítsa be a szükséges függőségek az operációs rendszer a különálló lépések alapján kell.</span><span class="sxs-lookup"><span data-stu-id="83750-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="83750-105">A githubon érhető el az összes csomag [kiadások][] lapot.</span><span class="sxs-lookup"><span data-stu-id="83750-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="83750-106">A csomag telepítése után futtassa `pwsh` parancsot egy terminálról.</span><span class="sxs-lookup"><span data-stu-id="83750-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u17]: #ubuntu-1710
[u18]: #ubuntu-1804
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-423
[fedora]: #fedora
[arch]: #arch-linux
[lai]: #linux-appimage
[tar]: #binary-archives

## <a name="installing-preview-releases"></a><span data-ttu-id="83750-107">Előzetes verziók telepítése</span><span class="sxs-lookup"><span data-stu-id="83750-107">Installing Preview Releases</span></span>

<span data-ttu-id="83750-108">A PowerShell Core előzetes kiadás telepítése Linux rendszeren keresztül egy Csomagtárház esetén a csomag nevét a változik `powershell` való `powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="83750-108">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="83750-109">Közvetlen letöltésére keresztül telepítése nem változik, a fájl neve eltérő.</span><span class="sxs-lookup"><span data-stu-id="83750-109">Installing via direct download does not change, other than the file name.</span></span>

<span data-ttu-id="83750-110">Íme egy táblát a parancsokat a különböző csomagkezelőinek használatával stabil és előzetes csomagok telepítéséhez:</span><span class="sxs-lookup"><span data-stu-id="83750-110">Here is a table of the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="83750-111">Distribution(s)</span><span class="sxs-lookup"><span data-stu-id="83750-111">Distribution(s)</span></span>|<span data-ttu-id="83750-112">Stabil parancs</span><span class="sxs-lookup"><span data-stu-id="83750-112">Stable Command</span></span> | <span data-ttu-id="83750-113">A parancs előzetes verzió</span><span class="sxs-lookup"><span data-stu-id="83750-113">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="83750-114">Ubuntu, a Debian</span><span class="sxs-lookup"><span data-stu-id="83750-114">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="83750-115">CentOS, a RedHat</span><span class="sxs-lookup"><span data-stu-id="83750-115">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="83750-116">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="83750-116">OpenSUSE</span></span> |`sudo zypper install powershell` | `sudo zypper install powershell-preview`|
| <span data-ttu-id="83750-117">Fedora</span><span class="sxs-lookup"><span data-stu-id="83750-117">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a><span data-ttu-id="83750-118">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="83750-118">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="83750-119">Telepítési Csomagtárház - Ubuntu 14.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-119">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="83750-120">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="83750-120">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="83750-121">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="83750-121">This is the preferred method.</span></span>

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

<span data-ttu-id="83750-122">Superuser, mint a Microsoft-tárház regisztrálása.</span><span class="sxs-lookup"><span data-stu-id="83750-122">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="83750-123">Ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni a telepítés.</span><span class="sxs-lookup"><span data-stu-id="83750-123">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="83750-124">Telepítési közvetlen letöltése – Ubuntu 14.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-124">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="83750-125">A Debian csomag `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` származó a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="83750-125">Download the Debian package `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="83750-126">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="83750-126">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="83750-127">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="83750-127">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="83750-128">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="83750-128">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="83750-129">Eltávolítás – Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="83750-129">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="83750-130">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="83750-130">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="83750-131">Telepítési csomag tárház - Ubuntu 16.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-131">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="83750-132">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="83750-132">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="83750-133">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="83750-133">This is the preferred method.</span></span>

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

<span data-ttu-id="83750-134">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="83750-134">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="83750-135">Telepítési közvetlen letöltése – Ubuntu 16.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-135">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="83750-136">A Debian csomag `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` származó a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="83750-136">Download the Debian package `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="83750-137">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="83750-137">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="83750-138">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="83750-138">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="83750-139">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="83750-139">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="83750-140">Eltávolítás – Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="83750-140">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1710"></a><span data-ttu-id="83750-141">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="83750-141">Ubuntu 17.10</span></span>

> [!NOTE]
> <span data-ttu-id="83750-142">Miután Ubuntu 17.04 támogatása hozzáadva `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="83750-142">Support for Ubuntu 17.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1710"></a><span data-ttu-id="83750-143">Telepítési csomag tárház - Ubuntu 17.10-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-143">Installation via Package Repository - Ubuntu 17.10</span></span>

<span data-ttu-id="83750-144">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="83750-144">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="83750-145">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="83750-145">This is the preferred method.</span></span>

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

<span data-ttu-id="83750-146">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="83750-146">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1710"></a><span data-ttu-id="83750-147">Telepítési közvetlen letöltése – Ubuntu 17.10-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-147">Installation via Direct Download - Ubuntu 17.10</span></span>

<span data-ttu-id="83750-148">A Debian csomag `powershell_6.0.2-1.ubuntu.17.10_amd64.deb` származó a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="83750-148">Download the Debian package `powershell_6.0.2-1.ubuntu.17.10_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="83750-149">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="83750-149">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.17.10_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="83750-150">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="83750-150">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="83750-151">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="83750-151">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1710"></a><span data-ttu-id="83750-152">Eltávolítás – Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="83750-152">Uninstallation - Ubuntu 17.10</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="83750-153">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="83750-153">Ubuntu 18.04</span></span>

> [!NOTE]
> <span data-ttu-id="83750-154">Miután Ubuntu 18.04 támogatása hozzáadva `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="83750-154">Support for Ubuntu 18.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="83750-155">Telepítési csomag tárház - Ubuntu 18.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-155">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="83750-156">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="83750-156">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="83750-157">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="83750-157">This is the preferred method.</span></span>

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

<span data-ttu-id="83750-158">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="83750-158">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="83750-159">Telepítési közvetlen letöltése – Ubuntu 18.04-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-159">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="83750-160">A Debian csomag `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` származó a [kiadások][] az Ubuntu-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="83750-160">Download the Debian package `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="83750-161">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="83750-161">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="83750-162">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="83750-162">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="83750-163">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="83750-163">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1804"></a><span data-ttu-id="83750-164">Eltávolítás – Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="83750-164">Uninstallation - Ubuntu 18.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="83750-165">Debian 8</span><span class="sxs-lookup"><span data-stu-id="83750-165">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="83750-166">Telepítési Csomagtárház – Debian 8-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-166">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="83750-167">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="83750-167">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="83750-168">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="83750-168">This is the preferred method.</span></span>

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

<span data-ttu-id="83750-169">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="83750-169">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="83750-170">Keresztül közvetlen letöltése – Debian 8 telepítés</span><span class="sxs-lookup"><span data-stu-id="83750-170">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="83750-171">A Debian csomag `powershell_6.0.2-1.debian.8_amd64.deb` származó a [kiadások][] oldal arra a Debian gépre.</span><span class="sxs-lookup"><span data-stu-id="83750-171">Download the Debian package `powershell_6.0.2-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="83750-172">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="83750-172">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="83750-173">A `dpkg -i` teljesítetlen függőségekkel parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="83750-173">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="83750-174">A következő parancsot, `apt-get install -f` oldja fel ezeket a problémákat, majd befejezi a PowerShell-csomag konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="83750-174">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="83750-175">Eltávolítás – Debian 8</span><span class="sxs-lookup"><span data-stu-id="83750-175">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="83750-176">Debian 9</span><span class="sxs-lookup"><span data-stu-id="83750-176">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="83750-177">Telepítési csomag tárház – Debian 9-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-177">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="83750-178">A PowerShell Core, Linux, az egyszerű telepítés (és frissítések) csomag tárházak van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="83750-178">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="83750-179">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="83750-179">This is the preferred method.</span></span>

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

<span data-ttu-id="83750-180">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ettől kezdve az imént kell használnia `sudo apt-get upgrade powershell` frissíteni.</span><span class="sxs-lookup"><span data-stu-id="83750-180">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="83750-181">Telepítési közvetlen letöltése – Debian 9-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-181">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="83750-182">A Debian csomag `powershell_6.0.2-1.debian.9_amd64.deb` származó a [kiadások][] oldal arra a Debian gépre.</span><span class="sxs-lookup"><span data-stu-id="83750-182">Download the Debian package `powershell_6.0.2-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="83750-183">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="83750-183">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="83750-184">Eltávolítás – Debian 9</span><span class="sxs-lookup"><span data-stu-id="83750-184">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="83750-185">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="83750-185">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="83750-186">Ez a csomag az Oracle Linux 7 is működik.</span><span class="sxs-lookup"><span data-stu-id="83750-186">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="83750-187">Telepítési csomag tárház (preferált) – CentOS 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-187">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="83750-188">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="83750-188">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="83750-189">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="83750-189">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="83750-190">Keresztül közvetlen letöltése – CentOS 7 telepítése</span><span class="sxs-lookup"><span data-stu-id="83750-190">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="83750-191">Használatával [CentOS 7][], töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadások][] oldal arra a CentOS-gépre.</span><span class="sxs-lookup"><span data-stu-id="83750-191">Using [CentOS 7][], download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="83750-192">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="83750-192">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="83750-193">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="83750-193">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="83750-194">Eltávolítás – CentOS 7</span><span class="sxs-lookup"><span data-stu-id="83750-194">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="83750-196">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="83750-196">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="83750-197">Telepítési csomag tárház (preferált) – Red Hat Enterprise Linux (RHEL) 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-197">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="83750-198">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="83750-198">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="83750-199">A Microsoft-tárházat a felügyelői, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="83750-199">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="83750-200">Telepítési közvetlen letöltése – Red Hat Enterprise Linux (RHEL) 7-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-200">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="83750-201">Töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` származó a [kiadások][] oldal arra a Red Hat Enterprise Linux-gépre.</span><span class="sxs-lookup"><span data-stu-id="83750-201">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="83750-202">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="83750-202">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="83750-203">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="83750-203">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="83750-204">Eltávolítás – Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="83750-204">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-423"></a><span data-ttu-id="83750-205">OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="83750-205">OpenSUSE 42.3</span></span>

<span data-ttu-id="83750-206">A PowerShell Core, telepítésekor `zypper` feltétlenül jelentik a következő hibával:</span><span class="sxs-lookup"><span data-stu-id="83750-206">When installing PowerShell Core, `zypper` may report the following error:</span></span>

```Output
Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
 Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
 Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
```

<span data-ttu-id="83750-207">Ebben az esetben ellenőrizze, hogy a kompatibilis `libcurl` könyvtár megtalálható úgy, hogy a következő parancsot a látható a `libcurl4` csomag telepítve vannak:</span><span class="sxs-lookup"><span data-stu-id="83750-207">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>

```sh
zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
```

<span data-ttu-id="83750-208">Majd válassza ki a `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` megoldáshoz, amikor a PowerShell-csomag telepítése.</span><span class="sxs-lookup"><span data-stu-id="83750-208">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the PowerShell package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-423"></a><span data-ttu-id="83750-209">Telepítés (preferált) – Csomagtárház OpenSUSE 42.3 keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-209">Installation via Package Repository (preferred) - OpenSUSE 42.3</span></span>

<span data-ttu-id="83750-210">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="83750-210">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---opensuse-423"></a><span data-ttu-id="83750-211">Telepítési közvetlen letöltése – OpenSUSE 42.3-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-211">Installation via Direct Download - OpenSUSE 42.3</span></span>

<span data-ttu-id="83750-212">Töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` származó a [kiadások][] lap arra az opensuse-alapú gépre.</span><span class="sxs-lookup"><span data-stu-id="83750-212">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="83750-213">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="83750-213">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-423"></a><span data-ttu-id="83750-214">Eltávolítás – OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="83750-214">Uninstallation - OpenSUSE 42.3</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a><span data-ttu-id="83750-215">Fedora</span><span class="sxs-lookup"><span data-stu-id="83750-215">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="83750-216">Fedora 28 csak akkor támogatott, a PowerShell Core 6.1-es és újabb.</span><span class="sxs-lookup"><span data-stu-id="83750-216">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="83750-217">Telepítési csomag tárház (preferált) – Fedora 27., Fedora 28-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-217">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="83750-218">A PowerShell Core for Linux hivatalos Microsoft-tárházak egyszerű telepítéshez (és frissítések) van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="83750-218">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="83750-219">Telepítési közvetlen letöltése – Fedora 27, Fedora 28-n keresztül</span><span class="sxs-lookup"><span data-stu-id="83750-219">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="83750-220">Töltse le az RPM-csomagot `powershell-6.0.2-1.rhel.7.x86_64.rpm` származó a [kiadások][] oldal arra a Fedora gépre.</span><span class="sxs-lookup"><span data-stu-id="83750-220">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="83750-221">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="83750-221">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="83750-222">Az RPM anélkül, hogy töltse le a köztes lépés is telepítheti:</span><span class="sxs-lookup"><span data-stu-id="83750-222">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="83750-223">Eltávolítás – Fedora 27., Fedora 28</span><span class="sxs-lookup"><span data-stu-id="83750-223">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="83750-224">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="83750-224">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="83750-225">A rendszer kísérleti emelőkaros támogatja.</span><span class="sxs-lookup"><span data-stu-id="83750-225">Arch support is experimental.</span></span>

<span data-ttu-id="83750-226">PowerShell érhető el a [Arch Linux][] felhasználói tárház (AUR).</span><span class="sxs-lookup"><span data-stu-id="83750-226">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="83750-227">Az összeállítható a [legújabb címkézett kiadás][arch-release]</span><span class="sxs-lookup"><span data-stu-id="83750-227">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="83750-228">Az összeállítható a [fő a legutóbbi véglegesítést][arch-git]</span><span class="sxs-lookup"><span data-stu-id="83750-228">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="83750-229">Használatával telepíthető a [legújabb kibocsátási bináris][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="83750-229">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="83750-230">A AUR csomagok közösségi kezelt – nem hivatalos támogatott.</span><span class="sxs-lookup"><span data-stu-id="83750-230">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="83750-231">A AUR a csomagok telepítésével kapcsolatos további információkért lásd: a [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a Közösség [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="83750-231">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="83750-233">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="83750-233">Linux AppImage</span></span>

> [!NOTE]
> <span data-ttu-id="83750-234">AppImage támogatási je experimentální.</span><span class="sxs-lookup"><span data-stu-id="83750-234">AppImage support is experimental</span></span>

<span data-ttu-id="83750-235">Legutóbbi Linux-disztribúció használatával töltse le a AppImage `powershell-6.0.1-x86_64.AppImage` származó a [kiadások][] oldal arra a Linux-gépre.</span><span class="sxs-lookup"><span data-stu-id="83750-235">Using a recent Linux distribution, download the AppImage `powershell-6.0.1-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="83750-236">Ezután hajtsa végre a következő billentyűparancsot a terminálon:</span><span class="sxs-lookup"><span data-stu-id="83750-236">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

<span data-ttu-id="83750-237">A [AppImage][] teszi lehetővé a PowerShell futtatása nélkül telepíti azt.</span><span class="sxs-lookup"><span data-stu-id="83750-237">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="83750-238">Egy hordozható alkalmazást, amely a PowerShell és annak függőségeit, (beleértve a .NET Core rendszerfüggőségekben) bundles javul csomagba.</span><span class="sxs-lookup"><span data-stu-id="83750-238">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="83750-239">A csomag nincs egyetlen bináris, amely a felhasználó Linux-disztribúció függetlenül működik.</span><span class="sxs-lookup"><span data-stu-id="83750-239">This package is a single binary that works independently of the user's Linux distribution.</span></span>

[appimage]: http://appimage.org/

## <a name="kali"></a><span data-ttu-id="83750-241">Kali</span><span class="sxs-lookup"><span data-stu-id="83750-241">Kali</span></span>

> [!NOTE]
> <span data-ttu-id="83750-242">Kali támogatási je experimentální.</span><span class="sxs-lookup"><span data-stu-id="83750-242">Kali support is experimental.</span></span>

### <a name="installation"></a><span data-ttu-id="83750-243">Telepítés</span><span class="sxs-lookup"><span data-stu-id="83750-243">Installation</span></span>

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

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="83750-244">Futtassa a Powershellt a legújabb Kali (GNU/Linux folyamatos Kali) azt telepítése nélkül</span><span class="sxs-lookup"><span data-stu-id="83750-244">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="83750-245">Eltávolítás – Kali</span><span class="sxs-lookup"><span data-stu-id="83750-245">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="83750-246">Raspbian</span><span class="sxs-lookup"><span data-stu-id="83750-246">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="83750-247">Raspbian támogatási je experimentální.</span><span class="sxs-lookup"><span data-stu-id="83750-247">Raspbian support is experimental.</span></span>

<span data-ttu-id="83750-248">PowerShell jelenleg csak a Raspbian Stretch támogatott.</span><span class="sxs-lookup"><span data-stu-id="83750-248">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="83750-249">Emellett coreclr-nek (és így a PowerShell Core) csak 2 tartományban és Pi 3 eszközökön módon fog más eszközök, például [Pi nulla](https://github.com/dotnet/coreclr/issues/10605), egy nem támogatott processzorral rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="83750-249">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="83750-250">Töltse le [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) , és kövesse a [telepítési utasításokat](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) a Pi eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="83750-250">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation"></a><span data-ttu-id="83750-251">Telepítés</span><span class="sxs-lookup"><span data-stu-id="83750-251">Installation</span></span>

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

<span data-ttu-id="83750-252">Igény szerint hozhat létre a szimbolikus hivatkozást úgy, hogy tudni indítsa el a Powershellt, a "pwsh" bináris elérési út megadása nélkül</span><span class="sxs-lookup"><span data-stu-id="83750-252">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="83750-253">Eltávolítás – Raspbian</span><span class="sxs-lookup"><span data-stu-id="83750-253">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="83750-254">Bináris archívum</span><span class="sxs-lookup"><span data-stu-id="83750-254">Binary Archives</span></span>

<span data-ttu-id="83750-255">PowerShell bináris `tar.gz` archívumok biztosított Linux-platformokhoz a speciális üzembe helyezési forgatókönyvek megvalósítását teszik lehetővé.</span><span class="sxs-lookup"><span data-stu-id="83750-255">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="83750-256">Függőségek</span><span class="sxs-lookup"><span data-stu-id="83750-256">Dependencies</span></span>

<span data-ttu-id="83750-257">PowerShell az összes Linux-disztribúciókra vonatkozó hordozható bináris épít fel.</span><span class="sxs-lookup"><span data-stu-id="83750-257">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="83750-258">De a .NET Core runtime szükséges különböző disztribúciókon különböző függőségek, és ezért PowerShell pedig ugyanezt.</span><span class="sxs-lookup"><span data-stu-id="83750-258">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="83750-259">A következő diagram a .NET Core 2.0 hivatalosan támogatott különböző Linux-disztribúciókon függőségeit jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="83750-259">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="83750-260">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="83750-260">OS</span></span>                 | <span data-ttu-id="83750-261">Függőségek</span><span class="sxs-lookup"><span data-stu-id="83750-261">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="83750-262">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="83750-262">Ubuntu 14.04</span></span>       | <span data-ttu-id="83750-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="83750-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="83750-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="83750-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="83750-265">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="83750-265">Ubuntu 16.04</span></span>       | <span data-ttu-id="83750-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="83750-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="83750-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="83750-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="83750-268">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="83750-268">Ubuntu 17.10</span></span>       | <span data-ttu-id="83750-269">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="83750-269">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="83750-270">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="83750-270">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="83750-271">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="83750-271">Ubuntu 18.04</span></span>       | <span data-ttu-id="83750-272">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="83750-272">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="83750-273">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="83750-273">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="83750-274">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="83750-274">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="83750-275">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="83750-275">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="83750-276">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="83750-276">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="83750-277">Debian 9 (Nyújtás)</span><span class="sxs-lookup"><span data-stu-id="83750-277">Debian 9 (Stretch)</span></span> | <span data-ttu-id="83750-278">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="83750-278">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="83750-279">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="83750-279">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="83750-280">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="83750-280">CentOS 7</span></span> <br> <span data-ttu-id="83750-281">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="83750-281">Oracle Linux 7</span></span> <br> <span data-ttu-id="83750-282">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="83750-282">RHEL 7</span></span> <br> <span data-ttu-id="83750-283">OpenSUSE OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="83750-283">OpenSUSE OpenSUSE 42.3</span></span> | <span data-ttu-id="83750-284">libunwind, libcurl, openssl-függvénytárak, libicu</span><span class="sxs-lookup"><span data-stu-id="83750-284">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="83750-285">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="83750-285">Fedora 27</span></span> <br> <span data-ttu-id="83750-286">28 Fedora</span><span class="sxs-lookup"><span data-stu-id="83750-286">Fedora 28</span></span> | <span data-ttu-id="83750-287">libunwind, libcurl, openssl-függvénytárak, libicu, a/compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="83750-287">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="83750-288">Nem hivatalosan támogatott Linux-disztribúciókon a PowerShell bináris fájljainak telepítéséhez telepíteni szeretné a cél operációs rendszer szükséges függőséget a különálló lépések.</span><span class="sxs-lookup"><span data-stu-id="83750-288">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="83750-289">Például a [Amazon Linux dockerfile] [ amazon-dockerfile] először telepíti a függőségeket, és ezt követően kiolvassa a Linuxos `tar.gz` archív.</span><span class="sxs-lookup"><span data-stu-id="83750-289">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="83750-290">Telepítés – bináris archívum</span><span class="sxs-lookup"><span data-stu-id="83750-290">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="83750-291">Linux</span><span class="sxs-lookup"><span data-stu-id="83750-291">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="83750-292">Bináris archívum eltávolítása</span><span class="sxs-lookup"><span data-stu-id="83750-292">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="83750-293">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="83750-293">Paths</span></span>

* <span data-ttu-id="83750-294">`$PSHOME` van `/opt/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="83750-294">`$PSHOME` is `/opt/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="83750-295">Felhasználói profilokat fog olvasni `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="83750-295">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="83750-296">Alapértelmezett profilokat fog olvasni `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="83750-296">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="83750-297">Felhasználói modulok fog olvasni `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="83750-297">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="83750-298">Megosztott modulok fog olvasni `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="83750-298">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="83750-299">Az alapértelmezett modulokat fog olvasni `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="83750-299">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="83750-300">PSReadline előzmények lesz rögzítve a `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="83750-300">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="83750-301">A profilok tiszteletben PowerShell a gazdagép konfiguráció, így az alapértelmezett gazdagép-specifikus profilok létezik `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="83750-301">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="83750-302">PowerShell tiszteletben tartja a [XDG alap könyvtár megadása] [ xdg-bds] Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="83750-302">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[kiadások]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
