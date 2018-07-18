---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-konfigurációk
ms.openlocfilehash: 171068acb51f44e31c81e63f6640222ef71bee38
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093694"
---
# <a name="dsc-configurations"></a>DSC-konfigurációk

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

DSC-konfigurációk a következők PowerShell-parancsfájlok, amelyek meghatározzák egy speciális típusú függvény.
Konfiguráció megadásához használja a PowerShell kulcsszó **konfigurációs**.

```powershell
Configuration MyDscConfiguration {
    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = 'Present'
            Name = 'RSAT'
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}
MyDscConfiguration
```

Mentse a parancsfájlt egy .ps1 fájlba.

## <a name="configuration-syntax"></a>Konfigurációs szintaxis

A konfigurációs parancsfájlt a következő részekből áll:

- A **konfigurációs** letiltása. Ez az a legkülső parancsfájlblokkban. Segítségével meghatározhatja a **konfigurációs** kulcsszó és a egy nevet. Ebben az esetben a konfiguráció név "MyDscConfiguration".
- Egy vagy több **csomópont** blokkokat. Ezek adják meg a konfigurálni kívánt csomópont (számítógép vagy virtuális gépeken). A fenti konfigurációban van egy **csomópont** egy számítógépet célzó letiltása a "TEST-PC1" nevű.
- Egy vagy több erőforrás blokkokat. Ez az, ahol a konfiguráció az erőforrásokat, konfiguráló tulajdonságainak beállítása. Ebben az esetben két erőforrás blokkok, amelyek a "WindowsFeature" erőforrás hívása vannak.

Belül egy **konfigurációs** letiltása, akkor is végrehajthat, amely általában egy PowerShell-függvény sikerült. Például az előző példában, ha nem szeretné a konfigurációban a célszámítógép nevét keményen code hozzáadhat egy paramétert a csomópont nevét:

```powershell
Configuration MyDscConfiguration {
    param(
        [string[]]$ComputerName='localhost'
    )
    Node $ComputerName {
        WindowsFeature MyFeatureInstance {
            Ensure = 'Present'
            Name = 'RSAT'
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}
MyDscConfiguration -ComputerName $ComputerName
```

Ebben a példában átadásával, megadhatja a csomópont nevét a **ComputerName** konfiguráció fordítása paramétert. A név az alapértelmezett érték "localhost".

## <a name="compiling-the-configuration"></a>A konfiguráció fordítása

A konfiguráció is kihirdeti, mielőtt rendelkezik, hogy a MOF-dokumentumba.
Ehhez a konfigurációs meghívásával, például egy PowerShell függvény akkor hívható meg.
A példában csak a konfiguráció nevét tartalmazó utolsó sora meghívja a konfigurációt.

> [!NOTE]
> Szeretne hívásokat indítani olyan konfiguráció, a függvény kell globális hatókör (csakúgy, mint bármely más PowerShell függvény).
> Meghatározhat, ez történik vagy a "rögzítési művelet" a parancsfájl vagy a konfigurációs parancsprogram futtatásával az F5 billentyűvel, vagy kattintson a a **parancsfájl futtatása** gomb az ISE-ben.
> Pont – forrás a parancsfájlt, futtassa a parancsot `. .\myConfig.ps1` ahol `myConfig.ps1` a parancsfájl, amely tartalmazza a konfiguráció neve.

A konfiguráció, hívja ezt:

- Oldja fel az összes változót
- Létrehoz egy mappát a neve megegyezik a konfiguráció az aktuális könyvtárban található.
- Létrehoz egy fájlt _csomópontnév_.mof az új címtárban, ahol _csomópontnév_ a célcsomópont a konfiguráció neve.
  Ha egynél több csomópont, a MOF-fájlt az egyes csomópontok létrejön.

> [!NOTE]
> A MOF-fájl összes a célcsomópont konfigurációs adatait tartalmazza. Emiatt fontos tárolja biztonságos helyen.
> További információkért lásd: [a MOF-fájl biztonságossá tétele](secureMOF.md).

A fenti eredmények a következő gyökérmappa-szerkezetében lévő első konfiguráció fordítása:

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

Ha a konfigurációs paramétert egy, a második példában látható módon, amely rendelkezik a fordítás során meg kell adni. Itt látható, hogyan néz:

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

## <a name="using-dependson"></a>DependsOn használatával

Egy hasznos DSC kulcsszó **DependsOn**. Általában (bár nem feltétlenül mindig), DSC vonatkozik a sorrendben jelennek meg a konfigurációs belül az erőforrásokat.
Azonban **DependsOn** Megadja, hogy erőforrások más erőforrások függenek, és az LCM Konfigurálása biztosítja, hogy a megfelelő sorrendben, függetlenül az erőforrás-példányok meghatározott sorrendben adják.
Például egy konfigurációs előfordulhat, hogy adja meg, amely egy példányát a **felhasználói** erőforrás függ, hogy létezik-e egy **csoport** példány:

```powershell
Configuration DependsOnExample {
    Node Test-PC1 {
        Group GroupExample {
            Ensure = 'Present'
            GroupName = 'TestGroup'
        }

        User UserExample {
            Ensure = 'Present'
            UserName = 'TestUser'
            FullName = 'TestUser'
            DependsOn = '[Group]GroupExample'
        }
    }
}
```

## <a name="using-new-resources-in-your-configuration"></a>A konfiguráció új erőforrások használata

Ha az előző példák futtatta, talán észrevette, hogy akkor is figyelmezteti, hogy explicit módon importálása nélkül erőforrás használja.
Még ma DSC tartalmaz 12 erőforrás jelenik meg a PSDesiredStateConfiguration modul részeként.
Külső modulok egyéb erőforrásokat kell helyezni `$env:PSModulePath` annak érdekében, hogy ismeri fel az LCM Konfigurálása.
Új parancsmag, [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), annak meghatározására, hogy milyen erőforrásokat telepítve a rendszeren, és használható a LCM által használható.
Ha ezek a modulok lettek helyezve `$env:PSModulePath` és a rendszer megfelelően ismeri fel [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), továbbra is szükségük van, nem tölthető be a konfigurációs belül.
**Az import-DscResource** , amely csak belül felismeri a dinamikus kulcsszó egy **konfigurációs** letiltása (azaz ez még nem parancsmag).
**Az import-DscResource** két paramétereket támogatja:

- **ModuleName** használatának ajánlott módja **Import-DscResource**. A modul (valamint a karakterlánc tömbje modulneveket) importálni erőforrásokat tartalmazó neve fogad el.
- **Név** neve, az erőforrás importálásához. Ez nem a valódi nevet, mint "Name" által visszaadott [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), de az osztály nevét használja, amikor az erőforrás-séma meghatározása (adja vissza a **ResourceType** által [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx)).

## <a name="see-also"></a>Lásd még:

- [Windows PowerShell Desired State Configuration áttekintése](overview.md)
- [DSC-erőforrások](resources.md)
- [A helyi Configuration Manager](metaConfig.md)