---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.topic: conceptual
title: a példában egy ismert probléma, illetve korlátozás writeup sablonját
ms.openlocfilehash: 8c1004e16f78913174af2e519e451f6fd9f30ff7
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794492"
---
 ><span data-ttu-id="3a055-103">Megjegyzés: a javasolt jellemző címet és a egy rövid leírást adjon meg</span><span class="sxs-lookup"><span data-stu-id="3a055-103">Note: provide a proposed descriptive title and a brief description</span></span>

## <a name="example-erroneous-executionpolicy-errors"></a><span data-ttu-id="3a055-104">Példa: Hibás ExecutionPolicy hibák</span><span class="sxs-lookup"><span data-stu-id="3a055-104">Example: Erroneous ExecutionPolicy errors</span></span>
<span data-ttu-id="3a055-105">Windows 7, a PowerShell-modulok és a DSC-erőforrások használatának kapcsolatos ExecutionPolicy jelentett hibákat eredményezhet.</span><span class="sxs-lookup"><span data-stu-id="3a055-105">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

### <a name="resolution"></a><span data-ttu-id="3a055-106">Felbontás</span><span class="sxs-lookup"><span data-stu-id="3a055-106">Resolution</span></span>

<span data-ttu-id="3a055-107">Oldja meg, állítsa be a **ExecutionPolicy** való **RemoteSigned** a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="3a055-107">To resolve, set the **ExecutionPolicy** to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```
