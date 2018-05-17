---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: PowerShell célállapot-konfiguráció részleges konfigurációk
ms.openlocfilehash: e6d80b065ad9e68517d2952b7643e4c611d82a0f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="powershell-desired-state-configuration-partial-configurations"></a>PowerShell célállapot-konfiguráció részleges konfigurációk

>Vonatkozik: A Windows PowerShell 5.0-s és újabb verziók.

PowerShell 5.0 használata esetén a kívánt állapot konfigurációs szolgáltatása (DSC) lehetővé teszi, hogy töredékben és a különböző forrásokból származó kézbesítendő konfigurációk. A helyi Configuration Manager (LCM) célcsomóponton a töredék mielőtt alkalmazná őket egy egyetlen beállításokkal együtt helyezi. Ez a funkció lehetővé teszi, hogy vezérlésének konfigurációs csapatok vagy személyek közötti megosztását.
Például ha két vagy több csoportjai fejlesztők dolgozik, egy szolgáltatás, előfordulhat, hogy minden egyes szeretnék kezelése a saját eszközeiken, a szolgáltatás-konfigurációk létrehozása. Ezek a konfigurációk mindegyikének sikerült igénylése a különböző lekéréses kiszolgálók, és azok különböző szakaszaiban a fejlesztési lehetett hozzáadni. Részleges konfiguráció is engedélyezze a különböző csapatok vagy személyek között különböző jellemzőinek csomópontok konfigurálása anélkül, hogy egyetlen konfigurációs dokumentum szerkesztéséhez koordinálására szabályozására. Például egy csoport előfordulhat, hogy felelős telepítése egy virtuális gép és az operációs rendszer, amíg egy másik csoport központi telepítését egyéb alkalmazások és szolgáltatások a virtuális gépen. Minden team részleges konfigurációk esetén a saját konfigurációs valamelyiken alatt feleslegesen bonyolítja nélkül hozhat létre.

Részleges konfigurációk leküldéses módot, lekéréses mód vagy a kettő kombinációja használható.

## <a name="partial-configurations-in-push-mode"></a>Részleges konfigurációk leküldéses módban
Részleges konfigurációk leküldéses üzemmódban használja, konfigurálnia a LCM fogadására a részleges konfiguráció célcsomóponton. Minden egyes részleges konfiguráció a cél lehet leküldeni a Publish-DSCConfiguration parancsmag használatával. Célcsomóponton majd egyesíti a részleges konfigurációs adatok egyetlen konfigurációja, és hívja a konfigurációs is alkalmazhat a [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) parancsmag.

