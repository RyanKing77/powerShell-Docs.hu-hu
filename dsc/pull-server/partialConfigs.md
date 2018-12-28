---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Részleges konfigurációk PowerShell Desired State Configuration
ms.openlocfilehash: b2b17e35597707eb97ecdcea9dda4466deeab0cb
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404277"
---
# <a name="powershell-desired-state-configuration-partial-configurations"></a>Részleges konfigurációk PowerShell Desired State Configuration

_A következőkre vonatkozik: Windows PowerShell 5.0-s és újabb verziók._

A PowerShell 5.0-s Desired State Configuration (DSC) lehetővé teszi a konfigurációkat a töredékeket, és a különböző forrásokból származó üzembe helyezhető. A helyi Configuration Manager (LCM) Konfigurálása a cél-csomóponton a szilánkok mielőtt alkalmazná őket, egyetlen konfigurációval együtt helyezi. Ez a funkció lehetővé teszi, hogy a döntés konfigurációról csapatok vagy személyek közötti megosztását. Például ha egy szolgáltatás a fejlesztők két vagy több csapat közreműködő, előfordulhat, hogy minden egyes szeretne létrehozni konfigurációk kezelésére, azok a szolgáltatás részét. Ezek a konfigurációk mindegyike sikerült le kell kérnie a különböző lekéréses kiszolgálót, és különböző szakaszaiban a fejlesztési adható. Részleges konfigurációk is lehetővé teszik különböző csapatok vagy személyek különböző aspektusa csomópontok konfigurálása koordinálására, egy egyetlen konfigurációs dokumentum szerkesztése nélkül. Például egy csapat felelős üzembe helyezése egy virtuális gép és az operációs rendszer, amíg egy másik csapat helyezhetők üzembe, más alkalmazások és szolgáltatások a virtuális gép lehet. Részleges konfigurációk minden egyes csapat hozhat létre a saját konfigurációs nélkül lehet őket szükségtelenül bonyolult folyamatban van.

Részleges konfigurációk leküldéses módban, lekéréses mód vagy a kettő kombinációját is használhatja.

## <a name="partial-configurations-in-push-mode"></a>Részleges konfigurációk leküldési módban

Részleges konfigurációk használata a leküldési módban, konfigurálhatók az LCM Konfigurálása a célcsomópont a részleges konfigurációk fogadásához. Minden egyes részleges konfiguráció a cél használatával lehet leküldeni a `Publish-DSCConfiguration` parancsmagot. A célcsomópont majd egyesíti a részleges egyetlen konfigurációval-konfigurációnak, és alkalmazhatja a konfiguráció meghívásával a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.

### <a name="configuring-the-lcm-for-push-mode-partial-configurations"></a>Az LCM konfigurálása a leküldéses módú részleges konfigurációk

Részleges konfigurációk esetén az LCM konfigurálása a leküldési módban, hozzon létre egy **DSCLocalConfigurationManager** egy konfigurációs **PartialConfiguration** az egyes részleges konfigurációk letiltása. Az LCM konfigurálása kapcsolatos további információkért lásd: [a Local Configuration Manager Windows](/powershell/dsc/metaConfig). Az alábbi példa bemutatja egy LCM konfigurációt, amely a két részleges konfigurációk vár –, amely telepíti az operációs rendszer, a másikat, amely telepíti és konfigurálja a SharePoint.

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

A **RefreshMode** esetében minden egyes részleges konfiguráció "Leküldéses" értékre van állítva. Nevei a **PartialConfiguration** blokkok (ebben az esetben az "ServiceAccountConfig" és "SharePointConfig") a konfigurációk, amelyek akkor lesznek leküldve a célcsomópont a nevei pontosan egyeznie kell.

> [!Note]
> A megnevezett egyes **PartialConfiguration** blokk meg kell egyeznie a tényleges konfiguráció neve szerint van megadva a konfigurációs parancsfájl, nem a MOF-fájlt, amely lehet a cél csomópont nevét, és neve`localhost`.

### <a name="publishing-and-starting-push-mode-partial-configurations"></a>Közzététel és Leküldéses módú részleges konfigurációk indítása

Majd hívja [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) átadja a mappákat, amelyek az egyes konfigurációkhoz konfigurációs dokumentumok tartalmazzák a **elérési út** paramétereket. `Publish-DSCConfiguration`a konfigurációs MOF-fájlok a célcsomópontokat helyezi. Miután közzétette mindkét, meghívhatja `Start-DSCConfiguration –UseExisting` célcsomóponton.

Például ha rendelkezik a következő konfigurációs MOF dokumentumok a szerzői műveletekhez részben csomóponton:

