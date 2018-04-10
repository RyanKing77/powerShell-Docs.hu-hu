---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály StopConfiguration metódusa
ms.openlocfilehash: dadb6912af2e4450381958ed465799056da49946
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály StopConfiguration metódusa

Leállítja a folyamatban lévő konfigurációs módosítást.

<a name="syntax"></a>Szintaxis
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a>Paraméterek
----------

*kényszerített* \[a\] **igaz** kényszerítése a konfigurációját, és állítsa le.

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