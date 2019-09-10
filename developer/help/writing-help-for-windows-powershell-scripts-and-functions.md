---
title: Súgó írása PowerShell-parancsfájlok és-függvények számára | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 859a6e22-75b1-43d4-ba62-62c107803b37
caps.latest.revision: 7
ms.openlocfilehash: af989fb2eeba6b68f2e3e6506f3f60d5be6f7d8a
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848102"
---
# <a name="writing-help-for-powershell-scripts-and-functions"></a>Súgó írása PowerShell-parancsfájlok és-függvények számára

A PowerShell-parancsfájlokat és-függvényeket teljes mértékben dokumentálni kell, ha másokkal vannak megosztva.
A parancsmag megjeleníti a parancsfájlt és a függvény súgóját a parancsmagok súgójában, valamint az összes `Get-Help` paramétert a parancsfájl és funkció Súgó témaköreiben. `Get-Help`

A PowerShell-parancsfájlok tartalmazhatnak egy súgótémakört a parancsfájlról, valamint a parancsfájl egyes funkcióihoz kapcsolódó súgótémaköröket is.
A parancsfájloktól függetlenül megosztott függvények magukban foglalhatják a saját súgótémaköröket.

Ez a dokumentum ismerteti a súgótémakörök formátumát és helyes elhelyezését, valamint útmutatást nyújt a tartalomhoz.

## <a name="types-of-script-and-function-help"></a>A szkriptek és függvények súgójának típusai

### <a name="comment-based-help"></a>Megjegyzés-alapú Súgó
A parancsfájlt vagy függvényt leíró súgótémakör a parancsfájlban vagy a függvényben megjegyzésként is megvalósítható.
Ha Megjegyzés-alapú súgót ír egy parancsfájlhoz, és a függvényeket egy parancsfájlban, gondosan figyeljen a Megjegyzés-alapú Súgó elhelyezésére vonatkozó szabályokra.
Az elhelyezés meghatározza, hogy `Get-Help` a parancsmag társítja-e a súgótémakört a parancsfájllal vagy a függvénnyel.
A Megjegyzés-alapú súgótémakörök írásával kapcsolatos további információkért lásd: [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).

### <a name="xml-based-command-help"></a>XML-alapú parancs súgója
A parancsfájlt vagy függvényt leíró súgótémakör a parancs Súgó sémáját használó XML-fájlban valósítható meg.
Ha a parancsfájlt vagy függvényt az XML-fájllal szeretné hozzárendelni, használja a `ExternalHelp` comment kulcsszót, majd az XML-fájl elérési útját és nevét.

Ha a `ExternalHelp` Megjegyzés kulcsszava megtalálható, elsőbbséget élvez a Megjegyzés-alapú súgóval, még akkor `Get-Help` is, ha nem talál a `ExternalHelp` kulcsszó értékével megegyező súgófájlokat.

### <a name="online-help"></a>Online súgó
A témaköröket közzéteheti az interneten, majd közvetlenül `Get-Help` megnyithatja a témákat.
A Megjegyzés-alapú súgótémakörök írásával kapcsolatos további információkért tekintse meg az [online súgó támogatásával](../module/supporting-online-help.md)foglalkozó témakört.

A szkriptek és a függvények fogalmi ("about") témaköreinek megírására nincs létrehozva metódus.
A témaköröket és azok URL-jeit azonban az interneten is közzéteheti a parancsok súgójának kapcsolódó hivatkozások szakaszában.

## <a name="content-considerations-for-script-and-function-help"></a>A parancsfájl és a függvény súgójának tartalmi szempontjai

- Ha egy rövid súgótémakörre ír, és csak néhányat tartalmaz a parancssori Súgó néhány szakasza, ügyeljen rá, hogy a parancsfájl vagy a függvény paramétereit is törölje. A példák szakasz egy vagy két mintáját is tartalmazhatja, még akkor is, ha úgy dönt, hogy kihagyja a példa leírásait.

- Az összes leírásban tekintse meg a parancsot parancsfájlként vagy függvényként. Ez az információ segít a felhasználónak a parancs megértésében és kezelésében.

  Például a következő részletes leírás megállapítja, hogy a New-topic parancs egy parancsfájl. Ez arra emlékezteti a felhasználókat, hogy az elérési utat és a teljes nevet meg kell adniuk a futtatásakor.

  > "A New-topic szkript egy üres elméleti témakört hoz létre a bemeneti fájlban található egyes témakörök nevéhez..."

  A következő részletes leírási állapotok `Disable-PSRemoting` függvényt képeznek. Ezek az információk különösen hasznosak a felhasználók számára, ha a munkamenet több, azonos nevű parancsot tartalmaz, amelyek némelyike egy magasabb prioritású paranccsal rejthető el.

  > A `Disable-PSRemoting` függvény letiltja az összes munkamenet-konfigurációt a helyi számítógépen...

- A parancsfájlokkal foglalkozó témakörben megtudhatja, hogyan használhatja a parancsfájlt egészként. Ha a parancsfájlban a functions súgó témakörei is megtalálhatók, Megemlítheti a parancsfájl súgójában található függvényeket, és a parancsfájl súgójának kapcsolódó hivatkozások szakaszában szereplő, a függvény Súgó témaköreire mutató hivatkozásokat is tartalmaz. Ezzel szemben, ha egy függvény egy parancsfájl részét képezi, magyarázza el a függvény súgójában, hogy a függvény milyen szerepet játszik a parancsfájlban, és hogyan használható egymástól függetlenül. Ezután sorolja fel a parancsfájl Súgó témakört a függvény súgójának kapcsolódó hivatkozások szakaszában.

- Ha példákat ír egy parancsfájl-súgótémakörre, ügyeljen arra, hogy a példában szereplő parancsfájl elérési útját is tartalmazza. Ez arra emlékezteti a felhasználókat, hogy explicit módon kell megadniuk az elérési utat, még akkor is, ha a parancsfájl az aktuális könyvtárban van.

- A függvény súgójában emlékeztesse a felhasználókat arra, hogy a függvény csak az aktuális munkamenetben legyen, és hogy más munkamenetekben is használhassa, hozzá kell adnia azt, vagy hozzá kell adnia egy PowerShell-profilt.

- `Get-Help`egy parancsfájlhoz vagy függvényhez tartozó súgótémakör megjelenítése csak akkor, ha a parancsfájlt és a súgótémakörök fájljait a megfelelő helyre menti. Ezért nem hasznos a PowerShell telepítésére vonatkozó utasítások, illetve a parancsfájl vagy függvény súgójának vagy funkciójának mentése vagy telepítése. Ehelyett vegyen fel minden olyan telepítési utasítást a dokumentumban, amelyet a parancsfájl vagy a függvény terjesztésére használ.

## <a name="see-also"></a>Lásd még:

[Megjegyzésekre épülő súgótémakörök írása](./writing-comment-based-help-topics.md)
