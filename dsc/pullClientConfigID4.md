---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A PowerShell 4.0 konfigurációs azonosítójával lekéréses ügyfél beállítása"
ms.openlocfilehash: 19328018d276cddd0877869b0ec69c14c51e4b85
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="setting-up-a-pull-client-using-configuration-id-in-powershell-40"></a>A PowerShell 4.0 konfigurációs azonosítójával lekéréses ügyfél beállítása

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

Minden egyes célcsomóponttal lekéréses módban a rendszergazda és az URL-címet kap, ahol lépjen kapcsolatba a lekérési kiszolgálójával konfigurációt beolvasandó ki. Ehhez az szükséges, hogy a helyi Configuration Manager (LCM) konfigurálnia a szükséges adatokat. A LCM konfigurálásához hoz létre egy speciális konfigurációs "metakonfigurációját" néven ismert. A LCM konfigurálásával kapcsolatos további információkért lásd: [Windows PowerShell 4.0 kívánt állapot konfigurációs helyi Configuration Manager](metaConfig4.md)

Az alábbi parancsfájl a LCM konfigurálja az lekéréses konfigurációk "PullServer" nevű kiszolgálóról:

```powershell
Configuration SimpleMetaConfigurationForPull 
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
SimpleMetaConfigurationForPull -Output "."
```

A parancsfájl **DownloadManagerCustomData** cserél az URL-címet a lekérési kiszolgálójával és (ebben a példában), lehetővé teszi egy nem biztonságos kapcsolatot. 

Ez a parancsfájl futtatása után az új mappát hoz létre kimeneti nevű **SimpleMetaConfigurationForPull** , és nincs helyezi metakonfigurációját MOF-fájlt.

A konfiguráció segítségével **Set-DscLocalConfigurationManager** a paraméterekkel **számítógépnév** (használja a "localhost") és **elérési** (helyének elérési útvonalát a cél csomópont localhost.meta.mof fájl). Például: 
```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path . –Verbose.
```

## <a name="configuration-id"></a>Konfiguráció azonosítója
A parancsfájl beállítása a **ConfigurationID** korábban erre a célra létrehozott egyedi azonosítóvá LCM tulajdonságának (GUID segítségével létrehozható a **New-Guid** parancsmag). A **ConfigurationID** van a LCM használja a megfelelő konfigurációja a lekérési kiszolgálón található. A konfigurációs MOF-fájlt a lekérési kiszolgálón névvel kell ellátni `ConfigurationID.mof`, ahol *ConfigurationID* értéke a **ConfigurationID** a célcsomópont LCM tulajdonsága.

## <a name="pulling-from-an-smb-server"></a>Húzza az SMB-kiszolgálón

Ha a lekérési kiszolgálón be van állítva egy SMB-fájlmegosztás, nem pedig egy webszolgáltatás-bővítmény, megadhatja a **DscFileDownloadManager** helyett a **WebDownLoadManager**.
A **DscFileDownloadManager** tart egy **SourcePath** tulajdonság helyett **ServerUrl**. A következő parancsfájl való lekérésére konfigurációi az SMB-megosztáson "SmbDscShare" nevű "CONTOSO-kiszolgáló" nevű kiszolgálóra LCM konfigurálja:

```powershell
Configuration SimpleMetaConfigurationForPull 
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
SimpleMetaConfigurationForPull -Output "."
```

## <a name="see-also"></a>Lásd még:

- [A DSC lekérési webkiszolgáló beállítása](pullServer.md)
- [Egy DSC SMB lekérési kiszolgálójával beállítása](pullServerSMB.md)

