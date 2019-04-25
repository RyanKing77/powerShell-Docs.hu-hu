---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration metódusa
ms.openlocfilehash: 03555cc73da1272bdebebc3d93b26aaf8fabc18e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62078690"
---
# <a name="removeconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>Az MSFT_DSCLocalConfigurationManager osztály RemoveConfiguration metódusa

Eltávolítja a konfigurációs fájlokat.

## <a name="syntax"></a>Szintaxis

```mof
uint32 RemoveConfiguration(
  [in] uint32  Stage,
  [in] boolean Force
);
```

## <a name="parameters"></a>Paraméterek

*Fázis* \[a\] melyik konfigurációs dokumentum eltávolításához adja meg. A következő értékek érvényesek:

|Érték |Leírás |
|:--- |:---|
|**1** | A **aktuális** konfigurációs dokumentum (current.mof). |
|**2** | A **függőben lévő** konfigurációs dokumentum (pending.mof).  |
|**4** | A **előző** konfigurációs dokumentum (previous.mof). |

*Kényszerített* \[a\] **igaz** a konfigurációról eltávolításának kényszerítése.

## <a name="return-value"></a>Vrácená hodnota

Sikeres; a nulla értéket ad vissza egyéb esetben egy hibakódot ad vissza.

## <a name="remarks"></a>Megjegyzés

Ez a statická metoda.

## <a name="requirements"></a>Követelmények

**MOF:** DscCore.mof

**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>Lásd még:

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)