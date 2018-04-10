---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A Konzol panel használata a Windows PowerShell ISE-ben
ms.assetid: 44d67705-87c7-4a69-a53e-6471fdebb757
ms.openlocfilehash: 5bbbdd3b1f0324ff1a4f2298459f58640c4dc9a6
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="how-to-use-the-console-pane-in-the-windows-powershell-ise"></a>A Konzol panel használata a Windows PowerShell ISE-ben

A konzol ablaktáblában a a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) működik, akárcsak a Windows PowerShell ISE önálló konzolablakban.

A parancs futtatásához a konzol ablaktáblában írja be a parancsot, és nyomja le az ENTER BILLENTYŰT. Több, sorrendben végrehajtani kívánt parancs megadásához írja be a SHIFT + ENTER parancsok között. Lásd: [kiegészítést használja a parancsfájl és a konzol ablaktáblában hogyan](How-to-Use-Tab-Completion-in-the-Script-Pane-and-Console-Pane.md) segítségre parancsokat.

A parancs az eszköztáron kattintson **művelet leállítása**, vagy nyomja le a CTRL + BREAK billentyűkombinációt. CTRL + C segítségével is leállítási egy parancs, ha a környezet nem egyértelmű. Például ha valamilyen szöveget az aktuális ablaktáblán kiválasztva, majd CTRL + C hozzárendeli a másolási művelet.

A Windows PowerShell v3 verziótól kezdve a Tesztkimenet ablaktáblán lett kombinálva, a konzol ablaktáblában. Ez az előnye, hogy például különálló Windows PowerShell-konzolján viselkedik, és megszünteti az eljárást, amely volt szükség, ha a különálló különbségeit. képes vagy:

- Válassza ki, és a szöveg a konzol ablaktáblában másolása a vágólapra a Beillesztés bármely más ablakban. Válassza ki a szöveget, kattintson a lenyomva az egérrel a kimenet ablaktáblán közben az egérrel húzza a rögzíteni kívánt szöveg. A kurzor nyílbillentyűk üzem közben is használható **SHIFT** szöveg kijelöléséhez. Ezután nyomja meg a CTRL + C, vagy kattintson a **másolási** ikonra az eszköztárban.

- Illessze be a kijelölt szöveg, a jelenlegi kurzor pozíciójával. Kattintson a **Beillesztés** ikon az eszköztáron.

- Törölje a konzol ablaktáblában összes szöveget. A konzol ablaktáblában törléséhez kattintson a **konzolpanelen törölje** ikonra az eszköztárban, vagy futtassa a parancsot az **Clear-állomás** vagy az alias **cls**.

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE bemutatása](Introducing-the-Windows-PowerShell-ISE.md)