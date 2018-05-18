---
ms.date: 04/11/2018
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC SMB-lekérési kiszolgálójának beállítása
ms.openlocfilehash: 92c03c99afd612fa2b5475e8c26991ff080584e9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="setting-up-a-dsc-smb-pull-server"></a><span data-ttu-id="1f061-103">A DSC SMB-lekérési kiszolgálójának beállítása</span><span class="sxs-lookup"><span data-stu-id="1f061-103">Setting up a DSC SMB pull server</span></span>

><span data-ttu-id="1f061-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="1f061-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f061-105">A lekéréses kiszolgáló (Windows-szolgáltatás *DSC-szolgáltatás*), Windows Server támogatott összetevője létezik azonban a következők: nem tervezi, hogy új funkciók és képességek kínálnak.</span><span class="sxs-lookup"><span data-stu-id="1f061-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="1f061-106">Javasoljuk, hogy kezdje a Váltás felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (tartalmazza a Windows Server-kiszolgáló lekéréses is) vagy a közösségi megoldásoknak a valamelyikét felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="1f061-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="1f061-107">A DSC [SMB](https://technet.microsoft.com/library/hh831795.aspx) lekéréses kiszolgáló egy olyan DSC konfigurációs fájlokat és a DSC-erőforrások számára elérhetővé tenni célcsomópontokat, ha azokat a csomópontokat, kérje meg őket az SMB-fájlmegosztások futtató számítógép.</span><span class="sxs-lookup"><span data-stu-id="1f061-107">A DSC [SMB](https://technet.microsoft.com/library/hh831795.aspx) pull server is a computer hosting SMB file shares that make DSC configuration files and DSC resources available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="1f061-108">A DSC használandó lekéréses SMB-kiszolgálón, akkor kell:</span><span class="sxs-lookup"><span data-stu-id="1f061-108">To use an SMB pull server for DSC, you have to:</span></span>
- <span data-ttu-id="1f061-109">Állítson be olyan kiszolgálón PowerShell 4.0-s vagy újabb SMB-fájlmegosztásra</span><span class="sxs-lookup"><span data-stu-id="1f061-109">Set up an SMB file share on a server running PowerShell 4.0 or higher</span></span>
- <span data-ttu-id="1f061-110">Az adott SMB-megosztás lekéréses 4.0-s vagy újabb rendszerű a PowerShell ügyfél konfigurálása</span><span class="sxs-lookup"><span data-stu-id="1f061-110">Configure a client running PowerShell 4.0 or higher to pull from that SMB share</span></span>

## <a name="using-the-xsmbshare-resource-to-create-an-smb-file-share"></a><span data-ttu-id="1f061-111">SMB-fájlmegosztás létrehozása a xSmbShare erőforrás használatával</span><span class="sxs-lookup"><span data-stu-id="1f061-111">Using the xSmbShare resource to create an SMB file share</span></span>

<span data-ttu-id="1f061-112">Nincsenek többféleképpen SMB-fájlmegosztás beállítása azonban nézzük hogyan ehhez DSC használatával.</span><span class="sxs-lookup"><span data-stu-id="1f061-112">There are a number of ways to set up an SMB file share, but let's look at how you can do this by using DSC.</span></span>

### <a name="install-the-xsmbshare-resource"></a><span data-ttu-id="1f061-113">Telepítse a xSmbShare erőforrás</span><span class="sxs-lookup"><span data-stu-id="1f061-113">Install the xSmbShare resource</span></span>

