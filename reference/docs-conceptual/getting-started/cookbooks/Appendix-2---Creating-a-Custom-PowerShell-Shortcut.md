---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: '2. függelék: Egyéni PowerShell-parancsikon létrehozása'
ms.assetid: 5d4fd421-5d43-4ec7-86fd-acfe887b066e
ms.openlocfilehash: e8081b7a64d313c8ef4bbccf95f250445dd68ad9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30949264"
---
# <a name="appendix-2---creating-a-custom-powershell-shortcut"></a><span data-ttu-id="4e4a3-103">Függelék: 2 - egyéni PowerShell parancsikon létrehozása</span><span class="sxs-lookup"><span data-stu-id="4e4a3-103">Appendix 2 - Creating a Custom PowerShell Shortcut</span></span>

<span data-ttu-id="4e4a3-104">Az alábbi eljárás ismerteti, hogy a program számos kényelmes testre szabott Windows PowerShell parancsikon létrehozása.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-104">The following procedure describes how to create a shortcut to Windows PowerShell that has several convenient options customized.</span></span>

1. <span data-ttu-id="4e4a3-105">Hozzon létre egy parancsikont, amely a PowerShell.exe.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-105">Create a shortcut that points to Powershell.exe.</span></span>

2. <span data-ttu-id="4e4a3-106">Kattintson a jobb gombbal a parancsikonra, és kattintson **tulajdonságok**.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-106">Right-click the shortcut, and then click **Properties**.</span></span>

3. <span data-ttu-id="4e4a3-107">Kattintson a **beállítások** fülre.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-107">Click the **Options** tab.</span></span>

4. <span data-ttu-id="4e4a3-108">Az a **beállítások szerkesztése** szakaszban jelölje be a **gyorsszerkesztési** jelölőnégyzetet.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-108">In the **Edit Options** section, select the **QuickEdit** check box.</span></span>

    <span data-ttu-id="4e4a3-109">Ez a beállítás lehetővé teszi a szöveget a Windows PowerShell konzol ablakban a bal oldali egérgombbal húzással ki, és lehetővé teszi, hogy a szöveg másolása a vágólapra ENTER billentyű megnyomásával, vagy kattintson a jobb gombbal az egérrel.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-109">This setting lets you select text in the Windows PowerShell console window by dragging the left mouse button, and it lets you copy text to the clipboard by pressing ENTER or by right-clicking the mouse.</span></span>

5. <span data-ttu-id="4e4a3-110">Az a **beállítások szerkesztése** szakaszban jelölje be a **beszúrási módban** jelölőnégyzetet.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-110">In the **Edit Options** section, select the **Insert Mode** check box.</span></span> <span data-ttu-id="4e4a3-111">Ez a beállítás lehetővé teszi a kattintson a jobb gombbal a konzolablakban automatikusan illessze be a vágólapra másolt szöveget.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-111">This setting lets you right-click in the console window to automatically paste text from the clipboard.</span></span>

6. <span data-ttu-id="4e4a3-112">Az a **parancselőzmények** szakaszban adja meg vagy válasszon egy 1 és 999 a közötti számot a **pufferméret** mezőbe.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-112">In the **Command History** section, type or select a number between 1 and 999 in the **Buffer Size** box.</span></span> <span data-ttu-id="4e4a3-113">Ez beállítja a konzol pufferben megtartott parancsok száma.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-113">This sets the number of typed commands that will be kept in the console buffer.</span></span>

7. <span data-ttu-id="4e4a3-114">Az a **parancselőzmények** szakaszban jelölje be a **régi ismétlődések vetni** elkerülése érdekében a konzol pufferből ismételt parancsok jelölőnégyzetet.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-114">In the **Command History** section, select the **Discard Old Duplicates** check box to eliminate repeated commands from the console buffer.</span></span>

8. <span data-ttu-id="4e4a3-115">Kattintson a **elrendezés** fülre.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-115">Click the **Layout** tab.</span></span>

9. <span data-ttu-id="4e4a3-116">Az a **képernyőpuffer** területen írja be egy 1 és 9999 közötti számot a **magasság** mezőbe.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-116">In the **Screen Buffer** section, type a number between 1 and 9999 in the **Height** box.</span></span> <span data-ttu-id="4e4a3-117">A magasság kimenete pufferelve van-e vonalak számát jelöli.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-117">The height represents the number of lines of output that are buffered.</span></span> <span data-ttu-id="4e4a3-118">Ez az maradnak meg, ha a konzolablakban görgetése sorok maximális számát.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-118">This is the maximum number of lines retained for viewing when you scroll through the console window.</span></span> <span data-ttu-id="4e4a3-119">Ha ez a szám nem éri el a magasság látható a **ablakméret** szakaszában, az ablak mérete magassága automatikusan csökken ugyanarra az értékre.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-119">If this number is lower than the height shown in the **Window size** section, the window size height will automatically be reduced to the same value.</span></span>

10. <span data-ttu-id="4e4a3-120">Az a **ablakméret** területen írja be egy 1 és 9999 a szélesség közötti számot.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-120">In the **Window Size** section, type a number between 1 and 9999 for the width.</span></span> <span data-ttu-id="4e4a3-121">Ez jelenti, hogy a karakterek, amelyek között a konzolablakban jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-121">This represents the number of characters that are displayed across the console window.</span></span> <span data-ttu-id="4e4a3-122">Az alapértelmezett vonalvastagságot 80-as, és a szélesség készült Windows PowerShell kimeneti formázás.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-122">The default width is 80, and Windows PowerShell's output formatting is designed for this width.</span></span>

11. <span data-ttu-id="4e4a3-123">Ha el szeretné helyezni a konzol adott helyen az asztalon, ha meg van nyitva, törölje a **a rendszer helyezi** jelölőnégyzetet a **ablak pozícióját** szakaszt, és módosítsa az értékeket a a **Balra** és **felső** mezőkben az a **ablak pozícióját** szakasz.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-123">If you want to place the console at a particular point on the desktop when it is opened, clear the **Let system position window** check box in the **Window position** section, and then change the values in the **Left** and **Top** boxes in the **Window position** section.</span></span>

12. <span data-ttu-id="4e4a3-124">Kattintson az **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="4e4a3-124">Click **OK**.</span></span>