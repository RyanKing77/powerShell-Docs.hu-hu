---
ms.date: 10/16/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Konfigurációk életbe léptetése
ms.openlocfilehash: 4a6e7e511446ab27307683ad3d5676391e7c791c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404495"
---
# <a name="enacting-configurations"></a>Konfigurációk életbe léptetése

>Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A PowerShell Desired State Configuration (DSC) konfigurációk kihirdeti két módja van: leküldéses és lekéréses módot.

## <a name="push-mode"></a>Leküldéses módban

![Leküldéses módban](../images/pushModel.png "leküldés üzemmód működése")

Leküldéses módban a felhasználó aktívan alkalmazása egy konfigurációs egy célcsomóponttal meghívásával hivatkozik a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) parancsmagot.

Miután létrehozta és fordításáról, akkor is kihirdeti, leküldéses módban meghívásával a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) beállítást, a parancsmag a - Path paraméterrel, a parancsmagot, amely a konfigurációs MOF elérési útját.
Például, ha a konfigurációs MOF a következő helyen található `C:\DSC\Configurations\localhost.mof`, a következő paranccsal a helyi számítógépen szeretné alkalmazni: `Start-DscConfiguration -Path 'C:\DSC\Configurations'`

> __Megjegyzés:__: Alapértelmezés szerint DSC háttérfeladatként futtatja a konfigurációt. A konfiguráció interaktívan, hívja meg a [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) az a __-várjon__ paraméter.

## <a name="pull-mode"></a>Lekérési mód

![Lekérési mód](../images/pullModel.png "lekéréses üzemmód működése")

Lekérési mód lekéréses ügyfelek szolgáltatásból való beolvasására a kívánt állapotban konfigurációját egy távoli lekéréses vannak konfigurálva.
Hasonlóképpen a lekéréses szolgáltatás be lett állítva a gazdagépen a DSC szolgáltatás, és kiépítette a konfigurációk és a pull-ügyfelek által igényelt forrásokat.
A pull-ügyfelek mindegyike rendelkezik, amely a rendszeres megfelelőségét ellenőrzi a konfigurációt a csomópont, ütemezett esemény.
Az esemény első alkalommal aktiválódik, ha a helyi Configuration Manager (LCM) Konfigurálása a leküldéses ügyfél kérést küld a lekéréses szolgáltatásával a szükséges az LCM Konfigurálása a megadott konfiguráció.
Ez a konfiguráció a lekéréses szolgáltatás létezik, és átadja a kezdeti érvényesség-ellenőrzések, a konfigurációs van letölti a lekérési ügyfél, ahol majd következő(k) az LCM Konfigurálása.

Az LCM ellenőrzi, hogy az ügyfél által megadott rendszeres időközönként a konfiguráció megfelel a **ConfigurationModeFrequencyMins** az LCM tulajdonságát.
Az LCM Konfigurálása a lekérési szolgáltatást a frissített konfiguráció által meghatározott időközönként ellenőrzi a **RefreshModeFrequency** az LCM tulajdonságát.
Az LCM konfigurálásával kapcsolatos további információkért lásd: [a Local Configuration Manager](../managing-nodes/metaConfig.md).

Az ajánlott megoldás egy lekéréses szolgáltatás üzemeltetéséhez a DSC-felhőszolgáltatás, [Azure Automation](https://azure.microsoft.com/services/automation/).
Ez üzemeltetett megoldás a grafikus felügyeleti, a jelentéseket és a központi felügyeletet biztosít.

A Windows Server lekéréses szolgáltatás beállításának további információkért lásd: [DSC lekérési kiszolgáló beállítása](pullServer.md).
Azonban, ismerje meg, hogy ez a megvalósítás csak korlátozott funkciókat, és néhány "mindezt saját maga" integrációt igényelnek.

Az alábbi témakörök ismertetik a lekérési szolgáltatást és az ügyfelek számára:

- [Az Azure Automation DSC – áttekintés](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
- [Az SMB-lekérési kiszolgálójának beállítása](pullServerSMB.md)
- [Lekérési ügyfél beállítása](pullClientConfigID.md)
