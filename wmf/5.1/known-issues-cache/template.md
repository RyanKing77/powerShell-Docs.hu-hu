---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
title: "egy ismert probléma vagy korlátozás átíráshoz sablon – példa"
ms.openlocfilehash: b93393b2c84e76a301e6406d1388e82e95a2959c
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
>Megjegyzés: Adja meg a javasolt informatív címet és egy rövid leírást

## <a name="example-erroneous-executionpolicy-errors"></a>Példa: Hibás ExecutionPolicy hibák ##
A Windows 7 a PowerShell-modulok és a DSC-erőforrások ExecutionPolicy kapcsolatos jelentett hibákat eredményezhet.

### <a name="resolution"></a>Felbontás

Oldja meg, állítsa be a **ExecutionPolicy** való **RemoteSigned** a következő parancs futtatásával egy rendszergazda jogú PowerShell-munkamenetben (Futtatás rendszergazdaként):

```powershell
Set-ExecutionPolicy RemoteSigned
```

