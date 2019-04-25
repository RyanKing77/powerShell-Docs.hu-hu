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
 >Megjegyzés: a javasolt jellemző címet és a egy rövid leírást adjon meg

## <a name="example-erroneous-executionpolicy-errors"></a>Példa: Hibás ExecutionPolicy hibák
Windows 7, a PowerShell-modulok és a DSC-erőforrások használatának kapcsolatos ExecutionPolicy jelentett hibákat eredményezhet.

### <a name="resolution"></a>Felbontás

Oldja meg, állítsa be a **ExecutionPolicy** való **RemoteSigned** a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):

```powershell
Set-ExecutionPolicy RemoteSigned
```
