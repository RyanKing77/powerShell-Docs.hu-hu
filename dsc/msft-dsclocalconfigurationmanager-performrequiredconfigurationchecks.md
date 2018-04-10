---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály PerformRequiredConfigurationChecks metódusa
ms.openlocfilehash: 9cc4384088fcc39b09979b8ae4d023fc46307b13
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály PerformRequiredConfigurationChecks metódusa

A Feladatütemező használatával egy konzisztencia-ellenőrzés indítása.

<a name="syntax"></a>Szintaxis
------

```mof
uint32 PerformRequiredConfigurationChecks(
  [in] uint32 Flags
);
```

<a name="parameters"></a>Paraméterek
----------

*Jelzők* \[a\] bitmaszk, amely határozza meg a konzisztencia-ellenőrzés futtatásához. A következő értékek érvényesek, és egy bitenkénti használatával egyesíthetők **vagy** műveletet:

|Érték |Leírás |
|:--- |:---|
|**1** | Normál konzisztencia-ellenőrzést. |
|**2** | A rendszer újraindítása után konzisztencia-ellenőrzést fenntartása. Ezt az értéket nem használható együtt más értékekkel. |
|**4** | A konfigurációs kell kell húzni a csomópont metakonfigurációját megadott lekérési kiszolgálójáról. Ez az érték mindig használható együtt **1**, az érték **5**. |
|**8** | A jelentéskészítő kiszolgáló állapota küldeni. |

## <a name="return-value"></a>Visszatérési érték
------------

Sikeres művelet; nulla értéket ad vissza Ellenkező esetben hibakódot.

## <a name="remarks"></a>Megjegyzések

Ez a statikus módszer.

## <a name="requirements"></a>Követelmények
------------
>**MOF:** DscCore.mof

>**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration


## <a name="see-also"></a>Lásd még:


[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)