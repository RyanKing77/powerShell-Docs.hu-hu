---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceGet metódusa
ms.openlocfilehash: 1b74adf2327af2e0f9416f1d00eac4e3b75e9013
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404168"
---
# <a name="resourceget-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály ResourceGet metódusa

Közvetlenül meghívja a **első** metódus a DSC-erőforrás.

## <a name="syntax"></a>Szintaxis

```mof
uint32 ResourceGet(
  [in]  string           ResourceType,
  [in]  string           ModuleName,
  [in]  uint8            resourceProperty[],
  [out] OMI_BaseResource configurations
);
```

## <a name="parameters"></a>Paraméterek

*Erőforrástípus* \[a\] hívja az erőforrás nevét.

*ModuleName* \[a\] neve a modul, amely tartalmazza az erőforrás meghívásához.

*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve. Használja a [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) parancsmaggal a erőforrás-tulajdonságok és azok típusát.

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