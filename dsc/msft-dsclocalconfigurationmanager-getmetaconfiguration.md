---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetMetaConfiguration metódusa
ms.openlocfilehash: e14237ef68b95d68e2f14071aa1fa6ba0717f39f
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892841"
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály GetMetaConfiguration metódusa

Lekérdezi a helyi Configuration Manager-beállításokat, hogy a konfigurációs ügynök szabályozására szolgálnak.

## <a name="syntax"></a>Szintaxis

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

## <a name="parameters"></a>Paraméterek

*MetaConfiguration* \[ki\] return tartalmaz egy beágyazott példányát a **MSFT_DSCMetaConfiguration** osztály, amely meghatározza a beállításokat.

## <a name="return-value"></a>Vrácená hodnota

Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.

## <a name="remarks"></a>Megjegyzések

Ez a statická metoda.

## <a name="requirements"></a>Követelmények

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Lásd még:

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)