---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: EnableDebugConfiguration metódusa
ms.openlocfilehash: f1290e4d898332361850ffc85aa0a8d79863c8f7
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727146"
---
# <a name="enabledebugconfiguration-method"></a>EnableDebugConfiguration metódusa

Lehetővé teszi a DSC-erőforrás hibakeresés.

## <a name="syntax"></a>Szintaxis

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

## <a name="parameters"></a>Paraméterek

*BreakAll* \[a\] állítja be egy töréspontot minden sor az erőforrás-szkriptben.

## <a name="return-value"></a>Vrácená hodnota

Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.

## <a name="remarks"></a>Megjegyzés

Ez a statická metoda.

## <a name="requirements"></a>Követelmények

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Lásd még:

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)
