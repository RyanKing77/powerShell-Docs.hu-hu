---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A Local Configuration Manager konfigurálása a Windows PowerShell korábbi verziói
ms.openlocfilehash: 31ba2ecdaa5a2ff7fcfddb1791c4d00343f4b5d5
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404247"
---
# <a name="configuring-the-local-configuration-manager-in-previous-versions-of-windows-powershell"></a>A Local Configuration Manager konfigurálása a Windows PowerShell korábbi verziói

>Érvényes: Windows PowerShell 4.0

**Windows PowerShell 5.0-s vagy újabb kapcsolatos információkért lásd: [a Local Configuration Manager](metaConfig.md).**

Helyi Configuration Manager egy, a Windows PowerShell Desired State Configuration (DSC) motor.
Az összes cél csomóponton fut, és ez felelős a konfigurációs erőforrásokat, amelyek szerepelnek a DSC-konfigurációs parancsprogram hívása.
Ez a témakör a helyi Configuration Manager tulajdonságai szerepelnek, és ismerteti, hogyan módosíthatja a Local Configuration Manager-beállítások egy cél-csomóponton.

## <a name="local-configuration-manager-properties"></a>Helyi Configuration Manager – tulajdonságok

Az alábbi listában a helyi Configuration Manager – tulajdonságok, amelyeket beállítása és lekérése.

