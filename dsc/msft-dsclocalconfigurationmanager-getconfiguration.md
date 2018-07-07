---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály GetConfiguration metódusa
ms.openlocfilehash: ae31ac30c152c96707b764ddaf00c924806afcfc
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892542"
---
# <a name="getconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály GetConfiguration metódusa

A konfigurációs dokumentum küldése a felügyelt csomóponthoz, és használja a **első** metódus a alkalmazni a konfigurációt a konfigurációs ügynök.

## <a name="syntax"></a>Szintaxis

```mof
uint32 GetConfiguration(
  [in]  uint8            configurationData[],
  [out] OMI_BaseResource configurations[]
);
```

## <a name="parameters"></a>Paraméterek

*configurationData* \[a\] adja meg a konfigurációs adatokat küldhet.

*konfigurációk* \[ki\] lépjen vissza, tartalmazza a konfigurációkat egy beágyazott példányát.

## <a name="return-value"></a>Vrácená hodnota

Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.

## <a name="remarks"></a>Megjegyzések

Ez a statická metoda.

## <a name="requirements"></a>Követelmények

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Lásd még:

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)