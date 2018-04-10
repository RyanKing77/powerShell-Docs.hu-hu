---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja
ms.assetid: d176a131-ab0c-43ee-80c1-f824ab8e4a05
ms.openlocfilehash: fd5ac2c34b173d4eba7636bb5760b1ac9abb4277
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="purpose-of-the-windows-powershell-ise-scripting-object-model"></a>A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja

Objektum társítva az űrlap és a funkció a Windows PowerShell integrált parancsfájlkezelési környezet (ISE). Az objektumhivatkozás modell ismerteti a tag tulajdonságai és metódusai, ezek az objektumok visszaállítását. Példák bemutatják, hogyan használható parancsfájlok közvetlenül elérje ezeket a metódusokat és tulajdonságok állnak rendelkezésre. A parancsfájl-kezelési objektummodell megkönnyíti a feladatok a következő tartományban kell lennie.

## <a name="customizing-the-appearance-of-windows-powershell-ise"></a>A Windows PowerShell ISE megjelenésének testreszabása

Csak akkor használhatja az objektum az alkalmazásbeállítások és a beállítások módosításához. Például módosíthatja azokat az alábbiak szerint:

- Módosíthatja a hibák, figyelmeztetések, részletes kimenetének színét, és a hibakeresési kimenete.
- Get, vagy a parancssori ablaktáblában, a kimeneti ablaktábla és a parancssori panelbe a háttérszíneket.
- Beállíthatja, hogy a kimeneti ablaktábla előtérszínét.
- A Windows PowerShell ISE betűtípusok és betűméret adhatja meg.
- Beállíthatja a figyelmeztetések. Ez a beállítás, amelyeket a fájl megnyitásakor, több PowerShell lap, vagy ha a fájl a parancsfájl futtatása előtt a fájl mentését figyelmeztetések tartalmazza.
- Egy nézet, ha a parancsfájl és a kimeneti ablaktábla nem egymás melletti és nézet között válthat a parancssori panelbe esetén fölött a Tesztkimenet ablaktáblán. A parancs ablaktábla rögzítheti az alsó vagy felső részén a Tesztkimenet ablaktáblán.

## <a name="enhancing-the-functionality-of-windows-powershell-ise"></a>A Windows PowerShell ISE működésére növelése

Csak akkor használhatja a objektum javítása érdekében a Windows PowerShell ISE működésére. Például a következőket teheti:

- Adja hozzá, és a Windows PowerShell ISE maga-példányt módosító. Például a menük módosításához, hozzáadhat új menüpontok és az új menüelemek leképezése parancsfájlok.
- Hozzon létre olyan parancsfájlok, amelyek a Windows PowerShell ISE menüparancsai és gombok segítségével elvégezhető feladatok elvégezhetők. Például hozzáadhat, távolítsa el, vagy válasszon egy PowerShell lapon.
- Parancsok és gombok segítségével végrehajtható feladatok komplemens számnak. Átnevezheti például a PowerShell-lapon.
- Szöveg pufferek a parancs ablaktáblán, a kimeneti ablaktábla és a parancssori panelbe fájl társított kezelheti. Például a következőket teheti:
  - Futtasson, vagy a teljes szöveg.
  - GET, vagy adjon meg egy kijelölt szöveg.
  - Futtassa a parancsfájlt, vagy futtassa a parancsfájlt kijelölt része.
  - Egy sor görgessen nézetbe.
  - Helyezze be a szöveget egy kalap pozíciójában.
  - Jelöljön ki egy szöveget.
  - Első sor utolsó száma.
- Végre fájlműveleteket. Például a következőket teheti:
  - Nyisson meg egy fájlt, mentse a fájlt, vagy mentse a fájlt egy másik nevet.
  - Határozza meg, hogy a fájl legutóbbi mentése megváltozott-e.
  - Beolvasni a fájlnevet.
  - Válasszon ki egy fájlt.

## <a name="automating-tasks"></a>Feladatok automatizálása

A parancsfájl-kezelési hálózatiobjektum-modellt hozhat létre a billentyűparancsok, gyakori műveletekhez.

## <a name="see-also"></a>Lásd még:

- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)