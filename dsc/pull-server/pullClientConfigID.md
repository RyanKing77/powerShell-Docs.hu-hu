---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs azonosítók PowerShell 5.0-s és újabb verziók használata lekérési ügyfél beállítása
ms.openlocfilehash: 14db98d240bc87aca3ee985db08c14b7c65d8bb8
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079489"
---
# <a name="set-up-a-pull-client-using-configuration-ids-in-powershell-50-and-later"></a>Konfigurációs azonosítók PowerShell 5.0-s és újabb verziók használata lekérési ügyfél beállítása

> A következőkre vonatkozik: Windows PowerShell 5.0

> [!IMPORTANT]
> A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak. Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).

Lekérési ügyfél beállítása előtt be kell állítania egy lekéréses kiszolgálót. Bár nem kötelező ebben a sorrendben, segít a hibák elhárításában, és így gondoskodik róla, hogy a regisztráció sikeres volt-e. Állítson be egy lekéréses kiszolgálót, használhatja a következő útmutatókat:

- [DSC SMB-lekérési kiszolgáló beállítása](pullServerSmb.md)
- [A DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md)

Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát. Az alábbi szakaszok bemutatják, hogyan lekérési ügyfél beállítása egy SMB-megosztáson, vagy a HTTP-DSC lekéréses kiszolgálón. Amikor a csomópont LCM frissíti, a konfigurált helyre, töltse le a hozzárendelt konfigurációkat, felveszi Önnel. Ha minden szükséges erőforrás nem létezik a csomóponton, azt automatikusan letöltheti őket a beállított helyről. Ha a csomópont konfigurálva van egy [jelentéskészítő kiszolgáló](reportServer.md), majd a művelet állapotát jelzi.

> [!NOTE]
> Ez a témakör a PowerShell 5.0-s vonatkozik. A PowerShell 4.0-s lekérési ügyfél beállításával kapcsolatos további információkért lásd: [egy lekérési ügyfél beállítása konfigurációs Azonosítóval a PowerShell 4.0-s](pullClientConfigID4.md)

## <a name="configure-the-pull-client-lcm"></a>Lekérési ügyfél LCM konfigurálása

Az alábbi példák bármelyikét végrehajtása hoz létre egy új nevű kimeneti mappát **PullClientConfigID** , és ott helyezi metaconfiguration MOF-fájlt. Ebben az esetben a metaconfiguration MOF-fájl neve lesz `localhost.meta.mof`.

A alkalmazni a konfigurációt, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési út** állítsa be a metaconfiguration MOF-fájl helyét. Például:

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigId –Verbose.
```

## <a name="configuration-id"></a>Konfiguráció azonosítója

Csoportok alábbi példák a **ConfigurationID** , az LCM tulajdonságát egy **Guid** , amely korábban létrehozott erre a célra. A **ConfigurationID** van, használja az LCM Konfigurálása a megfelelő konfiguráció keresése a lekérési kiszolgálón. A lekérési kiszolgálón a konfigurációs MOF-fájl neve legyen `ConfigurationID.mof`, ahol *ConfigurationID* értéke a **ConfigurationID** a célcsomópont LCM tulajdonságát. További információ: [konfigurációk közzététele egy lekéréses kiszolgálóra (v4 vagy v5)](publishConfigs.md).

Létrehozhat egy véletlenszerű **Guid** alább, vagy használja a példánál a [új GUID-azonosítója](/powershell/module/microsoft.powershell.utility/new-guid) parancsmagot.

```powershell
[System.Guid]::NewGuid()
```

Használatával kapcsolatos további részletekért **GUID** a környezetben, lásd: [GUID tervezése](/powershell/dsc/secureserver#guids).

## <a name="set-up-a-pull-client-to-download-configurations"></a>Lekérési ügyfél beállítása a konfiguráció letöltése

Minden egyes ügyfélnek meg kell adni a **lekéréses** módban, és a pull-kiszolgáló URL-címét a konfigurációja tárolására. Ehhez az szükséges, akkor a helyi Configuration Manager (LCM) konfigurálása a szükséges információkat. Az LCM konfigurálása, a konfiguráció, a kitüntetett különleges hoz létre a **DSCLocalConfigurationManager** attribútum. Az LCM konfigurálása kapcsolatos további információkért lásd: [a Local Configuration Manager](../managing-nodes/metaConfig.md).

### <a name="http-dsc-pull-server"></a>HTTP DSC Pull Server

A következő szkriptet az LCM lekéréses konfigurációk úgy konfigurálja a kiszolgáló neve "CONTOSO-PullSrv".

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

A parancsfájl a **ConfigurationRepositoryWeb** blokk határozza meg a lekéréses kiszolgálón. A **ServerUrl** adja meg az URL-címét a DSC lekéréses

### <a name="smb-share"></a>SMB-megosztás

A következő szkriptet az LCM konfigurálja lekéréses konfigurációk az SMB-megosztás a `\\SMBPullServer\Pull`.

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
            SourcePath = '\\SMBPullServer\Pull'
        }
    }
}
PullClientConfigID
```

