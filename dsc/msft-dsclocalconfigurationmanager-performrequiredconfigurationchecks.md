---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály PerformRequiredConfigurationChecks módszer"
ms.openlocfilehash: 26110b3920104da7343b8d55cf63440c12accbbc
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="performrequiredconfigurationchecks-method-of-the-msftdsclocalconfigurationmanager-class"></a>A MSFT_DSCLocalConfigurationManager osztály PerformRequiredConfigurationChecks módszer

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

*Jelzők* \[a\]  
Bitmaszk, amely határozza meg a konzisztencia-ellenőrzés futtatásához. A következő értékek érvényesek, és egy bitenkénti használatával egyesíthetők **vagy** műveletet:

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


 

 



