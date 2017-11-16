---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration módszer"
ms.openlocfilehash: faa113c442b80eea3ac474220b098b7d80ec50a8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>A MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration módszer

Eltávolítja a konfigurációs fájlok.

<a name="syntax"></a>Szintaxis
------

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

<a name="parameters"></a>Paraméterek
----------

*Szakasz* \[a\]  
Itt adhatja meg, melyik konfigurációs dokumentum eltávolítása. A következő értékek érvényesek:

|Érték |Leírás |
|:--- |:---|
|**1** | A **aktuális** konfigurációs dokumentum (current.mof). |
|**2** | A **függőben lévő** konfigurációs dokumentum (pending.mof).  |
|**4** | A **előző** konfigurációs dokumentum (previous.mof). |

*Kényszerített* \[a\]  
**Igaz** a konfiguráció eltávolításának kényszerítése.

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


 

 



