---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 DSC fejlesztései
ms.openlocfilehash: 92f82d62550e105a187fd7c0c58b49367c646a7e
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523042"
---
# <a name="improvements-in-desired-state-configuration-dsc-in-wmf-51"></a><span data-ttu-id="c81a7-103">A Desired State Configuration (DSC) a WMF 5.1 fejlesztései</span><span class="sxs-lookup"><span data-stu-id="c81a7-103">Improvements in Desired State Configuration (DSC) in WMF 5.1</span></span>

## <a name="dsc-class-resource-improvements"></a><span data-ttu-id="c81a7-104">DSC osztály erőforrás fejlesztései</span><span class="sxs-lookup"><span data-stu-id="c81a7-104">DSC class resource improvements</span></span>

<span data-ttu-id="c81a7-105">A WMF 5.1 hogy kijavítása az alábbi ismert problémák:</span><span class="sxs-lookup"><span data-stu-id="c81a7-105">In WMF 5.1, we have fixed the following known issues:</span></span>

- <span data-ttu-id="c81a7-106">Ha egy összetett/kivonat táblatípus osztályalapú DSC-erőforrás Get() függvény által visszaadott Get-DscConfiguration üres (null) értékeket, vagy hibát adhat vissza.</span><span class="sxs-lookup"><span data-stu-id="c81a7-106">Get-DscConfiguration may return empty values (null) or errors if a complex/hash table type is returned by Get() function of a class-based DSC resource.</span></span>
- <span data-ttu-id="c81a7-107">Get-DscConfiguration hibát ad vissza, ha a RunAs hitelesítő adatok a DSC-konfiguráció használatban van.</span><span class="sxs-lookup"><span data-stu-id="c81a7-107">Get-DscConfiguration returns error if RunAs credential is used in DSC configuration.</span></span>
- <span data-ttu-id="c81a7-108">Osztályalapú erőforrás összetett konfigurációban nem használható.</span><span class="sxs-lookup"><span data-stu-id="c81a7-108">Class-based resource cannot be used in a composite configuration.</span></span>
- <span data-ttu-id="c81a7-109">Start-DscConfiguration lefagy, ha a osztályalapú erőforrás rendelkezik egy tulajdonságot a saját típusú.</span><span class="sxs-lookup"><span data-stu-id="c81a7-109">Start-DscConfiguration hangs if class-based resource has a property of its own type.</span></span>
- <span data-ttu-id="c81a7-110">Osztály-alapú erőforrás-kizárólagos erőforrásként nem használható.</span><span class="sxs-lookup"><span data-stu-id="c81a7-110">Class-based resource cannot be used as an exclusive resource.</span></span>

## <a name="dsc-resource-debugging-improvements"></a><span data-ttu-id="c81a7-111">DSC-erőforrás hibakeresési javításai</span><span class="sxs-lookup"><span data-stu-id="c81a7-111">DSC resource debugging improvements</span></span>

<span data-ttu-id="c81a7-112">A WMF 5.0-a PowerShell-hibakereső nem állt le, az osztály-alapú erőforrás metódus (Get/Set/Test) közvetlenül.</span><span class="sxs-lookup"><span data-stu-id="c81a7-112">In WMF 5.0, the PowerShell debugger did not stop at the class-based resource method (Get/Set/Test) directly.</span></span>
<span data-ttu-id="c81a7-113">A WMF 5.1-es a hibakereső megáll az osztály-alapú erőforrás módszer ugyanúgy, mint a MOF-alapú erőforrások módszerek az.</span><span class="sxs-lookup"><span data-stu-id="c81a7-113">In WMF 5.1, the debugger stops at the class-based resource method in the same way as for MOF-based resources methods.</span></span>

## <a name="dsc-pull-client-supports-tls-11-and-tls-12"></a><span data-ttu-id="c81a7-114">DSC lekérési ügyfél támogatja a TLS 1.1 és TLS 1.2</span><span class="sxs-lookup"><span data-stu-id="c81a7-114">DSC pull client supports TLS 1.1 and TLS 1.2</span></span>

