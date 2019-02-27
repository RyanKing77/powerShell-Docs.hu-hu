---
title: Hogyan lehet hozzáadni egy lásd is szakasz szolgáltató súgótémakör |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9c754ac3-cee3-4c13-9bad-e499c8a68a09
caps.latest.revision: 4
ms.openlocfilehash: f5c48fd04c620828a6e99c5c5424d11b31fd10e5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848453"
---
# <a name="how-to-add-a-see-also-section-to-a-provider-help-topic"></a>„Lásd még” szakasz hozzáadása egy szolgáltatói súgótémakörhöz

Ez a szakasz azt ismerteti, hogyan töltse fel a **lásd még** szolgáltató súgótémakör szakaszában.

A **lásd még** szakasz témaköröket a szolgáltatóhoz kapcsolódó vagy segíthetnek a felhasználó jobb megismerésében és a szolgáltatóval áll. A témakör lehetnek parancsmag súgóját, szolgáltató Súgó és fogalmi ("tudnivalók") a Windows PowerShellben Súgó-témaköröket. Könyvekben, tanulmány és online témaköreit, beleértve az aktuális szolgáltató témakör online verzióját mutató hivatkozásokat is tartalmazhat.

Amikor online témaköröket, adja meg az URI-t vagy egyszerű szöveges keresési kifejezés. A `Get-Help` parancsmag nem hivatkozásra, és irányítsa át a listában a tájékozódhat. Emellett a `Online` paraméterében a `Get-Help` parancsmag nem működik a szolgáltató segítségével.

A Lásd még szakaszban alapján hozza létre a `RelatedLinks` elem és a benne található címkéket. A következő XML formátumú bemutatja, hogyan adja hozzá a címkéket.

### <a name="to-add-see-also-topics"></a>"Lásd még" témakörök hozzáadása

1. Az a *AssemblyName*belül a .dll-help.xml fájlt a `providerHelp` elem, adjon hozzá egy `RelatedLinks` elem. A `RelatedLinks` elemnek kell lennie az utolsó elem az a `providerHelp` elemet. Csak egy `RelatedLinks` elem engedélyezett a minden szolgáltató Súgó-témakör.

   Például:

    ```xml
    <providerHelp>
        <RelatedLinks>
        </RelatedLinks>
    </providerHelp>
    ```

2. Az egyes témakörében a **lásd még** szakasz belül a `RelatedLinks` elem, adjon hozzá egy `navigationLink` elem. Ezt követően belül `navigationLink` elem, vegyen fel egy `linkText` elem és a egy `uri` elemet. Ha nem használ a `uri` elemben adhatja hozzá őket egy üres elemeként (\<uri / >).

   Például:

    ```xml
    <providerHelp>
        <RelatedLinks>
            <navigationLink>
                <linkText> </linkText>
                <uri> </uri>
            </navigationLink>
        </RelatedLinks>
    </providerHelp>
    ```

3. Írja be a témakör nevét között a `linkText` címkék. Ha meg van adva egy URI-t, írja be között a `uri` címkék. Az aktuális szolgáltató témakör online verzióját között jelzi a `linkText` címkék, típus "Online verzió:" a témakör neve helyett. Általában a "Online verzió:" hivatkozás az első témakörében a Lásd még a témakör listában.

   Az alábbi példa három lásd még témakörök tartalmazzák. Az első tekintse meg az aktuális témakör online verzióját. A második egy Windows PowerShell parancsmag súgó-témakörének hivatkozik. A harmadik hivatkozik egy online témakört.

    ```xml
    <providerHelp>
        <RelatedLinks>
            <navigationLink>
                <linkText> Online version: </linkText>
                <uri>http://www.fabrikam.com/help/myFunction.htm</uri>
            </navigationLink>
            <navigationLink>
                <linkText> about_functions </linkText>
                <uri/>
            </navigationLink>
            <navigationLink>
                <linkText> Windows PowerShell Getting Started Guide </linkText>
                <uri>http://go.microsoft.com/fwlink/?LinkID=89597<uri/>
            </navigationLink>
        </RelatedLinks>
    </providerHelp>
    ```