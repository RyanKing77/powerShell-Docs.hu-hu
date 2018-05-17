---
ms.date: 10/11/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A helyi Configuration Manager konfigurálása
ms.openlocfilehash: 924abe12aa865989e83c975b599b3b65ddd45655
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="configuring-the-local-configuration-manager"></a>A helyi Configuration Manager konfigurálása

> Vonatkozik: A Windows PowerShell 5.0

A helyi Configuration Manager (LCM) Ez a motor a kívánt állapot konfigurációs szolgáltatása (DSC).
A LCM minden cél csomóponton fut, és elemzése és a csomópont küldött konfigurációk életbe.
Feladata még számos más DSC, beleértve a következő aspektusait.

- Annak meghatározása, frissítési mód (lekérés és küldés).
- Milyen gyakran egy csomópont kéri le, és konfigurációk ír elő megadása.
- A csomópont társítása lekéréses szolgáltatás.
- Adja meg a részleges konfigurációkat.

Egy különleges típusú konfiguráció segítségével adhatja meg, ezek közül a viselkedésmódok mindegyikének LCM konfigurálhatja.
Az alábbi szakaszok azt ismertetik, hogyan konfigurálhatja a LCM.

A Windows PowerShell 5.0 rendszerben jelent meg új beállítások, a helyi Configuration Manager kezelése.
A Windows PowerShell 4.0 a LCM konfigurálásával kapcsolatos további információkért lásd: [a helyi Configuration Manager konfigurálása a korábbi verziók a Windows PowerShell](metaconfig4.md).

## <a name="writing-and-enacting-an-lcm-configuration"></a>Írást, és életbe LCM konfigurálása során

A LCM konfigurálásához létrehozása és futtatása egy különleges típusú LCM beállításait alkalmazó konfiguráció.
Egy LCM konfiguráció megadásához használja a DscLocalConfigurationManager attribútum.
Az alábbiakban látható egy egyszerű leküldéses módba állítja a LCM konfigurációt.

```powershell
[DSCLocalConfigurationManager()]
configuration LCMConfig
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Push'
        }
    }
}
```

Beállítások alkalmazása az LCM folyamat hasonlít a DSC-konfiguráció alkalmazása.
Létrehoz egy LCM konfigurációs, fordítsa MOF-fájlt, és alkalmazza azt a csomópontot.
Ellentétben a DSC-konfigurációk, akkor nem kihirdeti LCM konfigurálása során meghívásával a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag.
Ehelyett meghívja a [Set-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx), hogy megadja a MOF-paraméterként LCM konfigurációjának elérési útvonala.
Miután kihirdeti LCM konfigurációját, a LCM tulajdonságainak meghívásával megtekintheti a [Get-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx) parancsmag.

Egy LCM konfiguráció csak korlátozott számú erőforrások a blokkok is tartalmazhat.
Az előző példában a nevű csak erőforrás van **beállítások**.
A rendelkezésre álló erőforrások a következők:

* **ConfigurationRepositoryWeb**: Adja meg egy HTTP-lekéréses szolgáltatás konfigurációjából.
* **ConfigurationRepositoryShare**: SMB-megosztáson konfigurációk határozza meg.
* **ResourceRepositoryWeb**: Adja meg a modulok lekéréses HTTP szolgáltatásnak.
* **ResourceRepositoryShare**: Adja meg a modulok SMB-megosztáson.
* **ReportServerWeb**: Adja meg egy HTTP-lekéréses szolgáltatás, ahová a rendszer elküldi a jelentéseket.
* **PartialConfiguration**: részleges konfigurációk engedélyezése adatokat biztosít.

## <a name="basic-settings"></a>Alapbeállítások

Eltérő megadva lekéréses szolgáltatás végpontok/elérési utakat és a részleges konfigurációk, az összes a LCM tulajdonságainak vannak konfigurálva a **beállítások** blokkot.
A következő tulajdonságok érhetők el egy **beállítások** blokkot.

