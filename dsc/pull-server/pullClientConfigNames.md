---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs nevekkel PowerShell 5.0-s és újabb verziók lekérési ügyfél beállítása
ms.openlocfilehash: fd038a105da7a83ecad9b571e611b65c8ec847b3
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404416"
---
# <a name="set-up-a-pull-client-using-configuration-names-in-powershell-50-and-later"></a>Konfigurációs nevekkel PowerShell 5.0-s és újabb verziók lekérési ügyfél beállítása

> Érvényes: Windows PowerShell 5.0

> [!IMPORTANT]
> A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak. Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).

Lekérési ügyfél beállítása előtt be kell állítania egy lekéréses kiszolgálót. Bár nem kötelező ebben a sorrendben, segít a hibák elhárításában, és így gondoskodik róla, hogy a regisztráció sikeres volt-e. Állítson be egy lekéréses kiszolgálót, használhatja a következő útmutatókat:

- [DSC SMB-lekérési kiszolgáló beállítása](pullServerSmb.md)
- [A DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md)

Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát. Az alábbi szakaszok bemutatják, hogyan lekérési ügyfél beállítása egy SMB-megosztáson, vagy a HTTP-DSC lekéréses kiszolgálón. Amikor a csomópont LCM frissíti, a konfigurált helyre, töltse le a hozzárendelt konfigurációkat, felveszi Önnel. Ha minden szükséges erőforrás nem létezik a csomóponton, azt automatikusan letöltheti őket a beállított helyről. Ha a csomópont konfigurálva van egy [jelentéskészítő kiszolgáló](reportServer.md), majd a művelet állapotát jelzi.

> **Megjegyzés:**: Ez a témakör a PowerShell 5.0-s vonatkozik.
A PowerShell 4.0-s lekérési ügyfél beállításával kapcsolatos további információkért lásd: [konfigurációs azonosító használatával a PowerShell 4.0-s lekérési ügyfél beállítása](pullClientConfigID4.md)

## <a name="configure-the-pull-client-lcm"></a>Lekérési ügyfél LCM konfigurálása

Az alábbi példák bármelyikét végrehajtása hoz létre egy új nevű kimeneti mappát **PullClientConfigName** , és ott helyezi metaconfiguration MOF-fájlt. Ebben az esetben a metaconfiguration MOF-fájl neve lesz `localhost.meta.mof`.

A alkalmazni a konfigurációt, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési út** állítsa be a metaconfiguration MOF-fájl helyét. Például:

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigName –Verbose.
```

## <a name="configuration-name"></a>Konfiguráció neve

Csoportok alábbi példák a **ConfigurationName** egy korábban lefordított konfiguráció nevét a LCM tulajdonságát erre a célra létrehozott. A **ConfigurationName** van, használja az LCM Konfigurálása a megfelelő konfiguráció keresése a lekérési kiszolgálón. A lekérési kiszolgálón a konfigurációs MOF-fájl neve legyen `<ConfigurationName>.mof`, ebben az esetben "ClientConfig.mof". További információkért lásd: [konfigurációk közzététele egy lekéréses kiszolgálóra (v4 vagy v5)](publishConfigs.md).

## <a name="set-up-a-pull-client-to-download-configurations"></a>Lekérési ügyfél beállítása a konfiguráció letöltése

Minden egyes ügyfélnek meg kell adni a **lekéréses** módban, és a pull-kiszolgáló URL-címét a konfigurációja tárolására. Ehhez az szükséges, akkor a helyi Configuration Manager (LCM) konfigurálása a szükséges információkat. Az LCM konfigurálása, a konfiguráció, a kitüntetett különleges hoz létre a **DSCLocalConfigurationManager** attribútum. Az LCM konfigurálása kapcsolatos további információkért lásd: [a Local Configuration Manager](../managing-nodes/metaConfig.md).

A következő szkriptet az LCM lekéréses konfigurációk úgy konfigurálja a kiszolgáló neve "CONTOSO-PullSrv".

- A parancsfájl a **ConfigurationRepositoryWeb** blokk határozza meg a lekéréses kiszolgálón. A **ServerURL** tulajdonsága azt adja meg a végpont a lekéréses kiszolgálón.

- A **RegistrationKey** tulajdonság egy lekéréses kiszolgálón található összes ügyfél csomópont és a lekéréses kiszolgálón között megosztott kulcs. Ugyanazt az értéket egy fájlt a lekérési kiszolgálón van tárolva.
  > **Megjegyzés:**: Regisztrációs kulcs csak a munkahelyi **webes** kiszolgálók lekérése. Továbbra is kell használnia **ConfigurationID** együtt egy **SMB** lekéréses kiszolgálón.
  > Használatával egy lekéréses kiszolgálót konfigurálásával kapcsolatos információkat **ConfigurationID**, lásd: [konfigurációs azonosítóval lekérési ügyfél beállítása](pullClientConfigId.md)

- A **ConfigurationNames** tulajdonság értéke egy tömb, amely megadja azoknak szól, az ügyfél csomópont-konfigurációk a nevét.
  >**Megjegyzés:** Ha egynél több értéket adja meg a **ConfigurationNames**, meg kell adnia **PartialConfiguration** letiltja a konfigurációban.
  >Részleges konfigurációk kapcsolatos további információkért lásd: [PowerShell Desired State Configuration részleges konfigurációk](partialConfigs.md).

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('ClientConfig')
        }
    }
}
PullClientConfigNames
```

