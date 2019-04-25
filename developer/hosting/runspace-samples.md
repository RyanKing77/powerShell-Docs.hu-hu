---
title: Futási térben minták |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c92a6d3d-8d34-4a76-bdc3-dea923d9858e
caps.latest.revision: 17
ms.openlocfilehash: e24d40746da91f60aaf2af655ddcadc88ab6a4db
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082736"
---
# <a name="runspace-samples"></a>Futási tér – minták

Ez a szakasz bemutatja, hogyan futási terek különböző típusú szinkron és aszinkron módon parancsok futtatásához használandó mintakód tartalmazza. Microsoft Visual Studio segítségével hozzon létre egy konzolalkalmazást, majd a kódot bemásolhatja a témakörei ebben a szakaszban a gazdaalkalmazást.

## <a name="in-this-section"></a>A szakasz tartalma

> [!NOTE]
> Hozzon létre egyéni gazdagép adaptert alkalmazások üzemeltetését a mintákat, lásd: [egyéni állomást mintát](./custom-host-samples.md).

 [Runspace01 minta](./runspace01-sample.md) Ez a példa bemutatja, hogyan használhatja a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) futtatásához az osztály a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmag szinkron módon történik, és a konzol kimenetét megjelenítése ablak.

 [Runspace02 minta](./runspace02-sample.md) Ez a példa bemutatja, hogyan használhatja a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) futtatásához az osztály a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) és [Sort-Object](/powershell/module/Microsoft.PowerShell.Utility/Sort-Object) parancsmagok szinkron módon történik. Az eredmények az alábbi parancsok használatával jelenik meg egy [System.Windows.Forms.Datagridview](/dotnet/api/System.Windows.Forms.DataGridView) vezérlő.

 [Runspace03 minta](./runspace03-sample.md) Ez a példa bemutatja, hogyan használhatja a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) osztály parancsfájllal szinkron módon történik, és nem megszakító hibáinak kezelése. A parancsfájl folyamat nevének listáját fogadja, és ezután lekéri a folyamatokat. A parancsfájl, beleértve a parancsfájl futtatásakor létrehozott megszakítást nem okozó hibákat is az eredményeket a konzolablakban jelennek meg.

 [Runspace04 minta](./runspace04-sample.md) Ez a példa bemutatja, hogyan használhatja a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) osztály parancsokat futtathat, és hogyan catch okozott a parancsok futtatásakor megszakítást hibák. Két parancsok futtatása, és az utolsó parancs, amely nem érvényes a paraméter argumentumként átadott. Ezért egyetlen objektum sem adja vissza, és a megszakító hiba lépett fel.

 [Runspace05 minta](./runspace05-sample.md) Ez a példa bemutatja, hogyan adhat hozzá egy beépülő modul segítségével egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektumot, hogy a beépülő modul a parancsmag érhető el a futási térben megnyitásakor. A beépülő modult biztosít a Get-Proc parancsmag (határozzák meg a [GetProcessSample01 minta](../cmdlet/getprocesssample01-sample.md)), amelyek használatával futtatja a szinkron módon történik a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.

 [Runspace06 minta](./runspace06-sample.md) Ez a példa bemutatja, hogyan adhat hozzá egy modult egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektumot, hogy a modul betöltése a futási térben megnyitásakor. A modul adja meg a Get-Proc parancsmag (határozzák meg a [GetProcessSample02 minta](../cmdlet/getprocesssample02-sample.md)), amelyek használatával futtatja a szinkron módon történik a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.

 [Runspace07 minta](./runspace07-sample.md) Ez a példa bemutatja, hogyan hozhat létre egy futási teret, és a futási térben használatával két parancsmag használatával szinkron módon futnak a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.

 [Runspace08 minta](./runspace08-sample.md) Ez a példa bemutatja, hogyan parancsokat és argumentumokat adhat hozzá, a folyamat egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum és a parancsok futtatása szinkron módon történik.

 [Runspace09 minta](./runspace09-sample.md) Ez a példa bemutatja, hogyan, a folyamat egy parancsfájl hozzáadása egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum és a parancsfájl futtatása aszinkron módon történik. Események a szkript kimenetének kezelésére szolgálnak.

 [Runspace10 minta](./runspace10-sample.md) Ez a példa bemutatja, hogyan hozhat létre egy alapértelmezett kezdeti munkamenet-állapot, a parancsmag hozzáadása a [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState), hogyan hozhat létre egy futási teret használ, a kezdeti munkamenet-állapot, és hogyan használatával futtassa a parancsot egy [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) objektum.

 [Runspace11 minta](./runspace11-sample.md) ez bemutatja, hogyan használhatja a [System.Management.Automation.Proxycommand](/dotnet/api/System.Management.Automation.ProxyCommand) osztállyal hoz létre, amely meghív egy meglévő parancsmagot, de korlátozza az elérhető paraméterek készletét proxy parancsot. A proxy parancsot, amellyel egy korlátozott futási térrel hozzon létre egy kezdeti munkamenet-állapothoz kerül. Ez azt jelenti, hogy a felhasználó hozzáférhet-e az a Funkciók, a parancsmag csak a proxy parancs keresztül.

## <a name="see-also"></a>Lásd még:
