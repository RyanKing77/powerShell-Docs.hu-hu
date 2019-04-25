---
title: A Windows PowerShell-szolgáltató létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- providers [PowerShell Programmer's Guide]
- providers [PowerShellProgrammer's Guide], creating
- Windows PowerShell Programmer's Guide, providers
ms.assetid: 863e48e9-7206-4c6a-a59a-2ab2d30396bc
caps.latest.revision: 5
ms.openlocfilehash: 06910f32752668f13400f9be0767a2179133df04
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081750"
---
# <a name="how-to-create-a-windows-powershell-provider"></a>Windows PowerShell-szolgáltató létrehozása

Ez a szakasz azt ismerteti, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban. Egy Windows PowerShell-szolgáltatóban kétféle módon lehet tekinteni. A felhasználó számára, hogy a szolgáltató a tárolt adatok egy készletét jelöli. A tárolt adatok lehetnek például az Internet Information Services (IIS) metabázis, a Microsoft Windows beállításjegyzék, a Windows fájlrendszerben, az Active Directory és a Windows PowerShell változót és az alias adataihoz.

A fejlesztők a Windows PowerShell-szolgáltató a felhasználó és az adatokat, amelynek hozzá kell a felhasználó közötti illesztőfelületet. A szempontból minden típusú szolgáltató ebben a szakaszban leírt támogat egy adott alaposztályok és a felületek, amelyek lehetővé teszik a Windows PowerShell-modul egyik elterjedt módja az egyes parancsmagok a felhasználó számára elérhetővé.

## <a name="providers-provided-by-windows-powershell"></a>Windows PowerShell által biztosított szolgáltatók

Windows PowerShell számos szolgáltató (például a fájlrendszer-szolgáltatót, a beállításjegyzék-szolgáltatója és a szolgáltató Alias) ismert adattárak eléréséhez használt biztosít. További információ a Windows PowerShell által biztosított szolgáltatók használja a következő parancsot az online súgó elérése:

**PS > get-help about_providers**

## <a name="accessing-the-stored-data-using-windows-powershell-paths"></a>A Windows PowerShell-elérési utak használata tárolt adatok elérése

A Windows PowerShell-modult, és parancsokat programozott módon révén Windows PowerShell-elérési utak Windows PowerShell-szolgáltatók érhetők el. A legtöbb esetben az elérési utak a szolgáltatón keresztül az adatok közvetlen elérésére szolgál. Azonban néhány elérési utak feloldható legyen a provider – belső elérési utak, amelyek lehetővé teszik a parancsmag a Windows PowerShell alkalmazásprogramozási felületek (API-k) használata az adatok eléréséhez. Hogyan működnek a Windows PowerShell-szolgáltatók Windows Powershellen belülről kapcsolatos további információkért lásd: [Windows PowerShell működése](http://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58).

## <a name="exposing-provider-cmdlets-using-windows-powershell-drives"></a>Meghajtók adatokhoz hozzáférést biztosító szolgáltató parancsmagok Windows PowerShell-lel

A Windows PowerShell-szolgáltató használatával a virtuális Windows PowerShell-meghajtók támogatott parancsmagjához tesz elérhetővé. Windows PowerShell a Windows PowerShell-meghajtó a következő szabályok érvényesek:

- Meghajtó neve lehet bármely alfanumerikus feladatütemezési.

- A meghajtó elérési útvonalon, "root" nevű érvényes bármikor adható meg.

- Meghajtó a tárolt adatok, nem csak a fájlrendszer valósítható meg.

- Minden olyan meghajtó biztosítja, hogy a saját aktuális működő helyét, lehetővé téve a felhasználó helyi megőrzendő időeltolású meghajtó között.

## <a name="in-this-section"></a>A szakasz tartalma

A következő táblázat felsorolja a témakörök, amelyek tartalmazzák a egymásra épülnek hitelesítésikód-példák. A második témakör kezdve az alapvető Windows PowerShell-szolgáltatóban inicializálva, és a Windows PowerShell-modul által nem inicializált, a következő témakörben funkciókat ad hozzá az adatokhoz fér hozzá, a következő témakörben az adatokat (kezelésére szolgáló funkciókkal bővíti a az elemek a tárolt adatok), és így tovább.

|Témakör|Meghatározás|
|-----------|----------------|
|[A Windows PowerShell-szolgáltató tervezése](./designing-your-windows-powershell-provider.md)|Ez a témakör ismerteti a dolgokat, érdemes lehet egy Windows PowerShell-szolgáltatóban implementálása előtt. Azt a Windows PowerShell szolgáltató alaposztályok és a használt felületek foglalja össze.|
|[Egy alapszintű Windows PowerShell-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md)|Ez a témakör bemutatja, hogyan hozhat létre, amely lehetővé teszi a Windows PowerShell modul inicializálása és meghívná a szolgáltató egy Windows PowerShell-szolgáltatóban.|
|[A Windows PowerShell meghajtót szolgáltató létrehozása](./creating-a-windows-powershell-drive-provider.md)|Ez a témakör bemutatja, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, amely lehetővé teszi a felhasználó elérheti egy adattár keresztül egy Windows PowerShell meghajtót.|
|[A Windows PowerShell elem szolgáltató létrehozása](./creating-a-windows-powershell-item-provider.md)|Ez a témakör bemutatja, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, amely lehetővé teszi a felhasználó módosíthatja a cikkeket a tárolóban.|
|[A Windows PowerShell tároló szolgáltató létrehozása](./creating-a-windows-powershell-container-provider.md)|Ez a témakör bemutatja, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, amely lehetővé teszi a felhasználó többrétegű adattárak működjön.|
|[A Windows PowerShell navigációs szolgáltató létrehozása](./creating-a-windows-powershell-navigation-provider.md)|Ez a témakör bemutatja, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, amely lehetővé teszi a felhasználó az adattár elemeit hierarchikus elrendezését.|
|[Egy Windows PowerShell-tartalmat szolgáltató létrehozása](./creating-a-windows-powershell-content-provider.md)|Ez a témakör bemutatja, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, amely lehetővé teszi a felhasználó a adattárban lévő cikkek tartalmának módosítására.|
|[A Windows PowerShell-tulajdonság szolgáltató létrehozása](./creating-a-windows-powershell-property-provider.md)|Ez a témakör bemutatja, hogyan hozhat létre egy Windows PowerShell-szolgáltatóban, amely lehetővé teszi a felhasználó a adattárban lévő elemek tulajdonságainak módosítására.|

## <a name="see-also"></a>Lásd még:

[Hogyan működik a Windows PowerShell](http://msdn.microsoft.com/en-us/ced30e23-10af-4700-8933-49873bd84d58)

[Windows PowerShell SDK](../windows-powershell-reference.md)

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)
