---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfiguráció, a szolgáltatás, a telepítő
title: Írási, fordítsa le és a konfiguráció alkalmazása
ms.openlocfilehash: fa4d98fd12202439ba7025fd8af3fa398653ca05
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404183"
---
> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

# <a name="write-compile-and-apply-a-configuration"></a>Írási, fordítsa le és a konfiguráció alkalmazása

Ebben a gyakorlatban létrehozásával és alkalmazásával a Desired State Configuration (DSC) konfigurációs elejétől a végéig ismerteti.
A következő példában, megtudhatja, hogyan írhat, és a egy nagyon egyszerű konfiguráció alkalmazása. A konfiguráció biztosítja, hogy a "HelloWorld.txt" fájl létezik a helyi gépen. Ha a fájl törléséhez DSC létrehozza azt a következő alkalommal, amikor frissíti.

DSC és működésének áttekintését lásd: [Desired State Configuration áttekintése fejlesztők számára](../overview/overview.md).

## <a name="requirements"></a>Követelmények

Ez a példa futtatásához szüksége lesz a futtató PowerShell 4.0-s vagy újabb.

## <a name="write-the-configuration"></a>A konfiguráció írása

A DSC [konfigurációs](configurations.md) egy külön PowerShell-függvény, amely meghatározza, hogyan szeretné konfigurálni egy vagy több cél számítógépek (csomópontok).

A PowerShell ISE-ben, vagy más PowerShell-szerkesztő írja be a következőt:

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

Mentse a fájlt "HelloWorld.ps1".

Konfiguráció definiálása olyan, mint egy függvény meghatározása. A **csomópont** letiltása, adja meg a célcsomópont konfigurálását, ebben az esetben `localhost`.

A konfiguráció meghívja az egyiket [erőforrások](../resources/resources.md), a `File` erőforrás. Erőforrások teheti meg, hiszen a munkát, a célcsomópont a konfiguráció által meghatározott állapotban van.

## <a name="compile-the-configuration"></a>A konfiguráció fordítása

DSC csomópont alkalmazandó konfiguráció azt először kell összeállítani egy MOF-fájlba.
A konfiguráció, például egy függvényt, futtató lefordítása fog egy ".mof" fájl által definiált minden csomópont esetében a `Node` letiltása.
Futtassa a konfigurációt, kell *pont forrás* a "HelloWorld.ps1" parancsfájlt az aktuális hatókörben.
További információkért lásd: [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts?view=powershell-6#script-scope-and-dot-sourcing).

*Pont forrás* az elérési út helyétől, után írja be a "HelloWorld.ps1" parancsfájl a `. ` (pont, terület). A következő lehetőségekkel, majd futtassa a konfiguráció például függvény meghívásával.

```powershell
. C:\Scripts\WebsiteTest.ps1
HelloWolrd
```

Ez létrehozza a következő kimenet:

```output
Directory: C:\Scripts\HelloWorld


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

## <a name="apply-the-configuration"></a>A konfiguráció alkalmazásához

Most, hogy a lefordított MOF, alkalmazhat a konfigurációt a célcsomópont (ebben az esetben az a helyi számítógép) meghívásával a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.

A `Start-DscConfiguration` arra utasítja a parancsmag a [helyi Configuration Manager (LCM) Konfigurálása](../managing-nodes/metaConfig.md), DSC, a alkalmazni a konfigurációt motorját.
Az LCM Konfigurálása a alkalmazni a konfigurációt a DSC-erőforrások hívása működik.

Az alábbi kód használatával hajtsa végre a `Start-DSCConfiguration` parancsmagot. Adja meg a könyvtár elérési útja a "localhost.mof" tárolódnak, a `-Path` paraméter. A `Start-DSCConfiguration` parancsmag átvizsgálja a megadott "\<computername\>.mof" fájlokat. A `Start-DSCConfiguration` parancsmag megkísérli minden ".mof" fájlt megtalálta a alkalmazni a számítógépnév, a fájlnév ("localhost", "kiszolgalo01", "tartományvezérlő-02", stb.) által meghatározott.

> [!NOTE]
> Ha a `-Wait` paraméter nincs megadva, `Start-DSCConfiguration` létrehoz egy háttérben futó feladatot, a művelet végrehajtásához. Adja meg a `-Verbose` paraméter lehetővé teszi, hogy tekintse meg a **részletes** a művelet kimenetét. `-Wait`, és `-Verbose` mindkét opcionális paraméterek.

```powershell
Start-DscConfiguration -Path C:\Scripts\HelloWorld -Verbose -Wait
```

## <a name="test-the-configuration"></a>A konfiguráció tesztelése

Miután a `Start-DSCConfiguration` parancsmag befejeződött, megjelenik egy "HelloWorld.txt" fájlt a megadott helyen. A tartalmak ellenőrizheti a [Get-tartalom](/powershell/module/microsoft.powershell.management/get-content) parancsmagot.

Emellett *tesztelése* az aktuális állapot használatával [a Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration).

A kimenet lehet "True", ha a csomópont jelenleg felel meg az alkalmazott konfiguráció.

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

## <a name="re-applying-the-configuration"></a>A beállítások újbóli alkalmazásával

A konfiguráció újra alkalmazva megtekintéséhez, eltávolíthatja a hozta létre a konfigurációs szövegfájlban. A használatát a `Start-DSCConfiguration` parancsmagot a `-UseExisting` paraméter. A `-UseExisting` paraméter utasítja `Start-DSCConfiguration` újból a alkalmazni az "current.mof" fájlt, amely jelöli a legutóbb sikeresen alkalmazott konfigurációs.

```powershell
Remove-Item -Path C:\Temp\HelloWorld.txt
```

## <a name="next-steps"></a>További lépések

- További információk a DSC-konfigurációk [DSC-konfigurációk](configurations.md).
- Megtudhatja, milyen DSC-erőforrás áll rendelkezésre, és hogyan hozhat létre egyéni DSC-erőforrásokat, [DSC-erőforrások](../resources/resources.md).
- DSC-konfigurációkat és erőforrásokat a [PowerShell-galériából](https://www.powershellgallery.com/).
