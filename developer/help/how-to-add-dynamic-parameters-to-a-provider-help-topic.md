---
title: Dinamikus paraméterek hozzáadása a szolgáltató súgótémakör |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e20e5ad6-a6e6-4a63-9d42-1ac54214f748
caps.latest.revision: 5
ms.openlocfilehash: cc4877242a16a9caa99564aeaae985f85e38791e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849524"
---
# <a name="how-to-add-dynamic-parameters-to-a-provider-help-topic"></a>Dinamikus paraméterek hozzáadása egy szolgáltatói súgótémakörhöz

Ez a szakasz azt ismerteti, hogyan töltse fel a **dinamikus paraméterek** szolgáltató súgótémakör szakaszában.

*Dinamikus paraméterek* egy parancsmag-paraméterek vagy a megadott feltétel-függvény, amely csak az érhető el.

A szolgáltató súgótémakör ismertetett dinamikus paraméterek a dinamikus paraméterek, amelyek a szolgáltató ad hozzá a parancsmag vagy a funkció használatakor a parancsmagot vagy a funkció a szolgáltató meghajtón.

Dinamikus paraméterek egyéni parancsmag súgójában talál egy szolgáltatót kell dokumentálni. Szolgáltató Súgó és az egyéni parancsmag súgóját írásakor szolgáltató, vegye fel a dinamikus paraméterek dokumentáció mindkét dokumentum. Egyéni parancsmag súgóját kapcsolatos további információkért lásd: [írása Windows PowerShell egyéni parancsmag segítségével a szolgáltatók](./writing-custom-cmdlet-help-for-windows-powershell-providers.md).

Ha a szolgáltató nem valósítja meg a dinamikus paraméterek, a szolgáltató Súgó-témakör tartalmaz egy üres `DynamicParameters` elemet.

### <a name="to-add-dynamic-parameters"></a>Dinamikus paraméterek hozzáadása

1. Az a *AssemblyName*belül a .dll-help.xml fájlt a `providerHelp` elem, adjon hozzá egy `DynamicParameters` elem. A `DynamicParameters` elem után meg kell jelennie a `Tasks` elem előtt a `RelatedLinks` elemet.

   Például:

    ```xml
    <providerHelp>
        <Tasks>
        </Tasks>
        <DynamicParameters>
        </DynamicParameters>
        <RelatedLinks>
        </RelatedLinks>
    </providerHelp>
    ```

   Ha a szolgáltató nem valósítja meg a dinamikus paraméterek a `DynamicParameters` elem lehet üres.

2. Belül a `DynamicParameters` elem, minden egyes dinamikus paraméterre, adjon hozzá egy `DynamicParameter` elemet.

   Például:

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
        </DynamicParameter>
    </DynamicParameters>
    ```

3. Az egyes `DynamicParameter` elem, adjon hozzá egy `Name` és `CmdletSupported` elemet.

   |Elem neve|Leírás|
   |------------------|-----------------|
   |Név|A paraméter neve.|
   |CmdletSupported|Adja meg a parancsmagok, amelyben a paraméter nem érvényes. Írja be a parancsmag nevek vesszővel tagolt listája.|

   Ha például a következő XML-dokumentumok a `Encoding` dinamikus paraméter, amely hozzáadja a Windows PowerShell fájlrendszer-szolgáltatót a `Add-Content`, `Get-Content`, `Set-Content` parancsmagok.

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
            <Name> Encoding </Name>
            <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
    </DynamicParameters>

    ```

4. Az egyes `DynamicParameter` elemben adjon hozzá egy `Type` elemet. A `Type` elem tárolója a `Name` elem, amely tartalmazza a dinamikus paraméter értéke a .NET-típus.

   Ha például a következő XML formátumú típusát jeleníti meg, amely .NET a `Encoding` dinamikus paraméter a [Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding](/dotnet/api/microsoft.powershell.commands.filesystemcmdletproviderencoding) enumerálása.

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
            <Name> Encoding </Name>
            <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
            <Type>
                <Name> Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding </Name>
            <Type>
    ...
    </DynamicParameters>
    ```

5. Adja hozzá a `Description` elem, amely a dinamikus paraméterek rövid leírását tartalmazza. A leírás szerkesztésekor kövesse az alábbi útmutatást az összes parancsmag-paraméterek a előírt [paraméter-adatok hozzáadása](./how-to-add-parameter-information.md).

   Például a következő XML-kódot tartalmaz a leírása a `Encoding` dinamikus paraméterét.

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
            <Name> Encoding </Name>
            <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
            <Type>
                <Name> Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding </Name>
            <Type>
            <Description> Specifies the encoding of the output file that contains the content. </Description>
    ...
    </DynamicParameters>
    ```

6. Adja hozzá a `PossibleValues` elem és az alárendelt elemei. Ezek az elemek együtt, a dinamikus paraméterek értékeit mutatják. Ez az elem a felsorolt értékek lett tervezve. A dinamikus paraméterek nem vesz egy értéket, ha például egy kapcsoló paraméter esetében, vagy az értékek számbavétele nem lehetséges, vagy adjon hozzá egy üres `PossibleValues` elemet.

   A következő táblázat felsorolja és ismerteti a `PossibleValues` elem és az alárendelt elemei.

   |Elem neve|Leírás|
   |------------------|-----------------|
   |PossibleValues|Az elem a tárolóban. Az alárendelt elemei az alábbiakban tekintheti át. Vegyen fel egy `PossibleValues` elem minden szolgáltató Súgó-témakör. Lehet, hogy az elem üres.|
   |PossibleValue|Az elem a tárolóban. Az alárendelt elemei az alábbiakban tekintheti át. Vegyen fel egy `PossibleValue` elem minden egyes érték a-dynamic paraméter.|
   |Érték|Az érték nevét adja meg.|
   |Leírás|Tento element obsahuje egy `Para` elemet. A szöveget a `Para` elem a nevű értékét mutatja be a `Value` elemet.|

   Például a következő XML formátumú látható egy `PossibleValue` eleme a `Encoding` dinamikus paraméterét.

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
    ...
            <Description> Specifies the encoding of the output file that contains the content. </Description>
            <PossibleValues>
                <PossibleValue>
                    <Value> ASCII </Value>
                    <Description>
                        <para> Uses the encoding for the ASCII (7-bit) character set. </para>
                    </Description>
                </PossibleValue>
    ...
            </PossibleValues>
    </DynamicParameters>
    ```

## <a name="example"></a>Példa

A következő példa bemutatja a `DynamicParameters` eleme a `Encoding` dinamikus paraméterét.

```xml
<DynamicParameters/>
    <DynamicParameter>
        <Name> Encoding </Name>
        <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
        <Type>
            <Name> Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding </Name>
        <Type>
        <Description> Specifies the encoding of the output file that contains the content. </Description>
        <PossibleValues>
            <PossibleValue>
                <Value> ASCII </Value>
                <Description>
                    <para> Uses the encoding for the ASCII (7-bit) character set. </para>
                </Description>
            </PossibleValue>
            <PossibleValue>
                <Value> Unicode </Value>
                <Description>
                    <para> Encodes in UTF-16 format using the little-endian byte order. </para>
                </Description>
            </PossibleValue>
        </PossibleValues>
</DynamicParameters>
```