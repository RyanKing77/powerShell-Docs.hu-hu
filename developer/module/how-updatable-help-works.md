---
title: Hogyan frissíthető súgó Works |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7674636e-a0f2-4587-bfc5-dd3e6ce5489e
caps.latest.revision: 6
ms.openlocfilehash: 8874cc18416937c4d3cb30d801f2714410304c8c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850224"
---
# <a name="how-updatable-help-works"></a>A frissíthető súgó működése

Ez a témakör ismerteti, hogyan frissíthető súgó folyamatok a HelpInfo XML-fájl és a CAB-fájlok az egyes modulok, és telepíti a frissítése a felhasználók súgóját.

## <a name="the-update-help-process"></a>Az Update-Help folyamat

Az alábbi lista ismerteti a műveleteket a [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsmag a súgófájlokat, a modul egy adott felhasználói felület kultúrafüggő részletei frissítésére szolgáló parancsot kell futtatásakor.
Az alábbi lista ismerteti a műveleteket a [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsmag a súgófájlokat, a modul egy adott felhasználói felület kultúrafüggő részletei frissítésére szolgáló parancsot kell futtatásakor.

1. `Update-Help` a távoli HelpInfo XML-fájl olvas be az értéket a megadott helyen a **HelpInfoURI** a moduljegyzékben kulcsra, és érvényesíti a sémának a fájlt. (A séma megtekintéséhez: [HelpInfo XML-séma](./helpinfo-xml-schema.md).) Ezután `Update-Help` keres egy helyi HelpInfo XML-fájl a modul a modul a címtárban a felhasználó számítógépén.

2. `Update-Help` a súgófájlok a megadott felhasználói felületi kulturális környezethez a helyi és távoli HelpInfo XML-fájlok, a modul verziószámát hasonlítja össze. Ha a távoli fájl verziószáma nagyobb, mint a helyi fájl a verziószámot, vagy ha az ott a modul nem helyi HelpInfo XML-fájljának `Update-Help` előkészíti az új súgófájlok letöltéséhez.

3. `Update-Help` kiválasztja a CAB-fájl a modulhoz megadott helyen a **HelpContentUri** elem a távoli HelpInfo XML-fájlban. A modul neve, a modul GUID és a felhasználói felület kultúrafüggő részletei használatával azonosíthatja a CAB-fájl.

4. `Update-Help` letölti a CAB-fájl, kibontja azt, ellenőrzi a tartalom súgófájlok és menti a Súgó tartalomfájlok a nyelvspecifikus alkönyvtárába a modul a felhasználó számítógépén.

5. `Update-Help` létrehoz egy helyi HelpInfo XML-fájlt a távoli HelpInfo XML-fájl másolásával. Úgy módosítja a helyi HelpInfo XML-fájlt, hogy csak a CAB-fájl, amely a telepített elemeket tartalmazza. Ezután menti a helyi HelpInfo XML-fájlt az modulkönyvtárat, és arra a következtetésre jut a frissítést.

## <a name="the-save-help-process"></a>A Save-Help folyamat

Az alábbi lista ismerteti a műveleteket a [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) és [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsmagok, amikor egy felhasználó futtatja a fájlmegosztásban lévő súgófájlokat, és használja ezeket a fájlokat a súgófájlok frissíteni a parancsokat a felhasználó számítógépén.
Az alábbi lista ismerteti a műveleteket a [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) és [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsmagok, amikor egy felhasználó futtatja a fájlmegosztásban lévő súgófájlokat, és használja ezeket a fájlokat a súgófájlok frissíteni a parancsokat a felhasználó számítógépén.

A `Save-Help` parancsmag egy parancsot a súgófájlokat, a modul mentse el egy fájlmegosztás által meghatározott válaszul a következő műveleteket hajtja végre a **DestinationPath** paraméter.

1. `Save-Help` a távoli HelpInfo XML-fájl olvas be az értéket a megadott helyen a **HelpInfoURI** a moduljegyzékben kulcsra, és érvényesíti a sémának a fájlt. (A séma megtekintéséhez: [HelpInfo XML-séma](./helpinfo-xml-schema.md).) Majd `Save-Help` keres egy helyi HelpInfo XML-fájl a könyvtárban, amely megadja a **DestinationPath** paramétert a `Save-Help` parancsot.

2. `Save-Help` a súgófájlok a megadott felhasználói felületi kulturális környezethez a helyi és távoli HelpInfo XML-fájlok, a modul verziószámát hasonlítja össze. Nagyobb, mint a helyi fájl a verziószámot a verziószámot a távoli fájl esetén, vagy ha nincs helyi HelpInfo XML-fájlt a modul a **DestinationPath** könyvtárban `Save-Help` előkészíti az új súgófájlok letöltéséhez.

3. `Save-Help` kiválasztja a CAB-fájl a modulhoz megadott helyen a **HelpContentUri** elem a távoli HelpInfo XML-fájlban. A modul neve, a modul GUID és a felhasználói felület kultúrafüggő részletei használatával azonosíthatja a CAB-fájl.

4. `Save-Help` letölti a CAB-fájlt, és menti a a **DestinationPath** könyvtár. (Ez nem hoz létre bármilyen nyelvspecifikus alkönyvtárak.)

5. `Save-Help` létrehoz egy helyi HelpInfo XML-fájlt a távoli HelpInfo XML-fájl másolásával. Úgy módosítja a helyi HelpInfo XML-fájlt, hogy csak elemei a mentett CAB-fájl tartalmazza. Ezután menti a helyi HelpInfo XML-fájl a a **DestinationPath** könyvtár és arra a következtetésre jut a frissítést.

   A `Update-Help` parancsmag a következő műveleteket hajtja végre a fájlok el egy fájlmegosztás által meghatározott felhasználó számítógépére a súgófájlokat frissítésére szolgáló parancsot kell válaszul a **SourcePath** paraméter.

1. `Update-Help` lekérdezi a távoli HelpInfo tartalmazó XML-fájlt a **SourcePath** könyvtár. Ezután egy helyi HelpInfo XML-fájl a modul a címtárban a felhasználó számítógépén keresi.

2. `Update-Help` a súgófájlok a megadott felhasználói felületi kulturális környezethez a helyi és távoli HelpInfo XML-fájlok, a modul verziószámát hasonlítja össze. Ha a verziószámot a távoli fájl nagyobb, mint a helyi fájl a verziószámot, vagy ha nincs helyi HelpInfo XML-fájl `Update-Help` előkészíti a súgófájlok új telepítését.

3. `Update-Help` a modul a CAB-fájl kiválasztása **SourcePath** könyvtár. A modul neve, a modul GUID és a felhasználói felület kultúrafüggő részletei használatával azonosíthatja a CAB-fájl.

4. `Update-Help` kibontja a CAB-fájl, ellenőrzi a tartalom súgófájlokat, és menti a Súgó tartalomfájlok modulkönyvtárat nyelvspecifikus alkönyvtárában a felhasználó számítógépén.

5. `Update-Help` létrehoz egy helyi HelpInfo XML-fájlt a távoli HelpInfo XML-fájl másolásával. Úgy módosítja a helyi HelpInfo XML-fájlt, hogy csak a CAB-fájl, amely a telepített elemeket tartalmazza. Ezután menti a helyi HelpInfo XML-fájlt az modulkönyvtárat, és arra a következtetésre jut a frissítést.