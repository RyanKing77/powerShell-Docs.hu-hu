---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.topic: conceptual
title: a példában egy ismert probléma, illetve korlátozás writeup sablonját
ms.openlocfilehash: 8c1004e16f78913174af2e519e451f6fd9f30ff7
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62055547"
---
 ><span data-ttu-id="c8799-103">Megjegyzés: a javasolt jellemző címet és a egy rövid leírást adjon meg</span><span class="sxs-lookup"><span data-stu-id="c8799-103">Note: provide a proposed descriptive title and a brief description</span></span>

## <a name="example-erroneous-executionpolicy-errors"></a><span data-ttu-id="c8799-104">Példa: Hibás ExecutionPolicy hibák</span><span class="sxs-lookup"><span data-stu-id="c8799-104">Example: Erroneous ExecutionPolicy errors</span></span>
<span data-ttu-id="c8799-105">Windows 7, a PowerShell-modulok és a DSC-erőforrások használatának kapcsolatos ExecutionPolicy jelentett hibákat eredményezhet.</span><span class="sxs-lookup"><span data-stu-id="c8799-105">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

### <a name="resolution"></a><span data-ttu-id="c8799-106">Felbontás</span><span class="sxs-lookup"><span data-stu-id="c8799-106">Resolution</span></span>

<span data-ttu-id="c8799-107">Oldja meg, állítsa be a **ExecutionPolicy** való **RemoteSigned** a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="c8799-107">To resolve, set the **ExecutionPolicy** to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```
