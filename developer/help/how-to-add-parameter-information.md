---
title: Paraméter-információk hozzáadása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cf6c1442-60aa-477a-8f30-ab02b1b11039
caps.latest.revision: 7
ms.openlocfilehash: d4a5fc934a41b00f89862674e44e4540680674f7
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083365"
---
# <a name="how-to-add-parameter-information"></a>Paraméteradatok hozzáadása

Ez a szakasz ismerteti, hogyan adhat hozzá a Paraméterek szakaszban, a parancsmag súgó-témakörének megjelenő tartalmat. A témakör a Paraméterek szakaszban megtalálja az összes, a parancsmag paramétereit, és minden paraméter részletes leírását.

A paraméterek szakasz tartalmát a Súgó-témakör szakaszának SZINTAXISA a tartalom összhangban kell lennie. A feladata a Súgó Szerző, győződjön meg arról, hogy a csomópont a szintaxist és a paraméterek hasonló XML-elemeket tartalmaz.

> [!NOTE]
> A súgófájl, nyissa meg a dll-Help.xml fájlok a Windows PowerShell telepítési könyvtárában található teljes megjelenítéséhez. Például a Microsoft.PowerShell.Commands.Management.dll-Help.xml fájl tartalma számos, a Windows PowerShell-parancsmagok számára.

### <a name="to-add-parameters"></a>Paraméterek hozzáadása

1. Nyissa meg a parancsmag Súgó-fájlt, és keresse meg a parancs csomópont vannak dokumentálja a parancsmaghoz. Hozzon létre egy új parancs csomópont kell új parancsmag hozzáadása. A súgófájl tartalmazza az egyes parancsmagok súgóját meg van adva, a parancs csomópont. Íme egy példa egy üres parancs csomópont.

    ```xml
    <command:command>
    </command:command>
    ```

2. A parancs csomóponton belül keresse meg a leírás csomópont, és paraméterek csomópont hozzáadása az alább látható módon. Paraméterek csak egy csomópont használata engedélyezett, és a szintaxis csomópont azonnal követnie kell.

    ```xml
    <command:command>
      <command:details></command:details>
      <maml:description></maml:description>
      <command:syntax></command:syntax>
      <command:parameters>
      </command:Parameters>
    </command:command>
    ```

3. A paraméterek csomóponton belül minden paraméter, a parancsmag paraméter csomópont hozzáadása alább látható módon.

   Ebben a példában egy paraméter csomópontot hozzáadják a három paramétert.

    ```xml
    <command:parameters>
      <command:parameter></command:parameter>
      <command:parameter></command:parameter>
      <command:parameter></command:parameter>
    </command:Parameters>
    ```

   Az azonos XML-címkéket, amelyek a szintaxis csomópont használja, és mivel az itt megadott paraméterek meg kell egyeznie a szintaxis csomópont által megadott paraméterek tartoznak, mert a paraméter csomópontok átmásolhatja a szintaxis csomópont, és illessze be őket a paraméterek csomópont. Azonban ügyeljen arra, hogy másolása paramétert csomópont csak egy példánya, még akkor is, ha a paraméter van megadva, a több paraméter állítja be a szintaxist.

4. Az egyes paraméterekhez tartozó csomópont, állítsa be az attribútumértékek, amelyek meghatározzák az egyes paraméterek jellemzőit. Ezek az attribútumok a következők: helyettesítés pipelineinput és pozíciójának megadása kötelező.

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
      </command:parameter>
      <command:parameter required="false" globbing="false"
               pipelineInput="false" position="named">
      </command:parameter>
      <command:parameter required="false" globbing="false"
               pipelineInput="false" position="named" ></command:parameter>
    </command:Parameters>
    ```

5. Az egyes paraméter csomópontok hozzáadása a paraméter neve. Íme egy példa a paraméter nevével, a paraméter csomópontot hozzáadni.

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
      </command:parameter>
    </command:Parameters>
    ```

6. Az egyes paraméter csomópontok hozzáadása a paraméter leírása. Íme egy példa a paraméter csomópont hozzáadott paraméter leírása.

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
        <maml:description>
          <maml:para> Add parameter description... </maml:para>
        </maml:description>
      </command:parameter>
    </command:parameters>
    ```

7. Minden paraméter csomópont esetében adja hozzá a .NET-keretrendszer typ parametru. A paraméter típusa a paraméter neve mellett jelenik meg.

   Íme egy példa a .NET-keretrendszer paramétertípus hozzáadva a paraméter csomópontra.

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
        <maml:description>
          <maml:para> Add parameter description... </maml:para>
        </maml:description>
        <dev:type> Add .NET Framework type... </dev:type>
      </command:parameter>
    </command:parameters>
    ```