<span data-ttu-id="c81a7-115">Korábban a DSC lekérési ügyfél csak támogatott SSL3.0 és TLS1.0 HTTPS-kapcsolaton keresztül.</span><span class="sxs-lookup"><span data-stu-id="c81a7-115">Previously, the DSC pull client only supported SSL3.0 and TLS1.0 over HTTPS connections.</span></span>
<span data-ttu-id="c81a7-116">Kényszerített biztonságosabb protokollokra, ha a lekérési ügyfél lenne működni.</span><span class="sxs-lookup"><span data-stu-id="c81a7-116">When forced to use more secure protocols, the pull client would stop functioning.</span></span>
<span data-ttu-id="c81a7-117">A WMF 5.1-es a DSC lekérési ügyfél már nem támogatja az SSL 3.0 és a biztonságosabb a TLS 1.1 és TLS 1.2 protokoll támogatása.</span><span class="sxs-lookup"><span data-stu-id="c81a7-117">In WMF 5.1, the DSC pull client no longer supports SSL 3.0 and adds support for the more secure TLS 1.1 and TLS 1.2 protocols.</span></span>

## <a name="improved-pull-server-registration"></a><span data-ttu-id="c81a7-118">Továbbfejlesztett lekéréses kiszolgáló regisztrálása</span><span class="sxs-lookup"><span data-stu-id="c81a7-118">Improved pull server registration</span></span>

<span data-ttu-id="c81a7-119">A WMF korábbi verzióiban egyidejű regisztrációk/reporting kéréseket a ESENT adatbázis használatakor DSC lekéréses kiszolgálóra LCM regisztrálása és/vagy a jelentés sikertelen vezetne.</span><span class="sxs-lookup"><span data-stu-id="c81a7-119">In the earlier versions of WMF, simultaneous registrations/reporting requests to a DSC pull server while using the ESENT database would lead to LCM failing to register and/or report.</span></span>
<span data-ttu-id="c81a7-120">Ezekben az esetekben az Eseménynapló bejegyzéseit, a lekérési kiszolgálón rendelkezik a hiba "Példány neve már használatban van."</span><span class="sxs-lookup"><span data-stu-id="c81a7-120">In such cases, the event logs on the pull server has the error "Instance Name already in use."</span></span>
<span data-ttu-id="c81a7-121">Több szálon futó forgatókönyvekben ESENT-adatbázisának eléréséhez használt helytelen mintát okozta.</span><span class="sxs-lookup"><span data-stu-id="c81a7-121">This was due to an incorrect pattern being used to access the ESENT database in a multi-threaded scenario.</span></span>
<span data-ttu-id="c81a7-122">A WMF 5.1 Ez a hiba elhárítása.</span><span class="sxs-lookup"><span data-stu-id="c81a7-122">In WMF 5.1, this issue has been fixed.</span></span>
<span data-ttu-id="c81a7-123">Egyidejű vagy a reporting (ESENT adatbázist érintő) jól működik, a WMF 5.1-es.</span><span class="sxs-lookup"><span data-stu-id="c81a7-123">Concurrent registrations or reporting (involving ESENT database) works fine in WMF 5.1.</span></span>
<span data-ttu-id="c81a7-124">Ez a probléma csak a ESENT adatbázis használható, és nem vonatkozik az OLEDB-adatbázishoz.</span><span class="sxs-lookup"><span data-stu-id="c81a7-124">This issue is applicable only to the ESENT database and does not apply to the OLEDB database.</span></span>

## <a name="enable-circular-log-on-esent-database-instance"></a><span data-ttu-id="c81a7-125">A ESENT adatbázispéldány körkörös napló engedélyezése</span><span class="sxs-lookup"><span data-stu-id="c81a7-125">Enable Circular log on ESENT database instance</span></span>

