---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály TestConfiguration metódusa
ms.openlocfilehash: 7815d458a9a67639a31c917510097212d104eb8a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály TestConfiguration metódusa

A konfigurációs dokumentum küld a felügyelt csomóponthoz, és a jelenlegi konfiguráció alapján a dokumentum ellenőrzi.

<a name="syntax"></a>Szintaxis
------

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

<a name="parameters"></a>Paraméterek
----------

*configurationData* \[a\] a confuguration környezet adatait.

*InDesiredState* \[kimenő\] a return határozza meg, hogy a felügyelt csomóponthoz a konfigurációs dokumentum által meghatározott állapotban.

*ResourcesInDesiredState* \[kimenő\] return tartalmaz beágyazott példányának a **MSFT_ResourceInDesiredState** osztály, amely meghatározza a kívánt állapot-erőforrást.

*ResourcesNotInDesiredState* \[kimenő\] return tartalmaz beágyazott példányának a **MSFT_ResourceNotInDesiredState** osztály, amely meghatározza az erőforrásokat, amelyek nem a megfelelő állapotban van.

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