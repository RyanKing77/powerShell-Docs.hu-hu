---
title: Windows PowerShell-mintakód | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1106829a-8ddc-454e-bbdd-ade15d4bffb4
caps.latest.revision: 7
ms.openlocfilehash: e9df44b17453e9f73f6eb388d9cbc8a69fce4ba2
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847994"
---
# <a name="windows-powershell-sample-code"></a>Windows PowerShell – Mintakód

A Windows PowerShell® minták a Windows SDKon keresztül érhetők el. Ez a szakasz tartalmazza a Windows SDK-mintákban található mintakód kódját.

> [!NOTE]
> Ha a Windows SDK telepítve van, a rendszer létrehoz egy **minta** könyvtárat, amelyben az összes Windows PowerShell-minta elérhetővé válik. Egy tipikus telepítési könyvtár a **C:\Program Files\Microsoft SDKs\Windows\v6.0**.
> Indítsa el a Windows PowerShellt, és írja be a **"CD Samples\SysMgmt\PowerShell"** parancsot a Windows PowerShell-minták könyvtárának megkereséséhez. Ebben a dokumentumban a Windows PowerShell-példákat tartalmazó könyvtárat  **\<PowerShell-minták >** nevezzük.

## <a name="sample-code-listing"></a>Mintakód listázása