<span data-ttu-id="c81a7-126">DSC-PullServer eariler verziójában a ESENT adatbázis-naplófájlokat is betelik a pullserver becouse az adatbázis-példány létrehozása nélkül a körkörös naplózást, a lemezterület.</span><span class="sxs-lookup"><span data-stu-id="c81a7-126">In eariler version of DSC-PullServer, the ESENT database log files were filling up the disk space of the pullserver becouse the database instance was being created without circular logging.</span></span> <span data-ttu-id="c81a7-127">Ebben a kiadásban lehetősége van a körkörös naplózás viselkedése a példányon a pullserver web.config szabályozására.</span><span class="sxs-lookup"><span data-stu-id="c81a7-127">In this release, you have the option to control the circular logging behavior of the instance using the web.config of the pullserver.</span></span> <span data-ttu-id="c81a7-128">Alapértelmezés szerint CircularLogging TRUE értékre van állítva.</span><span class="sxs-lookup"><span data-stu-id="c81a7-128">By default CircularLogging is set to TRUE.</span></span>

```
<appSettings>
    <add key="dbprovider" value="ESENT" />
    <add key="dbconnectionstr" value="C:\Program Files\WindowsPowerShell\DscService\Devices.edb" />
    <add key="CheckpointDepthMaxKB" value="512" />
    <add key="UseCircularESENTLogs" value="TRUE" />
  </appSettings>
```

## <a name="pull-partial-configuration-naming-convention"></a><span data-ttu-id="c81a7-129">Kérje le a részleges konfigurációs elnevezési egyezmény</span><span class="sxs-lookup"><span data-stu-id="c81a7-129">Pull partial configuration naming convention</span></span>

<span data-ttu-id="c81a7-130">A korábbi kiadásában egy részleges konfigurációs elnevezési lett, hogy a MOF-fájl neve, a lekéréses/szolgáltatás egyeznie kell a helyi configuration manager elkerülését, amelyek ezután meg kell egyeznie a megadott részben konfiguráció nevével a konfiguráció neve beágyazza a MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="c81a7-130">In the previous release, the naming convention for a partial configuration was that the MOF file name in the pull server/service should match the partial configuration name specified in the local configuration manager settings that in turn must match the configuration name embedded in the MOF file.</span></span>

<span data-ttu-id="c81a7-131">Az alábbi-pillanatképek megtekintéséhez:</span><span class="sxs-lookup"><span data-stu-id="c81a7-131">See the snapshots below:</span></span>

- <span data-ttu-id="c81a7-132">Helyi konfigurációs beállításokat, amely meghatározza egy részleges konfigurációs csomópont fogadására van engedélyezve.</span><span class="sxs-lookup"><span data-stu-id="c81a7-132">Local configuration settings which defines a partial configuration that a node is allowed to receive.</span></span>

![Minta metaconfiguration](../images/MetaConfigPartialOne.png)

- <span data-ttu-id="c81a7-134">Minta részleges konfiguráció definíciója</span><span class="sxs-lookup"><span data-stu-id="c81a7-134">Sample partial configuration definition</span></span>

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

- <span data-ttu-id="c81a7-135">A létrehozott MOF-fájl (ConfigurationName) beágyazott.</span><span class="sxs-lookup"><span data-stu-id="c81a7-135">'ConfigurationName' embedded in the generated MOF file.</span></span>

![Minta létrehozott mof-fájl](../images/PartialGeneratedMof.png)

- <span data-ttu-id="c81a7-137">A konfigurációs lekérési tárházban fájlnév</span><span class="sxs-lookup"><span data-stu-id="c81a7-137">FileName in the pull configuration repository</span></span>

![A konfigurációs adattárhoz fájlnév](../images/PartialInConfigRepository.png)

