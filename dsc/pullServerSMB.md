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
# <a name="setting-up-a-dsc-smb-pull-server"></a>A DSC SMB-lekérési kiszolgálójának beállítása

A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

> [!IMPORTANT]
> A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak. Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).

A DSC [SMB](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831795(v=ws.11)) lekéréses kiszolgálón DSC konfigurációs fájlokat és a DSC-erőforrások számára elérhetővé tenni célcsomópontokat, ha azokat a csomópontokat, kérje meg őket az SMB-fájlmegosztások futtató számítógépet.

A DSC SMB-lekérési kiszolgálójának használatához meg kell:

- A kiszolgálón futó PowerShell 4.0-s vagy újabb SMB-fájlmegosztás beállítása
- Kérje le az SMB-megosztáson lévő futó PowerShell 4.0-s vagy újabb ügyfél konfigurálása

## <a name="using-the-xsmbshare-resource-to-create-an-smb-file-share"></a>A xSmbShare erőforrást használja az SMB-fájlmegosztás létrehozása

Nincsenek számos módon állítsa be az SMB-fájlmegosztás, de nézzük, hogyan lehet ezt megteheti DSC használatával.

### <a name="install-the-xsmbshare-resource"></a>Telepítse a xSmbShare erőforrás

Hívja a [Install-Module](/powershell/module/PowershellGet/Install-Module) telepítésére szolgáló parancsmagot a **xSmbShare** modul.

> [!NOTE]
> `Install-Module` tartalmazza a **PowerShellGet** modult, amely része a PowerShell 5.0-s. Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modul előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).
> A **xSmbShare** tartalmazza a DSC-erőforrás **xSmbShare**, SMB-fájlmegosztás létrehozásához használható.

### <a name="create-the-directory-and-file-share"></a>A könyvtár- és megosztás létrehozása

Az alábbi konfigurációt használja a [fájl](fileResource.md) erőforrás a könyvtárban, a megosztás létrehozásához és a **xSmbShare** erőforrás az SMB-megosztás beállításához:

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

A konfiguráció hoz létre a könyvtár `C:\DscSmbShare` Ha már nem létezik, és ezután használja a könyvtárban, SMB-fájlmegosztásra. **FullAccess** olyan fiókot, amely írási, vagy törölje a fájlmegosztásból kell fordítani és **olvasási hozzáférés** bármely ügyfél csomópontok, a konfigurációk és/vagy DSC-erőforrások a megosztáson (ennek az az oka a kell megadni DSC fut, a rendszer fiók alapértelmezés szerint így magát a számítógépet a megosztás eléréséhez).

### <a name="give-file-system-access-to-the-pull-client"></a>A fájlrendszer elérése adhat a pull-ügyfél

Így **olvasási hozzáférés** ügyfélnek csomópont lehetővé teszi a csomóponton, hogy az SMB-megosztás eléréséhez, de, fájlok vagy mappák belül, amely nem osztozik. Explicit módon az SMB-megosztás mappát és almappák csomópontok elérésének engedélyezése az ügyfél rendelkezik. A Microsoft ehhez a DSC használatával vesz fel a **cNtfsPermissionEntry** erőforrás, amely tartalmazza a [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) modul. A következő konfigurációt ad hozzá egy **cNtfsPermissionEntry** ReadAndExecute hozzáférést a lekérési ügyfél blokkolása:

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

## <a name="placing-configurations-and-resources"></a>Konfigurációkat és erőforrásokat elhelyezése

Mentse a konfigurációs MOF-fájlok és/vagy ügyfél-csomópontok használatával kérhetők le az SMB-megosztás mappát használni kívánt DSC-erőforrások.

Minden olyan konfigurációs MOF-fájl neve legyen *ConfigurationID*.mof, ahol *ConfigurationID* értéke a **ConfigurationID** a célcsomópont LCM tulajdonságát. Lekérési ügyfél beállításával kapcsolatos további információkért lásd: [konfigurációs azonosítóval lekérési ügyfél beállítása](pullClientConfigID.md).

> [!NOTE]
> Ha használja az SMB-lekérési kiszolgálójának konfigurációazonosítók kell használnia. Konfigurációs nevek nem támogatottak az SMB.

