---
title: Megszakítást nem hibák |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 468dabd6-bfeb-448d-8e09-0996db516edd
caps.latest.revision: 8
ms.openlocfilehash: 5f804756e0e3e867832f15f50967fd6987f160a5
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067654"
---
# <a name="non-terminating-errors"></a>Megszakítást nem okozó hibák

Ez a témakör ismerteti a metódus okozó jelentésére használhatók. Emellett ismerteti a a módszerrel belül a parancsmag meghívása.

Ha egy nem megszakító hiba történik, a parancsmag meghívásával jelentse ezt a hibát a [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódust. A parancsmag egy nem megszakító hibát jelent, ha a parancsmag továbbra is megfelelően működjenek a bemeneti objektum és a további bejövő folyamat-objektumokat. Ha a parancsmagot hívja a [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) metódus, a parancsmag egy hiba rekordot, amely leírja a megszakítást nem okozó hiba kiváltó írhat. Hiba a rekordok kapcsolatos további információkért lásd: [Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md).

Parancsmagok segítségével meghívhatja [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) szükség szerint a saját feldolgozási módszerek bemeneti adatban. Azonban a parancsmagok segítségével meghívhatja [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) csak a hozzászólásláncot, amelynek a neve, a [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing), [ System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), vagy [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) bemeneti metódusához feldolgozásra. Ne hívja [System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError) egy másik szálból. Ehelyett kommunikálnak a főszálban vissza a hibákat.

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Cmdlet.WriteError](/dotnet/api/System.Management.Automation.Cmdlet.WriteError)

[System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing)

[System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)

[Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
