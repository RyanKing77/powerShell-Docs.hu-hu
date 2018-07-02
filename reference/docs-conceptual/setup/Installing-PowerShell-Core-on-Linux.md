# <a name="installing-powershell-core-on-linux"></a><span data-ttu-id="10961-101">A PowerShell Core telepítése Linux rendszerre</span><span class="sxs-lookup"><span data-stu-id="10961-101">Installing PowerShell Core on Linux</span></span>

<span data-ttu-id="10961-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.10][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span><span class="sxs-lookup"><span data-stu-id="10961-102">Supports [Ubuntu 14.04][u14], [Ubuntu 16.04][u16], [Ubuntu 17.10][u17], [Debian 8][deb8], [Debian 9][deb9], [CentOS 7][cos], [Red Hat Enterprise Linux (RHEL) 7][rhel7], [OpenSUSE 42.2][opensuse], [Fedora 27][fedora], [Fedora 28][fedora], and [Arch Linux][arch].</span></span>

<span data-ttu-id="10961-103">A Linux terjesztéseket, amelyek hivatalosan nem támogatottak, próbálkozhat a [PowerShell AppImage][lai].</span><span class="sxs-lookup"><span data-stu-id="10961-103">For Linux distributions that are not officially supported, you can try using the [PowerShell AppImage][lai].</span></span>
<span data-ttu-id="10961-104">Közvetlenül a Linux-használat PowerShell bináris fájljainak telepítéséhez is megpróbálhatja [ `tar.gz` archív][tar], de állítsa be a szükséges függőségek az operációs rendszer, a különálló lépések alapján kell.</span><span class="sxs-lookup"><span data-stu-id="10961-104">You can also try deploying PowerShell binaries directly using the Linux [`tar.gz` archive][tar], but you would need to set up the necessary dependencies based on the OS in separate steps.</span></span>

<span data-ttu-id="10961-105">Minden csomagok érhetők el a githubon [kiadott][] lap.</span><span class="sxs-lookup"><span data-stu-id="10961-105">All packages are available on our GitHub [releases][] page.</span></span>
<span data-ttu-id="10961-106">A csomag telepítése után futtassa `pwsh` terminálról.</span><span class="sxs-lookup"><span data-stu-id="10961-106">Once the package is installed, run `pwsh` from a terminal.</span></span>

[u14]: #ubuntu-1404
[u16]: #ubuntu-1604
[u17]: #ubuntu-1710
[deb8]: #debian-8
[deb9]: #debian-9
[cos]: #centos-7
[rhel7]: #red-hat-enterprise-linux-rhel-7
[opensuse]: #opensuse-422
[fedora]: #fedora
[arch]: #arch-linux
[lai]: #linux-appimage
[tar]: #binary-archives

## <a name="installing-preview-releases"></a><span data-ttu-id="10961-107">Előzetes kiadások telepítése</span><span class="sxs-lookup"><span data-stu-id="10961-107">Installing Preview Releases</span></span>

<span data-ttu-id="10961-108">PowerShell Core előzetes kiadás egy csomag tárház keresztül Linux telepítésekor a csomag nevét a változik `powershell` való `powershell-preview`.</span><span class="sxs-lookup"><span data-stu-id="10961-108">When installing a PowerShell Core Preview release for Linux via a Package Repository, the package name changes from `powershell` to `powershell-preview`.</span></span>

<span data-ttu-id="10961-109">Közvetlen letöltési keresztül telepítése nem változik, a fájl neve eltérő.</span><span class="sxs-lookup"><span data-stu-id="10961-109">Installing via direct download does not change, other than the file name.</span></span>

<span data-ttu-id="10961-110">Íme egy tábla a parancsok a különböző csomag-kezelők használatával stabil és preview-csomagok:</span><span class="sxs-lookup"><span data-stu-id="10961-110">Here is a table of the commands to install the stable and preview packages using the various package managers:</span></span>

|<span data-ttu-id="10961-111">Distrobution(s)</span><span class="sxs-lookup"><span data-stu-id="10961-111">Distrobution(s)</span></span>|<span data-ttu-id="10961-112">Stabil parancs</span><span class="sxs-lookup"><span data-stu-id="10961-112">Stable Command</span></span> | <span data-ttu-id="10961-113">Előzetes parancs</span><span class="sxs-lookup"><span data-stu-id="10961-113">Preview Command</span></span> |
|---------------|---------------|-----------------|
| <span data-ttu-id="10961-114">Ubuntu, Debian</span><span class="sxs-lookup"><span data-stu-id="10961-114">Ubuntu, Debian</span></span> |`sudo apt-get install -y powershell`| `sudo apt-get install -y powershell-preview`|
| <span data-ttu-id="10961-115">CentOS, RedHat</span><span class="sxs-lookup"><span data-stu-id="10961-115">CentOS, RedHat</span></span> |`sudo yum install -y powershell` | `sudo yum install -y powershell-preview`|
| <span data-ttu-id="10961-116">openSUSE</span><span class="sxs-lookup"><span data-stu-id="10961-116">OpenSUSE</span></span> |`sudo zypper install powershell` | `sudo zypper install powershell-preview`|
| <span data-ttu-id="10961-117">Fedora</span><span class="sxs-lookup"><span data-stu-id="10961-117">Fedora</span></span>   |`sudo dnf install -y powershell` | `sudo dnf install -y powershell-preview`|

