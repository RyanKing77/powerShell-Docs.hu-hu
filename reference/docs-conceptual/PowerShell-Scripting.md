---
ms.date: 08/27/2018
keywords: PowerShell, a parancsmag
title: PowerShell-parancsprogramok
ms.openlocfilehash: 8a152ab338d42f861b7ff38de44d68db14262abb
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851186"
---
# <a name="powershell"></a>PowerShell

PowerShell egy feladatalapú parancssori rendszerhéj és programozási nyelv, .NET épülő az.
PowerShell segítségével a rendszergazdák és a teljesítmény – a felhasználók gyorsan automatizálhatja a feladatokat, amelyek kezelése (Linux, macOS és Windows) operációs rendszerekkel és folyamatokkal.

PowerShell-parancsok segítségével kezelhet számítógépeket a parancssorból. PowerShell-szolgáltatók lehetővé teszik az adattárakban, például a beállításjegyzék eléréséhez, és a tanúsítványtárolót, egyszerűen, férni a fájlrendszerhez. PowerShell tartalmaz egy gazdag kifejezés az elemzési és a egy fejlett programozási nyelv.

## <a name="powershell-is-open-source"></a>PowerShell az nyílt forráskódú

PowerShell alap forráskód már elérhető a Githubon, és nyissa meg a közösségi közreműködést.
Lásd: [PowerShell forráskód a Githubon](https://github.com/powershell/powershell).

A bits szükséges kezdhet [a PowerShell első](https://github.com/PowerShell/PowerShell#get-powershell).
Vagy esetleg a gyors bemutatót [bevezetés](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell).

## <a name="powershell-design-goals"></a>PowerShell elérheti a céljait

PowerShell régóta fennálló problémák, és új funkciók hozzáadásával a parancssori és parancsfájl-kezelési környezet javítására szolgál.

### <a name="discoverability"></a>Felderíthetőség

PowerShell megkönnyíti a felderítését annak szolgáltatásait. Ha például megtekintése és módosítása a Windows-szolgáltatások parancsmagjainak listáját találja, írja be:

```powershell
Get-Command *-Service
```

Felfedezése, mely parancsmag feladatot el egy feladatot, miután további információ a parancsmag használatával a `Get-Help` parancsmagot. Például kapcsolatos súgó megjelenítése a `Get-Service` parancsmagot, írja be:

```powershell
Get-Help Get-Service
```

A legtöbb parancsmagok visszaadott objektumok, amelyek kezelhetők, és ezután jelenik meg a megjelenítendő szöveg. Teljes mértékben megérteni a parancsmag kimenete, irányítsa a kimenetét a `Get-Member` parancsmagot. Például a következő parancsot az objektum kimenete tagjainak információit jeleníti meg a `Get-Service` parancsmagot.

```powershell
Get-Service | Get-Member
```

### <a name="consistency"></a>Consistency

Rendszerek kezelése összetett feladat lehet. Egységes felület rendelkező eszközök segítségével szabályozhatja a járó összetettséget. Sajnos parancssori eszközök és parancsfájlok futtatására alkalmas COM-objektumok azok konzisztencia nem ismert.

A PowerShell konzisztencia az egyik elsődleges eszközei. Például, ha megismerheti, hogyan használható a `Sort-Object` parancsmag használhatja arra, hogy bármely parancsmag kimenete rendezéséhez. Ismerje meg a különböző rendezési rutinok minden parancsmag nem kell.

Tervezési rendezési tulajdonságok azok a parancsmagok ezenkívül parancsmag a fejlesztők nem szükséges. PowerShell az alapvető szolgáltatások egy keretrendszer, amely kényszeríti a konzisztencia biztosít. A keretrendszer kiküszöböli az egyes lehetőségek, hogy a fejlesztők van hátra. De cserébe teszi parancsmagok fejlesztését jóval egyszerűbb.

### <a name="interactive-and-scripting-environments"></a>Interaktív és parancsfájl-kezelési környezet

A Windows-parancssor használatával interaktív shell parancssori eszközökkel és az alapszintű parancsfájlok hozzáférést biztosít. Windows Script Host (WSH) rendelkezik a parancsfájlok futtatására alkalmas parancssori eszközeivel és a COM-automatizálási objektumok, de nem biztosít egy interaktív kezelőfelület.

PowerShell-ben interaktív shell és a egy parancsfájl-kezelési környezet. PowerShell parancssori eszközökkel, a COM-objektumok és a .NET-osztálytárak hozzáférhet. Ez a kombinációja bővíti ki az interaktív felhasználó, a parancsfájl-író és a rendszergazdához.

### <a name="object-orientation"></a>Objektum tájolása

PowerShell az objektum nem szöveg alapján történik. A parancs kimenete egy olyan objektum. A kimeneti objektum, a folyamat keresztül küldhet bemenetként egy másik parancsba.

Ez a folyamat ismerős felületet biztosít a személyek hasznosítani más ismertetése. PowerShell ezen elgondolás szöveg helyett objektumok küldésével.

### <a name="easy-transition-to-scripting"></a>A parancsfájl-kezelési egyszerű Váltás

PowerShell a parancs felderíthetőség teszi azt írja be a Váltás könnyen parancsok, interaktív módon való létrehozásának és futtatásának parancsfájlok. PowerShell átiratok és előzmények megkönnyítik egy fájlt egy parancsfájl használható parancsok másolása.
