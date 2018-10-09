---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Parancssori kiegészítés használata a Parancsfájl panelen és a Konzol panelen
ms.assetid: 3b752c3c-0bd0-4eca-a2d3-2d5a37fd9d84
ms.openlocfilehash: 24a3f00987ff5ca4bf82d1a3206857ec3c4b3f09
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851135"
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a><span data-ttu-id="9f3a2-103">Parancssori kiegészítés használata a Parancsfájl panelen és a Konzol panelen</span><span class="sxs-lookup"><span data-stu-id="9f3a2-103">How to Use Tab Completion in the Script Pane and Console Pane</span></span>

<span data-ttu-id="9f3a2-104">Kiegészítés automatikus segítséget nyújt, ha elkezdi beírni a parancsfájl ablaktáblán vagy a parancssori ablak.</span><span class="sxs-lookup"><span data-stu-id="9f3a2-104">Tab completion provides automatic help when you are typing in the Script Pane or in the Command Pane.</span></span> <span data-ttu-id="9f3a2-105">A következő lépések használatával Ez a funkció előnyeit:</span><span class="sxs-lookup"><span data-stu-id="9f3a2-105">Use the following steps to take advantage of this feature:</span></span>

## <a name="to-automatically-complete-a-command-entry"></a><span data-ttu-id="9f3a2-106">A parancs bejegyzés automatikus elvégzéséhez</span><span class="sxs-lookup"><span data-stu-id="9f3a2-106">To automatically complete a command entry</span></span>

<span data-ttu-id="9f3a2-107">A parancs vagy parancsfájl ablaktáblán írja be egy parancsot néhány karakterét, és nyomja le az FÜLRE kattintva válassza ki a kívánt befejezési szöveget.</span><span class="sxs-lookup"><span data-stu-id="9f3a2-107">In the Command Pane or Script Pane, type a few characters of a command and then press TAB to select the desired completion text.</span></span> <span data-ttu-id="9f3a2-108">Ha több elem kezdetben beírt szöveggel kezdődik, majd folytassa a Tab billentyűkombinációval, amíg meg nem jelenik meg a kívánt elemet.</span><span class="sxs-lookup"><span data-stu-id="9f3a2-108">If multiple items begin with the text that you initially typed, then continue pressing Tab until the item you want appears.</span></span> <span data-ttu-id="9f3a2-109">Kiegészítés segíthet írja be a parancsmag neve, a paraméter neve, változó neve, objektum tulajdonság neve vagy egy fájl elérési útját.</span><span class="sxs-lookup"><span data-stu-id="9f3a2-109">Tab completion can help with typing a cmdlet name, parameter name, variable name, object property name, or a file path.</span></span>

> [!NOTE]
> <span data-ttu-id="9f3a2-110">A parancsfájl panelen TAB billentyűkombinációval automatikusan befejezi a parancs csak akkor, ha szerkeszti, .ps1, .psd1 vagy .psm1 fájlok.</span><span class="sxs-lookup"><span data-stu-id="9f3a2-110">In the Script Pane, pressing TAB will automatically complete a command only when you are editing .ps1, .psd1, or .psm1 files.</span></span> <span data-ttu-id="9f3a2-111">Kiegészítés működik, bármikor, amikor elkezdi beírni a parancs ablaktáblán.</span><span class="sxs-lookup"><span data-stu-id="9f3a2-111">Tab completion works any time when you are typing in the Command Pane.</span></span>

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a><span data-ttu-id="9f3a2-112">Egy parancsmag-paraméterrel bejegyzést automatikus elvégzéséhez</span><span class="sxs-lookup"><span data-stu-id="9f3a2-112">To automatically complete a cmdlet parameter entry</span></span>

<span data-ttu-id="9f3a2-113">A parancs ablaktáblán vagy a parancsfájl panelen írja be a parancsmag kötőjellel, és nyomja le az lapon.</span><span class="sxs-lookup"><span data-stu-id="9f3a2-113">In the Command Pane or Script pane, type a cmdlet followed by a dash and then press TAB.</span></span>

<span data-ttu-id="9f3a2-114">Írja be például `Get-Process -` és nyomja le lapon többször viszont megjelenítéséhez a paraméterek a parancsmaghoz.</span><span class="sxs-lookup"><span data-stu-id="9f3a2-114">For example, type `Get-Process -` and then press TAB multiple times to display each of the parameters for the cmdlet in turn.</span></span>

## <a name="see-also"></a><span data-ttu-id="9f3a2-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9f3a2-115">See Also</span></span>

- [<span data-ttu-id="9f3a2-116">A Windows PowerShell ISE bemutatása</span><span class="sxs-lookup"><span data-stu-id="9f3a2-116">Introducing the Windows PowerShell ISE</span></span>](Introducing-the-Windows-PowerShell-ISE.md)
- [<span data-ttu-id="9f3a2-117">PowerShell-lap létrehozása</span><span class="sxs-lookup"><span data-stu-id="9f3a2-117">How to Create a PowerShell Tab</span></span>](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)
