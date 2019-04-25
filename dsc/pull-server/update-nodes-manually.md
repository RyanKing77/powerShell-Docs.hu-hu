---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Csomópontok frissítése lekérési kiszolgálóról
ms.openlocfilehash: 4333a5bf82ef45f22a062942ebe93409433623f5
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079098"
---
# <a name="update-nodes-from-a-pull-server"></a>Csomópontok frissítése lekérési kiszolgálóról

Az alábbi szakaszok azt feltételezik, hogy Ön már beállított egy lekéréses kiszolgálón. Ha nincs beállítva a lekéréses kiszolgálón, használhatja a következő útmutatókat:

- [DSC SMB-lekérési kiszolgáló beállítása](pullServerSmb.md)
- [A DSC HTTP-lekérési kiszolgáló beállítása](pullServer.md)

Minden egyes célcsomóponttal konfigurálható töltse le a konfigurációk, az erőforrásokat, és még jelentést annak állapotát. Ebből a cikkből megtudhatja, hogyan tölthet fel erőforrásokat, így elérhetők tölthető le, és konfigurálja az ügyfeleket, automatikusan erőforrások letöltéséhez. Amikor a csomópont kap keresztül egy hozzárendelt konfigurációs **lekéréses** vagy **leküldéses** (v5), automatikusan letölti az konfigurációjában megadott helyen található az LCM Konfigurálása a szükséges erőforrásokat.

## <a name="using-the-update-dscconfiguration-cmdlet"></a>Az Update-DSCConfiguration parancsmag használatával

A PowerShell 5.0-, kezdve a [Update-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/update-dscconfiguration) parancsmag frissíti a konfigurációját az LCM konfigurált lekérési kiszolgálóról egy csomópont kényszeríti.

```powershell
Update-DSCConfiguration -ComputerName "Server01"
```

## <a name="using-invoke-cimmethod"></a>Invoke-CIMMethod használatával

A PowerShell 4.0-s, manuálisan is kényszerítheti, hogy a használt konfiguráció frissítése lekérési ügyfél [Invoke-CIMMethod](/powershell/module/cimcmdlets/invoke-cimmethod). Az alábbi példa CIM-munkamenetet hoz létre a megadott hitelesítő adatokkal, a megfelelő CIM módszert hívja meg, és eltávolítja a munkamenetet.

```powershell
$cimSession = New-CimSession -ComputerName "Server01" -Credential $(Get-Credential)
Invoke-CimMethod -CimSession $cimSession -Namespace 'root/microsoft/windows/desiredstateconfiguration' -Class 'MSFT_DscLocalConfigurationManager' -MethodName 'PerformRequiredConfigurationChecks' -Arguments @{ 'Flags' = [uint32]1 } -Verbose
$cimSession | Remove-CimSession
```

## <a name="see-also"></a>Lásd még:

[PerformRequiredConfigurationChecks](/powershell/dsc/msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks)
