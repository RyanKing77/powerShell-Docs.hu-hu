---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A lekéréses kiszolgálóra konfigurációs azonosítókat (v4 vagy v5) használatával közzététele
ms.openlocfilehash: 0144fec43d7a8d65b79891567cc0dc3952175343
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079506"
---
# <a name="publish-to-a-pull-server-using-configuration-ids-v4v5"></a>A lekéréses kiszolgálóra konfigurációs azonosítókat (v4 vagy v5) használatával közzététele

Az alábbi szakaszok azt feltételezik, hogy Ön már beállított egy lekéréses kiszolgálón. Ha nincs beállítva a lekéréses kiszolgálón, használhatja a következő útmutatókat:

- [DSC SMB-lekérési kiszolgáló beállítása](pullServerSmb.md)
- [A DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md)

Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát. Ebből a cikkből megtudhatja, hogyan tölthet fel erőforrásokat, így elérhetők tölthető le, és konfigurálja az ügyfeleket, automatikusan erőforrások letöltéséhez. Amikor a csomópont kap keresztül egy hozzárendelt konfigurációs **lekéréses** vagy **leküldéses** (v5), automatikusan letölti az konfigurációjában megadott helyen található az LCM Konfigurálása a szükséges erőforrásokat.

## <a name="compile-configurations"></a>Compile Configurations

Az első lépés tárolásához [konfigurációk](../configurations/configurations.md) lekéréses kiszolgálón, hogy ".mof" fájlokba fordítsa őket. Általános, és több ügyfélre vonatkozik, hogy a konfigurációt, használja a `localhost` a csomópont blokkban. Az alábbi példában látható egy konfigurációs shell által használt `localhost` egy adott ügyfél neve helyett.

```powershell
Configuration GenericConfig
{
    Node localhost
    {

    }
}
GenericConfig
```

Az általános konfigurációs van lefordítva, miután rendelkeznie kell egy "localhost.mof" fájlt.

## <a name="renaming-the-mof-file"></a>A MOF-fájl átnevezése

A lekérési kiszolgálón Configuration ".mof" fájlok **ConfigurationName** vagy **ConfigurationID**. Attól függően, hogy mire szeretné a lekérési ügyfél beállítása lehetősége van egy megfelelően nevezze át a lefordított ".mof" fájlokat az alábbi szakaszt.

### <a name="configuration-ids-guid"></a>Konfigurációs azonosítók (GUID)

Nevezze át a "localhost.mof" fájlt kell "<GUID>.mof" fájl. Létrehozhat egy véletlenszerű **Guid** alább, vagy használja a példánál a [új GUID-azonosítója](/powershell/module/microsoft.powershell.utility/new-guid) parancsmagot.

```powershell
[System.Guid]::NewGuid()
```

Kimeneti példa

```output
Guid
----
64856475-939e-41fb-aba5-4469f4006059
```

A ".mof" fájlt bármilyen megfelelő módszerrel majd át lehet nevezni. Az alábbi példa a [Rename-cikk](/powershell/module/microsoft.powershell.management/rename-item) parancsmagot.

```powershell
Rename-Item -Path .\localhost.mof -NewName '64856475-939e-41fb-aba5-4469f4006059.mof'
```

Használatával kapcsolatos további részletekért **GUID** a környezetben, lásd: [GUID tervezése](/powershell/dsc/secureserver#guids).

### <a name="configuration-names"></a>Konfigurációs nevek

Nevezze át a "localhost.mof" fájlt kell "<Configuration Name>.mof" fájl. A következő példában az előző szakaszban a konfiguráció nevét használja. A ".mof" fájlt bármilyen megfelelő módszerrel majd át lehet nevezni. Az alábbi példa a [Rename-cikk](/powershell/module/microsoft.powershell.management/rename-item) parancsmagot.

```powershell
Rename-Item -Path .\localhost.mof -NewName 'GenericConfig.mof'
```

## <a name="create-the-checksum"></a>Az ellenőrzőösszeg létrehozása

Minden egyes ".mof" fájlt tárolja egy lekéréses kiszolgálón, vagy az SMB-megosztás szükség van még egy társított ".checksum" fájl. Ez a fájl lehetővé teszi, hogy az ügyfelek számára, amikor a társított ".mof" fájl módosult, és újra le kell tölteni.

Létrehozhat egy **ellenőrzőösszeg** az a [New-DSCCheckSum](/powershell/module/psdesiredstateconfiguration/new-dscchecksum) parancsmagot. Futtathat `New-DSCCheckSum` ellen a fájlok egy könyvtárat a `-Path` paraméter. Ha már létezik egy ellenőrzőösszeg, kényszerítheti, hogy az újból létrehozza azt a `-Force` paraméter. Az alábbi példa az előző szakaszban a ".mof" fájlt tartalmazó könyvtár megadva, és használja a `-Force` paraméter.

```powershell
New-DscChecksum -Path '.\' -Force
```

Nincs kimenet nem jelenik meg, de meg kell jelennie egy "<GUID or Configuration Name>. mof.checksum" fájl.

## <a name="where-to-store-mof-files-and-checksums"></a>MOF-fájlok és az ellenőrzőösszegeket tárolására

### <a name="on-a-dsc-http-pull-server"></a>On a DSC HTTP Pull Server

Amint azt a HTTP-lekérési kiszolgáló beállításakor [DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md), adja meg a könyvtárakat a **ModulePath** és **ConfigurationPath** kulcsok. A **ConfigurationPath** kulcs azt jelzi, ahol minden ".mof" fájlokat kell tárolni. A **ConfigurationPath** azt jelzi, ahol minden ".mof" és ".checksum" fájlok kell tárolni.

```powershell
    xDscWebService PSDSCPullServer
    {
    ...
        ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
        ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
    ...
    }

```

### <a name="on-an-smb-share"></a>SMB-megosztáson

Lekérési ügyfél SMB-megosztáson használandó beállításakor megadhatja egy **ConfigurationRepositoryShare**. ".Mof" fájlok és a ".checksum" fájlokat kell majd tárolni a **SourcePath** könyvtárat abból a **ConfigurationRepositoryShare** letiltása.

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Pull'
}
```

## <a name="next-steps"></a>Következő lépések

Következő lépésként érdemes lekérni a megadott konfiguráció Pull-ügyfelek konfigurálása. További információkért tekintse meg a következő útmutatókat:

- [Konfigurációs azonosítókat (v4) használatával lekérési ügyfél beállítása](pullClientConfigId4.md)
- [Konfigurációs azonosítókat (v5) használatával lekérési ügyfél beállítása](pullClientConfigId.md)
- [Konfigurációs nevekkel (v5) lekérési ügyfél beállítása](pullClientConfigNames.md)

## <a name="see-also"></a>Lásd még:

- [DSC SMB-lekérési kiszolgáló beállítása](pullServerSmb.md)
- [A DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md)
- [Csomag és a egy lekéréses kiszolgálót erőforrás feltöltése](package-upload-resources.md)
