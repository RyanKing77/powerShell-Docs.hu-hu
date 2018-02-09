---
ms.date: 2017-10-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A Windows PowerShell korábbi verzióiban a helyi Configuration Manager konfigurálása"
ms.openlocfilehash: 65eb2a8d5a99e977cf2f3dbd726240ec2d5a6142
ms.sourcegitcommit: 755d7bc0740573d73613cedcf79981ca3dc81c5e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/09/2018
---
# <a name="configuring-the-local-configuration-manager-in-previous-versions-of-windows-powershell"></a>A Windows PowerShell korábbi verzióiban a helyi Configuration Manager konfigurálása

>Vonatkozik: A Windows PowerShell 4.0

**A Windows PowerShell 5.0-s vagy újabb kapcsolatos információkért lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md).**

Helyi Configuration Manager a Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) motor.
Az összes célcsomópontokat fut, és hívja meg a konfigurációs erőforrások kerüljenek a DSC konfigurációs parancsfájl felelős.
Ez a témakör a tulajdonságok a helyi Configuration Manager, és ismerteti, hogyan módosíthatja a helyi Configuration Manager beállításait a célcsomóponton.

## <a name="local-configuration-manager-properties"></a>Helyi Configuration Manager-tulajdonságok

Az alábbi listában találja a helyi Configuration Manager – tulajdonságok beállítása vagy beolvasása.

