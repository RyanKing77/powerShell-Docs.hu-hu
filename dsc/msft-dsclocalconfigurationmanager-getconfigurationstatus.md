---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus metódusa
ms.openlocfilehash: dde4ac003b346018561481e05ca7374475f9ff1d
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály GetConfigurationStatus metódusa

A konfigurációs állapotának előzménye beolvasása.

<a name="syntax"></a>Szintaxis
------

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

<a name="parameters"></a>Paraméterek
----------

*Minden* \[a\] **igaz** Ha ez a módszer minden információt, a konfiguráció fut a gépen kell visszaadnia, beleértve a konfigurációs alkalmazás és a konzisztencia-ellenőrzést.

*configurationStatus* \[kimenő\] return tartalmaz beágyazott példányának a **MSFT_DSCConfigurationStatus** osztály, amely meghatározza a beállításokat.

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