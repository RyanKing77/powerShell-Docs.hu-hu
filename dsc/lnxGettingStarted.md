---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A kívánt állapot konfigurációs szolgáltatása (DSC) első lépései Linux rendszeren"
ms.openlocfilehash: fd4820d27de5958a325032ca3fc202a521c131b4
ms.sourcegitcommit: 28e71b0ae868014523631fec3f5417de751944f3
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2017
---
# <a name="get-started-with-desired-state-configuration-dsc-for-linux"></a><span data-ttu-id="bbff2-103">A kívánt állapot konfigurációs szolgáltatása (DSC) első lépései Linux rendszeren</span><span class="sxs-lookup"><span data-stu-id="bbff2-103">Get started with Desired State Configuration (DSC) for Linux</span></span>

<span data-ttu-id="bbff2-104">Ez a témakör ismerteti, hogyan Linux PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) az első lépéseiben.</span><span class="sxs-lookup"><span data-stu-id="bbff2-104">This topic explains how to get started using PowerShell Desired State Configuration (DSC) for Linux.</span></span> <span data-ttu-id="bbff2-105">A DSC kapcsolatos általános információkért lásd: [Ismerkedés a Windows PowerShell célállapot-konfiguráció](overview.md).</span><span class="sxs-lookup"><span data-stu-id="bbff2-105">For general information about DSC, see [Get Started with Windows PowerShell Desired State Configuration](overview.md).</span></span>

## <a name="supported-linux-operation-system-versions"></a><span data-ttu-id="bbff2-106">Támogatott Linux művelet-verziók</span><span class="sxs-lookup"><span data-stu-id="bbff2-106">Supported Linux operation system versions</span></span>

<span data-ttu-id="bbff2-107">A következő Linux operációsrendszer-verziók DSC Linux támogatottak.</span><span class="sxs-lookup"><span data-stu-id="bbff2-107">The following Linux operating system versions are supported for DSC for Linux.</span></span>
- <span data-ttu-id="bbff2-108">CentOS 5, 6 és 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bbff2-108">CentOS 5, 6, and 7 (x86/x64)</span></span>
- <span data-ttu-id="bbff2-109">Debian GNU/Linux 6, 7, 8 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bbff2-109">Debian GNU/Linux 6, 7 and 8 (x86/x64)</span></span>
- <span data-ttu-id="bbff2-110">Oracle Linux 5, 6, 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bbff2-110">Oracle Linux 5, 6 and 7 (x86/x64)</span></span>
- <span data-ttu-id="bbff2-111">Red Hat Enterprise Linux Server 5, 6, 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bbff2-111">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
- <span data-ttu-id="bbff2-112">SUSE Linux Enterprise Server 10, 11, 12 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bbff2-112">SUSE Linux Enterprise Server 10, 11 and 12 (x86/x64)</span></span>
- <span data-ttu-id="bbff2-113">Ubuntu Server 12.04 LTS, 14.04 LTS és 16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="bbff2-113">Ubuntu Server 12.04 LTS, 14.04 LTS and 16.04 LTS (x86/x64)</span></span>

<span data-ttu-id="bbff2-114">A következő táblázat ismerteti a szükséges csomagfüggőségek Linux a DSC-ből.</span><span class="sxs-lookup"><span data-stu-id="bbff2-114">The following table describes the required package dependencies for DSC for Linux.</span></span>

