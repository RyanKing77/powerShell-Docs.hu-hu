---
title: A PowerShell parancsfájlokban és függvényekben súgóinak |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 859a6e22-75b1-43d4-ba62-62c107803b37
caps.latest.revision: 7
ms.openlocfilehash: 98a3f61ff4fa2367f69357173d4e8e14288ff429
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847844"
---
# <a name="writing-help-for-powershell-scripts-and-functions"></a>A PowerShell parancsfájlokban és függvényekben súgóinak összeállítása

PowerShell-parancsprogramok és funkciók teljes körűen dokumentálni kell, amikor azok másokkal megosztott.
A `Get-Help` parancsmag megjeleníti a parancsfájl és függvény súgótémakörök ugyanebben a formátumban, Súgó a parancsmagok, és az összes láthatók a `Get-Help` paraméterek dolgozhat parancsfájl és függvény Súgó-témaköröket.

PowerShell-parancsfájlok belefoglalhatja a parancsfájllal kapcsolatos súgótémakör és egyes funkciók lehetőségekről szóló súgótémakörök a parancsfájlt.
Parancsfájlok függetlenül megosztott is többek között a saját Súgó-témaköröket.

Ez a dokumentum ismerteti a formátum és a megfelelő elhelyezési témakörök, és azt sugallja, hogy a tartalom irányelveket.

## <a name="types-of-script-and-function-help"></a>Parancsfájl és a függvény súgója

### <a name="comment-based-help"></a>Megjegyzés-alapú súgó
A parancsfájlokban vagy függvényekhez lévő hozzászólások csoportja, amely leírja a parancsfájlokban vagy függvényekhez súgótémakör is megvalósíthatók.
Megjegyzés-alapú súgó talál egy parancsfájlt, és a Functions egy parancsfájlban írásakor a szabályok gondos figyelmet fordítania a Megjegyzés-alapú súgó biztonságnak.
Az Elhelyezés határozza meg, hogy a `Get-Help` parancsmag Súgó-témakör társítja a parancsfájl vagy függvény.
Megjegyzés-alapú súgó-témaköröket írt kapcsolatos további információkért lásd: [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).

### <a name="xml-based-command-help"></a>XML-alapú Súgóihoz
XML-fájl, a parancssori súgó sémát használ, amely leírja a parancsfájlokban vagy függvényekhez súgótémakör implementálható.
A parancsfájlokban vagy függvényekhez társítása az XML-fájlt, használja a `ExternalHelp` comment kulcsszót, az elérési útját és nevét az XML-fájlt.

Ha a `ExternalHelp` kulcsszó szerepel, akkor élvez Megjegyzés-alapú súgó megjegyzést, akkor is, ha `Get-Help` , amely megfelel a súgófájl nem található a `ExternalHelp` kulcsszót.

### <a name="online-help"></a>Online súgó
A Súgó-témaköröket közzé az interneten, és majd közvetlen `Get-Help` a témakörök megnyitásához.
Megjegyzés-alapú súgó-témaköröket írt kapcsolatos további információkért lásd: [Online súgó támogatása](../module/supporting-online-help.md).

Nincs elméleti ("tudnivalók") témakörök a parancsfájlokban és függvényekben írásra létrehozott módszer.
Azonban könyvelheti fogalmi témakörök az internetes listán a témaköröket, és saját URL-parancs súgótémakör kapcsolódó hivatkozások szakaszában.

## <a name="content-considerations-for-script-and-function-help"></a>Tartalom szempontjai szkript és a függvény súgója

- Ha csak a rendelkezésre álló parancssori súgó szakaszok néhány való írás nagyon rövid súgótémakör, mindenképp adja hozzá a parancsfájlokban vagy függvényekhez paraméterek egyértelmű leírását. Is egy vagy két minta közé olyan parancsok tartoznak a példa szakaszban, akkor is, ha úgy dönt, hogy hagyja ki a következő példa leírása.

- Az összes leírásáért tekintse meg a parancsot, mint a parancsfájlokban vagy függvényekhez. Ez az információ segít a megértéséhez és kezeléséhez a parancsot.

  Például az alábbi részletes leírás szerint, hogy a New-témakör parancs a következő parancsfájlt. Ez is emlékezteti a felhasználókat, hogy kell futtatásakor. Ez az elérési út és a teljes nevét adja meg.

  > "A New-témakör a szkript létrehoz egy üres elvi témakör minden témakör név a bemeneti fájl..."

  Az alábbi részletes leírást megállapítja, hogy `Disable-PSRemoting` függvénye. Ezek az információk különösen hasznos a felhasználók számára, amikor a munkamenet ugyanazzal a névvel, amelyek némelyike ablakméreteitől függően egy parancs által a magasabb több parancsokat is tartalmaz.

  > A `Disable-PSRemoting` függvény letiltja a helyi számítógép összes munkamenet-konfigurációk...

- A parancsfájl súgótémakör azt ismertetik, hogyan használja a parancsfájl egész. Ha is funkciók Súgó-témaköröket a szkriptben, ilyen a parancsfájl Súgó-témakör az a Funkciók, majd hivatkozásokat tartalmaznak arra a függvény Súgó-témaköröket a parancsfájl súgótémakör kapcsolódó hivatkozások szakaszában. Ezzel szemben függvény része egy parancsfájlt, amikor elmagyarázza, a függvény Súgó-témakör a szerepkör, amely a függvény játszik a szkriptet, és hogyan, előfordulhat, hogy használható egymástól függetlenül. A parancsfájl súgótémakör függvény Súgó-témakör kapcsolódó hivatkozások szakaszában listája.

- Példák a parancsfájl súgótémakör írásakor, mindenképp adja hozzá a parancsfájl elérési útját az a példában a parancs. Ez is emlékezteti felhasználókat, hogy azok kell megadnia, explicit módon, is, ha a parancsfájl az aktuális könyvtárban található.

- A függvény súgótémakör emlékeztesse a felhasználókat, hogy a függvény csak az aktuális munkamenetben létezik, és szeretne használni, más munkamenetek, szükségük van hozzá, vagy adja hozzá a PowerShell-profilt.

- `Get-Help` a parancsfájlokban vagy függvényekhez tartozó súgó-témakör jeleníti meg, csak akkor, ha a parancsfájl és súgótémakör fájlokat a megfelelő helyekre lesznek mentve. Ezért hasznos nem, a PowerShell telepítése vagy Mentés vagy a parancsfájlokban vagy függvényekhez telepítése a parancsfájlokban vagy függvényekhez súgótémakörök útmutatást tartalmazza. Ehelyett tartalmazza a dokumentum, a parancsfájlokban vagy függvényekhez terjesztésére használt telepítési útmutatást.

## <a name="see-also"></a>Lásd még:

 [A parancsfájlokban és függvényekben XML-alapú súgó-témaköröket írása](./writing-xml-based-help-topics-for-scripts-and-functions.md)

 [XML-alapú súgó-témaköröket írása parancsok](./writing-xml-based-help-topics-for-commands.md)

 [Megjegyzés-alapú súgó-témaköröket írása](./writing-comment-based-help-topics.md)
