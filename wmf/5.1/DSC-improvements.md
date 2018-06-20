---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 DSC fejlesztései
ms.openlocfilehash: 32bdde6d43d17cc76c454fe10b00097753a9eebe
ms.sourcegitcommit: 2d9cf1ccb9a653db7726a408ebcb65530dcb1522
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/19/2018
ms.locfileid: "34309542"
---
# <a name="improvements-in-desired-state-configuration-dsc-in-wmf-51"></a><span data-ttu-id="1e6b3-103">A célállapot-konfiguráció (DSC) a WMF 5.1 fejlesztései</span><span class="sxs-lookup"><span data-stu-id="1e6b3-103">Improvements in Desired State Configuration (DSC) in WMF 5.1</span></span>

## <a name="dsc-class-resource-improvements"></a><span data-ttu-id="1e6b3-104">A DSC osztály erőforrás fejlesztései</span><span class="sxs-lookup"><span data-stu-id="1e6b3-104">DSC class resource improvements</span></span>

<span data-ttu-id="1e6b3-105">A WMF 5.1 rögzített azt az alábbi ismert problémák:</span><span class="sxs-lookup"><span data-stu-id="1e6b3-105">In WMF 5.1, we have fixed the following known issues:</span></span>

- <span data-ttu-id="1e6b3-106">Ha egy osztály-alapú DSC erőforrás Get() függvény által visszaadott komplex/kivonat táblatípust Get-DscConfiguration üres értékek (null) vagy hibákat adhat vissza.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-106">Get-DscConfiguration may return empty values (null) or errors if a complex/hash table type is returned by Get() function of a class-based DSC resource.</span></span>
- <span data-ttu-id="1e6b3-107">Get-DscConfiguration RunAs hitelesítő adatok használata a DSC-konfiguráció hibaüzenetet adja vissza.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-107">Get-DscConfiguration returns error if RunAs credential is used in DSC configuration.</span></span>
- <span data-ttu-id="1e6b3-108">Az osztály-alapú erőforrás összetett konfigurációban nem használható.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-108">Class-based resource cannot be used in a composite configuration.</span></span>
- <span data-ttu-id="1e6b3-109">Start-DscConfiguration lefagy, ha az osztály-alapú erőforrás rendelkezik saját típusú tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-109">Start-DscConfiguration hangs if class-based resource has a property of its own type.</span></span>
- <span data-ttu-id="1e6b3-110">Az osztály-alapú erőforrás kizárólagos erőforrásként nem használható.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-110">Class-based resource cannot be used as an exclusive resource.</span></span>

## <a name="dsc-resource-debugging-improvements"></a><span data-ttu-id="1e6b3-111">A DSC erőforrás hibakeresési fejlesztései</span><span class="sxs-lookup"><span data-stu-id="1e6b3-111">DSC resource debugging improvements</span></span>

<span data-ttu-id="1e6b3-112">A WMF 5.0-s a PowerShell hibakereső nem állt le a erőforrás osztály-alapú módszer (Get és Set/tesztelési célú) közvetlenül.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-112">In WMF 5.0, the PowerShell debugger did not stop at the class-based resource method (Get/Set/Test) directly.</span></span>
<span data-ttu-id="1e6b3-113">WMF 5.1 a hibakereső nem osztály-alapú erőforrás metódust. a MOF-alapú erőforrások módszerek ugyanúgy.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-113">In WMF 5.1, the debugger stops at the class-based resource method in the same way as for MOF-based resources methods.</span></span>

## <a name="dsc-pull-client-supports-tls-11-and-tls-12"></a><span data-ttu-id="1e6b3-114">DSC lekérési ügyfél támogatja a TLS 1.1 és TLS 1.2-es</span><span class="sxs-lookup"><span data-stu-id="1e6b3-114">DSC pull client supports TLS 1.1 and TLS 1.2</span></span>

<span data-ttu-id="1e6b3-115">Korábban a DSC lekérési ügyfél csak támogatott SSL3.0 és TLS1.0 HTTPS-kapcsolatokon keresztül.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-115">Previously, the DSC pull client only supported SSL3.0 and TLS1.0 over HTTPS connections.</span></span>
<span data-ttu-id="1e6b3-116">Kényszerítetten biztonságosabb protokollt használják, amikor a leküldéses ügyfél volna működését.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-116">When forced to use more secure protocols, the pull client would stop functioning.</span></span>
<span data-ttu-id="1e6b3-117">WMF 5.1 a DSC lekérési ügyfél már nem támogatja az SSL 3.0, és a biztonságosabb a TLS 1.1 és TLS 1.2 protokoll támogatása.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-117">In WMF 5.1, the DSC pull client no longer supports SSL 3.0 and adds support for the more secure TLS 1.1 and TLS 1.2 protocols.</span></span>

## <a name="improved-pull-server-registration"></a><span data-ttu-id="1e6b3-118">Továbbfejlesztett lekéréses kiszolgáló regisztrálása</span><span class="sxs-lookup"><span data-stu-id="1e6b3-118">Improved pull server registration</span></span>

<span data-ttu-id="1e6b3-119">WMF korábbi verzióiban egyidejű regisztrációk/reporting kérelmek egy DSC lekérési kiszolgálójával a ESENT adatbázis használatakor regisztrálni és/vagy a jelentést sikerült LCM vezetne.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-119">In the earlier versions of WMF, simultaneous registrations/reporting requests to a DSC pull server while using the ESENT database would lead to LCM failing to register and/or report.</span></span>
<span data-ttu-id="1e6b3-120">Ezekben az esetekben az eseménynaplók a lekérési kiszolgálón hibát a "Példány neve már használatban van."</span><span class="sxs-lookup"><span data-stu-id="1e6b3-120">In such cases, the event logs on the pull server has the error "Instance Name already in use."</span></span>
<span data-ttu-id="1e6b3-121">A többszálas forgatókönyvek ESENT-adatbázisának eléréséhez használt helytelen mintát miatt volt.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-121">This was due to an incorrect pattern being used to access the ESENT database in a multi-threaded scenario.</span></span>
<span data-ttu-id="1e6b3-122">A WMF 5.1 a probléma kijavítása.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-122">In WMF 5.1, this issue has been fixed.</span></span>
<span data-ttu-id="1e6b3-123">Egyidejű regisztrációk vagy reporting (ESENT adatbázist érintő) szolgáltatás megfelelően működik az WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-123">Concurrent registrations or reporting (involving ESENT database) works fine in WMF 5.1.</span></span>
<span data-ttu-id="1e6b3-124">A probléma csak a ESENT adatbázis használható, és nem vonatkozik az OLEDB-adatbázisban.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-124">This issue is applicable only to the ESENT database and does not apply to the OLEDB database.</span></span>

## <a name="enable-circular-log-on-esent-database-instance"></a><span data-ttu-id="1e6b3-125">Körkörös napló ESENT adatbázispéldányhoz engedélyezése</span><span class="sxs-lookup"><span data-stu-id="1e6b3-125">Enable Circular log on ESENT database instance</span></span>

<span data-ttu-id="1e6b3-126">A DSC-PullServer eariler verzióban ESENT adatbázis naplófájlokat a szabad lemezterület a körkörös naplózás nélkül létrehozásakor az adatbázispéldány fölött pullserver becouse volt betelőben.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-126">In eariler version of DSC-PullServer, the ESENT database log files were filling up the disk space of the pullserver becouse the database instance was being created without circular logging.</span></span> <span data-ttu-id="1e6b3-127">Ebben a kiadásban lehetősége van a körkörös naplózás működését a példányhoz, a pullserver web.config használatával.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-127">In this release, you have the option to control the circular logging behavior of the instance using the web.config of the pullserver.</span></span> <span data-ttu-id="1e6b3-128">Alapértelmezés szerint CircularLogging igaz értékre van beállítva.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-128">By default CircularLogging is set to TRUE.</span></span>

```
<appSettings>
    <add key="dbprovider" value="ESENT" />
    <add key="dbconnectionstr" value="C:\Program Files\WindowsPowerShell\DscService\Devices.edb" />
    <add key="CheckpointDepthMaxKB" value="512" />
    <add key="UseCircularESENTLogs" value="TRUE" />
  </appSettings>
```

## <a name="pull-partial-configuration-naming-convention"></a><span data-ttu-id="1e6b3-129">Lekéréses részleges konfigurációs elnevezési egyezmény</span><span class="sxs-lookup"><span data-stu-id="1e6b3-129">Pull partial configuration naming convention</span></span>

