---
title: Windows PowerShell-példakód |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1106829a-8ddc-454e-bbdd-ade15d4bffb4
caps.latest.revision: 7
ms.openlocfilehash: 264e9f7538e13b48d899e87541239250eb88f14e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851960"
---
# <a name="windows-powershell-sample-code"></a>Windows PowerShell – Mintakód

A Windows SDK-n keresztül Windows PowerShell® minták érhetők el. Ez a szakasz tartalmazza a mintakódot, amely a Windows SDK-minták az szerepel.

> [!NOTE]
> A Windows SDK telepítve van, amikor egy **minták** könyvtár jön létre, amelyben a Windows PowerShell-minták elérhetővé válnak. Egy tipikus telepítési könyvtár nem **C:\Program Files\Microsoft SDKs\Windows\v6.0**. Indítsa el a Windows PowerShell és a típus **"cd Samples\SysMgmt\PowerShell"** keresse meg a Windows PowerShell-minták könyvtárat. Ez a dokumentum a Windows PowerShell-minták könyvtár nevezzük  **\<PowerShell-minták >**.

## <a name="sample-code-listing"></a>Minta kódlista

|Mintakód|Leírás|
|-----------------|-----------------|
|[AccessDbProviderSample01 Code Sample](./accessdbprovidersample01-code-sample.md)|Ez az, hogy a szolgáltató ismertetett [alapvető Windows PowerShell-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md).|
|[AccessDbProviderSample02 kódminta](./accessdbprovidersample02-code-sample.md)|Ez az, hogy a szolgáltató ismertetett [egy Windows PowerShell-meghajtó szolgáltató létrehozása](./creating-a-windows-powershell-drive-provider.md).|
|[AccessDbProviderSample03 kódminta](./accessdbprovidersample03-code-sample.md)|Ez az, hogy a szolgáltató ismertetett [egy Windows PowerShell elem szolgáltató létrehozása](./creating-a-windows-powershell-item-provider.md).|
|[AccessDbProviderSample04 kódminta](./accessdbprovidersample04-code-sample.md)|Ez az, hogy a szolgáltató ismertetett [létrehozása a Windows PowerShell-tároló szolgáltató](./creating-a-windows-powershell-container-provider.md).|
|[AccessDbProviderSample05 Code Sample](./accessdbprovidersample05-code-sample.md)|Ez az, hogy a szolgáltató ismertetett [egy Windows PowerShell navigációs szolgáltató létrehozása](./creating-a-windows-powershell-navigation-provider.md).|
|[AccessDbProviderSample06 kódminta](./accessdbprovidersample06-code-sample.md)|Ez az, hogy a szolgáltató ismertetett [létrehozása a Windows PowerShell a Tartalomszolgáltatón](./creating-a-windows-powershell-content-provider.md).|
|[GetProc01 Kódminták](./getproc01-code-samples.md)|Ez az alapszintű `Get-Process` parancsmag minta ismertetett [létrehozásához az első parancsmag](../cmdlet/creating-a-cmdlet-without-parameters.md).|
|[GetProc02 Kódminták](./getproc02-code-samples.md)|Ez a `Get-Process` parancsmag minta ismertetett [a folyamat parancssori bemenet-paramétereket adunk hozzá](../cmdlet/adding-parameters-that-process-command-line-input.md).|
|[GetProc03 Kódminták](./getproc03-code-samples.md)|Ez a `Get-Process` parancsmag minta ismertetett [a folyamat folyamat bemeneti paramétereket adunk hozzá](../cmdlet/adding-parameters-that-process-pipeline-input.md).|
|[GetProc04 Kódminták](./getproc04-code-samples.md)|Ez a `Get-Process` parancsmag minta ismertetett [hozzáadása Nonterminating hibajelentés a parancsmaghoz](../cmdlet/adding-non-terminating-error-reporting-to-your-cmdlet.md).|
|[GetProc05 Kódminták](./getproc05-code-samples.md)|Ez `Get-Process` parancsmag hasonlít a parancsmag ismertetett [hozzáadása Nonterminating hibajelentés a parancsmaghoz](../cmdlet/adding-non-terminating-error-reporting-to-your-cmdlet.md).|
|[StopProc01 Kódminták](./stopproc01-code-samples.md)|Ez a `Stop-Process` parancsmag minta ismertetett [létrehozása egy parancsmag, hogy módosítja a rendszer](../cmdlet/creating-a-cmdlet-that-modifies-the-system.md).|
|[StopProcessSample04 Kódminták](./stopprocesssample04-code-samples.md)|Ez a `Stop-Process` parancsmag minta ismertetett [paraméterkészlettel hozzáadása egy parancsmag](../cmdlet/adding-parameter-sets-to-a-cmdlet.md).|
|[Runspace01 Kódminták](./runspace01-code-samples.md)|Ezek a Kódminták a futási térben ismertetett [létrehozása egy Console Application, hogy fut a megadott parancs](http://msdn.microsoft.com/en-us/793a6570-a072-4799-840b-172f28ce620e).|
|[Runspace02 Kódminták](./runspace02-code-samples.md)|Ebben a példában a [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) végrehajtásához az osztály a `Get-Process` parancsmag szinkron módon történik.|
|[RunSpace03 Kódminták](./runspace03-code-samples.md)|Ezek a Kódminták a futási térben ismertetett [létrehozása egy Console Application, hogy fut a megadott parancsfájl](http://msdn.microsoft.com/en-us/a93e6006-36db-4bcc-b9da-c5bebf4ffd68).|
|[RunSpace04 Kódminták](./runspace04-code-samples.md)|Ez a kódminta egy futási teret használ, az a [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) osztály egy parancsfájlt, amely a leállítási hibát generál végrehajtásához.|
|[RunSpace05 kódminta](./runspace05-code-sample.md)|Ez a forráskódja számára a Runspace05 minta ismertetett [konfigurálása a futási teret használ RunspaceConfiguration](http://msdn.microsoft.com/en-us/42681d19-2d05-4975-befd-afb1990e79b2).|
|[RunSpace06 kódminta](./runspace06-code-sample.md)|Ez a forráskódja számára a Runspace06 minta ismertetett [konfigurálása egy futási teret egy Windows PowerShell beépülő modullal](http://msdn.microsoft.com/en-us/a7289ee8-9732-49ee-91c7-d533e9538b83).|
|[RunSpace07 kódminta](./runspace07-code-sample.md)|Ez a forráskódja számára a Runspace07 minta ismertetett [egy alkalmazást, hogy hozzáadja konzolparancsok egy folyamat létrehozása](http://msdn.microsoft.com/en-us/01eb7808-e97b-4905-80be-9e2fa38c262e).|
|[RunSpace08 kódminta](./runspace08-code-sample.md)|Ez a forráskódja számára a Runspace08 minta ismertetett [létrehozása egy Console Application, hogy hozzáadja a parancs paraméterei](http://msdn.microsoft.com/en-us/848b2b46-60f1-4a86-b448-cfc7c0cccfba).|
|[RunSpace09 kódminta](./runspace09-code-sample.md)|Ez a forráskódja számára a Runspace09 minta ismertetett [egy Console Application, hogy meghívja a folyamat aszinkron módon létrehozása](http://msdn.microsoft.com/en-us/198c1c94-2a06-457e-93ce-c0d910618e47).|
|[RunSpace10 kódminta](./runspace10-code-sample.md)|Ez az a Runspace10 minta, amely egy parancsmag hozzáadja a forráskód [System.Management.Automation.Runspaces.Runspaceconfiguration](/dotnet/api/System.Management.Automation.Runspaces.RunspaceConfiguration) és a módosított konfigurációs információk segítségével a futási térben létrehozása.|

## <a name="see-also"></a>Lásd még:

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)