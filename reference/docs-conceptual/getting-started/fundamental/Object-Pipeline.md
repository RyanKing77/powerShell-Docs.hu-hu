---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: Objektum folyamat
ms.assetid: 523d8ae4-d743-47a4-b79a-806130ca688a
ms.openlocfilehash: 3fa41cc744cf3ab66fc5ef186ead8eb919429a76
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="object-pipeline"></a>Objektum folyamat
Folyamatok működni, mint egy láncolata csatlakoztatott cső. A feldolgozási sor mentén cikkek továbbítása minden szegmensben. Folyamatokat létrehozni a Windows PowerShellben, csatlakozzon a parancsok és az adatcsatorna operátor "|}". Minden parancs a következő parancs kimenete szolgál.

Folyamatok késései a számára a legértékesebb koncepció használt parancssori felületen. Megfelelően használják, adatcsatornák nem csak csökkenti a szükséges munka mennyiségét, az összetett parancsok megadásához, de is megkönnyítik a parancsokban munkahelyi áramló megjelenítéséhez. Egy kapcsolódó hasznos folyamatok jellemzője, ugyanis működésük egyes elemek külön-külön, nem kell módosítani őket e hogy nulla, egy vagy több elem a feldolgozási alapján. Továbbá minden egyes parancsot egy folyamat (más néven a feldolgozási sor elem) általában átadja a kimenetet a csővezeték--elem a következő parancsot. Ez általában csökkenti a erőforrás igény szerinti összetett parancsok, és lehetővé teszi, hogy a kimeneti azonnal első megkezdése.

Ebben a fejezetben azt fogja ismertetik, hogyan a Windows PowerShell kimenetátirányítási mechanizmusával eltér-e a legnépszerűbb ismertetése a folyamatok, és majd mutassa be néhány alapvető eszközök ellenőrzési folyamat kimeneti és is érdekében tekintse meg, hogyan működik, a folyamat használhat.

