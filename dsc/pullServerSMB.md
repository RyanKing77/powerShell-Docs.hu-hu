---
ms.date: 04/11/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC SMB-lekérési kiszolgálójának beállítása
ms.openlocfilehash: 1eac6c51aeca3ed573ba8fa27188103436004920
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892865"
---
# <a name="setting-up-a-dsc-smb-pull-server"></a><span data-ttu-id="b01e8-103">A DSC SMB-lekérési kiszolgálójának beállítása</span><span class="sxs-lookup"><span data-stu-id="b01e8-103">Setting up a DSC SMB pull server</span></span>

<span data-ttu-id="b01e8-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b01e8-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b01e8-105">A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak.</span><span class="sxs-lookup"><span data-stu-id="b01e8-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="b01e8-106">Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="b01e8-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="b01e8-107">A DSC [SMB](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831795(v=ws.11)) lekéréses kiszolgálón DSC konfigurációs fájlokat és a DSC-erőforrások számára elérhetővé tenni célcsomópontokat, ha azokat a csomópontokat, kérje meg őket az SMB-fájlmegosztások futtató számítógépet.</span><span class="sxs-lookup"><span data-stu-id="b01e8-107">A DSC [SMB](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831795(v=ws.11)) pull server is a computer hosting SMB file shares that make DSC configuration files and DSC resources available to target nodes when those nodes ask for them.</span></span>

<span data-ttu-id="b01e8-108">A DSC SMB-lekérési kiszolgálójának használatához meg kell:</span><span class="sxs-lookup"><span data-stu-id="b01e8-108">To use an SMB pull server for DSC, you have to:</span></span>

- <span data-ttu-id="b01e8-109">A kiszolgálón futó PowerShell 4.0-s vagy újabb SMB-fájlmegosztás beállítása</span><span class="sxs-lookup"><span data-stu-id="b01e8-109">Set up an SMB file share on a server running PowerShell 4.0 or higher</span></span>
- <span data-ttu-id="b01e8-110">Kérje le az SMB-megosztáson lévő futó PowerShell 4.0-s vagy újabb ügyfél konfigurálása</span><span class="sxs-lookup"><span data-stu-id="b01e8-110">Configure a client running PowerShell 4.0 or higher to pull from that SMB share</span></span>

## <a name="using-the-xsmbshare-resource-to-create-an-smb-file-share"></a><span data-ttu-id="b01e8-111">A xSmbShare erőforrást használja az SMB-fájlmegosztás létrehozása</span><span class="sxs-lookup"><span data-stu-id="b01e8-111">Using the xSmbShare resource to create an SMB file share</span></span>

<span data-ttu-id="b01e8-112">Nincsenek számos módon állítsa be az SMB-fájlmegosztás, de nézzük, hogyan lehet ezt megteheti DSC használatával.</span><span class="sxs-lookup"><span data-stu-id="b01e8-112">There are a number of ways to set up an SMB file share, but let's look at how you can do this by using DSC.</span></span>

### <a name="install-the-xsmbshare-resource"></a><span data-ttu-id="b01e8-113">Telepítse a xSmbShare erőforrás</span><span class="sxs-lookup"><span data-stu-id="b01e8-113">Install the xSmbShare resource</span></span>

<span data-ttu-id="b01e8-114">Hívja a [Install-Module](/powershell/module/PowershellGet/Install-Module) telepítésére szolgáló parancsmagot a **xSmbShare** modul.</span><span class="sxs-lookup"><span data-stu-id="b01e8-114">Call the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xSmbShare** module.</span></span>

> [!NOTE]
> <span data-ttu-id="b01e8-115">`Install-Module` tartalmazza a **PowerShellGet** modult, amely része a PowerShell 5.0-s.</span><span class="sxs-lookup"><span data-stu-id="b01e8-115">`Install-Module` is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="b01e8-116">Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modul előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="b01e8-116">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>
> <span data-ttu-id="b01e8-117">A **xSmbShare** tartalmazza a DSC-erőforrás **xSmbShare**, SMB-fájlmegosztás létrehozásához használható.</span><span class="sxs-lookup"><span data-stu-id="b01e8-117">The **xSmbShare** contains the DSC resource **xSmbShare**, which can be used to create an SMB file share.</span></span>