<span data-ttu-id="1e6b3-130">A korábbi változatban az elnevezési részleges-konfiguráció lett, hogy a MOF-fájl neve, a lekéréses/szolgáltatás meg kell felelnie a helyi configuration manager-beállításait, amely pedig meg kell egyeznie a részleges konfiguráció nevét a a beágyazott konfiguráció neve a MOF-fájlban.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-130">In the previous release, the naming convention for a partial configuration was that the MOF file name in the pull server/service should match the partial configuration name specified in the local configuration manager settings that in turn must match the configuration name embedded in the MOF file.</span></span>

<span data-ttu-id="1e6b3-131">Tekintse meg az alábbi pillanatképeket:</span><span class="sxs-lookup"><span data-stu-id="1e6b3-131">See the snapshots below:</span></span>

- <span data-ttu-id="1e6b3-132">Helyi konfigurációs beállításokat, amely meghatározza, hogy egy csomópont kap részleges konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-132">Local configuration settings which defines a partial configuration that a node is allowed to receive.</span></span>

![A minta metakonfigurációját](../images/MetaConfigPartialOne.png)

- <span data-ttu-id="1e6b3-134">A minta részleges konfiguráció definíciója</span><span class="sxs-lookup"><span data-stu-id="1e6b3-134">Sample partial configuration definition</span></span>

```powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

- <span data-ttu-id="1e6b3-135">A generált MOF-fájlnak a beágyazott (ConfigurationName).</span><span class="sxs-lookup"><span data-stu-id="1e6b3-135">'ConfigurationName' embedded in the generated MOF file.</span></span>

![A minta létrehozott mof-fájlt](../images/PartialGeneratedMof.png)

- <span data-ttu-id="1e6b3-137">A lekéréses konfigurációs tárházban fájlnév</span><span class="sxs-lookup"><span data-stu-id="1e6b3-137">FileName in the pull configuration repository</span></span>

![A konfigurációs tárházban fájlnév](../images/PartialInConfigRepository.png)

<span data-ttu-id="1e6b3-139">Azure Automation szolgáltatás neve MOF-fájlok használata a generált `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-139">Azure Automation service name generated MOF files as `<ConfigurationName>.<NodeName>.mof`.</span></span>
<span data-ttu-id="1e6b3-140">Az alábbi konfigurációs így PartialOne.localhost.mof lefordítja.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-140">So the configuration below compiles to PartialOne.localhost.mof.</span></span>

<span data-ttu-id="1e6b3-141">Ez lehetetlenné a részleges konfigurációs egyik lekéréses az Azure Automation szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-141">This made it impossible to pull one of your partial configuration from Azure Automation service.</span></span>

```powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

<span data-ttu-id="1e6b3-142">A WMF 5.1, a lekéréses/szolgáltatás egy részleges konfigurációs nevű `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-142">In WMF 5.1, a partial configuration in the pull server/service can be named as `<ConfigurationName>.<NodeName>.mof`.</span></span>
<span data-ttu-id="1e6b3-143">Továbbá a gép van húzza a lekérési egyetlen konfigurációja majd a konfigurációs fájl a lekérési kiszolgálón konfigurációs tárházban kiszolgálószolgáltatás minden olyan fájlnevet rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-143">Moreover, if a machine is pulling a single configuration from a pull server/service then the configuration file on the pull server configuration repository can have any file name.</span></span>
<span data-ttu-id="1e6b3-144">Erre a rugalmasságra elnevezési kezelését teszi a csomópontok részben Azure Automation szolgáltatás, ahol egyes a csomópont konfigurációs várható az Azure Automation DSC és helyileg kezelt részleges konfigurációjával.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-144">This naming flexibility allows you to manage your nodes partially by Azure Automation service, where some configuration for your node is coming from Azure Automation DSC and with a partial configuration that you manage locally.</span></span>

<span data-ttu-id="1e6b3-145">Alább állítja be egy csomópont lehet metakonfigurációját felügyelt mindkét helyileg, valamint által az Azure Automation szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-145">The metaconfiguration below sets up a node to be managed both locally as well as by Azure Automation service.</span></span>