- **AllowModuleOverwrite**: A vezérlők felülírja a régieket célcsomóponton engedélyezett e letöltött új konfigurációk a konfigurálási szolgáltatástól. A lehetséges értékek: True és FALSE (hamis).
- **CertificateID**: A konfigurációban az átadott hitelesítő adatok védelmére szolgáló tanúsítvány ujjlenyomatát. További információ: [hitelesítő adatai a Windows PowerShell Desired State Configuration engedélyezzen?](https://blogs.msdn.microsoft.com/powershell/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration/).
- **ConfigurationID**: Azt jelzi, hogy egy GUID Azonosítót, amely egy adott konfigurációs fájl beolvasása egy lekéréses szolgáltatás segítségével. A GUID biztosítja, hogy elérhető-e a megfelelő konfigurációs fájlt.
- **ConfigurationMode**: Itt adhatja meg, hogyan a Local Configuration Manager ténylegesen alkalmazza a konfigurációt, a célcsomópontokat. Is igénybe vehet a következő értékeket:
  - **ApplyOnly**: Ezzel a beállítással a DSC konfigurációjának alkalmazására szolgál, és nem módosítja a további, kivéve, ha egy új konfiguráció észlel, vagy Ön egy új konfiguráció küldése közvetlenül a cél csomópont, vagy ha kapcsolódik egy lekérési szolgáltatást és a DSC felderíti az új konfiguráció során ellenőrzi a lekérési szolgáltatással. Ha a cél csomópont-konfiguráció drifts, nincs művelet nem lesz végrehajtva.
  - **ApplyAndMonitor**: Ezzel a lehetőséggel (Ez az alapértelmezett beállítás) DSC vonatkozik minden új konfigurációt a célcsomópont közvetlenül az Ön által küldött, vagy egy lekéréses szolgáltatás a talált. Azt követően Ha a cél-csomópont konfigurációjának drifts a konfigurációs fájlból, DSC jelentések naplókban eltérést. DSC naplózásával kapcsolatos további információkért lásd: [eseménynaplók használata a Desired State Configuration hibáinak diagnosztizálása](http://blogs.msdn.com/b/powershell/archive/2014/01/03/using-event-logs-to-diagnose-errors-in-desired-state-configuration.aspx).
  - **ApplyAndAutoCorrect**: Ezzel a beállítással DSC minden új konfigurációt, attól függetlenül érvényes, közvetlenül a célcsomópont küldött Ön vagy egy lekéréses szolgáltatás a talált. Ezt követően a célcsomópont konfigurációjának drifts a konfigurációs fájlból, ha DSC-jelentések a naplókban az eltérés, és ezután megpróbálja módosítani ahhoz, hogy megfelelnek-e a konfigurációs fájlt a cél csomópont-konfiguráció.
- **ConfigurationModeFrequencyMins**: Azt a gyakoriságot (percben), amellyel DSC háttéralkalmazása próbál megvalósítása a jelenlegi konfiguráció célcsomóponton. Az alapértelmezett érték 15. Ez az érték beállítható a RefreshMode együtt. A RefreshMode LEKÉRÉSES értékre van állítva, ha a célcsomópont kapcsolatba lép a konfigurációs szolgáltatás RefreshFrequencyMins által meghatározott időközönként, és letölti az aktuális konfigurációt. A RefreshMode értékétől függetlenül ConfigurationModeFrequencyMins, által meghatározott időközönként a konzisztencia-motor alkalmazza a legújabb konfigurációt, a cél csomópontra letöltött. Egy egész számot kell megadni RefreshFrequencyMins ConfigurationModeFrequencyMins többszöröse.
- **Hitelesítő adatok**: Hitelesítő adatok (például a Get-Credential) azt jelzi, hogy távoli erőforrások eléréséhez, mint például a konfigurációs szolgáltatáshoz való szükséges.
- **DownloadManagerCustomData**: Egy tömb, amely tartalmazza a letöltéskezelő jellemző egyéni adatokat jelöli.
- **DownloadManagerName**: Azt jelzi, hogy a konfiguráció és a letöltéskezelő modul nevét.
- **RebootNodeIfNeeded**: Bizonyos konfigurációs módosítások egy célcsomóponttal szükség lehet, hogy újra kell indítani a módosítások a alkalmazni. A következő értékkel **igaz**, ez a tulajdonság a csomópont újraindul, amint a konfigurálás teljesen vonatkozik, további figyelmeztetés nélkül. Ha **hamis** (az alapértelmezett érték), a konfiguráció befejeződik, de a csomópont kell manuálisan újra kell indítani a módosítások érvénybe léptetéséhez.
- **RefreshFrequencyMins**: Ha meg van adva egy lekérési szolgáltatást használja. Azt a gyakoriságot (percben), a Local Configuration Manager kapcsolatba lép egy lekérési szolgáltatást a jelenlegi konfiguráció letöltéséhez. Ez az érték beállítható ConfigurationModeFrequencyMins együtt. A RefreshMode LEKÉRÉSES értékre van állítva, ha a célcsomópont kapcsolatba lép a lekéréses szolgáltatás RefreshFrequencyMins által meghatározott időközönként, és letölti az aktuális konfigurációt. A konzisztencia-motor ConfigurationModeFrequencyMins által meghatározott időközönként majd alkalmazza a legfrissebb konfigurációt, a cél csomópontra letöltött. Ha nincs beállítva egész RefreshFrequencyMins többszöröse ConfigurationModeFrequencyMins, a rendszer kerekíti. Az alapértelmezett érték 30.
- **A RefreshMode**: Lehetséges értékek a következők **leküldéses** (alapértelmezett), és **lekéréses**. A "leküldéses" konfigurációban be kell jelölnie egy konfigurációs fájlt a cél csomópontokon bármelyik ügyfélszámítógép használatával. A "PULL parancs" módban be kell állítania egy lekéréses szolgáltatás a helyi Configuration Manager kapcsolatba, és a konfigurációs fájlok eléréséhez.

### <a name="example-of-updating-local-configuration-manager-settings"></a>Példa a Local Configuration Manager-beállítások frissítése

A helyi Configuration Manager-beállítások a cél csomópont együtt frissítheti egy **LocalConfigurationManager** letiltása a konfigurációs parancsfájl, a csomópont blokkon belül, az alábbi példában látható módon.

```powershell
Configuration ExampleConfig
{
    Node “Server001”
    {
        LocalConfigurationManager
        {
            ConfigurationID = "646e48cb-3082-4a12-9fd9-f71b9a562d4e"
            ConfigurationModeFrequencyMins = 45
            ConfigurationMode = "ApplyAndAutocorrect"
            RefreshMode = "Pull"
            RefreshFrequencyMins = 90
            DownloadManagerName = "WebDownloadManager"
            DownloadManagerCustomData = (@{ServerUrl="https://$PullService/psdscpullserver.svc"})
            CertificateID = "71AA68562316FE3F73536F1096B85D66289ED60E"
            Credential = $cred
            RebootNodeIfNeeded = $true
            AllowModuleOverwrite = $false
        }
# One or more resource blocks can be added here
    }
}

# The following line invokes the configuration and creates a file called Server001.meta.mof at the specified path
ExampleConfig -OutputPath "c:\users\public\dsc"
```

A szkript futtatása az előző példában állít elő a MOF-fájl, amely megadja, és tárolja a kívánt beállításokat.
A alkalmazni a beállításokat, használhatja a **Set-DscLocalConfigurationManager** parancsmag, az alábbi példában látható módon.

```powershell
Set-DscLocalConfigurationManager -Path "c:\users\public\dsc"
```

> **Megjegyzés:**: Az a **elérési** paramétert meg kell adnia a megadott elérési útját a **OutputPath** paraméter a konfigurációt az előző példában meghívásakor.

Az aktuális helyi Configuration Manager-beállítások megtekintéséhez használja a **Get-DscLocalConfigurationManager** parancsmagot.
Ha hívhat meg ezt a parancsmagot paraméterek nélkül, alapértelmezés szerint, megjelenik a csomópont, amelyen futtatja, a Local Configuration Manager beállításait.
Adjon meg egy másik csomópontra, használja a **CimSession** paraméter ezzel a parancsmaggal.
