---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync módszer"
ms.openlocfilehash: e680bfd1c5b39d364c90cf5ef6b43d0a568af23a
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="sendconfigurationapplyasync-method-of-the-msftdsclocalconfigurationmanager-class"></a>A MSFT_DSCLocalConfigurationManager osztály SendConfigurationApplyAsync módszer

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

*ConfigurationData* \[a\]  
A környezet konfigurációjának adatait.

*kényszerített* \[a\]  
**Igaz** kényszerítése a konfigurációját, és állítsa le.

*a JobId értékének* \[a\]  
A konfigurációs küldési feladat Azonosítóját.

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


 

 



