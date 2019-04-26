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
# <a name="how-to-invoke-scripts-within-a-cmdlet"></a><span data-ttu-id="d282a-102">Parancsmagok és szkriptek meghívása parancsmagokon belül</span><span class="sxs-lookup"><span data-stu-id="d282a-102">How to Invoke Scripts Within a Cmdlet</span></span>

<span data-ttu-id="d282a-103">Ez a példa bemutatja, hogyan meghívni egy parancsmaghoz megadott parancsfájl.</span><span class="sxs-lookup"><span data-stu-id="d282a-103">This example shows how to invoke a script that is supplied to a cmdlet.</span></span> <span data-ttu-id="d282a-104">A parancsfájl a parancsmag által végrehajtott, és az eredményeket vissza a parancsmag egy gyűjteménye, [System.Management.Automation.PSObject](/dotnet/api/System.Management.Automation.PSObject) objektumokat.</span><span class="sxs-lookup"><span data-stu-id="d282a-104">The script is executed by the cmdlet, and its results are returned to the cmdlet as a collection of [System.Management.Automation.PSObject](/dotnet/api/System.Management.Automation.PSObject) objects.</span></span>

## <a name="to-invoke-a-script-block"></a><span data-ttu-id="d282a-105">Parancsprogram-blokkot meghívásához</span><span class="sxs-lookup"><span data-stu-id="d282a-105">To invoke a script block</span></span>

1. <span data-ttu-id="d282a-106">A parancs ellenőrzi, hogy a parancsprogram-blokkot lett megadva a parancsmaghoz.</span><span class="sxs-lookup"><span data-stu-id="d282a-106">The command verifies that a script block was supplied to the cmdlet.</span></span> <span data-ttu-id="d282a-107">Ha a parancsprogram-blokkot lett megadva, a parancs a megfelelő paraméterekkel rendelkező parancsfájl-blokkon hív meg.</span><span class="sxs-lookup"><span data-stu-id="d282a-107">If a script block was supplied, the command invokes the script block with its required parameters.</span></span>

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

2. <span data-ttu-id="d282a-108">Ezt követően a szkript végighalad a visszaadott gyűjteményét [System.Management.Automation.PSObject](/dotnet/api/System.Management.Automation.PSObject) objektumokat, és végezze el a szükséges műveletek.</span><span class="sxs-lookup"><span data-stu-id="d282a-108">Then, the script iterates through the returned collection of [System.Management.Automation.PSObject](/dotnet/api/System.Management.Automation.PSObject) objects and perform the necessary operations.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="d282a-109">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d282a-109">See Also</span></span>

[<span data-ttu-id="d282a-110">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="d282a-110">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