### <a name="create-the-directory-and-file-share"></a><span data-ttu-id="b01e8-118">A könyvtár- és megosztás létrehozása</span><span class="sxs-lookup"><span data-stu-id="b01e8-118">Create the directory and file share</span></span>

<span data-ttu-id="b01e8-119">Az alábbi konfigurációt használja a [fájl](fileResource.md) erőforrás a könyvtárban, a megosztás létrehozásához és a **xSmbShare** erőforrás az SMB-megosztás beállításához:</span><span class="sxs-lookup"><span data-stu-id="b01e8-119">The following configuration uses the [File](fileResource.md) resource to create the directory for the share and the **xSmbShare** resource to set up the SMB share:</span></span>

```powershell
Configuration SmbShare
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Import-DscResource -ModuleName xSmbShare

    Node localhost
    {

        File CreateFolder
        {
            DestinationPath = 'C:\DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
        }

        xSMBShare CreateShare
        {
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

<span data-ttu-id="b01e8-120">A konfiguráció hoz létre a könyvtár `C:\DscSmbShare` Ha már nem létezik, és ezután használja a könyvtárban, SMB-fájlmegosztásra.</span><span class="sxs-lookup"><span data-stu-id="b01e8-120">The configuration creates the directory `C:\DscSmbShare` if it doesn't already exists, and then uses that directory as an SMB file share.</span></span> <span data-ttu-id="b01e8-121">**FullAccess** olyan fiókot, amely írási, vagy törölje a fájlmegosztásból kell fordítani és **olvasási hozzáférés** bármely ügyfél csomópontok, a konfigurációk és/vagy DSC-erőforrások a megosztáson (ennek az az oka a kell megadni DSC fut, a rendszer fiók alapértelmezés szerint így magát a számítógépet a megosztás eléréséhez).</span><span class="sxs-lookup"><span data-stu-id="b01e8-121">**FullAccess** should be given to any account that needs to write to or delete from the file share, and **ReadAccess** must be given to any client nodes that get configurations and/or DSC resources from the share ( this is because DSC runs as the system account by default, so the computer itself has to have access to the share).</span></span>

### <a name="give-file-system-access-to-the-pull-client"></a><span data-ttu-id="b01e8-122">A fájlrendszer elérése adhat a pull-ügyfél</span><span class="sxs-lookup"><span data-stu-id="b01e8-122">Give file system access to the pull client</span></span>

<span data-ttu-id="b01e8-123">Így **olvasási hozzáférés** ügyfélnek csomópont lehetővé teszi a csomóponton, hogy az SMB-megosztás eléréséhez, de, fájlok vagy mappák belül, amely nem osztozik.</span><span class="sxs-lookup"><span data-stu-id="b01e8-123">Giving **ReadAccess** to a client node allows that node to access the SMB share, but not to files or folders within that share.</span></span> <span data-ttu-id="b01e8-124">Explicit módon az SMB-megosztás mappát és almappák csomópontok elérésének engedélyezése az ügyfél rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="b01e8-124">You have to explicitly grant client nodes access to the SMB share folder and sub-folders.</span></span> <span data-ttu-id="b01e8-125">A Microsoft ehhez a DSC használatával vesz fel a **cNtfsPermissionEntry** erőforrás, amely tartalmazza a [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) modul.</span><span class="sxs-lookup"><span data-stu-id="b01e8-125">We can do this with DSC by adding using the **cNtfsPermissionEntry** resource, which is contained in the [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) module.</span></span> <span data-ttu-id="b01e8-126">A következő konfigurációt ad hozzá egy **cNtfsPermissionEntry** ReadAndExecute hozzáférést a lekérési ügyfél blokkolása:</span><span class="sxs-lookup"><span data-stu-id="b01e8-126">The following configuration adds a **cNtfsPermissionEntry** block that grants ReadAndExecute access to the pull client:</span></span>

```powershell
Configuration DSCSMB
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Import-DscResource -ModuleName xSmbShare
    Import-DscResource -ModuleName cNtfsAccessControl

    Node localhost
    {

        File CreateFolder
        {
            DestinationPath = 'DscSmbShare'
            Type = 'Directory'
            Ensure = 'Present'
        }

        xSMBShare CreateShare
        {
            Name = 'DscSmbShare'
            Path = 'DscSmbShare'
            FullAccess = 'administrator'
            ReadAccess = 'myDomain\Contoso-Server$'
            FolderEnumerationMode = 'AccessBased'
            Ensure = 'Present'
            DependsOn = '[File]CreateFolder'
        }

        cNtfsPermissionEntry PermissionSet1
        {
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

## <a name="placing-configurations-and-resources"></a><span data-ttu-id="b01e8-127">Konfigurációkat és erőforrásokat elhelyezése</span><span class="sxs-lookup"><span data-stu-id="b01e8-127">Placing configurations and resources</span></span>

<span data-ttu-id="b01e8-128">Mentse a konfigurációs MOF-fájlok és/vagy ügyfél-csomópontok használatával kérhetők le az SMB-megosztás mappát használni kívánt DSC-erőforrások.</span><span class="sxs-lookup"><span data-stu-id="b01e8-128">Save any configuration MOF files and/or DSC resources that you want client nodes to pull in the SMB share folder.</span></span>

<span data-ttu-id="b01e8-129">Minden olyan konfigurációs MOF-fájl neve legyen *ConfigurationID*.mof, ahol *ConfigurationID* értéke a **ConfigurationID** a célcsomópont LCM tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="b01e8-129">Any configuration MOF file must be named *ConfigurationID*.mof, where *ConfigurationID* is the value of the **ConfigurationID** property of the target node's LCM.</span></span> <span data-ttu-id="b01e8-130">Lekérési ügyfél beállításával kapcsolatos további információkért lásd: [konfigurációs azonosítóval lekérési ügyfél beállítása](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="b01e8-130">For more information about setting up pull clients, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b01e8-131">Ha használja az SMB-lekérési kiszolgálójának konfigurációazonosítók kell használnia.</span><span class="sxs-lookup"><span data-stu-id="b01e8-131">You must use configuration IDs if you are using an SMB pull server.</span></span> <span data-ttu-id="b01e8-132">Konfigurációs nevek nem támogatottak az SMB.</span><span class="sxs-lookup"><span data-stu-id="b01e8-132">Configuration names are not supported for SMB.</span></span>

<span data-ttu-id="b01e8-133">Minden egyes erőforrás a modul zip és nevű megfelelően van szükség az a következő mintának `{Module Name}_{Module Version}.zip`.</span><span class="sxs-lookup"><span data-stu-id="b01e8-133">Each resource module needs to be zipped and named according the the following pattern `{Module Name}_{Module Version}.zip`.</span></span> <span data-ttu-id="b01e8-134">Ha például 3.1.2.0 modul verziójával xWebAdminstration modul neve "xWebAdministration_3.2.1.0.zip".</span><span class="sxs-lookup"><span data-stu-id="b01e8-134">For example, a module named xWebAdminstration with a module version of 3.1.2.0 would be named 'xWebAdministration_3.2.1.0.zip'.</span></span> <span data-ttu-id="b01e8-135">Minden egyes modul verzióját tartalmaznia kell egy egyetlen zip-fájlt.</span><span class="sxs-lookup"><span data-stu-id="b01e8-135">Each version of a module must be contained in a single zip file.</span></span> <span data-ttu-id="b01e8-136">Mivel csak egyetlen verziója is minden egyes zip-fájlt a WMF 5.0-s hozzá a modul formátum az erőforráshoz egyetlen címtárban több modul verziók támogatása nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="b01e8-136">Since there is only a single version of a resource in each zip file the module format added in WMF 5.0 with support for multiple module versions in a single directory is not supported.</span></span> <span data-ttu-id="b01e8-137">Ez azt jelenti, hogy előtt becsomagolást mentése erőforrás modulok DSC lekéréses kiszolgálón való használatra kell, hogy módosítsa a könyvtár struktúra.</span><span class="sxs-lookup"><span data-stu-id="b01e8-137">This means that before packaging up DSC resource modules for use with pull server you need to make a small change to the directory structure.</span></span> <span data-ttu-id="b01e8-138">Az alapértelmezett formátum a modulok DSC-erőforrás a WMF 5.0 tartalmazó `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`.</span><span class="sxs-lookup"><span data-stu-id="b01e8-138">The default format of modules containing DSC resource in WMF 5.0 is `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`.</span></span> <span data-ttu-id="b01e8-139">Előtt terveztük a lekérési kiszolgálón csomagolási egyszerűen távolítsa el a `{Module version}` mappát az elérési út válik, így `{Module Folder}\DscResources\{DSC Resource Folder}\`.</span><span class="sxs-lookup"><span data-stu-id="b01e8-139">Before packaging up for the pull server simply remove the `{Module version}` folder so the path becomes `{Module Folder}\DscResources\{DSC Resource Folder}\`.</span></span> <span data-ttu-id="b01e8-140">Ezzel a mappa zip-fent leírtak szerint, és helyezze a zip-fájlok az SMB-megosztás mappát.</span><span class="sxs-lookup"><span data-stu-id="b01e8-140">With this change, zip the folder as described above and place these zip files in the SMB share folder.</span></span>

## <a name="creating-the-mof-checksum"></a><span data-ttu-id="b01e8-141">A MOF-ellenőrzőösszeg létrehozása</span><span class="sxs-lookup"><span data-stu-id="b01e8-141">Creating the MOF checksum</span></span>

<span data-ttu-id="b01e8-142">A konfigurációs MOF-fájlt kell ellenőrzőösszeg fájl párosítani, hogy a cél csomópont egy LCM ellenőrizheti a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="b01e8-142">A configuration MOF file needs to be paired with a checksum file so that an LCM on a target node can validate the configuration.</span></span>
<span data-ttu-id="b01e8-143">Ellenőrzőösszeg létrehozásához hívja a [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="b01e8-143">To create a checksum, call the [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) cmdlet.</span></span> <span data-ttu-id="b01e8-144">A parancsmag lép egy `Path` paraméter, amely a mappát, ahol a konfigurációs MOF található.</span><span class="sxs-lookup"><span data-stu-id="b01e8-144">The cmdlet takes a `Path` parameter that specifies the folder where the configuration MOF is located.</span></span> <span data-ttu-id="b01e8-145">A parancsmag létrehoz egy ellenőrzőösszeg-fájlt `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve.</span><span class="sxs-lookup"><span data-stu-id="b01e8-145">The cmdlet creates a checksum file named `ConfigurationMOFName.mof.checksum`, where `ConfigurationMOFName` is the name of the configuration mof file.</span></span>
<span data-ttu-id="b01e8-146">Ha egynél több konfigurációs MOF-fájlok a megadott mappában, a mappában az egyes konfigurációkhoz egy ellenőrzőösszeg jön létre.</span><span class="sxs-lookup"><span data-stu-id="b01e8-146">If there are more than one configuration MOF files in the specified folder, a checksum is created for each configuration in the folder.</span></span>

<span data-ttu-id="b01e8-147">Az ellenőrzőösszeg-fájlnak kell lennie a konfigurációs MOF-fájl ugyanabban a címtárban (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` alapértelmezés szerint), és a neve megegyezik a `.checksum` bővítmény hozzáfűzve.</span><span class="sxs-lookup"><span data-stu-id="b01e8-147">The checksum file must be present in the same directory as the configuration MOF file (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` by default), and have the same name with the `.checksum` extension appended.</span></span>

> [!NOTE]
> <span data-ttu-id="b01e8-148">Ha módosítja a konfigurációs MOF-fájl bármilyen módon, az ellenőrzőösszeg-fájl is létre kell hoznia.</span><span class="sxs-lookup"><span data-stu-id="b01e8-148">If you change the configuration MOF file in any way, you must also recreate the checksum file.</span></span>

## <a name="setting-up-a-pull-client-for-smb"></a><span data-ttu-id="b01e8-149">Az SMB-lekérési ügyfél beállítása</span><span class="sxs-lookup"><span data-stu-id="b01e8-149">Setting up a pull client for SMB</span></span>

<span data-ttu-id="b01e8-150">Ügyfél, amely lekéri a konfigurációk és/vagy az SMB-megosztáson erőforrások beállításához, konfigurálja az ügyfél helyi Configuration Manager (LCM) Konfigurálása a **ConfigurationRepositoryShare** és **ResourceRepositoryShare** adja meg a megosztást, amelyről a konfigurációkat és erőforrásokat DSC lekéréses blokkokat.</span><span class="sxs-lookup"><span data-stu-id="b01e8-150">To set up a client that pulls configurations and/or resources from an SMB share, you configure the client's Local Configuration Manager (LCM) with **ConfigurationRepositoryShare** and **ResourceRepositoryShare** blocks that specify the share from which to pull configurations and DSC resources.</span></span>

<span data-ttu-id="b01e8-151">Az LCM konfigurálása kapcsolatos további információkért lásd: [konfigurációs azonosítóval lekérési ügyfél beállítása](pullClientConfigID.md).</span><span class="sxs-lookup"><span data-stu-id="b01e8-151">For more information about configuring the LCM, see [Setting up a pull client using configuration ID](pullClientConfigID.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b01e8-152">Az egyszerűség kedvéért ez a példa a **PSDscAllowPlainTextPassword** a titkosítatlan szöveges jelszó átadásának engedélyezése a **Credential** paraméter.</span><span class="sxs-lookup"><span data-stu-id="b01e8-152">For simplicity, this example uses the **PSDscAllowPlainTextPassword** to allow passing a plaintext password to the **Credential** parameter.</span></span> <span data-ttu-id="b01e8-153">További információ a hitelesítő adatok biztonságosabb passing: [hitelesítő adatait a konfigurációs adatok beállításai](configDataCredentials.md).</span><span class="sxs-lookup"><span data-stu-id="b01e8-153">For information about passing credentials more securely, see [Credentials Options in Configuration Data](configDataCredentials.md).</span></span>
>
> <span data-ttu-id="b01e8-154">**Kell** adjon meg egy **ConfigurationID** a a **beállítások** egy metaconfiguration egy SMB-lekérési kiszolgálójának, akkor is, ha csak erőforrások hívásokat küldenek a kódblokkot.</span><span class="sxs-lookup"><span data-stu-id="b01e8-154">You **MUST** specify a **ConfigurationID** in the **Settings** block of a metaconfiguration for an SMB pull server, even if you are only pulling resources.</span></span>

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

## <a name="acknowledgements"></a><span data-ttu-id="b01e8-155">Köszönetnyilvánítás</span><span class="sxs-lookup"><span data-stu-id="b01e8-155">Acknowledgements</span></span>

<span data-ttu-id="b01e8-156">Speciális köszönhetően a következőket:</span><span class="sxs-lookup"><span data-stu-id="b01e8-156">Special thanks to the following:</span></span>

- <span data-ttu-id="b01e8-157">Mike F. Robbins, amelynek a DSC SMB-vel bejegyzések segített ebben a témakörben a tartalom értesítse.</span><span class="sxs-lookup"><span data-stu-id="b01e8-157">Mike F. Robbins, whose posts on using SMB for DSC helped inform the content in this topic.</span></span> <span data-ttu-id="b01e8-158">Jelenleg a blogra [Mike F Robbins](http://mikefrobbins.com/).</span><span class="sxs-lookup"><span data-stu-id="b01e8-158">His blog is at [Mike F Robbins](http://mikefrobbins.com/).</span></span>
- <span data-ttu-id="b01e8-159">Serge Nikalaichyk, akik készített a **cNtfsAccessControl** modul.</span><span class="sxs-lookup"><span data-stu-id="b01e8-159">Serge Nikalaichyk, who authored the **cNtfsAccessControl** module.</span></span> <span data-ttu-id="b01e8-160">Ez a modul a forrása a [cNtfsAccessControl](https://github.com/SNikalaichyk/cNtfsAccessControl).</span><span class="sxs-lookup"><span data-stu-id="b01e8-160">The source for this module is at [cNtfsAccessControl](https://github.com/SNikalaichyk/cNtfsAccessControl).</span></span>

## <a name="see-also"></a><span data-ttu-id="b01e8-161">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b01e8-161">See also</span></span>

[<span data-ttu-id="b01e8-162">Windows PowerShell Desired State Configuration áttekintése</span><span class="sxs-lookup"><span data-stu-id="b01e8-162">Windows PowerShell Desired State Configuration Overview</span></span>](overview.md)

[<span data-ttu-id="b01e8-163">Konfigurációk életbe léptetése</span><span class="sxs-lookup"><span data-stu-id="b01e8-163">Enacting configurations</span></span>](enactingConfigurations.md)

[<span data-ttu-id="b01e8-164">Lekérési ügyfél beállítása konfigurációs azonosítóval</span><span class="sxs-lookup"><span data-stu-id="b01e8-164">Setting up a pull client using configuration ID</span></span>](pullClientConfigID.md)