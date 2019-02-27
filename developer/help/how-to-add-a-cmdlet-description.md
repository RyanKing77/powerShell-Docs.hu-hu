---
title: Egy parancsmag leírás hozzáadása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 47af9d57-bd63-4596-816a-0b717418476b
caps.latest.revision: 10
ms.openlocfilehash: a2e4c4d42566d5a52006924eab02295c37cf3159
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851428"
---
# <a name="how-to-add-a-cmdlet-description"></a>A parancsmag leírásának hozzáadása

Ez a szakasz ismerteti, hogyan adhat hozzá a DESCRIPTION szakaszban, a parancsmag súgójában megjelenő tartalmat. Ez a tartalom a súgófájlban a parancs csomópont az egyes parancsmagok kerül.

> [!NOTE]
> A súgófájl, nyissa meg a dll-Help.xml fájlok a Windows PowerShell telepítési könyvtárában található teljes megjelenítéséhez. Például a Microsoft.PowerShell.Commands.Management.dll-Help.xml fájl tartalma számos, a Windows PowerShell-parancsmagok számára.

### <a name="to-add-a-description"></a>Leírás hozzáadása

- Kezdje azzal, hogy további részleteket a parancsmag alapszintű funkcióit ismerteti. Sok esetben ismertetik a kifejezések, a parancsmag neve, és a egy példával szemlélteti ismeretlen fogalmak ismertetéséhez. Elmagyarázhatja például, ha a parancsmag adatokat fűz hozzá egy fájlt, adatok hozzáadja egy meglévő fájl végéhez.

- A parancsmag az a funkciók megkereséséhez tekintse át a paramétert. A parancsmag az elsődleges funkciója ismertetik, és az egyéb funkciók és szolgáltatások. Feltételezzük például, ha a fő függvényt a parancsmag egy tulajdonság, de a parancsmaggal módosíthatja az összes tulajdonságát, így részletes leírásában. Ha a parancsmag-paraméterek lehetővé teszik a felhasználók hozzájárulásával adatokat különböző módon, ismertetik.

- Olyan módon, hogy a felhasználók használhatják a parancsmag mellett a nyilvánvaló használja a információkat tartalmaznak. Például használhatja az objektum, amely a `Get-Host` parancsmag lekéri a Windows PowerShell-parancsablakot a szöveg színének módosítása.

  Példa:  "A `Get-Acl` parancsmag lekérdezi a biztonsági leíró fájl vagy erőforrás képviselő objektum. A biztonsági leíró tartalmazza a hozzáférés-vezérlési listák (ACL-ek) az erőforrás. Az ACL-t adja meg az engedélyeket, felhasználó és felhasználói csoport rendelkezik az erőforrás elérésére."

- A részletes leírása a parancsmag kell ismertetnie, de azt nem kell ismertetnie fogalmakat, amelyek a parancsmagot használja. További megjegyzések fogalom definíciók helyezze el.

## <a name="see-also"></a>Lásd még:

[Windows PowerShell SDK](../windows-powershell-reference.md)
