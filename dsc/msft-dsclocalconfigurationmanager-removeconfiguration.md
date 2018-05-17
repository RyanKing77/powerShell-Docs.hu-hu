---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration metódusa
ms.openlocfilehash: c68d17d38336dec08e078366ea5f2071fcf7c5a8
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration metódusa

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

*Szakasz* \[a\] határozza meg, melyik konfigurációs dokumentum eltávolítása. A következő értékek érvényesek:

|Érték |Leírás |
|:--- |:---|
|**1** | A **aktuális** konfigurációs dokumentum (current.mof). |
|**2. régiója** | A **függőben lévő** konfigurációs dokumentum (pending.mof).  |
|**4** | A **előző** konfigurációs dokumentum (previous.mof). |

*Kényszerített* \[a\] **igaz** a konfiguráció eltávolításának kényszerítése.

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