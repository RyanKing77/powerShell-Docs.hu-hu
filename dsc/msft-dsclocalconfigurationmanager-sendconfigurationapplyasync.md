---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync metódusa
ms.openlocfilehash: 7ff821a277a548869862741551ee9897e417ea45
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync metódusa

A konfigurációs dokumentum aszinkron módon küld a felügyelt csomóponthoz, és a konfigurációs ügynök segítségével a konfiguráció alkalmazásához.

<a name="syntax"></a>Szintaxis
------

```mof
uint32 SendConfigurationApplyAsync(
  [in] uint8   ConfigurationData[],
  [in] boolean force,
  [in] string  jobId
);
```

<a name="parameters"></a>Paraméterek
----------

*ConfigurationData* \[a\] konfigurációjának a környezet adatait.

*kényszerített* \[a\] **igaz** kényszerítése a konfigurációját, és állítsa le.

*a JobId értékének* \[a\] küldési a konfigurációs feladat az azonosító.

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