|  <span data-ttu-id="bbff2-115">Szükséges csomag</span><span class="sxs-lookup"><span data-stu-id="bbff2-115">Required package</span></span> |  <span data-ttu-id="bbff2-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="bbff2-116">Description</span></span> |  <span data-ttu-id="bbff2-117">Minimális verzió</span><span class="sxs-lookup"><span data-stu-id="bbff2-117">Minimum version</span></span> | 
|---|---|---|
| <span data-ttu-id="bbff2-118">Glibc</span><span class="sxs-lookup"><span data-stu-id="bbff2-118">glibc</span></span>| <span data-ttu-id="bbff2-119">GNU könyvtár</span><span class="sxs-lookup"><span data-stu-id="bbff2-119">GNU Library</span></span>| <span data-ttu-id="bbff2-120">2…4 – 31.30</span><span class="sxs-lookup"><span data-stu-id="bbff2-120">2…4 – 31.30</span></span>| 
| <span data-ttu-id="bbff2-121">Python</span><span class="sxs-lookup"><span data-stu-id="bbff2-121">python</span></span>| <span data-ttu-id="bbff2-122">Python</span><span class="sxs-lookup"><span data-stu-id="bbff2-122">Python</span></span>| <span data-ttu-id="bbff2-123">2.4 – 3.4</span><span class="sxs-lookup"><span data-stu-id="bbff2-123">2.4 – 3.4</span></span>| 
| <span data-ttu-id="bbff2-124">omiserver</span><span class="sxs-lookup"><span data-stu-id="bbff2-124">omiserver</span></span>| <span data-ttu-id="bbff2-125">Nyílt kezelési infrastruktúra</span><span class="sxs-lookup"><span data-stu-id="bbff2-125">Open Management Infrastructure</span></span>| <span data-ttu-id="bbff2-126">1.0.8.1</span><span class="sxs-lookup"><span data-stu-id="bbff2-126">1.0.8.1</span></span>| 
| <span data-ttu-id="bbff2-127">Openssl</span><span class="sxs-lookup"><span data-stu-id="bbff2-127">openssl</span></span>| <span data-ttu-id="bbff2-128">OpenSSL-függvénytárak</span><span class="sxs-lookup"><span data-stu-id="bbff2-128">OpenSSL Libraries</span></span>| <span data-ttu-id="bbff2-129">0.9.8-as vagy 1.0</span><span class="sxs-lookup"><span data-stu-id="bbff2-129">0.9.8 or 1.0</span></span>| 
| <span data-ttu-id="bbff2-130">ctypes</span><span class="sxs-lookup"><span data-stu-id="bbff2-130">ctypes</span></span>| <span data-ttu-id="bbff2-131">Python CTypes könyvtár</span><span class="sxs-lookup"><span data-stu-id="bbff2-131">Python CTypes library</span></span>| <span data-ttu-id="bbff2-132">Meg kell egyeznie a Python-verzió</span><span class="sxs-lookup"><span data-stu-id="bbff2-132">Must match Python version</span></span>| 
| <span data-ttu-id="bbff2-133">libcurl</span><span class="sxs-lookup"><span data-stu-id="bbff2-133">libcurl</span></span>| <span data-ttu-id="bbff2-134">cURL http ügyféloldali kódtár</span><span class="sxs-lookup"><span data-stu-id="bbff2-134">cURL http client library</span></span>| <span data-ttu-id="bbff2-135">7.15.1</span><span class="sxs-lookup"><span data-stu-id="bbff2-135">7.15.1</span></span>| 

## <a name="installing-dsc-for-linux"></a><span data-ttu-id="bbff2-136">A Linux DSC telepítése</span><span class="sxs-lookup"><span data-stu-id="bbff2-136">Installing DSC for Linux</span></span>

<span data-ttu-id="bbff2-137">Telepítenie kell a [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) Linux DSC telepítése előtt.</span><span class="sxs-lookup"><span data-stu-id="bbff2-137">You must install the [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) before installing DSC for Linux.</span></span>

### <a name="installing-omi"></a><span data-ttu-id="bbff2-138">OMI telepítése</span><span class="sxs-lookup"><span data-stu-id="bbff2-138">Installing OMI</span></span>

<span data-ttu-id="bbff2-139">Állapotkonfiguráció szükséges Linux ír elő az Open Management Infrastructure (OMI) CIM-kiszolgáló, 1.0.8.1 verzió vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="bbff2-139">Desired State Configuration for Linux requires the Open Management Infrastructure (OMI) CIM server, version 1.0.8.1 or later.</span></span> <span data-ttu-id="bbff2-140">OMI tölthető le: az Open Group: [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi).</span><span class="sxs-lookup"><span data-stu-id="bbff2-140">OMI can be downloaded from The Open Group: [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi).</span></span>

