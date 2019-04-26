---
title: GetProc02 (C#) mintakód |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e4e1eee3-316b-43a4-8a60-313391619be6
caps.latest.revision: 6
ms.openlocfilehash: 2ac4aea2fdefdfe86349c14fe9b87cd8c41db090
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081705"
---
# <a name="getproc02-c-sample-code"></a>GetProc02 (C#) – mintakód

Az alábbi kód megvalósítását mutatja be egy `Get-Process` parancsmagot, amely elfogadja a parancssori bemenet. Figyelje meg, hogy ez a megvalósítás meghatározása egy `Name` paraméter lehetővé teszik a parancssori bemenet, és használja a [System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29) kimenetként, metódus a folyamat küld kimeneti mechanizmus objektumokat.

## <a name="code-sample"></a>Kódminta

[!code-csharp[GetProcessSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample02/GetProcessSample02.cs#L11-L76 "GetProcessSample02.cs")]

## <a name="see-also"></a>Lásd még:

[Windows PowerShell SDK](../windows-powershell-reference.md)