<span data-ttu-id="1f061-114">Hívja a [Install-modul](https://technet.microsoft.com/library/dn807162.aspx) telepítésére szolgáló parancsmagot a **xSmbShare** modul.</span><span class="sxs-lookup"><span data-stu-id="1f061-114">Call the [Install-Module](https://technet.microsoft.com/library/dn807162.aspx) cmdlet to install the **xSmbShare** module.</span></span>
><span data-ttu-id="1f061-115">**Megjegyzés:**: **Install-modul** megtalálható a **PowerShellGet** modul, amely PowerShell 5.0 szerepel.</span><span class="sxs-lookup"><span data-stu-id="1f061-115">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="1f061-116">Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modulok előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="1f061-116">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span> <span data-ttu-id="1f061-117">A **xSmbShare** tartalmazza a DSC-erőforrás **xSmbShare**, amelyek segítségével az SMB-fájlmegosztás létrehozása.</span><span class="sxs-lookup"><span data-stu-id="1f061-117">The **xSmbShare** contains the DSC resource **xSmbShare**, which can be used to create an SMB file share.</span></span>

### <a name="create-the-directory-and-file-share"></a><span data-ttu-id="1f061-118">A könyvtár- és fájlmegosztás létrehozása</span><span class="sxs-lookup"><span data-stu-id="1f061-118">Create the directory and file share</span></span>

<span data-ttu-id="1f061-119">A következő konfigurációt használja a [fájl](fileResource.md) a megosztáshoz a következő könyvtár létrehozásakor erőforrás és a **xSmbShare** erőforrás az SMB-megosztás beállítása:</span><span class="sxs-lookup"><span data-stu-id="1f061-119">The following configuration uses the [File](fileResource.md) resource to create the directory for the share and the **xSmbShare** resource to set up the SMB share:</span></span>

```powershell
Configuration SmbShare {

Import-DscResource -ModuleName PSDesiredStateConfiguration
Import-DscResource -ModuleName xSmbShare

    Node localhost {

        File CreateFolder {

            DestinationPath = 'C:\DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'

        }

        xSMBShare CreateShare {

            Name = 'DscSmbShare'
            Path = 'C:\DscSmbShare'
            FullAccess = 'admininstrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'

        }

    }

}
```

<span data-ttu-id="1f061-120">A konfigurációs hoz létre a könyvtár `C:\DscSmbShare` Ha már nem létezik, és ezután könyvtárhoz, SMB-fájlmegosztásra.</span><span class="sxs-lookup"><span data-stu-id="1f061-120">The configuration creates the directory `C:\DscSmbShare` if it doesn't already exists, and then uses that directory as an SMB file share.</span></span> <span data-ttu-id="1f061-121">**FullAccess** biztosítani kell írni, vagy a fájlmegosztás törlése fiókoknak és **olvasási hozzáférés** esetlegesen konfigurációk és/vagy a DSC-erőforrások lekérése a megosztást (Ennek oka az ügyfél csomópontokon kell megadni A DSC fiókként fut, a rendszer alapértelmezés szerint így magát a számítógépet a megosztás eléréséhez).</span><span class="sxs-lookup"><span data-stu-id="1f061-121">**FullAccess** should be given to any account that needs to write to or delete from the file share, and **ReadAccess** must be given to any client nodes that get configurations and/or DSC resources from the share ( this is because DSC runs as the system account by default, so the computer itself has to have access to the share).</span></span>


### <a name="give-file-system-access-to-the-pull-client"></a><span data-ttu-id="1f061-122">A fájlrendszer elérése adnak a leküldéses ügyfél</span><span class="sxs-lookup"><span data-stu-id="1f061-122">Give file system access to the pull client</span></span>

<span data-ttu-id="1f061-123">Jogosultságot ad **olvasási hozzáférés** egy ügyfél csomópont lehetővé teszi, hogy az SMB-megosztáshoz hozzáférést, de nem fájlok vagy mappák belül, amely megosztási csomópont.</span><span class="sxs-lookup"><span data-stu-id="1f061-123">Giving **ReadAccess** to a client node allows that node to access the SMB share, but not to files or folders within that share.</span></span> <span data-ttu-id="1f061-124">Explicit módon az SMB-megosztás mappát és az almappák csomópontok elérésének engedélyezése az ügyfél rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="1f061-124">You have to explicitly grant client nodes access to the SMB share folder and sub-folders.</span></span> <span data-ttu-id="1f061-125">Azt is ugyanezt a műveletet a DSC használata hozzáadásával a **cNtfsPermissionEntry** erőforrás, amelyet a [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) modul.</span><span class="sxs-lookup"><span data-stu-id="1f061-125">We can do this with DSC by adding using the **cNtfsPermissionEntry** resource, which is contained in the [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) module.</span></span> <span data-ttu-id="1f061-126">Az alábbi konfiguráció bővíti a **cNtfsPermissionEntry** , amely ReadAndExecute hozzáférést biztosít az lekéréses ügyfél letiltása:</span><span class="sxs-lookup"><span data-stu-id="1f061-126">The following configuration adds a **cNtfsPermissionEntry** block that grants ReadAndExecute access to the pull client:</span></span>

```powershell
Configuration DSCSMB {

Import-DscResource -ModuleName PSDesiredStateConfiguration
Import-DscResource -ModuleName xSmbShare
Import-DscResource -ModuleName cNtfsAccessControl

    Node localhost {

        File CreateFolder {

            DestinationPath = 'DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'

        }

        xSMBShare CreateShare {

            Name = 'DscSmbShare'
            Path = 'DscSmbShare'
            FullAccess = 'administrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'

        }

        cNtfsPermissionEntry PermissionSet1 {

        Ensure = 'Present'
        Path = 'C:\DSCSMB'
        Principal = 'myDomain\Contoso-Server$'
        AccessControlInformation = @(
            cNtfsAccessControlInformation
            {
                AccessControlType = 'Allow'
                FileSystemRights = 'ReadAndExecute'
                Inheritance = 'ThisFolderSubfoldersAndFiles'
                NoPropagateInherit = $false
            }
        )
        DependsOn = '[File]CreateFolder'

        }


    }

}
```

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="1f061-127">Konfigurációk és erőforrások</span><span class="sxs-lookup"><span data-stu-id="1f061-127">Placing configurations and resources</span></span>

<span data-ttu-id="1f061-128">Bármely konfiguráció MOF-fájlok és/vagy az SMB-megosztás mappát bekérésére ügyfél csomópontok használni kívánt DSC-erőforrások mentéséhez.</span><span class="sxs-lookup"><span data-stu-id="1f061-128">Save any configuration MOF files and/or DSC resources that you want client nodes to pull in the SMB share folder.</span></span>

<span data-ttu-id="1f061-129">Bármely konfiguráció MOF-fájlt névvel kell ellátni _ConfigurationID_.mof, ahol _ConfigurationID_ értéke a **ConfigurationID** a célcsomópont LCM tulajdonsága.</span><span class="sxs-lookup"><span data-stu-id="1f061-129">Any configuration MOF file must be named _ConfigurationID_.mof, where _ConfigurationID_ is the value of the **ConfigurationID** property of the target node's LCM.</span></span> <span data-ttu-id="1f061-130">Lekéréses ügyfelek beállításával kapcsolatos további információkért lásd: [ügyféltelepítéshez lekéréses konfigurációs azonosítójával](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="1f061-130">For more information about setting up pull clients, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

><span data-ttu-id="1f061-131">**Megjegyzés:** konfigurációs azonosítókat kell használnia, ha lekéréses SMB-kiszolgálón használja.</span><span class="sxs-lookup"><span data-stu-id="1f061-131">**Note:** You must use configuration IDs if you are using an SMB pull server.</span></span> <span data-ttu-id="1f061-132">Az SMB-a konfigurációs nevek nem támogatottak.</span><span class="sxs-lookup"><span data-stu-id="1f061-132">Configuration names are not supported for SMB.</span></span>

<span data-ttu-id="1f061-133">Minden erőforrás modul zip és nevű megfelelően kell a következő mintát `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="1f061-133">Each resource module needs to be zipped and named according the the following pattern `{Module Name}_{Module Version}.zip`.</span></span> <span data-ttu-id="1f061-134">Például 3.1.2.0 modul verziójával xWebAdminstration nevű modul volna neve "xWebAdministration_3.2.1.0.zip".</span><span class="sxs-lookup"><span data-stu-id="1f061-134">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span> <span data-ttu-id="1f061-135">Egy modul verziói szerepelnie kell egy egyetlen zip-fájlt.</span><span class="sxs-lookup"><span data-stu-id="1f061-135">Each version of a module must be contained in a single zip file.</span></span> <span data-ttu-id="1f061-136">Mivel a modul formátum szerepel a WMF 5.0 minden zip-fájlban szereplő erőforrás csak egyetlen verziója támogatása a egyetlen könyvtárban található több verziója nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="1f061-136">Since there is only a single version of a resource in each zip file the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span> <span data-ttu-id="1f061-137">Ez azt jelenti, hogy csomagolási erőforrás modulok DSC lekérési kiszolgálójával való használatra mentése előtt meg kell győződnie egy kis módosítási könyvtárszerkezete.</span><span class="sxs-lookup"><span data-stu-id="1f061-137">This means that before packaging up DSC resource modules for use with pull server you need to make a small change to the directory structure.</span></span> <span data-ttu-id="1f061-138">Az alapértelmezett DSC erőforrást a WMF 5.0 tartalmazó modulok formátuma "{modul mappa}\{verziója} \DscResources\{DSC Erőforrásmappa}\'.</span><span class="sxs-lookup"><span data-stu-id="1f061-138">The default format of modules containing DSC resource in WMF 5.0 is '{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\'.</span></span> <span data-ttu-id="1f061-139">Előtt feliratkozott a lekérési kiszolgálójával csomagolás egyszerűen távolítsa el a **{verziója}** mappában, így az elérési útja bekerül a(z) {modul mappa} \DscResources\{DSC Erőforrásmappa}\'.</span><span class="sxs-lookup"><span data-stu-id="1f061-139">Before packaging up for the pull server simply remove the **{Module version}** folder so the path becomes '{Module Folder}\DscResources\{DSC Resource Folder}\'.</span></span> <span data-ttu-id="1f061-140">A módosítás a mappát a zip-fent leírt módon, és helyezze el a zip-fájlok az SMB-megosztás mappát.</span><span class="sxs-lookup"><span data-stu-id="1f061-140">With this change, zip the folder as described above and place these zip files in the SMB share folder.</span></span>

## <a name="creating-the-mof-checksum"></a><span data-ttu-id="1f061-141">A MOF-ellenőrzőösszeg létrehozása</span><span class="sxs-lookup"><span data-stu-id="1f061-141">Creating the MOF checksum</span></span>
<span data-ttu-id="1f061-142">Konfigurációs MOF-fájlt kell, hogy egy LCM a cél csomópont azt is ellenőrzi a konfigurációt az ellenőrzőösszeg-fájl megfeleltetni.</span><span class="sxs-lookup"><span data-stu-id="1f061-142">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span>
<span data-ttu-id="1f061-143">Hozzon létre egy ellenőrzőösszeg, hívja meg a [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="1f061-143">To create a checksum, call the [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) cmdlet.</span></span> <span data-ttu-id="1f061-144">A parancsmag tart egy **elérési** paraméter meghatározza, hogy a mappát, ahol a konfigurációs MOF található.</span><span class="sxs-lookup"><span data-stu-id="1f061-144">The cmdlet takes a **Path** parameter that specifies the folder where the configuration MOF is located.</span></span> <span data-ttu-id="1f061-145">A parancsmag létrehoz egy ellenőrzőösszeg nevű `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve.</span><span class="sxs-lookup"><span data-stu-id="1f061-145">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span>
<span data-ttu-id="1f061-146">Ha egynél több konfigurációs MOF-fájlok a megadott mappában, ellenőrzőösszeg minden konfigurációs a mappában létrejön.</span><span class="sxs-lookup"><span data-stu-id="1f061-146">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>

<span data-ttu-id="1f061-147">Az ellenőrzőösszeg-fájlnak kell lennie a konfigurációs MOF-fájlnak ugyanabban a könyvtárban (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` alapértelmezés szerint), és a neve megegyezik a `.checksum` fűz hozzá a kiterjesztést.</span><span class="sxs-lookup"><span data-stu-id="1f061-147">The checksum file must be present in the same directory as the configuration MOF file (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` by default), and have the same name with the `.checksum` extension appended.</span></span>

><span data-ttu-id="1f061-148">**Megjegyzés:**: Ha megváltoztatja a konfigurációs MOF-fájl bármely olyan módon, az ellenőrzőösszeg-fájl is kell hozni.</span><span class="sxs-lookup"><span data-stu-id="1f061-148">**Note**: If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

## <a name="setting-up-a-pull-client-for-smb"></a><span data-ttu-id="1f061-149">Az SMB-lekéréses ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="1f061-149">Setting up a pull client for SMB</span></span>

<span data-ttu-id="1f061-150">Ügyfél, amely lekéri a konfigurációk és/vagy az SMB-megosztáson erőforrások beállításához konfigurálása az ügyfél helyi Configuration Manager (LCM) rendelkező **ConfigurationRepositoryShare** és **ResourceRepositoryShare** mutatnak adja meg a megosztást, amelyről való lekérésére konfigurációk és a DSC-erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="1f061-150">To set up a client that pulls configurations and/or resources from an SMB share, you configure the client's Local Configuration Manager (LCM) with **ConfigurationRepositoryShare** and **ResourceRepositoryShare** blocks that specify the share from which to pull configurations and DSC resources.</span></span>

<span data-ttu-id="1f061-151">A LCM konfigurálásával kapcsolatos további információkért lásd: [ügyféltelepítéshez lekéréses konfigurációs azonosítójával](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="1f061-151">For more information about configuring the LCM, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

><span data-ttu-id="1f061-152">**Megjegyzés:** az egyszerűség, a példában a **PSDscAllowPlainTextPassword** engedélyezi a titkosítatlan szöveges jelszó átadja a **Credential** paraméter.</span><span class="sxs-lookup"><span data-stu-id="1f061-152">**Note:** For simplicity, this example uses the **PSDscAllowPlainTextPassword** to allow passing a plaintext password to the **Credential** parameter.</span></span> <span data-ttu-id="1f061-153">További információ a hitelesítő adatok biztonsága érdekében átadásakor: [konfigurációs adatokat a hitelesítő adatok beállítások](configDataCredentials.md).</span><span class="sxs-lookup"><span data-stu-id="1f061-153">For information about passing credentials more securely, see [Credentials Options in Configuration Data](configDataCredentials.md).</span></span>

><span data-ttu-id="1f061-154">**Megjegyzés:** meg kell adnia egy **ConfigurationID** a a **beállítások** egy metakonfigurációját az SMB lekérési kiszolgálójával, még akkor is, ha csak akkor vannak húzza erőforrások blokkja.</span><span class="sxs-lookup"><span data-stu-id="1f061-154">**Note:** You must specify a **ConfigurationID** in the **Settings** block of a metaconfiguration for an SMB pull server, even if you are only pulling resources.</span></span>

```powershell
$secpasswd = ConvertTo-SecureString “Pass1Word” -AsPlainText -Force
$mycreds = New-Object System.Management.Automation.PSCredential (“TestUser”, $secpasswd)

[DSCLocalConfigurationManager()]
configuration SmbCredTest
{
    Node $AllNodes.NodeName
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
            ConfigurationID    = '16db7357-9083-4806-a80c-ebbaf4acd6c1'
        }

         ConfigurationRepositoryShare SmbConfigShare
        {
            SourcePath = '\\WIN-E0TRU6U11B1\DscSmbShare'
            Credential = $mycreds
        }

        ResourceRepositoryShare SmbResourceShare
        {
            SourcePath = '\\WIN-E0TRU6U11B1\DscSmbShare'
            Credential = $mycreds

        }
    }
}

$ConfigurationData = @{

    AllNodes = @(

        @{

            #the "*" means "all nodes named in ConfigData" so we don't have to repeat ourselves

            NodeName="localhost"

            PSDscAllowPlainTextPassword = $true

        })



}
```

## <a name="acknowledgements"></a><span data-ttu-id="1f061-155">Köszönetnyilvánítás</span><span class="sxs-lookup"><span data-stu-id="1f061-155">Acknowledgements</span></span>

<span data-ttu-id="1f061-156">Különleges környezetnek köszönhetően a következőket:</span><span class="sxs-lookup"><span data-stu-id="1f061-156">Special thanks to the following:</span></span>

- <span data-ttu-id="1f061-157">Nagy F. Robbins, amelynek bejegyzéseket az SMB protokoll segítségével a DSC segített tájékoztatja a tartalom ebben a témakörben.</span><span class="sxs-lookup"><span data-stu-id="1f061-157">Mike F. Robbins, whose posts on using SMB for DSC helped inform the content in this topic.</span></span> <span data-ttu-id="1f061-158">Jelenleg a blog [nagy F Robbins](http://mikefrobbins.com/).</span><span class="sxs-lookup"><span data-stu-id="1f061-158">His blog is at [Mike F Robbins](http://mikefrobbins.com/).</span></span>
- <span data-ttu-id="1f061-159">Serge Nikalaichyk, akik lett létrehozva a **cNtfsAccessControl** modul.</span><span class="sxs-lookup"><span data-stu-id="1f061-159">Serge Nikalaichyk, who authored the **cNtfsAccessControl** module.</span></span> <span data-ttu-id="1f061-160">Ez a modul forrásának jelenleg https://github.com/SNikalaichyk/cNtfsAccessControl.</span><span class="sxs-lookup"><span data-stu-id="1f061-160">The source for this module is at https://github.com/SNikalaichyk/cNtfsAccessControl.</span></span>

## <a name="see-also"></a><span data-ttu-id="1f061-161">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1f061-161">See also</span></span>
- [<span data-ttu-id="1f061-162">A Windows PowerShell célállapot-konfiguráló áttekintése</span><span class="sxs-lookup"><span data-stu-id="1f061-162">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)
- [<span data-ttu-id="1f061-163">Konfigurációk életbe léptetése</span><span class="sxs-lookup"><span data-stu-id="1f061-163">Enacting configurations</span></span>](enactingConfigurations.md)
- [<span data-ttu-id="1f061-164">Lekérési ügyfél beállítása konfigurációs azonosítóval</span><span class="sxs-lookup"><span data-stu-id="1f061-164">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)