|  Tulajdonság  |  Típus  |  Leírás   |
|----------- |------- |--------------- |
| ActionAfterReboot| karakterlánc| Itt adhatja meg, mi történik, a rendszer újraindítása után a beállítások alkalmazása során. A lehetséges értékek a következők __"ContinueConfiguration"__ és __"StopConfiguration"__. <ul><li> __ContinueConfiguration__: továbbra is a számítógép újraindítása után a jelenlegi konfiguráció alkalmazása. Ez az az alapértelmezett érték</li><li>__StopConfiguration__: állítsa le a számítógép újraindítása után az aktuális konfigurációt.</li></ul>|
| AllowModuleOverwrite| logikai érték| __$TRUE__ Ha lekéréses szolgáltatásból letöltött új konfigurációk engedélyezettek-e a célcsomóponton lévő régi felülírják. Ellenkező esetben $FALSE.|
| CertificateID| karakterlánc| A konfigurációban átadott hitelesítő biztosításához használt tanúsítvány ujjlenyomata. További információ: [szeretné védeni a Windows PowerShell célállapot-konfiguráció-felhasználó hitelesítő adatait a](http://blogs.msdn.com/b/powershell/archive/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration.aspx)?. <br> __Megjegyzés:__ ez kezeli automatikusan Azure Automation DSC lekérési szolgáltatás használatakor.|
| ConfigurationDownloadManagers| CimInstance]| Elavult. Használjon __ConfigurationRepositoryWeb__ és __ConfigurationRepositoryShare__ érdekében adja meg a konfigurációs lekéréses szolgáltatás végpontjait.|
| ConfigurationID| karakterlánc| A visszamenőleges kompatibilitás érdekében régebbi lekéréses szolgáltatás verziók. A GUID, amely azonosítja a konfigurációs fájl lekérni egy lekéréses szolgáltatásból. Ha a konfiguráció neve MOF ConfigurationID.mof neve a csomópont konfigurációk fogja lekérni lekéréses szolgáltatás.<br> __Megjegyzés:__ állítani ezt a tulajdonságot, ha regisztrálja a csomópont egy lekéréses szolgáltatással használatával __RegistrationKey__ nem működik. További információkért lásd: [konfigurációs nevű lekéréses ügyféltelepítéshez](pullClientConfigNames.md).|
| ConfigurationMode| karakterlánc | Itt adhatja meg, hogyan a LCM ténylegesen a beállítások alkalmazása a célcsomópontokat. A lehetséges értékek: __"ApplyOnly"__,__"ApplyAndMonitor"__, és __"ApplyAndAutoCorrect"__. <ul><li>__ApplyOnly__: DSC konfigurációjának alkalmazására szolgál, és nincs semmi hatása további, kivéve, ha az új konfiguráció célcsomóponton való vagy szolgáltatás új konfigurációt van lekért fejlesztőre. Az új konfiguráció első alkalmazása után DSC nem ellenőrzi a korábban konfigurált állapotból eltéréseket. Vegye figyelembe, hogy DSC megkísérli a konfiguráció alkalmazásához, amíg az sikeres előtt nem __ApplyOnly__ lép érvénybe. </li><li> __ApplyAndMonitor__: Ez az az alapértelmezett érték. A LCM alkalmazza minden új konfigurációt. Az új konfiguráció első alkalmazása után a célcsomóponton drifts kívánt állapotból, ha DSC jelent a naplókban az eltérés. Vegye figyelembe, hogy DSC megkísérli a konfiguráció alkalmazásához, amíg az sikeres előtt nem __ApplyAndMonitor__ lép érvénybe.</li><li>__ApplyAndAutoCorrect__: DSC alkalmazza minden új konfigurációt. Az új konfiguráció első alkalmazása után a célcsomópont drifts kívánt állapotból, ha DSC jelent a naplókban az eltérés, majd újra alkalmazza a jelenlegi konfiguráció.</li></ul>|
| ConfigurationModeFrequencyMins| UInt32| Milyen gyakran (percben), a jelenlegi konfiguráció be van jelölve, és alkalmazza. A rendszer figyelmen kívül hagyja ezt a tulajdonságot, ha a ConfigurationMode tulajdonsága ApplyOnly. Az alapértelmezett érték 15.|
| DebugMode| karakterlánc| A lehetséges értékek: __nincs__, __ForceModuleImport__, és __összes__. <ul><li>Beállítása __nincs__ gyorsítótárazott erőforrások használatára. Ez az alapértelmezett, és éles esetekben kell használni.</li><li>Beállítás __ForceModuleImport__, DSC erőforrás modul, töltse be újra, még akkor is, ha azokat korábban betöltötte és gyorsítótárazott LCM okoz. Ez teljesítményére hatással van a DSC-műveletek, minden modul használatára van töltve. Általában akkor használja ezt az értéket közben egy erőforrás-hibakeresés</li><li>Ebben a kiadásban __összes__ azonos __ForceModuleImport__</li></ul> |
| RebootNodeIfNeeded| logikai érték| Állítsa ezt a beállítást __$true__ automatikusan újraindítja a csomópont a konfigurációkat, amelyek a szükséges újraindítás alkalmazása után. Ellenkező esetben kell újraindítani a rendszert manuálisan minden beállítást, amelynek ezt a csomópontot. Az alapértelmezett érték __$false__. Ezt a beállítást, ha újraindítás feltétel végrehajtása nem DSC (például a Windows Installer) által használandó egyesítése együtt a [xPendingReboot](https://github.com/powershell/xpendingreboot) modul.|
| RefreshMode| karakterlánc| Itt adhatja meg, hogyan a LCM lekérdezi a konfigurációkat. A lehetséges értékek a következők __"Letiltva"__, __"Push"__, és __"Pull"__. <ul><li>__Letiltott__: a DSC-konfigurációk le van tiltva ezen a csomóponton.</li><li> __Leküldéses__: konfigurációk meghívásával kezdeményezett a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag. A konfiguráció alkalmazása azonnal megtörténik a csomópontra. Ez az alapértelmezett érték.</li><li>__Lekéréses:__ lekéréses szolgáltatás vagy az SMB elérési konfigurációk rendszeresen ellenőrzi a csomópont van konfigurálva. Ha ez a tulajdonság értéke __lekéréses__, egy HTTP (szolgáltatás) vagy SMB (megosztás) elérési utat adjon meg egy __ConfigurationRepositoryWeb__ vagy __ConfigurationRepositoryShare__ blokkot.</li></ul>|
| RefreshFrequencyMins| UInt32| Az időtartamot (percben), amelynél a LCM frissített konfigurációt beolvasandó lekéréses szolgáltatás ellenőrzi. A rendszer figyelmen kívül hagyja ezt az értéket, ha a LCM nem lekéréses módban van konfigurálva. Az alapértelmezett érték 30.|
| ReportManagers| CimInstance]| Elavult. Használjon __ReportServerWeb__ küldendő végpont meghatározása érdekében jelentésadatait lekéréses szolgáltatáshoz.|
| ResourceModuleManagers| CimInstance]| Elavult. Használjon __ResourceRepositoryWeb__ és __ResourceRepositoryShare__ lekéréses meghatározása érdekében szolgáltatás HTTP-végpontokról vagy SMB-elérési utak, illetve.|
| PartialConfigurations| CimInstance| Nincs megvalósítva. Ne használja.|
| StatusRetentionTimeInDays | UInt32| A LCM tartja az aktuális konfigurációs állapotát napok száma.|

