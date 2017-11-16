---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály TestConfiguration módszer"
ms.openlocfilehash: 8e9986837aaf41b1396a2399c58675bc51b0b708
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>A MSFT_DSCLocalConfigurationManager osztály TestConfiguration módszer

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

*configurationData* \[a\]  
A confuguration környezet adatait.

*InDesiredState* \[kimenő\]  
A visszatérési határozza meg, hogy a felügyelt csomóponthoz a konfigurációs dokumentum által meghatározott állapotban.

*ResourcesInDesiredState* \[kimenő\]  
A visszatérési, tartalmazza a beágyazott példányának a **MSFT_ResourceInDesiredState** osztály, amely meghatározza a kívánt állapot-erőforrást.

*ResourcesNotInDesiredState* \[kimenő\]  
A visszatérési, tartalmazza a beágyazott példányának a **MSFT_ResourceNotInDesiredState** osztály, amely meghatározza az erőforrásokat, amelyek nem a megfelelő állapotban van.

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


 

 



