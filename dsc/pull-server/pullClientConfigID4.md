---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációs azonosítók használata a PowerShell 4.0-s lekérési ügyfél beállítása
ms.openlocfilehash: 9adc767e91ff19d373c122a0d493e7b8703d5476
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404396"
---
# <a name="set-up-a-pull-client-using-configuration-ids-in-powershell-40"></a>Konfigurációs azonosítók használata a PowerShell 4.0-s lekérési ügyfél beállítása

>Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

> [!IMPORTANT]
> A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak. Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).

Lekérési ügyfél beállítása előtt be kell állítania egy lekéréses kiszolgálót. Bár nem kötelező ebben a sorrendben, segít a hibák elhárításában, és így gondoskodik róla, hogy a regisztráció sikeres volt-e. Állítson be egy lekéréses kiszolgálót, használhatja a következő útmutatókat:

- [DSC SMB-lekérési kiszolgáló beállítása](pullServerSmb.md)
- [A DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md)

Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát. Az alábbi szakaszok bemutatják, hogyan lekérési ügyfél beállítása egy SMB-megosztáson, vagy a HTTP-DSC lekéréses kiszolgálón. Amikor a csomópont LCM frissíti, a konfigurált helyre, töltse le a hozzárendelt konfigurációkat, felveszi Önnel. Ha minden szükséges erőforrás nem létezik a csomóponton, azt automatikusan letöltheti őket a beállított helyről. Ha a csomópont konfigurálva van egy [jelentéskészítő kiszolgáló](reportServer.md), majd a művelet állapotát jelzi.

## <a name="configure-the-pull-client-lcm"></a>Lekérési ügyfél LCM konfigurálása

Az alábbi példák bármelyikét végrehajtása hoz létre egy új nevű kimeneti mappát **PullClientConfigID** , és ott helyezi metaconfiguration MOF-fájlt. Ebben az esetben a metaconfiguration MOF-fájl neve lesz `localhost.meta.mof`.

A alkalmazni a konfigurációt, hívja meg a **Set-DscLocalConfigurationManager** parancsmag, az a **elérési út** állítsa be a metaconfiguration MOF-fájl helyét. Például:

```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path .\PullClientConfigId –Verbose.
```

## <a name="configuration-id"></a>Konfiguráció azonosítója

Set alábbi példák a **ConfigurationID** , az LCM tulajdonságát egy **Guid** , amely korábban létrehozott erre a célra. A **ConfigurationID** van, használja az LCM Konfigurálása a megfelelő konfiguráció keresése a lekérési kiszolgálón. A lekérési kiszolgálón a konfigurációs MOF-fájl neve legyen `ConfigurationID.mof`, ahol *ConfigurationID* értéke a **ConfigurationID** a célcsomópont LCM tulajdonságát. További információkért lásd: [konfigurációk közzététele egy lekéréses kiszolgálóra (v4 vagy v5)](publishConfigs.md).

Létrehozhat egy véletlenszerű **Guid** az alábbi példa használatával.

```powershell
[System.Guid]::NewGuid()
```

## <a name="set-up-a-pull-client-to-download-configurations"></a>Lekérési ügyfél beállítása a konfiguráció letöltése

Minden egyes ügyfélnek meg kell adni a **lekéréses** módban, és a pull-kiszolgáló URL-címét a konfigurációja tárolására. Ehhez az szükséges, akkor a helyi Configuration Manager (LCM) konfigurálása a szükséges információkat. Az LCM konfigurálása, a létrehozott konfigurációs, különleges típusú egy **LocalConfigurationManager** letiltása. Az LCM konfigurálása kapcsolatos további információkért lásd: [a Local Configuration Manager](../managing-nodes/metaConfig4.md).

## <a name="http-dsc-pull-server"></a>HTTP-DSC lekéréses kiszolgálón

Ha a lekéréses kiszolgálón webszolgáltatásként, amely be van állítva, akkor be a **DownloadManagerName** való **WebDownloadManager**. A **WebDownloadManager** meg kell adnia egy **ServerUrl** , a **DownloadManagerCustomData** kulcsot. Megadhat egy értéket is **AllowUnsecureConnection**, amint az az alábbi példában. A következő szkriptet az LCM konfigurálja a pull-konfigurációk "PullServer" nevű kiszolgálóról.

```powershell
Configuration PullClientConfigId
{
    LocalConfigurationManager
    {
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "WebDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30;
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "http://PullServer:8080/PSDSCPullServer/PSDSCPullServer.svc"; AllowUnsecureConnection = “TRUE”}
    }
}
PullClientConfigId -Output "."
```

## <a name="smb-share"></a>SMB-megosztás

Ha a lekérési kiszolgálón be van állítva, az SMB-fájlmegosztás, nem pedig egy webszolgáltatás, állít be a **DownloadManagerName** való **DscFileDownloadManager** helyett a **WebDownLoadManager**. A **DscFileDownloadManager** meg kell adnia egy **SourcePath** tulajdonságot a **DownloadManagerCustomData**. A következő szkriptet a kiszolgáló neve "CONTOSO-kiszolgáló" a "SmbDscShare" nevű SMB-megosztáson konfigurációk lekérni az LCM konfigurálása.

```powershell
Configuration PullClientConfigId
{
    LocalConfigurationManager
    {
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "DscFileDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30;
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "\\CONTOSO-SERVER\SmbDscShare"}
    }
}
PullClientConfigId -Output "."
```

## <a name="next-steps"></a>Következő lépések

A lekérési ügyfél beállítása után a következő útmutatók használatával hajtsa végre a következő lépéseket:

- [Konfigurációk közzétételére egy lekéréses kiszolgálót (v4 vagy v5)](publishConfigs.md)
- [Csomag és a egy lekéréses kiszolgálót (v4) erőforrás feltöltése](package-upload-resources.md)

## <a name="see-also"></a>Lásd még:

- [DSC lekérési kiszolgáló beállítása](pullServer.md)
- [A DSC SMB-lekérési kiszolgálójának beállítása](pullServerSMB.md)
