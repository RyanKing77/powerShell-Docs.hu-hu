---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Fontos Windows PowerShell alapfogalmainak ismertetése"
ms.assetid: 3e601e38-4520-4578-a48d-b6779f1d35ee
ms.openlocfilehash: 1ffcfefcc7ffc7c98ba4d1e3ccc9a59cd9b0baac
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="understanding-important-windows-powershell-concepts"></a>Fontos Windows PowerShell alapfogalmainak ismertetése
A Windows PowerShell-kialakítás számos különböző környezetek fogalom egyesíti. Ezek az adott parancskörnyezet vagy programozási környezetben révén személyek számára ismerős, de nagyon kevés személyek fogja tudni az összes. Ezek a fogalmak némelyike megnézi a rendszerhéj hasznos áttekintést nyújt.

### <a name="commands-are-not-text-based"></a>Parancsok nincsenek szöveges
Hagyományos parancssori felület parancsok, parancsmagok úgy tervezték, hogy az objektumok - kezelését Windows PowerShell eltérően strukturált, nem csak egy karakterlánc, a képernyőn megjelenő információkat. A parancskimenet mindig hordoz magában, mentén további információt, amely akkor használhatja, ha esetleg szükség lenne rá. Ez a témakör a jelen dokumentum részletesen ismertetik.

Szöveg – a feldolgozás eszközök segítségével parancssori adatok feldolgozása a múltban, ha megtalálja, hogy azok viselkedése rendellenes próbálja használni őket a Windows PowerShellben. A legtöbb esetben nem kell szöveg – a feldolgozás eszközök adott információkat. Az adatok egy részének közvetlenül a szabványos Windows PowerShell objektum adatkezelési parancsok segítségével végezheti el.

### <a name="the-command-family-is-extensible"></a>A parancs termékcsalád bővíthető.
Például a Cmd.exe felületek nem rendelkezik, így az a beépített parancskészlethez közvetlenül bővítése. Külső parancssori eszközök, a Cmd.exe futtató hozhat létre, de a külső eszközök nem rendelkeznek a szolgáltatások, például súgó integrációs, és Cmd.exe automatikusan tudja, hogy azok érvényes parancsokat.

A natív bináris parancsokat a Windows PowerShellben, úgynevezett *parancsmagok* (jelentős parancs-segítségével), a parancsmagok az Ön által létrehozott és hozzáadni kívánt Windows PowerShell beépülő modul használatával kiegészíthető. A Windows PowerShell *beépülő modulok* fordításának, csakúgy, mint bármely más felületen bináris eszközök. A Windows PowerShell-hitelesítésszolgáltatókat adhat hozzá a rendszerhéj, valamint a új parancsmagokat használhatja őket.

A belső Windows PowerShell-parancsok speciális jellege miatt hivatkozik rájuk, *parancsmagok*.

> [!NOTE]
> Windows PowerShell parancsok, parancsmagok nem futtathatók. Azt fogja nem lehet megvitatása azokat a Windows PowerShell felhasználói útmutatója részletesen, de parancs típusú kategóriákként tudnia hasznosak lehetnek. A Windows PowerShell parancsfájlok, amelyek UNIX rendszerhéj-parancsfájlok és a Cmd.exe parancsfájlokat hasonló, de egy .ps1 fájlnévkiterjesztéssel rendelkeznek támogatja. A Windows PowerShell is hozhat létre, amely közvetlenül a felületen vagy parancsfájlokban használható belső funkciók.

### <a name="windows-powershell-handles-console-input-and-display"></a>A Windows PowerShell leírók konzol bemeneti és megjelenítése
A parancs beírásakor a Windows PowerShell mindig dolgozza fel a parancssori bemenet közvetlenül. A Windows PowerShell is formázza a kimenete a a képernyőn látható. Ez azért fontos, mivel csökkenti a szükséges minden egyes parancsmag munka és biztosítja, hogy mindig műveleteket végezheti el a ugyanúgy, függetlenül attól, milyen parancsmag használatával. Egy példa hogyan élettartama Ez leegyszerűsíti a eszköz fejlesztők és a felhasználók, a parancssori súgó.

Hagyományos parancssori eszközök rendelkeznek a saját sémákat és Súgó megjelenítése. Néhány parancssori eszközök használata **/?** a súgóablak; elindítása mások **-?**, **/H**, vagy akár  **//** . Súgó néhány jelenik meg a grafikus felhasználói Felülettel ablakban, nem pedig a konzolon megjelenített. Néhány bonyolult eszközöket, például az alkalmazás updaters belső fájlok a Súgó megjelenítése előtt csomagolja ki. A megfelelő paramétert használja, ha az eszköz lehet, hogy mi írt be, és a feladatütemezés végrehajtása automatikusan figyelmen kívül.

A parancs beírásakor a Windows PowerShell mindent meg automatikusan elemezni és előre dolgozza fel a Windows PowerShell. Ha használja a **-?** a paraméter egy Windows PowerShell-parancsmaggal, mindig jelent "megjelenítése Súgó a parancs". Parancsmag-fejlesztőknek nem kell elemezni a parancs; csak akkor kell adnia a súgószöveg.

Fontos megérteni, hogy a Súgó a Windows PowerShell számára elérhető a Windows PowerShell hagyományos parancssori eszközök futása közben is. A Windows PowerShell feldolgozza a paraméterek és az eredményeket a külső eszközök.

> [!NOTE]
> Ha egy grafikus alkalmazást a Windows PowerShellben, az alkalmazás ablak. A Windows PowerShell inkonzisztensek, csak ha feldolgozása a parancssori adjon meg, adjon meg vagy az alkalmazás kimeneti küld vissza a konzolablakban; Hogyan működik az alkalmazás belső nincs hatással.

### <a name="windows-powershell-uses-some-c-syntax"></a>A Windows PowerShell néhány C# szintaxist használja.
Windows PowerShell szintaxis funkciókat és nagyon hasonló a C# programozási nyelv, mert a Windows PowerShell-alapú a .NET-keretrendszer használtakon kulcsszavak rendelkezik. A Windows PowerShell könnyebben sokkal további C#, ha a nyelv érdekli.

Ha nem egy C# programozói, a hasonlóság nem fontos. Azonban ha már ismeri a C#, a közös vonásai teheti a Windows PowerShell sokkal könnyebben.