A parancsfájl a **ConfigurationRepositoryShare** letiltása a lekéréses kiszolgálón, amely ebben az esetben csak az SMB-megosztás határozza meg.

## <a name="set-up-a-pull-client-to-download-resources"></a>Lekérési ügyfél beállítása az erőforrások letöltéséhez

Ha csak adja meg a **ConfigurationRepositoryWeb** vagy **ConfigurationRepositoryShare** letiltása az LCM konfigurálása (a korábbi példákhoz), a lekéréses ügyfél kéri az azonos erőforrásokat a hely lekéri a konfigurációt. Megadhat az erőforrások eltérő helyekről is. Önálló kiszolgálóként egy erőforrás helyének megadásához használja a **ResourceRepositoryWeb** letiltása. Egy erőforrás helye, SMB-megosztáson megadásához használja a **ResourceRepositoryShare** letiltása.

> [!NOTE]
> Kombinálhatja **ConfigurationRepositoryWeb** a **ResourceRepositoryShare** vagy **ConfigurationRepositoryShare** a **ResourceRepositoryWeb** . Erre vonatkozó példákat nem látható az alábbiakban.

### <a name="http-dsc-pull-server"></a>HTTP DSC Pull Server

A következő metaconfiguration konfigurálja beolvasni a konfigurációkat a lekérési ügyfél **CONTOSO-PullSrv** és erőforrását **CONTOSO-ResourceSrv**.

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
    }
}
PullClientConfigID
```

### <a name="smb-share"></a>SMB-megosztás

Az alábbi példa bemutatja, hogy az SMB-megosztás a pull-konfigurációk úgy állít be egy ügyfél egy metaconfiguration `\\SMBPullServer\Configurations`, és erőforrásokat, az SMB-megosztás `\\SMBPullServer\Resources`.

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
            SourcePath = '\\SMBPullServer\Configurations'
        }

        ResourceRepositoryShare SMBResourceServer
        {
            SourcePath = '\\SMBPullServer\Resources'
        }
    }
}
PullClientConfigID
```

#### <a name="automatically-download-resources-in-push-mode"></a>Automatikus letöltése a leküldési módban erőforrások

A PowerShell 5.0-es verziótól kezdve a pull-ügyfelek is letölthető modulok SMB-megosztáson, akkor is, ha vannak konfigurálva **leküldéses** mód. Ez különösen hasznos forgatókönyvekben, ahol nem szeretné beállítani egy lekéréses kiszolgálót. A **ResourceRepositoryShare** blokk megadása nélkül is használható egy **ConfigurationRepositoryShare**. Az alábbi példa bemutatja egy metaconfiguration, amely beállítja egy ügyfél lekéréses erőforrásokhoz az SMB-megosztáson `\\SMBPullServer\Resources`. Amikor a csomópont nem **PUSHED** konfigurációt, azt automatikusan letölti bármilyen szükséges erőforrásokat a a megadott megosztás.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigID
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Push'
            ConfigurationID = '1d545e3b-60c3-47a0-bf65-5afc05182fd0'
        }

        ResourceRepositoryShare SMBResourceServer
        {
            SourcePath = '\\SMBPullServer\Resources'
        }
    }
}
PullClientConfigID
```

## <a name="set-up-a-pull-client-to-report-status"></a>Állapot jelentése érdekében a lekérési ügyfél beállítása

Alapértelmezés szerint csomópontok nem küldenek jelentéseket konfigurált lekéréses kiszolgálón. Egy lekéréses kiszolgálót használhat a konfigurációk, az erőforrások és a jelentéskészítés, de létre kell hoznia egy **ReportRepositoryWeb** beállítása a jelentéskészítési letiltása.

### <a name="http-dsc-pull-server"></a>HTTP DSC Pull Server

Az alábbi példa bemutatja egy metaconfiguration, amely beállítja a pull-konfigurációkat és erőforrásokat, majd küldje el jelentésadatokat, egyetlen lekéréses kiszolgálóra ügyfelet.

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

A jelentéskészítő kiszolgáló megadásához használja a **ReportRepositoryWeb** letiltása. A jelentéskészítő kiszolgáló nem lehet SMB-kiszolgálón.
A következő metaconfiguration konfigurálja beolvasni a konfigurációkat a lekérési ügyfél **CONTOSO-PullSrv** és erőforrását **CONTOSO-ResourceSrv**, és a jelentések küldéséhez  **CONTOSO-ReportSrv**:

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

### <a name="smb-share"></a>SMB-megosztás

A jelentéskészítő kiszolgáló nem lehet SMB-megosztáson.

## <a name="next-steps"></a>Következő lépések

A lekérési ügyfél beállítása után a következő útmutatók használatával hajtsa végre a következő lépéseket:

- [Konfigurációk közzétételére egy lekéréses kiszolgálót (v4 vagy v5)](publishConfigs.md)
- [Csomag és a egy lekéréses kiszolgálót (v4) erőforrás feltöltése](package-upload-resources.md)

## <a name="see-also"></a>Lásd még:

* [A konfigurációs nevek lekérési ügyfél beállítása](pullClientConfigNames.md)
