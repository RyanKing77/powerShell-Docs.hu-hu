---
ms.date: 12/12/2018
keywords: DSC, PowerShell, konfigurálás, beállítás
title: A helyi Configuration Manager konfigurálása
ms.openlocfilehash: 42544036d87fcea3189fd6d2e55579fe87f137e1
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215388"
---
# <a name="configuring-the-local-configuration-manager"></a>A helyi Configuration Manager konfigurálása

> Érvényes: Windows PowerShell 5,0

A helyi Configuration Manager (LCD ChipOnGlas) a kívánt állapot-konfiguráció (DSC) motorja.
Az LCD ChipOnGlas minden cél csomóponton fut, és felelős a csomópontnak eljuttatott konfigurációk elemzéséhez és létrehozásához.
A DSC számos más aspektusa is felelős, beleértve az alábbiakat is.

- A frissítési mód (leküldéses vagy lekéréses) meghatározása.
- Annak megadása, hogy a csomópont milyen gyakran kér le és hozza meg a konfigurációkat.
- A csomópont társítása a lekéréses szolgáltatással.
- Részleges konfigurációk megadása.

Egy speciális konfiguráció használatával konfigurálhatja az LCD ChipOnGlas-t az egyes viselkedések megadásához.
Az alábbi szakaszok azt ismertetik, hogyan konfigurálható az LCD ChipOnGlas.

A Windows PowerShell 5,0 új beállításokat vezetett be a helyi Configuration Manager kezeléséhez.
Az LCD Windows PowerShell 4,0-ben való konfigurálásával kapcsolatos információkért lásd: [a helyi Configuration Manager konfigurálása a Windows PowerShell korábbi verzióiban](metaconfig4.md).

## <a name="writing-and-enacting-an-lcm-configuration"></a>LCD-konfiguráció írása és létrehozása

Az LCD ChipOnGlas konfigurálásához hozzon létre és futtasson egy olyan speciális konfigurációt, amely az LCD-beállításokat alkalmazza.
Az LCD ChipOnGlas-konfiguráció megadásához használja a DscLocalConfigurationManager attribútumot.
Az alábbi ábrán egy egyszerű konfiguráció látható, amely az LCD-t leküldéses módba állítja.

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

A beállítások az LCD-re való alkalmazásának folyamata hasonló a DSC-konfiguráció alkalmazásához.
Létre fog hozni egy LCD ChipOnGlas-konfigurációt, le kell fordítania egy MOF-fájlba, majd alkalmaznia kell azt a csomópontra.
A DSC-konfigurációktól eltérően a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmag meghívásával nem hozhatja végre az LCD-konfigurációt.
Ehelyett hívja a [set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager), és adja meg a (z) paraméterként az LCD ChipOnGlas konfigurációjának elérési útját.
Miután megadta az LCD ChipOnGlas-konfigurációt, megtekintheti az LCD- [DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) parancsmag meghívásával elérhető tulajdonságait.

Az LCD ChipOnGlas-konfiguráció csak korlátozott erőforrás-készletekhez tartalmazhat blokkokat.
Az előző példában az egyetlen nevű erőforrás a **beállítás**.
A többi elérhető erőforrás a következők:

* **ConfigurationRepositoryWeb**: http lekéréses szolgáltatást határoz meg a konfigurációkhoz.
* **ConfigurationRepositoryShare**: a konfigurációk SMB-megosztását adja meg.
* **ResourceRepositoryWeb**: a modulok http lekéréses szolgáltatását adja meg.
* **ResourceRepositoryShare**: a modulok SMB-megosztását adja meg.
* **ReportServerWeb**: egy http lekéréses szolgáltatást ad meg, amelybe a rendszer elküldi a jelentéseket.
* **PartialConfiguration**: lehetővé teszi a részleges konfigurációk engedélyezését.

## <a name="basic-settings"></a>Alapbeállítások

