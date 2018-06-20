---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.topic: conceptual
title: egy ismert probléma vagy korlátozás átíráshoz sablon – példa
ms.openlocfilehash: 453d4e40b906ebcab7314f04e138ded271338846
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34221935"
---
><span data-ttu-id="0b502-103">Megjegyzés: Adja meg a javasolt informatív címet és egy rövid leírást</span><span class="sxs-lookup"><span data-stu-id="0b502-103">Note: provide a proposed descriptive title and a brief description</span></span>

## <a name="example-erroneous-executionpolicy-errors"></a><span data-ttu-id="0b502-104">Példa: Hibás ExecutionPolicy hibák</span><span class="sxs-lookup"><span data-stu-id="0b502-104">Example: Erroneous ExecutionPolicy errors</span></span> ##
<span data-ttu-id="0b502-105">A Windows 7 a PowerShell-modulok és a DSC-erőforrások ExecutionPolicy kapcsolatos jelentett hibákat eredményezhet.</span><span class="sxs-lookup"><span data-stu-id="0b502-105">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

### <a name="resolution"></a><span data-ttu-id="0b502-106">Felbontás</span><span class="sxs-lookup"><span data-stu-id="0b502-106">Resolution</span></span>

<span data-ttu-id="0b502-107">Oldja meg, állítsa be a **ExecutionPolicy** való **RemoteSigned** a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):</span><span class="sxs-lookup"><span data-stu-id="0b502-107">To resolve, set the **ExecutionPolicy** to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```
