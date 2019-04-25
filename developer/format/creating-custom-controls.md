---
title: Egyéni vezérlők létrehozását |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c3baa406-cd33-4420-be5a-07ef09d93480
caps.latest.revision: 8
ms.openlocfilehash: 3504ab1d974c55e9279172d0e851961474ccb926
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066685"
---
# <a name="creating-custom-controls"></a>Egyéni vezérlők létrehozása

Egyéni vezérlők olyan formázási fájl legrugalmasabb összetevői. Egyéni vezérlők ellentétben a táblázat, lista és széles körű nézeteket, amelyek meghatározzák az adatok, például az adatok táblázatként formális szerkezete lehetővé teszik, hogy meghatározza, hogyan jelenjen meg az egyes adat. Megadhatja, hogy az elérhető formázási fájl összes nézet egyéni vezérlők tulajdonságkészlettel, meghatározhatja egy adott nézet számára elérhető egyéni vezérlők, vagy megadhatja, hogy a vezérlők elérhető objektumok egy csoportjára.

## <a name="custom-control-example"></a>Egyéni vezérlő példa

Az alábbi példa bemutatja a Certificates.Format.ps1xml fájlban meghatározott egyéni vezérlőt. Ezt az egyéni vezérlőt különítjük el a [System.Management.Automation.Signature](/dotnet/api/System.Management.Automation.Signature) táblázat nézetben megjelenített objektumok.

```xml
<Controls>
  <Control>
    <Name>SignatureTypes-GroupingFormat</Name>
    <CustomControl>
      <CustomEntries>
        <CustomEntry>
          <CustomItem>
            <Frame>
              <LeftIndent>4</LeftIndent>
              <CustomItem>
                <Text AssemblyName="System.Management.Automation" BaseName="FileSystemProviderStrings"
                  ResourceId="DirectoryDisplayGrouping"/>
                <ExpressionBinding>
                  <ScriptBlock>split-path $_.Path</ScriptBlock>
                </ExpressionBinding>
                <NewLine/>
              </CustomItem>
            </Frame>
          </CustomItem>
        </CustomEntry>
      </CustomEntries>
    </CustomControl>
  </Control>
</Controls>

```

## <a name="see-also"></a>Lásd még:

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
