---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC használata a Nano Serveren
ms.openlocfilehash: 9e26c525b48e8656a3479db9c0a760eaeb8cf58a
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="using-dsc-on-nano-server"></a>A DSC használata a Nano Serveren

> Vonatkozik: A Windows PowerShell 5.0

**A Nano Server DSC** egy választható csomag van a `NanoServer\Packages` a Windows Server 2016 adathordozó mappájában. A csomag létrehozásakor a virtuális merevlemez a Nano Server megadásával telepítésének **Microsoft-NanoServer-DSC-csomag** értékeként a **csomagok** paramétere a **új-NanoServerImage**  függvény. Például ha egy virtuális gép virtuális hoz létre, a parancs volna a következőhöz hasonló:

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

További információ a telepítéséről és használatáról a Nano Server, valamint kezelése a PowerShell távelérése a Nano Server: [Ismerkedés a Nano Server](https://technet.microsoft.com/library/mt126167.aspx).


## <a name="dsc-features-available-on-nano-server"></a>A DSC szolgáltatás Nano Server

 Mivel a Nano Server támogatja a Windows Server teljes verzióját képest API-kat csak korlátozott számú, a Nano Server DSC nem rendelkezik teljes funkciói egyenértékűek teljes termékváltozatok jelenleg futó DSC. A Nano Server DSC aktív fejlesztés, és még nincs kész szolgáltatás.

 A következő DSC-funkciók érhetők el jelenleg a Nano Server:


* Mind eseménylekérési és eseményküldési módban

* Minden DSC-parancsmag a teljes verzióját a Windows Server, beleértve a következőket:
  * [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx)
  * [Set-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn521621.aspx)
  * [Enable-DscDebug](https://technet.microsoft.com/en-us/library/mt517870.aspx)
  * [Disable-DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx)
  * [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx)
  * [Stop-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143542.aspx)
  * [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx)
  * [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx)
  * [Publish-DscConfiguraiton](https://technet.microsoft.com/en-us/library/mt517875.aspx)
  * [Update-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541.aspx)
  * [Restore-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407383.aspx)
  * [Remove-DscConfigurationDocument](https://technet.microsoft.com/en-us/library/mt143544.aspx)
  * [Get-DscConfigurationStatus](https://technet.microsoft.com/en-us/library/mt517868.aspx)
  * [Invoke-DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx)
  * [Keresés – DscResource](https://technet.microsoft.com/en-us/library/mt517874.aspx)
  * [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)
  * [Új DscChecksum](https://technet.microsoft.com/en-us/library/dn521622.aspx)

* Konfiguráció fordítása (lásd: [a DSC-konfigurációk](configurations.md))

  **Probléma:** jelszó-titkosítási (lásd: [biztonságossá tétele a MOF-fájlt](securemof.md)) konfigurálása során fordítás nem működik.

* Metaconfigurations fordítása (lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md))

* Egy erőforrás felhasználó környezetében futó (lásd: [DSC futtató felhasználó hitelesítő adataival (RunAs)](runAsUser.md))

* Az osztály-alapú erőforrások (lásd: [PowerShell osztályokra egyéni DSC-erőforrás írása](authoringResourceClass.md))

* A DSC-erőforrások hibakeresés (lásd: [hibakeresés DSC erőforrások](debugresource.md))

  **Probléma:** nem működik, ha egy erőforrás PsDscRunAsCredential használ (lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md))

* [Csomópontok közötti függőségek megadása](crossNodeDependencies.md)

* [Erőforrás versioning](sxsResource.md)

* Lekéréses ügyfél (konfigurációk és erőforrások) (lásd: [ügyféltelepítéshez lekéréses konfigurációs nevek használatával](pullClientConfigNames.md))

* [Részleges konfigurációk (lekéréses & leküldéses)](partialConfigs.md)

* [A lekérési kiszolgálójával Reporting](reportServer.md)

* MOF-titkosítás

* Események naplózása

* Azure Automation DSC-jelentés

* Teljes körűen működőképes erőforrások
  * [Archív](archiveResource.md)
  * [Környezet](environmentResource.md)
  * [Fájl](fileResource.md)
  * [Log](logResource.md)
  * ProcessSet
  * [Registry](registryResource.md)
  * [Parancsfájl](scriptResource.md)
  * WindowsPackageCab
  * [WindowsProcess](windowsProcessResource.md)
  * WaitForAll (lásd: [cross-csomópont függőségek megadását](crossNodeDependencies.md))
  * WaitForAny (lásd: [cross-csomópont függőségek megadását](crossNodeDependencies.md))
  * WaitForSome (lásd: [cross-csomópont függőségek megadását](crossNodeDependencies.md))

* Részlegesen működési erőforrásokhoz
  * [Csoport](groupResource.md)
  * GroupSet

  **Probléma:** felett erőforrást sikertelen, ha a példány neve kétszer (kétszer azonos konfigurációval fut)

  * [Service](serviceResource.md)
  * ServiceSet

  **Probléma:** csak akkor működik, a (állapot): a szolgáltatás indítása/leállítása. Nem sikerül, ha egy próbál módosítani más szolgáltatás tulajdonságai, például a startuptype, a hitelesítő adatokat, a leírás stb... A hiba lépett fel hasonlít:

  *[Management.managementobject] típus nem található: Győződjön meg arról, hogy a típust tartalmazó szerelvény be töltve.*

* Erőforrások, amelyek nem működik
  * [Felhasználó](userResource.md)


## <a name="dsc-features-not-available-on-nano-server"></a>A DSC-szolgáltatások Nano Server rendszeren nem érhető el

A következő DSC-szolgáltatások nem érhetők el jelenleg a Nano Server:

* MOF dokumentum titkosított egy visszafejtése
* Lekérési kiszolgálójával--nem jelenleg állítható be a lekérési kiszolgálón Nano
* Mindent, ami nem funkció akkor működik a listájában

## <a name="using-custom-dsc-resources-on-nano-server"></a>Egyéni DSC-erőforrások Nano Server segítségével

Windows API-k és a CLR-könyvtárak érhető el a Nano Server korlátozott készleteinek miatt a teljes CLR-verzió Windows működő DSC erőforrások feltétlenül működik a Nano Server.
Fejezze be a végpontok közötti tesztelése előtt DSC egyéni erőforrások telepítése éles környezetben.

## <a name="see-also"></a>Lásd még:
- [Ismerkedés a Nano Server](https://technet.microsoft.com/library/mt126167.aspx)