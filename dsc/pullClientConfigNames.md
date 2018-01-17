---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Konfigurációs nevek használatával lekéréses ügyfél beállítása"
ms.openlocfilehash: 11de53fc349ce0ebacf0d4855d82fa8a22d55c99
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="setting-up-a-pull-client-using-configuration-names"></a>Konfigurációs nevek használatával lekéréses ügyfél beállítása

> Vonatkozik: A Windows PowerShell 5.0

Minden egyes célcsomóponttal lekéréses módban a rendszergazda és az URL-címet kap, ahol lépjen kapcsolatba a lekérési kiszolgálójával konfigurációt beolvasandó ki.
Ehhez az szükséges, hogy a helyi Configuration Manager (LCM) konfigurálnia a szükséges adatokat.
A LCM konfigurálásához hoz létre egy speciális konfigurációs attribútummal. az **DSCLocalConfigurationManager** attribútum.
A LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md).

> **Megjegyzés:**: Ez a témakör PowerShell 5.0 vonatkozik.
A PowerShell 4.0 lekéréses ügyfél beállításával kapcsolatos információkért lásd: [konfigurációs azonosítójával PowerShell 4.0 lekéréses ügyfél beállítása](pullClientConfigID4.md)

Az alábbi parancsfájl a LCM konfigurálja az lekéréses konfigurációk "CONTOSO-PullSrv" nevű kiszolgálóról:

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

A parancsfájl a **ConfigurationRepositoryWeb** blokk határozza meg a lekérési kiszolgálójával.
A **ServerURL** tulajdonság határozza meg a végpont a lekérési kiszolgálón.

A **RegistrationKey** tulajdonsága egy megosztott kulcsot lekéréses kiszolgáló összes ügyfél-csomópontok és az adott lekéréses kiszolgáló között.
Ugyanazt az értéket a fájl a lekérési kiszolgálón tárolja.

A **ConfigurationNames** tulajdonsága olyan tömb, amely meghatározza a konfigurációkat, az ügyfél-csomópontnak szánt nevét.
A lekérési kiszolgálón a konfigurációs MOF-fájlja nevet kell kapniuk az ügyfél-csomópontnak *ConfigurationNames*.mof, ahol *ConfigurationNames* értéke megegyezik a **ConfigurationNames**  a metakonfigurációját az tulajdonsága.

>**Megjegyzés:** Ha egynél több értéket adja meg a **ConfigurationNames**, meg kell adni **PartialConfiguration** blokkolja a konfigurációt.
Részleges konfigurációkkal kapcsolatos információkért lásd: [PowerShell célállapot-konfiguráció részleges konfigurációk](partialConfigs.md).

A parancsfájl futtatása után a rendszer létrehoz egy új kimeneti mappát **PullClientConfigNames** , és nincs helyezi metakonfigurációját MOF-fájlt.
Ebben az esetben a metakonfigurációját MOF-fájl neve lehet `localhost.meta.mof`.

A konfiguráció alkalmazásához, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési** beállítása a metakonfigurációját MOF-fájl helyét.

```powershell
Set-DSCLocalConfigurationManager localhost –Path .\PullClientConfigNames –Verbose.
```

> **Megjegyzés:**: regisztrációs kulcsokat csak lekéréses webkiszolgálók működik.
Továbbra is használnia kell **ConfigurationID** az SMB-lekéréses kiszolgálóval.
A lekérési kiszolgálójával használatával konfigurálásával kapcsolatos információkat **ConfigurationID**, lásd: [konfigurációs azonosítójával lekéréses ügyfél beállítása](PullClientConfigNames.md)

## <a name="resource-and-report-servers"></a>Erőforrás-és a jelentés

Ha csak adja meg a **ConfigurationRepositoryWeb** vagy **ConfigurationRepositoryShare** (ahogy az előző példában) LCM konfigurációs letiltása, a lekéréses ügyfél erőforrásokat fogja lekérni a megadott kiszolgálón, de nem küld jelentéseket rá.
Konfigurációk, erőforrások és jelentéskészítési olyan egyetlen lekéréses kiszolgálót is használhat, de létre kell hoznia egy **ReportRepositoryWeb** blokk jelentéskészítés beállítása.
A következő példa bemutatja egy metakonfigurációját állítja be az ügyfél lekéréses konfigurációk és az erőforrások és a jelentés adatainak, lekéréses egyetlen kiszolgálóra történő küldés.

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
        }
    }
}
PullClientConfigNames
```

Az erőforrások és a jelentéskészítő különböző lekéréses kiszolgálók is megadható.
Adjon meg egy erőforrás-kiszolgáló, használhatja a **ResourceRepositoryWeb** (a lekéréses webkiszolgálók) vagy egy **ResourceRepositoryShare** blokk (az SMB-lekérési kiszolgálón).
Adja meg a jelentéskészítő kiszolgálón, akkor használja a **ReportRepositoryWeb** blokkot.
A jelentéskészítő kiszolgáló nem lehet egy SMB-kiszolgálón.
A következő metakonfigurációját beállítja a konfigurációk a beolvasandó lekéréses ügyfél **CONTOSO-PullSrv** és erőforrását **CONTOSO-ResourceSrv**, és a jelentések küldése  **CONTOSO-ReportSrv**:

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

        ResourceRepositoryWeb CONTOSO-ResourceSrv
        {
            ServerURL = 'https://CONTOSO-ResourceSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '30ef9bd8-9acf-4e01-8374-4dc35710fc90'
        }

        ReportServerWeb CONTOSO-ReportSrv
        {
            ServerURL = 'https://CONTOSO-ReportSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '6b392c6a-818c-4b24-bf38-47124f1e2f14'
        }
    }
}
PullClientConfigNames
```

## <a name="see-also"></a>Lásd még:

* [Konfigurációs azonosítójú lekéréses ügyfél beállítása](PullClientConfigNames.md)
* [A DSC lekérési webkiszolgáló beállítása](pullServer.md)