## <a name="ubuntu-1404"></a><span data-ttu-id="10961-118">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="10961-118">Ubuntu 14.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1404"></a><span data-ttu-id="10961-119">Telepítési csomag tárház - Ubuntu 14.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="10961-119">Installation via Package Repository - Ubuntu 14.04</span></span>

<span data-ttu-id="10961-120">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="10961-120">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="10961-121">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="10961-121">This is the preferred method.</span></span>

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

<span data-ttu-id="10961-122">Felügyelő, mint a Microsoft-tárház regisztrálni.</span><span class="sxs-lookup"><span data-stu-id="10961-122">As superuser, register the Microsoft repository.</span></span>
<span data-ttu-id="10961-123">Ettől kezdve csak kell használnia `sudo apt-get upgrade powershell` a telepítés frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="10961-123">From then on, you just need to use `sudo apt-get upgrade powershell` to update the installation.</span></span>

### <a name="installation-via-direct-download---ubuntu-1404"></a><span data-ttu-id="10961-124">Közvetlen letöltése – Ubuntu 14.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="10961-124">Installation via Direct Download - Ubuntu 14.04</span></span>

<span data-ttu-id="10961-125">A Debian csomag `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="10961-125">Download the Debian package `powershell_6.0.2-1.ubuntu.14.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="10961-126">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="10961-126">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.14.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="10961-127">A `dpkg -i` unmet függőségekkel rendelkező parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="10961-127">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="10961-128">A következő parancs `apt-get install -f` megoldja a problémát, majd a PowerShell-csomag konfigurálása befejeződik.</span><span class="sxs-lookup"><span data-stu-id="10961-128">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1404"></a><span data-ttu-id="10961-129">Az Eltávolítás - Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="10961-129">Uninstallation - Ubuntu 14.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1604"></a><span data-ttu-id="10961-130">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="10961-130">Ubuntu 16.04</span></span>

### <a name="installation-via-package-repository---ubuntu-1604"></a><span data-ttu-id="10961-131">Telepítési csomag tárház - Ubuntu 16.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="10961-131">Installation via Package Repository - Ubuntu 16.04</span></span>

<span data-ttu-id="10961-132">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="10961-132">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="10961-133">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="10961-133">This is the preferred method.</span></span>

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

<span data-ttu-id="10961-134">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="10961-134">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1604"></a><span data-ttu-id="10961-135">Közvetlen letöltése – Ubuntu 16.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="10961-135">Installation via Direct Download - Ubuntu 16.04</span></span>

<span data-ttu-id="10961-136">A Debian csomag `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="10961-136">Download the Debian package `powershell_6.0.2-1.ubuntu.16.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="10961-137">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="10961-137">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.16.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="10961-138">A `dpkg -i` unmet függőségekkel rendelkező parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="10961-138">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="10961-139">A következő parancs `apt-get install -f` megoldja a problémát, majd a PowerShell-csomag konfigurálása befejeződik.</span><span class="sxs-lookup"><span data-stu-id="10961-139">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1604"></a><span data-ttu-id="10961-140">Az Eltávolítás - Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="10961-140">Uninstallation - Ubuntu 16.04</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1710"></a><span data-ttu-id="10961-141">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="10961-141">Ubuntu 17.10</span></span>

> [!NOTE]
> <span data-ttu-id="10961-142">Ubuntu 17.04 támogatása után lett hozzáadva. `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="10961-142">Support for Ubuntu 17.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1710"></a><span data-ttu-id="10961-143">Telepítési csomag tárház - Ubuntu 17.10 keresztül</span><span class="sxs-lookup"><span data-stu-id="10961-143">Installation via Package Repository - Ubuntu 17.10</span></span>

<span data-ttu-id="10961-144">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="10961-144">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="10961-145">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="10961-145">This is the preferred method.</span></span>

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

<span data-ttu-id="10961-146">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="10961-146">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1710"></a><span data-ttu-id="10961-147">Közvetlen letöltése – Ubuntu 17.10 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="10961-147">Installation via Direct Download - Ubuntu 17.10</span></span>

<span data-ttu-id="10961-148">A Debian csomag `powershell_6.0.2-1.ubuntu.17.10_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="10961-148">Download the Debian package `powershell_6.0.2-1.ubuntu.17.10_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="10961-149">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="10961-149">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.ubuntu.17.10_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="10961-150">A `dpkg -i` unmet függőségekkel rendelkező parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="10961-150">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="10961-151">A következő parancs `apt-get install -f` megoldja a problémát, majd a PowerShell-csomag konfigurálása befejeződik.</span><span class="sxs-lookup"><span data-stu-id="10961-151">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1710"></a><span data-ttu-id="10961-152">Az Eltávolítás - Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="10961-152">Uninstallation - Ubuntu 17.10</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="ubuntu-1804"></a><span data-ttu-id="10961-153">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="10961-153">Ubuntu 18.04</span></span>

> [!NOTE]
> <span data-ttu-id="10961-154">Ubuntu 18.04 támogatása után lett hozzáadva. `6.1.0-preview.2`</span><span class="sxs-lookup"><span data-stu-id="10961-154">Support for Ubuntu 18.04 was added after `6.1.0-preview.2`</span></span>

### <a name="installation-via-package-repository---ubuntu-1804"></a><span data-ttu-id="10961-155">Telepítési csomag tárház - Ubuntu 18.04 keresztül</span><span class="sxs-lookup"><span data-stu-id="10961-155">Installation via Package Repository - Ubuntu 18.04</span></span>

<span data-ttu-id="10961-156">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="10961-156">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="10961-157">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="10961-157">This is the preferred method.</span></span>

```sh
# Import the public repository GPG keys
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Register the Microsoft Ubuntu repository
sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list

