---
ms.date: 12/12/2018
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az Import-DSCResource használata
ms.openlocfilehash: f22c741969b1429074e7307a00a5c014cf563089
ms.sourcegitcommit: 6ae5b50a4b3ffcd649de1525c3ce6f15d3669082
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/14/2019
ms.locfileid: "56265501"
---
# <a name="using-import-dscresource"></a>Az Import-DSCResource használata

`Import-DScResource` a dinamikus kulcsszóval, amely csak akkor használható egy konfigurációs parancsfájl-blokkon belül van. A `Import-DSCResource` kulcsszó importálásához a konfiguráció szükséges erőforrásokat. Alatt lévő erőforrások `$phsome` importálása automatikusan történik, de továbbra is ajánlott eljárás, explicit módon a használt összes erőforrások importálása a [konfigurációs](Configurations.md).

A szintaxisának `Import-DSCResource` alább láthatók.  Amikor modulok megadása név szerint, nem követelmény a listában minden új sorba.

```syntax
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName>]
```

|Paraméter  |Leírás  |
|---------|---------|
|`-Name`|A DSC erőforrás neve, amely importálnia kell. Ha a modul neve meg van adva, a parancs keresi ezeket DSC erőforrások Ez a modul; Ellenkező esetben a parancs a DSC-erőforrás görbékhez keres a DSC-erőforrások. Helyettesítő karakterek használata támogatott.|
|`-ModuleName`|A modul neve, vagy modul megadását.  Modul importálása erőforrásokat ad meg, ha a parancs megpróbálja importálása csak azokat az erőforrásokat. Csak a modul adja meg, ha a parancs importálására a modul DSC-erőforrások.|

```powershell
Import-DscResource -ModuleName xActiveDirectory;
```

## <a name="example-use-import-dscresource-within-a-configuration"></a>Példa: Import-DSCResource használható konfiguráció

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
> Több értéket erőforrás és modulok nevének megadása a ugyanezt a parancsot nem támogatottak. Nem determinisztikus jelenség melyik erőforrást kell, hogy melyik modul betöltése, abban az esetben, ha ugyanaz az erőforrás létezik-e több modulban kapcsolatos rendelkezhet. Alább parancs eredményez hiba történik a fordítás során.
>
> ```powershell
> Import-DscResource -Name UserConfigProvider*,TestLogger1 -ModuleName UserConfigProv,PsModuleForTestLogger
> ```

Csak a Name paraméter használata esetén vegye figyelembe a következőkre:

- Egy erőforrás-igényes művelet, attól függően, hogy a számítógépen telepített modulok száma is.
- Az első erőforrás található a megadott nevű betölti azt. Abban az esetben, ahol egynél több erőforrás azonos nevű telepítve van, a megfelelő erőforrás tudott betölteni.

Az ajánlott használati, ha `–ModuleName` rendelkező a `-Name` paramétert, az alábbiaknak megfelelően.

A használati rendelkezik a következő előnyöket biztosítja:

- A megadott erőforrás keresési hatókör korlátozásával csökkenti a teljesítményre gyakorolt hatást.
- Explicit módon meghatározza a modult, amely meghatározza az erőforrás, biztosítva, hogy a helyes erőforrás be van töltve.

> [!NOTE]
> PowerShell 5.0-s DSC erőforrások több verziója is van, és verziók is telepíthető egy számítógép-mellé. Ez történik, azzal, hogy egy erőforrás-modul több verziója modul azonos mappában találhatók.
> További információkért lásd: [erőforrásokat használó többféle verzióját tartalmazó](sxsresource.md).

## <a name="intellisense-with-import-dscresource"></a>Az Import-DSCResource IntelliSense

A DSC-konfiguráció ISE készítésekor PowerShell biztosít erőforrásokat és erőforrás-tulajdonságok IntelliSence. Az erőforrás-definíciókban a `$pshome` modul elérési útján automatikusan be vannak töltve. Ha importál eszközzel a `Import-DSCResource` kulcsszóval, a megadott erőforrás-definíciókban is hozzáadja, és az Intellisense tartalmazza az importált erőforrás-séma ki van bontva.

![Erőforrás Intellisense](/media/resource-intellisense.png)

> [!NOTE]
> PowerShell 5.0 verziótól kezdve kiegészítést lett felvéve a ISE DSC-erőforrások és azok tulajdonságait. További információkért lásd: [erőforrások](../resources/resources.md).

A konfigurációs összeállításakor PowerShell erőforrás blokkok a konfiguráció érvényesítéséhez használja az importált erőforrás-definíciókban.
Minden erőforrás blokk van hitelesítve, az erőforrás-schema definíció, a következő szabályok segítségével.

- Csak a sémában definiált tulajdonságok használhatók.
- Az adattípusok mindegyik tulajdonság megfelelőek-e.
- Kulcsok tulajdonságok vannak megadva.
- Nem csak olvasható tulajdonságot használja.
- Érték ellenőrzése típusok képezi le.

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

Fordítási hiba történt a konfigurációs eredményez.

```output
PSDesiredStateConfiguration\WindowsFeature: At least one of the values ‘Invalid’ is not supported or valid for property ‘Ensure’ on class ‘WindowsFeature’. Please specify only supported values: Present, Absent.
```

IntelliSense és a séma érvényesítése elkerülése futási időben elemzési és fordítási idő alatt további hibák catch teszik lehetővé.

> [!NOTE]
> Az egyes DSC erőforrások rendelkezhet egy névvel, és egy **FriendlyName** az erőforrás-séma határozza meg. Az alábbiakban az első két sort "MSFT_ServiceResource.shema.mof".
> ```syntax
> [ClassVersion("1.0.0"),FriendlyName("Service")]
> class MSFT_ServiceResource : OMI_BaseResource
> ```
> Ehhez az erőforráshoz konfiguráció használatakor is megadhat **MSFT_ServiceResource** vagy **szolgáltatás**.

## <a name="powershell-v4-and-v5-differences"></a>PowerShell v4 és v5 különbségek

Tekintse meg a PowerShell 4.0 vs konfigurációk készítésekor több különbségek vannak. PowerShell 5.0-s és újabb verziók. Ez a szakasz a különbségek ki, hogy megjelenik ez a cikk vonatkozik.

### <a name="multiple-resource-versions"></a>Több erőforrás-verzió

Telepítéséről és használatáról a különböző verzióinak egymás melletti erőforrások az PowerShell 4.0 nem támogatott. Erőforrások importálja a konfigurációs problémákat észlel, győződjön meg arról, hogy csak egy verziója van telepítve az erőforrás.

Az alábbi két ábrán a **xPSDesiredStateConfiguration** modul telepítve vannak.

![Rögzített több erőforrás-verzió](/media/multiple-resource-versions-broken.md)

A legfelső szintű modulkönyvtárat másolja a tartalmát a kívánt modul verziója.

![Rögzített több erőforrás-verzió](/media/multiple-resource-versions-fixed.md)

### <a name="resource-location"></a>Erőforrás helye

Jelentéskészítő és -konfigurációk fordítása, ha az erőforrások bármely által megadott könyvtárban tárolható a [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path). A PowerShell 4.0 a LCM igényel "Program Files\WindowsPowerShell\Modules" a rendszer ne tárolja az összes DSC erőforrás modul vagy `$pshome\Modules`. PowerShell 5.0 verziótól kezdve ez a követelmény el lett távolítva, és erőforrás-modulok bármely által megadott könyvtárban tárolható `PSModulePath`.

## <a name="see-also"></a>Lásd még:

- [Erőforrások](../resources/resources.md)
