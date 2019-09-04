---
ms.date: 12/12/2018
keywords: DSC, PowerShell, konfigurálás, beállítás
title: Az Import-DSCResource használata
ms.openlocfilehash: e1c2c06d756a70c2de516f330e3123235ce740ba
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215398"
---
# <a name="using-import-dscresource"></a>Az Import-DSCResource használata

`Import-DScResource`egy dinamikus kulcsszó, amely csak a konfigurációs parancsfájlok blokkjában használható. A `Import-DSCResource` konfigurációban szükséges erőforrások importálására szolgáló kulcsszó. A rendszer automatikusan importálja az erőforrásokat, de az ajánlott eljárás a konfigurációban használt összes erőforrás explicit módon történő importálása is. [](Configurations.md) `$pshome`

A szintaxisa `Import-DSCResource` alább látható.  A modulok név szerint történő megadásakor követelmény, hogy mindegyiket egy új sorba sorolja.

```syntax
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName>]
```

|Paraméter  |Leírás  |
|---------|---------|
|`-Name`|A DSC-erőforrás neve (i), amelyet importálnia kell. Ha a modul neve meg van adva, a parancs ezen a modulon belül keresi a DSC-erőforrásokat. Ellenkező esetben a parancs az összes DSC-erőforrás elérési útján keresi a DSC-erőforrásokat. A helyettesítő karakterek használata támogatott.|
|`-ModuleName`|A modul neve vagy a modul specifikációja.  Ha egy modulból importálandó erőforrásokat ad meg, a parancs csak ezeket az erőforrásokat fogja importálni. Ha csak a modult adta meg, a parancs a modulban lévő összes DSC-erőforrást importálja.|

```powershell
Import-DscResource -ModuleName xActiveDirectory;
```

## <a name="example-use-import-dscresource-within-a-configuration"></a>Példa: Az import-DSCResource használata egy konfiguráción belül

```powershell
Configuration MSDSCConfiguration
{
    # Search for and imports Service, File, and Registry from the module PSDesiredStateConfiguration.
    Import-DSCResource -ModuleName PSDesiredStateConfiguration -Name Service, File, Registry
    
    # Search for and import Resource1 from the module that defines it.
    # If only –Name parameter is used then resources can belong to different PowerShell modules as well.
    # TimeZone resource is from the ComputerManagementDSC module which is not installed by default.
    # As a best practice, list each requirement on a different line if possible.  This makes reviewing
    # multiple changes in source control a bit easier.
    Import-DSCResource -Name File
    Import-DSCResource -Name TimeZone

    # Search for and import all DSC resources inside the module PSDesiredStateConfiguration.
    # When specifying the modulename parameter, it is a requirement to list each on a new line.
    Import-DSCResource -ModuleName PSDesiredStateConfiguration
    Import-DSCResource -ModuleName ComputerManagementDsc
...
```

> [!NOTE]
> Ha több értéket ad meg az erőforrás-nevekhez és a modulok nevéhez, a parancs nem támogatott. Nem determinisztikus-viselkedéssel rendelkezik arról, hogy melyik erőforrást kell betölteni, ha az adott erőforrás több modulban is megtalálható. Az alábbi parancs hibát okoz a fordítás során.
>
> ```powershell
> Import-DscResource -Name UserConfigProvider*,TestLogger1 -ModuleName UserConfigProv,PsModuleForTestLogger
> ```

Csak a name paraméter használata esetén megfontolandó szempontok:

- Ez egy erőforrás-igényes művelet a gépen telepített modulok számától függően.
- A rendszer betölti a megadott névvel rendelkező első erőforrást. Abban az esetben, ha egynél több azonos nevű erőforrás van telepítve, akkor a hibás erőforrást is betöltheti.

Az ajánlott használatot a paraméterrel kell `-Name` megadni `–ModuleName` az alább leírtak szerint.

Ez a használat a következő előnyökkel jár:

- A megadott erőforrás keresési hatókörének korlátozásával csökkenti a teljesítményre gyakorolt hatást.
- Explicit módon definiálja az erőforrást meghatározó modult, amely biztosítja a megfelelő erőforrás betöltését.

> [!NOTE]
> A PowerShell 5,0-ben a DSC-erőforrások több verzióval is rendelkezhetnek, és a verziók a számítógépen egymás mellett telepíthetők. Ez egy olyan erőforrás-modul több verziójával valósul meg, amely ugyanabban a modul mappában található.
> További információ: [erőforrások használata több verzióval](sxsresource.md).

## <a name="intellisense-with-import-dscresource"></a>IntelliSense importálással – DSCResource

