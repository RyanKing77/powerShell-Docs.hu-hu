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
><span data-ttu-id="2b60a-103">Megjegyzés: Adja meg a javasolt informatív címet és egy rövid leírást</span><span class="sxs-lookup"><span data-stu-id="2b60a-103">Note: provide a proposed descriptive title and a brief description</span></span>

## <a name="example-erroneous-executionpolicy-errors"></a><span data-ttu-id="2b60a-104">Példa: Hibás ExecutionPolicy hibák</span><span class="sxs-lookup"><span data-stu-id="2b60a-104">Example: Erroneous ExecutionPolicy errors</span></span> ##
<span data-ttu-id="2b60a-105">A Windows 7 a PowerShell-modulok és a DSC-erőforrások ExecutionPolicy kapcsolatos jelentett hibákat eredményezhet.</span><span class="sxs-lookup"><span data-stu-id="2b60a-105">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

### <a name="resolution"></a><span data-ttu-id="2b60a-106">Felbontás</span><span class="sxs-lookup"><span data-stu-id="2b60a-106">Resolution</span></span>

<span data-ttu-id="2b60a-107">Oldja meg, állítsa be a **ExecutionPolicy** való **RemoteSigned** a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="2b60a-107">To resolve, set the **ExecutionPolicy** to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```