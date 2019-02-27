---
title: Egy PowerShell-modul importálása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 697791b3-2135-4a39-b9d7-8566ed67acf2
caps.latest.revision: 13
ms.openlocfilehash: bb5d036e5658c365a4fafa2cac05c0bba9f87019
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845450"
---
# <a name="importing-a-powershell-module"></a>PowerShell-modul importálása

Egyszer a modul telepítve van a rendszeren, valószínűleg érdemes importálja a modult. A folyamat, amely a modul tölt be aktív memória importálása, úgy, hogy egy felhasználó hozzáférhessen a modult a PowerShell-munkamenetben. A PowerShell 2.0, importálhatja egy újonnan telepített PowerShell-modul hívásával [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmagot. A PowerShell 3.0-ban a PowerShell az implicit módon modul importálása, ha egy függvény vagy a modul parancsmagjai hívja meg a felhasználó képes. Vegye figyelembe, hogy mindkét azt feltételezik, hogy egy helyen, ahol PowerShell talált a modul telepítése További információkért lásd: [egy PowerShell-modul telepítése](./installing-a-powershell-module.md). Egy moduljegyzék használatával korlátozhatja a modul mely részei lesznek exportálva, és paramétereket is használhatja a `Import-Module` korlátozhatja, hogy milyen okozzák importált hívás.

## <a name="importing-a-snap-in-powershell-10"></a>Importálás beépülő modult (PowerShell 1.0-s)

Modulokat a PowerShell 1.0 nem létezik: Ehelyett kellett regisztrálása és használata a beépülő modulok. Azonban nem ajánlott ezt a technológiát ezen a ponton használja, a modulok használata általában egyszerűbb, telepítse és importálja. További információkért lásd: [egy Windows PowerShell beépülő modul létrehozása](../cmdlet/how-to-create-a-windows-powershell-snap-in.md).

## <a name="importing-a-module-with-import-module-powershell-20"></a>Az Import-Module (PowerShell 2.0-s) modul importálása

A PowerShell 2.0 használja a megfelelő elnevezett [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmag segítségével importálja a modult. Ez a parancsmag futtatásakor Windows PowerShell keres a megadott modul belül a megadott könyvtárakat a `PSModulePath` változó. Ha a megadott könyvtárban található, Windows PowerShell megkeresi a fájlokat a következő sorrendben: modul jegyzékfájlok (.psd1), parancsfájl-modul fájlok (.psm1), a modul bináris fájlok (.dll). Könyvtárak a keresés történő hozzáadásával kapcsolatos további információkért lásd: [módosítása a PSModulePath telepítési útvonal](./modifying-the-psmodulepath-installation-path.md). A következő kód bemutatja, hogyan modul importálása:

```powershell
Import-Module myModule
```

Feltételezve, hogy myModule volt megtalálható a `PSModulePath`, PowerShell aktív memóriába kellene tölteni myModule. Ha myModule nem található egy `PSModulePath` elérési útja, sikerült továbbra is explicit módon megadhatja a PowerShell, hogy hol található azt:

```powershell
Import-Module -Name C:\myRandomDirectory\myModule -Verbose
```

Is használhatja a - verbose paraméterrel meghatározhatja, mi exportálása folyamatban van a modul ki és mit aktív memóriába hoznak. Is exportál, és importálja a felhasználó számára elérhetővé tett korlátozása: a különbség az, kezelőjét látható-e. A modul kódot alapvetően exportálások szabályozza. Ezzel szemben az import szabályozza a `Import-Module` hívja. További információkért lásd: **korlátozása a tagok, hogy Importálódtak**, az alábbi.

## <a name="implicitly-importing-a-module-powershell-30"></a>Implicit módon importálásával egy modul (PowerShell 3.0-s)

A Windows PowerShell 3.0-es verziótól kezdve rendszer importálja a automatikusan parancsot minden olyan parancsmag vagy a modul függvény való használata során. Ez a funkció működik a modulok egy könyvtárban, amely ez az érték szerepel a **PSModulePath** környezeti változót. Ha nem menti a modul egy érvényes elérési utat azonban, továbbra is betöltheti őket az explicit használatával [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) beállítást, a fent leírt.

A következő műveleteket aktiválhat automatikus importálása modulok, más néven "modul automatikus telepítési."

- Egy parancsmaggal a parancsot. Például `Get-ExecutionPolicy` importálja a Microsoft.PowerShell.Security modult, amely tartalmazza a `Get-ExecutionPolicy` parancsmagot.

- Használatával a [Get-Command](/powershell/module/Microsoft.PowerShell.Core/Get-Command) -parancsmaggal beolvasható a parancsot.  Például `Get-Command Get-JobTrigger` importálja a **PSScheduledJob** modul, amely tartalmazza a `Get-JobTrigger` parancsmagot. A `Get-Command` helyettesítő karaktereket tartalmazó parancs felderítési tekinthető, és nem indítja el a modulok importálása.

- Használatával a [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) parancsmag egy parancsmag súgójának. Például `Get-Help Get-WinEvent` importálja a Microsoft.PowerShell.Diagnostics modult, amely tartalmazza a `Get-WinEvent` parancsmagot.

Támogatja a modulok automatikus importálása a `Get-Command` parancsmag lekéri az összes parancsmag és funkció a minden telepített modulok, még akkor is, ha a modul nincs importálva a munkamenetbe. További információkért tekintse meg a Súgó-témakör a [Get-Command](/powershell/module/Microsoft.PowerShell.Core/Get-Command) parancsmagot.

## <a name="the-importing-process"></a>Az importálás folyamat

Modul importálása során létrejön egy új munkamenet-állapot a modult, és a egy [System.Management.Automation.PSModuleInfo](/dotnet/api/System.Management.Automation.PSModuleInfo) objektum létrehozása a memóriában. Egy munkamenet-állapot jön létre az egyes importált modulok (Ez tartalmazza a a legfelső szintű modul, és minden beágyazott modulok). A tagok a legfelső szintű modul, beleértve azokat a tagokat, a legfelső szintű modul, minden beágyazott modulok által korábban exportált rendszerből kiexportált ezután importálva lesznek a hívónak a munkamenet-állapot.

A metaadatok modul rendszerből kiexportált tagok rendelkezik ModuleName tulajdonságot. Ez a tulajdonság megjelenik az exportált őket a modul neve.

> [!WARNING]
> Ha egy exportált tag nevét használja egy nem jóváhagyott műveletet, vagy ha a tag nevét tiltott karaktereket használ, egy figyelmeztetés jelenik meg ha a [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmagot futtatja.

Alapértelmezés szerint a [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmag nem ad vissza minden objektumot a folyamat. Azonban a parancsmag támogatja a `PassThru` paraméter, amely segítségével adja vissza egy [System.Management.Automation.PSModuleInfo](/dotnet/api/System.Management.Automation.PSModuleInfo) az egyes modulok importált objektum. Elküldheti a kimenetet a gazdagépre, a felhasználók fusson a [Write-Host](/powershell/module/Microsoft.PowerShell.Utility/Write-Host) parancsmagot.

## <a name="restricting--the-members-that-are-imported"></a>A tagok importált korlátozása

A modul az importálás után a [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmagot, alapértelmezésben minden exportált modul tagokat is importálja a munkamenetet, többek között a parancsok exportált a modul egy beágyazott modul által. Alapértelmezés szerint változók és aliasok nem exportálja. Korlátozza a tagok exportált, használja a [moduljegyzék](./how-to-write-a-powershell-module-manifest.md). Ha korlátozni szeretné az importált tagok, a következő paramétereinek használata a `Import-Module` parancsmagot.

- `Function`: Ez a paraméter az exportált funkciók korlátozza. (Ha egy moduljegyzék használja, lásd a FunctionsToExport kulcs.)

- `Cmdlet`: Ez a paraméter korlátozza a parancsmagok exportált (Ha egy modul jegyzékfájl, tekintse meg a CmdletsToExport kulcsot használ.)

- `Variable`: Ez a paraméter korlátozza a változók exportált (Ha egy modul jegyzékfájl, tekintse meg a VariablesToExport kulcsot használ.)

- `Alias`: Ez a paraméter korlátozza az aliasokat exportált (Ha egy modul jegyzékfájl, tekintse meg a AliasesToExport kulcsot használ.)

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-modul írása](./writing-a-windows-powershell-module.md)