# Update the list of products
sudo apt-get update

# Install PowerShell
sudo apt-get install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="10961-158">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="10961-158">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---ubuntu-1804"></a><span data-ttu-id="10961-159">Közvetlen letöltése – Ubuntu 18.04 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="10961-159">Installation via Direct Download - Ubuntu 18.04</span></span>

<span data-ttu-id="10961-160">A Debian csomag `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` a a [kiadott][] lap települ az Ubuntu gépre.</span><span class="sxs-lookup"><span data-stu-id="10961-160">Download the Debian package `powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb` from the [releases][] page onto the Ubuntu machine.</span></span>

<span data-ttu-id="10961-161">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="10961-161">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.1.0-preview.3-1.ubuntu.18.04_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="10961-162">A `dpkg -i` unmet függőségekkel rendelkező parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="10961-162">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="10961-163">A következő parancs `apt-get install -f` megoldja a problémát, majd a PowerShell-csomag konfigurálása befejeződik.</span><span class="sxs-lookup"><span data-stu-id="10961-163">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---ubuntu-1710"></a><span data-ttu-id="10961-164">Az Eltávolítás - Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="10961-164">Uninstallation - Ubuntu 17.10</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-8"></a><span data-ttu-id="10961-165">Debian 8</span><span class="sxs-lookup"><span data-stu-id="10961-165">Debian 8</span></span>

### <a name="installation-via-package-repository---debian-8"></a><span data-ttu-id="10961-166">Telepítési csomag tárház - Debian 8 keresztül</span><span class="sxs-lookup"><span data-stu-id="10961-166">Installation via Package Repository - Debian 8</span></span>

<span data-ttu-id="10961-167">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="10961-167">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="10961-168">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="10961-168">This is the preferred method.</span></span>

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

<span data-ttu-id="10961-169">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="10961-169">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-8"></a><span data-ttu-id="10961-170">Keresztül közvetlen letöltése – Debian 8 telepítése</span><span class="sxs-lookup"><span data-stu-id="10961-170">Installation via Direct Download - Debian 8</span></span>

<span data-ttu-id="10961-171">A Debian csomag `powershell_6.0.2-1.debian.8_amd64.deb` a a [kiadott][] a Debian gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="10961-171">Download the Debian package `powershell_6.0.2-1.debian.8_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="10961-172">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="10961-172">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.8_amd64.deb
sudo apt-get install -f
```

> [!NOTE]
> <span data-ttu-id="10961-173">A `dpkg -i` unmet függőségekkel rendelkező parancs meghiúsul.</span><span class="sxs-lookup"><span data-stu-id="10961-173">The `dpkg -i` command fails with unmet dependencies.</span></span>
> <span data-ttu-id="10961-174">A következő parancs `apt-get install -f` megoldja a problémát, majd a PowerShell-csomag konfigurálása befejeződik.</span><span class="sxs-lookup"><span data-stu-id="10961-174">The next command, `apt-get install -f` resolves these issues then finishes configuring the PowerShell package.</span></span>

### <a name="uninstallation---debian-8"></a><span data-ttu-id="10961-175">Az Eltávolítás - Debian 8</span><span class="sxs-lookup"><span data-stu-id="10961-175">Uninstallation - Debian 8</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="debian-9"></a><span data-ttu-id="10961-176">Debian 9</span><span class="sxs-lookup"><span data-stu-id="10961-176">Debian 9</span></span>

### <a name="installation-via-package-repository---debian-9"></a><span data-ttu-id="10961-177">Telepítési csomag tárház – Debian 9 keresztül</span><span class="sxs-lookup"><span data-stu-id="10961-177">Installation via Package Repository - Debian 9</span></span>

<span data-ttu-id="10961-178">PowerShell-Core, Linux, közzétett csomag tárolóhelyekkel egyszerű telepítés (és a frissítések).</span><span class="sxs-lookup"><span data-stu-id="10961-178">PowerShell Core, for Linux, is published to package repositories for easy installation (and updates).</span></span>
<span data-ttu-id="10961-179">Ez az elsődleges módszer.</span><span class="sxs-lookup"><span data-stu-id="10961-179">This is the preferred method.</span></span>

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

<span data-ttu-id="10961-180">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ettől ugyanúgy kell használnia `sudo apt-get upgrade powershell` frissíti.</span><span class="sxs-lookup"><span data-stu-id="10961-180">After registering the Microsoft repository once as superuser, from then on, you just need to use `sudo apt-get upgrade powershell` to update it.</span></span>

### <a name="installation-via-direct-download---debian-9"></a><span data-ttu-id="10961-181">Közvetlen letöltése – Debian 9 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="10961-181">Installation via Direct Download - Debian 9</span></span>

<span data-ttu-id="10961-182">A Debian csomag `powershell_6.0.2-1.debian.9_amd64.deb` a a [kiadott][] a Debian gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="10961-182">Download the Debian package `powershell_6.0.2-1.debian.9_amd64.deb` from the [releases][] page onto the Debian machine.</span></span>

<span data-ttu-id="10961-183">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="10961-183">Then execute the following in the terminal:</span></span>

```sh
sudo dpkg -i powershell_6.0.2-1.debian.9_amd64.deb
sudo apt-get install -f
```

