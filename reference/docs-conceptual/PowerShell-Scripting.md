---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: PowerShell-parancsprogramok
ms.openlocfilehash: c6ba3abc2544834e2cbec16a524f79399a1d2599
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39094051"
---
# <a name="powershell"></a>PowerShell

A .NET-keretrendszer épülő PowerShell egy feladatalapú parancssori rendszerhéj és programozási nyelv; kifejezetten a rendszergazdák és kiemelt felhasználók felügyeletének részeként (Linux, macOS, Unix és Windows) több operációs rendszer és az operációs rendszereket futtató alkalmazásokhoz kapcsolódó folyamatok gyors automatizálása tervezték.

## <a name="powershell-is-open-source"></a>PowerShell az nyílt forráskódú

PowerShell alap forráskód már elérhető a Githubon, és nyissa meg a közösségi közreműködést.
Lásd: [PowerShell forráskód a Githubon](https://github.com/powershell/powershell).

A bits szükséges kezdhet [a PowerShell első](https://github.com/PowerShell/PowerShell#get-powershell).
Vagy esetleg a gyors bemutatót [első lépések](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell)

## <a name="powershell-design-goals"></a>PowerShell elérheti a céljait
PowerShell régóta fennálló problémák, és új funkciók hozzáadásával a parancssori és parancsfájl-kezelési környezet javítására szolgál.

### <a name="discoverability"></a>Felderíthetőség
PowerShell megkönnyíti a felderítését annak szolgáltatásait. Ha például megtekintése és módosítása a Windows-szolgáltatások parancsmagjainak listáját találja, írja be:

```powershell
Get-Command *-Service
```

Felfedezése, mely parancsmag feladatot el egy feladatot, miután további információ a parancsmag használatával a `Get-Help` parancsmagot.
Például kapcsolatos súgó megjelenítése a `Get-Service` parancsmagot, írja be:

```powershell
Get-Help Get-Service
```
A legtöbb parancsmagok gridre bocsáthatja ki az objektumok, amelyek kezelhetők, és megjelenítendő szöveget, majd meg.
Teljes mértékben megérteni, hogy a parancsmag kimenete, kanálu kimenete a `Get-Member` parancsmagot.
Például a következő parancsot az objektum kimenete tagjainak információit jeleníti meg a `Get-Service` parancsmagot.

```powershell
Get-Service | Get-Member
```

### <a name="consistency"></a>Consistency
Rendszerek kezelése egy összetett feladat lehet, és eszközöket, amelyek egy egységes felületen segítségével szabályozhatja a járó összetettséget.
Sajnos azonban nem parancssori eszközöket, és nem alkalmas parancsfájlok futtatására COM-objektumok az előzőekben a konzisztencia.

A PowerShell konzisztencia az egyik elsődleges eszközei.
Például, ha megismerheti, hogyan használható a `Sort-Object` parancsmag használhatja arra, hogy bármely parancsmag kimenete rendezéséhez.
További információt a különböző rendezési rutinok minden parancsmag nem rendelkezik.

A parancsmag a fejlesztők emellett nem rendelkezik a parancsmagok rendezési szolgáltatások tervezéséhez.
PowerShell biztosít egy keretrendszer, amely olyan alapvető szolgáltatásokat nyújt, és újrainicializálására kényszeríti a kapcsolatos a felület számos szempontból konzisztens.
A keretrendszer kiküszöböli néhány, a lehetőségek, amelyek általában a fejlesztők marad, de cserébe lehetővé teszi a hatékony és könnyen használható parancsmagok fejlesztését jóval egyszerűbb.

### <a name="interactive-and-scripting-environments"></a>Interaktív és parancsfájl-kezelési környezet
PowerShell az egy kombinált interaktív és parancsfájl-kezelési környezet, amely hozzáférést biztosít a parancssori eszközökkel és COM-objektumok, és lehetővé teszi, hogy a teljesítmény, a .NET Framework Class Library (FCL) használja.

Ebben a környezetben javítja esetén a Windows parancssor használatával, amely több parancssori eszközökkel interaktív környezetet biztosít.
Azt is javítja Windows Script Host (WSH) parancsfájlokat, amelyek lehetővé teszik több parancssori eszközeivel és COM-automatizálási objektumok, de nem ad meg egy interaktív környezetet.

Minden ezek a szolgáltatások kombinálásával PowerShell terjeszti ki a lehetőséget, az interaktív felhasználó és a parancsfájl-író, és megkönnyíti a rendszerfelügyelet könnyebben kezelhető.

### <a name="object-orientation"></a>Objektum tájolása
Bár a PowerShell dolgozhat parancsok beírásával a szöveg, PowerShell objektumokat, nem szöveg alapján történik.
A parancs kimenete egy olyan objektum.
A kimeneti objektum bemenetként küldhet egy másik parancsba.
Ennek eredményeképpen PowerShell felületet biztosít a jól ismert egy új és hatékony parancssori paradigmát bevezetése mellett egyéb parancskörnyezet ismerő személyek számára.
Ez a kiszolgálóvirtualizálás koncepcióján azáltal, hogy engedélyezi parancsokat küldhet az objektumokat, nem pedig szöveg közötti adatküldés.

### <a name="easy-transition-to-scripting"></a>A parancsfájl-kezelési egyszerű Váltás
Írja be az átállás egyszerűen parancsokat interaktív módon való létrehozásának és futtatásának parancsfájlok PowerShell teszi.
Fedezze fel, amelyek egy feladatot hajtanak végre a parancsokat a PowerShell-parancssort, írja be az parancsokat.
Ezután mentheti azokat a parancsokat egy szöveges vagy egy korábbi előtt egy fájl, amely egy parancsfájlt, hogy másolja őket.
