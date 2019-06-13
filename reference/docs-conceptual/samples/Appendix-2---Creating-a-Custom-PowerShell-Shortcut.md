---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: '2\. függelék: Egyéni PowerShell-parancsikon létrehozása'
ms.openlocfilehash: 6f1a6a8187b1797103e3620b2cf9155978807ea5
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030305"
---
# <a name="appendix-2---creating-a-custom-powershell-shortcut"></a><span data-ttu-id="6dabc-103">2 – egyéni PowerShell-parancsikon létrehozása. függelék:</span><span class="sxs-lookup"><span data-stu-id="6dabc-103">Appendix 2 - Creating a Custom PowerShell Shortcut</span></span>

<span data-ttu-id="6dabc-104">Az alábbi eljárás ismerteti, hogyan lehet parancsikon létrehozása a Windows PowerShell parancsmag, amely a testre szabott beállítások több kényelmes érhetők el.</span><span class="sxs-lookup"><span data-stu-id="6dabc-104">The following procedure describes how to create a shortcut to Windows PowerShell that has several convenient options customized.</span></span>

1. <span data-ttu-id="6dabc-105">Hozzon létre egy hivatkozást, amely a Powershell.exe mutat.</span><span class="sxs-lookup"><span data-stu-id="6dabc-105">Create a shortcut that points to Powershell.exe.</span></span>

2. <span data-ttu-id="6dabc-106">Kattintson a jobb gombbal a parancsikonra, majd kattintson **tulajdonságok**.</span><span class="sxs-lookup"><span data-stu-id="6dabc-106">Right-click the shortcut, and then click **Properties**.</span></span>

3. <span data-ttu-id="6dabc-107">Kattintson a **beállítások** fülre.</span><span class="sxs-lookup"><span data-stu-id="6dabc-107">Click the **Options** tab.</span></span>

4. <span data-ttu-id="6dabc-108">Az a **beállítások szerkesztése** szakaszban jelölje be a **Gyorsszerkesztés** jelölőnégyzetet.</span><span class="sxs-lookup"><span data-stu-id="6dabc-108">In the **Edit Options** section, select the **QuickEdit** check box.</span></span>

    <span data-ttu-id="6dabc-109">Ez a beállítás lehetővé teszi a Windows PowerShell-konzolablakot lévő szöveg kijelölése a bal oldali gombbal húzásával, és lehetővé teszi, hogy a szöveg másolása a vágólapra ENTER billentyű lenyomásával, vagy kattintson a jobb gombbal az egérrel.</span><span class="sxs-lookup"><span data-stu-id="6dabc-109">This setting lets you select text in the Windows PowerShell console window by dragging the left mouse button, and it lets you copy text to the clipboard by pressing ENTER or by right-clicking the mouse.</span></span>

5. <span data-ttu-id="6dabc-110">Az a **beállítások szerkesztése** szakaszban jelölje be a **mód Insert** jelölőnégyzetet.</span><span class="sxs-lookup"><span data-stu-id="6dabc-110">In the **Edit Options** section, select the **Insert Mode** check box.</span></span> <span data-ttu-id="6dabc-111">Ez a beállítás lehetővé teszi, hogy, kattintson a jobb gombbal a konzolablakban automatikusan beilleszteni a vágólapra másolt szöveget.</span><span class="sxs-lookup"><span data-stu-id="6dabc-111">This setting lets you right-click in the console window to automatically paste text from the clipboard.</span></span>

6. <span data-ttu-id="6dabc-112">Az a **eszközparancs-előzmények** szakaszban adja meg egy 1 és 999 közötti a számot a **puffer mérete** mezőbe.</span><span class="sxs-lookup"><span data-stu-id="6dabc-112">In the **Command History** section, type or select a number between 1 and 999 in the **Buffer Size** box.</span></span> <span data-ttu-id="6dabc-113">Ez beállítja a konzol pufferben megtartott parancsok beírásával számát.</span><span class="sxs-lookup"><span data-stu-id="6dabc-113">This sets the number of typed commands that will be kept in the console buffer.</span></span>

7. <span data-ttu-id="6dabc-114">Az a **eszközparancs-előzmények** szakaszban jelölje be a **Régi előfordulások törlése** melletti jelölőnégyzetet, hogy a konzol puffer ismétlődő parancsokat kiküszöbölése.</span><span class="sxs-lookup"><span data-stu-id="6dabc-114">In the **Command History** section, select the **Discard Old Duplicates** check box to eliminate repeated commands from the console buffer.</span></span>

8. <span data-ttu-id="6dabc-115">Kattintson a **elrendezés** fülre.</span><span class="sxs-lookup"><span data-stu-id="6dabc-115">Click the **Layout** tab.</span></span>

9. <span data-ttu-id="6dabc-116">Az a **Képernyőpufferen** területén adjon meg egy 1 és 9999 közötti számot a **magasság** mezőbe.</span><span class="sxs-lookup"><span data-stu-id="6dabc-116">In the **Screen Buffer** section, type a number between 1 and 9999 in the **Height** box.</span></span> <span data-ttu-id="6dabc-117">A magasságot kimenete pufferelve van sornyi számát jelöli.</span><span class="sxs-lookup"><span data-stu-id="6dabc-117">The height represents the number of lines of output that are buffered.</span></span> <span data-ttu-id="6dabc-118">Ez a megőrzött meg, ha a konzolablakban görgetve sorok maximális számát.</span><span class="sxs-lookup"><span data-stu-id="6dabc-118">This is the maximum number of lines retained for viewing when you scroll through the console window.</span></span> <span data-ttu-id="6dabc-119">Ez a szám kisebb-e a magasságát, ahogyan a **ablakméret** szakaszban az ablak mérete magassága automatikusan csökken az ugyanarra az értékre.</span><span class="sxs-lookup"><span data-stu-id="6dabc-119">If this number is lower than the height shown in the **Window size** section, the window size height will automatically be reduced to the same value.</span></span>

10. <span data-ttu-id="6dabc-120">Az a **ablakméret** területén adjon meg egy számot 1 és 9999 a szélesség között.</span><span class="sxs-lookup"><span data-stu-id="6dabc-120">In the **Window Size** section, type a number between 1 and 9999 for the width.</span></span> <span data-ttu-id="6dabc-121">Ez jelöli, amelyek között a konzolablakban jelennek karakterek száma.</span><span class="sxs-lookup"><span data-stu-id="6dabc-121">This represents the number of characters that are displayed across the console window.</span></span> <span data-ttu-id="6dabc-122">Az alapértelmezett szélesség értéke 80, és a Windows PowerShell-kimeneti formázás a szélesség lett tervezve.</span><span class="sxs-lookup"><span data-stu-id="6dabc-122">The default width is 80, and Windows PowerShell's output formatting is designed for this width.</span></span>

11. <span data-ttu-id="6dabc-123">Ha el szeretné helyezni az asztalon, egy adott időpontban a konzolon, ha meg van nyitva, törölje a **a rendszer helyezi** jelölőnégyzetet a **ablak helyének** szakaszt, és módosítsa az értékeket a a **Balra** és **felső** lévő a **ablak helyének** szakaszban.</span><span class="sxs-lookup"><span data-stu-id="6dabc-123">If you want to place the console at a particular point on the desktop when it is opened, clear the **Let system position window** check box in the **Window position** section, and then change the values in the **Left** and **Top** boxes in the **Window position** section.</span></span>

12. <span data-ttu-id="6dabc-124">Kattintson az **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="6dabc-124">Click **OK**.</span></span>
