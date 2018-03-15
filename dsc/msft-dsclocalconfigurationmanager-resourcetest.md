---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály ResourceTest módszer"
ms.openlocfilehash: 799b1cd91dfacf25c0e5e734ca96d20a776103f0
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a>A MSFT_DSCLocalConfigurationManager osztály ResourceTest módszer

Közvetlenül meghívja a **teszt** DSC erőforrás metódust.

<a name="syntax"></a>Szintaxis
------

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

<a name="parameters"></a>Paraméterek
----------

*A ResourceType* \[a\]  
Hívása az erőforrás neve.

*Modulnév* \[a\]  
A modul, amely tartalmazza a hívni az erőforrás neve.

*resourceProperty* \[a\]  
Adja meg az erőforrás-tulajdonság neve és értéke egy kivonattáblát a kulcs-érték, illetve. Használja a [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx) parancsmag az erőforrás-tulajdonságok és azok típusát.

*InDesiredState* \[kimenő\]  
A return, ez a tulajdonság értéke **igaz** Ha a célcsomópont a megfelelő állapotban van.

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


 

 



