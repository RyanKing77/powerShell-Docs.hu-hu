---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Lekérési ügyfél beállítása konfigurációs azonosítóval
ms.openlocfilehash: 95dfb4a182f9ecf592ae8c53e47fde4418ed6a8a
ms.sourcegitcommit: ece1794c94be4880a2af5a2605ed4721593643b6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/16/2018
---
# <a name="setting-up-a-pull-client-using-configuration-id"></a>Lekérési ügyfél beállítása konfigurációs azonosítóval

> Vonatkozik: A Windows PowerShell 5.0

> [!IMPORTANT]
> A lekéréses kiszolgáló (Windows-szolgáltatás *DSC-szolgáltatás*), Windows Server támogatott összetevője létezik azonban a következők: nem tervezi, hogy új funkciók és képességek kínálnak. Javasoljuk, hogy kezdje a Váltás felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (tartalmazza a Windows Server-kiszolgáló lekéréses is) vagy a közösségi megoldásoknak a valamelyikét felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).

Minden egyes célcsomóponttal lekéréses módban a rendszergazda és az URL-címet kap, ahol lépjen kapcsolatba a lekérési kiszolgálójával konfigurációt beolvasandó ki. Ehhez az szükséges, hogy a helyi Configuration Manager (LCM) konfigurálnia a szükséges adatokat. A LCM konfigurálásához hoz létre egy speciális konfigurációs attribútummal. az **DSCLocalConfigurationManager** attribútum. A LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md).

> **Megjegyzés:**: Ez a témakör PowerShell 5.0 vonatkozik. A PowerShell 4.0 lekéréses ügyfél beállításával kapcsolatos információkért lásd: [konfigurációs azonosítójával PowerShell 4.0 lekéréses ügyfél beállítása](pullClientConfigID4.md)

A következő parancsfájl úgy konfigurálja a LCM lekéréses konfigurációk "CONTOSO-PullSrv" nevű kiszolgálóról.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }
    }
}
PullClientConfigID
```

A parancsfájl a **ConfigurationRepositoryWeb** blokk határozza meg a lekérési kiszolgálójával. A **kiszolgáló URL-címe**

A parancsfájl futtatása után a rendszer létrehoz egy új kimeneti mappát **PullClientConfigID** , és nincs helyezi metakonfigurációját MOF-fájlt. Ebben az esetben a metakonfigurációját MOF-fájl neve lehet `localhost.meta.mof`.

A konfiguráció alkalmazásához, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési** beállítása a metakonfigurációját MOF-fájl helyét. Például: `Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigID –Verbose.`

## <a name="configuration-id"></a>Konfiguráció azonosítója

A parancsfájl beállítása a **ConfigurationID** korábban erre a célra létrehozott egyedi azonosítóvá LCM tulajdonságának (GUID segítségével létrehozható a **New-Guid** parancsmag). A **ConfigurationID** van a LCM használja a megfelelő konfigurációja a lekérési kiszolgálón található. A konfigurációs MOF-fájlt a lekérési kiszolgálón névvel kell ellátni _ConfigurationID_.mof, ahol _ConfigurationID_ értéke a **ConfigurationID** a TARGET tulajdonság csomópont LCM.

## <a name="smb-pull-server"></a>SMB-lekérési kiszolgálón

Állíthat be egy ügyfél lekéréses konfigurációi az SMB-kiszolgálón, használja a **ConfigurationRepositoryShare** blokkot. Az egy **ConfigurationRepositoryShare** blokkot, a kiszolgáló elérési útvonalát úgy, hogy adja meg a **SourcePath** tulajdonság. A következő metakonfigurációját konfigurálja a célcsomóponton való lekérésére egy SMB lekérési kiszolgálójáról nevű **SMBPullServer**.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryShare SMBPullServer
        {
            SourcePath = '\\SMBPullServer\PullSource'

        }
    }
}
PullClientConfigID
```

## <a name="resource-and-report-servers"></a>Erőforrás-és a jelentés

Ha csak adja meg a **ConfigurationRepositoryWeb** vagy **ConfigurationRepositoryShare** (ahogy az előző példában) LCM konfigurációs letiltása, a lekéréses ügyfél erőforrásokat fogja lekérni a megadott kiszolgálón, de nem küld jelentéseket rá. Konfigurációk, erőforrások és jelentéskészítési olyan egyetlen lekéréses kiszolgálót is használhat, de létre kell hoznia egy **ReportRepositoryWeb** blokk jelentéskészítés beállítása.

A következő példa bemutatja egy metakonfigurációját állítja be az ügyfél lekéréses konfigurációk és az erőforrások és a jelentés adatainak, lekéréses egyetlen kiszolgálóra történő küldés.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }


        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

Az erőforrások és a jelentéskészítő különböző lekéréses kiszolgálók is megadható. Adjon meg egy erőforrás-kiszolgáló, használhatja a **ResourceRepositoryWeb** (a lekéréses webkiszolgálók) vagy egy **ResourceRepositoryShare** blokk (az SMB-lekérési kiszolgálón).
Adja meg a jelentéskészítő kiszolgálón, akkor használja a **ReportRepositoryWeb** blokkot. A jelentéskészítő kiszolgáló nem lehet egy SMB-kiszolgálón.
A következő metakonfigurációját beállítja a konfigurációk a beolvasandó lekéréses ügyfél **CONTOSO-PullSrv** és erőforrását **CONTOSO-ResourceSrv**, és a jelentések küldése  **CONTOSO-ReportSrv**:

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'

        }

        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-REsourceSrv:8080/PSDSCPullServer.svc'
        }
    }
}
PullClientConfigID
```

## <a name="see-also"></a>Lásd még:

* [Konfigurációs nevek lekéréses ügyfél beállítása](pullClientConfigNames.md)