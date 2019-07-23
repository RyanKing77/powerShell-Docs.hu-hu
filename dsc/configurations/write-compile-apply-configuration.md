---
ms.date: 12/12/2018
keywords: DSC, PowerShell, konfigurálás, szolgáltatás, beállítás
title: Konfiguráció írása, fordítása és alkalmazása
ms.openlocfilehash: 8bcd55518b0409b9a4b02ca95f027a0a77eb5300
ms.sourcegitcommit: 118eb294d5a84a772e6449d42a9d9324e18ef6b9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/22/2019
ms.locfileid: "68372177"
---
> Érvényes: Windows PowerShell 4,0, Windows PowerShell 5,0

# <a name="write-compile-and-apply-a-configuration"></a>Konfiguráció írása, fordítása és alkalmazása

Ez a gyakorlat végigvezeti a kívánt állapot-konfiguráció (DSC) konfigurációjának a kezdéstől a befejezésig történő létrehozásán és alkalmazásán.
Az alábbi példában megtudhatja, hogyan írhat és alkalmazhat egy nagyon egyszerű konfigurációt. A konfiguráció biztosítja, hogy a "HelloWorld. txt" fájl létezik a helyi gépen. Ha törli a fájlt, a DSC a következő frissítésekor újra létrehozza azt.

A DSC és annak működésének áttekintését lásd: [a fejlesztők számára a kívánt állapot konfigurációjának áttekintése](../overview/overview.md).

## <a name="requirements"></a>Követelmények

A példa futtatásához a PowerShell 4,0-es vagy újabb verzióját futtató számítógépre lesz szüksége.

## <a name="write-the-configuration"></a>A konfiguráció megírása

A DSC- [konfiguráció](configurations.md) egy speciális PowerShell-függvény, amely meghatározza, hogyan szeretné konfigurálni egy vagy több célszámítógépet (csomópontot).

A PowerShell ISE vagy más PowerShell-szerkesztőben írja be a következőt:

```powershell
Configuration HelloWorld {

    # Import the module that contains the File resource.
    Import-DscResource -ModuleName PsDesiredStateConfiguration

    # The Node statement specifies which targets to compile MOF files for, when this configuration is executed.
    Node 'localhost' {

        # The File resource can ensure the state of files, or copy them from a source to a destination with persistent updates.
        File HelloWorld {
            DestinationPath = "C:\Temp\HelloWorld.txt"
            Ensure = "Present"
            Contents   = "Hello World from DSC!"
        }
    }
}
```

> ! Fontos olyan speciális forgatókönyvekben, ahol több modult kell importálni, hogy ugyanabban a konfigurációban több DSC-erőforrással is működjön, ügyeljen arra, hogy minden modult külön sorba helyezzen `Import-DscResource`a használatával.
> Ez könnyebben karbantartható a verziókövetés és a szükséges, ha a DSC-t az Azure-beli állapot konfigurációjában kell megtartani.
>
> ```powershell
>  Configuration HelloWorld {
>
>   # Import the module that contains the File resource.
>   Import-DscResource -ModuleName PsDesiredStateConfiguration
>   Import-DscResource -ModuleName xWebAdministration
>
> ```

Mentse a fájlt "HelloWorld. ps1" néven.

A konfiguráció definiálása hasonló a függvények definiálásához. A **csomópont** -blokk meghatározza a konfigurálni kívánt célként megadott csomópontot, ebben `localhost`az esetben.

A [konfiguráció egy](../resources/resources.md)erőforrást, az `File` erőforrást hívja meg. Az erőforrások feladata annak biztosítása, hogy a cél csomópont a konfiguráció által meghatározott állapotban legyen.

## <a name="compile-the-configuration"></a>A konfiguráció fordítása

