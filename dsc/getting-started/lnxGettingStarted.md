---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Ismerkedés a Desired State Configuration (DSC) rétegen a Linux rendszeren
ms.openlocfilehash: 69f087434455aae8e97ea07c79c52e493412d134
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686599"
---
# <a name="get-started-with-desired-state-configuration-dsc-for-linux"></a><span data-ttu-id="47dc0-103">Ismerkedés a Desired State Configuration (DSC) rétegen a Linux rendszeren</span><span class="sxs-lookup"><span data-stu-id="47dc0-103">Get started with Desired State Configuration (DSC) for Linux</span></span>

<span data-ttu-id="47dc0-104">Ez a témakör ismerteti, hogyan kezdheti el a PowerShell Desired State Configuration (DSC) használatával Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="47dc0-104">This topic explains how to get started using PowerShell Desired State Configuration (DSC) for Linux.</span></span> <span data-ttu-id="47dc0-105">DSC kapcsolatos általános információkért lásd: [Ismerkedés a Windows PowerShell Desired State Configuration](../overview/overview.md).</span><span class="sxs-lookup"><span data-stu-id="47dc0-105">For general information about DSC, see [Get Started with Windows PowerShell Desired State Configuration](../overview/overview.md).</span></span>

## <a name="supported-linux-operation-system-versions"></a><span data-ttu-id="47dc0-106">Támogatott Linux-művelet rendszerekről</span><span class="sxs-lookup"><span data-stu-id="47dc0-106">Supported Linux operation system versions</span></span>

<span data-ttu-id="47dc0-107">A következő Linux operációsrendszer-verziók Linuxhoz készült DSC támogatottak.</span><span class="sxs-lookup"><span data-stu-id="47dc0-107">The following Linux operating system versions are supported for DSC for Linux.</span></span>

- <span data-ttu-id="47dc0-108">CentOS 5, 6 és 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="47dc0-108">CentOS 5, 6, and 7 (x86/x64)</span></span>
- <span data-ttu-id="47dc0-109">Debian GNU/Linux 6, 7, 8 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="47dc0-109">Debian GNU/Linux 6, 7 and 8 (x86/x64)</span></span>
- <span data-ttu-id="47dc0-110">Oracle Linux 5, 6 és 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="47dc0-110">Oracle Linux 5, 6 and 7 (x86/x64)</span></span>
- <span data-ttu-id="47dc0-111">Red Hat Enterprise Linux Server 5, 6 és 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="47dc0-111">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
- <span data-ttu-id="47dc0-112">SUSE Linux Enterprise Server 10, 11, 12 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="47dc0-112">SUSE Linux Enterprise Server 10, 11 and 12 (x86/x64)</span></span>
- <span data-ttu-id="47dc0-113">Ubuntu Server 12.04 LTS, 14.04 LTS és 16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="47dc0-113">Ubuntu Server 12.04 LTS, 14.04 LTS and 16.04 LTS (x86/x64)</span></span>

<span data-ttu-id="47dc0-114">A következő táblázat ismerteti a szükséges csomag függőségeit a DSC Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="47dc0-114">The following table describes the required package dependencies for DSC for Linux.</span></span>

|  <span data-ttu-id="47dc0-115">Szükséges csomag</span><span class="sxs-lookup"><span data-stu-id="47dc0-115">Required package</span></span> |  <span data-ttu-id="47dc0-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="47dc0-116">Description</span></span> |  <span data-ttu-id="47dc0-117">Minimális verziója</span><span class="sxs-lookup"><span data-stu-id="47dc0-117">Minimum version</span></span> |
|---|---|---|
| <span data-ttu-id="47dc0-118">glibc</span><span class="sxs-lookup"><span data-stu-id="47dc0-118">glibc</span></span>| <span data-ttu-id="47dc0-119">GNU könyvtár</span><span class="sxs-lookup"><span data-stu-id="47dc0-119">GNU Library</span></span>| <span data-ttu-id="47dc0-120">2…4 – 31.30</span><span class="sxs-lookup"><span data-stu-id="47dc0-120">2…4 – 31.30</span></span>|
| <span data-ttu-id="47dc0-121">python</span><span class="sxs-lookup"><span data-stu-id="47dc0-121">python</span></span>| <span data-ttu-id="47dc0-122">Python</span><span class="sxs-lookup"><span data-stu-id="47dc0-122">Python</span></span>| <span data-ttu-id="47dc0-123">2.4 – 3.4</span><span class="sxs-lookup"><span data-stu-id="47dc0-123">2.4 – 3.4</span></span>|
| <span data-ttu-id="47dc0-124">omiserver</span><span class="sxs-lookup"><span data-stu-id="47dc0-124">omiserver</span></span>| <span data-ttu-id="47dc0-125">Nyílt kezelési infrastruktúra</span><span class="sxs-lookup"><span data-stu-id="47dc0-125">Open Management Infrastructure</span></span>| <span data-ttu-id="47dc0-126">1.0.8.1</span><span class="sxs-lookup"><span data-stu-id="47dc0-126">1.0.8.1</span></span>|
| <span data-ttu-id="47dc0-127">openssl</span><span class="sxs-lookup"><span data-stu-id="47dc0-127">openssl</span></span>| <span data-ttu-id="47dc0-128">OpenSSL-függvénytárak</span><span class="sxs-lookup"><span data-stu-id="47dc0-128">OpenSSL Libraries</span></span>| <span data-ttu-id="47dc0-129">0.9.8-as vagy 1.0</span><span class="sxs-lookup"><span data-stu-id="47dc0-129">0.9.8 or 1.0</span></span>|
| <span data-ttu-id="47dc0-130">ctypes</span><span class="sxs-lookup"><span data-stu-id="47dc0-130">ctypes</span></span>| <span data-ttu-id="47dc0-131">Python CTypes könyvtár</span><span class="sxs-lookup"><span data-stu-id="47dc0-131">Python CTypes library</span></span>| <span data-ttu-id="47dc0-132">Meg kell egyeznie a Python-verzió</span><span class="sxs-lookup"><span data-stu-id="47dc0-132">Must match Python version</span></span>|
| <span data-ttu-id="47dc0-133">libcurl</span><span class="sxs-lookup"><span data-stu-id="47dc0-133">libcurl</span></span>| <span data-ttu-id="47dc0-134">a cURL http-klienskódtár</span><span class="sxs-lookup"><span data-stu-id="47dc0-134">cURL http client library</span></span>| <span data-ttu-id="47dc0-135">7.15.1</span><span class="sxs-lookup"><span data-stu-id="47dc0-135">7.15.1</span></span>|

## <a name="installing-dsc-for-linux"></a><span data-ttu-id="47dc0-136">Linuxhoz készült DSC telepítése</span><span class="sxs-lookup"><span data-stu-id="47dc0-136">Installing DSC for Linux</span></span>

<span data-ttu-id="47dc0-137">Telepítenie kell a [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) Linuxhoz készült DSC telepítése előtt.</span><span class="sxs-lookup"><span data-stu-id="47dc0-137">You must install the [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) before installing DSC for Linux.</span></span>

### <a name="installing-omi"></a><span data-ttu-id="47dc0-138">OMI telepítése</span><span class="sxs-lookup"><span data-stu-id="47dc0-138">Installing OMI</span></span>

