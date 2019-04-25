---
title: Windows PowerShell-modul írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bfbccc5b-2b2b-432a-a971-9f8ab503cdc3
caps.latest.revision: 17
ms.openlocfilehash: 3c6d8e410427d6cfaa1c15db421b3fe935f7d322
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082056"
---
# <a name="writing-a-windows-powershell-module"></a><span data-ttu-id="10141-102">Windows PowerShell-modul írása</span><span class="sxs-lookup"><span data-stu-id="10141-102">Writing a Windows PowerShell Module</span></span>

<span data-ttu-id="10141-103">Ez a dokumentum íródott, a parancsfájl a fejlesztők és a parancsmag fejlesztőknek szól, akik csomagolása és terjesztése a Windows PowerShell-parancsmagokat kell.</span><span class="sxs-lookup"><span data-stu-id="10141-103">This document is written for administrators, script developers, and cmdlet developers who need to package and distribute their Windows PowerShell cmdlets.</span></span> <span data-ttu-id="10141-104">Windows PowerShell-modulok használatával csomagot, és terjesztése a Windows PowerShell-megoldások lefordított nyelv használata nélkül.</span><span class="sxs-lookup"><span data-stu-id="10141-104">By using Windows PowerShell modules, you can package and distribute your Windows PowerShell solutions without using a compiled language.</span></span>

<span data-ttu-id="10141-105">Windows PowerShell-modulok lehetővé teszi, hogy a partíció, rendszerezheti és a Windows PowerShell-kód absztrakt önálló, újrafelhasználható egységekbe.</span><span class="sxs-lookup"><span data-stu-id="10141-105">Windows PowerShell modules enable you to partition, organize, and abstract your Windows PowerShell code into self-contained, reusable units.</span></span> <span data-ttu-id="10141-106">Ezek újrafelhasználható egységgel egyszerűen oszthat meg másokkal közvetlenül a modulok.</span><span class="sxs-lookup"><span data-stu-id="10141-106">With these reusable units, you can easily share your modules directly with others.</span></span> <span data-ttu-id="10141-107">Ha a parancsfájl-fejlesztő, csomagolja újra külső modulról egyéni parancsfájl-alapú alkalmazások létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="10141-107">If you are a script developer, you can also repackage third-party modules to create custom script-based applications.</span></span> <span data-ttu-id="10141-108">Modulok, például a Perl, Python, és más programozási nyelven modulok hasonló, újrafelhasználható, szabadon terjeszthető összetevők használata további előnye, hogy ismételje meg a becsomagolást és absztrakt több összetevő lehetővé teszi, éles használatra kész-parancsfájl-kezelési megoldások engedélyezése egyéni megoldások létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="10141-108">Modules, similar to modules in other scripting languages such as Perl and Python, enable production-ready scripting solutions that use reusable, redistributable components, with the added benefit of enabling you to repackage and abstract multiple components to create custom solutions.</span></span>

<span data-ttu-id="10141-109">A legalapvetőbb, a Windows PowerShell egy .psm1 fájlban modulként mentett érvényes Windows PowerShell parancsfájl kód kezeli.</span><span class="sxs-lookup"><span data-stu-id="10141-109">At their most basic, Windows PowerShell will treat any valid Windows PowerShell script code saved in a .psm1 file as a module.</span></span> <span data-ttu-id="10141-110">PowerShell bármilyen bináris parancsmag szerelvény modulként automatikusan is kezeli.</span><span class="sxs-lookup"><span data-stu-id="10141-110">PowerShell will also automatically treat any binary cmdlet assembly as a module.</span></span> <span data-ttu-id="10141-111">Azonban használhatja egy modul (vagy még pontosabban egy moduljegyzék) szeretné a teljes megoldás együtt.</span><span class="sxs-lookup"><span data-stu-id="10141-111">However, you can also use a module (or more specifically, a module manifest) to bundle an entire solution together.</span></span> <span data-ttu-id="10141-112">A következő esetekben gyakori használati Windows PowerShell-modulok ismertetik.</span><span class="sxs-lookup"><span data-stu-id="10141-112">The following scenarios describe typical uses for Windows PowerShell modules.</span></span>

### <a name="libraries"></a><span data-ttu-id="10141-113">Kódtárak</span><span class="sxs-lookup"><span data-stu-id="10141-113">Libraries</span></span>