Ahhoz, hogy egy DSC-konfigurációt egy csomóponton lehessen alkalmazni, először egy MOF-fájlba kell lefordítani.
A konfiguráció, például egy függvény futtatása lefordít egy ". MOF" fájlt a `Node` blokk által meghatározott összes csomóponthoz.
A konfiguráció futtatásához a "HelloWorld. ps1" parancsfájlt az aktuális hatókörbe kell *leadnia* .
További információ: [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts?view=powershell-6#script-scope-and-dot-sourcing).

<!-- markdownlint-disable MD038 -->
*Adja meg* a "HelloWorld. ps1" parancsfájlt úgy, hogy beírja azt az elérési utat, `. ` ahol a tárolta, a (pont, szóköz) után. Ezután futtathatja a konfigurációt úgy, hogy a függvényt hívja meg.
<!-- markdownlint-enable MD038 -->

```powershell
. C:\Scripts\HelloWorld.ps1
HelloWorld
```

Ez a következő kimenetet hozza létre:

```output
Directory: C:\Scripts\HelloWorld


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

## <a name="apply-the-configuration"></a>A konfiguráció alkalmazása

Most, hogy már rendelkezik a lefordított MOF-vel, a konfigurációt alkalmazhatja a cél csomópontra (ebben az esetben a helyi számítógépre) a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmag meghívásával.

A `Start-DscConfiguration` parancsmag a konfiguráció alkalmazásához megadja a [helyi Configuration Manager (LCD ChipOnGlas)](../managing-nodes/metaConfig.md), a DSC motorját.
Az LCD-eszközök meghívja a DSC-erőforrásokat a konfiguráció alkalmazásához.

Az alábbi kód használatával hajtsa végre `Start-DSCConfiguration` a parancsmagot. Adja meg a könyvtár elérési útját, ahol a "localhost. MOF `-Path` " a paraméterre van tárolva. A `Start-DSCConfiguration` parancsmag a "\<számítógépnév\>. MOF" fájlokhoz megadott könyvtárat vizsgálja. A `Start-DSCConfiguration` parancsmag megpróbálja alkalmazni az összes olyan ". MOF" fájlt, amely a fájlnévben ("localhost", "kiszolgalo01", "DC-02" stb.) megadott számítógépnévre hivatkozik.

> [!NOTE]
> Ha a `-Wait` paraméter nincs megadva, `Start-DSCConfiguration` a létrehoz egy háttér-feladatot a művelet végrehajtásához. A `-Verbose` paraméter megadásával megtekintheti a művelet **részletes** kimenetét. `-Wait`a és `-Verbose` a választható paraméterek is.

```powershell
Start-DscConfiguration -Path C:\Scripts\HelloWorld -Verbose -Wait
```

## <a name="test-the-configuration"></a>A konfiguráció tesztelése

A `Start-DSCConfiguration` parancsmag befejezését követően egy "HelloWorld. txt" fájlt kell látnia a megadott helyen. A tartalmat a [Get-Content](/powershell/module/microsoft.powershell.management/get-content) parancsmaggal ellenőrizheti.

Tesztelheti az *aktuális* állapotot a [test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)használatával is.

Ha a csomópont jelenleg megfelel az alkalmazott konfigurációnak, a kimenetnek "true" értékűnek kell lennie.

```powershell
Test-DSCConfiguration
```

```output
True
```

```powershell
Get-Content -Path C:\Temp\HelloWorld.txt
```

```output
Hello World from DSC!
```

## <a name="re-applying-the-configuration"></a>A konfiguráció újbóli alkalmazása

A konfiguráció ismételt alkalmazásának megtekintéséhez eltávolíthatja a konfiguráció által létrehozott szövegfájlt. A használja `Start-DSCConfiguration` a parancsmagot a `-UseExisting` paraméterrel. A `-UseExisting` paraméter `Start-DSCConfiguration` arra utasítja, hogy újra alkalmazza a "current. MOF" fájlt, amely a legutóbb sikeresen alkalmazott konfigurációt jelképezi.

```powershell
Remove-Item -Path C:\Temp\HelloWorld.txt
```

## <a name="next-steps"></a>További lépések

- Tudjon meg többet a DSC-konfigurációkról a [DSC](configurations.md)-konfigurációknál.
- Ismerje meg, hogy milyen DSC-erőforrások érhetők el, és hogyan hozhat létre egyéni DSC-erőforrásokat a [DSC](../resources/resources.md)-erőforrásokon.
- Keresse meg a DSC-konfigurációkat és-erőforrásokat a [PowerShell-Galéria](https://www.powershellgallery.com/).
