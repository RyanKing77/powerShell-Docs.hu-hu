---
title: OutputType attribútummal Deklarace |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a97a98ee-ffc0-42f0-a9a6-b0717b39c798
caps.latest.revision: 5
ms.openlocfilehash: 7aa6fa407e509a31c4066c4f73ae01b02b2f338c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845212"
---
# <a name="outputtype-attribute-declaration"></a>OutputType adatok attribútumdeklarációja

A `OutputType` attribútum azonosítja a .NET-keretrendszer típusok egy parancsmag, függvény vagy parancsfájl által visszaadott.

## <a name="syntax"></a>Szintaxis

```csharp
[OutputType(params string[] type)]
[OutputType(params Type[] type)]
[OutputType(params string[] type, Named Parameters...)]
[OutputType(params Type[] type, Named Parameters...)]
```

#### <a name="parameters"></a>Paraméterek

Típus (`string[]` vagy `Type[]`) szükséges. Megadja a parancsmag függvény vagy parancsfájl által visszaadott típusát.

ParameterSetName (nem kötelező string[]). Adja meg a megadott típusok visszaadó paraméterkészlettel a `type` paraméter.

providerCmdlet nem kötelező. Adja meg a szolgáltató parancsmag, amely visszaadja a megadott típusok a `type` paraméter.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
