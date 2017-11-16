---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "ApplyConfiguration metódust a MSFT_DSCLocalConfigurationManager osztály"
ms.openlocfilehash: febaf972a2a452eb9aaf3ec7fbc5e41f3f463a58
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="applyconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>ApplyConfiguration metódust a MSFT_DSCLocalConfigurationManager osztály

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

*kényszerített* \[a\]  
Ha ez **igaz**, a jelenlegi konfiguráció megváltoztatni, még akkor is, ha egy konfigurációjának kiszámítása függőben van.

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

 

 



