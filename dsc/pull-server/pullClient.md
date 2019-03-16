---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC lekérési ügyfél beállítása
ms.openlocfilehash: 54c68ac26e5388260e252ce01418170e26ddecde
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054254"
---
# <a name="setting-up-a-dsc-pull-client"></a>DSC lekérési ügyfél beállítása

> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

> [!IMPORTANT]
> A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak. Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).

Minden egyes célcsomóponttal le kell lekéréses mód használatára, hogy rendelkezik, és megadott URL-cím vagy a fájl helyét, ahol ezt a kapcsolatot a lekéréses kiszolgálón beolvasni a konfigurációkat és erőforrásokat, és ha kell adatokat küldhessen a azt.

A következő témakörök azt ismertetik, hogyan állítsa be a pull-ügyfelek:

* [Lekérési ügyfél beállítása konfigurációs nevekkel](pullClientConfigNames.md)
* [Lekérési ügyfél beállítása konfigurációs azonosítóval](pullClientConfigID.md)

> [!NOTE]
> Ezek a témakörök a PowerShell 5.0-s vonatkozik. A PowerShell 4.0-s lekérési ügyfél beállítása, lásd: [egy lekérési ügyfél beállítása konfigurációs Azonosítóval a PowerShell 4.0-s](pullClientConfigID4.md).