<span data-ttu-id="c81a7-139">Az Azure Automation szolgáltatás neve MOF-fájlok használata a létrehozott `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="c81a7-139">Azure Automation service name generated MOF files as `<ConfigurationName>.<NodeName>.mof`.</span></span>
<span data-ttu-id="c81a7-140">Ezért az alábbi konfigurációval való PartialOne.localhost.mof lefordítja.</span><span class="sxs-lookup"><span data-stu-id="c81a7-140">So the configuration below compiles to PartialOne.localhost.mof.</span></span>

<span data-ttu-id="c81a7-141">Ez lehetetlenné lekéréses egy részleges konfigurálásakor az Azure Automation szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="c81a7-141">This made it impossible to pull one of your partial configuration from Azure Automation service.</span></span>

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

<span data-ttu-id="c81a7-142">A WMF 5.1-es, a lekéréses/szolgáltatás egy részleges konfigurációt is előtereként `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="c81a7-142">In WMF 5.1, a partial configuration in the pull server/service can be named as `<ConfigurationName>.<NodeName>.mof`.</span></span>
<span data-ttu-id="c81a7-143">Ezen felül egy gép van lehetőség a lekérési egyetlen konfigurációval kiszolgálók/szolgáltatások a lekéréses kiszolgálón konfigurációs adattárhoz majd a konfigurációs fájlt minden olyan fájlnevet rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="c81a7-143">Moreover, if a machine is pulling a single configuration from a pull server/service then the configuration file on the pull server configuration repository can have any file name.</span></span>
<span data-ttu-id="c81a7-144">E elnevezési rugalmasság lehetővé teszi a csomópontok részlegesen kezelése az Azure Automation szolgáltatás, néhány beállítást a csomópont a az Azure Automation DSC és a egy részleges konfigurációval helyileg kezelt forrását.</span><span class="sxs-lookup"><span data-stu-id="c81a7-144">This naming flexibility allows you to manage your nodes partially by Azure Automation service, where some configuration for your node is coming from Azure Automation DSC and with a partial configuration that you manage locally.</span></span>

<span data-ttu-id="c81a7-145">Az alábbi állítja be egy csomópont lehet metaconfiguration felügyelt is helyileg, valamint az Azure Automation által szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="c81a7-145">The metaconfiguration below sets up a node to be managed both locally as well as by Azure Automation service.</span></span>

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

## <a name="using-psdscrunascredential-with-dsc-composite-resources"></a><span data-ttu-id="c81a7-146">Összetett erőforrások DSC PsDscRunAsCredential használata</span><span class="sxs-lookup"><span data-stu-id="c81a7-146">Using PsDscRunAsCredential with DSC composite resources</span></span>