8. Az egyes paraméter csomópontok hozzáadása a paraméter alapértelmezett értékét. A tartalom megjelenik a következő mondat hozzáadódik a paraméter leírása: Az alapértelmezett érték a "DefaultValue".

   Íme egy példa a paraméter alapértelmezett értéke a paraméter csomópontra kerül.

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
        <maml:description>
          <maml:para> Add parameter description... </maml:para>
        </maml:description>
        <dev:type> Add .NET Framework type... </dev:type>
        <dev:defaultvalue> Add default value...</dev:defaultvalue>
      </command:parameter>
    </command:parameters>
    ```

9. Minden paraméter, amely több érték tartozik a lehetséges értékek csomópontot.

   Íme egy példa a a lehetséges értékek csomópont, amely meghatározza a két lehetséges értéket a paraméterhez

    ```xml
    <dev:possiblevalues>
      <dev:possiblevalue>
        <dev:value>Unknown</dev:value>
        <maml:description>
          <maml:para></maml:para>
        </maml:description>
      /dev:possiblevalue>
      <dev:possiblevalue>
        <dev:value>String</dev:value>
        <maml:description>
          <maml:para></maml:para>
        </maml:description>
      </dev:possibleValue>
    </dev:possiblevalues>
    ```

Az alábbiakban néhány dolog láthat, amikor a-paramétereket adunk hozzá.

- A paraméter az attribútumok nem jelennek meg az összes nézetben megtekinthetők, a parancsmag Súgó-témakör. Azonban ezek jelennek meg a következő paraméter leírása, amikor a felhasználó kéri a teljes tábla (Get-Help \<cmdletname > – teljes) vagy paramétert (Get-Help \<cmdletname >-paraméter) nézetben, a következő témakörben.

- A paraméter leírása az egyik legfontosabb részeit egy parancsmag Súgó-témakör. A leírás rövid, valamint alapos kell lennie. Azt se feledje, hogy ha a paraméter leírása túl hosszú, például ha a két paramétert léphetnek kapcsolatba egymással, adhat hozzá további tartalmak, a parancsmag Súgó-témakör a megjegyzések szakasza.

  A paraméter leírása kétféle típusú információt biztosít.

- A parancsmag funkciója a paraméter használata esetén.

- Milyen jogi érték a paraméterhez.

- A paraméterértékek ki, a .NET-keretrendszer objektumként, mert felhasználók több információra van szüksége ezekre az értékekre, mint a hagyományos parancssori súgó lennének. A felhasználó értesítése, milyen típusú adatot a paraméter az célja, hogy fogadja el, és példákat is tartalmaznak.

A paraméter alapértelmezett értéke az érték, amely akkor használatos, ha a paraméter nincs megadva a parancssorban. Vegye figyelembe, hogy az alapértelmezett érték megadása nem kötelező, és nincs szükség van bizonyos paraméterek, például a szükséges paramétereket. A legtöbb nem kötelező paraméter alapértelmezett értékének kell adnia.

Az alapértelmezett érték a felhasználó nem használja a paraméterrel hatásának megértéséhez segítséget nyújt. Írja le az alapértelmezett érték nagyon kifejezetten, például az "aktuális könyvtár" vagy "Windows PowerShell telepítési könyvtárát ($pshome)" egy opcionális elérési útja. Az alapértelmezett beállítás, például a következő mondat használt leíró mondatok is kiírhatja a `PassThru` paramétert: "Ha PassThru nincs megadva, a parancsmag nem felel meg a folyamat objektumokat."  Emellett mert ellentétes a mező neve jelenik meg az értéket "**alapértelmezett érték**", "alapértelmezett érték" kifejezés szerepeljenek a bejegyzés nem kell.

Az alapértelmezett érték a paraméter nem jelenik meg az összes nézetben megtekinthetők, a parancsmag Súgó-témakör. Azonban, amikor a teljes kéri a felhasználót a következő paraméter leírása (valamint a paraméter-attribútumok) tábla megjelenik (Get-Help \<cmdletname > – teljes) vagy paramétert (Get-Help \<cmdletname >-paraméter) megtekintése a témakör.

A következő XML formátumú látható két `<dev:defaultValue>` hozzá címkéket a `<command:parameter>` csomópont. Figyelje meg, hogy az alapértelmezett érték a következő záró után azonnal `</command:parameterValue>` tag (Ha a paraméter értéke meg van adva) vagy a záró `</maml:description>` címke, a paraméter leírása. név.

```xml
<command:parameters>
  <command:parameter required="true" globbing="true"
           pipelineInput="false" position="named">
    <maml:name> Parameter name </maml:name>
    <maml:description>
      <maml:para> Parameter Description </maml:para>
    </maml:description>
    <command:parameterValue required="true">
      Value
    </command:parameterValue>
    <dev:defaultValue> Default parameter value </dev:defaultValue>
  </command:parameter>
</command:parameters>
```

Értékek hozzáadásához, felsorolt típusok

Ha a paraméter több értéket vagy értékek sorszámozott típus, egy nem kötelező használható \<dev:possibleValues > csomópont. Ez a csomópont lehetővé teszi, hogy adjon meg egy nevet és leírást a több érték.

Vegye figyelembe, hogy a felsorolt értékek leírását nem jelennek meg az alapértelmezett bármelyikét súgó nézetek által megjelenített a `Get-Help` parancsmag, de más Súgó megtekintők jelenhetnek meg ezt a tartalmat a nézeteket.

A következő XML-mutatja egy `<dev:possibleValues>` két értéket a megadott csomópont.

```xml
<command:parameters>
  <command:parameter required="true" globbing="true"
           pipelineInput="false" position="named">
    <maml:name> Parameter name </maml:name>
    <maml:description>
      <maml:para> Parameter Description </maml:para>
    </maml:description>
    <command:parameterValue required="true">
      Value
    </command:parameterValue>
    <dev:defaultValue> Default parameter value </dev:defaultValue>
    <dev:possibleValues>
      <dev:possibleValue>
        <dev:value> Value 1 </dev:value>
        <maml:description>
          <maml:para> Description 1 </maml:para>
        </maml:description>
      <dev:possibleValue>
      <dev:possibleValue>
        <dev:value> Value 2 </dev:value>
        <maml:description>
          <maml:para> Description 2 </maml:para>
        </maml:description>
      <dev:possibleValue>
    </dev:possibleValues>
  </command:parameter>
</command:parameters>
```