A lekéréses szolgáltatási végpontok/elérési utak és a részleges konfigurációk megadása nélkül az LCD ChipOnGlas összes tulajdonsága egy **beállítási** blokkban van konfigurálva.
A **Beállítások** blokkban a következő tulajdonságok érhetők el.

|  Tulajdonság  |  Típus  |  Leírás   |
|----------- |------- |--------------- |
| ActionAfterReboot| sztring| Meghatározza, hogy mi történjen a konfiguráció alkalmazása során indított újraindítás után. A lehetséges értékek a következők: __"ContinueConfiguration"__ és __"stopconfiguration metódusa"__ . <ul><li> __ContinueConfiguration__: A számítógép újraindítása után folytassa a jelenlegi konfiguráció alkalmazását. Ez az alapértelmezett érték</li><li>__Stopconfiguration metódusa__: A számítógép újraindítása után állítsa le a jelenlegi konfigurációt.</li></ul>|
| AllowModuleOverwrite| bool| __$True__ , hogy a lekéréses szolgáltatásból letöltött új konfigurációk felülírhatják-e a régieket a cél csomóponton. Ellenkező esetben $FALSE.|
| CertificateID| sztring| Egy konfigurációban átadott hitelesítő adatok védelméhez használt tanúsítvány ujjlenyomata. További információ: a [hitelesítő adatok biztonságossá tétele a Windows PowerShell kívánt állapotának konfigurációjában](http://blogs.msdn.com/b/powershell/archive/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration.aspx)?. <br> __Megjegyzés:__ a Azure Automation DSC lekéréses szolgáltatás használata esetén ez automatikusan felügyelhető.|
| ConfigurationDownloadManagers| CimInstance []| Elavult. A konfigurációs lekéréses végpontok definiálásához használja a __ConfigurationRepositoryWeb__ és a __ConfigurationRepositoryShare__ blokkokat.|
| ConfigurationID| sztring| A régebbi lekéréses szolgáltatás verzióival való visszamenőleges kompatibilitás érdekében. A lekéréses szolgáltatásból lekérdezni kívánt konfigurációs fájlt azonosító GUID. A csomópont lekéri a konfigurációkat a lekéréses szolgáltatásban, ha a konfigurációs MOF neve ConfigurationID. MOF néven szerepel.<br> __Megjegyzés:__ Ha ezt a tulajdonságot állítja be, akkor a __RegistrationKey__ használatával a csomópont regisztrálása lekéréses szolgáltatással nem működik. További információ: [lekéréses ügyfél beállítása konfigurációs nevekkel](../pull-server/pullClientConfigNames.md).|
| ConfigurationMode| sztring | Meghatározza, hogy az LCD ChipOnGlas ténylegesen alkalmazza a konfigurációt a cél csomópontokra. A lehetséges értékek a következők: __"ApplyOnly"__ , __"ApplyAndMonitor"__ és __"ApplyAndAutoCorrect"__ . <ul><li>__ApplyOnly__: A DSC alkalmazza a konfigurációt, és nem tesz tovább mást, kivéve, ha új konfigurációt küld a cél csomópontra, vagy amikor új konfigurációt végez egy szolgáltatásból. Új konfiguráció kezdeti alkalmazása után a DSC nem keres eltolódást egy előzőleg konfigurált állapotból. Vegye figyelembe, hogy a DSC addig próbálkozik a konfiguráció alkalmazásával, amíg a __ApplyOnly__ érvénybe lép. </li><li> __ApplyAndMonitor__: Ez az alapértelmezett érték. Az LCD ChipOnGlas minden új konfigurációt alkalmaz. Egy új konfiguráció kezdeti alkalmazása után, ha a cél csomópont a kívánt állapotba sodródik, a DSC a naplókban lévő eltérést jelenti. Vegye figyelembe, hogy a DSC addig próbálkozik a konfiguráció alkalmazásával, amíg a __ApplyAndMonitor__ érvénybe lép.</li><li>__ApplyAndAutoCorrect__: A DSC minden új konfigurációt alkalmaz. Egy új konfiguráció kezdeti alkalmazása után, ha a cél csomópont a kívánt állapotba sodródik, a DSC a naplókban jelzi a következetlenségeket, majd újból alkalmazza az aktuális konfigurációt.</li></ul>|
| ConfigurationModeFrequencyMins| UInt32| Az aktuális konfigurációt percek alatt ellenőrzi és alkalmazza. Ezt a tulajdonságot a rendszer figyelmen kívül hagyja, ha a ConfigurationMode tulajdonság értéke ApplyOnly. Az alapértelmezett érték 15.|
| DebugMode| sztring| A lehetséges értékek a következők: __none__, __ForceModuleImport__és __all__. <ul><li>Állítsa a __nincs__ értékre a gyorsítótárazott erőforrások használatához. Ez az alapértelmezett érték, és éles környezetben kell használni.</li><li>A __ForceModuleImport__beállítás hatására az LCD-modul a DSC-erőforrás moduljait is betölti, még akkor is, ha azokat előzőleg betöltötték és gyorsítótárazták. Ez hatással van a DSC-műveletek teljesítményére, mivel minden modul használatban van. Ezt az értéket általában az erőforrás hibakeresése során érdemes használni</li><li>Ebben a kiadásban az __összes__ ugyanaz, mint a __ForceModuleImport__</li></ul> |
| RebootNodeIfNeeded| bool| Ezzel `$true` a beállítással engedélyezheti az erőforrások számára a csomópont újraindítását a `$global:DSCMachineStatus` jelző használatával. Ellenkező esetben manuálisan kell újraindítani a csomópontot minden szükséges konfigurációhoz. Az alapértelmezett érték: `$false`. Ha ezt a beállítást akkor szeretné használni, ha a DSC-től eltérő (például Windows Installer) állapotú újraindítás feltételt alkalmaz, ezt a beállítást a [xPendingReboot](https://github.com/powershell/xpendingreboot) modullal kell kombinálni.|
| RefreshMode| sztring| Meghatározza, hogyan legyenek a LCD-LCD-konfigurációk. A lehetséges értékek: __"Letiltva__", __"push"__ és __"pull"__ . <ul><li>__Letiltva__: A DSC-konfigurációk le vannak tiltva ehhez a csomóponthoz.</li><li> __Leküldés__: A konfigurációk a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmag meghívásával indíthatók el. A rendszer azonnal alkalmazza a konfigurációt a csomópontra. Ez az alapértelmezett érték.</li><li>__Lekéréses__ A csomópont úgy van konfigurálva, hogy rendszeresen keressen konfigurációkat egy lekéréses szolgáltatásból vagy SMB-útvonalból. Ha ez a tulajdonság a __pull__értékre van állítva, meg kell adnia egy http (szolgáltatás) vagy SMB (megosztás) elérési utat egy __ConfigurationRepositoryWeb__ vagy __ConfigurationRepositoryShare__ blokkban.</li></ul>|
| RefreshFrequencyMins| Uint32| Az az időtartam (percben kifejezve), ameddig az LCD-egység ellenőrzi a lekéréses szolgáltatást a frissített konfigurációk lekérdezéséhez. A rendszer figyelmen kívül hagyja ezt az értéket, ha az LCD ChipOnGlas nem lekéréses módban van konfigurálva. Az alapértelmezett érték 30.|
| ReportManagers| CimInstance []| Elavult. __ReportServerWeb__ -blokkokkal definiálhat egy végpontot, amely jelentést küld egy lekéréses szolgáltatásnak.|
| ResourceModuleManagers| CimInstance []| Elavult. A lekéréses szolgáltatás HTTP-végpontjai vagy SMB-elérési útjai a __ResourceRepositoryWeb__ és a __ResourceRepositoryShare__ blokk használatával definiálhatók.|
| PartialConfigurations| CimInstance| Nincs implementálva. Ne használja.|
| StatusRetentionTimeInDays | UInt32| Azon napok száma, ameddig az LCD-ben az aktuális konfiguráció állapota megmarad.|

> [!NOTE]
> Az LCD ChipOnGlas a következő alapján indítja el a **ConfigurationModeFrequencyMins** ciklust:
>
> - Új metaconfig alkalmaz a használatával`Set-DscLocalConfigurationManager`
> - Számítógép újraindítása
>
> Minden olyan feltételnél, ahol az időzítő folyamata összeomlást tapasztal, 30 másodpercen belül észlelhető, és a ciklus újra fog indulni.
> Egy egyidejű művelet késleltetheti a ciklus indítását, ha a művelet időtartama meghaladja a beállított ciklusok gyakoriságát, a következő időzítő nem fog elindulni.
>
> Példa: a metaconfig 15 perces lekéréses gyakorisággal van konfigurálva, és a lekéréses művelet a T1 időpontban történik.  A csomópont 16 percen belül nem fejeződik be.  Az első 15 perces ciklus figyelmen kívül lesz hagyva, és a következő lekérés a T1 + 15 + 15 időpontban történik.

## <a name="pull-service"></a>Lekéréses szolgáltatás

Az LCD ChipOnGlas-konfiguráció a következő típusú lekéréses szolgáltatási végpontok definiálását támogatja:

- **Konfigurációs kiszolgáló**: A DSC-konfigurációk tárháza. A konfigurációs kiszolgálók definiálása a **ConfigurationRepositoryWeb** (webalapú kiszolgálók esetében) és a **ConfigurationRepositoryShare** (SMB-alapú kiszolgálók esetében) használatával.
- **Erőforrás-kiszolgáló**: Egy PowerShell-modulként csomagolt DSC-erőforrások tárháza. Az **ResourceRepositoryWeb** (webalapú kiszolgálók esetében) és a **ResourceRepositoryShare** (SMB-alapú kiszolgálók) blokkolja az erőforrás-kiszolgálók definiálását.
- **Jelentéskészítő kiszolgáló**: Egy szolgáltatás, amelyet a DSC a jelentésre vonatkozó adatokat küld. Jelentéskészítő kiszolgálók definiálása **ReportServerWeb** -blokkok használatával. A jelentéskészítő kiszolgálónak webszolgáltatásnak kell lennie.

A lekéréses szolgáltatással kapcsolatos további részletekért tekintse meg a [kívánt állapot konfigurációjának lekérése szolgáltatást](../pull-server/pullServer.md).

## <a name="configuration-server-blocks"></a>Konfigurációs kiszolgáló blokkolja

Webalapú konfigurációs kiszolgáló definiálásához létre kell hoznia egy **ConfigurationRepositoryWeb** -blokkot.
A **ConfigurationRepositoryWeb** a következő tulajdonságokat határozzák meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|AllowUnsecureConnection|bool|Állítsa **$true** értékre, ha engedélyezni szeretné a csomópontról a kiszolgálóra való csatlakozást hitelesítés nélkül. A hitelesítés megköveteléséhez állítsa **$false** értékre.|
|CertificateID|sztring|A kiszolgálón történő hitelesítéshez használt tanúsítvány ujjlenyomata.|
|ConfigurationNames|Karakterlánc []|A cél csomópont által lekért konfigurációk neveinek tömbje. Ezeket csak akkor használja a rendszer, ha a csomópontot **RegistrationKey**használatával regisztrálják a lekéréses szolgáltatásban. További információ: [lekéréses ügyfél beállítása konfigurációs nevekkel](../pull-server/pullClientConfigNames.md).|
|RegistrationKey|sztring|Egy GUID, amely regisztrálja a csomópontot a lekéréses szolgáltatásban. További információ: [lekéréses ügyfél beállítása konfigurációs nevekkel](../pull-server/pullClientConfigNames.md).|
|ServerURL|sztring|A konfigurációs szolgáltatás URL-címe.|
|ProxyURL*|sztring|A konfigurációs szolgáltatással folytatott kommunikáció során használandó http-proxy URL-címe.|
|ProxyCredential*|pscredential|A http-proxyhoz használandó hitelesítő adat.|

> [!NOTE]
> * A Windows 1809-es és újabb verzióiban támogatott.

A helyszíni csomópontok ConfigurationRepositoryWeb-értékének egyszerűbb konfigurálását bemutató parancsfájl elérhető – lásd: [DSC-Metaconfigurations generálása](https://docs.microsoft.com/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

Az SMB-alapú konfigurációs kiszolgáló definiálásához létre kell hoznia egy **ConfigurationRepositoryShare** -blokkot.
A **ConfigurationRepositoryShare** a következő tulajdonságokat határozzák meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|Hitelesítőadat|MSFT_Credential|Az SMB-megosztás hitelesítéséhez használt hitelesítő adat.|
|SourcePath|sztring|Az SMB-megosztás elérési útja.|

## <a name="resource-server-blocks"></a>Erőforrás-kiszolgáló blokkolja

Webalapú erőforrás-kiszolgáló definiálásához létre kell hoznia egy **ResourceRepositoryWeb** -blokkot.
A **ResourceRepositoryWeb** a következő tulajdonságokat határozzák meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|AllowUnsecureConnection|bool|Állítsa **$true** értékre, ha engedélyezni szeretné a csomópontról a kiszolgálóra való csatlakozást hitelesítés nélkül. A hitelesítés megköveteléséhez állítsa **$false** értékre.|
|CertificateID|sztring|A kiszolgálón történő hitelesítéshez használt tanúsítvány ujjlenyomata.|
|RegistrationKey|sztring|Egy GUID, amely azonosítja a csomópontot a lekéréses szolgáltatáshoz.|
|ServerURL|sztring|A konfigurációs kiszolgáló URL-címe.|
|ProxyURL*|sztring|A konfigurációs szolgáltatással folytatott kommunikáció során használandó http-proxy URL-címe.|
|ProxyCredential*|pscredential|A http-proxyhoz használandó hitelesítő adat.|

> [!NOTE]
> * A Windows 1809-es és újabb verzióiban támogatott.

A helyszíni csomópontok ResourceRepositoryWeb-értékének egyszerűbb konfigurálását bemutató parancsfájl elérhető – lásd: [DSC-Metaconfigurations generálása](https://docs.microsoft.com/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

Egy SMB-alapú erőforrás-kiszolgáló definiálásához létre kell hoznia egy **ResourceRepositoryShare** -blokkot.
A **ResourceRepositoryShare** a következő tulajdonságokat határozza meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|Hitelesítőadat|MSFT_Credential|Az SMB-megosztás hitelesítéséhez használt hitelesítő adat. A hitelesítő adatok átadására példát a [DSC SMB-lekérési kiszolgáló beállítása](../pull-server/pullServerSMB.md) című témakörben talál.|
|SourcePath|sztring|Az SMB-megosztás elérési útja.|

## <a name="report-server-blocks"></a>Jelentéskészítő kiszolgáló – blokkok

A jelentéskészítő kiszolgáló definiálásához létre kell hoznia egy **ReportServerWeb** -blokkot.
A jelentéskészítő kiszolgáló szerepkör nem kompatibilis az SMB-alapú lekéréses szolgáltatással.
A **ReportServerWeb** a következő tulajdonságokat határozza meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|AllowUnsecureConnection|bool|Állítsa **$true** értékre, ha engedélyezni szeretné a csomópontról a kiszolgálóra való csatlakozást hitelesítés nélkül. A hitelesítés megköveteléséhez állítsa **$false** értékre.|
|CertificateID|sztring|A kiszolgálón történő hitelesítéshez használt tanúsítvány ujjlenyomata.|
|RegistrationKey|sztring|Egy GUID, amely azonosítja a csomópontot a lekéréses szolgáltatáshoz.|
|ServerURL|sztring|A konfigurációs kiszolgáló URL-címe.|
|ProxyURL*|sztring|A konfigurációs szolgáltatással folytatott kommunikáció során használandó http-proxy URL-címe.|
|ProxyCredential*|pscredential|A http-proxyhoz használandó hitelesítő adat.|

> [!NOTE]
> * A Windows 1809-es és újabb verzióiban támogatott.

A helyszíni csomópontok ReportServerWeb-értékének egyszerűbb konfigurálását bemutató parancsfájl elérhető – lásd: [DSC-Metaconfigurations generálása](https://docs.microsoft.com/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

## <a name="partial-configurations"></a>Részleges konfigurációk

Részleges konfiguráció definiálásához létre kell hoznia egy **PartialConfiguration** -blokkot.
A részleges konfigurációkról a [DSC részleges konfigurációit](../pull-server/partialConfigs.md)ismertető témakörben olvashat bővebben.
A **PartialConfiguration** a következő tulajdonságokat határozza meg.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|ConfigurationSource|karakterlánc []|A **ConfigurationRepositoryWeb** -és **ConfigurationRepositoryShare** -blokkokban korábban definiált konfigurációs kiszolgálók neveinek tömbje, ahol a részleges konfigurációt a rendszer lekéri.|
|DependsOn|karakterlánc{}|Azon egyéb konfigurációk neveinek listája, amelyeket a részleges konfiguráció alkalmazása előtt kell végrehajtani.|
|Leírás|sztring|A részleges konfiguráció leírására szolgáló szöveg|
|ExclusiveResources|karakterlánc []|Erőforrások tömbje, amely kizárólag erre a részleges konfigurációra vonatkozik.|
|RefreshMode|sztring|Megadja, hogy az LCD ChipOnGlas hogyan kapja meg ezt a részleges konfigurációt. A lehetséges értékek: __"Letiltva__", __"push"__ és __"pull"__ . <ul><li>__Letiltva__: Ez a részleges konfiguráció le van tiltva.</li><li> __Leküldés__: A részleges konfigurációt a rendszer leküldi a csomópontra a [publish-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) parancsmag meghívásával. Miután a csomópont összes részleges konfigurációját leküldték vagy lehúzta a szolgáltatásból, a konfiguráció meghívásával `Start-DscConfiguration –UseExisting`indítható el. Ez az alapértelmezett érték.</li><li>__Lekéréses__ A csomópont úgy van konfigurálva, hogy rendszeresen keressen egy lekéréses szolgáltatás részleges konfigurációját. Ha ez a tulajdonság a __pull__értékre van állítva, egy lekéréses szolgáltatást kell megadnia egy __ConfigurationSource__ tulajdonságban. Azure Automation lekéréses szolgáltatással kapcsolatos további információkért lásd: [Azure Automation DSC – áttekintés](https://docs.microsoft.com/azure/automation/automation-dsc-overview).</li></ul>|
|ResourceModuleSource|karakterlánc []|Azon erőforrás-kiszolgálók neveinek tömbje, amelyekről le kell tölteni a szükséges erőforrásokat ehhez a részleges konfigurációhoz. Ezeknek a névnek a **ResourceRepositoryWeb** -és **ResourceRepositoryShare** -blokkokban korábban definiált szolgáltatási végpontokra kell vonatkoznia.|

__Megjegyzés:__ a részleges KONFIGURÁCIÓK Azure Automation DSC-vel támogatottak, de minden egyes Automation-fiókból csak egy konfigurációt lehet kihúzni.

## <a name="see-also"></a>Lásd még:

### <a name="concepts"></a>Fogalmak
[A kívánt állapot konfigurációjának áttekintése](../overview/overview.md)

[Első lépések a Azure Automation DSC-vel](https://docs.microsoft.com/azure/automation/automation-dsc-getting-started)

### <a name="other-resources"></a>Egyéb források

[Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager)

[Lekérési ügyfél beállítása konfigurációs nevekkel](../pull-server/pullClientConfigNames.md)