## <a name="pull-service"></a>Lekéréses szolgáltatás

LCM konfigurációt is támogatja a következő típusú lekéréses Szolgáltatásvégpontok:

- **Konfigurációs kiszolgáló**: a DSC-konfigurációk tára. Adja meg a konfigurációs kiszolgálók használatával **ConfigurationRepositoryWeb** (a web-alapú kiszolgálók) és **ConfigurationRepositoryShare** (az SMB-alapú kiszolgálók) blokkokat.
- **Erőforrás-kiszolgáló**: a DSC-erőforrások, PowerShell-modulok csomagolt tára. Adja meg az erőforrás-kiszolgálók használatával **ResourceRepositoryWeb** (a web-alapú kiszolgálók) és **ResourceRepositoryShare** (az SMB-alapú kiszolgálók) blokkokat.
- **Jelentéskészítő kiszolgáló**: egy szolgáltatás, amely DSC jelentés adatokat küld. Adja meg a jelentéskészítő kiszolgáló használatával **ReportServerWeb** blokkolja. A jelentéskészítő kiszolgáló webszolgáltatás kell lennie.

További információ a lekéréses szolgáltatás:, [kívánt állapot konfigurációs lekéréses szolgáltatás](pullServer.md).

## <a name="configuration-server-blocks"></a>Konfigurációs kiszolgáló blokkok