### <a name="uninstallation---debian-9"></a><span data-ttu-id="10961-184">Az Eltávolítás - Debian 9</span><span class="sxs-lookup"><span data-stu-id="10961-184">Uninstallation - Debian 9</span></span>

```sh
sudo apt-get remove powershell
```

## <a name="centos-7"></a><span data-ttu-id="10961-185">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="10961-185">CentOS 7</span></span>

> [!NOTE]
> <span data-ttu-id="10961-186">Ez a csomag is működik-e az Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="10961-186">This package also works on Oracle Linux 7.</span></span>

### <a name="installation-via-package-repository-preferred---centos-7"></a><span data-ttu-id="10961-187">Telepítési csomag tárház (ajánlott) – CentOS 7 keresztül</span><span class="sxs-lookup"><span data-stu-id="10961-187">Installation via Package Repository (preferred) - CentOS 7</span></span>

<span data-ttu-id="10961-188">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="10961-188">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="10961-189">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="10961-189">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---centos-7"></a><span data-ttu-id="10961-190">Közvetlen letöltése – CentOS 7 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="10961-190">Installation via Direct Download - CentOS 7</span></span>

<span data-ttu-id="10961-191">Használatával [CentOS 7][], a RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a CentOS gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="10961-191">Using [CentOS 7][], download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the CentOS machine.</span></span>

<span data-ttu-id="10961-192">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="10961-192">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="10961-193">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="10961-193">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---centos-7"></a><span data-ttu-id="10961-194">Az Eltávolítás - CentOS 7</span><span class="sxs-lookup"><span data-stu-id="10961-194">Uninstallation - CentOS 7</span></span>

```sh
sudo yum remove powershell
```

[CentOS 7]: https://www.centos.org/download/

## <a name="red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="10961-196">Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="10961-196">Red Hat Enterprise Linux (RHEL) 7</span></span>

### <a name="installation-via-package-repository-preferred---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="10961-197">Telepítési csomag tárház (ajánlott) - Red Hat Enterprise Linux (RHEL) 7 keresztül</span><span class="sxs-lookup"><span data-stu-id="10961-197">Installation via Package Repository (preferred) - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="10961-198">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="10961-198">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

```sh
# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft.repo

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
pwsh
```

<span data-ttu-id="10961-199">A Microsoft-tárház a felügyelő, egyszer regisztrálás után ugyanúgy kell használnia `sudo yum update powershell` PowerShell frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="10961-199">After registering the Microsoft repository once as superuser, you just need to use `sudo yum update powershell` to update PowerShell.</span></span>

### <a name="installation-via-direct-download---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="10961-200">Közvetlen letöltése – Red Hat Enterprise Linux (RHEL) 7 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="10961-200">Installation via Direct Download - Red Hat Enterprise Linux (RHEL) 7</span></span>

<span data-ttu-id="10961-201">A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a Red Hat Enterprise Linux-gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="10961-201">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Red Hat Enterprise Linux machine.</span></span>

<span data-ttu-id="10961-202">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="10961-202">Then execute the following in the terminal:</span></span>

```sh
sudo yum install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="10961-203">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="10961-203">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo yum install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---red-hat-enterprise-linux-rhel-7"></a><span data-ttu-id="10961-204">Az Eltávolítás - Red Hat Enterprise Linux (RHEL) 7</span><span class="sxs-lookup"><span data-stu-id="10961-204">Uninstallation - Red Hat Enterprise Linux (RHEL) 7</span></span>

```sh
sudo yum remove powershell
```

## <a name="opensuse-422"></a><span data-ttu-id="10961-205">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="10961-205">OpenSUSE 42.2</span></span>

<span data-ttu-id="10961-206">PowerShell központ telepítésekor `zypper` előfordulhat, hogy a következő hiba jelentését:</span><span class="sxs-lookup"><span data-stu-id="10961-206">When installing PowerShell Core, `zypper` may report the following error:</span></span>

```Output
Problem: nothing provides libcurl needed by powershell-6.0.1-1.rhel.7.x86_64
 Solution 1: do not install powershell-6.0.1-1.rhel.7.x86_64
 Solution 2: break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies
