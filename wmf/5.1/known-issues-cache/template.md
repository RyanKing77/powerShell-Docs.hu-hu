---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.topic: conceptual
title: a példában egy ismert probléma, illetve korlátozás writeup sablonját
ms.openlocfilehash: ed7ae3de392c8902917e5b98fd4fc9d5138ccaed
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688678"
---
><span data-ttu-id="99f37-103">Megjegyzés: a javasolt jellemző címet és a egy rövid leírást adjon meg</span><span class="sxs-lookup"><span data-stu-id="99f37-103">Note: provide a proposed descriptive title and a brief description</span></span>

## <a name="example-erroneous-executionpolicy-errors"></a><span data-ttu-id="99f37-104">Példa: Hibás ExecutionPolicy hibák</span><span class="sxs-lookup"><span data-stu-id="99f37-104">Example: Erroneous ExecutionPolicy errors</span></span> ##
<span data-ttu-id="99f37-105">Windows 7, a PowerShell-modulok és a DSC-erőforrások használatának kapcsolatos ExecutionPolicy jelentett hibákat eredményezhet.</span><span class="sxs-lookup"><span data-stu-id="99f37-105">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

### <a name="resolution"></a><span data-ttu-id="99f37-106">Felbontás</span><span class="sxs-lookup"><span data-stu-id="99f37-106">Resolution</span></span>

<span data-ttu-id="99f37-107">Oldja meg, állítsa be a **ExecutionPolicy** való **RemoteSigned** a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="99f37-107">To resolve, set the **ExecutionPolicy** to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```