<span data-ttu-id="10141-114">Modulok segítségével csomagolása és terjesztése javul kódtárakat, függvények, amelyek a leggyakoribb feladatok végrehajtását.</span><span class="sxs-lookup"><span data-stu-id="10141-114">Modules can be used to package and distribute cohesive libraries of functions that perform common tasks.</span></span> <span data-ttu-id="10141-115">Általában ezek a függvények nevei oszthat meg egy vagy több főneveket, amely mutatja, hogy ezek a gyakori feladat.</span><span class="sxs-lookup"><span data-stu-id="10141-115">Typically, the names of these functions share one or more nouns that reflect the common task that they are used for.</span></span> <span data-ttu-id="10141-116">Ezek a függvények is lehet .NET-osztályok hasonló abban, hogy a nyilvános és privát tagokat is rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="10141-116">These functions can also be similar to .NET Framework classes in that they can have public and private members.</span></span> <span data-ttu-id="10141-117">Például egy könyvtár, Funkciók fájlátvitel tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="10141-117">For example, a library can contain a set of functions for file transfers.</span></span> <span data-ttu-id="10141-118">Ebben az esetben a főnév szótárral kezdheti az általános feladatban lehet "fájl."</span><span class="sxs-lookup"><span data-stu-id="10141-118">In this case, the noun reflecting the common task might be "file."</span></span>

### <a name="configuration"></a><span data-ttu-id="10141-119">Konfiguráció</span><span class="sxs-lookup"><span data-stu-id="10141-119">Configuration</span></span>

<span data-ttu-id="10141-120">Modulok segítségével testre szabhatja környezete egyes parancsmagokat, a szolgáltatók, a functions és a változók hozzáadásával.</span><span class="sxs-lookup"><span data-stu-id="10141-120">Modules can be used to customize your environment by adding specific cmdlets, providers, functions, and variables.</span></span>

### <a name="compiled-code-development-and-distribution"></a><span data-ttu-id="10141-121">Lefordított kódot fejlesztési és terjesztési</span><span class="sxs-lookup"><span data-stu-id="10141-121">Compiled Code Development and Distribution</span></span>

<span data-ttu-id="10141-122">A parancsmag és a szolgáltató fejlesztők modulok segítségével tesztelése és terjesztése a lefordított kódot anélkül, hogy a beépülő modulok létrehozása. A lefordított kódot modulként (bináris modult) tartalmazó szerelvény anélkül, hogy hozzon létre és regisztrálja a beépülő modulok importálhatja azokat.</span><span class="sxs-lookup"><span data-stu-id="10141-122">Cmdlet and provider developers can use modules to test and distribute their compiled code without needing to create snap-ins. They can import the assembly that contains the compiled code as a module (a binary module) without needing to create and register snap-ins.</span></span>

## <a name="see-also"></a><span data-ttu-id="10141-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="10141-123">See Also</span></span>

[<span data-ttu-id="10141-124">Egy Windows PowerShell-modul ismertetése</span><span class="sxs-lookup"><span data-stu-id="10141-124">Understanding a Windows PowerShell Module</span></span>](./understanding-a-windows-powershell-module.md)

[<span data-ttu-id="10141-125">Egy PowerShell-szkript-modul írása</span><span class="sxs-lookup"><span data-stu-id="10141-125">How to Write a PowerShell Script Module</span></span>](./how-to-write-a-powershell-script-module.md)

[<span data-ttu-id="10141-126">Egy bináris PowerShell-modul írása</span><span class="sxs-lookup"><span data-stu-id="10141-126">How to Write a PowerShell Binary Module</span></span>](./how-to-write-a-powershell-binary-module.md)

[<span data-ttu-id="10141-127">A PowerShell-modul jegyzék írása</span><span class="sxs-lookup"><span data-stu-id="10141-127">How to Write a PowerShell Module Manifest</span></span>](http://msdn.microsoft.com/en-us/abe4c24b-e64e-4a61-81d5-18c4fceba0b6)

[<span data-ttu-id="10141-128">A PSModulePath telepítési elérési út módosítása</span><span class="sxs-lookup"><span data-stu-id="10141-128">Modifying the PSModulePath Installation Path</span></span>](./modifying-the-psmodulepath-installation-path.md)

[<span data-ttu-id="10141-129">Egy PowerShell-modul importálása</span><span class="sxs-lookup"><span data-stu-id="10141-129">Importing a PowerShell Module</span></span>](./importing-a-powershell-module.md)

[<span data-ttu-id="10141-130">Egy PowerShell-modul telepítése</span><span class="sxs-lookup"><span data-stu-id="10141-130">Installing a PowerShell Module</span></span>](./installing-a-powershell-module.md)
