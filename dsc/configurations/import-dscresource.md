---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az Import-DSCResource használatával
ms.openlocfilehash: 6bc3c1aa1d34a05e3188666da825322235c0672e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404289"
---
# <a name="using-import-dscresource"></a>Az Import-DSCResource használatával

`Import-DScResource` van egy dinamikus kulcsszóval, amely csak egy konfigurációs parancsfájl-blokkon belül használható. A `Import-DSCResource` kulcsszó használatával importálja a konfigurációt a szükséges erőforrásokat. Alatt lévő erőforrások `$phsome` importálása automatikusan történik, de továbbra is ajánlott explicit módon importálja az összes erőforrás használatban a [konfigurációs](Configurations.md).

A szintaxist a `Import-DSCResource` alább találja.

```syntax
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>]
```

|Paraméter  |Leírás  |
|---------|---------|
|`-Name`|A DSC erőforrás neve, amely importálnia kell. Ha a modul neve van megadva, a parancs megkeresi ezen DSC-erőforrások belül ez a modul; Ellenkező esetben a parancs a DSC-erőforrások keresés minden DSC-erőforrás elérési utat. A helyettesítő karakterek használata támogatott.|
|`-ModuleName`|Container modul neve, vagy a modul előírásokat.  Erőforrások importálása a modul adja meg, ha a parancs megpróbál importálása csak azokat az erőforrásokat. Ha csak a modul adja meg, a parancs importálja a modult a DSC-erőforrások.|

A helyettesítő karaktereket is használhat a `-Name` paraméter használatakor `Import-DSCResource`.

```powershell
Import-DscResource -Name * -ModuleName xActiveDirectory;
```

## <a name="example-use-import-dscresource-within-a-configuration"></a>Példa: Az Import-DSCResource használja a konfiguráció belül

```powershell
Configuration MSDSCConfiguration
{
    # Search for and imports Service, File, and Registry from the module PSDesiredStateConfiguration.
    Import-DSCResource -ModuleName MS_DSC1 -name Service, File, Registry

    # Search for and import Resource1 from the module that defines it.
    # If only –Name parameter is used then resources can belong to different PowerShell modules as well.
    # TimeZone resource is from the ComputerManagementDSC module which is not installed by default.
    Import-DSCResource -Name File, TimeZone

    # Search for and import all DSC resources inside the module PSDesiredStateConfiguration.
    Import-DSCResource -ModuleName PSDesiredStateConfiguration
...
```

> [!NOTE]
> Több érték erőforrás és modulok nevének megadása a ugyanazt a parancsot nem támogatottak. Lehet, hogy a nem determinisztikus viselkedés kapcsolatos melyik erőforrást kell betölteni a modul, abban az esetben, ha ugyanazon az erőforráson több modul megtalálható. Alább parancs hibát eredményez a fordítás közben.
>
> ```powershell
> Import-DscResource -Name UserConfigProvider*,TestLogger1 -ModuleName UserConfigProv,PsModuleForTestLogger
> ```

Csak a Name paraméter használatakor figyelembe kell dolgot:

- Egy erőforrás-igényes művelet gépen telepített modul számától függően.
- Az első erőforrás található a megadott nevű betölti azt. Abban az esetben, ahol egynél több erőforrás azonos nevű telepítve van, akkor sikerült betölteni a helytelen erőforrás.

A javasolt felhasználás az, hogy adja meg `–ModuleName` együtt a `-Name` paramétert, az alábbiakban leírtak szerint.

A szintaxis a következő előnyökkel jár:

- Csökkenti a teljesítményre gyakorolt hatás, a keresés hatókörét, a megadott erőforrás korlátozza.
- Explicit módon a modult, amely meghatározza az erőforrást, biztosítva a megfelelő erőforrás betöltött határozza meg.

> [!NOTE]
> A PowerShell 5.0-s DSC-erőforrásokat több verziója is rendelkezik, és verziók egy számítógép egymás mellett telepíthető. Ez valósul meg kellene resource modul több verzióját, a modul mappájában található.
> További információkért lásd: [eltérő verziójú erőforrások használata](sxsresource.md).

## <a name="intellisense-with-import-dscresource"></a>Az Import-DSCResource az IntelliSense

