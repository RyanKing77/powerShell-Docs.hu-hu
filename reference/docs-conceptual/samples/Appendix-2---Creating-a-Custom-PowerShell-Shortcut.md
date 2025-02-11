---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: '2\. függelék: Egyéni PowerShell-parancsikon létrehozása'
ms.openlocfilehash: 6f1a6a8187b1797103e3620b2cf9155978807ea5
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030305"
---
# <a name="appendix-2---creating-a-custom-powershell-shortcut"></a>2 – egyéni PowerShell-parancsikon létrehozása. függelék:

Az alábbi eljárás ismerteti, hogyan lehet parancsikon létrehozása a Windows PowerShell parancsmag, amely a testre szabott beállítások több kényelmes érhetők el.

1. Hozzon létre egy hivatkozást, amely a Powershell.exe mutat.

2. Kattintson a jobb gombbal a parancsikonra, majd kattintson **tulajdonságok**.

3. Kattintson a **beállítások** fülre.

4. Az a **beállítások szerkesztése** szakaszban jelölje be a **Gyorsszerkesztés** jelölőnégyzetet.

    Ez a beállítás lehetővé teszi a Windows PowerShell-konzolablakot lévő szöveg kijelölése a bal oldali gombbal húzásával, és lehetővé teszi, hogy a szöveg másolása a vágólapra ENTER billentyű lenyomásával, vagy kattintson a jobb gombbal az egérrel.

5. Az a **beállítások szerkesztése** szakaszban jelölje be a **mód Insert** jelölőnégyzetet. Ez a beállítás lehetővé teszi, hogy, kattintson a jobb gombbal a konzolablakban automatikusan beilleszteni a vágólapra másolt szöveget.

6. Az a **eszközparancs-előzmények** szakaszban adja meg egy 1 és 999 közötti a számot a **puffer mérete** mezőbe. Ez beállítja a konzol pufferben megtartott parancsok beírásával számát.

7. Az a **eszközparancs-előzmények** szakaszban jelölje be a **Régi előfordulások törlése** melletti jelölőnégyzetet, hogy a konzol puffer ismétlődő parancsokat kiküszöbölése.

8. Kattintson a **elrendezés** fülre.

9. Az a **Képernyőpufferen** területén adjon meg egy 1 és 9999 közötti számot a **magasság** mezőbe. A magasságot kimenete pufferelve van sornyi számát jelöli. Ez a megőrzött meg, ha a konzolablakban görgetve sorok maximális számát. Ez a szám kisebb-e a magasságát, ahogyan a **ablakméret** szakaszban az ablak mérete magassága automatikusan csökken az ugyanarra az értékre.

10. Az a **ablakméret** területén adjon meg egy számot 1 és 9999 a szélesség között. Ez jelöli, amelyek között a konzolablakban jelennek karakterek száma. Az alapértelmezett szélesség értéke 80, és a Windows PowerShell-kimeneti formázás a szélesség lett tervezve.

11. Ha el szeretné helyezni az asztalon, egy adott időpontban a konzolon, ha meg van nyitva, törölje a **a rendszer helyezi** jelölőnégyzetet a **ablak helyének** szakaszt, és módosítsa az értékeket a a **Balra** és **felső** lévő a **ablak helyének** szakaszban.

12. Kattintson az **OK** gombra.