```powershell
Get-ChildItem -Recurse
```

```output
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

Közzé kívánja, majd futtassa a konfiguráció az alábbiak szerint:

```powershell
Publish-DscConfiguration .\ServiceAccountConfig -ComputerName 'TestVM'
Publish-DscConfiguration .\SharePointConfig -ComputerName 'TestVM'
Start-DscConfiguration -UseExisting -ComputerName 'TestVM'
```

```output
Id     Name            PSJobTypeName   State         HasMoreData     Location             Command
--     ----            -------------   -----         -----------     --------             -------
17     Job17           Configuratio... Running       True            TestVM            Start-DscConfiguration...
```

> [!Note]
> A futtató felhasználó az [Publish-DSCConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) parancsmagot rendszergazdai jogosultsággal kell rendelkeznie a célként megadott csomóponton.

## <a name="partial-configurations-in-pull-mode"></a>Részleges konfigurációk lekéréses módban

Részleges konfigurációk is le kell kérnie, egy vagy több lekéréses kiszolgálót a (pull-kiszolgálókkal kapcsolatos további információkért lásd: [Windows PowerShell Desired State Configuration lekéréses kiszolgálók](pullServer.md). Ehhez az szükséges, akkor az LCM konfigurálása a részleges konfigurációk, lekéréses és nevet, és megfelelően keresse meg a konfiguráció a dokumentumokat a lekéréses kiszolgálójára célcsomóponton.

### <a name="configuring-the-lcm-for-pull-node-configurations"></a>Az LCM konfigurálása a pull-csomópont-konfigurációk

Részleges konfigurációk lekéréses kiszolgálóról lekérni az LCM konfigurálása, határozhat meg a lekéréses kiszolgálón vagy egy **ConfigurationRepositoryWeb** (a HTTP-lekéréses kiszolgálón) vagy **ConfigurationRepositoryShare** () az egy SMB-lekérési kiszolgálójának) letiltása. Ezután létre fog hozni **PartialConfiguration** hivatkozni, a lekéréses kiszolgálón használatával blokkolja a **ConfigurationSource** tulajdonság. Is szeretne létrehozni egy **beállítások** letiltása, hogy az LCM lekéréses módban használja-e, és adja meg a **ConfigurationNames** vagy **ConfigurationID** , amely a lekéréses kiszolgálón és a cél csomópont használata a felismerésében. A következő meta-konfiguráció a CONTOSO-PullSrv nevű HTTP-lekéréses kiszolgálón határozza meg, és két részleges konfigurációk, amelyek használják, amely a lekérési kiszolgálón.

Az LCM használatával konfigurálásával kapcsolatos további információkat a **ConfigurationNames**, lásd: [konfigurációs nevek lekérési ügyfél beállítása](pullClientConfigNames.md). Az LCM használatával konfigurálásával kapcsolatos információkat **ConfigurationID**, lásd: [konfigurációs azonosítóval lekérési ügyfél beállítása](pullClientConfigID.md).

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configuration-names"></a>Az LCM konfigurálása a lekérési mód konfigurációk konfigurációs nevekkel

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

#### <a name="configuring-the-lcm-for-pull-mode-configurations-using-configurationid"></a>Az LCM konfigurálása a lekérési mód konfigurációk ConfigurationID használatával

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

Részleges konfigurációk egynél több lekéréses kiszolgálóról kérheti le – ugyanúgy kell minden lekéréses kiszolgálón határozza meg, és ezután tekintse meg a megfelelő lekérési kiszolgálóval **PartialConfiguration** letiltása.

Miután létrehozta a metaadat-konfiguráció, futtatnia kell, hogy hozzon létre egy konfigurációs dokumentumot (MOF-fájlt), és ezután hívja meg [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) az LCM konfigurálása.

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationnames"></a>Kiosztási és a konfigurációs dokumentum elhelyezése a lekérési kiszolgálón (ConfigurationNames)

A részleges konfigurációs dokumentumokat megadott mappába kell helyezni a **ConfigurationPath** a a `web.config` a lekéréses kiszolgálón fájlt (általában `C:\Program
Files\WindowsPowerShell\DscService\Configuration`).

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-51"></a>A lekérési kiszolgálón a PowerShell 5.1 elnevezési konfigurációs dokumentumok

Egy különálló lekéréses kiszolgálóról csak egy részleges konfigurációs van lehetőség, ha a konfigurációs dokumentum rendelkezhet egy tetszőleges nevet. Egy lekéréses kiszolgálóról egynél több részleges konfigurációs van lehetőség, ha a konfigurációs dokumentum elnevezheti vagy `<ConfigurationName>.mof`, ahol *ConfigurationName* a részleges konfiguráció neve vagy `<ConfigurationName>.<NodeName>.mof`, ahol *ConfigurationName* a részleges konfiguráció neve és *csomópontnév* a célcsomópont neve. Ez lehetővé teszi a pull-konfigurációk az Azure Automation DSC lekérési kiszolgálóról.

#### <a name="naming-configuration-documents-on-the-pull-server-in-powershell-50"></a>A lekérési kiszolgálón a PowerShell 5.0 elnevezési konfigurációs dokumentumok

A konfigurációs dokumentum a következő névvel kell rendelkeznie: `ConfigurationName.mof`, ahol *ConfigurationName* a részleges konfiguráció neve. A példánkban a konfigurációs dokumentumokat kell elnevezése a következő:

```
ServiceAccountConfig.mof
ServiceAccountConfig.mof.checksum
SharePointConfig.mof
SharePointConfig.mof.checksum
```

### <a name="naming-and-placing-the-configuration-documents-on-the-pull-server-configurationid"></a>Kiosztási és a konfigurációs dokumentum elhelyezése a lekérési kiszolgálón (ConfigurationID)

A részleges konfigurációs dokumentumokat megadott mappába kell helyezni a **ConfigurationPath** a a `web.config` a lekéréses kiszolgálón fájlt (általában `C:\Program Files\WindowsPowerShell\DscService\Configuration`). A konfigurációs dokumentum a következő névvel kell rendelkeznie: `<ConfigurationName>.<ConfigurationID>.mof`, ahol _ConfigurationName_ a részleges konfiguráció neve és _ConfigurationID_ a konfiguráció azonosítója definiálva van a Az LCM célcsomóponton. A példánkban a konfigurációs dokumentumokat kell elnevezése a következő:

```
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
ServiceAccountConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof
SharePointConfig.1d545e3b-60c3-47a0-bf65-5afc05182fd0.mof.checksum
```

### <a name="running-partial-configurations-from-a-pull-server"></a>Részleges konfigurációk futtatása egy lekéréses kiszolgálóról

Miután az LCM Konfigurálása a célként megadott csomóponton lett konfigurálva, és a konfigurációs dokumentumot létrehozott és a lekérési kiszolgálón megfelelően nevű, a célcsomópont a részleges konfigurációk kéri, kombinálhatja őket, és a alkalmazni az így létrejövő konfiguráció rendszeres által megadott időközönként a **RefreshFrequencyMins** az LCM tulajdonságát. Ha azt szeretné, frissítésének kényszerítése, meghívhatja a [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration) lekérni a konfigurációkat, a parancsmag, majd `Start-DSCConfiguration –UseExisting` a alkalmazni őket.

## <a name="partial-configurations-in-mixed-push-and-pull-modes"></a>A vegyes eseménylekérési részleges konfigurációk

Is kombinálhatók leküldéses és lekéréses részleges konfigurációk módban. Lehet, hogy egy részleges konfigurációval, amely lekéréses kiszolgálóról, miközben egy másik részleges konfigurációs leküldéssel kéri le. Adja meg az egyes részleges konfigurációs frissítési módot, a korábbi szakaszokban ismertetett módon. Például a következő meta-konfiguráció ismerteti az ugyanebben a példában a `ServiceAccountConfig` részleges konfigurációs lekéréses módban, és a `SharePointConfig` részleges konfigurációs leküldési módban.

### <a name="mixed-push-and-pull-modes-using-configurationnames"></a>Vegyes eseménylekérési ConfigurationNames használatával

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

### <a name="mixed-push-and-pull-modes-using-configurationid"></a>Vegyes eseménylekérési ConfigurationID használatával

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

Vegye figyelembe, hogy a **RefreshMode** "Lekérés" található a megadott van, de a **RefreshMode** számára a `SharePointConfig` részleges konfigurációs "Push".

Nevezze el, és keresse meg a konfigurációs MOF-fájlok, a megfelelő frissítési módok esetében fentebb leírtakhoz hasonlóan.
Hívás `Publish-DSCConfiguration` közzététele a `SharePointConfig` részleges konfigurációs, és vagy várjon, amíg a `ServiceAccountConfig` konfiguráció le kell kérnie a a lekéréses kiszolgálón, vagy frissítésének kényszerítése meghívásával [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration).

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

## <a name="see-also"></a>Lásd még:

[Windows PowerShell Desired State Configuration lekéréses kiszolgálók](pullServer.md)

[A helyi Configuration Manager Windows](../managing-nodes/metaConfig.md)