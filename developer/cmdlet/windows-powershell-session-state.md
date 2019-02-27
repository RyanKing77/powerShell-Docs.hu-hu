---
title: Windows PowerShell munkamenet-állapot |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Cmdlets [PowerShell], session state
- session state [PowerShell]
ms.assetid: 74912940-2b10-4a76-b174-6d035d71c02b
caps.latest.revision: 8
ms.openlocfilehash: 5d4effb508c9f2544832dad557671520cb0a7ac7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851701"
---
# <a name="windows-powershell-session-state"></a><span data-ttu-id="53fbb-102">Windows PowerShell-munkamenet állapota</span><span class="sxs-lookup"><span data-stu-id="53fbb-102">Windows PowerShell Session State</span></span>

<span data-ttu-id="53fbb-103">A munkamenet-állapot hivatkozik egy Windows PowerShell-munkamenetben vagy a modul az aktuális konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="53fbb-103">Session state refers to the current configuration of a Windows PowerShell session or module.</span></span> <span data-ttu-id="53fbb-104">Egy Windows PowerShell-munkamenetet a megfelelő operatív környezetet interaktív módon használja a parancssori felhasználói vagy programozott módon a gazdaalkalmazást.</span><span class="sxs-lookup"><span data-stu-id="53fbb-104">A Windows PowerShell session is the operational environment that is used interactively by the command-line user or programmatically by a host application.</span></span> <span data-ttu-id="53fbb-105">A munkamenet-állapot, a munkamenet a globális munkamenet-állapot nevezzük.</span><span class="sxs-lookup"><span data-stu-id="53fbb-105">The session state for a session is referred to as the global session state.</span></span>

<span data-ttu-id="53fbb-106">Fejlesztői szemszögből egy Windows PowerShell-munkamenetet egy fogadó alkalmazás megnyitásakor egy Windows PowerShell futási teret, és ha lezárja a futási térben közötti időt jelenti.</span><span class="sxs-lookup"><span data-stu-id="53fbb-106">From a developer perspective, a Windows PowerShell session refers to the time between when a host application opens a Windows PowerShell runspace and when it closes the runspace.</span></span> <span data-ttu-id="53fbb-107">A munkamenet tekintett meg egy másik módja, a Windows PowerShell-motor hív meg, amíg a futási térben létezik egy példányát élettartama.</span><span class="sxs-lookup"><span data-stu-id="53fbb-107">Looked at another way, the session is the lifetime of an instance of the Windows PowerShell engine that is invoked while the runspace exists.</span></span>

## <a name="module-session-state"></a><span data-ttu-id="53fbb-108">A modul munkamenet-állapot</span><span class="sxs-lookup"><span data-stu-id="53fbb-108">Module Session State</span></span>

<span data-ttu-id="53fbb-109">A modul munkamenet-állapotok jönnek létre, amikor a modulban vagy a beágyazott modulok egyike a munkamenet importálva.</span><span class="sxs-lookup"><span data-stu-id="53fbb-109">Module session states are created whenever the module or one of its nested modules is imported into the session.</span></span> <span data-ttu-id="53fbb-110">Amikor egy modul egy elem, például a parancsmag, függvény vagy parancsfájl exportálja, egy hivatkozás, hogy hozzáadódik a globális munkamenet-állapot, a munkamenet.</span><span class="sxs-lookup"><span data-stu-id="53fbb-110">When a module exports an element such as a cmdlet, function, or script, a reference to that element is added to the global session state of the session.</span></span> <span data-ttu-id="53fbb-111">Azonban az elem futtatásakor hajtja azt végre a munkamenet-állapot, a modul belül.</span><span class="sxs-lookup"><span data-stu-id="53fbb-111">However, when the element is run, it is executed within the session state of the module.</span></span>

## <a name="session-state-data"></a><span data-ttu-id="53fbb-112">Munkamenet-állapot adatait</span><span class="sxs-lookup"><span data-stu-id="53fbb-112">Session-State Data</span></span>

<span data-ttu-id="53fbb-113">Munkamenet-állapot adatainak nyilvános vagy privát is lehet.</span><span class="sxs-lookup"><span data-stu-id="53fbb-113">Session state data can be public or private.</span></span> <span data-ttu-id="53fbb-114">Nyilvános adatok a munkamenet-állapot kívülről érkező hívások számára érhető el, nem csak a munkamenet-állapot belül hívásait érhető el privát adatok esetében.</span><span class="sxs-lookup"><span data-stu-id="53fbb-114">Public data is available to calls from outside the session state while private data is available only to calls from within the session state.</span></span> <span data-ttu-id="53fbb-115">Például a modul rendelkezhet titkos függvény, amely csak a modul által, vagy csak belső hívható által exportált nyilvános prvek.</span><span class="sxs-lookup"><span data-stu-id="53fbb-115">For example, a module can have a private function that can be called only by the module or only internally by a public element that has been exported.</span></span> <span data-ttu-id="53fbb-116">Ez hasonlít a nyilvános és egy .NET-keretrendszer típusú tagok.</span><span class="sxs-lookup"><span data-stu-id="53fbb-116">This is similar to the private and public members of a .NET Framework type.</span></span>