|Mintakód|Leírás|
|-----------------|-----------------|
|[AccessDbProviderSample01-kód minta](./accessdbprovidersample01-code-sample.md)|Ez az [alapszintű Windows PowerShell-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md)című témakörben leírt szolgáltató.|
|[AccessDbProviderSample02-kód minta](./accessdbprovidersample02-code-sample.md)|Ezt a szolgáltatót a [Windows PowerShell-meghajtó létrehozásával](./creating-a-windows-powershell-drive-provider.md)kapcsolatban ismertetjük.|
|[AccessDbProviderSample03-kód minta](./accessdbprovidersample03-code-sample.md)|Ezt a szolgáltatót a [Windows PowerShell-elemek szolgáltatójának létrehozása](./creating-a-windows-powershell-item-provider.md)című témakörben találja.|
|[AccessDbProviderSample04-kód minta](./accessdbprovidersample04-code-sample.md)|Ez az a szolgáltató, amely a [Windows PowerShell-tároló szolgáltatójának létrehozása](./creating-a-windows-powershell-container-provider.md)című témakörben található.|
|[AccessDbProviderSample05-kód minta](./accessdbprovidersample05-code-sample.md)|Ez a [Windows PowerShell navigációs szolgáltató létrehozása](./creating-a-windows-powershell-navigation-provider.md)című témakörben leírt szolgáltató.|
|[AccessDbProviderSample06-kód minta](./accessdbprovidersample06-code-sample.md)|Ezt a szolgáltatót a [Windows PowerShell-tartalomszolgáltató létrehozása](./creating-a-windows-powershell-content-provider.md)című témakörben találja.|
|[GetProc01](./getproc01-code-samples.md)|Ez az `Get-Process` [első parancsmag létrehozása](../cmdlet/creating-a-cmdlet-without-parameters.md)című témakörben leírt alapszintű parancsmag.|
|[GetProc02](./getproc02-code-samples.md)|Ez az `Get-Process` a parancsmag-minta, [amely a parancssori bevitelt feldolgozó paraméterek hozzáadását](../cmdlet/adding-parameters-that-process-command-line-input.md)ismerteti.|
|[GetProc03](./getproc03-code-samples.md)|Ez az `Get-Process` a parancsmag-minta, [amely a folyamat bemenetét feldolgozó paraméterek hozzáadását](../cmdlet/adding-parameters-that-process-pipeline-input.md)írja le.|
|[GetProc04](./getproc04-code-samples.md)|Ez a `Get-Process` parancsmagnak a nem [lezáró hibajelentések a parancsmaghoz való hozzáadása](../cmdlet/adding-non-terminating-error-reporting-to-your-cmdlet.md)című részében ismertetett példa.|
|[GetProc05](./getproc05-code-samples.md)|Ez `Get-Process` a parancsmag hasonló ahhoz a parancsmaghoz, amelyet a nem [lezáró hibajelentések hozzáadása a parancsmaghoz](../cmdlet/adding-non-terminating-error-reporting-to-your-cmdlet.md)című témakör ismertet.|
|[StopProc01](./stopproc01-code-samples.md)|Ez a `Stop-Process` parancsmag a rendszer módosítását [módosító parancsmag létrehozása](../cmdlet/creating-a-cmdlet-that-modifies-the-system.md)című példa.|
|[StopProcessSample04](./stopprocesssample04-code-samples.md)|Ez az `Stop-Process` a parancsmag, amely a [paramétereket adja hozzá a parancsmaghoz](../cmdlet/adding-parameter-sets-to-a-cmdlet.md).|
|[Runspace01](./runspace01-code-samples.md)|Ezek a RunSpace a [megadott parancsot futtató konzolos alkalmazás létrehozása](/dotnet/csharp/programming-guide/inside-a-program/hello-world-your-first-program)című témakörben leírt példák.|
|[Runspace02](./runspace02-code-samples.md)|Ez a példa a [System. Management. Automation. Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) osztályt használja a `Get-Process` parancsmag szinkron módon történő végrehajtásához.|
|[RunSpace03](./runspace03-code-samples.md)|Ezek a RunSpace a "megadott parancsfájlt futtató konzolszoftver létrehozása" című témakörben leírt példák.|
|[RunSpace04](./runspace04-code-samples.md)|Ez egy RunSpace, amely a [System. Management. Automation. Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) osztályt használja egy olyan parancsfájl végrehajtásához, amely megszakítási hibát generál.|
|[RunSpace05-kód minta](./runspace05-code-sample.md)|Ez a Runspace05 minta forráskódja, amely a RunSpace a [RunspaceConfiguration használatával történő konfigurálását](https://msdn.microsoft.com/en-us/42681d19-2d05-4975-befd-afb1990e79b2)ismerteti.|
|[RunSpace06-kód minta](./runspace06-code-sample.md)|Ez a Runspace06 minta forráskódja, amely a [RunSpace Windows PowerShell beépülő modullal történő konfigurálását](https://msdn.microsoft.com/en-us/a7289ee8-9732-49ee-91c7-d533e9538b83)ismerteti.|
|[RunSpace07-kód minta](./runspace07-code-sample.md)|Ez a Runspace07 minta forráskódja, [amely egy olyan konzol-alkalmazás létrehozása, amely parancsokat vesz fel egy folyamathoz](https://msdn.microsoft.com/en-us/01eb7808-e97b-4905-80be-9e2fa38c262e).|
|[RunSpace08-kód minta](./runspace08-code-sample.md)|Ez a Runspace08 minta forráskódja, [amely egy parancs paramétereinek](https://msdn.microsoft.com/en-us/848b2b46-60f1-4a86-b448-cfc7c0cccfba)hozzáadására szolgáló konzol-alkalmazás létrehozása című témakörben szerepel.|
|[RunSpace09-kód minta](./runspace09-code-sample.md)|Ez a Runspace09-minta forráskódja, amely a folyamat aszinkron meghívására szolgáló [konzolos alkalmazás létrehozása](https://msdn.microsoft.com/en-us/198c1c94-2a06-457e-93ce-c0d910618e47)című témakörben szerepel.|
|[RunSpace10-kód minta](./runspace10-code-sample.md)|Ez a Runspace10 minta forráskódja, amely egy parancsmagot hoz létre a [System. Management. Automation. futási terek. Runspaceconfiguration fájlhoz](/dotnet/api/System.Management.Automation.Runspaces.RunspaceConfiguration) , majd a módosított konfigurációs adatokat használja a RunSpace létrehozásához.|

## <a name="see-also"></a>Lásd még:

[A Windows PowerShell programozói útmutatója](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)