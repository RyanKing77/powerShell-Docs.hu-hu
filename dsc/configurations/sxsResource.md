---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Egy adott verzióját egy telepített erőforrás importálása
ms.openlocfilehash: 5ed81e11aa67eb6590d958647f48a33b1b5f1c0e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404148"
---
# <a name="import-a-specific-version-of-an-installed-resource"></a>Egy adott verzióját egy telepített erőforrás importálása

> Érvényes: Windows PowerShell 5.0

A PowerShell 5.0-DSC-erőforrások különböző verzióit egy számítógép egymás mellett telepíthető. Egy resource modul erőforrás külön verziói tárolhat mappák nevű verziója.

## <a name="installing-separate-resource-versions-side-by-side"></a>Külön erőforrást verziók egymás melletti telepítése

Használhatja a **MinimumVersion**, **MaximumVersion**, és **RequiredVersion** paramétereit a [Install-Module](/powershell/module/PowershellGet/Install-Module) parancsmag használatával adja meg melyik verzió modulok telepítéséhez. Hívó **Install-Module** verziót telepíti a legújabb verzió megadása nélkül.

Például, nincsenek különböző verzióinak a **xFailOverCluster** modult, amelyek mindegyike tartalmaz egy **xCluster** erőforrás. Hívó **Install-Module** a verzió megadása nélkül száma a modul legújabb verzióját telepíti.

```powershell
PS> Install-Module xFailOverCluster
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

Egy adott verzióját egy modul telepítéséhez, adja meg egy **RequiredVersion** 1.1.0.0-s az. Ez telepíti a megadott verzióját, a telepített verzió párhuzamosan lesz.

```powershell
PS> Install-Module xFailOverCluster -RequiredVersion 1.1
```

Most meg kell jelennie mindkét modul verziójának használatakor felsorolt `Get-DSCResource`.

```powershell
PS> Get-DscResource xCluster
```

```output
ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a>Erőforrás-verzió megadása az konfiguráció

Ha rendelkezik a számítógépen telepített külön erőforrást verziók, adjon meg a verziót az erőforrás-konfiguráció használatakor. Adjon meg ehhez a **ModuleVersion** paraméterében a **Import-DscResource** kulcsszó. Ha nem adja meg, amelyek egynél több verziója telepítve van egy adott erőforrás erőforrás modul verzióját, a konfigurációs hibát jelez.

A következő konfigurációt mutatja be, adja meg a verziót az erőforrás meghívásához:

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName xFailOverCluster -ModuleVersion 1.1

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

>Megjegyzés: Az Import-DscResource-ModuleVersion paramétert a PowerShell 4.0-s nem érhető el. A PowerShell 4.0-s adjon meg egy modul verziót az Import-DscResource ModuleName paraméterének egy modul specifikáció objektum átadásával. Egy modul specifikáció objektum ModuleName és RequiredVersion kulcsokat tartalmazó kivonattáblát. Például:

```powershell
configuration VersionTest
{
    Import-DscResource -ModuleName (@{ModuleName='xFailOverCluster'; RequiredVersion='1.1'} )

    Node 'localhost'
    {
       xCluster ClusterTest
       {
            Name                          = 'TestCluster'
            StaticIPAddress               = '10.0.0.3'
            DomainAdministratorCredential = Get-Credential
        }
     }
}
```

Ez a PowerShell 5.0 is fog működni, de javasoljuk, hogy használja a **ModuleVersion** paraméter.

## <a name="see-also"></a>Lásd még:

- [DSC-konfigurációk](configurations.md)
- [DSC-erőforrások](../resources/resources.md)
