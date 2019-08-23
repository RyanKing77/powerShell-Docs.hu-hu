---
ms.date: 12/12/2018
keywords: DSC, PowerShell, konfigurálás, beállítás
title: Közzététel a lekérési kiszolgálón konfigurációs azonosítók (v4/V5) használatával
ms.openlocfilehash: c258814f480b91eba75c7ce9abf70c558f1f469e
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986574"
---
# <a name="publish-to-a-pull-server-using-configuration-ids-v4v5"></a>Közzététel a lekérési kiszolgálón konfigurációs azonosítók (v4/V5) használatával

Az alábbi fejezetek feltételezik, hogy már beállított egy lekéréses kiszolgálót. Ha még nem állította be a lekéréses kiszolgálót, az alábbi útmutatók használhatók:

- [DSC SMB-lekérési kiszolgáló beállítása](pullServerSmb.md)
- [DSC HTTP lekérési kiszolgáló beállítása](pullServer.md)

Mindegyik cél csomópont beállítható úgy, hogy a konfigurációkat, erőforrásokat és az állapotukat is letöltsön. Ebből a cikkből megtudhatja, hogyan tölthet fel erőforrásokat, így letöltheti őket, és konfigurálhatja az ügyfeleket az erőforrások automatikus letöltéséhez. Ha a csomópont kap egy hozzárendelt konfigurációt a lekéréses vagy leküldéses (V5) kapcsolaton keresztül, akkor automatikusan letölti a konfiguráció által igényelt erőforrásokat a helyi Configuration Manager (LCD ChipOnGlas) mezőben megadott helyről.

## <a name="compile-configurations"></a>Konfigurációk fordítása

A [konfigurációk](../configurations/configurations.md) egy lekéréses kiszolgálón való tárolásának első lépése a `.mof` fájlokba való fordítás. Ahhoz, hogy egy konfiguráció általános legyen, és több ügyfélre is `localhost` érvényes legyen, használja a csomópont-blokkban. Az alábbi példában egy adott ügyfél neve `localhost` helyett egy konfigurációs rendszerhéj látható.

```powershell
Configuration GenericConfig
{
    Node localhost
    {

    }
}
GenericConfig
```

Miután lefordította az általános konfigurációt, rendelkeznie kell egy `localhost.mof` fájllal.

## <a name="renaming-the-mof-file"></a>A MOF-fájl átnevezése

A konfigurációs `.mof` fájlokat a **ConfigurationName** vagy a **ConfigurationID**használatával tárolhatja egy lekérési kiszolgálón. Attól függően, hogy miként szeretné beállítani a lekéréses ügyfeleket, az alábbi szakaszból választhatja ki a lefordított `.mof` fájlok megfelelő átnevezését.

### <a name="configuration-ids-guid"></a>Konfigurációs azonosítók (GUID)

`localhost.mof` A`<GUID>.mof` fájl átnevezéséhez át kell neveznie a fájlt. Létrehozhat egy véletlenszerű **GUID azonosítót** az alábbi példában vagy a [New-GUID](/powershell/module/microsoft.powershell.utility/new-guid) parancsmag használatával.

```powershell
[System.Guid]::NewGuid()
```

Minta kimenete

```Output
Guid
----
64856475-939e-41fb-aba5-4469f4006059
```

Ezt követően bármely elfogadható módszer `.mof` használatával átnevezheti a fájlt. Az alábbi példa az [Átnevezés-Item](/powershell/module/microsoft.powershell.management/rename-item) parancsmagot használja.

```powershell
Rename-Item -Path .\localhost.mof -NewName '64856475-939e-41fb-aba5-4469f4006059.mof'
```

A **GUID** -azonosítók a környezetben történő használatáról további információt a [következő](/powershell/dsc/secureserver#guids)témakörben talál: guids.

### <a name="configuration-names"></a>Konfigurációs nevek

`localhost.mof` A`<Configuration Name>.mof` fájl átnevezéséhez át kell neveznie a fájlt. A következő példában a rendszer az előző szakasz konfigurációs nevét használja. Ezt követően bármely elfogadható módszer `.mof` használatával átnevezheti a fájlt. Az alábbi példa az [Átnevezés-Item](/powershell/module/microsoft.powershell.management/rename-item) parancsmagot használja.

```powershell
Rename-Item -Path .\localhost.mof -NewName 'GenericConfig.mof'
```

## <a name="create-the-checksum"></a>Az ellenőrzőösszeg létrehozása

A lekéréses kiszolgálón tárolt `.checksum` fájloknak,vagyazSMB-megosztásnakhozzákellrendelnieegytársítottfájlt.`.mof`
Ez a fájl lehetővé teszi, hogy az `.mof` ügyfelek tudják, mikor módosult a társított fájl, és újra le kell tölteni.

A [New-DSCCheckSum](/powershell/module/psdesiredstateconfiguration/new-dscchecksum) parancsmaggal létrehozhat egy **ellenőrzőösszeget** . `New-DSCCheckSum` A`-Path` paraméter használatával a fájlok könyvtára is futtatható.
Ha egy ellenőrzőösszeg már létezik, akkor kényszerítheti, hogy újra létrehozza a `-Force` paraméterrel. A következő példa egy könyvtárat adott meg, `.mof` amely az előző szakaszban található fájlt tartalmazza, és `-Force` a paramétert használja.

```powershell
New-DscChecksum -Path '.\' -Force
```

A rendszer nem jelenít meg kimenetet, de most egy `<GUID or Configuration Name>.mof.checksum` fájlt kell látnia.

## <a name="where-to-store-mof-files-and-checksums"></a>A MOF-fájlok és-ellenőrzőösszegek tárolása

### <a name="on-a-dsc-http-pull-server"></a>DSC HTTP lekéréses kiszolgálón

A HTTP lekéréses kiszolgáló beállításakor a [DSC http lekérési kiszolgáló beállítása](pullServer.md)című részben leírtaknak megfelelően meg kell adnia a **ModulePath** és a **ConfigurationPath** kulcsokhoz tartozó címtárakat. A **ModulePath** kulcs azt jelzi, hogy hol kell `.zip` tárolni a modul csomagolt fájljait. A **ConfigurationPath** jelzi, hogy `.mof` hol kell `.checksum` tárolni a fájlokat és a fájlokat.

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

Ha a lekéréses ügyfelet SMB-megosztás használatára állítja be, akkor meg kell adnia egy **ConfigurationRepositoryShare**.
Az `.mof` összes fájlt `.checksum` és fájlt a **ConfigurationRepositoryShare** blokkból kell tárolni a **SourcePath** könyvtárban.

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Pull'
}
```

## <a name="next-steps"></a>További lépések

Ezután konfigurálnia kell a lekéréses ügyfeleket a megadott konfiguráció lekéréséhez. További információkért lásd az alábbi útmutatók egyikét:

- [Lekérési ügyfél beállítása konfigurációs azonosítók (v4) használatával](pullClientConfigId4.md)
- [Lekérési ügyfél beállítása konfigurációs azonosítók (V5) használatával](pullClientConfigId.md)
- [Lekérési ügyfél beállítása konfigurációs nevek (V5) használatával](pullClientConfigNames.md)

## <a name="see-also"></a>Lásd még:

- [DSC SMB-lekérési kiszolgáló beállítása](pullServerSmb.md)
- [DSC HTTP lekérési kiszolgáló beállítása](pullServer.md)
- [Erőforrások becsomagolása és feltöltése egy lekérési kiszolgálóra](package-upload-resources.md)
