---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A MSFT_DSCLocalConfigurationManager osztály ResourceSet módszer"
ms.openlocfilehash: 3486ef559102929f8d05994a4bf6e45d49a0c140
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="resourceset-method-of-the-msftdsclocalconfigurationmanager-class"></a>A MSFT_DSCLocalConfigurationManager osztály ResourceSet módszer

Közvetlenül meghívja a **beállítása** DSC erőforrás metódust.

<a name="syntax"></a>Szintaxis
------

```mof
uint32 ResourceSet(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean RebootRequired
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

*RebootRequired* \[kimenő\]  
A return, ez a tulajdonság értéke **igaz** Ha célcsomóponton újra kell indítani.

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

 

 



