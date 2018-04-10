---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
title: egy ismert probléma vagy korlátozás átíráshoz sablon – példa
ms.openlocfilehash: cecf31127aaa1942471877a2056230ab592bd095
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
>Megjegyzés: Adja meg a javasolt informatív címet és egy rövid leírást

## <a name="example-erroneous-executionpolicy-errors"></a>Példa: Hibás ExecutionPolicy hibák ##
A Windows 7 a PowerShell-modulok és a DSC-erőforrások ExecutionPolicy kapcsolatos jelentett hibákat eredményezhet.

### <a name="resolution"></a>Felbontás

Oldja meg, állítsa be a **ExecutionPolicy** való **RemoteSigned** a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):

```powershell
Set-ExecutionPolicy RemoteSigned
```