---
title: Hogyan belül egy parancsmag-szkriptek meghívása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cc0bc6ce-48a5-4d9c-927e-636bca743e9f
caps.latest.revision: 9
ms.openlocfilehash: 7dcb8bc20ab56225764854f9dc6fdfd858ed7451
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067875"
---
# <a name="how-to-invoke-scripts-within-a-cmdlet"></a>Parancsmagok és szkriptek meghívása parancsmagokon belül

Ez a példa bemutatja, hogyan meghívni egy parancsmaghoz megadott parancsfájl. A parancsfájl a parancsmag által végrehajtott, és az eredményeket vissza a parancsmag egy gyűjteménye, [System.Management.Automation.PSObject](/dotnet/api/System.Management.Automation.PSObject) objektumokat.

## <a name="to-invoke-a-script-block"></a>Parancsprogram-blokkot meghívásához

1. A parancs ellenőrzi, hogy a parancsprogram-blokkot lett megadva a parancsmaghoz. Ha a parancsprogram-blokkot lett megadva, a parancs a megfelelő paraméterekkel rendelkező parancsfájl-blokkon hív meg.

    ```csharp
    if (script != null)
    {
      WriteDebug("Executing script block.");

      // Invoke the script block with the required arguments.
      Collection<PSObject> PSObjects =
                     script.Invoke(
                                   line,
                                   simpleMatch,
                                   caseSensitive
                                  );
    ```

2. Ezt követően a szkript végighalad a visszaadott gyűjteményét [System.Management.Automation.PSObject](/dotnet/api/System.Management.Automation.PSObject) objektumokat, és végezze el a szükséges műveletek.

    ```c
    foreach (PSObject psObject in psObjects)
    {
      if (LanguagePrimitives.IsTrue(psObject))
      {
        result = new MatchInfo();
        result.Line = line;
        result.IgnoreCase = !caseSensitive;

        break;
      }
    }

    ```

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