```

<span data-ttu-id="10961-207">Ebben az esetben ellenőrizze, hogy a kompatibilis `libcurl` könyvtár megtalálható úgy, hogy a következő parancsot a jeleníti meg a `libcurl4` csomag telepítve:</span><span class="sxs-lookup"><span data-stu-id="10961-207">In this case, verify that a compatible `libcurl` library is present by checking that the following command shows the `libcurl4` package as installed:</span></span>

```sh
zypper search --file-list --match-exact '/usr/lib64/libcurl.so.4'
```

<span data-ttu-id="10961-208">Válassza ki a `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` megoldás a PowerShell csomag telepítésekor.</span><span class="sxs-lookup"><span data-stu-id="10961-208">Then choose the `break powershell-6.0.1-1.rhel.7.x86_64 by ignoring some of its dependencies` solution when installing the PowerShell package.</span></span>

### <a name="installation-via-package-repository-preferred---opensuse-422"></a><span data-ttu-id="10961-209">Telepítési csomag tárház (ajánlott) - OpenSUSE 42.2 keresztül</span><span class="sxs-lookup"><span data-stu-id="10961-209">Installation via Package Repository (preferred) - OpenSUSE 42.2</span></span>

<span data-ttu-id="10961-210">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="10961-210">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---opensuse-422"></a><span data-ttu-id="10961-211">Közvetlen letöltése – OpenSUSE 42.2 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="10961-211">Installation via Direct Download - OpenSUSE 42.2</span></span>

<span data-ttu-id="10961-212">A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a OpenSUSE gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="10961-212">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the OpenSUSE machine.</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="10961-213">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="10961-213">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo zypper install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---opensuse-422"></a><span data-ttu-id="10961-214">Az Eltávolítás - OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="10961-214">Uninstallation - OpenSUSE 42.2</span></span>

```sh
sudo zypper remove powershell
```

## <a name="fedora"></a><span data-ttu-id="10961-215">Fedora</span><span class="sxs-lookup"><span data-stu-id="10961-215">Fedora</span></span>

> [!NOTE]
> <span data-ttu-id="10961-216">Fedora 28 csak akkor támogatott, a PowerShell Core 6.1 vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="10961-216">Fedora 28 is only supported in PowerShell Core 6.1 and newer.</span></span>

### <a name="installation-via-package-repository-preferred---fedora-27-fedora-28"></a><span data-ttu-id="10961-217">Telepítési csomag tárház (ajánlott) - Fedora 27 Fedora 28 keresztül</span><span class="sxs-lookup"><span data-stu-id="10961-217">Installation via Package Repository (preferred) - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="10961-218">Egyszerű telepítés (és a frissítések) hivatalos Microsoft tárolóhelyekkel PowerShell Core Linux van közzétéve.</span><span class="sxs-lookup"><span data-stu-id="10961-218">PowerShell Core for Linux is published to official Microsoft repositories for easy installation (and updates).</span></span>

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

### <a name="installation-via-direct-download---fedora-27-fedora-28"></a><span data-ttu-id="10961-219">Közvetlen letöltése – Fedora 27, Fedora 28 történő telepítést</span><span class="sxs-lookup"><span data-stu-id="10961-219">Installation via Direct Download - Fedora 27, Fedora 28</span></span>

<span data-ttu-id="10961-220">A RPM csomag `powershell-6.0.2-1.rhel.7.x86_64.rpm` a a [kiadott][] a Fedora gép oldalon.</span><span class="sxs-lookup"><span data-stu-id="10961-220">Download the RPM package `powershell-6.0.2-1.rhel.7.x86_64.rpm` from the [releases][] page onto the Fedora machine.</span></span>

<span data-ttu-id="10961-221">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="10961-221">Then execute the following in the terminal:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install powershell-6.0.2-1.rhel.7.x86_64.rpm
```

<span data-ttu-id="10961-222">A RPM nélkül letölti a köztes lépés is telepíthet:</span><span class="sxs-lookup"><span data-stu-id="10961-222">You can also install the RPM without the intermediate step of downloading it:</span></span>

```sh
sudo dnf install compat-openssl10
sudo dnf install https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-1.rhel.7.x86_64.rpm
```

### <a name="uninstallation---fedora-27-fedora-28"></a><span data-ttu-id="10961-223">Az Eltávolítás - Fedora 27, Fedora 28</span><span class="sxs-lookup"><span data-stu-id="10961-223">Uninstallation - Fedora 27, Fedora 28</span></span>

```sh
sudo dnf remove powershell
```

## <a name="arch-linux"></a><span data-ttu-id="10961-224">Linux architektúrája</span><span class="sxs-lookup"><span data-stu-id="10961-224">Arch Linux</span></span>

> [!NOTE]
> <span data-ttu-id="10961-225">Emelőkaros funkció kísérleti.</span><span class="sxs-lookup"><span data-stu-id="10961-225">Arch support is experimental.</span></span>

<span data-ttu-id="10961-226">PowerShell érhető el a [architektúrája Linux][] felhasználói tárház (AUR).</span><span class="sxs-lookup"><span data-stu-id="10961-226">PowerShell is available from the [Arch Linux][] User Repository (AUR).</span></span>

* <span data-ttu-id="10961-227">Az összeállítható a [legújabb címkézett kiadás][arch-release]</span><span class="sxs-lookup"><span data-stu-id="10961-227">It can be compiled with the [latest tagged release][arch-release]</span></span>
* <span data-ttu-id="10961-228">Az összeállítható a [fő legújabb véglegesítési][arch-git]</span><span class="sxs-lookup"><span data-stu-id="10961-228">It can be compiled from the [latest commit to master][arch-git]</span></span>
* <span data-ttu-id="10961-229">Használatával telepíthető a [bináris legújabb kiadás][arch-bin]</span><span class="sxs-lookup"><span data-stu-id="10961-229">It can be installed using the [latest release binary][arch-bin]</span></span>

<span data-ttu-id="10961-230">A AUR csomagok karbantartása közösségi – nincs hivatalos támogatás.</span><span class="sxs-lookup"><span data-stu-id="10961-230">Packages in the AUR are community maintained - there is no official support.</span></span>

