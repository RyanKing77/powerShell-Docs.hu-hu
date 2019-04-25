---
title: Windows PowerShell-modul írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bfbccc5b-2b2b-432a-a971-9f8ab503cdc3
caps.latest.revision: 17
ms.openlocfilehash: 3c6d8e410427d6cfaa1c15db421b3fe935f7d322
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082056"
---
# <a name="writing-a-windows-powershell-module"></a>Windows PowerShell-modul írása

Ez a dokumentum íródott, a parancsfájl a fejlesztők és a parancsmag fejlesztőknek szól, akik csomagolása és terjesztése a Windows PowerShell-parancsmagokat kell. Windows PowerShell-modulok használatával csomagot, és terjesztése a Windows PowerShell-megoldások lefordított nyelv használata nélkül.

Windows PowerShell-modulok lehetővé teszi, hogy a partíció, rendszerezheti és a Windows PowerShell-kód absztrakt önálló, újrafelhasználható egységekbe. Ezek újrafelhasználható egységgel egyszerűen oszthat meg másokkal közvetlenül a modulok. Ha a parancsfájl-fejlesztő, csomagolja újra külső modulról egyéni parancsfájl-alapú alkalmazások létrehozásához. Modulok, például a Perl, Python, és más programozási nyelven modulok hasonló, újrafelhasználható, szabadon terjeszthető összetevők használata további előnye, hogy ismételje meg a becsomagolást és absztrakt több összetevő lehetővé teszi, éles használatra kész-parancsfájl-kezelési megoldások engedélyezése egyéni megoldások létrehozásához.

A legalapvetőbb, a Windows PowerShell egy .psm1 fájlban modulként mentett érvényes Windows PowerShell parancsfájl kód kezeli. PowerShell bármilyen bináris parancsmag szerelvény modulként automatikusan is kezeli. Azonban használhatja egy modul (vagy még pontosabban egy moduljegyzék) szeretné a teljes megoldás együtt. A következő esetekben gyakori használati Windows PowerShell-modulok ismertetik.

### <a name="libraries"></a>Kódtárak

Modulok segítségével csomagolása és terjesztése javul kódtárakat, függvények, amelyek a leggyakoribb feladatok végrehajtását. Általában ezek a függvények nevei oszthat meg egy vagy több főneveket, amely mutatja, hogy ezek a gyakori feladat. Ezek a függvények is lehet .NET-osztályok hasonló abban, hogy a nyilvános és privát tagokat is rendelkeznek. Például egy könyvtár, Funkciók fájlátvitel tartalmazhat. Ebben az esetben a főnév szótárral kezdheti az általános feladatban lehet "fájl."

### <a name="configuration"></a>Konfiguráció

Modulok segítségével testre szabhatja környezete egyes parancsmagokat, a szolgáltatók, a functions és a változók hozzáadásával.

### <a name="compiled-code-development-and-distribution"></a>Lefordított kódot fejlesztési és terjesztési

A parancsmag és a szolgáltató fejlesztők modulok segítségével tesztelése és terjesztése a lefordított kódot anélkül, hogy a beépülő modulok létrehozása. A lefordított kódot modulként (bináris modult) tartalmazó szerelvény anélkül, hogy hozzon létre és regisztrálja a beépülő modulok importálhatja azokat.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-modul ismertetése](./understanding-a-windows-powershell-module.md)

[Egy PowerShell-szkript-modul írása](./how-to-write-a-powershell-script-module.md)

[Egy bináris PowerShell-modul írása](./how-to-write-a-powershell-binary-module.md)

[A PowerShell-modul jegyzék írása](http://msdn.microsoft.com/en-us/abe4c24b-e64e-4a61-81d5-18c4fceba0b6)

[A PSModulePath telepítési elérési út módosítása](./modifying-the-psmodulepath-installation-path.md)

[Egy PowerShell-modul importálása](./importing-a-powershell-module.md)

[Egy PowerShell-modul telepítése](./installing-a-powershell-module.md)
