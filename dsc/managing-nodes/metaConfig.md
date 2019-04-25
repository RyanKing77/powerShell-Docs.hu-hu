---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A helyi Configuration Manager
ms.openlocfilehash: 86d2cc17872692a738e9c68121b8931833d2a251
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079676"
---
# <a name="configuring-the-local-configuration-manager"></a>A helyi Configuration Manager

> A következőkre vonatkozik: Windows PowerShell 5.0

A helyi Configuration Manager (LCM) Konfigurálása a Desired State Configuration (DSC) rétegen a motor.
Az LCM minden célként megadott csomóponton fut, és -elemzés és a csomópont küldött konfigurációk életbe léptetése.
Feladata még számos egyéb aspektusait DSC, többek között a következőket.

- Frissítési mód (leküldéses és lekéréses) meghatározása.
- Adja meg, milyen gyakran egy csomópont lekéri és konfigurációk ír elő.
- A csomópont társítása lekérési szolgáltatást.
- Részleges konfigurációk megadása.

Egy speciális típusú konfigurációs használatával minden egyes ezen viselkedés megadása az LCM konfigurálása.
A következő szakaszok ismertetik az LCM konfigurálása.

Windows PowerShell 5.0 bevezetett új beállítások kezeléséhez a Local Configuration Manager.
Az LCM konfigurálása a Windows PowerShell 4.0 kapcsolatos információkért lásd: [konfigurálása a Local Configuration Manager korábbi verzióiban a Windows PowerShell-ben](metaconfig4.md).

## <a name="writing-and-enacting-an-lcm-configuration"></a>És a egy LCM konfiguráció életbe léptetése

Az LCM konfigurálása, létrehozása és futtatása egy speciális típusú konfigurációt, amely érvényes LCM beállításait.
Adjon meg egy LCM konfigurációt, használja a DscLocalConfigurationManager attribútum.
Az alábbiakban látható egy egyszerű leküldéses módba állítja a LCM konfigurációját.

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

A beállítások alkalmazására LCM Konfigurálása a folyamat hasonlít a DSC-konfiguráció alkalmazása.
Az LCM konfigurálása létrehoz, fordítsa MOF-fájlba, és alkalmazza azt a csomópontot.
Ellentétben a DSC-konfigurációk, hogy nem kihirdeti az LCM konfigurálása meghívásával a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.
Ehelyett hívja [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager), Főhitelesítésszolgáltató az LCM konfigurálása paraméterként MOF elérési útját.
Az LCM konfigurálása, kihirdeti, miután a LCM tulajdonságainak meghívásával láthatja a [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) parancsmagot.

Az LCM konfigurálása egységenként csak korlátozott számú erőforrásokat is tartalmazhat.
Az előző példában a nevű egyetlen erőforrás van **beállítások**.
A rendelkezésre álló erőforrások a következők:

* **ConfigurationRepositoryWeb**: egy HTTP-lekéréses szolgáltatást konfigurációk határozza meg.
* **ConfigurationRepositoryShare**: Itt adhatja meg a konfigurációk SMB-megosztáson.
* **ResourceRepositoryWeb**: Itt adhatja meg a modulok egy HTTP lekéréses szolgáltatás.
* **ResourceRepositoryShare**: Itt adhatja meg a modulok SMB-megosztáson.
* **ReportServerWeb**: Itt adhatja meg egy HTTP-lekéréses szolgáltatás, amely jelentések küldik.
* **PartialConfiguration**: ahhoz, hogy részleges konfigurációk adatokat biztosít.

## <a name="basic-settings"></a>Alapbeállítások

Eltérő lekéréses szolgáltatás végpontok/elérési utakat és részleges konfigurációk megadása, mind az LCM tulajdonságainak konfigurált egy **beállítások** letiltása.
A következő tulajdonságok érhetők el egy **beállítások** letiltása.

