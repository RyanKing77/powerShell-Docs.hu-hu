---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ApplyConfiguration metódusa
ms.openlocfilehash: 2844e354e0d054b13b92267ce314536d88a1c33e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály ApplyConfiguration metódusa

A konfigurációs ügynök használja a beállítások, amelyek függőben van.

Nincs függőben lévő konfiguráció, ha ez a módszer az aktuális konfigurációt újra alkalmazza.


## <a name="syntax"></a>Szintaxis
------

```mof
uint32 ApplyConfiguration(
  [in] boolean force
);
```

## <a name="parameters"></a>Paraméterek
----------

*kényszerített* \[a\] ebben **igaz**, a jelenlegi konfiguráció megváltoztatni, még akkor is, ha egy konfigurációjának kiszámítása függőben van.

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