A web-alapú konfigurációs kiszolgáló megadásához hozzon létre egy **ConfigurationRepositoryWeb** blokkot.
A **ConfigurationRepositoryWeb** következő tulajdonságait határozza meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|AllowUnsecureConnection|logikai érték|Beállítása **$TRUE** a kiszolgálóhoz hitelesítés anélkül, hogy a csomópont kapcsolatok lehetővé tételéhez. Beállítása **$FALSE** hitelesítést igényel.|
|CertificateID|karakterlánc|A kiszolgálón elvégzett hitelesítéshez használt tanúsítvány ujjlenyomata.|
|ConfigurationNames|String]|A cél csomópont lekérése konfigurációk nevei tömbjét. Segítségükkel lehetséges ugyanis csak akkor, ha a csomópont használatával a lekéréses szolgáltatással van regisztrálva a **RegistrationKey**. További információkért lásd: [konfigurációs nevű lekéréses ügyféltelepítéshez](pullClientConfigNames.md).|
|RegistrationKey|karakterlánc|A csomópont regisztrálja a lekéréses szolgáltatásban GUID. További információkért lásd: [konfigurációs nevű lekéréses ügyféltelepítéshez](pullClientConfigNames.md).|
|Kiszolgáló URL-címe|karakterlánc|A konfigurációs szolgáltatás URL-CÍMÉT.|

