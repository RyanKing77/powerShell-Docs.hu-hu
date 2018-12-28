---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A DSC használata a Nano Serveren
ms.openlocfilehash: fd81fe56d16100f45d9ee2dfd8fdc303c2a6c17a
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404237"
---
# <a name="using-dsc-on-nano-server"></a>A DSC használata a Nano Serveren

> Érvényes: Windows PowerShell 5.0

**A Nano Serveren DSC** a választható csomag létezik a `NanoServer\Packages` mappájában, a Windows Server 2016 adathordozójáról. A csomag létrehozásakor egy virtuális Merevlemezt a Nano Server megadásával telepíthető **Microsoft-NanoServer-DSC-Package** értékeként a **csomagok** paraméterében a **New-NanoServerImage**  függvény. Ha például egy virtuális Merevlemezt a virtuális gép létrehozásakor, a parancs lenne a következőhöz hasonló:

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

További információ a telepítése és használata a Nano Serveren, valamint a PowerShell-táveléréssel a Nano Server kezelése: [Ismerkedés a Nano Serverrel](/windows-server/get-started/getting-started-with-nano-server).

## <a name="dsc-features-available-on-nano-server"></a>DSC-funkciók érhető el a Nano Serveren

Mivel a Nano Server támogatja a Windows Server teljes verzióját képest API-k csak korlátozott számú, DSC, a Nano Serveren nem rendelkezik teljes funkciói egyenértékűek teljes Termékváltozatai jelenleg futó DSC. A Nano Serveren a DSC szolgáltatás aktív fejlesztés alatt áll, és még nem teljes funkció.

A következő DSC-funkciók érhetők el jelenleg a Nano Serveren:

Leküldéses és lekéréses módok

- Minden DSC-parancsmagok a teljes verzióját a Windows Server, beleértve a következőket:
- [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager)
- [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager)
- [Enable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug)
- [Disable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug)
- [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration)
- [Stop-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Stop-DscConfiguration)
- [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration)
- [Test-DscConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)
- [Publish-DscConfiguraiton](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration)
- [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration)
- [Restore-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Restore-DscConfiguration)
- [Remove-DscConfigurationDocument](/powershell/module/PSDesiredStateConfiguration/Remove-DscConfigurationDocument)
- [Get-DscConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus)
- [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource)
- [Find-DscResource](https://technet.microsoft.com/en-us/library/mt517874.aspx)
- [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)
- [Új DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum)

- Konfiguráció fordítása (lásd: [DSC-konfigurációk](../configurations/configurations.md))

  **A probléma leírása:** Jelszó titkosítása (lásd: [a MOF-fájl biztonságossá tétele](../pull-server/secureMOF.md)) konfigurálása során összeállítása nem működik.

- Metaconfigurations összeállítása (lásd: [a Local Configuration Manager](../managing-nodes/metaConfig.md))

- Egy erőforrás felhasználó környezetében fut (lásd: [DSC futtatása felhasználói hitelesítő adatokkal (RunAs)](../configurations/runAsUser.md))

- Osztályalapú erőforrások (lásd: [PowerShell-osztályokkal egyéni DSC-erőforrás írása](../resources/authoringResourceClass.md))

- DSC-erőforrások hibakeresés (lásd: [hibakeresés DSC-erőforrások](../troubleshooting/debugResource.md))

  **A probléma leírása:** Nem működik, ha egy erőforrás PsDscRunAsCredential használ (lásd: [DSC futtatása felhasználói hitelesítő adatokkal](../configurations/runAsUser.md))

- [Csomópontok közötti függőségek megadása](../configurations/crossNodeDependencies.md)

- [Erőforrás-verziókezelés](../configurations/sxsResource.md)

- Lekérési ügyfél (konfigurációk és erőforrások) (lásd: [konfigurációs nevek lekérési ügyfél beállítása](../pull-server/pullClientConfigNames.md))

- [Részleges konfigurációk (lekéréses & leküldéses)](../pull-server/partialConfigs.md)

- [A jelentéskészítés lekéréses kiszolgálón](../pull-server/reportServer.md)

- MOF-titkosítás

- Eseménynaplózás

- Az Azure Automation DSC jelentési

- Erőforrások, amelyek teljes körűen használható

- **Archívum**
- **Környezet**
- **Fájl**
- **Log**
- **ProcessSet**
- **Registry**
- **Parancsfájl**
- **WindowsPackageCab**
- **WindowsProcess**
- **WaitForAll** (lásd: [csomópontok közötti függőségek megadása](../configurations/crossNodeDependencies.md))
- **WaitForAny** (lásd: [csomópontok közötti függőségek megadása](../configurations/crossNodeDependencies.md))
- **WaitForSome** (lásd: [csomópontok közötti függőségek megadása](../configurations/crossNodeDependencies.md))

- Erőforrások, amelyek részben működési
- **Csoport**
- **GroupSet**

  **A probléma leírása:** Erőforrások felett sikertelen, ha az adott példány volat dvakrát (ugyanaz a konfiguráció kétszer fut)

- **Service**
- **ServiceSet**

  **A probléma leírása:** Csak akkor működik, a (állapot) szolgáltatás indítása/leállítása. Nem sikerül, ha az egyik megpróbálja módosítani a más szolgáltatás-attribútumok indítási típusa, a hitelesítő adatokat, a leírás stb... A hiba lépett fel hasonlít:

  *[Management.managementobject] típus nem található: Győződjön meg arról, hogy ez a típus tartalmazó szerelvény be töltve.*

- Erőforrások, amelyek nem működik
- **Felhasználó**

## <a name="dsc-features-not-available-on-nano-server"></a>DSC-funkciók nem érhető el a Nano Serveren

A következő DSC-funkciók nem érhetők el jelenleg a Nano Serveren:

- Egy titkosított MOF dokumentum visszafejtése
- Lekérési kiszolgáló –, jelenleg nem állíthat egy lekéréses kiszolgálót a Nano Serveren
- Bármi, amely nem szerepel a listában, a szolgáltatás működése

## <a name="using-custom-dsc-resources-on-nano-server"></a>Egyéni DSC-erőforrások használata a Nano Serveren

Korlátozott csoportok Windows API-k és a CLR-beli kódtárak érhető el a Nano Serveren, mert DSC-erőforrások, amelyek működnek a Windows teljes CLR verziója nem feltétlenül működik a Nano Serveren.
Fejezze be a teljes körű tesztelés éles környezetben olyan egyéni DSC-erőforrások üzembe helyezése előtt.

## <a name="see-also"></a>Lásd még:

- [Ismerkedés a Nano Serverrel](/windows-server/get-started/getting-started-with-nano-server)