A DSC-konfiguráció ISE-ben történő létrehozásakor a PowerShell IntelliSence biztosít az erőforrásokhoz és az erőforrás-tulajdonságokhoz. A `$pshome` modul elérési útjának erőforrás-definíciói automatikusan betöltődik. Ha a `Import-DSCResource` kulcsszó használatával importál erőforrásokat, a rendszer hozzáadja a megadott erőforrás-definíciókat, az IntelliSense kibontása pedig az importált erőforrás sémájának belefoglalásához.

![Erőforrás IntelliSense](../media/resource-intellisense.png)

> [!NOTE]
> A PowerShell 5,0-től kezdve a TAB befejezését a DSC-erőforrásokhoz és azok tulajdonságaihoz adta hozzá a rendszer. További információ: [erőforrások](../resources/resources.md).

A konfiguráció fordításakor a PowerShell az importált erőforrás-definíciók használatával ellenőrzi a konfigurációban lévő összes erőforrás-blokkot.
Az egyes erőforrás-blokkokat az erőforrás sémájának definíciója alapján érvényesíti a következő szabályokhoz.

- Csak a sémában definiált tulajdonságok használatosak.
- Az egyes tulajdonságok adattípusai helyesek.
- A kulcsok tulajdonságai meg vannak adva.
- A rendszer nem használ írásvédett tulajdonságot.
- Érvényesítés az érték térképek típusain.

Vegye figyelembe a következő konfigurációt:

```powershell
Configuration SchemaValidationInCorrectEnumValue
{
    # It is best practice to explicitly import all resources used in your Configuration.
    # This includes resources that are imported automatically, like WindowsFeature.
    Import-DSCResource -Name WindowsFeature
    Node localhost
    {
        WindowsFeature ROLE1
        {
            Name = “Telnet-Client”
            Ensure = “Invalid”
        }
    }
}
```

A konfiguráció fordítása hibát eredményez.

```output
PSDesiredStateConfiguration\WindowsFeature: At least one of the values ‘Invalid’ is not supported or valid for property ‘Ensure’ on class ‘WindowsFeature’. Please specify only supported values: Present, Absent.
```

Az IntelliSense és a séma érvényesítése lehetővé teszi, hogy több hibát kapjon az elemzési és a fordítási idő során, és elkerülve a szövődmények futási idejét.

> [!NOTE]
> Minden DSC-erőforrás rendelkezhet egy névvel, és az erőforrás sémája által definiált **FriendlyName** is. Az alábbiakban a "MSFT_ServiceResource. shema. MOF" első két sora látható.
> ```syntax
> [ClassVersion("1.0.0"),FriendlyName("Service")]
> class MSFT_ServiceResource : OMI_BaseResource
> ```
> Ha ezt az erőforrást egy konfigurációban használja, megadhatja a **MSFT_ServiceResource** vagy a **szolgáltatást**.

## <a name="powershell-v4-and-v5-differences"></a>PowerShell v4 és V5 különbségek

A PowerShell 4,0-ben és a-ben a konfigurációk létrehozásakor több különbség jelenik meg. PowerShell 5,0 és újabb verziók. Ebben a szakaszban a jelen cikkhez kapcsolódó különbségek láthatók.

### <a name="multiple-resource-versions"></a>Több erőforrás-verzió

A PowerShell 4,0 nem támogatja az erőforrások különböző verzióinak egyoldalas telepítését és használatát. Ha az erőforrások a konfigurációba való importálásával kapcsolatos problémákat tapasztal, győződjön meg arról, hogy az erőforrásnak csak egy verziója van telepítve.

Az alábbi képen a **xPSDesiredStateConfiguration** modul két verziója van telepítve.

![Több erőforrás-verzió javítva](../media/multiple-resource-versions-broken.png)

Másolja a kívánt modul verziójának tartalmát a modul könyvtárának legfelső szintjére.

![Több erőforrás-verzió javítva](../media/multiple-resource-versions-fixed.png)

### <a name="resource-location"></a>Erőforrás helye

Konfigurációk létrehozásakor és fordításakor az erőforrások a [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path)által meghatározott bármely könyvtárban tárolhatók. A PowerShell 4,0-ben a teljes DSC-erőforrás modulokat a "program Files\WindowsPowerShell\Modules" vagy `$pshome\Modules`a (z) alatt kell tárolni. A PowerShell 5,0-es verziójától kezdve ez a követelmény el lett távolítva, és az erőforrás-modulok `PSModulePath`a által meghatározott bármely könyvtárban tárolhatók.

## <a name="see-also"></a>Lásd még:

- [Erőforrások](../resources/resources.md)
