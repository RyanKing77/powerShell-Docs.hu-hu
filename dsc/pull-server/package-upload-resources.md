---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Csomag és a egy lekéréses kiszolgálót erőforrás feltöltése
ms.openlocfilehash: 29a62f96393a53c9e7da57a5e51732dcb0937194
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404171"
---
# <a name="package-and-upload-resources-to-a-pull-server"></a>Csomag és a egy lekéréses kiszolgálót erőforrás feltöltése

Az alábbi szakaszok azt feltételezik, hogy Ön már beállított egy lekéréses kiszolgálón. Ha nincs beállítva a lekéréses kiszolgálón, használhatja a következő útmutatókat:

- [DSC SMB-lekérési kiszolgáló beállítása](pullServerSmb.md)
- [A DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md)

Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát. Ebből a cikkből megtudhatja, hogyan tölthet fel erőforrásokat, így elérhetők tölthető le, és konfigurálja az ügyfeleket, automatikusan erőforrások letöltéséhez. Amikor a csomópont kap keresztül egy hozzárendelt konfigurációs **lekéréses** vagy **leküldéses** (v5), automatikusan letölti az konfigurációjában megadott helyen található az LCM Konfigurálása a szükséges erőforrásokat.

## <a name="package-resource-modules"></a>Package erőforrás modulok

Az egyes erőforrások letöltéséhez ügyfél érhető el egy ".zip" fájlban kell tárolni. Az alábbi példa jelennek meg a szükséges lépéseket, használja a [xPSDesiredStateConfiguration](https://www.powershellgallery.com/packages/xPSDesiredStateConfiguration/8.4.0.0) erőforrás.

> [!NOTE]
> Ha bármely PowerShell 4.0-t használó ügyfelek, az erőforrás mappastruktúra flaten kell, és bármely verziója mappák eltávolítása. További információkért lásd: [több erőforrás verzió](../configurations/import-dscresource.md#multiple-resource-versions).

Az erőforrás-könyvtár használatával minden olyan segédprogram, szkript vagy metódushoz, amely igény szerint képes tömöríteni. A Windows, *kattintson a jobb gombbal* a "xPSDesiredStateConfiguration" könyvtárat, és válassza a "Küldés", majd a "Tömörített mappa".

![Kattintson a jobb gombbal](../media/right-click.gif)

### <a name="naming-the-resource-archive"></a>Az erőforrás-archívum elnevezése

Az erőforrás-archívum neve a következő formátumban kell:

```
{ModuleName}_{Version}.zip
```

A fenti példában a "xPSDesiredStateConfiguration.zip" átnevezve "xPSDesiredStateConfiguration_8.4.4.0.zip" kell lennie.

### <a name="create-checksums"></a>Hozzon létre az ellenőrzőösszegek

Az erőforrás-modul tömörített, és a átnevezve, kell hoznia egy **ellenőrzőösszeg**.  A **ellenőrzőösszeg** használja, az LCM Konfigurálása az ügyfél határozza meg, ha az erőforrás módosítva lett, és újra le kell tölteni. Létrehozhat egy **ellenőrzőösszeg** az a [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) parancsmag, az alábbi példában látható módon.

```powershell
New-DscChecksum -Path .\xPSDesiredStateConfiguration_8.4.4.0.zip
```

Nem lehet jelenik meg semmilyen kimenet, de meg kell jelennie egy "xPSDesiredStateConfiguration_8.4.4.0.zip.checksum". Futtathat `New-DSCCheckSum` ellen a fájlok egy könyvtárat a `-Path` paraméter. Ha már létezik egy ellenőrzőösszeg, kényszerítheti, hogy az újból létrehozza azt a `-Force` paraméter.

### <a name="where-to-store-resource-archives"></a>Erőforrás-archívumok tárolására

#### <a name="on-a-dsc-http-pull-server"></a>A DSC HTTP lekéréses kiszolgálón

Amint azt a HTTP-lekérési kiszolgáló beállításakor [DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md), adja meg a könyvtárakat a **ModulePath** és **ConfigurationPath** kulcsok. A **ConfigurationPath** kulcs azt jelzi, ahol minden ".mof" fájlokat kell tárolni. A **ModulePath** azt jelzi, ahol minden DSC-erőforrás modulokat kell tárolni.

```powershell
    xDscWebService PSDSCPullServer
    {
    ...
        ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
        ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
    ...
    }

```

#### <a name="on-an-smb-share"></a>SMB-megosztáson

Ha megadott egy **ResourceRepositoryShare**, ha a lekérési ügyfél beállítása archívumok és az ellenőrzőösszegeket tárolja a **SourcePath** könyvtárat abból a **ResourceRepositoryShare** letiltása.

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Configurations'
}

ResourceRepositoryShare SMBResourceServer
{
    SourcePath = '\\SMBPullServer\Resources'
}
```

Ha csak egy **ConfigurationRepositoryShare**, ha a lekérési ügyfél beállítása archívumok és az ellenőrzőösszegeket tárolja a **SourcePath** könyvtárat abból a  **ConfigurationRepositoryShare** letiltása.

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Pull'
}
```

#### <a name="updating-resources"></a>Erőforrások frissítése

Kényszerítheti, hogy az erőforrások frissítése, a verziószámot az archívum neve módosításával, vagy hozzon létre egy új ellenőrzőösszeg csomópont. A Pull-ügyfél ellenőrzi, hogy a szükséges erőforrások újabb verzióját, valamint ellenőrzőösszegekkel, frissül, amikor frissíti az LCM Konfigurálása.

## <a name="see-also"></a>Lásd még:

- [DSC SMB-lekérési kiszolgáló beállítása](pullServerSmb.md)
- [A DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md)