|  Tulajdonság  |  Típus  |  Leírás   |
|----------- |------- |--------------- |
| ActionAfterReboot| sztring| Itt adhatja meg, mi történik a számítógép újraindítása után a beállítások alkalmazása során. A lehetséges értékek a következők __"ContinueConfiguration"__ és __"StopConfiguration"__. <ul><li> __ContinueConfiguration__: Továbbra is a számítógép újraindítása után az aktuális konfiguráció alkalmazása. Ez az az alapértelmezett érték</li><li>__StopConfiguration__: Állítsa le a számítógép újraindítása után az aktuális konfigurációt.</li></ul>|
| AllowModuleOverwrite| bool| __$TRUE__ Ha a lekéréses szolgáltatásból letöltött új konfigurációk engedélyezettek-e a régieket célcsomóponton felülírásához. Más esetekben $FALSE.|
| CertificateID| sztring| A konfigurációban az átadott hitelesítő adatok védelmére szolgáló tanúsítvány ujjlenyomatát. További információ: [hitelesítő adatai a Windows PowerShell Desired State Configuration engedélyezzen](http://blogs.msdn.com/b/powershell/archive/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration.aspx)?. <br> __Megjegyzés:__ automatikusan ez történik, ha az Azure Automation DSC lekéréses szolgáltatás segítségével.|
| ConfigurationDownloadManagers| CimInstance[]| Elavult. Használat __ConfigurationRepositoryWeb__ és __ConfigurationRepositoryShare__ érdekében adja meg a konfigurációs lekérési szolgáltatásvégpontokat.|
| ConfigurationID| sztring| Visszamenőleges kompatibilitáshoz régebbi lekéréses Service a verziók. Egy GUID Azonosítót, amely azonosítja a konfigurációs fájl egy lekéréses szolgáltatásból való beolvasására. A konfiguráció nevét MOF ConfigurationID.mof neve a csomópont konfigurációk fogja lekérni a lekéréses szolgáltatás.<br> __Megjegyzés:__ Ha ezt a tulajdonságot, a csomópont történő regisztrációt egy lekéréses szolgáltatás használatával __RegistrationKey__ nem működik. További információkért lásd: [konfigurációs nevekkel lekérési ügyfél beállítása](../pull-server/pullClientConfigNames.md).|
| ConfigurationMode| sztring | Itt adhatja meg, hogyan az LCM ténylegesen alkalmazza a konfigurációt, a célcsomópontokat. Lehetséges értékek a következők __"ApplyOnly"__,__"ApplyAndMonitor"__, és __"ApplyAndAutoCorrect"__. <ul><li>__ApplyOnly__: DSC konfigurációjának alkalmazására szolgál, és nem módosítja a további, kivéve, ha egy új konfiguráció leküldéssel a célcsomópont, vagy ha egy új konfigurációt a szolgáltatástól kéri le. Új konfiguráció kezdeti léptetés DSC nem ellenőrzi az előzőleg konfigurált állapotba való eltéréseket. Vegye figyelembe, hogy a alkalmazni a konfigurációt, egészen addig, amíg a sikeres előtt megkísérli DSC __ApplyOnly__ lép érvénybe. </li><li> __ApplyAndMonitor__: Ez az alapértelmezett érték. Az LCM vonatkozik minden új konfigurációt. Új konfiguráció, kezdeti alkalmazása után a a célcsomópont drifts a kívánt állapotból, ha DSC jelentések naplók az eltérést. Vegye figyelembe, hogy a alkalmazni a konfigurációt, egészen addig, amíg a sikeres előtt megkísérli DSC __ApplyAndMonitor__ lép érvénybe.</li><li>__ApplyAndAutoCorrect__: DSC vonatkozik minden új konfigurációt. Kezdeti alkalmazását követően az új konfiguráció a célcsomópont drifts a kívánt állapotból, ha DSC-jelentések a naplókban az eltérés, és majd újra alkalmazza a jelenlegi konfiguráció.</li></ul>|
| ConfigurationModeFrequencyMins| UInt32| Milyen gyakran percek alatt, a jelenlegi konfiguráció be van jelölve és alkalmazása. A rendszer figyelmen kívül hagyja ezt a tulajdonságot, ha a ConfigurationMode tulajdonsága ApplyOnly. Az alapértelmezett érték 15.|
| DebugMode| sztring| Lehetséges értékek a következők __nincs__, __ForceModuleImport__, és __összes__. <ul><li>Állítsa be __None__ a gyorsítótárazott erőforrások. Ez az alapértelmezett beállítás, és éles forgatókönyvekben használjon.</li><li>Beállítás __ForceModuleImport__, ide az újrabetöltéshez DSC erőforrás modulokat, még akkor is, ha azokat korábban már betöltötte és gyorsítótárba helyezték a LCM okoz. Ez hatással van DSC műveletek teljesítményének, minden egyes modul újbóli felhasználására. Általában használna az ezt az értéket egy erőforrás-hibakeresés közben</li><li>Ebben a kiadásban __összes__ azonos __ForceModuleImport__</li></ul> |
| RebootNodeIfNeeded| bool| Állítsa a bestattempt értékre `$true` lehetővé teszik az erőforrások újraindításához, a Node használatával, a `$global:DSCMachineStatus` jelzőt. Ellenkező esetben el manuálisan indítsa újra a csomópont minden olyan konfiguráció, amely ezt megköveteli. Az alapértelmezett érték: `$false`. Használja ezt a beállítást, ha újraindítás feltétel nem DSC (például a Windows Installer) szerint van gyakorlatokkal, kombinálja együtt a [xPendingReboot](https://github.com/powershell/xpendingreboot) modul.|
| A RefreshMode| sztring| Itt adhatja meg, hogyan az LCM lekéri a konfigurációt. A lehetséges értékek a következők __"Letiltva"__, __"Push"__, és __"Lekérés"__. <ul><li>__Letiltott__: DSC-konfigurációk le van tiltva ezen a csomóponton.</li><li> __Leküldéses__: Konfigurációk meghívásával kezdeményezett a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot. A konfiguráció alkalmazása azonnal megtörténik a csomópontra. Ez az alapértelmezett érték.</li><li>__Kérje le:__ A csomópont rendszeresen ellenőrzi a lekérési szolgáltatást vagy az SMB elérési konfigurációk van konfigurálva. Ha ez a tulajdonság értéke __lekéréses__, (szolgáltatás) HTTP- vagy SMB (megosztás) elérési utat adjon meg egy __ConfigurationRepositoryWeb__ vagy __ConfigurationRepositoryShare__ letiltása.</li></ul>|
| RefreshFrequencyMins| Uint32| Az időintervallum, percek alatt, ahol az LCM lekéréses szolgáltatásával a szükséges frissített konfigurációk ellenőrzi. A rendszer figyelmen kívül hagyja ezt az értéket, ha az LCM lekéréses módban nincs konfigurálva. Az alapértelmezett érték 30.|
| ReportManagers| CimInstance[]| Elavult. Használat __ReportServerWeb__ küldése végpontokat blokkolja egy lekéréses szolgáltatás számára.|
| ResourceModuleManagers| CimInstance[]| Elavult. Használat __ResourceRepositoryWeb__ és __ResourceRepositoryShare__ lekéréses meghatározásához blokkok service HTTP-végpontokat vagy SMB elérési utak jelölik.|
| PartialConfigurations| CimInstance| Není implementována. Ne használja.|
| StatusRetentionTimeInDays | UInt32| Az LCM tartja az aktuális konfigurációs állapotát napok száma.|

> [!NOTE]
> Az LCM elindításakor a **ConfigurationModeFrequencyMins** ciklus alapján:
>
> - Egy új metaconfig használatával alkalmazta `Set-DscLocalConfigurationManager`
> - A gép újraindítása
>
> Minden olyan feltétel, ahol az időzítő folyamata során lép fel, amelyek 30 másodpercen belül összeomlás, és újraindítja a ciklus.
> Egy párhuzamos művelet sikerült. a ciklus késleltetés az indítás alatt, ha ez a művelet időtartama meghaladja a konfigurált ciklus gyakoriságát, a következő időzítő nem indul el.
>
> A példában a metaconfig lekéréses 15 perces gyakorisággal van beállítva, és egy lekéréses T1 kapcsolaton keresztül történik.  A csomópont nem fejeződik be a munkahelyi 16 percig.  Az első 15 perces ciklus a rendszer figyelmen kívül hagyja, és a következő lekéréses fog zajlani a T1 + 15: 15.

## <a name="pull-service"></a>Lekérési szolgáltatást

Az LCM konfigurálása is támogatja a következő típusú lekéréses Szolgáltatásvégpontok:

- **Konfigurációs kiszolgáló**: Egy adattár a DSC-konfigurációk. Adja meg a konfigurációs kiszolgálók használatával **ConfigurationRepositoryWeb** (a web-alapú kiszolgálók) és **ConfigurationRepositoryShare** (az SMB-alapú kiszolgálók) blokkokat.
- **Erőforrás-kiszolgáló**: DSC-erőforrások PowerShell-modulok csomagolt egy adattárat. Erőforrás-kiszolgálók megadása segítségével **ResourceRepositoryWeb** (a web-alapú kiszolgálók) és **ResourceRepositoryShare** (az SMB-alapú kiszolgálók) blokkokat.
- **Jelentéskészítő kiszolgáló**: Egy szolgáltatás, amely a DSC jelentéskészítő adatokat küld. Adja meg a jelentéskészítő kiszolgálók használatával **ReportServerWeb** blokkokat. A jelentéskészítő kiszolgáló webszolgáltatás kell lennie.

További információ a lekéréses szolgáltatás:, [Desired State Configuration lekéréses szolgáltatás](../pull-server/pullServer.md).

## <a name="configuration-server-blocks"></a>Konfigurációs kiszolgáló blokkok

Annak meghatározásához, web-alapú konfigurációs kiszolgáló, hozzon létre egy **ConfigurationRepositoryWeb** letiltása.
A **ConfigurationRepositoryWeb** határozza meg az alábbi tulajdonságokat.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|AllowUnsecureConnection|bool|Állítsa be **$TRUE** , hogy a kiszolgáló hitelesítése nélkül csatlakozhat a csomópontról. Állítsa be **$FALSE** hitelesítést igényel.|
|CertificateID|sztring|A kiszolgáló hitelesítésére használt tanúsítvány ujjlenyomatát.|
|ConfigurationNames|String]|Le kell kérnie a cél csomópont-konfigurációk nevek tömbje. Ezek használhatók csak akkor, ha a csomópont regisztrálva van a lekéréses szolgáltatás segítségével egy **RegistrationKey**. További információkért lásd: [konfigurációs nevekkel lekérési ügyfél beállítása](../pull-server/pullClientConfigNames.md).|
|RegistrationKey|sztring|Regisztrálja a csomópontot a lekéréses szolgáltatás GUID azonosítója. További információkért lásd: [konfigurációs nevekkel lekérési ügyfél beállítása](../pull-server/pullClientConfigNames.md).|
|ServerURL|sztring|A konfigurációs szolgáltatás URL-címe|

Példa parancsfájl egyszerűsítése érdekében a ConfigurationRepositoryWeb érték konfigurálása a helyszíni csomópont nem érhető el – lásd: [létrehozása DSC metaconfigurations](https://docs.microsoft.com/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

Meghatároz egy SMB-alapú konfigurációs kiszolgálót, létre kell hozni egy **ConfigurationRepositoryShare** letiltása.
A **ConfigurationRepositoryShare** határozza meg az alábbi tulajdonságokat.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|Hitelesítő adatok|MSFT_Credential|Az SMB-megosztás hitelesítéséhez használt hitelesítő adatokat.|
|SourcePath|sztring|Az SMB-megosztás elérési útja.|

## <a name="resource-server-blocks"></a>Erőforrás-kiszolgáló blokkok

Annak meghatározásához, web-alapú erőforrás-kiszolgáló, hozzon létre egy **ResourceRepositoryWeb** letiltása.
A **ResourceRepositoryWeb** határozza meg az alábbi tulajdonságokat.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|AllowUnsecureConnection|bool|Állítsa be **$TRUE** , hogy a kiszolgáló hitelesítése nélkül csatlakozhat a csomópontról. Állítsa be **$FALSE** hitelesítést igényel.|
|CertificateID|sztring|A kiszolgáló hitelesítésére használt tanúsítvány ujjlenyomatát.|
|RegistrationKey|sztring|Egy GUID Azonosítót, amely azonosítja a csomópont a pull-szolgáltatáshoz.|
|ServerURL|sztring|A konfigurációs kiszolgáló URL-címe|

Példa parancsfájl egyszerűsítése érdekében a ResourceRepositoryWeb érték konfigurálása a helyszíni csomópont nem érhető el – lásd: [létrehozása DSC metaconfigurations](https://docs.microsoft.com/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

Meghatároz egy SMB-alapú erőforrás-kiszolgáló, létre kell hozni egy **ResourceRepositoryShare** letiltása.
**ResourceRepositoryShare** határozza meg az alábbi tulajdonságokat.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|Hitelesítő adatok|MSFT_Credential|Az SMB-megosztás hitelesítéséhez használt hitelesítő adatokat. A hitelesítő adatokat továbbít egy példa: [a DSC SMB-lekérési kiszolgálójának beállítása](../pull-server/pullServerSMB.md)|
|SourcePath|sztring|Az SMB-megosztás elérési útja.|

## <a name="report-server-blocks"></a>Jelentéskészítő kiszolgáló blokkok

Adja meg a jelentéskészítő kiszolgálón, létre kell hozni egy **ReportServerWeb** letiltása.
A jelentéskészítő kiszolgálói szerepkör, ezért nem kompatibilis az SMB-alapú lekérési szolgáltatást.
**ReportServerWeb** határozza meg az alábbi tulajdonságokat.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|AllowUnsecureConnection|bool|Állítsa be **$TRUE** , hogy a kiszolgáló hitelesítése nélkül csatlakozhat a csomópontról. Állítsa be **$FALSE** hitelesítést igényel.|
|CertificateID|sztring|A kiszolgáló hitelesítésére használt tanúsítvány ujjlenyomatát.|
|RegistrationKey|sztring|Egy GUID Azonosítót, amely azonosítja a csomópont a pull-szolgáltatáshoz.|
|ServerURL|sztring|A konfigurációs kiszolgáló URL-címe|

Példa parancsfájl egyszerűsítése érdekében a ReportServerWeb érték konfigurálása a helyszíni csomópont nem érhető el – lásd: [létrehozása DSC metaconfigurations](https://docs.microsoft.com/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

## <a name="partial-configurations"></a>Részleges konfigurációk

Egy részleges konfiguráció definiálása, létre kell hozni egy **PartialConfiguration** letiltása.
Részleges konfigurációk kapcsolatos további információkért lásd: [DSC részleges konfigurációk](../pull-server/partialConfigs.md).
**PartialConfiguration** határozza meg az alábbi tulajdonságokat.

|Tulajdonság|Típus|Leírás|
|---|---|---|
|ConfigurationSource|String]|Korábban definiált konfigurációs kiszolgálók nevére tömbjét **ConfigurationRepositoryWeb** és **ConfigurationRepositoryShare** blokkok, ahol a részleges konfigurációs származhatnak.|
|DependsOn|Karakterlánc{}|Egyéb konfigurációk, amelyek a részleges konfiguráció alkalmazása előtt el kell végezni a nevek listája.|
|Leírás|sztring|A részleges konfigurációját leíró szöveg.|
|ExclusiveResources|String]|Ehhez a konfigurációhoz részleges kizárólagos erőforrások tömbje.|
|A RefreshMode|sztring|Itt adhatja meg, hogyan az LCM lekérdezi a részleges ezt a konfigurációt. A lehetséges értékek a következők __"Letiltva"__, __"Push"__, és __"Lekérés"__. <ul><li>__Letiltott__: A részleges konfigurációja le van tiltva.</li><li> __Leküldéses__: A részleges konfiguráció át lett helyezve a csomópont meghívásával a [Publish-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) parancsmagot. A csomópont minden részleges konfigurációk vagy leküldött vagy egy szolgáltatás származhatnak, miután a konfiguráció meghívásával indítható `Start-DscConfiguration –UseExisting`. Ez az alapértelmezett érték.</li><li>__Kérje le:__ A csomópont rendszeresen keressen egy lekéréses szolgáltatás részleges konfigurációs van konfigurálva. Ha ez a tulajdonság értéke __lekéréses__, meg kell adnia egy lekéréses szolgáltatás egy __ConfigurationSource__ tulajdonság. Azure Automation-lekérési szolgáltatással kapcsolatos további információkért lásd: [Azure Automation DSC áttekintése](https://docs.microsoft.com/azure/automation/automation-dsc-overview).</li></ul>|
|ResourceModuleSource|String]|Tömb, ahonnan letölthető a részleges konfiguráció szükséges erőforrások erőforrás-kiszolgálók nevére. Ezeket a neveket kell hivatkoznia a korábban meghatározott szolgáltatásvégpontokra **ResourceRepositoryWeb** és **ResourceRepositoryShare** blokkokat.|

__Megjegyzés:__ részleges konfigurációk az Azure Automation DSC használata támogatott, de csak egy konfigurációs is le kell kérnie, a csomópontonkénti minden automation-fiók.

## <a name="see-also"></a>Lásd még:

### <a name="concepts"></a>Fogalmak
[Desired State Configuration áttekintése](../overview/overview.md)

[Azure Automation DSC – első lépések](https://docs.microsoft.com/azure/automation/automation-dsc-getting-started)

### <a name="other-resources"></a>Egyéb források

[Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager)

[A konfigurációs nevek lekérési ügyfél beállítása](../pull-server/pullClientConfigNames.md)
