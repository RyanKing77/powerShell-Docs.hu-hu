---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A parancsfájl és a konzol ablaktáblában kiegészítést használata"
ms.assetid: 3b752c3c-0bd0-4eca-a2d3-2d5a37fd9d84
ms.openlocfilehash: ba8d0af7e7fc0f1df9f65116be899097b0a97a3c
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a><span data-ttu-id="2820c-103">A parancsfájl és a konzol ablaktáblában kiegészítést használata</span><span class="sxs-lookup"><span data-stu-id="2820c-103">How to Use Tab Completion in the Script Pane and Console Pane</span></span>
<span data-ttu-id="2820c-104">Kiegészítést automatikus segítséget nyújt, ha a parancsfájl ablaktáblán vagy a parancssori ablaktáblában írja be.</span><span class="sxs-lookup"><span data-stu-id="2820c-104">Tab completion provides automatic help when you are typing in the Script Pane or in the Command Pane.</span></span> <span data-ttu-id="2820c-105">Ez a funkció előnyeit tegye a következőket:</span><span class="sxs-lookup"><span data-stu-id="2820c-105">Use the following steps to take advantage of this feature:</span></span>

## <a name="to-automatically-complete-a-command-entry"></a><span data-ttu-id="2820c-106">A parancs bejegyzés automatikusan befejezéséhez</span><span class="sxs-lookup"><span data-stu-id="2820c-106">To automatically complete a command entry</span></span>
<span data-ttu-id="2820c-107">A parancs vagy parancsfájl ablaktáblán írja be a parancsot néhány karakterét, és nyomja le az FÜLRE kattintva válassza ki a kívánt befejezési szöveget.</span><span class="sxs-lookup"><span data-stu-id="2820c-107">In the Command Pane or Script Pane, type a few characters of a command and then press TAB to select the desired completion text.</span></span> <span data-ttu-id="2820c-108">Ha több elemet a szöveg, amelyet eredetileg megadott kezdődik, akkor olvassa tovább Tab billentyűkombinációval, amíg meg nem jelenik meg a kívánt elemet.</span><span class="sxs-lookup"><span data-stu-id="2820c-108">If multiple items begin with the text that you initially typed, then continue pressing Tab until the item you want appears.</span></span> <span data-ttu-id="2820c-109">Kiegészítést is segítséget nyújt egy parancsmag neve, a paraméter neve, a változó neve, a objektum tulajdonság neve vagy a egy fájl elérési útját írja be.</span><span class="sxs-lookup"><span data-stu-id="2820c-109">Tab completion can help with typing a cmdlet name, parameter name, variable name, object property name, or a file path.</span></span>

> [!NOTE]
> <span data-ttu-id="2820c-110">A parancsfájl ablaktáblán TAB billentyűkombinációval automatikusan befejezi a parancs csak akkor, ha szerkeszti, .ps1, .psd1 vagy .psm1 fájlok.</span><span class="sxs-lookup"><span data-stu-id="2820c-110">In the Script Pane, pressing TAB will automatically complete a command only when you are editing .ps1, .psd1, or .psm1 files.</span></span> <span data-ttu-id="2820c-111">Kiegészítést bármikor, ha a parancs ablaktábla ír működik.</span><span class="sxs-lookup"><span data-stu-id="2820c-111">Tab completion works any time when you are typing in the Command Pane.</span></span>

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a><span data-ttu-id="2820c-112">A parancsmag paraméter bejegyzés automatikusan befejezéséhez</span><span class="sxs-lookup"><span data-stu-id="2820c-112">To automatically complete a cmdlet parameter entry</span></span>
<span data-ttu-id="2820c-113">A parancs vagy a parancsfájl ablaktáblán írja be a parancsmag kötőjellel, és nyomja le az lapon.</span><span class="sxs-lookup"><span data-stu-id="2820c-113">In the Command Pane or Script pane, type a cmdlet followed by a dash, and then press TAB.</span></span>

<span data-ttu-id="2820c-114">Írja be például `Get-Process -` majd nyomja le az lapon többször a paraméterek, a parancsmag pedig megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="2820c-114">For example, type `Get-Process -` and then press TAB multiple times to display each of the parameters for the cmdlet in turn.</span></span>

## <a name="see-also"></a><span data-ttu-id="2820c-115">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2820c-115">See Also</span></span>
- [<span data-ttu-id="2820c-116">A Windows PowerShell ISE használatával</span><span class="sxs-lookup"><span data-stu-id="2820c-116">Using Windows PowerShell ISE</span></span>](using-the-windows-powershell-ise.md)
- [<span data-ttu-id="2820c-117">A PowerShell lap létrehozása</span><span class="sxs-lookup"><span data-stu-id="2820c-117">How to Create a PowerShell Tab</span></span>](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)

