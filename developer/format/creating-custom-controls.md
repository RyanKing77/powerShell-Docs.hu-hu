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
# <a name="creating-custom-controls"></a><span data-ttu-id="9c0c4-102">Egyéni vezérlők létrehozása</span><span class="sxs-lookup"><span data-stu-id="9c0c4-102">Creating Custom Controls</span></span>

<span data-ttu-id="9c0c4-103">Egyéni vezérlők olyan formázási fájl legrugalmasabb összetevői.</span><span class="sxs-lookup"><span data-stu-id="9c0c4-103">Custom controls are the most flexible components of a formatting file.</span></span> <span data-ttu-id="9c0c4-104">Egyéni vezérlők ellentétben a táblázat, lista és széles körű nézeteket, amelyek meghatározzák az adatok, például az adatok táblázatként formális szerkezete lehetővé teszik, hogy meghatározza, hogyan jelenjen meg az egyes adat.</span><span class="sxs-lookup"><span data-stu-id="9c0c4-104">Unlike table, list, and wide views that define a formal structure of data, such as a table of data, custom controls allow you to define how an individual piece of data is displayed.</span></span> <span data-ttu-id="9c0c4-105">Megadhatja, hogy az elérhető formázási fájl összes nézet egyéni vezérlők tulajdonságkészlettel, meghatározhatja egy adott nézet számára elérhető egyéni vezérlők, vagy megadhatja, hogy a vezérlők elérhető objektumok egy csoportjára.</span><span class="sxs-lookup"><span data-stu-id="9c0c4-105">You can define a common set of custom controls that are available to all the views of the formatting file, you can define custom controls that are available to a specific view, or you can define a set of controls that are available to a group of objects.</span></span>

## <a name="custom-control-example"></a><span data-ttu-id="9c0c4-106">Egyéni vezérlő példa</span><span class="sxs-lookup"><span data-stu-id="9c0c4-106">Custom Control Example</span></span>

<span data-ttu-id="9c0c4-107">Az alábbi példa bemutatja a Certificates.Format.ps1xml fájlban meghatározott egyéni vezérlőt.</span><span class="sxs-lookup"><span data-stu-id="9c0c4-107">The following example shows a custom control that is defined in the Certificates.Format.ps1xml file.</span></span> <span data-ttu-id="9c0c4-108">Ezt az egyéni vezérlőt különítjük el a [System.Management.Automation.Signature](/dotnet/api/System.Management.Automation.Signature) táblázat nézetben megjelenített objektumok.</span><span class="sxs-lookup"><span data-stu-id="9c0c4-108">This custom control is used to separate the [System.Management.Automation.Signature](/dotnet/api/System.Management.Automation.Signature) objects displayed in a table view.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="9c0c4-109">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9c0c4-109">See Also</span></span>

[<span data-ttu-id="9c0c4-110">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="9c0c4-110">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
