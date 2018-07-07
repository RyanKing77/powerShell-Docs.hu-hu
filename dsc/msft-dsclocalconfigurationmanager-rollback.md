---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály RollBack metódusa
ms.openlocfilehash: 4956900ecd2c9cb7f2e2b5bcab94616f9f5d5565
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893018"
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály RollBack metódusa

Visszaállítja a konfigurációt egy korábbi verzióra.

## <a name="syntax"></a>Szintaxis

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

## <a name="parameters"></a>Paraméterek

*configurationNumber* \[a\] adja meg a kért konfiguráció.

## <a name="return-value"></a>Vrácená hodnota

Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.

## <a name="remarks"></a>Megjegyzések

Ez a statická metoda.

## <a name="requirements"></a>Követelmények

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Lásd még:

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)