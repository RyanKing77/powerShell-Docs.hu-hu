---
title: Hibával kapcsolatos információk megjelenítése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 76fcc0c1-9795-45d3-a564-40f822b657b5
caps.latest.revision: 8
ms.openlocfilehash: 4bc8666ee9053eb368402c8644558f4fe2dcc9ee
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068283"
---
# <a name="displaying-error-information"></a>Hibaadatok megjelenítése

Ez a témakör ismerteti a módszereket, amelyben a felhasználók megjeleníthetik a hibával kapcsolatos információk.

A parancsmag hibát észlel, ha a hiba adatait bemutatása, alapértelmezés szerint hasonló a következő hibakimenet.

```powershell
$ stop-service lanmanworkstation
You do not have sufficient permissions to stop the service Workstation.
```

Azonban felhasználók megtekinthetik hibák kategória szerint beállításával a `$ErrorView` változó `"CategoryView"`. Kategória nézet hibaüzenet helyett a hiba szabad szöveges leírása származó azon információkat jeleníti meg. Ez a nézet lehet hasznos, ha hibák vizsgálata hosszú listáját. Kategória nézetben az előző hibaüzenet jelenik meg a következő.

```powershell
$ $ErrorView = "CategoryView"
$ stop-service lanmanworkstation
CloseError: (System.ServiceProcess.ServiceController:ServiceController) [stop-service], ServiceCommandException
```

Hiba történt a kategóriák kapcsolatos további információkért lásd: [Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md).

## <a name="see-also"></a>Lásd még:

[Windows PowerShell Hibarekordjainak](./windows-powershell-error-records.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