<span data-ttu-id="47dc0-139">Desired State Configuration for Linux számára az Open Management Infrastructure (OMI) CIM-kiszolgáló, 1.0.8.1 verzió vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="47dc0-139">Desired State Configuration for Linux requires the Open Management Infrastructure (OMI) CIM server, version 1.0.8.1 or later.</span></span> <span data-ttu-id="47dc0-140">OMI letölthető az Open Group: [Nyissa meg a Management Infrastructure (OMI)](https://github.com/Microsoft/omi).</span><span class="sxs-lookup"><span data-stu-id="47dc0-140">OMI can be downloaded from The Open Group: [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi).</span></span>

<span data-ttu-id="47dc0-141">OMI telepítéséhez telepítse a csomagot, amely megfelelő a Linux rendszer (.rpm vagy .deb) és az OpenSSL-verzió (ssl_098 vagy ssl_100) és az architektúra (x64/x86).</span><span class="sxs-lookup"><span data-stu-id="47dc0-141">To install OMI, install the package that is appropriate for your Linux system (.rpm or .deb) and OpenSSL version (ssl_098 or ssl_100), and architecture (x64/x86).</span></span> <span data-ttu-id="47dc0-142">RPM-csomagot a CentOS, a Red Hat Enterprise Linux, a SUSE Linux Enterprise Server és az Oracle Linux alkalmasak.</span><span class="sxs-lookup"><span data-stu-id="47dc0-142">RPM packages are appropriate for CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, and Oracle Linux.</span></span> <span data-ttu-id="47dc0-143">A Debian GNU/Linux és Ubuntu Server megfelelőek-DEB-csomag.</span><span class="sxs-lookup"><span data-stu-id="47dc0-143">DEB packages are appropriate for Debian GNU/Linux and Ubuntu Server.</span></span> <span data-ttu-id="47dc0-144">A ssl_098 csomagok megfelelők OpenSSL 0.9.8-as telepítve van, miközben telepítve OpenSSL 1.0 megfelelő számítógépek a ssl_100 csomagok számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="47dc0-144">The ssl_098 packages are appropriate for computers with OpenSSL 0.9.8 installed while the ssl_100 packages are appropriate for computers with OpenSSL 1.0 installed.</span></span>

> [!NOTE]
> <span data-ttu-id="47dc0-145">A telepített OpenSSL-verzió azonosításához futtassa a parancsot `openssl version`.</span><span class="sxs-lookup"><span data-stu-id="47dc0-145">To determine the installed OpenSSL version, run the command `openssl version`.</span></span>

<span data-ttu-id="47dc0-146">A következő paranccsal telepítse az OMI CentOS 7 x64 rendszerre.</span><span class="sxs-lookup"><span data-stu-id="47dc0-146">Run the following command to install OMI on a CentOS 7 x64 system.</span></span>

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### <a name="installing-dsc"></a><span data-ttu-id="47dc0-147">DSC telepítése</span><span class="sxs-lookup"><span data-stu-id="47dc0-147">Installing DSC</span></span>

<span data-ttu-id="47dc0-148">Linuxhoz készült DSC érhető el letöltésre [Itt](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/tag/v1.1.1-294).</span><span class="sxs-lookup"><span data-stu-id="47dc0-148">DSC for Linux is available for download [here](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/tag/v1.1.1-294).</span></span>

<span data-ttu-id="47dc0-149">DSC telepítéséhez telepítse a csomagot, amely megfelelő a Linux rendszer (.rpm vagy .deb) és az OpenSSL-verzió (ssl_098 vagy ssl_100) és az architektúra (x64/x86).</span><span class="sxs-lookup"><span data-stu-id="47dc0-149">To install DSC, install the package that is appropriate for your Linux system (.rpm or .deb) and OpenSSL version (ssl_098 or ssl_100), and architecture (x64/x86).</span></span> <span data-ttu-id="47dc0-150">RPM-csomagot a CentOS, a Red Hat Enterprise Linux, a SUSE Linux Enterprise Server és az Oracle Linux alkalmasak.</span><span class="sxs-lookup"><span data-stu-id="47dc0-150">RPM packages are appropriate for CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, and Oracle Linux.</span></span> <span data-ttu-id="47dc0-151">A Debian GNU/Linux és Ubuntu Server megfelelőek-DEB-csomag.</span><span class="sxs-lookup"><span data-stu-id="47dc0-151">DEB packages are appropriate for Debian GNU/Linux and Ubuntu Server.</span></span> <span data-ttu-id="47dc0-152">A ssl_098 csomagok megfelelők OpenSSL 0.9.8-as telepítve van, miközben telepítve OpenSSL 1.0 megfelelő számítógépek a ssl_100 csomagok számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="47dc0-152">The ssl_098 packages are appropriate for computers with OpenSSL 0.9.8 installed while the ssl_100 packages are appropriate for computers with OpenSSL 1.0 installed.</span></span>

> [!NOTE]
> <span data-ttu-id="47dc0-153">A telepített OpenSSL-verzió azonosításához futtassa a parancs openssl-verziót.</span><span class="sxs-lookup"><span data-stu-id="47dc0-153">To determine the installed OpenSSL version, run the command openssl version.</span></span>

<span data-ttu-id="47dc0-154">Futtassa a következő parancsot, DSC CentOS 7 x64 rendszer telepítése.</span><span class="sxs-lookup"><span data-stu-id="47dc0-154">Run the following command to install DSC on a CentOS 7 x64 system.</span></span>

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`

## <a name="using-dsc-for-linux"></a><span data-ttu-id="47dc0-155">Linuxhoz készült DSC használatával</span><span class="sxs-lookup"><span data-stu-id="47dc0-155">Using DSC for Linux</span></span>

<span data-ttu-id="47dc0-156">Az alábbi szakaszok azt ismertetik, hogyan hozhat létre és futtathat a DSC-konfigurációk Linux-számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="47dc0-156">The following sections explain how to create and run DSC configurations on Linux computers.</span></span>

### <a name="creating-a-configuration-mof-document"></a><span data-ttu-id="47dc0-157">A konfigurációs MOF-dokumentum létrehozása</span><span class="sxs-lookup"><span data-stu-id="47dc0-157">Creating a configuration MOF document</span></span>

<span data-ttu-id="47dc0-158">A Windows PowerShell a konfigurációs kulcsszó a Linux rendszerű számítógépek esetében konfiguráció létrehozásához csakúgy, mint a Windows-számítógépek esetében használatos.</span><span class="sxs-lookup"><span data-stu-id="47dc0-158">The Windows PowerShell Configuration keyword is used to create a configuration for Linux computers, just like for Windows computers.</span></span> <span data-ttu-id="47dc0-159">A következő lépések írják le a konfigurációs dokumentum egy Windows PowerShell használatával egy Linux-számítógép létrehozása.</span><span class="sxs-lookup"><span data-stu-id="47dc0-159">The following steps describe the creation of a configuration document for a Linux computer using Windows PowerShell.</span></span>

1. <span data-ttu-id="47dc0-160">Az nx modul importálásához.</span><span class="sxs-lookup"><span data-stu-id="47dc0-160">Import the nx module.</span></span> <span data-ttu-id="47dc0-161">Az nx Windows PowerShell-modul tartalmaz beépített erőforrások sémáját DSC Linux rendszeren, és telepítve legyen a helyi számítógépen, és importálja a konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="47dc0-161">The nx Windows PowerShell module contains the schema for Built-In resources for DSC for Linux, and must be installed to your local computer and imported in the configuration.</span></span>

   - <span data-ttu-id="47dc0-162">Nx-modul telepítéséhez, másolni vagy nx modulkönyvtárat `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` vagy `$PSHOME\Modules`.</span><span class="sxs-lookup"><span data-stu-id="47dc0-162">To install the nx module, copy the nx module directory to either `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` or `$PSHOME\Modules`.</span></span> <span data-ttu-id="47dc0-163">Az nx-modul a DSC Linux-telepítési csomag tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="47dc0-163">The nx module is included in the DSC for Linux installation package.</span></span> <span data-ttu-id="47dc0-164">A konfigurációban az nx modul importálásához használja a `Import-DSCResource` parancsot:</span><span class="sxs-lookup"><span data-stu-id="47dc0-164">To import the nx module in your configuration, use the `Import-DSCResource` command:</span></span>

   ```powershell
   Configuration ExampleConfiguration{

    Import-DSCResource -Module nx

   }
   ```

2. <span data-ttu-id="47dc0-165">A konfiguráció meghatározása és a konfigurációs dokumentum létrehozása:</span><span class="sxs-lookup"><span data-stu-id="47dc0-165">Define a configuration and generate the configuration document:</span></span>

   ```powershell
   Configuration ExampleConfiguration
   {
        Import-DscResource -Module nx

        Node  "linuxhost.contoso.com"
        {
            nxFile ExampleFile 
            {
                DestinationPath = "/tmp/example"
                Contents = "hello world `n"
                Ensure = "Present"
                Type = "File"
            }
        }
   }

   ExampleConfiguration -OutputPath:"C:\temp"
   ```

### <a name="push-the-configuration-to-the-linux-computer"></a><span data-ttu-id="47dc0-166">A konfiguráció leküldése a Linux-számítógép</span><span class="sxs-lookup"><span data-stu-id="47dc0-166">Push the configuration to the Linux computer</span></span>

<span data-ttu-id="47dc0-167">Konfigurációs dokumentumok (MOF-fájlok) a Linux rendszerű számítógépen történő lehet leküldeni a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="47dc0-167">Configuration documents (MOF files) can be pushed to the Linux computer using the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span> <span data-ttu-id="47dc0-168">Ez a parancsmag használatához az a [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration), vagy [a Test-DscConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration) parancsmagok távolról egy Linux rendszerű számítógépre kell használnia a CIMSession.</span><span class="sxs-lookup"><span data-stu-id="47dc0-168">In order to use this cmdlet, along with the [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration), or [Test-DscConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration) cmdlets, remotely to a Linux computer, you must use a CIMSession.</span></span> <span data-ttu-id="47dc0-169">A [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) parancsmag segítségével hozzon létre egy Linux rendszerű számítógép CIMSession.</span><span class="sxs-lookup"><span data-stu-id="47dc0-169">The [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) cmdlet is used to create a CIMSession to the Linux computer.</span></span>

<span data-ttu-id="47dc0-170">A következő kód bemutatja a DSC-CIMSession létrehozása Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="47dc0-170">The following code shows how to create a CIMSession for DSC for Linux.</span></span>

```powershell
$Node = "ostc-dsc-01"
$Credential = Get-Credential -UserName:"root" -Message:"Enter Password:"

#Ignore SSL certificate validation
#$opt = New-CimSessionOption -UseSsl:$true -SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true

#Options for a trusted SSL certificate
$opt = New-CimSessionOption -UseSsl:$true
$Sess=New-CimSession -Credential:$credential -ComputerName:$Node -Port:5986 -Authentication:basic -SessionOption:$opt -OperationTimeoutSec:90
```

> [!NOTE]
> <span data-ttu-id="47dc0-171">"Push" mód a felhasználó hitelesítő adatait a gyökér szintű felhasználó a Linux rendszerű számítógépen kell lennie.</span><span class="sxs-lookup"><span data-stu-id="47dc0-171">For “Push” mode, the user credential must be the root user on the Linux computer.</span></span>
> <span data-ttu-id="47dc0-172">Csak az SSL/TLS-kapcsolatok támogatottak DSC Linux rendszeren a `New-CimSession` – UseSSL paraméter $true értékűre kell használni.</span><span class="sxs-lookup"><span data-stu-id="47dc0-172">Only SSL/TLS connections are supported for DSC for Linux, the `New-CimSession` must be used with the –UseSSL parameter set to $true.</span></span>
> <span data-ttu-id="47dc0-173">Az SSL-tanúsítvány által használt OMI (DSC) a fájlban megadott: `/opt/omi/etc/omiserver.conf` a tulajdonságokkal: pemfile és kulcsfájl.</span><span class="sxs-lookup"><span data-stu-id="47dc0-173">The SSL certificate used by OMI (for DSC) is specified in the file: `/opt/omi/etc/omiserver.conf` with the properties: pemfile and keyfile.</span></span>
> <span data-ttu-id="47dc0-174">Ha ez a tanúsítvány nem megbízható által a Windows-számítógép, amely futtatja a [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) parancsmagot, ha szeretné, figyelmen kívül hagyja a tanúsítványok ellenőrzését a CIMSession beállításokkal: `-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`</span><span class="sxs-lookup"><span data-stu-id="47dc0-174">If this certificate is not trusted by the Windows computer that you are running the [New-CimSession](/powershell/module/CimCmdlets/New-CimSession) cmdlet on, you can choose to ignore certificate validation with the CIMSession Options: `-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`</span></span>

<span data-ttu-id="47dc0-175">A következő paranccsal küldje le a DSC-konfiguráció a Linux-csomópont.</span><span class="sxs-lookup"><span data-stu-id="47dc0-175">Run the following command to push the DSC configuration to the Linux node.</span></span>

`Start-DscConfiguration -Path:"C:\temp" -CimSession:$Sess -Wait -Verbose`

### <a name="distribute-the-configuration-with-a-pull-server"></a><span data-ttu-id="47dc0-176">A konfigurációt egy pull-kiszolgálóval</span><span class="sxs-lookup"><span data-stu-id="47dc0-176">Distribute the configuration with a pull server</span></span>

<span data-ttu-id="47dc0-177">Konfigurációk lehetnek elosztva egy Linux-számítógép egy pull-kiszolgálóval, csakúgy, mint a Windows-számítógépek.</span><span class="sxs-lookup"><span data-stu-id="47dc0-177">Configurations can be distributed to a Linux computer with a pull server, just like for Windows computers.</span></span> <span data-ttu-id="47dc0-178">Egy lekéréses kiszolgálót használ, tekintse át [Windows PowerShell Desired State Configuration lekéréses kiszolgálók](../pull-server/pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="47dc0-178">For guidance on using a pull server, see [Windows PowerShell Desired State Configuration Pull Servers](../pull-server/pullServer.md).</span></span> <span data-ttu-id="47dc0-179">További információt és Linux rendszerű számítógépek egy pull-kiszolgálóval kapcsolatos korlátozások: a kibocsátási megjegyzések a Desired State Configuration Linux rendszeren.</span><span class="sxs-lookup"><span data-stu-id="47dc0-179">For additional information and limitations related to using Linux computers with a pull server, see the Release Notes for Desired State Configuration for Linux.</span></span>

### <a name="working-with-configurations-locally"></a><span data-ttu-id="47dc0-180">Helyi konfigurációk használata</span><span class="sxs-lookup"><span data-stu-id="47dc0-180">Working with configurations locally</span></span>

<span data-ttu-id="47dc0-181">Linuxhoz készült DSC-szkriptek a helyi számítógépről Linux-konfigurációval is tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="47dc0-181">DSC for Linux includes scripts to work with configuration from the local Linux computer.</span></span> <span data-ttu-id="47dc0-182">Ezek a szkriptek keresse meg `/opt/microsoft/dsc/Scripts` és a következőket tartalmazzák:</span><span class="sxs-lookup"><span data-stu-id="47dc0-182">These scripts are locate in `/opt/microsoft/dsc/Scripts` and include the following:</span></span>

- <span data-ttu-id="47dc0-183">GetDscConfiguration.py</span><span class="sxs-lookup"><span data-stu-id="47dc0-183">GetDscConfiguration.py</span></span>

<span data-ttu-id="47dc0-184">Visszaadja az aktuális konfigurációt alkalmazta a számítógépre.</span><span class="sxs-lookup"><span data-stu-id="47dc0-184">Returns the current configuration applied to the computer.</span></span> <span data-ttu-id="47dc0-185">A Windows PowerShell-parancsmag hasonló `Get-DscConfiguration` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="47dc0-185">Similar to the Windows PowerShell cmdlet `Get-DscConfiguration` cmdlet.</span></span>

`# sudo ./GetDscConfiguration.py`

- <span data-ttu-id="47dc0-186">GetDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="47dc0-186">GetDscLocalConfigurationManager.py</span></span>

<span data-ttu-id="47dc0-187">Az aktuális meta-konfiguráció a számítógépen alkalmazott adja vissza.</span><span class="sxs-lookup"><span data-stu-id="47dc0-187">Returns the current meta-configuration applied to the computer.</span></span> <span data-ttu-id="47dc0-188">A parancsmag hasonló [Get-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="47dc0-188">Similar to the cmdlet [Get-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) cmdlet.</span></span>

`# sudo ./GetDscLocalConfigurationManager.py`

- <span data-ttu-id="47dc0-189">InstallModule.py</span><span class="sxs-lookup"><span data-stu-id="47dc0-189">InstallModule.py</span></span>

<span data-ttu-id="47dc0-190">Egy egyéni DSC-resource modul telepítése.</span><span class="sxs-lookup"><span data-stu-id="47dc0-190">Installs a custom DSC resource module.</span></span> <span data-ttu-id="47dc0-191">A modul megosztott objektumtár tartalmazó .zip fájl és a séma MOF-fájlok elérési útja szükséges.</span><span class="sxs-lookup"><span data-stu-id="47dc0-191">Requires the path to a .zip file containing the module shared object library and schema MOF files.</span></span>

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

- <span data-ttu-id="47dc0-192">RemoveModule.py</span><span class="sxs-lookup"><span data-stu-id="47dc0-192">RemoveModule.py</span></span>

<span data-ttu-id="47dc0-193">Eltávolít egy egyéni DSC-erőforrás modult.</span><span class="sxs-lookup"><span data-stu-id="47dc0-193">Removes a custom DSC resource module.</span></span> <span data-ttu-id="47dc0-194">A név egyben a modul eltávolítása szükséges.</span><span class="sxs-lookup"><span data-stu-id="47dc0-194">Requires the name of the module to remove.</span></span>

`# sudo ./RemoveModule.py cnx_Resource`

- <span data-ttu-id="47dc0-195">StartDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="47dc0-195">StartDscLocalConfigurationManager.py</span></span>

<span data-ttu-id="47dc0-196">A konfigurációs MOF-fájlt a számítógépre vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="47dc0-196">Applies a configuration MOF file to the computer.</span></span> <span data-ttu-id="47dc0-197">Hasonló a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="47dc0-197">Similar to the [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) cmdlet.</span></span> <span data-ttu-id="47dc0-198">A konfiguráció alkalmazásához MOF elérési útja szükséges.</span><span class="sxs-lookup"><span data-stu-id="47dc0-198">Requires the path to the configuration MOF to apply.</span></span>

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

- <span data-ttu-id="47dc0-199">SetDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="47dc0-199">SetDscLocalConfigurationManager.py</span></span>

<span data-ttu-id="47dc0-200">Meta konfigurációs MOF-fájlt a számítógépre vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="47dc0-200">Applies a Meta Configuration MOF file to the computer.</span></span> <span data-ttu-id="47dc0-201">Hasonló a [Set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="47dc0-201">Similar to the [Set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) cmdlet.</span></span> <span data-ttu-id="47dc0-202">A alkalmazni Meta konfigurációs MOF elérési útja szükséges.</span><span class="sxs-lookup"><span data-stu-id="47dc0-202">Requires the path to the Meta Configuration MOF to apply.</span></span>

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## <a name="powershell-desired-state-configuration-for-linux-log-files"></a><span data-ttu-id="47dc0-203">PowerShell Desired State Configuration for Linux-naplófájlok</span><span class="sxs-lookup"><span data-stu-id="47dc0-203">PowerShell Desired State Configuration for Linux Log Files</span></span>

<span data-ttu-id="47dc0-204">A következő naplófájlokat Linux üzenetek DSC jön létre.</span><span class="sxs-lookup"><span data-stu-id="47dc0-204">The following log files are generated for DSC for Linux messages.</span></span>

|<span data-ttu-id="47dc0-205">Naplófájl</span><span class="sxs-lookup"><span data-stu-id="47dc0-205">Log file</span></span>|<span data-ttu-id="47dc0-206">Könyvtár</span><span class="sxs-lookup"><span data-stu-id="47dc0-206">Directory</span></span>|<span data-ttu-id="47dc0-207">Leírás</span><span class="sxs-lookup"><span data-stu-id="47dc0-207">Description</span></span>|
|---|---|---|
|<span data-ttu-id="47dc0-208">**omiserver.log**</span><span class="sxs-lookup"><span data-stu-id="47dc0-208">**omiserver.log**</span></span>|`/var/opt/omi/log`|<span data-ttu-id="47dc0-209">Az OMI a CIM-kiszolgáló működésével kapcsolatos üzenetek.</span><span class="sxs-lookup"><span data-stu-id="47dc0-209">Messages relating to the operation of the OMI CIM server.</span></span>|
|<span data-ttu-id="47dc0-210">**dsc.log**</span><span class="sxs-lookup"><span data-stu-id="47dc0-210">**dsc.log**</span></span>|`/var/opt/omi/log`|<span data-ttu-id="47dc0-211">A helyi Configuration Manager (LCM) Konfigurálása és a DSC-erőforrás műveletek működésével kapcsolatos üzenetek.</span><span class="sxs-lookup"><span data-stu-id="47dc0-211">Messages relating to the operation of the Local Configuration Manager (LCM) and DSC resource operations.</span></span>|
