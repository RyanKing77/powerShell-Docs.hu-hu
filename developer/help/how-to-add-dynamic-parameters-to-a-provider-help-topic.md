---
title: Dinamikus paraméterek hozzáadása szolgáltatói súgótémakörre | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e20e5ad6-a6e6-4a63-9d42-1ac54214f748
caps.latest.revision: 5
ms.openlocfilehash: 59839e9b8b6f2a56f2f1a9c755f2f1a85deb34aa
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848113"
---
# <a name="how-to-add-dynamic-parameters-to-a-provider-help-topic"></a>Dinamikus paraméterek hozzáadása egy szolgáltatói súgótémakörhöz

Ez a szakasz azt ismerteti, hogyan tölthetők fel a szolgáltatói súgótémakör **dinamikus paraméterek** szakasza.

A *dinamikus paraméterek* olyan parancsmagok vagy függvények paramétereinek, amelyek csak meghatározott feltételek esetén érhetők el.

A szolgáltatói súgótémakör által dokumentált dinamikus paraméterek a szolgáltató által a parancsmaghoz vagy függvényhez hozzáadott dinamikus paraméterek, ha a szolgáltató meghajtóján a parancsmagot vagy a függvényt használja a rendszer.

A dinamikus paraméterek a szolgáltatók egyéni parancsmag súgójában is dokumentálva lehetnek. Ha a szolgáltató súgóját és az egyéni parancsmag súgóját is megírta a szolgáltatók számára, a dinamikus paraméterek dokumentációját is adja meg mindkét dokumentumban.

Ha a szolgáltató nem valósít meg dinamikus paramétereket, a szolgáltatói súgótémakör üres `DynamicParameters` elemet tartalmaz.

### <a name="to-add-dynamic-parameters"></a>Dinamikus paraméterek hozzáadása

1. A *AssemblyName*. dll-help. xml fájlban a `providerHelp` elemen belül adjon hozzá egy `DynamicParameters` elemet. Az `DynamicParameters` elemnek az `Tasks` elem után és az `RelatedLinks` elem előtt kell megjelennie.

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

   Ha a szolgáltató nem valósít meg dinamikus paramétereket, az `DynamicParameters` elem üres is lehet.

2. A `DynamicParameters` elemen belül minden dinamikus paraméterhez adjon hozzá egy `DynamicParameter` elemet.

   Például:

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
        </DynamicParameter>
    </DynamicParameters>
    ```

3. Minden `DynamicParameter` elemnél adjon hozzá egy `Name` és `CmdletSupported` egy elemet.

   |Elem neve|Leírás|
   |------------------|-----------------|
   |Név|Megadja a paraméter nevét.|
   |CmdletSupported|Meghatározza azokat a parancsmagokat, amelyekben a paraméter érvényes. Adja meg a parancsmagok neveinek vesszővel tagolt listáját.|

   A következő XML- `Encoding` dokumentumok például a Windows PowerShell fájlrendszer-szolgáltató által a, `Add-Content` `Get-Content` `Set-Content` a parancsmagokhoz hozzáadott dinamikus paraméter.

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
            <Name> Encoding </Name>
            <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
    </DynamicParameters>

    ```

4. Minden `DynamicParameter` elemnél adjon hozzá egy `Type` elemet. Az `Type` elem a dinamikus paraméter értékének `Name` .net-típusát tartalmazó elem tárolója.

   Például a következő XML azt mutatja, hogy a `Encoding` dinamikus paraméter .net-típusa a [Microsoft. PowerShell. commands. FileSystemCmdletProviderEncoding](/dotnet/api/microsoft.powershell.commands.filesystemcmdletproviderencoding) enumerálása.

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

5. Adja hozzá `Description` a (z) elemet, amely a dinamikus paraméter rövid leírását tartalmazza. A Leírás összeállítása során az összes parancsmag-paraméterhez megadott irányelvek [alapján adja](./how-to-add-parameter-information.md)meg a paraméter-információkat.

   A következő XML például tartalmazza a `Encoding` dinamikus paraméter leírását.

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

6. Adja hozzá `PossibleValues` az elemet és annak alárendelt elemeit. Ezek az elemek együttesen írják le a dinamikus paraméter értékeit. Ez az elem enumerált értékekhez lett tervezve. Ha a dinamikus paraméter nem vesz fel értéket, például egy kapcsoló paraméterrel, vagy az értékek nem sorolhatók fel, adjon hozzá egy üres `PossibleValues` elemet.

   Az alábbi táblázat felsorolja és leírja az `PossibleValues` elemet és annak alárendelt elemeit.

   |Elem neve|Leírás|
   |------------------|-----------------|
   |PossibleValues|Ez az elem egy tároló. Az alárendelt elemek az alábbiakban olvashatók. Adjon hozzá `PossibleValues` egy elemet az egyes szolgáltatói témakörökhöz. Az elem üres is lehet.|
   |PossibleValue|Ez az elem egy tároló. Az alárendelt elemek az alábbiakban olvashatók. Adjon hozzá `PossibleValue` egy elemet a dinamikus paraméter minden értékéhez.|
   |Érték|Megadja az érték nevét.|
   |Leírás|Ez az elem egy `Para` elemet tartalmaz. Az `Para` elem szövege a `Value` elemben szereplő értéket írja le.|

   A következő XML például a `PossibleValue` `Encoding` dinamikus paraméter egy elemét jeleníti meg.

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

A következő példában a `DynamicParameters` `Encoding` dinamikus paraméter elemét láthatja.

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