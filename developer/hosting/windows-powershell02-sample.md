---
title: Windows PowerShell02 minta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 92492a7e-257d-47d3-b119-89df3c5545e8
caps.latest.revision: 9
ms.openlocfilehash: 89ad17257ebac56105a93672317a149515e80d32
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850357"
---
# <a name="windows-powershell02-sample"></a>Windows PowerShell02 – minta

Ez a példa bemutatja, hogyan futtathat parancsokat aszinkron módon történik a futási terek futási térben készlet használatával. A minta parancsok álló listát hoz létre, és majd futtatja azokat a parancsokat, amíg a Windows PowerShell motor megnyílik egy futási teret a készletből, szükség esetén.

## <a name="requirements"></a>Követelmények

- Ez a minta Windows PowerShell 2.0 szükséges.

## <a name="demonstrates"></a>Bemutatók

Ez a minta bemutatja a következőket:

- Egy RunspacePool objektum létrehozása a futási terek nyitható meg egyszerre engedélyezett minimális és maximális számát.

- Létrehoz egy listát az parancsokat.

- A parancsok aszinkron módon fut.

- Hívása a [System.Management.Automation.Runspaces.Runspacepool.Getavailablerunspaces*](/dotnet/api/System.Management.Automation.Runspaces.RunspacePool.GetAvailableRunspaces) metódus ingyenes hány futási terek megtekintéséhez.

- A parancs kimenete a rögzítés a [System.Management.Automation.Powershell.Endinvoke*](/dotnet/api/System.Management.Automation.PowerShell.EndInvoke) metódust.

## <a name="example"></a>Példa

Ez a példa bemutatja, hogyan lehet megnyitni a futási terek futási térben készlet, és hogyan aszinkron módon futtathat parancsokat a ezeket futási terek.

[!code-csharp[PowerShell02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/PowerShell02/PowerShell02.cs#L11-L96 "PowerShell02.cs")]

## <a name="see-also"></a>Lásd még:

[A Windows PowerShell-gazdagépet alkalmazás írása](./writing-a-windows-powershell-host-application.md)