<span data-ttu-id="10961-231">A csomagok telepítése a AUR a további információkért lásd: a [architektúrája Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) vagy a közösségi [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span><span class="sxs-lookup"><span data-stu-id="10961-231">For more information on installing packages from the AUR, see the [Arch Linux wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_packages) or the community [DockerFile](https://github.com/PowerShell/PowerShell/blob/master/docker/community/archlinux/Dockerfile).</span></span>

[architektúrája Linux]: https://www.archlinux.org/download/
[Arch Linux]: https://www.archlinux.org/download/
[arch-release]: https://aur.archlinux.org/packages/powershell/
[arch-git]: https://aur.archlinux.org/packages/powershell-git/
[arch-bin]: https://aur.archlinux.org/packages/powershell-bin/

## <a name="linux-appimage"></a><span data-ttu-id="10961-233">Linux AppImage</span><span class="sxs-lookup"><span data-stu-id="10961-233">Linux AppImage</span></span>

> [!NOTE]
> <span data-ttu-id="10961-234">AppImage funkció kísérleti</span><span class="sxs-lookup"><span data-stu-id="10961-234">AppImage support is experimental</span></span>

<span data-ttu-id="10961-235">A legutóbbi Linux-eloszlás használatával töltse le a AppImage `powershell-6.0.1-x86_64.AppImage` a a [kiadott][] a Linux-gépek oldalon.</span><span class="sxs-lookup"><span data-stu-id="10961-235">Using a recent Linux distribution, download the AppImage `powershell-6.0.1-x86_64.AppImage` from the [releases][] page onto the Linux machine.</span></span>

<span data-ttu-id="10961-236">A terminálban majd hajtsa végre az alábbiakat:</span><span class="sxs-lookup"><span data-stu-id="10961-236">Then execute the following in the terminal:</span></span>

```bash
chmod a+x powershell-6.0.1-x86_64.AppImage
./powershell-6.0.1-x86_64.AppImage
```

<span data-ttu-id="10961-237">A [AppImage][] lehetővé teszi, hogy a telepítés nélküli PowerShell futtatásához.</span><span class="sxs-lookup"><span data-stu-id="10961-237">The [AppImage][] lets you run PowerShell without installing it.</span></span>
<span data-ttu-id="10961-238">Egy hordozható alkalmazás, amely a PowerShell és a függőségek (beleértve a .NET Core rendszer függőségeket) bundles egy javul csomagba.</span><span class="sxs-lookup"><span data-stu-id="10961-238">It is a portable application that bundles PowerShell and its dependencies (including .NET Core's system dependencies) into one cohesive package.</span></span>
<span data-ttu-id="10961-239">Ez a csomag, amely a felhasználó a Linux-disztribúció függetlenül működik egy bináris.</span><span class="sxs-lookup"><span data-stu-id="10961-239">This package  is a single binary that works independently of the user's Linux distribution.</span></span>

[appimage]: http://appimage.org/

## <a name="kali"></a><span data-ttu-id="10961-241">Kali</span><span class="sxs-lookup"><span data-stu-id="10961-241">Kali</span></span>

> [!NOTE]
> <span data-ttu-id="10961-242">Kali funkció kísérleti.</span><span class="sxs-lookup"><span data-stu-id="10961-242">Kali support is experimental.</span></span>

### <a name="installation"></a><span data-ttu-id="10961-243">Telepítés</span><span class="sxs-lookup"><span data-stu-id="10961-243">Installation</span></span>

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

### <a name="run-powershell-in-latest-kali-kali-gnulinux-rolling-without-installing-it"></a><span data-ttu-id="10961-244">Futtassa a PowerShell legújabb Kali (Kali GNU/Linux folyamatos) a telepítés nélküli</span><span class="sxs-lookup"><span data-stu-id="10961-244">Run PowerShell in latest Kali (Kali GNU/Linux Rolling) without installing it</span></span>

```sh
# Grab the latest App Image
wget https://github.com/PowerShell/PowerShell/releases/download/v6.0.2/powershell-6.0.2-x86_64.AppImage

# Make executable
chmod a+x powershell-6.0.2-x86_64.AppImage

# Start PowerShell
./powershell-6.0.2-x86_64.AppImage
```

### <a name="uninstallation---kali"></a><span data-ttu-id="10961-245">Az Eltávolítás - Kali</span><span class="sxs-lookup"><span data-stu-id="10961-245">Uninstallation - Kali</span></span>

```sh
sudo dpkg -r powershell_6.0.2-1.ubuntu.16.04_amd64.deb
```

## <a name="raspbian"></a><span data-ttu-id="10961-246">Raspbian</span><span class="sxs-lookup"><span data-stu-id="10961-246">Raspbian</span></span>

> [!NOTE]
> <span data-ttu-id="10961-247">Raspbian funkció kísérleti.</span><span class="sxs-lookup"><span data-stu-id="10961-247">Raspbian support is experimental.</span></span>

<span data-ttu-id="10961-248">PowerShell jelenleg csak Raspbian Stretch támogatott.</span><span class="sxs-lookup"><span data-stu-id="10961-248">Currently, PowerShell is only supported on Raspbian Stretch.</span></span>

<span data-ttu-id="10961-249">Is CoreCLR (és így PowerShell Core) csak Pi 2 és Pi 3 eszközökön módon fog más eszközök, például [Pi nulla](https://github.com/dotnet/coreclr/issues/10605), egy nem támogatott processzorral rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="10961-249">Also CoreCLR (and thus PowerShell Core) will only work on Pi 2 and Pi 3 devices as other devices, like [Pi Zero](https://github.com/dotnet/coreclr/issues/10605), have an unsupported processor.</span></span>

<span data-ttu-id="10961-250">Töltse le [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) , és kövesse a [telepítési utasításokat](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) a Pi eléréséhez.</span><span class="sxs-lookup"><span data-stu-id="10961-250">Download [Raspbian Stretch](https://www.raspberrypi.org/downloads/raspbian/) and follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to get it onto your Pi.</span></span>

### <a name="installation"></a><span data-ttu-id="10961-251">Telepítés</span><span class="sxs-lookup"><span data-stu-id="10961-251">Installation</span></span>

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

<span data-ttu-id="10961-252">Nem kötelező elérési út megadását a "pwsh" bináris nélkül indítsa el a Powershellt szeretné szimbolikus hivatkozást hozhat létre</span><span class="sxs-lookup"><span data-stu-id="10961-252">Optionally you can create a symbolic link to be able to start PowerShell without specifying path to the "pwsh" binary</span></span>

```sh
# Start PowerShell from bash with sudo to create a symbolic link
sudo ~/powershell/pwsh -c New-Item -ItemType SymbolicLink -Path "/usr/bin/pwsh" -Target "\$PSHOME/pwsh" -Force

# alternatively you can run following to create a symbolic link
# sudo ln -s ~/powershell/pwsh /usr/bin/pwsh

# Now to start PowerShell you can just run "pwsh"
```

### <a name="uninstallation---raspbian"></a><span data-ttu-id="10961-253">Az Eltávolítás - Raspbian</span><span class="sxs-lookup"><span data-stu-id="10961-253">Uninstallation - Raspbian</span></span>

```sh
rm -rf ~/powershell
```

## <a name="binary-archives"></a><span data-ttu-id="10961-254">Bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="10961-254">Binary Archives</span></span>

<span data-ttu-id="10961-255">PowerShell bináris `tar.gz` archívumokat biztosított Linux-platformokhoz lehetővé központi telepítési forgatókönyveket.</span><span class="sxs-lookup"><span data-stu-id="10961-255">PowerShell binary `tar.gz` archives are provided for Linux platforms to enable advanced deployment scenarios.</span></span>

### <a name="dependencies"></a><span data-ttu-id="10961-256">Függőségek</span><span class="sxs-lookup"><span data-stu-id="10961-256">Dependencies</span></span>

<span data-ttu-id="10961-257">PowerShell alkot az összes Linux terjesztésekről hordozható bináris fájljait.</span><span class="sxs-lookup"><span data-stu-id="10961-257">PowerShell builds portable binaries for all Linux distributions.</span></span>
<span data-ttu-id="10961-258">De a .NET Core runtime szükséges a különböző terjesztések átviteli különböző függőségek, és ezért PowerShell szerepe ugyanaz.</span><span class="sxs-lookup"><span data-stu-id="10961-258">But .NET Core runtime requires different dependencies on different distributions, and hence PowerShell does the same.</span></span>

<span data-ttu-id="10961-259">Az alábbi ábra mutatja a .NET Core 2.0 függőségek hivatalosan által támogatott különböző Linux terjesztéseket.</span><span class="sxs-lookup"><span data-stu-id="10961-259">The following chart shows the .NET Core 2.0 dependencies that are officially supported on different Linux distributions.</span></span>

| <span data-ttu-id="10961-260">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="10961-260">OS</span></span>                 | <span data-ttu-id="10961-261">Függőségek</span><span class="sxs-lookup"><span data-stu-id="10961-261">Dependencies</span></span> |
| ------------------ | ------------ |
| <span data-ttu-id="10961-262">Ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="10961-262">Ubuntu 14.04</span></span>       | <span data-ttu-id="10961-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="10961-263">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="10961-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="10961-264">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="10961-265">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="10961-265">Ubuntu 16.04</span></span>       | <span data-ttu-id="10961-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="10961-266">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="10961-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span><span class="sxs-lookup"><span data-stu-id="10961-267">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu55</span></span> |
| <span data-ttu-id="10961-268">Ubuntu 17.10</span><span class="sxs-lookup"><span data-stu-id="10961-268">Ubuntu 17.10</span></span>       | <span data-ttu-id="10961-269">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="10961-269">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="10961-270">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span><span class="sxs-lookup"><span data-stu-id="10961-270">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu57</span></span> |
| <span data-ttu-id="10961-271">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="10961-271">Ubuntu 18.04</span></span>       | <span data-ttu-id="10961-272">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="10961-272">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="10961-273">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span><span class="sxs-lookup"><span data-stu-id="10961-273">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu60</span></span> |
| <span data-ttu-id="10961-274">Debian 8 (Jessie)</span><span class="sxs-lookup"><span data-stu-id="10961-274">Debian 8 (Jessie)</span></span>  | <span data-ttu-id="10961-275">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="10961-275">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="10961-276">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span><span class="sxs-lookup"><span data-stu-id="10961-276">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.0, libicu52</span></span> |
| <span data-ttu-id="10961-277">Debian 9 (Stretch)</span><span class="sxs-lookup"><span data-stu-id="10961-277">Debian 9 (Stretch)</span></span> | <span data-ttu-id="10961-278">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span><span class="sxs-lookup"><span data-stu-id="10961-278">libc6, libgcc1, libgssapi-krb5-2, liblttng-ust0, libstdc++6,</span></span> <br> <span data-ttu-id="10961-279">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span><span class="sxs-lookup"><span data-stu-id="10961-279">libcurl3, libunwind8, libuuid1, zlib1g, libssl1.0.2, libicu57</span></span> |
| <span data-ttu-id="10961-280">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="10961-280">CentOS 7</span></span> <br> <span data-ttu-id="10961-281">Oracle Linux 7</span><span class="sxs-lookup"><span data-stu-id="10961-281">Oracle Linux 7</span></span> <br> <span data-ttu-id="10961-282">RHEL 7</span><span class="sxs-lookup"><span data-stu-id="10961-282">RHEL 7</span></span> <br> <span data-ttu-id="10961-283">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="10961-283">OpenSUSE 42.2</span></span> | <span data-ttu-id="10961-284">libunwind, libcurl, openssl-függvénytárak, libicu</span><span class="sxs-lookup"><span data-stu-id="10961-284">libunwind, libcurl, openssl-libs, libicu</span></span> |
| <span data-ttu-id="10961-285">27 Fedora</span><span class="sxs-lookup"><span data-stu-id="10961-285">Fedora 27</span></span> <br> <span data-ttu-id="10961-286">28 Fedora</span><span class="sxs-lookup"><span data-stu-id="10961-286">Fedora 28</span></span> | <span data-ttu-id="10961-287">libunwind, libcurl, openssl-függvénytárak, libicu, / compat-openssl10</span><span class="sxs-lookup"><span data-stu-id="10961-287">libunwind, libcurl, openssl-libs, libicu, compat-openssl10</span></span> |

<span data-ttu-id="10961-288">Az telepítéséhez PowerShell bináris fájljait, a Linux terjesztéseket, amelyek hivatalosan nem támogatottak, kell telepíteni a cél operációs rendszer szükséges függőségek külön lépéseket.</span><span class="sxs-lookup"><span data-stu-id="10961-288">To deploy PowerShell binaries on Linux distributions that are not officially supported, you need to install the necessary dependencies for the target OS in separate steps.</span></span>
<span data-ttu-id="10961-289">Például a [Amazon Linux dockerfile] [ amazon-dockerfile] függőségek először telepíti, és kinyeri a Linux `tar.gz` archív.</span><span class="sxs-lookup"><span data-stu-id="10961-289">For example, our [Amazon Linux dockerfile][amazon-dockerfile] installs dependencies first, and then extracts the Linux `tar.gz` archive.</span></span>

[amazon-dockerfile]: https://github.com/PowerShell/PowerShell/blob/master/docker/community/amazonlinux/Dockerfile

### <a name="installation---binary-archives"></a><span data-ttu-id="10961-290">Telepítés – bináris archívumokat</span><span class="sxs-lookup"><span data-stu-id="10961-290">Installation - Binary Archives</span></span>

#### <a name="linux"></a><span data-ttu-id="10961-291">Linux</span><span class="sxs-lookup"><span data-stu-id="10961-291">Linux</span></span>

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

### <a name="uninstalling-binary-archives"></a><span data-ttu-id="10961-292">Bináris archívumokat eltávolítása</span><span class="sxs-lookup"><span data-stu-id="10961-292">Uninstalling binary archives</span></span>

```sh
sudo rm -rf /usr/bin/pwsh /opt/microsoft/powershell
```

## <a name="paths"></a><span data-ttu-id="10961-293">Elérési utak</span><span class="sxs-lookup"><span data-stu-id="10961-293">Paths</span></span>

* <span data-ttu-id="10961-294">`$PSHOME` van `/opt/microsoft/powershell/6.0.2/`</span><span class="sxs-lookup"><span data-stu-id="10961-294">`$PSHOME` is `/opt/microsoft/powershell/6.0.2/`</span></span>
* <span data-ttu-id="10961-295">Felhasználói profilok rendszer nem olvas be `~/.config/powershell/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="10961-295">User profiles will be read from `~/.config/powershell/profile.ps1`</span></span>
* <span data-ttu-id="10961-296">Alapértelmezett profilok rendszer nem olvas be `$PSHOME/profile.ps1`</span><span class="sxs-lookup"><span data-stu-id="10961-296">Default profiles will be read from `$PSHOME/profile.ps1`</span></span>
* <span data-ttu-id="10961-297">Modulok felhasználói rendszer nem olvas be `~/.local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="10961-297">User modules will be read from `~/.local/share/powershell/Modules`</span></span>
* <span data-ttu-id="10961-298">Megosztott modulok rendszer nem olvas be `/usr/local/share/powershell/Modules`</span><span class="sxs-lookup"><span data-stu-id="10961-298">Shared modules will be read from `/usr/local/share/powershell/Modules`</span></span>
* <span data-ttu-id="10961-299">Az alapértelmezett modulokat rendszer nem olvas be `$PSHOME/Modules`</span><span class="sxs-lookup"><span data-stu-id="10961-299">Default modules will be read from `$PSHOME/Modules`</span></span>
* <span data-ttu-id="10961-300">A rögzítendő PSReadline előzmények `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span><span class="sxs-lookup"><span data-stu-id="10961-300">PSReadline history will be recorded to `~/.local/share/powershell/PSReadLine/ConsoleHost_history.txt`</span></span>

<span data-ttu-id="10961-301">A profilok tiszteletben PowerShell gazdagép konfiguráció, így az alapértelmezett gazdagép-specifikus profilok létezik az `Microsoft.PowerShell_profile.ps1` ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="10961-301">The profiles respect PowerShell's per-host configuration, so the default host-specific profiles exists at `Microsoft.PowerShell_profile.ps1` in the same locations.</span></span>

<span data-ttu-id="10961-302">PowerShell tiszteletben tartja a [XDG Base könyvtár megadása] [ xdg-bds] Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="10961-302">PowerShell respects the [XDG Base Directory Specification][xdg-bds] on Linux.</span></span>

[kiadott]: https://github.com/PowerShell/PowerShell/releases/latest
[releases]: https://github.com/PowerShell/PowerShell/releases/latest
[xdg-bds]: https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html