## <a name="set-up-a-pull-client-to-download-resources"></a>Lekérési ügyfél beállítása az erőforrások letöltéséhez

Ha csak adja meg egy **ConfigurationRepositoryWeb** vagy **ConfigurationRepositoryShare** letiltása az LCM konfigurálása (ahogy az előző példában), a lekérési ügyfél azonos erőforrásokat kéri a ".mof" fájlokat tároló helye. Emellett megadhatja a különböző helyeken, ahol az ügyfelek erőforrások letöltéséhez. Adja meg az erőforrás-kiszolgáló, használhatja a **ResourceRepositoryWeb** (a lekérési kiszolgáló) vagy egy **ResourceRepositoryShare** letiltása (a egy SMB-lekérési kiszolgálójának).

Az alábbi példa bemutatja egy metaconfiguration, amely ügyfél beállítja a konfigurációkat egy lekéréses kiszolgálót és erőforrásokat, SMB-megosztáson töltheti le.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }

        ResourceRepositoryShare SMBResources
        {
            SourcePath = '\\SMBPullServer\Resources'
        }
    }
}
PullClientConfigNames
```

## <a name="set-up-a-pull-client-to-report-status"></a>Állapot jelentése érdekében a lekérési ügyfél beállítása

Egy lekéréses kiszolgálót használhat a konfigurációk, erőforrások és jelentéskészítés. Jelentéskészítés nincs konfigurálva az ügyfelek alapértelmezés szerint. Állapot jelentése érdekében egy ügyfél konfigurálásához létre kell hoznia egy **ReportRepositoryWeb** letiltása. Az alábbi példa bemutatja egy metaconfiguration, amely beállítja a pull-konfigurációkat és erőforrásokat, majd küldje el jelentésadatokat, egyetlen lekéréses kiszolgálóra ügyfelet.

> [!NOTE]
> A jelentéskészítő kiszolgáló nem lehet SMB-megosztáson.

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientConfigNames
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }

        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }

        ReportServerWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = 'fbc6ef09-ad98-4aad-a062-92b0e0327562'
        }
    }
}
PullClientConfigNames
```

## <a name="see-also"></a>Lásd még:

* [Konfigurációs Azonosítóval rendelkező lekérési ügyfél beállítása](PullClientConfigNames.md)
* [DSC lekérési kiszolgáló beállítása](pullServer.md)
