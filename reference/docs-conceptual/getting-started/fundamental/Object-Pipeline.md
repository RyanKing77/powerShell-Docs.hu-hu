---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Objektumfolyamat
ms.assetid: 523d8ae4-d743-47a4-b79a-806130ca688a
ms.openlocfilehash: 6102ec6e8fbf38fdc2bc5fa9c583244ef639dec8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="object-pipeline"></a>Objektumfolyamat
Folyamatok működni, mint egy láncolata csatlakoztatott cső. A feldolgozási sor mentén cikkek továbbítása minden szegmensben. Folyamatokat létrehozni a Windows PowerShellben, csatlakozzon a parancsok és az adatcsatorna operátor "|}". Minden parancs a következő parancs kimenete szolgál.

Folyamatok késései a számára a legértékesebb koncepció használt parancssori felületen. Megfelelően használják, adatcsatornák nem csak csökkenti a szükséges munka mennyiségét, az összetett parancsok megadásához, de is megkönnyítik a parancsokban munkahelyi áramló megjelenítéséhez. Egy kapcsolódó hasznos folyamatok jellemzője, ugyanis működésük egyes elemek külön-külön, nem kell módosítani őket e hogy nulla, egy vagy több elem a feldolgozási alapján. Továbbá minden egyes parancsot egy folyamat (más néven a feldolgozási sor elem) általában átadja a kimenetet a csővezeték--elem a következő parancsot. Ez általában csökkenti a erőforrás igény szerinti összetett parancsok, és lehetővé teszi, hogy a kimeneti azonnal első megkezdése.

Ebben a fejezetben azt fogja ismertetik, hogyan a Windows PowerShell kimenetátirányítási mechanizmusával eltér-e a legnépszerűbb ismertetése a folyamatok, és majd mutassa be néhány alapvető eszközök ellenőrzési folyamat kimeneti és is érdekében tekintse meg, hogyan működik, a folyamat használhat.