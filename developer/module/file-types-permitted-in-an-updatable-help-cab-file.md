---
title: Fájltípus esetében engedélyezett a egy frissíthető súgó CAB-fájl |} A Microsoft Docs
ms.custom: ''
ms.date: 03/22/2012
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Windows PowerShell 3.0
ms.assetid: acabdb93-c41a-4b8d-acbe-45cdab91e198
caps.latest.revision: 10
ms.openlocfilehash: 3562804157ebdfca561445a8671d726b55cc4efd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082447"
---
# <a name="file-types-permitted-in-an-updatable-help-cab-file"></a>Frissíthető CAB-súgófájlok megengedett fájltípusai

Ez a témakör felsorolja és ismerteti a tartalom frissíthető súgó CAB-fájlok.

## <a name="updatable-help-cab-file-requirements"></a>Frissíthető súgó CAB-fájl követelményei

Tömörítetlen CAB-fájl tartalmának alapértelmezés szerint 1 GB-os korlátozva. Megkerülésére ezt a korlátot, a felhasználóknak meg kell használni a **kényszerített** paraméterében a [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) és [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) parancsmagok.

Ahhoz, hogy biztosítsa a súgófájlokat, amelyek az internetről letöltött biztonságát, az frissíthető súgó CAB-fájl csak az alábbi fájltípusokat tartalmazhatnak. A [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsmag érvényesíti az összes fájlt a Súgó-témakör sémák alapján. Ha a `Update-Help` parancsmag egy fájlt, amely érvénytelen vagy nem engedélyezett típusú észlel, nem telepíti a érvénytelen fájlt, és leállítja a felhasználó számítógépén lévő fájlok telepítése.

- XML-alapú súgó-témaköröket parancsmagok.

- XML-alapú súgó-témaköröket parancsfájlokban és függvényekben.

- XML-alapú súgó-témaköröket Windows PowerShell-szolgáltatók.

- Szöveges súgótémakörök, például a témákról.

A [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) amikor, kibontja a CAB ellenőrzi a cab-fájl tartalmát. Ha `Update-Help` megkeresi a nem megfelelő fájltípusok egy frissíthető súgó CAB-fájl, a leállítási hibát generál, és leállítja a műveletet. Bármely súgófájlok nem telepít, a CAB, azokat is, az megfelelő típusú.