Minden egyes erőforrás a modul zip és nevű megfelelően van szükség az a következő mintának `{Module Name}_{Module Version}.zip`. Ha például 3.1.2.0 modul verziójával xWebAdminstration modul neve "xWebAdministration_3.2.1.0.zip". Minden egyes modul verzióját tartalmaznia kell egy egyetlen zip-fájlt. Mivel csak egyetlen verziója is minden egyes zip-fájlt a WMF 5.0-s hozzá a modul formátum az erőforráshoz egyetlen címtárban több modul verziók támogatása nem támogatott. Ez azt jelenti, hogy előtt becsomagolást mentése erőforrás modulok DSC lekéréses kiszolgálón való használatra kell, hogy módosítsa a könyvtár struktúra. Az alapértelmezett formátum a modulok DSC-erőforrás a WMF 5.0 tartalmazó `{Module Folder}\{Module Version}\DscResources\{DSC Resource Folder}\`. Előtt terveztük a lekérési kiszolgálón csomagolási egyszerűen távolítsa el a `{Module version}` mappát az elérési út válik, így `{Module Folder}\DscResources\{DSC Resource Folder}\`. Ezzel a mappa zip-fent leírtak szerint, és helyezze a zip-fájlok az SMB-megosztás mappát.

## <a name="creating-the-mof-checksum"></a>A MOF-ellenőrzőösszeg létrehozása

A konfigurációs MOF-fájlt kell ellenőrzőösszeg fájl párosítani, hogy a cél csomópont egy LCM ellenőrizheti a konfigurációt.
Ellenőrzőösszeg létrehozásához hívja a [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) parancsmagot. A parancsmag lép egy `Path` paraméter, amely a mappát, ahol a konfigurációs MOF található. A parancsmag létrehoz egy ellenőrzőösszeg-fájlt `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve.
Ha egynél több konfigurációs MOF-fájlok a megadott mappában, a mappában az egyes konfigurációkhoz egy ellenőrzőösszeg jön létre.

Az ellenőrzőösszeg-fájlnak kell lennie a konfigurációs MOF-fájl ugyanabban a címtárban (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` alapértelmezés szerint), és a neve megegyezik a `.checksum` bővítmény hozzáfűzve.

> [!NOTE]
> Ha módosítja a konfigurációs MOF-fájl bármilyen módon, az ellenőrzőösszeg-fájl is létre kell hoznia.

## <a name="setting-up-a-pull-client-for-smb"></a>Az SMB-lekérési ügyfél beállítása

Ügyfél, amely lekéri a konfigurációk és/vagy az SMB-megosztáson erőforrások beállításához, konfigurálja az ügyfél helyi Configuration Manager (LCM) Konfigurálása a **ConfigurationRepositoryShare** és **ResourceRepositoryShare** adja meg a megosztást, amelyről a konfigurációkat és erőforrásokat DSC lekéréses blokkokat.

Az LCM konfigurálása kapcsolatos további információkért lásd: [konfigurációs azonosítóval lekérési ügyfél beállítása](pullClientConfigID.md).

> [!NOTE]
> Az egyszerűség kedvéért ez a példa a **PSDscAllowPlainTextPassword** a titkosítatlan szöveges jelszó átadásának engedélyezése a **Credential** paraméter. További információ a hitelesítő adatok biztonságosabb passing: [hitelesítő adatait a konfigurációs adatok beállításai](configDataCredentials.md).
>
> **Kell** adjon meg egy **ConfigurationID** a a **beállítások** egy metaconfiguration egy SMB-lekérési kiszolgálójának, akkor is, ha csak erőforrások hívásokat küldenek a kódblokkot.

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

## <a name="acknowledgements"></a>Köszönetnyilvánítás

Speciális köszönhetően a következőket:

- Mike F. Robbins, amelynek a DSC SMB-vel bejegyzések segített ebben a témakörben a tartalom értesítse. Jelenleg a blogra [Mike F Robbins](http://mikefrobbins.com/).
- Serge Nikalaichyk, akik készített a **cNtfsAccessControl** modul. Ez a modul a forrása a [cNtfsAccessControl](https://github.com/SNikalaichyk/cNtfsAccessControl).

## <a name="see-also"></a>Lásd még:

[Windows PowerShell Desired State Configuration áttekintése](overview.md)

[Konfigurációk életbe léptetése](enactingConfigurations.md)

[Lekérési ügyfél beállítása konfigurációs azonosítóval](pullClientConfigID.md)