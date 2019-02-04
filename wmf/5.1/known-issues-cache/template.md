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
>Megjegyzés: a javasolt jellemző címet és a egy rövid leírást adjon meg

## <a name="example-erroneous-executionpolicy-errors"></a>Példa: Hibás ExecutionPolicy hibák ##
Windows 7, a PowerShell-modulok és a DSC-erőforrások használatának kapcsolatos ExecutionPolicy jelentett hibákat eredményezhet.

### <a name="resolution"></a>Felbontás

Oldja meg, állítsa be a **ExecutionPolicy** való **RemoteSigned** a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):

```powershell
Set-ExecutionPolicy RemoteSigned
```