### <a name="configuring-the-lcm-for-push-mode-partial-configurations"></a>A leküldéses módú részleges konfigurációk LCM konfigurálása
Leküldéses módban a LCM részleges konfigurációk beállításához hozzon létre egy **DSCLocalConfigurationManager** egy konfigurációs **PartialConfiguration** minden egyes részleges konfiguráció blokkja. A LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager Windows](https://technet.microsoft.com/library/mt421188.aspx).
A következő példa bemutatja, hogy két részleges konfigurációk vár LCM konfigurálása során – egy, az operációs rendszer központi telepítését végző és egy, amely telepíti és konfigurálja a SharePoint.

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemo
{
    Node localhost
    {

           PartialConfiguration ServiceAccountConfig
        {
            Description = 'Configuration to add the SharePoint service account to the Administrators group.'
            RefreshMode = 'Push'
        }
           PartialConfiguration SharePointConfig
        {
            Description = 'Configuration for the SharePoint server'
            RefreshMode = 'Push'
        }
    }
}
PartialConfigDemo
```

A **RefreshMode** az egyes részleges beállítás "Leküldéses". Neve a **PartialConfiguration** blokkok (ebben az esetben az "ServiceAccountConfig" és "SharePointConfig") meg kell egyeznie a pontosan a célcsomóponton vannak leküldve konfigurációkat nevét.

>**Megjegyzés:** a megnevezett egyes **PartialConfiguration** blokk meg kell egyeznie a tényleges nevét, a konfiguráció a konfigurációs parancsfájl, a MOF-fájl neve nem a megadott kell lennie, amely nevét, illetve a célcsomóponttal vagy `localhost`.

### <a name="publishing-and-starting-push-mode-partial-configurations"></a>Közzététel, és Leküldéses módú részleges konfigurációk indítása

Majd meghívja a [Publish-DSCConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) átadja a mappákat, amely minden konfigurációs konfigurációs dokumentumok tartalmazzák a **elérési** paraméterek. `Publish-DSCConfiguration`a konfigurációs MOF-fájlok sorbaállítása a célcsomópontokat helyezi. Miután közzétette mindkét konfigurációjában, hívása `Start-DSCConfiguration –UseExisting` célcsomóponton.

Ha például azzal állítottuk össze a következő konfigurációs MOF dokumentumokat a szerzői műveletekhez csomóponton:

```powershell
PS C:\PartialConfigTest> Get-ChildItem -Recurse


    Directory: C:\PartialConfigTest


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        8/11/2016   1:55 PM                ServiceAccountConfig
d-----       11/17/2016   4:14 PM                SharePointConfig


    Directory: C:\PartialConfigTest\ServiceAccountConfig


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        8/11/2016   2:02 PM           2034 TestVM.mof


    Directory: C:\DscTests\SharePointConfig


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       11/17/2016   4:14 PM           1930 TestVM.mof
```

Szeretné közzétenni, és futtassa a konfiguráció a következőképpen:

```powershell
PS C:\PartialConfigTest> Publish-DscConfiguration .\ServiceAccountConfig -ComputerName 'TestVM'
PS C:\PartialConfigTest> Publish-DscConfiguration .\SharePointConfig -ComputerName 'TestVM'
PS C:\PartialConfigTest> Start-DscConfiguration -UseExisting -ComputerName 'TestVM'

Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
17     Job17           Configuratio... Running       True            TestVM            Start-DscConfiguration...
```

>**Megjegyzés:** futtató felhasználó az [Publish-DSCConfiguration](https://msdn.microsoft.com/powershell/reference/5.1/psdesiredstateconfiguration/publish-dscconfiguration) parancsmag a célcsomóponton lévő rendszergazdai jogosultsággal kell rendelkeznie.

## <a name="partial-configurations-in-pull-mode"></a>Részleges konfigurációk lekéréses módban

Részleges konfigurációk is lekért egy vagy több lekéréses kiszolgáló (lekéréses-kiszolgálókkal kapcsolatos további információkért lásd: [Windows PowerShell kívánt állapot konfigurációs lekéréses kiszolgálók](pullServer.md). Ehhez az szükséges, hogy a LCM konfigurálnia a részleges konfigurációk, lekéréses és nevet, és megfelelően keresse meg a konfigurációs dokumentumokat a lekérési kiszolgálón célcsomóponton.

### <a name="configuring-the-lcm-for-pull-node-configurations"></a>A csomópont-konfigurációk lekéréses LCM konfigurálása

A lekérési kiszolgálójáról részleges konfigurációk le tudja LCM konfigurálásához adhat meg a lekérési kiszolgálójával vagy egy **ConfigurationRepositoryWeb** (a HTTP-lekérési kiszolgálón) vagy **ConfigurationRepositoryShare** () az SMB-lekérési kiszolgálón) blokkot. Ezután létrehozhat **PartialConfiguration** mutatnak a lekérési kiszolgálójával használatával tekintse meg a **ConfigurationSource** tulajdonság. Is szeretne létrehozni egy **beállítások** blokk megadásához, hogy a LCM lekéréses módot használ, és adja meg a **ConfigurationNames** vagy **ConfigurationID** , amely a lekérési kiszolgálójával, és cél csomópont használja a felismerésében. A következő metaadat-konfiguráció a CONTOSO-PullSrv nevű HTTP-lekérési kiszolgálón határozza meg, és használja, amely két részleges konfigurációkat lekérési kiszolgálón.

A LCM történő konfigurálásáról további információt a **ConfigurationNames**, lásd: [ügyféltelepítéshez lekéréses konfigurációs nevek használatával](pullClientConfigNames.md).
További információk a LCM történő konfigurálásáról **ConfigurationID**, lásd: [ügyféltelepítéshez lekéréses konfigurációs azonosítójával](pullClientConfigID.md).

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configuration-names"></a>Lekéréses mód konfigurációk konfigurációs nevek használatával LCM konfigurálása

```powershell
[DscLocalConfigurationManager()]
Configuration PartialConfigDemoConfigNames
{
        Settings
        {
            RefreshFrequencyMins            = 30;
            RefreshMode                     = "PULL";
            ConfigurationMode               ="ApplyAndAutocorrect";
            AllowModuleOverwrite            = $true;
            RebootNodeIfNeeded              = $true;
            ConfigurationModeFrequencyMins  = 60;
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey                 = 5b41f4e6-5e6d-45f5-8102-f2227468ef38
            ConfigurationNames              = @("ServiceAccountConfig", "SharePointConfig")
        }

        PartialConfiguration ServiceAccountConfig
        {
            Description                     = "ServiceAccountConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
        }

        PartialConfiguration SharePointConfig
        {
            Description                     = "SharePointConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
        }

}
```

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configurationid"></a>Lekéréses mód konfigurációk használatával ConfigurationID LCM konfigurálása

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemoConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode                     = 'Pull'
            ConfigurationID                 = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins            = 30
            RebootNodeIfNeeded              = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }

           PartialConfiguration ServiceAccountConfig
        {
            Description                     = 'Configuration for the Base OS'
            ConfigurationSource             = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            RefreshMode                     = 'Pull'
        }
           PartialConfiguration SharePointConfig
        {
            Description                     = 'Configuration for the Sharepoint Server'
            ConfigurationSource             = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode                     = 'Pull'
        }
    }
}
PartialConfigDemo
```

Képes lekérni a részleges konfigurációk egynél több lekérési kiszolgálójáról – egyes lekéréses kiszolgálók meghatározása, és majd tekintse át a megfelelő lekérési kiszolgálójával, az egyes ugyanúgy kell **PartialConfiguration** blokkot.

Miután létrehozta a metaadat-konfiguráció, futtatnia kell, hogy hozzon létre egy konfigurációs dokumentumot (MOF-fájlt), és majd meghívják a [Set-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621(v=wps.630).aspx) a LCM konfigurálásához.

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationnames"></a>Kiosztási és helyezi el a konfigurációs dokumentumok a lekérési kiszolgálón (ConfigurationNames)

A megadott mappába kell helyezni a részleges konfigurációs dokumentumok a **ConfigurationPath** a a `web.config` a lekérési kiszolgálójával fájlt (általában `C:\Program Files\WindowsPowerShell\DscService\Configuration`).

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-51"></a>A lekérési kiszolgálón PowerShell 5.1 elnevezési konfigurációs dokumentumok

Ha csak egy részleges konfigurációs lekéréses kiszolgálóról vannak húzza, a konfigurációs dokumentum lehet-e bármely nevük.
A lekérési kiszolgálójáról egynél több részleges konfigurációs rendszer húzza, ha a konfigurációs dokumentum elnevezheti vagy `<ConfigurationName>.mof`, ahol _ConfigurationName_ a részleges konfiguráció neve vagy `<ConfigurationName>.<NodeName>.mof`, ahol  _ConfigurationName_ a részleges konfiguráció neve és _csomópontnév_ célcsomóponton neve.
Ez lehetővé teszi a lekéréses beállításokat Azure Automation DSC lekérési kiszolgálójáról.


#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-50"></a>A lekérési kiszolgálón PowerShell 5.0-s elnevezési konfigurációs dokumentumok

A konfigurációs dokumentumok kell elnevezése a következő: `ConfigurationName.mof`, ahol _ConfigurationName_ a részleges konfiguráció neve. A fenti példában a konfigurációs dokumentumok nevet kell adni az alábbiak szerint:

```
ServiceAccountConfig.mof
ServiceAccountConfig.mof.checksum
SharePointConfig.mof
SharePointConfig.mof.checksum
```

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationid"></a>Kiosztási és helyezi el a konfigurációs dokumentumok a lekérési kiszolgálón (ConfigurationID)

A megadott mappába kell helyezni a részleges konfigurációs dokumentumok a **ConfigurationPath** a a `web.config` a lekérési kiszolgálójával fájlt (általában `C:\Program Files\WindowsPowerShell\DscService\Configuration`). A konfigurációs dokumentumok kell elnevezése a következő: _ConfigurationName_. _ConfigurationID_`.mof`, ahol _ConfigurationName_ a részleges konfiguráció neve és _ConfigurationID_ a konfiguráció azonosítója definiálva van a célszámítógépen LCM csomópont. A fenti példában a konfigurációs dokumentumok nevet kell adni az alábbiak szerint:

```
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
```


### <a name="running-partial-configurations-from-a-pull-server"></a>A lekérési kiszolgálójáról részleges konfigurációk futtatása

Miután célcsomóponton LCM van konfigurálva, és a konfigurációs dokumentumot létrehozott és a lekérési kiszolgálón megfelelően nevű, a célcsomóponton fogja lekérni a részleges konfigurációk, ötvözze őket, és rendszeres az eredményként létrejövő konfiguráció alkalmazása által meghatározott időközönként a **RefreshFrequencyMins** a LCM tulajdonsága. Szeretne frissítésének kényszerítése, ha hívása a [frissítés-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541.aspx) parancsmag való lekérésére a konfigurációk, majd `Start-DSCConfiguration –UseExisting` alkalmazás érdekében.


## <a name="partial-configurations-in-mixed-push-and-pull-modes"></a>A vegyes eseménylekérési és eseményküldési módban részleges konfigurációk

Is kombinálhatók leküldéses és lekéréses módok részleges konfigurációk. Ez azt jelenti, hogy egy részleges konfigurációs lekérési kiszolgálójáról, miközben egy másik részleges konfigurációs fejlesztőre beillesztett lehet. Adja meg a frissítési mód minden részleges konfiguráció, a korábbi szakaszokban ismertetett módon.
Például a következő metaadat-konfiguráció ismerteti az ugyanebben a példában a `ServiceAccountConfig` lekéréses módban részleges konfigurációs és a `SharePointConfig` részleges konfigurációs leküldéses módban.

### <a name="mixed-push-and-pull-modes-using-configurationnames"></a>Vegyes eseménylekérési és eseményküldési módban ConfigurationNames használatával

```powershell
[DscLocalConfigurationManager()]
Configuration PartialConfigDemoConfigNames
{
        Settings
        {
            RefreshFrequencyMins            = 30;
            RefreshMode                     = "PULL";
            ConfigurationMode               = "ApplyAndAutocorrect";
            AllowModuleOverwrite            = $true;
            RebootNodeIfNeeded              = $true;
            ConfigurationModeFrequencyMins  = 60;
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL                       = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey                 = 5b41f4e6-5e6d-45f5-8102-f2227468ef38
            ConfigurationNames              = @("ServiceAccountConfig", "SharePointConfig")
        }

        PartialConfiguration ServiceAccountConfig
        {
            Description                     = "ServiceAccountConfig"
            ConfigurationSource             = @("[ConfigurationRepositoryWeb]CONTOSO-PullSrv")
            RefreshMode                     = 'Pull'
        }

        PartialConfiguration SharePointConfig
        {
            Description                     = "SharePointConfig"
            DependsOn                       = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode                     = 'Push'
        }

}
```

### <a name="mixed-push-and-pull-modes-using-configurationid"></a>Vegyes eseménylekérési és eseményküldési módban ConfigurationID használatával

```powershell
[DSCLocalConfigurationManager()]
configuration PartialConfigDemo
{
    Node localhost
    {
        Settings
        {
            RefreshMode             = 'Pull'
            ConfigurationID         = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins    = 30
            RebootNodeIfNeeded      = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL               = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }

           PartialConfiguration ServiceAccountConfig
        {
            Description             = 'Configuration for the Base OS'
            ConfigurationSource     = '[ConfigurationRepositoryWeb]CONTOSO-PullSrv'
            RefreshMode             = 'Pull'
        }
           PartialConfiguration SharePointConfig
        {
            Description             = 'Configuration for the Sharepoint Server'
            DependsOn               = '[PartialConfiguration]ServiceAccountConfig'
            RefreshMode             = 'Push'
        }
    }
}
PartialConfigDemo
```

Vegye figyelembe, hogy a **RefreshMode** "Pull", a beállítások blokk megadott van, de a **RefreshMode** a a `SharePointConfig` részleges beállítás "Push".

Név, és keresse meg a konfigurációs MOF-fájlok, a megfelelő frissítési módok a fent leírt módon. Hívás **Publish-DSCConfiguration** közzététele a `SharePointConfig` részleges konfigurációs, és vagy várja meg a `ServiceAccountConfig` konfiguráció kell húzni a lekérési kiszolgálójáról, vagy frissítésének kényszerítése meghívásával [ Frissítés-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541(v=wps.630).aspx).

## <a name="example-serviceaccountconfig-partial-configuration"></a>Példa ServiceAccountConfig részleges konfiguráció

```powershell
Configuration ServiceAccountConfig
{
    Param (
        [Parameter(Mandatory,
                   HelpMessage="Domain credentials required to add domain\sharepoint_svc to the local Administrators group.")]
        [ValidateNotNullOrEmpty()]
        [pscredential]$Credential
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration


    Node localhost
    {
        Group LocalAdmins
        {
            GroupName           = 'Administrators'
            MembersToInclude    = 'domain\sharepoint_svc',
                                  'admins@example.domain'
            Ensure              = 'Present'
            Credential          = $Credential

        }

        WindowsFeature Telnet
        {
            Name                = 'Telnet-Server'
            Ensure              = 'Absent'
        }
    }
}
ServiceAccountConfig

```
## <a name="example-sharepointconfig-partial-configuration"></a>Példa SharePointConfig részleges konfiguráció
```powershell
Configuration SharePointConfig
{
    Param (
        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [pscredential]$ProductKey
    )

    Import-DscResource -ModuleName xSharePoint

    Node localhost
    {
        xSPInstall SharePointDefault
        {
            Ensure      = 'Present'
            BinaryDir   = '\\FileServer\Installers\Sharepoint\'
            ProductKey  = $ProductKey
        }
    }
}
SharePointConfig
```
##<a name="see-also"></a>Lásd még:

**Fogalmak**
[Windows PowerShell célállapot-konfiguráló lekéréses kiszolgálók](pullServer.md)

[A Windows a helyi Configuration Manager konfigurálása](https://technet.microsoft.com/library/mt421188.aspx)