```powershell
[DscLocalConfigurationManager()]
Configuration RegistrationMetaConfig
{
    Settings
    {
        RefreshFrequencyMins = 30
        RefreshMode = "PULL"
    }

    ConfigurationRepositoryWeb web
    {
        ServerURL =  $endPoint
        RegistrationKey = $registrationKey
        ConfigurationNames = $configurationName
    }

    # Partial configuration managed by Azure Automation service.
    PartialConfiguration PartialConfigurationManagedByAzureAutomation
    {
        ConfigurationSource = "[ConfigurationRepositoryWeb]Web"
    }

    # This partial configuration is managed locally.
    PartialConfiguration OnPremisesConfig
    {
        RefreshMode = "PUSH"
        ExclusiveResources = @("Script")
    }

}

RegistrationMetaConfig
Set-DscLocalConfigurationManager -Path .\RegistrationMetaConfig -Verbose
```

## <a name="using-psdscrunascredential-with-dsc-composite-resources"></a><span data-ttu-id="1e6b3-146">PsDscRunAsCredential használata DSC összetett erőforrások</span><span class="sxs-lookup"><span data-stu-id="1e6b3-146">Using PsDscRunAsCredential with DSC composite resources</span></span>

<span data-ttu-id="1e6b3-147">Támogatja az [ *PsDscRunAsCredential* ](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) a DSC [összetett](https://msdn.microsoft.com/en-us/powershell/dsc/authoringresourcecomposite) erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-147">We have added support for using [*PsDscRunAsCredential*](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) with DSC [Composite](https://msdn.microsoft.com/en-us/powershell/dsc/authoringresourcecomposite) resources.</span></span>

<span data-ttu-id="1e6b3-148">Megadhat egy értéket a PsDscRunAsCredential összetett erőforráshoz, konfigurációk használata esetén.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-148">You can now specify a value for PsDscRunAsCredential when using composite resources inside configurations.</span></span>
<span data-ttu-id="1e6b3-149">Megadása esetén összes erőforrás futhat egy összetett erőforrás RunAs felhasználóként.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-149">When specified, all resources run inside a composite resource as a RunAs user.</span></span>
<span data-ttu-id="1e6b3-150">Ha egy összetett erőforrást egy másik összetett erőforrás, az összes erőforrást is végrehajtása RunAs felhasználóként.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-150">If a composite resource calls another composite resource, all of its resources are also executed as RunAs user.</span></span>
<span data-ttu-id="1e6b3-151">RunAs hitelesítő adatok rendszer nem propagál minden összetett erőforrás hierarchia szintje.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-151">RunAs credentials are propagated to any level of the composite resource hierarchy.</span></span>
<span data-ttu-id="1e6b3-152">Ha bármilyen olyan erőforrás összetett erőforrás belül PsDscRunAsCredential saját érték Megadja, egy merge hiba eredménye, konfiguráció fordításakor.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-152">If any resource inside a composite resource specifies its own value for PsDscRunAsCredential, a merge error results during configuration compilation.</span></span>

<span data-ttu-id="1e6b3-153">Ez a példa bemutatja a használati [WindowsFeatureSet](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_newresources) összetett erőforrás PSDesiredStateConfiguration modulban.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-153">This example shows usage with [WindowsFeatureSet](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_newresources) composite resource included in PSDesiredStateConfiguration module.</span></span>

```powershell
Configuration InstallWindowsFeature
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        WindowsFeatureSet features
        {
            Name = @("Telnet-Client","SNMP-Service")
            Ensure = "Present"
            IncludeAllSubFeature = $true
            PsDscRunAsCredential = Get-Credential
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost'
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}

InstallWindowsFeature -ConfigurationData $configData
```

## <a name="dsc-module-and-configuration-signing-validations"></a><span data-ttu-id="1e6b3-154">DSC modul és a konfigurációs ellenőrzések aláírása</span><span class="sxs-lookup"><span data-stu-id="1e6b3-154">DSC module and configuration signing validations</span></span>

<span data-ttu-id="1e6b3-155">A DSC konfiguráció és a modulok terjesztése a kezelt számítógépek számára a lekérési kiszolgálójáról.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-155">In DSC, configurations and modules are distributed to managed computers from the pull server.</span></span>
<span data-ttu-id="1e6b3-156">Ha a lekérési kiszolgálójával biztonsága sérül, a támadó potenciálisan módosíthatja a konfigurációkat és a modulok a lekérési kiszolgálón és kell terjeszteni az összes felügyelt csomóponthoz, az összes veszélyeztetése.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-156">If the pull server is compromised, an attacker can potentially modify the configurations and modules on the pull server and have it distributed to all managed nodes, compromising all of them.</span></span>

<span data-ttu-id="1e6b3-157">A WMF 5.1 DSC támogatja a katalógus és konfigurációs digitális aláírások ellenőrzése (. MOF) formátumú fájlok.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-157">In WMF 5.1, DSC supports validating the digital signatures on catalog and configuration (.MOF) files.</span></span>
<span data-ttu-id="1e6b3-158">Ez a szolgáltatás megakadályozza, hogy a csomópontok a konfigurációk vagy fájlok modul, amely nem egy megbízható aláíró aláírásával, vagy amely illetéktelenül után megbízható aláíró által aláírt végrehajtása.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-158">This feature prevents nodes from executing configurations or module files which are not signed by a trusted signer or which have been tampered with after they have been signed by trusted signer.</span></span>

### <a name="how-to-sign-configuration-and-module"></a><span data-ttu-id="1e6b3-159">Csatlakozás a konfigurációs és modul</span><span class="sxs-lookup"><span data-stu-id="1e6b3-159">How to sign configuration and module</span></span>

***
* <span data-ttu-id="1e6b3-160">Konfigurációs fájlok (. MOF-ot): A meglévő PowerShell-parancsmag [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) ki van bővítve a MOF-fájlok aláírása támogatásához.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-160">Configuration Files (.MOFs): The existing PowerShell cmdlet [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) is extended to support signing of MOF files.</span></span>
* <span data-ttu-id="1e6b3-161">Modulok: Ha bejelentkezik a megfelelő modul katalógus az alábbi lépéseket követve modulok aláírása történik:</span><span class="sxs-lookup"><span data-stu-id="1e6b3-161">Modules: Signing of modules is done by signing the corresponding module catalog using the following steps:</span></span>
    1. <span data-ttu-id="1e6b3-162">Hozzon létre egy katalógusfájlt: egy katalógusfájlt kriptográfiai kivonatokat vagy ujjlenyomatok gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-162">Create a catalog file: A catalog file contains a collection of cryptographic hashes or thumbprints.</span></span>
       <span data-ttu-id="1e6b3-163">Minden egyes ujjlenyomat felel meg egy fájlt, amely a moduljában található.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-163">Each thumbprint corresponds to a file that is included in the module.</span></span>
       <span data-ttu-id="1e6b3-164">A következő új parancsmagját [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), engedélyezése a felhasználók számára hozzon létre egy katalógusfájlt az a modul hozzá lett adva.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-164">The new cmdlet [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), has been added to enable users to create a catalog file for their module.</span></span>
    2. <span data-ttu-id="1e6b3-165">A katalógus-fájl aláírásához: használata [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) a katalógus-fájl aláírásához.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-165">Sign the catalog file: Use [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) to sign the catalog file.</span></span>
    3. <span data-ttu-id="1e6b3-166">Helyezze a katalógus fájlt a modul mappában található.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-166">Place the catalog file inside the module folder.</span></span>
<span data-ttu-id="1e6b3-167">Szabály szerint modul katalógusfájlt a modul neve megegyezik a modul a mappában kell helyezni.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-167">By convention, module catalog file should be placed under the module folder with the same name as the module.</span></span>

### <a name="localconfigurationmanager-settings-to-enable-signing-validations"></a><span data-ttu-id="1e6b3-168">LocalConfigurationManager beállítások aláíró érvényesítést engedélyezése</span><span class="sxs-lookup"><span data-stu-id="1e6b3-168">LocalConfigurationManager settings to enable signing validations</span></span>

#### <a name="pull"></a><span data-ttu-id="1e6b3-169">Lekéréses</span><span class="sxs-lookup"><span data-stu-id="1e6b3-169">Pull</span></span>

<span data-ttu-id="1e6b3-170">A csomópont LocalConfigurationManager modulok és a jelenlegi beállításai alapján a konfigurációk aláírási érvényesítést végez.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-170">The LocalConfigurationManager of a node performs signing validation of modules and configurations based on its current settings.</span></span>
<span data-ttu-id="1e6b3-171">Az aláírás érvényesítése alapértelmezés szerint le van tiltva.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-171">By default, signature validation is disabled.</span></span>
<span data-ttu-id="1e6b3-172">Az aláírás érvényesítése a "SignatureValidation" blokk hozzáadásával a csomópont látható az alábbi meta-konfiguráció definíciójának engedélyezhető:</span><span class="sxs-lookup"><span data-stu-id="1e6b3-172">Signature validation can enabled by adding the ‘SignatureValidation’ block to the meta-configuration definition of the node as shown below:</span></span>

```powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PULL'
    }

    ConfigurationRepositoryWeb pullserver{
      ConfigurationNames = 'sql'
      ServerURL = 'http://localhost:8080/PSDSCPullServer/PSDSCPullServer.svc'
      AllowUnsecureConnection = $true
      RegistrationKey = 'd6750ff1-d8dd-49f7-8caf-7471ea9793fc' # Replace this with correct registration key.
    }
    SignatureValidation validations{
        # If the TrustedStorePath property is provided then LCM will use the custom path. Otherwise, the LCM will use default trusted store path (Cert:\LocalMachine\DSCStore) to find the signing certificate.
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType = 'Configuration','Module'         # This is a list of DSC artifacts, for which LCM need to verify their digital signature before executing them on the node.
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
```

<span data-ttu-id="1e6b3-173">A fenti metakonfigurációját beállítása a csomópont lehetővé teszi, hogy a letöltött konfigurációk és a modulok aláírás érvényesítése.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-173">Setting the above metaconfiguration on a node enables signature validation on downloaded configurations and modules.</span></span>
<span data-ttu-id="1e6b3-174">A helyi Configuration Manager végrehajtja a következő lépéseket a digitális aláírások ellenőrzése.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-174">The Local Configuration Manager performs the following steps to verify the digital signatures.</span></span>

1. <span data-ttu-id="1e6b3-175">Ellenőrizze a konfigurációs fájl aláírását (. MOF) érvénytelen.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-175">Verify the signature on a configuration file (.MOF) is valid.</span></span>
   <span data-ttu-id="1e6b3-176">A PowerShell-parancsmagot használja [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), amely ki van bővítve 5.1 MOF aláírás érvényesítése támogatásához.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-176">It uses the PowerShell cmdlet [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), which is extended in 5.1 to support MOF signature validation.</span></span>
2. <span data-ttu-id="1e6b3-177">Ellenőrizze, hogy a hitelesítésszolgáltató, amely jogosult az aláíró megbízható-e.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-177">Verify the certificate authority that authorized the signer is trusted.</span></span>
3. <span data-ttu-id="1e6b3-178">A konfiguráció modul/erőforrás-függőségek letöltése egy ideiglenes helyre.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-178">Download module/resource dependencies of the configuration to a temp location.</span></span>
4. <span data-ttu-id="1e6b3-179">A katalógus, a modul bekerüljön aláírásának ellenőrzése.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-179">Verify the signature of the catalog included inside the module.</span></span>
    * <span data-ttu-id="1e6b3-180">Keresés a `<moduleName>.cat` fájlt, és ellenőrizze a parancsmaggal aláírásának [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e6b3-180">Find a `<moduleName>.cat` file and verify its signature using the cmdlet  [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).</span></span>
    * <span data-ttu-id="1e6b3-181">Ellenőrizze, hogy a hitelesített az aláíró hitelesítésszolgáltatót megbízható-e.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-181">Verify the certification authority that authenticated the signer is trusted.</span></span>
    * <span data-ttu-id="1e6b3-182">Ellenőrizze, hogy a modul tartalma nem változott az új parancsmaggal [teszt-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e6b3-182">Verify the content of the modules has not been tampered using the new cmdlet [Test-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).</span></span>
5. <span data-ttu-id="1e6b3-183">Install-modul $env: ProgramFiles\WindowsPowerShell\Modules\\</span><span class="sxs-lookup"><span data-stu-id="1e6b3-183">Install-Module to $env:ProgramFiles\WindowsPowerShell\Modules\\</span></span>
6. <span data-ttu-id="1e6b3-184">A konfigurációs folyamat</span><span class="sxs-lookup"><span data-stu-id="1e6b3-184">Process configuration</span></span>

> <span data-ttu-id="1e6b3-185">Megjegyzés: Az aláírás érvényesítése modul-katalógus és konfigurációs csak hajtható végre, ha a konfigurációs alkalmazza a rendszer először, vagy ha a modul letöltése és telepítése.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-185">Note: Signature validation on module-catalog and configuration is only performed when the configuration is applied to the system for the first time or when the module is downloaded and installed.</span></span>
<span data-ttu-id="1e6b3-186">Konzisztencia futtatása nem ellenőrzik az aláírás Current.mof vagy modul függőségeit.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-186">Consistency runs do not validate the signature of Current.mof or its module dependencies.</span></span>
<span data-ttu-id="1e6b3-187">Ellenőrzése nem sikerült fel, ha például ha a konfigurációs lekért a lekérési kiszolgálójával nincs aláírva, majd a konfiguráció feldolgozása leáll, a hiba alább látható és az ideiglenes fájlok törlődnek.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-187">If verification has failed at any stage, for instance, if the configuration pulled from the pull server is unsigned, then processing of the configuration terminates with the error shown below and all temporary files are deleted.</span></span>

![Minta kimenet Hibakonfigurációját](../images/PullUnsignedConfigFail.png)

<span data-ttu-id="1e6b3-189">Hasonlóképpen húzza egy modult, amelynek a katalógus nem aláírt eredménye a következő hiba:</span><span class="sxs-lookup"><span data-stu-id="1e6b3-189">Similarly, pulling a module whose catalog is not signed results in the following error:</span></span>

![A minta hiba kimenetigyorsítótár-modul](../images/PullUnisgnedCatalog.png)

#### <a name="push"></a><span data-ttu-id="1e6b3-191">Leküldéses</span><span class="sxs-lookup"><span data-stu-id="1e6b3-191">Push</span></span>

<span data-ttu-id="1e6b3-192">Egy leküldéses keresztül konfigurációs előfordulhat, hogy lehessen illetéktelenül módosítani a forrásnál, mielőtt azt a csomópont.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-192">A configuration delivered by using push might be tampered with at its source before it delivered to the node.</span></span>
<span data-ttu-id="1e6b3-193">A helyi Configuration Manager hasonló aláírás érvényesítése lépéseket megnyomott vagy közzétett beállítás(ok) hajt végre.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-193">The Local Configuration Manager performs similar signature validation steps for pushed or published configuration(s).</span></span>
<span data-ttu-id="1e6b3-194">Alább van az aláírás érvényesítése leküldéses átfogó példát.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-194">Below is a complete example of signature validation for push.</span></span>

- <span data-ttu-id="1e6b3-195">A csomópont aláírás-ellenőrzés engedélyezése.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-195">Enable signature validation on the node.</span></span>

```powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PUSH'
    }
    SignatureValidation validations{
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType =  'Configuration','Module'
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
```

- <span data-ttu-id="1e6b3-196">Hozzon létre egy minta konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-196">Create a sample configuration file.</span></span>

```powershell
# Sample configuration
Configuration Test
{

    File foo
    {
        DestinationPath =  "$env:TEMP\signingTest.txt"
        Contents = "ABC"
    }
}
Test
```

- <span data-ttu-id="1e6b3-197">Próbálja meg a nem aláírt konfigurációs fájl küldését csomóponthoz.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-197">Try pushing the unsigned configuration file in to the node.</span></span>

```powershell
Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
```

![ErrorUnsignedMofPushed](../images/PushUnsignedMof.png)

- <span data-ttu-id="1e6b3-199">A konfigurációs fájl kódaláíró tanúsítvánnyal aláírásához.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-199">Sign the configuration file using code-signing certificate.</span></span>

![SignMofFile](../images/SignMofFile.png)

- <span data-ttu-id="1e6b3-201">Próbálja küldését a MOF-fájlját.</span><span class="sxs-lookup"><span data-stu-id="1e6b3-201">Try pushing the signed MOF file.</span></span>

![SignMofFile](../images/PushSignedMof.png)
