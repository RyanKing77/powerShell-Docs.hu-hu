---
title: Futási terek létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 17f323c3-e873-449e-8a28-477f1c6b5e12
caps.latest.revision: 6
ms.openlocfilehash: b4e61600f68521e4e7ab56ceae3349381e88a70a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848145"
---
# <a name="creating-runspaces"></a>Futási terek létrehozása

A futási térben egy fogadó alkalmazás által elindított a parancsok a működési környezetben. Ebben a környezetben a parancsokat és adatok, amelyek jelenleg találhatók és minden olyan nyelvi korlátozások jelenleg tartalmaz.

 Alkalmazások üzemeltetése használhatja a Windows PowerShell-lel, az összes elérhető a core-parancsokat is tartalmaz, ami által biztosított alapértelmezett futási térben vagy hozzon létre egy egyéni futási teret, amely a rendelkezésre álló parancsokat csak egy részhalmazát tartalmazza. Hozzon létre egy testre szabott futási teret, hozzon létre egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektumra, és rendelje hozzá a futási térben.

## <a name="runspace-tasks"></a>Futási térben feladatok

1. [Egy InitialSessionState létrehozása](./creating-an-initialsessionstate.md)

2. [Egy korlátozott futási térrel létrehozása](./creating-a-constrained-runspace.md)

3. [Több futási terek létrehozása](./creating-multiple-runspaces.md)

## <a name="see-also"></a>Lásd még:
