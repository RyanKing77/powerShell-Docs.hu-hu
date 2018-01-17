---
ms.date: 2017-10-16
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Életbe konfigurációk"
ms.openlocfilehash: 4285dbe04c9745ec2a859e479848da2881c18de0
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="enacting-configurations"></a>Életbe konfigurációk

>Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) konfigurációk kihirdeti két módja van: leküldéses és lekéréses módot.

## <a name="push-mode"></a>Leküldéses mód

![Leküldéses módot](images/pushModel.png "leküldés üzemmód működése")

Leküldéses módban a felhasználó aktívan alkalmazása egy konfigurációs egy célcsomóponttal meghívásával hivatkozik a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) parancsmag.

Miután létrehozta, és a konfiguráció fordítása, akkor is kihirdeti azt leküldéses módban meghívásával a [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) beállítása, a parancsmag a - Path paramétert a konfigurációs MOF elérési útját a parancsmag.
Például, ha a konfiguráció MOF itt található: `C:\DSC\Configurations\localhost.mof`, volna vonatkoznak a helyi gép a következő paranccsal:`Start-DscConfiguration -Path 'C:\DSC\Configurations'`

> __Megjegyzés:__: DSC alapértelmezés szerint egy konfigurációs fut háttérfeladatként. Interaktív módon futtassa a konfigurációt, hívja meg a [Start-DscConfiguration](https://technet.microsoft.com/library/dn521623.aspx) rendelkező a __-Várjon, amíg__ paraméter.

## <a name="pull-mode"></a>Lekéréses mód

![Lekéréses mód](images/pullModel.png "lekéréses üzemmód működése")

Lekéréses módban lekéréses ügyfél lekérni a kívánt állapot konfigurációját egy távoli lekéréses szolgáltatásból van konfigurálva.
Hasonlóképpen, a lekéréses szolgáltatás állomás a DSC szolgáltatás beállítása és konfigurációkat és a lekéréses ügyfelek által igényelt erőforrás van kiépítve.
Mindegyik lekéréses ügyfél rendelkezik-e egy ütemezett eseményre, hogy a csomópont konfigurálása rendszeres megfelelőségi ellenőrzést végez.
Az esemény akkor váltódik ki az első alkalommal, amikor a helyi Configuration Manager (LCM) az lekéréses ügyfélen egy kérést küld a lekéréses szolgáltatás a LCM a megadott konfiguráció lekérése.
Ha ez a konfiguráció lekéréses szolgáltatás létezik, és adja át, kezdeti érvényességi ellenőrzéseket, a konfiguráció az lekéréses ügyfélnek, amelyen, majd végrehajtja a rendszer által a LCM le.

A LCM ellenőrzi, hogy az ügyfél által meghatározott rendszeres időközönként a konfiguráció megfelel a **ConfigurationModeFrequencyMins** a LCM tulajdonsága.
A LCM lekéréses szolgáltatás frissített konfiguráció által meghatározott rendszeres időközönként ellenőrzi a **RefreshModeFrequency** a LCM tulajdonsága.
A LCM konfigurálásával kapcsolatos további információkért lásd: [konfigurálása a helyi Configuration Manager](metaConfig.md).

Az ajánlott megoldás egy lekéréses szolgáltatást tartalmazó a DSC felhőszolgáltatás [Azure Automation](https://azure.microsoft.com/en-us/services/automation/).
Ez üzemeltetett megoldás grafikus felügyeleti, a jelentéskészítés és a központi felügyeletet biztosít.

Egy lekéréses szolgáltatás a Windows Server beállításával kapcsolatos további információkért lásd: [DSC lekérési webkiszolgáló beállítása](pullServer.md).
Ismerje meg, azonban, hogy ez a megvalósítás csak korlátozott szolgáltatásokat, és szükséges az egyes "elvégezhető saját kezűleg" integráció.

Az alábbi témakörök ismertetik lekéréses szolgáltatás és az ügyfelek:

- [Azure Automation DSC – áttekintés](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview)
- [Az SMB-lekérési kiszolgálójával beállítása](pullServerSMB.md)
- [A lekéréses ügyfél konfigurálása](pullClientConfigID.md)