<span data-ttu-id="bbff2-141">OMI telepítéséhez telepítse a csomagot, amely megfelel a Linux rendszer (.rpm vagy .deb) és a OpenSSL-verzió (ssl_098 vagy ssl_100) és az architektúra (x64/x86).</span><span class="sxs-lookup"><span data-stu-id="bbff2-141">To install OMI, install the package that is appropriate for your Linux system (.rpm or .deb) and OpenSSL version (ssl_098 or ssl_100), and architecture (x64/x86).</span></span> <span data-ttu-id="bbff2-142">RPM csomagok CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server és Oracle Linux alkalmasak.</span><span class="sxs-lookup"><span data-stu-id="bbff2-142">RPM packages are appropriate for CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, and Oracle Linux.</span></span> <span data-ttu-id="bbff2-143">DEB-csomagokat a Debian GNU/Linux és Ubuntu Server alkalmasak.</span><span class="sxs-lookup"><span data-stu-id="bbff2-143">DEB packages are appropriate for Debian GNU/Linux and Ubuntu Server.</span></span> <span data-ttu-id="bbff2-144">A ssl_098 csomagok megfelelőek OpenSSL telepítve, miközben az OpenSSL 1.0 telepítve olyan számítógépek a ssl_100 csomagok 0.9.8-as rendelkező számítógépek.</span><span class="sxs-lookup"><span data-stu-id="bbff2-144">The ssl_098 packages are appropriate for computers with OpenSSL 0.9.8 installed while the ssl_100 packages are appropriate for computers with OpenSSL 1.0 installed.</span></span>

> <span data-ttu-id="bbff2-145">**Megjegyzés:**: a parancs futtatásával határozza meg a telepített OpenSSL-verzió, `openssl version`.</span><span class="sxs-lookup"><span data-stu-id="bbff2-145">**Note**: To determine the installed OpenSSL version, run the command `openssl version`.</span></span>

<span data-ttu-id="bbff2-146">A következő paranccsal telepíthető OMI CentOS 7 x64 rendszeren.</span><span class="sxs-lookup"><span data-stu-id="bbff2-146">Run the following command to install OMI on a CentOS 7 x64 system.</span></span>

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### <a name="installing-dsc"></a><span data-ttu-id="bbff2-147">A DSC telepítése</span><span class="sxs-lookup"><span data-stu-id="bbff2-147">Installing DSC</span></span>

