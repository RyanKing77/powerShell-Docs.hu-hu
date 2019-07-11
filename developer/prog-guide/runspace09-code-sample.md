---
title: Kódminta RunSpace09 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 136e451f-767b-42e0-bd6f-6486693abd5e
caps.latest.revision: 6
ms.openlocfilehash: 1a21af4b48a414d9c9fee57871eacb0a39c9ab11
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734894"
---
# <a name="runspace09-code-sample"></a>Runspace09 – Kódminta

Itt van a forráskódot a Runspace09 minta ismertetett [egy Console Application, hogy meghívja a folyamat aszinkron módon létrehozása](https://msdn.microsoft.com/en-us/198c1c94-2a06-457e-93ce-c0d910618e47). Ez a mintaalkalmazás hoz létre, és megnyílik egy futási teret, létrehozása és aszinkron módon hív meg egy folyamatot, és ezután használt folyamat-események a parancsfájl műveletek aszinkron feldolgozásához. A jelen alkalmazás által futtatott parancsfájl 0,5 másodperces időközönként (500 ms) hoz létre az egész számok 1 és 10 közötti.

## <a name="code-sample"></a>Kódminta

[!code-csharp[Runspace09.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace09/Runspace09.cs#L11-L113 "Runspace09.cs")]

## <a name="see-also"></a>Lásd még:

[Windows PowerShell SDK](../windows-powershell-reference.md)