<span data-ttu-id="c81a7-147">Mostantól támogatjuk a [ *PsDscRunAsCredential* ](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) DSC- [összetett](https://msdn.microsoft.com/powershell/dsc/authoringresourcecomposite) erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="c81a7-147">We have added support for using [*PsDscRunAsCredential*](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) with DSC [Composite](https://msdn.microsoft.com/powershell/dsc/authoringresourcecomposite) resources.</span></span>

<span data-ttu-id="c81a7-148">Most már megadhatja egy értéket PsDscRunAsCredential az összetett erőforrások belül konfigurációk használata esetén.</span><span class="sxs-lookup"><span data-stu-id="c81a7-148">You can now specify a value for PsDscRunAsCredential when using composite resources inside configurations.</span></span>
<span data-ttu-id="c81a7-149">Megadása esetén az összes erőforrás belül futó összetett erőforrás futtató felhasználóként.</span><span class="sxs-lookup"><span data-stu-id="c81a7-149">When specified, all resources run inside a composite resource as a RunAs user.</span></span>
<span data-ttu-id="c81a7-150">Ha egy összetett erőforrást egy másik összetett erőforrást, minden erőforrását is végrehajtása futtató felhasználóként.</span><span class="sxs-lookup"><span data-stu-id="c81a7-150">If a composite resource calls another composite resource, all of its resources are also executed as RunAs user.</span></span>
<span data-ttu-id="c81a7-151">RunAs hitelesítő adatokat a rendszer propagálja a webhelyre az összetett erőforrás hierarchia minden szintjére.</span><span class="sxs-lookup"><span data-stu-id="c81a7-151">RunAs credentials are propagated to any level of the composite resource hierarchy.</span></span>
<span data-ttu-id="c81a7-152">Ha bármely erőforrás összetett erőforrás belül a saját értékét PsDscRunAsCredential határozza, akkor egy egyesítési hibát eredményez, konfiguráció fordításakor.</span><span class="sxs-lookup"><span data-stu-id="c81a7-152">If any resource inside a composite resource specifies its own value for PsDscRunAsCredential, a merge error results during configuration compilation.</span></span>

<span data-ttu-id="c81a7-153">Ez a példa bemutatja a használatot a [WindowsFeatureSet](https://msdn.microsoft.com/powershell/wmf/dsc_newresources) PSDesiredStateConfiguration modulban található összetett erőforrást.</span><span class="sxs-lookup"><span data-stu-id="c81a7-153">This example shows usage with [WindowsFeatureSet](https://msdn.microsoft.com/powershell/wmf/dsc_newresources) composite resource included in PSDesiredStateConfiguration module.</span></span>

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

## <a name="dsc-module-and-configuration-signing-validations"></a><span data-ttu-id="c81a7-154">DSC-modul és a konfigurációs ellenőrzések aláírása</span><span class="sxs-lookup"><span data-stu-id="c81a7-154">DSC module and configuration signing validations</span></span>

<span data-ttu-id="c81a7-155">A DSC konfigurációkat és a modulok oszlanak meg a felügyelt számítógépekre a lekérési kiszolgálóról.</span><span class="sxs-lookup"><span data-stu-id="c81a7-155">In DSC, configurations and modules are distributed to managed computers from the pull server.</span></span>
<span data-ttu-id="c81a7-156">A lekéréses kiszolgálón biztonsága sérül, ha egy támadó is potenciálisan módosíthatja a konfigurációkat és a modulok a lekérési kiszolgálón és annak ossza el az összes felügyelt csomópont veszélyeztetése azokat.</span><span class="sxs-lookup"><span data-stu-id="c81a7-156">If the pull server is compromised, an attacker can potentially modify the configurations and modules on the pull server and have it distributed to all managed nodes, compromising all of them.</span></span>

<span data-ttu-id="c81a7-157">A WMF 5.1, DSC támogatja a katalógus és a konfiguráció a digitális aláírások ellenőrzése (. MOF) formátumú fájlok.</span><span class="sxs-lookup"><span data-stu-id="c81a7-157">In WMF 5.1, DSC supports validating the digital signatures on catalog and configuration (.MOF) files.</span></span>
<span data-ttu-id="c81a7-158">Ez a funkció meggátolja, hogy a csomópontok konfigurációk vagy amely nem egy megbízható aláíró által aláírt, vagy amelyek illetéktelenül után megbízható aláíró által aláírt modul fájlok végrehajtása.</span><span class="sxs-lookup"><span data-stu-id="c81a7-158">This feature prevents nodes from executing configurations or module files which are not signed by a trusted signer or which have been tampered with after they have been signed by trusted signer.</span></span>

### <a name="how-to-sign-configuration-and-module"></a><span data-ttu-id="c81a7-159">Csatlakozás a konfigurációs és modul</span><span class="sxs-lookup"><span data-stu-id="c81a7-159">How to sign configuration and module</span></span>

***
* <span data-ttu-id="c81a7-160">Konfigurációs fájlok (. MOF-fájlok): A meglévő PowerShell-parancsmag [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) ki van bővítve a MOF-fájlok-aláírás támogatásához.</span><span class="sxs-lookup"><span data-stu-id="c81a7-160">Configuration Files (.MOFs): The existing PowerShell cmdlet [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) is extended to support signing of MOF files.</span></span>
* <span data-ttu-id="c81a7-161">Modulok: Modulok aláírása végzi el a megfelelő modul katalógus az alábbi lépéseket követve aláíró:</span><span class="sxs-lookup"><span data-stu-id="c81a7-161">Modules: Signing of modules is done by signing the corresponding module catalog using the following steps:</span></span>
    1. <span data-ttu-id="c81a7-162">Hozzon létre egy katalógus fájlt: egy katalógusfájlt kriptográfiai kivonatokat vagy ujjlenyomat gyűjteményét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="c81a7-162">Create a catalog file: A catalog file contains a collection of cryptographic hashes or thumbprints.</span></span>
       <span data-ttu-id="c81a7-163">Minden egyes ujjlenyomat felel meg egy fájlt, amely a modul része.</span><span class="sxs-lookup"><span data-stu-id="c81a7-163">Each thumbprint corresponds to a file that is included in the module.</span></span>
       <span data-ttu-id="c81a7-164">Új parancsmag [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), engedélyezze a felhasználók számára, hogy a modul olyan katalógusfájlt bővült.</span><span class="sxs-lookup"><span data-stu-id="c81a7-164">The new cmdlet [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), has been added to enable users to create a catalog file for their module.</span></span>
    2. <span data-ttu-id="c81a7-165">A katalógus-fájl aláírásához: használata [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) a katalógus-fájl aláírásához.</span><span class="sxs-lookup"><span data-stu-id="c81a7-165">Sign the catalog file: Use [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) to sign the catalog file.</span></span>
    3. <span data-ttu-id="c81a7-166">Helyezze a katalógus-fájlt a modul mappán belül.</span><span class="sxs-lookup"><span data-stu-id="c81a7-166">Place the catalog file inside the module folder.</span></span>
<span data-ttu-id="c81a7-167">Szabályok szerint modul katalógus fájl neve megegyezik a modul az a modul mappában kell elhelyezni.</span><span class="sxs-lookup"><span data-stu-id="c81a7-167">By convention, module catalog file should be placed under the module folder with the same name as the module.</span></span>

### <a name="localconfigurationmanager-settings-to-enable-signing-validations"></a><span data-ttu-id="c81a7-168">Aláírás-ellenőrzés engedélyezése LocalConfigurationManager beállításai</span><span class="sxs-lookup"><span data-stu-id="c81a7-168">LocalConfigurationManager settings to enable signing validations</span></span>

#### <a name="pull"></a><span data-ttu-id="c81a7-169">A lekéréses</span><span class="sxs-lookup"><span data-stu-id="c81a7-169">Pull</span></span>

<span data-ttu-id="c81a7-170">A csomópont a LocalConfigurationManager aláíró érvényesítési modulok és konfigurációk a jelenlegi beállításai alapján hajt végre.</span><span class="sxs-lookup"><span data-stu-id="c81a7-170">The LocalConfigurationManager of a node performs signing validation of modules and configurations based on its current settings.</span></span>
<span data-ttu-id="c81a7-171">Aláírás-ellenőrzése alapértelmezés szerint le van tiltva.</span><span class="sxs-lookup"><span data-stu-id="c81a7-171">By default, signature validation is disabled.</span></span>
<span data-ttu-id="c81a7-172">Aláírás-ellenőrzése a "SignatureValidation" blokk hozzáadásával a csomópont látható az alábbi meta-konfiguráció definíciójának engedélyezhető:</span><span class="sxs-lookup"><span data-stu-id="c81a7-172">Signature validation can enabled by adding the ‘SignatureValidation’ block to the meta-configuration definition of the node as shown below:</span></span>

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

<span data-ttu-id="c81a7-173">A csomópont a fenti metaconfiguration beállítás lehetővé teszi, hogy a letöltött konfigurációkat és a modulok az aláírás-ellenőrzése.</span><span class="sxs-lookup"><span data-stu-id="c81a7-173">Setting the above metaconfiguration on a node enables signature validation on downloaded configurations and modules.</span></span>
<span data-ttu-id="c81a7-174">A Local Configuration Manager végrehajtja a következő lépéseket a digitális aláírások ellenőrzése.</span><span class="sxs-lookup"><span data-stu-id="c81a7-174">The Local Configuration Manager performs the following steps to verify the digital signatures.</span></span>

1. <span data-ttu-id="c81a7-175">A konfigurációs fájl aláírásának ellenőrzése (. MOF) formátumú érvényességét.</span><span class="sxs-lookup"><span data-stu-id="c81a7-175">Verify the signature on a configuration file (.MOF) is valid.</span></span>
   <span data-ttu-id="c81a7-176">A PowerShell-parancsmagot használja [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), amely ki van bővítve a 5.1 támogatása a MOF-aláírás-ellenőrzése.</span><span class="sxs-lookup"><span data-stu-id="c81a7-176">It uses the PowerShell cmdlet [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), which is extended in 5.1 to support MOF signature validation.</span></span>
2. <span data-ttu-id="c81a7-177">Ellenőrizze, hogy jogosult az aláíró hitelesítésszolgáltató megbízható-e.</span><span class="sxs-lookup"><span data-stu-id="c81a7-177">Verify the certificate authority that authorized the signer is trusted.</span></span>
3. <span data-ttu-id="c81a7-178">Töltse le a konfigurációs modul és az erőforrások függőségeinek egy ideiglenes helyre.</span><span class="sxs-lookup"><span data-stu-id="c81a7-178">Download module/resource dependencies of the configuration to a temp location.</span></span>
4. <span data-ttu-id="c81a7-179">A katalógus tartalmazza a modulban aláírásának ellenőrzésére.</span><span class="sxs-lookup"><span data-stu-id="c81a7-179">Verify the signature of the catalog included inside the module.</span></span>
    * <span data-ttu-id="c81a7-180">Keresse meg a `<moduleName>.cat` fájlt, és ellenőrizze a parancsmag segítségével aláírását [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).</span><span class="sxs-lookup"><span data-stu-id="c81a7-180">Find a `<moduleName>.cat` file and verify its signature using the cmdlet  [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).</span></span>
    * <span data-ttu-id="c81a7-181">Ellenőrizze, hogy a hitelesített az aláíró hitelesítésszolgáltatót megbízható-e.</span><span class="sxs-lookup"><span data-stu-id="c81a7-181">Verify the certification authority that authenticated the signer is trusted.</span></span>
    * <span data-ttu-id="c81a7-182">Ellenőrizze, hogy a modul tartalma nem módosították az új parancsmaggal [Test-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).</span><span class="sxs-lookup"><span data-stu-id="c81a7-182">Verify the content of the modules has not been tampered using the new cmdlet [Test-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).</span></span>
5. <span data-ttu-id="c81a7-183">Install-Module $env való: ProgramFiles\WindowsPowerShell\Modules\\</span><span class="sxs-lookup"><span data-stu-id="c81a7-183">Install-Module to $env:ProgramFiles\WindowsPowerShell\Modules\\</span></span>
6. <span data-ttu-id="c81a7-184">A konfigurációs folyamat</span><span class="sxs-lookup"><span data-stu-id="c81a7-184">Process configuration</span></span>

> <span data-ttu-id="c81a7-185">Megjegyzés: A modul-katalógus és konfigurációs aláírás-ellenőrzése csak történik, amikor a konfiguráció alkalmazása a rendszer először, vagy ha a modul letöltését és telepítését.</span><span class="sxs-lookup"><span data-stu-id="c81a7-185">Note: Signature validation on module-catalog and configuration is only performed when the configuration is applied to the system for the first time or when the module is downloaded and installed.</span></span>
<span data-ttu-id="c81a7-186">Konzisztencia-futtatások nem ellenőrzik az aláírás Current.mof vagy a modul függőségeit.</span><span class="sxs-lookup"><span data-stu-id="c81a7-186">Consistency runs do not validate the signature of Current.mof or its module dependencies.</span></span>
<span data-ttu-id="c81a7-187">Ellenőrzése nem sikerült minden fázisban, ha például ha a konfiguráció az abból lekért a lekéréses kiszolgálón nincs aláírva, majd az alábbi hiba miatt leállítja a konfiguráció feldolgozása és az ideiglenes fájlok törlése.</span><span class="sxs-lookup"><span data-stu-id="c81a7-187">If verification has failed at any stage, for instance, if the configuration pulled from the pull server is unsigned, then processing of the configuration terminates with the error shown below and all temporary files are deleted.</span></span>

![Példa hiba kimeneti konfigurációja](../images/PullUnsignedConfigFail.png)

<span data-ttu-id="c81a7-189">Hasonlóképpen egy modult, amelynek a katalógus nincs lehetőség aláírt a következő hibaüzenetet eredményezi:</span><span class="sxs-lookup"><span data-stu-id="c81a7-189">Similarly, pulling a module whose catalog is not signed results in the following error:</span></span>

![Minta hiba kimeneti modul](../images/PullUnisgnedCatalog.png)

#### <a name="push"></a><span data-ttu-id="c81a7-191">Leküldéses</span><span class="sxs-lookup"><span data-stu-id="c81a7-191">Push</span></span>

<span data-ttu-id="c81a7-192">Ügyfélleküldés használatával kommunikálásra előfordulhat, hogy lehessen illetéktelenül módosítani a forrásban mielőtt megkapná a csomópont azt.</span><span class="sxs-lookup"><span data-stu-id="c81a7-192">A configuration delivered by using push might be tampered with at its source before it delivered to the node.</span></span>
<span data-ttu-id="c81a7-193">A Local Configuration Manager leküldött vagy közzétett beállítás(ok) aláírás-ellenőrzés hasonló lépéseket hajtja végre.</span><span class="sxs-lookup"><span data-stu-id="c81a7-193">The Local Configuration Manager performs similar signature validation steps for pushed or published configuration(s).</span></span>
<span data-ttu-id="c81a7-194">Alább az aláírás-ellenőrzése leküldés teljes példát.</span><span class="sxs-lookup"><span data-stu-id="c81a7-194">Below is a complete example of signature validation for push.</span></span>

- <span data-ttu-id="c81a7-195">Engedélyezze az aláírás-ellenőrzése a csomóponton.</span><span class="sxs-lookup"><span data-stu-id="c81a7-195">Enable signature validation on the node.</span></span>

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

- <span data-ttu-id="c81a7-196">Hozzon létre egy minta konfigurációs fájlt.</span><span class="sxs-lookup"><span data-stu-id="c81a7-196">Create a sample configuration file.</span></span>

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

- <span data-ttu-id="c81a7-197">Próbálja ki a nem aláírt konfigurációs fájlt leküldése a csomópontot.</span><span class="sxs-lookup"><span data-stu-id="c81a7-197">Try pushing the unsigned configuration file in to the node.</span></span>

```powershell
Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
```

![ErrorUnsignedMofPushed](../images/PushUnsignedMof.png)

- <span data-ttu-id="c81a7-199">A konfigurációs fájl használatával kódaláíró tanúsítvány aláírására.</span><span class="sxs-lookup"><span data-stu-id="c81a7-199">Sign the configuration file using code-signing certificate.</span></span>

![SignMofFile](../images/SignMofFile.png)

- <span data-ttu-id="c81a7-201">Próbálja ki, hogyan lehet továbbítani rá az aláírt MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="c81a7-201">Try pushing the signed MOF file.</span></span>

![SignMofFile](../images/PushSignedMof.png)
