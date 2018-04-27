---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-konfigurációk
ms.openlocfilehash: ffeb953048c0a65352618d2ab141ee10ead4c663
ms.sourcegitcommit: a9aa5e8d0fab0cbb3e4e6cff0e3ca8c0339ab4e6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/27/2018
---
# <a name="dsc-configurations"></a>A DSC-konfigurációk

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A DSC-konfigurációk olyan PowerShell-parancsfájlok, amelyek meghatározzák a függvény futásakor.
A konfiguráció megadásához használja a PowerShell kulcsszó **konfigurációs**.

```powershell
Configuration MyDscConfiguration {

    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
MyDscConfiguration

```

Mentse a parancsfájlt egy .ps1 fájlba.

## <a name="configuration-syntax"></a>Konfigurációs szintaxis

Egy konfigurációs parancsfájl a következő részből áll:

- A **konfigurációs** blokkot. Ez egy, a legkülső parancsprogram-blokkot tartalmazzon. Segítségével meghatározhatja a **konfigurációs** kulcsszó és megadása. Ebben az esetben a konfiguráció neve nem "MyDscConfiguration".
- Egy vagy több **csomópont** blokkolja. Ezek határozzák meg a konfigurálni kívánt csomópontok (számítógépek és virtuális gépeken). A fenti konfigurációban van egy **csomópont** blokkot, amelynek célpontja a számítógép neve a "TEST-PC1".
- Egy vagy több erőforrás-címblokkokat. Ez azért, ahol a konfigurációt az erőforrásokat, amelyek azt konfigurálja tulajdonságainak beállítása. Ebben az esetben két erőforrás-blokk, a "WindowsFeature" erőforrás hívható, amelyek nincsenek.

Belül egy **konfigurációs** blokk, akkor is végrehajthat, amelyek általában egy PowerShell-függvény sikertelen. Például az előző példában, ha nem szeretné a nevét, a konfigurációban, a célszámítógép merevlemez code hozzáadhat egy paraméter, a csomópont neve:

```powershell
Configuration MyDscConfiguration {

    param(
        [string[]]$ComputerName="localhost"
    )
    Node $ComputerName {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
MyDscConfiguration -ComputerName $ComputerName

```

Ebben a példában, akkor adja meg a csomópont neve úgy, hogy azt a **számítógépnév** paramétert, ha a konfiguráció fordítása. A név az alapértelmezett érték "localhost".

## <a name="compiling-the-configuration"></a>A konfiguráció fordítása

Egy konfigurációs is kihirdeti, mielőtt, hogy a MOF-dokumentumba van.
Ehhez a konfigurációs hívja, például akkor hívja meg a PowerShell függvényt.
A példában csak a konfiguráció nevét tartalmazó utolsó sora meghívja a konfiguráció.

>**Megjegyzés:** hívni egy konfigurációt, a függvény hatókörében kell lennie globális (úgy, mint bármely más PowerShell függvény).
>A hiba akkor fordulhat elő vagy az "rögzítési" a parancsfájlt, hogy vagy a konfigurációs parancsfájl futtatásával F5 használatával, vagy kattintson a a **-parancsfájl futtatása** az ISE gombjára.
>A parancsfájl pont-forrás, futtassa a parancsot `. .\myConfig.ps1` ahol `myConfig.ps1` a parancsfájlt, amely tartalmazza a konfiguráció neve.

A konfigurációs hívásakor azt:

- Oldja fel az összes változó
- Létrejön egy mappa neve megegyezik a konfiguráció az aktuális könyvtár.
- Létrehoz egy nevű fájlt _csomópontnév_.mof új könyvtárban, ahol _csomópontnév_ a célcsomópont a konfiguráció neve.
    Ha egynél több csomópont, a MOF-fájlt az egyes csomópontok létrejön.

>**Megjegyzés:**: A MOF-fájl tartalmazza az összes célcsomóponton vonatkozó konfigurációs adatokat. Ezért fontos biztonságának megőrzése.
>További információkért lásd: [biztonságossá tétele a MOF-fájlt](secureMOF.md).

A következő gyökérmappa-szerkezetében lévő eredmények felett első konfiguráció fordítása:

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       10/23/2015   4:32 PM           2842 localhost.mof
```

Ha a konfigurációs paramétert egy, a második példában látható módon, amelynek meg kell adni a fordítás során. Hogyan lenne, amely itt található:

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration -ComputerName 'MyTestNode'
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----       10/23/2015   4:32 PM           2842 MyTestNode.mof
```

## <a name="using-dependson"></a>DependsOn tulajdonság használatával

A hasznos DSC kulcsszót **DependsOn**. Általában (azonban nem feltétlenül mindig), DSC alkalmazza a megjelenési sorrendjükben belül a konfigurációs lévő erőforrásokat.
Azonban **DependsOn** Megadja, hogy erőforrások más erőforrások függenek, és a LCM biztosítja, hogy lesznek alkalmazva a megfelelő sorrendben, függetlenül attól, amelyben az erőforrások példányok meghatározásának sorrendje.
Például egy konfigurációban előfordulhat, hogy adja meg, amely egy példányát a **felhasználói** erőforrás létezik-e függ a **csoport** példány:

```powershell
Configuration DependsOnExample {
    Node Test-PC1 {
        Group GroupExample {
            Ensure = "Present"
            GroupName = "TestGroup"
        }

        User UserExample {
            Ensure = "Present"
            UserName = "TestUser"
            FullName = "TestUser"
            DependsOn = "[Group]GroupExample"
        }
    }
}

```

## <a name="using-new-resources-in-your-configuration"></a>A konfiguráció új erőforrások használata

Ha az előző példákban futtatta, akkor előfordulhat, hogy észrevette, hogy akkor is figyelmezteti, hogy egy erőforrás használta explicit importálása nélkül.
A DSC ma, 12-erőforrásokkal érhető el, a PSDesiredStateConfiguration modulja részét.
Egyéb erőforrások külső modulban kell helyezni `$env:PSModulePath` ahhoz, hogy ismeri fel a LCM.
Egy új parancsmagot [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), annak meghatározására, hogy milyen erőforrásokat telepítve a rendszeren, és használható a LCM által használható.
Ha ezek a modulok lettek helyezve `$env:PSModulePath` megfelelően ismeri fel és [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), betöltését belül a konfigurációs továbbra is szükséges.
**Import-DscResource** belül csak érzékelt dinamikus kulcsszó egy **konfigurációs** blokk (azaz nincs parancsmag).
**Importálás – DscResource** két paramétereket támogatja:
- **Modulnév** használatának ajánlott módja **Import-DscResource**. A modul, amely tartalmazza az erőforrásokat, importálandók (valamint a karakterlánc tömbje modulneveket) neve fogad.
- **Név** neve, az erőforrás importálásához. Ez nem a rövid név, mint a "Name" által visszaadott [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), de az osztály nevét, ha használt meghatározása az erőforrás-séma (adja vissza a **ResourceType** által [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx)).

## <a name="see-also"></a>Lásd még:
* [A Windows PowerShell célállapot-konfiguráló áttekintése](overview.md)
* [A DSC-erőforrások](resources.md)
* [A helyi Configuration Manager konfigurálása](metaConfig.md)
