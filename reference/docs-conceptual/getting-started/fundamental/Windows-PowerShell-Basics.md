---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A Windows PowerShell alapjai
ms.assetid: 6b3cbbc8-060c-4877-b00b-7300dbbe4e28
ms.openlocfilehash: 7b5cdfce876aa7d5559fe772379829011b275a02
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="windows-powershell-basics"></a><span data-ttu-id="77299-103">A Windows PowerShell alapjai</span><span class="sxs-lookup"><span data-stu-id="77299-103">Windows PowerShell Basics</span></span>
<span data-ttu-id="77299-104">Grafikus felhasználói felületeket bizonyos alapvető fogalmakkal, amelyek a jól ismert, hogy a számítógép-felhasználók használja.</span><span class="sxs-lookup"><span data-stu-id="77299-104">Graphical user interfaces use some basic concepts that are well known to most computer users.</span></span> <span data-ttu-id="77299-105">Felhasználók ezek a feladatok végrehajtásához felületek szoftverben támaszkodnak.</span><span class="sxs-lookup"><span data-stu-id="77299-105">Users rely on the familiarity of those interfaces to accomplish tasks.</span></span> <span data-ttu-id="77299-106">Operációs rendszer jelenlegi felhasználók tallózható, általában az adott funkciót és a helyi menük környezetfüggő funkció eléréséhez eléréséhez legördülő menükben elemekre grafikus ábrázolása.</span><span class="sxs-lookup"><span data-stu-id="77299-106">Operating systems present users with a graphical representation of items that can be browsed, usually with drop-down menus for accessing specific functionality and context menus for accessing context-specific functionality.</span></span>

<span data-ttu-id="77299-107">Például a Windows PowerShell parancssori felület (CLI) kell használnia egy másik módszert információt teszi közzé, mert menük vagy grafikus rendszerek, hogy a felhasználó nem rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="77299-107">A command-line interface (CLI), such as Windows PowerShell, must use a different approach to expose information, because it does not have menus or graphical systems to help the user.</span></span> <span data-ttu-id="77299-108">A parancsnév előtti azokat kell.</span><span class="sxs-lookup"><span data-stu-id="77299-108">You need to know command names before you can use them.</span></span> <span data-ttu-id="77299-109">Bár a szolgáltatások grafikus felhasználói Felülettel környezetben egyenértékű összetett parancsok adhatja meg, meg kell a gyakran használt parancsok és megismerése parancs paraméterei.</span><span class="sxs-lookup"><span data-stu-id="77299-109">Although you can type complex commands that are equivalent to the features in a GUI environment, you must become familiar with commonly-used commands and command parameters.</span></span>

<span data-ttu-id="77299-110">A legtöbb CLIs nem rendelkeznek, amelyek segítségével a felhasználó a felület további minták.</span><span class="sxs-lookup"><span data-stu-id="77299-110">Most CLIs do not have patterns that can help the user to learn the interface.</span></span> <span data-ttu-id="77299-111">CLIs volt az első operációs rendszer ismertetése, mivel számos parancs és a paraméter nevének sincs kijelölve önkényesen.</span><span class="sxs-lookup"><span data-stu-id="77299-111">Because CLIs were the first operating system shells, many command names and parameter names were selected arbitrarily.</span></span> <span data-ttu-id="77299-112">Tömör parancs neve általában keresztül egyértelmű ők lettek választható.</span><span class="sxs-lookup"><span data-stu-id="77299-112">Terse command names were generally chosen over clear ones.</span></span> <span data-ttu-id="77299-113">Bár a legtöbb CLIs integrált Súgó rendszer és a parancs tervezési szabványok, általában tervezték őket a legkorábbi parancsok kompatibilisek, a parancskészlethez továbbra is alakú által döntések évtizedekben telt el.</span><span class="sxs-lookup"><span data-stu-id="77299-113">Although help systems and command design standards are integrated into most CLIs, they have been generally designed for compatibility with the earliest commands, so the command set is still shaped by decisions made decades ago.</span></span>

<span data-ttu-id="77299-114">A Windows PowerShell előnyeit CLIs történelmi ismerete egy felhasználó úgy lett kialakítva.</span><span class="sxs-lookup"><span data-stu-id="77299-114">Windows PowerShell was designed to take advantage of a user's historic knowledge of CLIs.</span></span> <span data-ttu-id="77299-115">Ebben a fejezetben előadás néhány alapvető eszközök és a fogalmakat, amelyek segítségével gyorsan további Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77299-115">In this chapter, we will talk about some basic tools and concepts that you can use to learn Windows PowerShell quickly.</span></span> <span data-ttu-id="77299-116">Ezek a következők:</span><span class="sxs-lookup"><span data-stu-id="77299-116">They include:</span></span>

- <span data-ttu-id="77299-117">Get-parancs használatával</span><span class="sxs-lookup"><span data-stu-id="77299-117">Using Get-Command</span></span>

- <span data-ttu-id="77299-118">Cmd.exe és UNIX-parancsok használatával</span><span class="sxs-lookup"><span data-stu-id="77299-118">Using Cmd.exe and UNIX commands</span></span>

- <span data-ttu-id="77299-119">Külső parancsok használata</span><span class="sxs-lookup"><span data-stu-id="77299-119">Using External Commands</span></span>

- <span data-ttu-id="77299-120">Kiegészítést használata</span><span class="sxs-lookup"><span data-stu-id="77299-120">Using Tab-Completion</span></span>

- <span data-ttu-id="77299-121">Get-Help használatával</span><span class="sxs-lookup"><span data-stu-id="77299-121">Using Get-Help</span></span>

