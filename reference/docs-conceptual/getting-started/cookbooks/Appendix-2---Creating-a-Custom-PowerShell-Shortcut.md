---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: '2. függelék: Egyéni PowerShell-parancsikon létrehozása'
ms.assetid: 5d4fd421-5d43-4ec7-86fd-acfe887b066e
ms.openlocfilehash: e8081b7a64d313c8ef4bbccf95f250445dd68ad9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30949264"
---
# <a name="appendix-2---creating-a-custom-powershell-shortcut"></a>Függelék: 2 - egyéni PowerShell parancsikon létrehozása

Az alábbi eljárás ismerteti, hogy a program számos kényelmes testre szabott Windows PowerShell parancsikon létrehozása.

1. Hozzon létre egy parancsikont, amely a PowerShell.exe.

2. Kattintson a jobb gombbal a parancsikonra, és kattintson **tulajdonságok**.

3. Kattintson a **beállítások** fülre.

4. Az a **beállítások szerkesztése** szakaszban jelölje be a **gyorsszerkesztési** jelölőnégyzetet.

    Ez a beállítás lehetővé teszi a szöveget a Windows PowerShell konzol ablakban a bal oldali egérgombbal húzással ki, és lehetővé teszi, hogy a szöveg másolása a vágólapra ENTER billentyű megnyomásával, vagy kattintson a jobb gombbal az egérrel.

5. Az a **beállítások szerkesztése** szakaszban jelölje be a **beszúrási módban** jelölőnégyzetet. Ez a beállítás lehetővé teszi a kattintson a jobb gombbal a konzolablakban automatikusan illessze be a vágólapra másolt szöveget.

6. Az a **parancselőzmények** szakaszban adja meg vagy válasszon egy 1 és 999 a közötti számot a **pufferméret** mezőbe. Ez beállítja a konzol pufferben megtartott parancsok száma.

7. Az a **parancselőzmények** szakaszban jelölje be a **régi ismétlődések vetni** elkerülése érdekében a konzol pufferből ismételt parancsok jelölőnégyzetet.

8. Kattintson a **elrendezés** fülre.

9. Az a **képernyőpuffer** területen írja be egy 1 és 9999 közötti számot a **magasság** mezőbe. A magasság kimenete pufferelve van-e vonalak számát jelöli. Ez az maradnak meg, ha a konzolablakban görgetése sorok maximális számát. Ha ez a szám nem éri el a magasság látható a **ablakméret** szakaszában, az ablak mérete magassága automatikusan csökken ugyanarra az értékre.

10. Az a **ablakméret** területen írja be egy 1 és 9999 a szélesség közötti számot. Ez jelenti, hogy a karakterek, amelyek között a konzolablakban jelennek meg. Az alapértelmezett vonalvastagságot 80-as, és a szélesség készült Windows PowerShell kimeneti formázás.

11. Ha el szeretné helyezni a konzol adott helyen az asztalon, ha meg van nyitva, törölje a **a rendszer helyezi** jelölőnégyzetet a **ablak pozícióját** szakaszt, és módosítsa az értékeket a a **Balra** és **felső** mezőkben az a **ablak pozícióját** szakasz.

12. Kattintson az **OK** gombra.