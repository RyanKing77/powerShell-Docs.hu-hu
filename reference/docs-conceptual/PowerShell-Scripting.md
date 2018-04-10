---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: PowerShell Scripting
ms.openlocfilehash: 3304ecc3129b710a003725715803a03b68f79b45
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="powershell"></a>PowerShell

A .NET-keretrendszer épülő PowerShell egy feladatalapú parancssori rendszerhéj és programozási nyelv; kifejezetten a rendszergazdák és a kiemelt-felhasználók, gyorsan automatizálják több operációs rendszer (Linux, macOS, Unix és a Windows) és a kapcsolódó ezen operációs rendszereken futó alkalmazások számára tervezték.

## <a name="powershell-is-open-source"></a>PowerShell nyílt forráskódú

PowerShell alap forráskód mostantól elérhető a Githubon és közösségi hozzájárulások meg van nyitva. Lásd: [PowerShell forrás a Githubon](https://github.com/powershell/powershell).

Kezdésként használhatja az kell, a bits [get PowerShell](https://github.com/PowerShell/PowerShell#get-powershell).
Vagy esetleg a kalauz következő [első lépések](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell)

## <a name="powershell-design-goals"></a>PowerShell céljai
A Windows PowerShell szolgáltatást javítására készült, a parancssori és parancsfájl-kezelési környezet kiküszöbölhetők azon régóta fennálló problémák, és vegye fel az új szolgáltatásokat.

### <a name="discoverability"></a>Felderíthetőségét
Windows PowerShell megkönnyíti, hogy annak funkció felderítéséhez. Például található megtekintése és módosítása a központi Windows-szolgáltatások parancsmagjainak listáját, írja be:

```
Get-Command *-Service
```

Miután értesült, mely parancsmag éri el a feladat, hogy többet is megtudhat a parancsmag a Get-Help parancsmag használatával. Például a Get-Service parancsmag súgójának megjelenítéséhez írja be:

```
Get-Help Get-Service
```
A legtöbb parancsmagok hozható létre az objektumokat, amely nem kezelhetők, és majd nyújtott be a megjelenítendő szöveg. Teljes megértéséhez, hogy a parancsmag kimenete, átadhatja a Get-tag parancsmag kimenete. Például a következő parancsot a Get-Service parancsmaggal a objektum kimeneti tagjai információkat jelenít meg.

```
Get-Service | Get-Member
```

### <a name="consistency"></a>Consistency
Rendszerek kezelése egy összetett feladat lehet, és szabályozására rejlő összetettségét súgó eszközt, amely egységes illesztőfelületet. Sajnos nem parancssori eszközök, és nem alkalmas parancsfájlok futtatására COM-objektumok az előzőekben azok konzisztencia.

A Windows PowerShell konzisztenciájának az egyik elsődleges eszközei. Például ha megtanulhatja a rendezési-Object parancsmag használatával, használhatja ezt az információt rendezéséhez bármely parancsmag kimenetét. Nincs a különböző rendezési rutinok minden parancsmag további.

Parancsmag fejlesztők továbbá nem rendelkeznek a parancsmagok rendezési szolgáltatások tervezéséhez. A Windows PowerShell ad nekik a keretrendszer, amely az alapszintű funkciókat biztosítja, és kényszeríti a konzisztens interfész sok szempontból kapcsolatban. A keretrendszer nem néhány a lehetőségeket, amelyek általában a fejlesztők megmaradnak, de ismét, így hatékony és könnyen használható parancsmagok teljes körű fejlesztésével jóval egyszerűbb.

### <a name="interactive-and-scripting-environments"></a>Interaktív és parancsfájl-kezelési környezet
A Windows PowerShell egy kombinált interaktív és parancsfájl-kezelési környezet, amely hozzáférést biztosít a parancssori eszközök és a COM-objektumok, és is lehetővé teszi a teljesítmény a .NET Framework Class Library (FCL) használatát.

Ebben a környezetben, a Windows parancssor, amely több parancssori eszközökkel interaktív környezetet biztosít az javítja. Azt is javítja a Windows Script Host (WSH) parancsfájlok, amelyek lehetővé teszik több parancssori eszközök és a COM-automatizálási objektumok használata, de nem ad meg egy interaktív környezetben.

Ezek a funkciók eléréséhez kombinálásával Windows PowerShell az interaktív felhasználó és a parancsfájl-író képességét, és rendszer-felügyeleti még kezelhetőbbé teszik.

### <a name="object-orientation"></a>Objektum tájolását
Írja be a parancsok szöveg kommunikálni a Windows PowerShell, bár a Windows PowerShell objektumokat, nem szöveges alapul. A parancs eredménye egy objektumot. A kimeneti objektum bemenetként egy másik parancsba is küldhet. Ennek eredményeképpen Windows PowerShell felületet biztosít a megszokott új és hatékony parancssori paradigma bevezetése mellett egyéb ismertetése ismerő személyek számára. A parancs teszi objektumok, nem pedig szöveg küldése közötti adatküldés fogalma kiterjed.

### <a name="easy-transition-to-scripting"></a>Egyszerű átmenet parancsfájlok
A Windows PowerShell írjanak átmenet egyszerűen parancsok interaktív módon való létrehozása és futtatása a parancsfájlok elérhetővé válnak. A Windows PowerShell parancssorába felderítéséhez a parancsok, amelyek a feladat elvégzésére parancsok adhatja meg. Ezt követően mentheti azokat a parancsokat a Beszélgetés szövegének vagy előzményeit előtt másolja őket egy fájl, amely parancsfájlként.