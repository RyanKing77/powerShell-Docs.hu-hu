---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: PerformRequiredConfigurationChecks method
ms.openlocfilehash: 909e3a48d08e0220ab0efc6a03bea7ead5d9843e
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734405"
---
# <a name="performrequiredconfigurationchecks-method"></a>PerformRequiredConfigurationChecks method

A Feladatütemező használatával egy konzisztencia-ellenőrzés indítása.

## <a name="syntax"></a>Szintaxis

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

## <a name="parameters"></a>Paraméterek

*Jelölők* \[a\] bitmaszk, amely meghatározza a konzisztencia-ellenőrzés futtatásához. A következő értékek érvényesek, és a egy bitenkénti használatával egyesíthető **vagy** műveletet:

|Érték |Leírás |
|:--- |:---|
|**1** | Normál konzisztencia-ellenőrzést. |
|**2** | Újraindítás után konzisztencia-ellenőrzést folytatása. Ez az érték nem egyesíthetők más értékeket. |
|**4** | A megadott csomópont a metaconfiguration lekéréses kiszolgálón kell kéri le a konfigurációt. Ez az érték mindig kombinálni kell **1**, a egy értéke **5**. |
|**8** | A jelentéskészítő kiszolgáló állapota küldeni. |

## <a name="return-value"></a>Vrácená hodnota

Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.

## <a name="remarks"></a>Megjegyzés

Ez a statická metoda.

## <a name="requirements"></a>Követelmények

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Lásd még:

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