<span data-ttu-id="bbff2-148">Linux DSC érhető el a letöltési [Itt](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="bbff2-148">DSC for Linux is available for download [here](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/latest).</span></span> 

<span data-ttu-id="bbff2-149">A DSC telepítéséhez telepítse a csomagot, amely megfelel a Linux rendszer (.rpm vagy .deb) és a OpenSSL-verzió (ssl_098 vagy ssl_100) és az architektúra (x64/x86).</span><span class="sxs-lookup"><span data-stu-id="bbff2-149">To install DSC, install the package that is appropriate for your Linux system (.rpm or .deb) and OpenSSL version (ssl_098 or ssl_100), and architecture (x64/x86).</span></span> <span data-ttu-id="bbff2-150">RPM csomagok CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server és Oracle Linux alkalmasak.</span><span class="sxs-lookup"><span data-stu-id="bbff2-150">RPM packages are appropriate for CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, and Oracle Linux.</span></span> <span data-ttu-id="bbff2-151">DEB-csomagokat a Debian GNU/Linux és Ubuntu Server alkalmasak.</span><span class="sxs-lookup"><span data-stu-id="bbff2-151">DEB packages are appropriate for Debian GNU/Linux and Ubuntu Server.</span></span> <span data-ttu-id="bbff2-152">A ssl_098 csomagok megfelelőek OpenSSL telepítve, miközben az OpenSSL 1.0 telepítve olyan számítógépek a ssl_100 csomagok 0.9.8-as rendelkező számítógépek.</span><span class="sxs-lookup"><span data-stu-id="bbff2-152">The ssl_098 packages are appropriate for computers with OpenSSL 0.9.8 installed while the ssl_100 packages are appropriate for computers with OpenSSL 1.0 installed.</span></span>

> <span data-ttu-id="bbff2-153">**Megjegyzés:**: annak meghatározásához, a telepített OpenSSL-verzió, a parancs openssl verzióját futtatják.</span><span class="sxs-lookup"><span data-stu-id="bbff2-153">**Note**: To determine the installed OpenSSL version, run the command openssl version.</span></span>
 
<span data-ttu-id="bbff2-154">A következő paranccsal telepíthető DSC CentOS 7 x64 rendszeren.</span><span class="sxs-lookup"><span data-stu-id="bbff2-154">Run the following command to install DSC on a CentOS 7 x64 system.</span></span>

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`


## <a name="using-dsc-for-linux"></a><span data-ttu-id="bbff2-155">A DSC használata Linux rendszeren</span><span class="sxs-lookup"><span data-stu-id="bbff2-155">Using DSC for Linux</span></span>

<span data-ttu-id="bbff2-156">Az alábbi szakaszok ismertetik, hogyan hozhat létre és futtathat a DSC-konfigurációk a Linux rendszerű számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="bbff2-156">The following sections explain how to create and run DSC configurations on Linux computers.</span></span>

### <a name="creating-a-configuration-mof-document"></a><span data-ttu-id="bbff2-157">Konfigurációs MOF dokumentumok létrehozása</span><span class="sxs-lookup"><span data-stu-id="bbff2-157">Creating a configuration MOF document</span></span>

<span data-ttu-id="bbff2-158">A Windows PowerShell-konfiguráció kulcsszó létrehozásához használt Linux rendszerű számítógépek konfigurációját hasonlóan a Windows rendszerű számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="bbff2-158">The Windows PowerShell Configuration keyword is used to create a configuration for Linux computers, just like for Windows computers.</span></span> <span data-ttu-id="bbff2-159">A következő lépések azt mutatják be, a Windows PowerShell használatával Linux számítógép konfigurációs dokumentum létrehozása.</span><span class="sxs-lookup"><span data-stu-id="bbff2-159">The following steps describe the creation of a configuration document for a Linux computer using Windows PowerShell.</span></span>

1. <span data-ttu-id="bbff2-160">A nx modul importálása.</span><span class="sxs-lookup"><span data-stu-id="bbff2-160">Import the nx module.</span></span> <span data-ttu-id="bbff2-161">Nx Windows PowerShell-modul tartalmaz az a séma beépített erőforrások DSC Linux, és telepítve legyen a helyi számítógépen, és importálja a konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="bbff2-161">The nx Windows PowerShell module contains the schema for Built-In resources for DSC for Linux, and must be installed to your local computer and imported in the configuration.</span></span>

    <span data-ttu-id="bbff2-162">-A nx modul telepítése, másolja a nx modulkönyvtárat vagy `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` vagy `$PSHOME\Modules`.</span><span class="sxs-lookup"><span data-stu-id="bbff2-162">-To install the nx module, copy the nx module directory to either `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` or `$PSHOME\Modules`.</span></span> <span data-ttu-id="bbff2-163">A nx modul tartalmazza a DSC Linux-telepítési csomag (MSI).</span><span class="sxs-lookup"><span data-stu-id="bbff2-163">The nx module is included in the DSC for Linux installation package (MSI).</span></span> <span data-ttu-id="bbff2-164">A nx moduljának a konfiguráció importálásához használja a __Import-DSCResource__ parancs:</span><span class="sxs-lookup"><span data-stu-id="bbff2-164">To import the nx module in your configuration, use the __Import-DSCResource__ command:</span></span>
    
```powershell
Configuration ExampleConfiguration{
   
    Import-DSCResource -Module nx

}
```
2. <span data-ttu-id="bbff2-165">A konfiguráció és a konfigurációs dokumentum létrehozása:</span><span class="sxs-lookup"><span data-stu-id="bbff2-165">Define a configuration and generate the configuration document:</span></span>

```powershell
Configuration ExampleConfiguration{
   
    Import-DscResource -Module nx
 
    Node  "linuxhost.contoso.com"{
    nxFile ExampleFile {

        DestinationPath = "/tmp/example"
        Contents = "hello world `n"
        Ensure = "Present"
        Type = "File"
    }

    }
}
ExampleConfiguration -OutputPath:"C:\temp" 
```

### <a name="push-the-configuration-to-the-linux-computer"></a><span data-ttu-id="bbff2-166">A konfigurációs leküldése a Linux rendszerű számítógép</span><span class="sxs-lookup"><span data-stu-id="bbff2-166">Push the configuration to the Linux computer</span></span>

<span data-ttu-id="bbff2-167">Konfigurációs dokumentumok (MOF-fájlok) a Linux rendszerű számítógépen történő továbbíthatja a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="bbff2-167">Configuration documents (MOF files) can be pushed to the Linux computer using the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet.</span></span> <span data-ttu-id="bbff2-168">Ahhoz, hogy ez a parancsmag, valamint a [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx), vagy [teszt-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) parancsmagok távolról a Linux-számítógép segítségével kell egy CIMSession.</span><span class="sxs-lookup"><span data-stu-id="bbff2-168">In order to use this cmdlet, along with the [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx), or [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlets, remotely to a Linux computer, you must use a CIMSession.</span></span> <span data-ttu-id="bbff2-169">A [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) parancsmag segítségével hozzon létre egy CIMSession Linux rendszerű számítógép.</span><span class="sxs-lookup"><span data-stu-id="bbff2-169">The [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) cmdlet is used to create a CIMSession to the Linux computer.</span></span>

<span data-ttu-id="bbff2-170">A következő kód bemutatja, hogyan hozzon létre egy CIMSession DSC Linux.</span><span class="sxs-lookup"><span data-stu-id="bbff2-170">The following code shows how to create a CIMSession for DSC for Linux.</span></span>

```powershell
$Node = "ostc-dsc-01"
$Credential = Get-Credential -UserName:"root" -Message:"Enter Password:"

#Ignore SSL certificate validation
#$opt = New-CimSessionOption -UseSsl:$true -SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true

#Options for a trusted SSL certificate
$opt = New-CimSessionOption -UseSsl:$true 
$Sess=New-CimSession -Credential:$credential -ComputerName:$Node -Port:5986 -Authentication:basic -SessionOption:$opt -OperationTimeoutSec:90 
```

> <span data-ttu-id="bbff2-171">**Megjegyzés:**:</span><span class="sxs-lookup"><span data-stu-id="bbff2-171">**Note**:</span></span>
* <span data-ttu-id="bbff2-172">Az "Push" módban a felhasználó hitelesítő adatainak a gyökér szintű felhasználó a Linux rendszerű számítógépen kell lennie.</span><span class="sxs-lookup"><span data-stu-id="bbff2-172">For “Push” mode, the user credential must be the root user on the Linux computer.</span></span>
* <span data-ttu-id="bbff2-173">A Linux, a New-CimSession együtt kell használni a – UseSSL paraméter $true DSC csak SSL/TLS kapcsolatok támogatottak.</span><span class="sxs-lookup"><span data-stu-id="bbff2-173">Only SSL/TLS connections are supported for DSC for Linux, the New-CimSession must be used with the –UseSSL parameter set to $true.</span></span>
* <span data-ttu-id="bbff2-174">Az SSL-tanúsítvány által használt OMI (DSC) a fájlban megadott: `/opt/omi/etc/omiserver.conf` a tulajdonságokkal: pemfile és keyfile.</span><span class="sxs-lookup"><span data-stu-id="bbff2-174">The SSL certificate used by OMI (for DSC) is specified in the file: `/opt/omi/etc/omiserver.conf` with the properties: pemfile and keyfile.</span></span>
<span data-ttu-id="bbff2-175">Ha ez a tanúsítvány nem megbízható által a Windows-számítógép, amely futtatja a [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) parancsmagot, ha szeretné, figyelmen kívül hagyja a CIMSession beállításokkal tanúsítvány érvényesítése:`-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`</span><span class="sxs-lookup"><span data-stu-id="bbff2-175">If this certificate is not trusted by the Windows computer that you are running the [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) cmdlet on, you can choose to ignore certificate validation with the CIMSession Options: `-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`</span></span>

<span data-ttu-id="bbff2-176">A következő parancsot a DSC-konfiguráció leküldése a Linux-csomópont.</span><span class="sxs-lookup"><span data-stu-id="bbff2-176">Run the following command to push the DSC configuration to the Linux node.</span></span>

`Start-DscConfiguration -Path:"C:\temp" -CimSession:$Sess -Wait -Verbose`

### <a name="distribute-the-configuration-with-a-pull-server"></a><span data-ttu-id="bbff2-177">A lekérési kiszolgálójával a konfiguráció terjesztése</span><span class="sxs-lookup"><span data-stu-id="bbff2-177">Distribute the configuration with a pull server</span></span>

<span data-ttu-id="bbff2-178">Konfigurációk is terjeszthetők a Linux-számítógép lekéréses kiszolgálóval, csakúgy, mint a Windows rendszerű számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="bbff2-178">Configurations can be distributed to a Linux computer with a pull server, just like for Windows computers.</span></span> <span data-ttu-id="bbff2-179">A lekérési kiszolgálójával használatával útmutatóért lásd: [Windows PowerShell kívánt állapot konfigurációs lekéréses kiszolgálók](pullServer.md).</span><span class="sxs-lookup"><span data-stu-id="bbff2-179">For guidance on using a pull server, see [Windows PowerShell Desired State Configuration Pull Servers](pullServer.md).</span></span> <span data-ttu-id="bbff2-180">További információért és Linux számítógépeket használ egy lekéréses-kiszolgálóval kapcsolatos korlátozások tekintse meg a kibocsátási megjegyzéseket a célállapot-konfiguráció Linux.</span><span class="sxs-lookup"><span data-stu-id="bbff2-180">For additional information and limitations related to using Linux computers with a pull server, see the Release Notes for Desired State Configuration for Linux.</span></span>

### <a name="working-with-configurations-locally"></a><span data-ttu-id="bbff2-181">Helyileg konfigurációk használata</span><span class="sxs-lookup"><span data-stu-id="bbff2-181">Working with configurations locally</span></span>

<span data-ttu-id="bbff2-182">Linux DSC tartalmaz a helyi Linux számítógép-konfiguráció használható parancsfájlokat.</span><span class="sxs-lookup"><span data-stu-id="bbff2-182">DSC for Linux includes scripts to work with configuration from the local Linux computer.</span></span> <span data-ttu-id="bbff2-183">Ezek a parancsfájlok keresse meg `/opt/microsoft/dsc/Scripts` és adja meg a következőket:</span><span class="sxs-lookup"><span data-stu-id="bbff2-183">These scripts are locate in `/opt/microsoft/dsc/Scripts` and include the following:</span></span>
* <span data-ttu-id="bbff2-184">GetDscConfiguration.py</span><span class="sxs-lookup"><span data-stu-id="bbff2-184">GetDscConfiguration.py</span></span>

 <span data-ttu-id="bbff2-185">A jelenlegi konfiguráció a számítógépen alkalmazott adja vissza.</span><span class="sxs-lookup"><span data-stu-id="bbff2-185">Returns the current configuration applied to the computer.</span></span> <span data-ttu-id="bbff2-186">Hasonló a Windows PowerShell-parancsmag Get-DscConfiguration parancsmagnak.</span><span class="sxs-lookup"><span data-stu-id="bbff2-186">Similar to the Windows PowerShell cmdlet Get-DscConfiguration cmdlet.</span></span>

`# sudo ./GetDscConfiguration.py`

* <span data-ttu-id="bbff2-187">GetDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="bbff2-187">GetDscLocalConfigurationManager.py</span></span>

 <span data-ttu-id="bbff2-188">Visszaadja a jelenlegi metaadat-konfiguráció alkalmazni a számítógépen.</span><span class="sxs-lookup"><span data-stu-id="bbff2-188">Returns the current meta-configuration applied to the computer.</span></span> <span data-ttu-id="bbff2-189">A parancsmag hasonló [Get-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="bbff2-189">Similar to the cmdlet [Get-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx) cmdlet.</span></span>

`# sudo ./GetDscLocalConfigurationManager.py`

* <span data-ttu-id="bbff2-190">InstallModule.py</span><span class="sxs-lookup"><span data-stu-id="bbff2-190">InstallModule.py</span></span>

 <span data-ttu-id="bbff2-191">Egy egyéni DSC erőforrás modult telepít.</span><span class="sxs-lookup"><span data-stu-id="bbff2-191">Installs a custom DSC resource module.</span></span> <span data-ttu-id="bbff2-192">A modul megosztott objektumtár tartalmazó .zip fájl és a séma MOF-fájlok elérési útja van szükség.</span><span class="sxs-lookup"><span data-stu-id="bbff2-192">Requires the path to a .zip file containing the module shared object library and schema MOF files.</span></span>

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

* <span data-ttu-id="bbff2-193">RemoveModule.py</span><span class="sxs-lookup"><span data-stu-id="bbff2-193">RemoveModule.py</span></span>

 <span data-ttu-id="bbff2-194">Eltávolít egy egyéni DSC erőforrás modult.</span><span class="sxs-lookup"><span data-stu-id="bbff2-194">Removes a custom DSC resource module.</span></span> <span data-ttu-id="bbff2-195">Eltávolítja a modul neve igényel.</span><span class="sxs-lookup"><span data-stu-id="bbff2-195">Requires the name of the module to remove.</span></span>

`# sudo ./RemoveModule.py cnx_Resource`

* <span data-ttu-id="bbff2-196">StartDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="bbff2-196">StartDscLocalConfigurationManager.py</span></span> 

 <span data-ttu-id="bbff2-197">A számítógép érvényes konfigurációs MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="bbff2-197">Applies a configuration MOF file to the computer.</span></span> <span data-ttu-id="bbff2-198">Hasonló a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="bbff2-198">Similar to the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet.</span></span> <span data-ttu-id="bbff2-199">A konfiguráció alkalmazásához MOF elérési igényel.</span><span class="sxs-lookup"><span data-stu-id="bbff2-199">Requires the path to the configuration MOF to apply.</span></span>

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

* <span data-ttu-id="bbff2-200">SetDscLocalConfigurationManager.py</span><span class="sxs-lookup"><span data-stu-id="bbff2-200">SetDscLocalConfigurationManager.py</span></span>

 <span data-ttu-id="bbff2-201">A számítógép érvényes Meta konfigurációs MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="bbff2-201">Applies a Meta Configuration MOF file to the computer.</span></span> <span data-ttu-id="bbff2-202">Hasonló a [Set-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="bbff2-202">Similar to the [Set-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx) cmdlet.</span></span> <span data-ttu-id="bbff2-203">Elérési útját a Meta konfigurációs MOF alkalmazásához szükséges.</span><span class="sxs-lookup"><span data-stu-id="bbff2-203">Requires the path to the Meta Configuration MOF to apply.</span></span>

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## <a name="powershell-desired-state-configuration-for-linux-log-files"></a><span data-ttu-id="bbff2-204">PowerShell kívánt állapot konfigurációs Linux-naplófájlok</span><span class="sxs-lookup"><span data-stu-id="bbff2-204">PowerShell Desired State Configuration for Linux Log Files</span></span>

<span data-ttu-id="bbff2-205">A következő naplófájlokba Linux üzenetek DSC jön létre.</span><span class="sxs-lookup"><span data-stu-id="bbff2-205">The following log files are generated for DSC for Linux messages.</span></span>

|<span data-ttu-id="bbff2-206">Naplófájl</span><span class="sxs-lookup"><span data-stu-id="bbff2-206">Log file</span></span>|<span data-ttu-id="bbff2-207">Könyvtár</span><span class="sxs-lookup"><span data-stu-id="bbff2-207">Directory</span></span>|<span data-ttu-id="bbff2-208">Leírás</span><span class="sxs-lookup"><span data-stu-id="bbff2-208">Description</span></span>|
|---|---|---|
|<span data-ttu-id="bbff2-209">omiserver.log</span><span class="sxs-lookup"><span data-stu-id="bbff2-209">omiserver.log</span></span>|<span data-ttu-id="bbff2-210">/var/OPT/OMI/log</span><span class="sxs-lookup"><span data-stu-id="bbff2-210">/var/opt/omi/log</span></span>|<span data-ttu-id="bbff2-211">Az OMI a CIM-kiszolgáló működésével kapcsolatos üzeneteket.</span><span class="sxs-lookup"><span data-stu-id="bbff2-211">Messages relating to the operation of the OMI CIM server.</span></span>|
|<span data-ttu-id="bbff2-212">DSC.log</span><span class="sxs-lookup"><span data-stu-id="bbff2-212">dsc.log</span></span>|<span data-ttu-id="bbff2-213">/var/OPT/OMI/log</span><span class="sxs-lookup"><span data-stu-id="bbff2-213">/var/opt/omi/log</span></span>|<span data-ttu-id="bbff2-214">A helyi Configuration Manager (LCM) és a DSC erőforrás műveletek működésével kapcsolatos üzeneteket.</span><span class="sxs-lookup"><span data-stu-id="bbff2-214">Messages relating to the operation of the Local Configuration Manager (LCM) and DSC resource operations.</span></span>|

