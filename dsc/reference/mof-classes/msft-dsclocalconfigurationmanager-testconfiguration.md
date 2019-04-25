---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály TestConfiguration metódusa
ms.openlocfilehash: d746832b01310f43a7aae33dd0fa70c0928bb3e0
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62078078"
---
# <a name="testconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály TestConfiguration metódusa

A konfigurációs dokumentum a felügyelt csomópont küld, és ellenőrzi az aktuális konfiguráció ellen a dokumentumot.

## <a name="syntax"></a>Szintaxis

```mof
uint32 TestConfiguration(
  [in]  uint8                          configurationData[],
  [out] boolean                        InDesiredState,
  [out] MSFT_ResourceInDesiredState    ResourcesInDesiredState[],
  [out] MSFT_ResourceNotInDesiredState ResourcesNotInDesiredState[]
);
```

## <a name="parameters"></a>Paraméterek

*configurationData* \[a\] confuguration a környezet adatait.

*InDesiredState* \[ki\] lépjen vissza, a Megadja, hogy a kezelt csomópontok a konfigurációs dokumentum által meghatározott állapotban van-e.

*ResourcesInDesiredState* \[ki\] return tartalmaz egy beágyazott példányát a **MSFT_ResourceInDesiredState** osztály, amely meghatározza az erőforrást, amely a kívánt állapotban.

*ResourcesNotInDesiredState* \[ki\] return tartalmaz egy beágyazott példányát a **MSFT_ResourceNotInDesiredState** osztály, amely megadja az erőforrások, amelyek nem a kívánt állapotban.

## <a name="return-value"></a>Vrácená hodnota

Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.

## <a name="remarks"></a>Megjegyzés

Ez a statická metoda.

## <a name="requirements"></a>Követelmények

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Lásd még:

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)