<span data-ttu-id="53fbb-117">A végrehajtó motor az aktuális Windows PowerShell-munkamenet környezetében az aktuális példánya a munkamenet-állapot adatait tárolja.</span><span class="sxs-lookup"><span data-stu-id="53fbb-117">Session-state data is stored by the current instance of the execution engine within the context of the current Windows PowerShell session.</span></span> <span data-ttu-id="53fbb-118">Munkamenet-állapot adatait a következő elemek alkotják:</span><span class="sxs-lookup"><span data-stu-id="53fbb-118">Session-state data consists of the following items:</span></span>

- <span data-ttu-id="53fbb-119">Elérési út</span><span class="sxs-lookup"><span data-stu-id="53fbb-119">Path information</span></span>

- <span data-ttu-id="53fbb-120">Meghajtó adatai</span><span class="sxs-lookup"><span data-stu-id="53fbb-120">Drive information</span></span>

- <span data-ttu-id="53fbb-121">Windows PowerShell szolgáltató adatai</span><span class="sxs-lookup"><span data-stu-id="53fbb-121">Windows PowerShell provider information</span></span>

- <span data-ttu-id="53fbb-122">Információk az importált modulok és a modul elem (például a parancsmagok, függvények és parancsfájlok), amely a modul által exportált mutató hivatkozásokat.</span><span class="sxs-lookup"><span data-stu-id="53fbb-122">Information about the imported modules and references to the module elements (such as cmdlets, functions, and scripts) that are exported by the module.</span></span> <span data-ttu-id="53fbb-123">Ezt az információt, és ezeket a hivatkozásokat olyan, csak a globális munkamenet-állapot.</span><span class="sxs-lookup"><span data-stu-id="53fbb-123">This information and these references are for the global session state only.</span></span>

- <span data-ttu-id="53fbb-124">Változó adatainak munkamenet-állapot</span><span class="sxs-lookup"><span data-stu-id="53fbb-124">Session-state variable information</span></span>

## <a name="accessing-session-state-data-within-cmdlets"></a><span data-ttu-id="53fbb-125">A munkamenet-állapot adatainak parancsmagokban elérése</span><span class="sxs-lookup"><span data-stu-id="53fbb-125">Accessing Session-State Data Within Cmdlets</span></span>

<span data-ttu-id="53fbb-126">Parancsmagok vagy érhessék el az adatokat a munkamenet-állapot keresztül közvetve a [System.Management.Automation.Pscmdlet.Sessionstate\*](/dotnet/api/System.Management.Automation.PSCmdlet.SessionState) parancsmag osztály vagy közvetlenül a tulajdonság a [ System.Management.Automation.Sessionstate](/dotnet/api/System.Management.Automation.SessionState) osztály.</span><span class="sxs-lookup"><span data-stu-id="53fbb-126">Cmdlets can access session-state data either indirectly through the [System.Management.Automation.Pscmdlet.Sessionstate\*](/dotnet/api/System.Management.Automation.PSCmdlet.SessionState) property of the cmdlet class or directly through the [System.Management.Automation.Sessionstate](/dotnet/api/System.Management.Automation.SessionState) class.</span></span> <span data-ttu-id="53fbb-127">A [System.Management.Automation.Sessionstate](/dotnet/api/System.Management.Automation.SessionState) osztály biztosít, amelyek segítségével megvizsgálhatja a munkamenet-állapot adatait különböző típusú tulajdonságok.</span><span class="sxs-lookup"><span data-stu-id="53fbb-127">The [System.Management.Automation.Sessionstate](/dotnet/api/System.Management.Automation.SessionState) class provides properties that can be used to investigate different types of session-state data.</span></span>

## <a name="see-also"></a><span data-ttu-id="53fbb-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="53fbb-128">See Also</span></span>

[<span data-ttu-id="53fbb-129">System.Management.Automation.Pscmdlet.Sessionstate</span><span class="sxs-lookup"><span data-stu-id="53fbb-129">System.Management.Automation.Pscmdlet.Sessionstate</span></span>](/dotnet/api/System.Management.Automation.PSCmdlet.SessionState)

[<span data-ttu-id="53fbb-130">System.Management.Automation.Sessionstate?Displayproperty=Fullname</span><span class="sxs-lookup"><span data-stu-id="53fbb-130">System.Management.Automation.Sessionstate?Displayproperty=Fullname</span></span>](/dotnet/api/System.Management.Automation.SessionState)

[<span data-ttu-id="53fbb-131">Windows PowerShell-parancsmagok</span><span class="sxs-lookup"><span data-stu-id="53fbb-131">Windows PowerShell Cmdlets</span></span>](./cmdlet-overview.md)

[<span data-ttu-id="53fbb-132">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="53fbb-132">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="53fbb-133">Windows PowerShell Shell SDK</span><span class="sxs-lookup"><span data-stu-id="53fbb-133">Windows PowerShell Shell SDK</span></span>](../windows-powershell-reference.md)
