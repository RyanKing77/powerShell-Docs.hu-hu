---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Egy DSC SMB lekérési kiszolgálójával beállítása"
ms.openlocfilehash: ff3faeb1952e6116cf97b1aaf8f125d8931dd35e
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="setting-up-a-dsc-smb-pull-server"></a>Egy DSC SMB lekérési kiszolgálójával beállítása

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A DSC [SMB](https://technet.microsoft.com/library/hh831795.aspx) lekéréses kiszolgáló egy olyan DSC konfigurációs fájlokat és a DSC-erőforrások számára elérhetővé tenni célcsomópontokat, ha azokat a csomópontokat, kérje meg őket az SMB-fájlmegosztások futtató számítógép.

A DSC használandó lekéréses SMB-kiszolgálón, akkor kell:
- Állítson be olyan kiszolgálón PowerShell 4.0-s vagy újabb SMB-fájlmegosztásra
- Az adott SMB-megosztás lekéréses 4.0-s vagy újabb rendszerű a PowerShell ügyfél konfigurálása

## <a name="using-the-xsmbshare-resource-to-create-an-smb-file-share"></a>SMB-fájlmegosztás létrehozása a xSmbShare erőforrás használatával

Nincsenek többféleképpen SMB-fájlmegosztás beállítása azonban nézzük hogyan ehhez DSC használatával.

### <a name="install-the-xsmbshare-resource"></a>Telepítse a xSmbShare erőforrás

Hívja a [Install-modul](https://technet.microsoft.com/library/dn807162.aspx) telepítésére szolgáló parancsmagot a **xSmbShare** modul.
>**Megjegyzés:**: **Install-modul** megtalálható a **PowerShellGet** modul, amely PowerShell 5.0 szerepel. Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modulok előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186). A **xSmbShare** tartalmazza a DSC-erőforrás **xSmbShare**, amelyek segítségével az SMB-fájlmegosztás létrehozása.

### <a name="create-the-directory-and-file-share"></a>A könyvtár- és fájlmegosztás létrehozása

A következő konfigurációt használja a [fájl](fileResource.md) a megosztáshoz a következő könyvtár létrehozásakor erőforrás és a **xSmbShare** erőforrás az SMB-megosztás beállítása:

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

A konfigurációs hoz létre a könyvtár `C:\DscSmbShare` Ha már nem létezik, és ezután könyvtárhoz, SMB-fájlmegosztásra. **FullAccess** biztosítani kell írni, vagy a fájlmegosztás törlése fiókoknak és **olvasási hozzáférés** esetlegesen konfigurációk és/vagy a DSC-erőforrások lekérése a megosztást (Ennek oka az ügyfél csomópontokon kell megadni A DSC fiókként fut, a rendszer alapértelmezés szerint így magát a számítógépet a megosztás eléréséhez).


### <a name="give-file-system-access-to-the-pull-client"></a>A fájlrendszer elérése adnak a leküldéses ügyfél

Jogosultságot ad **olvasási hozzáférés** egy ügyfél csomópont lehetővé teszi, hogy az SMB-megosztáshoz hozzáférést, de nem fájlok vagy mappák belül, amely megosztási csomópont. Explicit módon az SMB-megosztás mappát és az almappák csomópontok elérésének engedélyezése az ügyfél rendelkezik. Azt is ugyanezt a műveletet a DSC használata hozzáadásával a **cNtfsPermissionEntry** erőforrás, amelyet a [CNtfsAccessControl](https://www.powershellgallery.com/packages/cNtfsAccessControl/1.2.0) modul. Az alábbi konfiguráció bővíti a **cNtfsPermissionEntry** , amely ReadAndExecute hozzáférést biztosít az lekéréses ügyfél letiltása:

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

## <a name="placing-configurations-and-resources"></a>Konfigurációk és erőforrások

Bármely konfiguráció MOF-fájlok és/vagy az SMB-megosztás mappát bekérésére ügyfél csomópontok használni kívánt DSC-erőforrások mentéséhez.

Bármely konfiguráció MOF-fájlt névvel kell ellátni _ConfigurationID_.mof, ahol _ConfigurationID_ értéke a **ConfigurationID** a célcsomópont LCM tulajdonsága. Lekéréses ügyfelek beállításával kapcsolatos további információkért lásd: [ügyféltelepítéshez lekéréses konfigurációs azonosítójával](pullClientConfigID.md).

>**Megjegyzés:** konfigurációs azonosítókat kell használnia, ha lekéréses SMB-kiszolgálón használja. Az SMB-a konfigurációs nevek nem támogatottak.

Minden erőforrás modul zip és nevű megfelelően kell a következő mintát `{Module Name}_{Module Version}.zip`. Például 3.1.2.0 modul verziójával xWebAdminstration nevű modul volna neve "xWebAdministration_3.2.1.0.zip". Egy modul verziói szerepelnie kell egy egyetlen zip-fájlt. Mivel a modul formátum szerepel a WMF 5.0 minden zip-fájlban szereplő erőforrás csak egyetlen verziója támogatása a egyetlen könyvtárban található több verziója nem támogatott. Ez azt jelenti, hogy csomagolási erőforrás modulok DSC lekérési kiszolgálójával való használatra mentése előtt meg kell győződnie egy kis módosítási könyvtárszerkezete. Az alapértelmezett DSC erőforrást a WMF 5.0 tartalmazó modulok formátuma "{modul mappa}\{verziója} \DscResources\{DSC Erőforrásmappa}\'. Előtt feliratkozott a lekérési kiszolgálójával csomagolás egyszerűen távolítsa el a **{verziója}** mappában, így az elérési útja bekerül a(z) {modul mappa} \DscResources\{DSC Erőforrásmappa}\'. A módosítás a mappát a zip-fent leírt módon, és helyezze el a zip-fájlok az SMB-megosztás mappát. 

## <a name="creating-the-mof-checksum"></a>A MOF-ellenőrzőösszeg létrehozása
Konfigurációs MOF-fájlt kell, hogy egy LCM a cél csomópont azt is ellenőrzi a konfigurációt az ellenőrzőösszeg-fájl megfeleltetni. Hozzon létre egy ellenőrzőösszeg, hívja meg a [New-DSCCheckSum](https://technet.microsoft.com/en-us/library/dn521622.aspx) parancsmag. A parancsmag tart egy **elérési** paraméter meghatározza, hogy a mappát, ahol a konfigurációs MOF található. A parancsmag létrehoz egy ellenőrzőösszeg nevű `ConfigurationMOFName.mof.checksum`, ahol `ConfigurationMOFName` a konfigurációs mof-fájl neve. Ha egynél több konfigurációs MOF-fájlok a megadott mappában, ellenőrzőösszeg minden konfigurációs a mappában létrejön.

Az ellenőrzőösszeg-fájlnak kell lennie a konfigurációs MOF-fájlnak ugyanabban a könyvtárban (`$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration` alapértelmezés szerint), és a neve megegyezik a `.checksum` fűz hozzá a kiterjesztést.

>**Megjegyzés:**: Ha megváltoztatja a konfigurációs MOF-fájl bármely olyan módon, az ellenőrzőösszeg-fájl is kell hozni.

## <a name="setting-up-a-pull-client-for-smb"></a>Az SMB-lekéréses ügyfél beállítása

Ügyfél, amely lekéri a konfigurációk és/vagy az SMB-megosztáson erőforrások beállításához konfigurálása az ügyfél helyi Configuration Manager (LCM) rendelkező **ConfigurationRepositoryShare** és **ResourceRepositoryShare** mutatnak adja meg a megosztást, amelyről való lekérésére konfigurációk és a DSC-erőforrásokat.

A LCM konfigurálásával kapcsolatos további információkért lásd: [ügyféltelepítéshez lekéréses konfigurációs azonosítójával](pullClientConfigID.md).

>**Megjegyzés:** az egyszerűség, a példában a **PSDscAllowPlainTextPassword** engedélyezi a titkosítatlan szöveges jelszó átadja a **Credential** paraméter. További információ a hitelesítő adatok biztonsága érdekében átadásakor: [konfigurációs adatokat a hitelesítő adatok beállítások](configDataCredentials.md).

>**Megjegyzés:** meg kell adnia egy **ConfigurationID** a a **beállítások** egy metakonfigurációját az SMB lekérési kiszolgálójával, még akkor is, ha csak akkor vannak húzza erőforrások blokkja.

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

Különleges környezetnek köszönhetően a következőket:

- Nagy F. Robbins, amelynek bejegyzéseket az SMB protokoll segítségével a DSC segített tájékoztatja a tartalom ebben a témakörben. Jelenleg a blog [nagy F Robbins](http://mikefrobbins.com/).
- Serge Nikalaichyk, akik lett létrehozva a **cNtfsAccessControl** modul. Ez a modul forrásának jelenleg https://github.com/SNikalaichyk/cNtfsAccessControl.

## <a name="see-also"></a>Lásd még:
- [A Windows PowerShell célállapot-konfiguráló áttekintése](overview.md)
- [Konfigurációk életbe léptetése](enactingConfigurations.md)
- [Lekérési ügyfél beállítása konfigurációs azonosítóval](pullClientConfigID.md)

 
