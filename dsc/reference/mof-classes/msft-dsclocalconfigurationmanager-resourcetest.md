---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály ResourceTest metódusa
ms.openlocfilehash: e7645b0c6b93b96cb01f72c1c92d468f7642ea13
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048462"
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály ResourceTest metódusa

Közvetlenül meghívja a **teszt** metódus a DSC-erőforrás.

## <a name="syntax"></a>Szintaxis

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

## <a name="parameters"></a>Paraméterek

*Erőforrástípus* \[a\] hívja az erőforrás nevét.

*ModuleName* \[a\] neve a modul, amely tartalmazza az erőforrás meghívásához.

*resourceProperty* \[a\] határozza meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve. Használja a [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource) parancsmaggal a erőforrás-tulajdonságok és azok típusát.

*InDesiredState* \[ki\] a visszaadandó, ez a tulajdonság értéke **igaz** Ha a célcsomópont a kívánt állapotban van.

## <a name="return-value"></a>Vrácená hodnota

Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.

## <a name="remarks"></a>Megjegyzés

Ez a statická metoda.

## <a name="requirements"></a>Követelmények

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Lásd még:

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)