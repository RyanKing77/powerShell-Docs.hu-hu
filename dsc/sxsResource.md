---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Eltérő verziójú erőforrások használata
ms.openlocfilehash: 9e5b989be3f33fb9151f76cecb6d5f700b1e36c9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="using-resources-with-multiple-versions"></a>Eltérő verziójú erőforrások használata

> Vonatkozik: A Windows PowerShell 5.0

PowerShell 5.0-s DSC erőforrások több verziója is van, és verziók is telepíthető egy számítógép-mellé. Ez történik, azzal, hogy egy erőforrás-modul több verziója modul azonos mappában találhatók.

## <a name="installing-multiple-resource-versions-side-by-side"></a>Több erőforrás verziók-párhuzamos telepítése

Használhatja a **MinimumVersion**, **MaximumVersion**, és **RequiredVersion** paraméterei a [Install-modul](https://technet.microsoft.com/library/dn807162.aspx) parancsmag használatával adja meg a modul telepítése melyik verzióját. Hívása **Install-modul** egy verziót telepíti a legújabb verziót megadása nélkül.

Például több verziója van a **xFailOverCluster** modult tartalmaz, amelyek mindegyike egy **xCluster** kívánt erőforrás. A hívás eredménye **Install-modul** nélkül a verzió megadása számot a következőképpen történik:

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, ...
```

Most, ha meghívja a **Install-modul** ebben az esetben adja meg, de egy **RequiredVersion** 1.1.0.0-s, az azt eredményezi, a következő:

```powershell
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Install-Module xFailOverCluster -RequiredVersion 1.1
C:\Program Files\WindowsPowerShell\Modules\xFailOverCluster> Get-DscResource xCluster

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      xCluster                  xFailOverCluster               1.1        {DomainAdministratorCredential, Name, ...
PowerShell      xCluster                  xFailOverCluster               1.2.0.0    {DomainAdministratorCredential, Name, ...
```

## <a name="specifying-a-resource-version-in-a-configuration"></a>Adja meg egy erőforrás-verziója konfigurációban

Ha egy számítógépen több erőforrást, konfiguráció használatakor meg kell adnia az adott erőforrás verziója. Ehhez adja meg a **ModuleVersion** paramétere a **Import-DscResource** kulcsszó. Ha nem adja meg egy erőforrás-modul egy erőforrást, amelyek több verziója telepítve van a verziója, a konfigurációs hibát generál.

A következő konfigurációs adja meg az erőforrás hívására verzióját mutatja be:

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

>Megjegyzés: Az Import-DscResource ModuleVersion paramétere nem érhető el a PowerShell 4.0. A PowerShell 4.0-s adjon meg egy modul verziót úgy, hogy egy modul specification objektum importálási-DscResource ModuleName paraméterének. A modul specification objektum egy kivonattáblát a modulnév és RequiredVersion kulcsot tartalmazó. Például:

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

Ez is PowerShell 5.0 fog működni, de javasoljuk, hogy használja a **ModuleVersion** paraméter.

## <a name="see-also"></a>Lásd még:
* [A DSC-konfigurációk](configurations.md)
* [A DSC-erőforrások](resources.md)