- **AllowModuleOverwrite**: felülírhatják-e a konfigurálási szolgáltatástól letöltött új konfigurációk a célcsomóponton lévő régi felülírják. A lehetséges értékek: True és False.
- **CertificateID**: konfigurációban átadott hitelesítő adatok biztonságossá tételére használt tanúsítvány ujjlenyomata. További információ: [biztonságossá tétele a Windows PowerShell célállapot-konfiguráció-felhasználó hitelesítő adatait?](http://blogs.msdn.com/b/powershell/archive/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration.aspx).
- **ConfigurationID**: azt jelzi, egy GUID Azonosítót, amely egy adott konfigurációs fájl beolvasása lekéréses szolgáltatás használható. A GUID biztosítja, hogy elérhetők-e a megfelelő konfigurációs fájlt.
- **ConfigurationMode**: határozza meg, hogy a helyi Configuration Manager ténylegesen a beállítások alkalmazása a célcsomópontokat. Ez a következő értékeket veheti:
  - **ApplyOnly**: Ezzel a lehetőséggel DSC konfigurációjának alkalmazására szolgál, és nincs semmi hatása további, kivéve, ha az új konfiguráció észlel, Ön egy új konfiguráció küldése közvetlenül a célcsomópont, vagy ha csatlakozik egy lekéréses szolgáltatás és a DSC-ből ellenőrzi a lekérési szolgáltatással felderíti az új konfigurációt. Ha a cél a csomópont-konfiguráció drifts, semmilyen művelet nem lesz végrehajtva.
  - **ApplyAndMonitor**: Ezzel a beállítással (Ez az alapértelmezett), DSC minden új konfigurációt vonatkozik, hogy közvetlenül a célcsomópont küldött Ön által vagy észleltek egy lekéréses szolgáltatás. Ezt követően Ha a cél-csomópont konfigurációjának a drifts a konfigurációs fájlból, DSC jelentések a naplókban az eltérés. A DSC-naplózás kapcsolatban bővebben lásd: [eseménynaplók használata a célállapot-konfiguráció hibáinak diagnosztizálásához](http://blogs.msdn.com/b/powershell/archive/2014/01/03/using-event-logs-to-diagnose-errors-in-desired-state-configuration.aspx).
  - **ApplyAndAutoCorrect**: Ezzel a lehetőséggel DSC attól függetlenül is érvényes minden új konfigurációt, közvetlenül a célcsomópont küldött Ön által vagy észleltek egy lekéréses szolgáltatás. Azt követően Ha a cél-csomópont konfigurációjának a drifts a konfigurációs fájlból, DSC jelent a naplókban az eltérés, és megpróbálja módosítani a cél csomópont-konfigurációt vonandó felelnek meg a konfigurációs fájl.
- **ConfigurationModeFrequencyMins**: azt a gyakoriságot, amellyel a DSC szolgáltatás Háttéralkalmazása kísérletet tesz az aktuális konfiguráció célcsomóponton végrehajtásához (percben). Az alapértelmezett érték 15. Ez az érték beállítható RefreshMode együtt. Amikor LEKÉRÉSES RefreshMode van beállítva, a célcsomópont kapcsolatba lép a konfigurációs szolgáltatás RefreshFrequencyMins által beállított időközönként, és tölti le a jelenlegi konfiguráció. RefreshMode értékétől függetlenül ConfigurationModeFrequencyMins, által beállított időközönként a konzisztencia-motor alkalmazza a legfrissebb konfigurációt, amely a célcsomópont le vannak töltve. Egy egész számot kell megadni RefreshFrequencyMins ConfigurationModeFrequencyMins többszöröse.
- **Hitelesítő adatok**: azt jelzi, hitelesítő adatokat (például a Get-Credential) eléréséhez szükséges távoli erőforrások, például a konfigurációs szolgáltatással való kapcsolatfelvételre.
- **DownloadManagerCustomData**: a letöltéskezelő jellemző egyéni adatokat tartalmazó tömb jelöli.
- **DownloadManagerName**: a konfigurációs és a modul letöltéskezelő nevét jelöli.
- **RebootNodeIfNeeded**: bizonyos konfigurációs módosítások egy célcsomóponttal előfordulhat, hogy újra kell indítani a módosítások alkalmazandó. A értékű **igaz**, ez a tulajdonság a csomópont újraindul, amint a konfiguráció lett teljesen vonatkozik, további figyelmeztetés nélkül. Ha **hamis** (az alapértelmezett érték), a konfiguráció befejeződik, de a csomópont újra kell indítani, manuálisan a módosítások életbe léptetéséhez.
- **RefreshFrequencyMins**: használható, ha meg van adva egy lekéréses szolgáltatást. Azt a gyakoriságot (percben) a helyi Configuration Manager kapcsolatba lép egy lekéréses szolgáltatást, hogy töltse le a jelenlegi konfiguráció. Ez az érték beállítható ConfigurationModeFrequencyMins együtt. Amikor LEKÉRÉSES RefreshMode van beállítva, a célcsomópont kapcsolatba lép a lekéréses szolgáltatás RefreshFrequencyMins által beállított időközönként, és tölti le a jelenlegi konfiguráció. ConfigurationModeFrequencyMins által beállított időközönként a konzisztencia-motor majd alkalmazza a legfrissebb konfigurációt, amely a célcsomópont le vannak töltve. Ha RefreshFrequencyMins értéke nem egész számú többszöröse az ConfigurationModeFrequencyMins, a rendszer kerekíti. Az alapértelmezett érték 30.
- **RefreshMode**: a lehetséges értékek: **leküldéses** (alapértelmezett) és **lekéréses**. A "leküldéses" konfigurációban el kell helyezni a konfigurációs fájl minden egyes célcsomóponttal bármelyik ügyfélszámítógép. A "pull" módban be kell állítania egy lekéréses szolgáltatás a helyi Configuration Manager kapcsolódni, és a konfigurációs fájlokat.

### <a name="example-of-updating-local-configuration-manager-settings"></a>Példa helyi Configuration Manager-beállításainak frissítése folyamatban

A helyi Configuration Manager egy célcsomóponttal beállításainak frissítéséhez többek között a **LocalConfigurationManager** blokkolja egy konfigurációs parancsfájl a csomópont blokkon belül, a következő példában látható módon.

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

A parancsprogram futtatása az előző példában szereplő állít elő, a MOF-fájlt ad meg, és a kívánt beállításokat tárolja.
A beállítások alkalmazásához, használhatja a **Set-DscLocalConfigurationManager** parancsmag, a következő példában látható módon.

```powershell
Set-DscLocalConfigurationManager -Path "c:\users\public\dsc"
```

> **Megjegyzés:**: az a **elérési** paraméter, meg kell adnia ugyanazt az elérési utat, amely a megadott a **OutputPath** paraméter az előző példában szereplő konfigurációs meghívásakor.

A helyi Configuration Manager jelenlegi beállítások megtekintéséhez használja a **Get-DscLocalConfigurationManager** parancsmag.
Ha ezt a parancsmagot, paraméter nélküli indít, alapértelmezés szerint azt megkapják a helyi Configuration Manager beállításokat a csomópont, amelyen futtatja azt.
Adja meg egy másik csomópontra, a **CimSession** ezzel a parancsmaggal paraméter.
