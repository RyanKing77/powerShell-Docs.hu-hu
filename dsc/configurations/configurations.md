---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-konfigurációk
ms.openlocfilehash: 6af27f442de3080facd65892c713c989d0e388c5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684289"
---
# <a name="dsc-configurations"></a>DSC-konfigurációk

> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

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

Mentse a parancsfájlt, mint egy `.ps1` fájlt.

## <a name="configuration-syntax"></a>Konfigurációs szintaxis

A konfigurációs parancsfájlt a következő részekből áll:

- A **konfigurációs** letiltása. Ez az a legkülső parancsfájlblokkban. Segítségével meghatározhatja a **konfigurációs** kulcsszó és a egy nevet. Ebben az esetben a konfiguráció név "MyDscConfiguration".
- Egy vagy több **csomópont** blokkokat. Ezek adják meg a konfigurálni kívánt csomópont (számítógép vagy virtuális gépeken). A fenti konfigurációban van egy **csomópont** egy számítógépet célzó letiltása a "TEST-PC1" nevű. A csomópont blokk fogadhat több számítógépnevet.
- Egy vagy több erőforrás blokkokat. Ez az, ahol a konfiguráció az erőforrásokat, konfiguráló tulajdonságainak beállítása. Ebben az esetben két erőforrás blokkok, amelyek a "WindowsFeature" erőforrás hívása vannak.

Belül egy **konfigurációs** letiltása, akkor is végrehajthat, amely általában egy PowerShell-függvény sikerült. Például az előző példában, ha nem szeretné a konfigurációban a célszámítógép nevét keményen code hozzáadhat egy paramétert a csomópont nevét:

Ebben a példában átadásával, megadhatja a csomópont nevét a **ComputerName** konfiguráció fordítása paramétert. A név az alapértelmezett érték "localhost".

```powershell
Configuration MyDscConfiguration
{
    param
    (
        [string[]]$ComputerName='localhost'
    )

    Node $ComputerName
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

A **csomópont** blokk is fogadhat több számítógépnevet. A fenti példában, használhatja a `-ComputerName` paraméter vagy számítógépek közvetlenül pass vesszővel elválasztott listáját a **csomópont** letiltása.

```powershell
MyDscConfiguration -ComputerName "localhost", "Server01"
```

A számítógépek listáját megadásakor a **csomópont** letiltása, a konfigurációt, belül kell használnia tömb-jelöléssel.

```powershell
Configuration MyDscConfiguration
{
    Node @('localhost', 'Server01')
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

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
> További információkért lásd: [a MOF-fájl biztonságossá tétele](../pull-server/secureMOF.md).

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

## <a name="using-new-resources-in-your-configuration"></a>A konfiguráció új erőforrások használata

Ha az előző példák futtatta, talán észrevette, hogy akkor is figyelmezteti, hogy explicit módon importálása nélkül erőforrás használja.
Még ma DSC tartalmaz 12 erőforrás jelenik meg a PSDesiredStateConfiguration modul részeként.

A parancsmag [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), annak meghatározására, hogy milyen erőforrásokat telepítve a rendszeren, és használható a LCM által használható.
Ha ezek a modulok lettek helyezve `$env:PSModulePath` és a rendszer megfelelően ismeri fel [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), továbbra is szükségük van, nem tölthető be a konfigurációs belül.

**Az import-DscResource** , amely csak belül felismeri a dinamikus kulcsszó egy **konfigurációs** letiltása, már nem ez a parancsmag.
**Az import-DscResource** két paramétereket támogatja:

- **ModuleName** használatának ajánlott módja **Import-DscResource**. A modul (valamint a karakterlánc tömbje modulneveket) importálni erőforrásokat tartalmazó neve fogad el.
- **Név** neve, az erőforrás importálásához. Ez nem a valódi nevet, mint "Name" által visszaadott [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), de az osztály nevét használja, amikor az erőforrás-séma meghatározása (adja vissza a **ResourceType** által [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)).

További tájékoztatást `Import-DSCResource`, lásd: [Import-DSCResource használatával](import-dscresource.md)

## <a name="powershell-v4-and-v5-differences"></a>PowerShell v4 és 5-ös verziójának különbségek

Ha a DSC-erőforrások kell tárolni a PowerShell 4.0-s különbségek vannak. További információkért lásd: [erőforrás helye](import-dscresource.md#resource-location).

## <a name="see-also"></a>Lásd még:

- [Windows PowerShell Desired State Configuration áttekintése](../overview/overview.md)
- [DSC-erőforrások](../resources/resources.md)
- [A helyi Configuration Manager](../managing-nodes/metaConfig.md)
