---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC lekérési ügyfél beállítása
ms.openlocfilehash: 4c56671313b93cc12ce9460ce41e1710e0d6a526
ms.sourcegitcommit: ece1794c94be4880a2af5a2605ed4721593643b6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/16/2018
---
# <a name="setting-up-a-dsc-pull-client"></a>A DSC lekérési ügyfél beállítása

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

> [!IMPORTANT]
> A lekéréses kiszolgáló (Windows-szolgáltatás *DSC-szolgáltatás*), Windows Server támogatott összetevője létezik azonban a következők: nem tervezi, hogy új funkciók és képességek kínálnak. Javasoljuk, hogy kezdje a Váltás felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (tartalmazza a Windows Server-kiszolgáló lekéréses is) vagy a közösségi megoldásoknak a valamelyikét felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).

Minden cél fürtcsomópont lekéréses módban a rendszergazda és megadott URL-cím vagy a fájl helyét, akkor vegye fel a kapcsolatot a lekérési kiszolgálójával, hogy konfigurációk és erőforrások helyével, valamint azt kell jelentésadatok küldése.

Az alábbi témakörök ismertetik a lekéréses ügyfelek beállítása:

* [Lekérési ügyfél beállítása konfigurációs nevekkel](pullClientConfigNames.md)
* [Lekérési ügyfél beállítása konfigurációs azonosítóval](pullClientConfigID.md)

> **Megjegyzés:**: ezek a témakörök PowerShell 5.0 vonatkozik. A PowerShell 4.0 lekéréses ügyfél beállításához tekintse meg a [ügyféltelepítéshez lekéréses konfigurációs azonosítójával PowerShell 4.0](pullClientConfigID4.md).