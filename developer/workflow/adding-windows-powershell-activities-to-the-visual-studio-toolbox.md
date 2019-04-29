---
title: Windows PowerShell-tevékenységek hozzáadása a Visual Studio-eszközkészlet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9c8ef289-0659-42d1-9976-044b144201eb
caps.latest.revision: 6
ms.openlocfilehash: 2a8372d937fc3c959f7d829bb52495048423d506
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080475"
---
# <a name="adding-windows-powershell-activities-to-the-visual-studio-toolbox"></a>Windows PowerShell-tevékenységek hozzáadása a Visual Studio Toolboxhoz

Mielőtt egy PowerShell-munkafolyamat munkafolyamat-Tervező használatával hoz létre, először hozzá kell adnia a PowerShell-tevékenységek, egy Visual Studio munkafolyamat Konzolalkalmazás-projektet az eszközkészlet. Az alábbi eljárás bemutatja, hogyan Microsoft.PowerShell.Core.Activities szerelvény a tevékenységek hozzáadása a Visual Studio-eszközkészlet.

### <a name="adding-windows-powershell-activities-to-the-toolbox"></a>Windows PowerShell-tevékenységek hozzáadása az eszközkészlethez

1. Hozzon létre egy új munkafolyamat Konzolalkalmazás-projektet a Visual Studióban.

2. Az a **nézet** menüben kattintson a **eszközkészlet**.

3. Egy új lap hozzáadása az eszköztáron kattintson a jobb gombbal az eszközkészlet belül, és kattintson a **lap hozzáadása**, és az új lapon adjon meg egy nevet, például "PowerShell tevékenységek".

   Egy lap hozzáadása lehetővé teszi, hogy a PowerShell tevékenységek eszközkészlet más eszközökből külön csoportot.

4. Az eszközkészlet új lapon kattintson a **elemek kiválasztása...** . A **eszközkészlet elemek kiválasztása** párbeszédpanel jelenik meg.

5. Az a **eszközkészlet elemek kiválasztása** párbeszédpanelen kattintson a **System.Activities** fülre.

6. Kattintson a **Tallózás**.

7. Keresse meg a %WINDIR%\Microsoft.NET\assembly\GAC_MSIL\Microsoft.PowerShell.Core.Activities\v4.0_3.0.0.0__31bf3856ad364e mappát, és kattintson duplán a Microsoft.PowerShell.Core.Activities.dll.

8. Kattintson az **OK** gombra. A tevékenységek által a Microsoft.PowerShell.Core.Activities szerelvényben definiált mostantól elérhetők az eszközkészlet.

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-munkafolyamat írása](./writing-a-windows-powershell-workflow.md)

[Tevékenységek feldolgozása Windows PowerShell-munkafolyamat létrehozása](./creating-a-workflow-with-windows-powershell-activities.md)