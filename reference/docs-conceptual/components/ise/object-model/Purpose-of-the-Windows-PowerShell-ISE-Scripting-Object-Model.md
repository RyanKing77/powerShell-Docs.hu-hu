---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja
ms.assetid: d176a131-ab0c-43ee-80c1-f824ab8e4a05
ms.openlocfilehash: fd5ac2c34b173d4eba7636bb5760b1ac9abb4277
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404595"
---
# <a name="purpose-of-the-windows-powershell-ise-scripting-object-model"></a>A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja

Objektum társítva az űrlap és a funkció a Windows PowerShell integrált parancsfájlkezelési környezet (ISE). Az objektummodell-hivatkozás információt nyújt a tag tulajdonságai és metódusai, amelyek ezen objektumok teszik közzé. Példák bemutatják, hogyan használható parancsfájlok ezeket a metódusokat és tulajdonságokat közvetlen elérésére vannak megadva. A parancsfájl-kezelési objektummodell egyszerűbbé teszi a feladatok a következő tartományban.

## <a name="customizing-the-appearance-of-windows-powershell-ise"></a>A Windows PowerShell ISE-ben megjelenésének testreszabása

Használhatja a hálózatiobjektum-modellt az alkalmazásbeállítások és a beállítások módosításához. Például módosíthatja őket a következő:

- Módosíthatja a hibák, figyelmeztetések, részletes kimenetek színét, és hibakeresési adja vissza.
- Készítsen, vagy állítsa a háttérszínt a parancsot, a Tesztkimenet ablaktáblán, és a parancsfájl panelen.
- Beállíthatja, hogy az előtér színe a Tesztkimenet ablaktáblán.
- Beállíthatja a betűtípus neve és a betűméret a Windows PowerShell ISE-ben.
- Beállíthatja a figyelmeztetések. Ezzel a beállítással a fájl megnyitásakor, több PowerShell-lap, vagy ha a fájl a parancsfájl futtatása előtt a rendszer mentette a fájlt félhasználókkal rendelkező figyelmeztetéseket tartalmaz.
- A parancsfájl panelen és a kimeneti ablaktábla amelyeknél egymás melletti nézet és a egy nézet közötti válthat, ahol a parancsfájl panelen van felül a Tesztkimenet ablaktáblán. Rögzítheti a parancs ablaktábla alsó vagy felső részén a Tesztkimenet ablaktáblán.

## <a name="enhancing-the-functionality-of-windows-powershell-ise"></a>A Windows PowerShell ISE-ben funkciójának javítása

Használhatja a hálózatiobjektum-modellt a Windows PowerShell ISE-ben funkciójának javítása. Ha például a következőket teheti:

- Adja hozzá, és módosítsa a Windows PowerShell ISE-ben maga példányát. Például ha módosítani szeretné a menük, adjon hozzá új menüelemmel szabadon képezze le az új elemeket és parancsfájlok.
- Hozzon létre a parancsfájlok, amelyek a Windows PowerShell ISE-ben a parancsokhoz és a gombok segítségével elvégezhető feladatokat hajtanak végre. Például hozzáadhatja, távolítsa el, vagy válassza ki a PowerShell-lap.
- Kiegészítik a feladatok menü parancsai és gombok használatával elvégezhető. Átnevezheti például PowerShell-lap.
- Szöveg pufferek, társított egy fájlt a parancs panelen, a kimeneti ablaktábla és a parancsfájl panelen módosíthatja. Ha például a következőket teheti:
  - Szerezzen be, vagy a teljes szöveg.
  - Szerezzen be, vagy állítsa be a kijelölt szöveg.
  - Parancsfájl futtatása, vagy futtassa a parancsfájlt egy kiválasztott része.
  - Egy sor görgessen nézetben.
  - Szöveg beszúrása egy kalap pozíciónál.
  - Jelöljön ki egy szöveget.
  - Az utolsó sor beolvasása.
- Végre fájlműveleteket. Ha például a következőket teheti:
  - Nyisson meg egy fájlt, mentse a fájlt, vagy mentse a fájlt egy másik nevet.
  - Határozza meg, hogy egy fájl legutóbbi mentése után megváltozott-e.
  - A fájl nevének lekérése.
  - Válasszon ki egy fájlt.

## <a name="automating-tasks"></a>Feladatok automatizálása

A parancsfájl-kezelési objektummodell használhatja a gyakori műveletekhez használható billentyűparancsok létrehozásához.

## <a name="see-also"></a>Lásd még:

- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)