Egyszerűbbé teheti a ConfigurationRepositoryWeb értéke konfigurálása a helyszíni csomópontok nem érhető el – példa parancsfájl lásd [metaconfigurations DSC generálásához.](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

Az SMB-alapú konfigurációs kiszolgáló megadásához hozzon létre egy **ConfigurationRepositoryShare** blokkot.
A **ConfigurationRepositoryShare** következő tulajdonságait határozza meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|hitelesítő adatok|MSFT_Credential|Az SMB-megosztás felé történő hitelesítésre használt hitelesítő adat.|
|SourcePath|karakterlánc|Az SMB-megosztás elérési útja|

## <a name="resource-server-blocks"></a>Erőforrás-kiszolgáló blokkok

A webes erőforrás-kiszolgáló megadásához hozzon létre egy **ResourceRepositoryWeb** blokkot.
A **ResourceRepositoryWeb** következő tulajdonságait határozza meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|AllowUnsecureConnection|logikai érték|Beállítása **$TRUE** a kiszolgálóhoz hitelesítés anélkül, hogy a csomópont kapcsolatok lehetővé tételéhez. Beállítása **$FALSE** hitelesítést igényel.|
|CertificateID|karakterlánc|A kiszolgálón elvégzett hitelesítéshez használt tanúsítvány ujjlenyomata.|
|RegistrationKey|karakterlánc|A csomópont a lekéréses szolgáltatás azonosító egy GUID.|
|Kiszolgáló URL-címe|karakterlánc|A konfigurációs kiszolgáló URL-CÍMÉT.|

Egyszerűbbé teheti a ResourceRepositoryWeb értéke konfigurálása a helyszíni csomópontok nem érhető el – példa parancsfájl lásd [metaconfigurations DSC generálásához.](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

Az erőforrás SMB-alapú kiszolgáló megadásához hozzon létre egy **ResourceRepositoryShare** blokkot.
**ResourceRepositoryShare** következő tulajdonságait határozza meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|hitelesítő adatok|MSFT_Credential|Az SMB-megosztás felé történő hitelesítésre használt hitelesítő adat. Például egy sikeres hitelesítő adatokat, lásd: [egy DSC SMB lekérési kiszolgálójával beállítása](pullServerSMB.md)|
|SourcePath|karakterlánc|Az SMB-megosztás elérési útja|

## <a name="report-server-blocks"></a>Jelentéskészítő kiszolgáló blokkok

Adja meg a jelentéskészítő kiszolgálón, akkor hozzon létre egy **ReportServerWeb** blokkot.
A jelentéskészítő kiszolgálói szerepkör nem található kompatibilis SMB-alapú lekéréses szolgáltatás.
**ReportServerWeb** következő tulajdonságait határozza meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|AllowUnsecureConnection|logikai érték|Beállítása **$TRUE** a kiszolgálóhoz hitelesítés anélkül, hogy a csomópont kapcsolatok lehetővé tételéhez. Beállítása **$FALSE** hitelesítést igényel.|
|CertificateID|karakterlánc|A kiszolgálón elvégzett hitelesítéshez használt tanúsítvány ujjlenyomata.|
|RegistrationKey|karakterlánc|A csomópont a lekéréses szolgáltatás azonosító egy GUID.|
|Kiszolgáló URL-címe|karakterlánc|A konfigurációs kiszolgáló URL-CÍMÉT.|

Egyszerűbbé teheti a ReportServerWeb értéke konfigurálása a helyszíni csomópontok nem érhető el – példa parancsfájl lásd [metaconfigurations DSC generálásához.](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

## <a name="partial-configurations"></a>Részleges konfigurációk

A részleges konfiguráció megadásához hozzon létre egy **PartialConfiguration** blokkot.
Részleges konfigurációkkal kapcsolatos további információkért lásd: [DSC részleges konfigurációk](partialConfigs.md).
**PartialConfiguration** következő tulajdonságait határozza meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|ConfigurationSource|String]|A konfigurációs kiszolgáló, korábban definiált nevét tömbjét **ConfigurationRepositoryWeb** és **ConfigurationRepositoryShare** blokkok, ahol a részleges konfigurációs lekért.|
|dependsOn|Karakterlánc{}|Más konfigurációk, el kell végezni a részleges konfiguráció alkalmazása előtt neveinek listáját.|
|Leírás|karakterlánc|A részleges konfigurációs leíró szöveg.|
|ExclusiveResources|String]|Részleges konfiguráció kizárólagos álló tömb.|
|RefreshMode|karakterlánc|Itt adhatja meg, hogyan a LCM lekérdezi a részleges konfiguráció. A lehetséges értékek a következők __"Letiltva"__, __"Push"__, és __"Pull"__. <ul><li>__Letiltott__: A részleges konfiguráció le van tiltva.</li><li> __Leküldéses__: A részleges konfigurációs rendszer előkészítésre továbbít a csomópontra hívásával a [Publish-DscConfiguration](https://technet.microsoft.com/en-us/library/mt517875.aspx) parancsmag. A csomópont részleges konfigurációi leküldött vagy a szolgáltatástól lekért, miután a konfigurációs meghívásával indítható `Start-DscConfiguration –UseExisting`. Ez az alapértelmezett érték.</li><li>__Lekéréses:__ a csomópont konfigurálva van egy lekéréses szolgáltatásból részleges konfiguráció rendszeresen ellenőrzi. Ha ez a tulajdonság értéke __lekéréses__, meg kell adnia egy lekéréses szolgáltatást egy __ConfigurationSource__ tulajdonság. Azure Automation lekéréses szolgáltatással kapcsolatos további információkért lásd: [Azure Automation DSC – áttekintés](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview).</li></ul>|
|ResourceModuleSource|String]|Az erőforrás-kiszolgáló, amelyről letöltheti a szükséges erőforrások a részleges konfiguráció nevét tömbjét. Ezeket a neveket kell vonatkoznia a korábban meghatározott szolgáltatásvégpontokra **ResourceRepositoryWeb** és **ResourceRepositoryShare** blokkolja.|

__Megjegyzés:__ részleges konfigurációk vannak támogatva az Azure Automation DSC Szolgáltatásban, de csak egy konfigurációs lekért minden egyes csomópontok automation-fiók is lehet.

## <a name="see-also"></a>Lásd még:

### <a name="concepts"></a>Fogalmak
[Szükségeskonfiguráció-State konfigurálása – áttekintés](overview.md)

[Ismerkedés az Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started)

### <a name="other-resources"></a>Egyéb források

[Set-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx)

[Konfigurációs nevek lekéréses ügyfél beállítása](pullClientConfigNames.md)