Szerzői műveletek a DSC-konfiguráció ISE-ben, ha a PowerShell IntelliSence biztosít az erőforrások és erőforrás-tulajdonságok. Erőforrás-definíciók alapján a `$pshome` modul elérési útja automatikusan töltődnek be. Erőforrások importálásakor a `Import-DSCResource` kulcsszó, az adott erőforrás-definíciókban hozzáadja, és az Intellisense tartalmazza az importált erőforrás-séma ki van bontva.

![Erőforrás Intellisense](/media/resource-intellisense.png)

> [!NOTE]
> A PowerShell 5.0-es verziótól kezdve kiegészítés hozzáadva a DSC-erőforrások és a hozzájuk tartozó tulajdonságok ISE-ben. További információkért lásd: [erőforrások](../resources/resources.md).

A konfiguráció összeállításakor PowerShell ellenőrzése a konfiguráció az összes erőforrás blokkokat használja az importált erőforrás-definíciókban.
Minden erőforrás blokk érvényesítve, az erőforrás sémadefiníciót, használja a következő szabályokat.

- Csak a sémában definiált tulajdonságok szolgálnak.
- Az adattípusok minden egyes tulajdonság megfelelőek-e.
- Kulcsok tulajdonságok vannak megadva.
- Nem csak olvasható tulajdonság használható.
- A maps-típusok érvényesítése értéknek.

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

Hiba történt a konfiguráció eredményez fordítása.

```output
PSDesiredStateConfiguration\WindowsFeature: At least one of the values ‘Invalid’ is not supported or valid for property ‘Ensure’ on class ‘WindowsFeature’. Please specify only supported values: Present, Absent.
```

Az IntelliSense és a séma érvényesítése elkerülése futási időben elemzési és fordítási idő alatt további hibák észlelését teszi lehetővé.

> [!NOTE]
> Az egyes DSC-erőforrások is rendelkezik egy névvel, és a egy **FriendlyName** az erőforrás-séma határozza meg. Az alábbiakban "MSFT_ServiceResource.shema.mof" első két sorát.
> ```syntax
> [ClassVersion("1.0.0"),FriendlyName("Service")]
> class MSFT_ServiceResource : OMI_BaseResource
> ```
> Az erőforrás-konfiguráció használatakor megadhatja **MSFT_ServiceResource** vagy **szolgáltatás**.

## <a name="powershell-v4-and-v5-differences"></a>PowerShell v4 és 5-ös verziójának különbségek

Amikor a jelentéskészítési konfigurációk a PowerShell 4.0 VS-ben több különbségek vannak. A PowerShell 5.0-s és újabb verziók. Ez a szakasz kiemeli a különbségeket, hogy megjelenik-e ez a cikk a.

### <a name="multiple-resource-versions"></a>Több erőforrás-verzió

Különböző verzióinak egymás melletti erőforrások telepítéséről és a PowerShell 4.0-s nem támogatott. Ha azt tapasztalja, erőforrások importálása a konfigurációs problémákat, győződjön meg arról, hogy csak egy verziója van telepítve az erőforrás.

A két verziója az alábbi képen a **xPSDesiredStateConfiguration** modulnak vannak telepítve.

![Rögzített több erőforrás-verzió](/media/multiple-resource-versions-broken.md)

Másolja a tartalmát a kívánt modul verzióját a legfelső szintű modulkönyvtárat.

![Rögzített több erőforrás-verzió](/media/multiple-resource-versions-fixed.md)

### <a name="resource-location"></a>Erőforrás helye

Amikor szerzői és konfigurációk fordítása, az erőforrások bármely által megadott könyvtárban tárolható a [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path). A PowerShell 4.0-s, az LCM Konfigurálása szükséges minden DSC-erőforrás modulok "Program Files\WindowsPowerShell\Modules" alapján kell tárolni, vagy `$pshome\Modules`. A PowerShell 5.0-es verziótól kezdve ez a követelmény el lett távolítva, és az erőforrás-modulokat bármilyen által megadott könyvtárban tárolható `PSModulePath`.

## <a name="see-also"></a>Lásd még:

- [Erőforrások](../resources/resources.md)
