---
ms.date: 08/23/2018
keywords: PowerShell, a parancsmag
title: Fontos PowerShell fogalmainak megértése
ms.assetid: 3e601e38-4520-4578-a48d-b6779f1d35ee
ms.openlocfilehash: 5f8192f962cebb8ee5e5384e39b48de811b11003
ms.sourcegitcommit: 59727f71dc204785a1bcdedc02716d8340a77aeb
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/28/2018
ms.locfileid: "43134240"
---
# <a name="understanding-important-powershell-concepts"></a>Fontos PowerShell fogalmainak megértése

A PowerShell-tervezési fogalmak számos különböző környezetekben történő integrálható. A fogalmak számos parancskörnyezet vagy programozási környezetben kezelőfelülettel személyek ismerős lesz. Azonban néhány személy fog tudni ezek mindegyike. Ezek a fogalmak némelyike megnézzük a rendszerhéj hasznos áttekintést nyújt.

## <a name="output-is-object-based"></a>Objektum alapú kimenete

Ellentétben a hagyományos parancssori felületen a PowerShell-parancsmagok objektumok kezelésére tervezték.
Egy objektum, amely több, mint a karakterlánc, a képernyőn megjelenő strukturált adatokat. A parancs kimenete mindig hajtja további információt, amelyet használhat, ha szüksége lesz rá.

Ha már használta a szöveg – a feldolgozás eszközök múltbeli adatok feldolgozásához, látni fogja, hogy azok eltérően viselkednek a PowerShell használatakor. A legtöbb esetben nem kell szöveg – a feldolgozás eszközök konkrét információk kinyeréséhez. Közvetlenül érheti el a PowerShell szabványos objektum-szintaxis használatával az adatok egyes részeit.

## <a name="the-command-family-is-extensible"></a>A parancs termékcsalád bővíthető

Felületek, például a Cmd.exe lehetőséget, hogy közvetlenül a beépített parancsa beállítása nem biztosíthat.
Külső parancssori eszközök, amely a Cmd.exe hozhat létre. De ezek külső eszközök nincs súgó integrációs szolgáltatások. A Cmd.exe automatikusan nem ismert, hogy a külső eszközök-e érvényes parancsokat.

A natív parancsokat a PowerShell nevezzük *parancsmagok* (ejtsd parancs-lehetővé teszi, hogy). Létrehozhat saját parancsmagok modulokat, és függvények használatával összeállított programkódban vagy szkriptekben. Modulok parancsmagok és szolgáltatók hozzáadhatja a rendszerhéjat. PowerShell-parancsfájlokat, amelyek hasonló UNIX shell-szkript és a Cmd.exe kötegelt fájlokat is támogatja.

## <a name="powershell-handles-console-input-and-display"></a>PowerShell konzolon bemeneti és a megjelenített kezeli

A parancs beírásakor PowerShell mindig dolgozza fel a parancssori bemenet közvetlenül. PowerShell is formázza a kimenet a képernyőn látható. Ez a különbség azért fontos, mert csökkentik az egyes parancsmag szükséges munkát. Ez biztosítja, hogy mindig műveleteket végezheti el bármilyen parancsmaggal ugyanúgy. A parancsmag a fejlesztők nem kell elemezni a parancssori argumentumokat, vagy formázza a kimeneti kód írása.

A hagyományos parancssori eszközökkel rendelkezik saját rendszerek és a Súgó megjelenítése. Egyes parancssori eszközök használata **/?** a Súgó megjelenített; aktiválásához mások **-?**, **/H**, vagy akár **//**. Néhány súgó jelenik meg a grafikus felhasználói felület ablakban, és nem jelennek meg a konzolon. Használja a megfelelő paramétert, ha az eszköz előfordulhat, hogy hagyja figyelmen kívül mit írt be, és automatikusan a feladat végrehajtásának elindításához.
Mivel PowerShell automatikusan elemzi, és feldolgozza a parancssorban a **-?** paraméter mindig jelenti a "show me Súgó parancs".

> [!NOTE]
> Ha egy grafikus alkalmazást futtatja a PowerShell, az alkalmazás az ablak nyílik meg.
> PowerShell inkonzisztensek, csak ha feldolgozása a parancssori bemenet, ellátási vagy az alkalmazás kimenete a konzolablakban vissza. Hogyan működik az alkalmazás belső nincs hatással.

## <a name="powershell-uses-some-c-syntax"></a>PowerShell néhány C# szintaxisát használja.

PowerShell a .NET-keretrendszer épül. Egyes szintaxis szolgáltatások és a kulcsszavak azt megosztja a C# programozási nyelv. PowerShell megismeréséhez teheti, hogy sokkal könnyebben tanulhatja a C#. Ha már ismeri a C#, ezek Hasonlóságok teheti könnyebben PowerShell megismeréséhez.