---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A PowerShell lap létrehozása a Windows PowerShell ISE"
ms.assetid: c10c18c7-9ece-4fd0-83dc-a19c53d4fd83
ms.openlocfilehash: 3cfeb18babe6b63f0e02da8cf0fd460950f1afce
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="how-to-create-a-powershell-tab-in-windows-powershell-ise"></a><span data-ttu-id="22091-103">A PowerShell lap létrehozása a Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="22091-103">How to Create a PowerShell Tab in Windows PowerShell ISE</span></span>
<span data-ttu-id="22091-104">Lapok a a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) lehetővé teszi, hogy egyszerre hozzon létre, és ugyanahhoz az alkalmazáshoz belül több végrehajtási környezetet használja.</span><span class="sxs-lookup"><span data-stu-id="22091-104">Tabs in the Windows PowerShell Integrated Scripting Environment (ISE) allow you to simultaneously create and use several execution environments within the same application.</span></span>
<span data-ttu-id="22091-105">PowerShell lapokon megfelel egy külön végrehajtási környezet vagy a munkamenet.</span><span class="sxs-lookup"><span data-stu-id="22091-105">Each PowerShell tab corresponds to a separate execution environment or session.</span></span>

> <span data-ttu-id="22091-106">**MEGJEGYZÉS:**:</span><span class="sxs-lookup"><span data-stu-id="22091-106">**NOTE**:</span></span>
>
> <span data-ttu-id="22091-107">Változók, funkcióit és az egyik lapon létrehozott aliasok nem jelenik meg egy másik.</span><span class="sxs-lookup"><span data-stu-id="22091-107">Variables, functions, and aliases that you create in one tab do not carry over to another.</span></span> <span data-ttu-id="22091-108">Azok a különböző Windows PowerShell-munkamenetekben.</span><span class="sxs-lookup"><span data-stu-id="22091-108">They are different Windows PowerShell sessions.</span></span>

<span data-ttu-id="22091-109">Az alábbi lépések segítségével megnyitása és bezárása egy Windows PowerShell lapján.</span><span class="sxs-lookup"><span data-stu-id="22091-109">Use the following steps to open or close a tab in Windows PowerShell.</span></span>
<span data-ttu-id="22091-110">Nevezze át a lapon, állítsa be a [DisplayName](The-PowerShellTab-Object.md#displayname) a Windows PowerShell lapon scripting objektum tulajdonságát.</span><span class="sxs-lookup"><span data-stu-id="22091-110">To rename a tab, set the [DisplayName](The-PowerShellTab-Object.md#displayname) property on the Windows PowerShell Tab scripting object.</span></span>

## <a name="to-create-and-use-a-new-powershell-tab"></a><span data-ttu-id="22091-111">Hozzon létre, és egy új PowerShell lapon</span><span class="sxs-lookup"><span data-stu-id="22091-111">To create and use a new PowerShell Tab</span></span>

<span data-ttu-id="22091-112">Az a **fájl** menüben kattintson a **új PowerShell lapon**. Az új PowerShell lapon mindig weblapként jelennek meg az aktív ablak.</span><span class="sxs-lookup"><span data-stu-id="22091-112">On the **File** menu, click **New PowerShell Tab**. The new PowerShell tab always opens as the active window.</span></span>
<span data-ttu-id="22091-113">PowerShell lapok Növekményesen számozása a ahhoz, azok megnyitása.</span><span class="sxs-lookup"><span data-stu-id="22091-113">PowerShell tabs are incrementally numbered in the order that they are opened.</span></span>
<span data-ttu-id="22091-114">Minden lap társítva a saját Windows PowerShell-konzolablakot.</span><span class="sxs-lookup"><span data-stu-id="22091-114">Each tab is associated with its own Windows PowerShell console window.</span></span>
<span data-ttu-id="22091-115">A saját munkamenet megnyitása (Ez a korlátozott Windows PowerShell ISE 2.0 8.) egyszerre legfeljebb 32 PowerShell lapokon lehet</span><span class="sxs-lookup"><span data-stu-id="22091-115">You can have up to 32 PowerShell tabs with their own session open at a time (this is limited to 8 on Windows PowerShell ISE 2.0.)</span></span>

<span data-ttu-id="22091-116">Vegye figyelembe, hogy gombra kattintva a **új** vagy **nyitott** az eszköztáron látható ikonok hozzon létre egy új lapon külön munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="22091-116">Note that clicking the **New** or **Open** icons on the toolbar does not create a new tab with a separate session.</span></span>
<span data-ttu-id="22091-117">Ehelyett a gombok egy munkamenet-nyisson meg egy új vagy meglévő parancsfájl a jelenleg aktív lapon.</span><span class="sxs-lookup"><span data-stu-id="22091-117">Instead, those buttons open a new or existing script file on the currently active tab with a session.</span></span>
<span data-ttu-id="22091-118">Fájlok nyissa meg az egyes lapon és a munkamenet több parancsfájlt is.</span><span class="sxs-lookup"><span data-stu-id="22091-118">You can have multiple script files open with each tab and session.</span></span>
<span data-ttu-id="22091-119">A parancsprogram lapfülek munkamenet csak alatt jelennek meg a munkamenet lapok aktív a társított munkamenet esetén.</span><span class="sxs-lookup"><span data-stu-id="22091-119">The script tabs for a session only appear below the session tabs when the associated session is active.</span></span>

<span data-ttu-id="22091-120">A PowerShell lapon aktívvá tételéhez kattintson a lap. Jelölje be minden nyitott, a PowerShell-lapról a **nézet** menüben kattintson a használni kívánt PowerShell fülre.</span><span class="sxs-lookup"><span data-stu-id="22091-120">To make a PowerShell tab active, click the tab. To select from all PowerShell tabs that are open, on the **View** menu, click the PowerShell tab you want to use.</span></span>

## <a name="to-create-and-use-a-new-remote-powershell-tab"></a><span data-ttu-id="22091-121">Hozzon létre, és egy új távoli PowerShell lapon</span><span class="sxs-lookup"><span data-stu-id="22091-121">To create and use a new Remote PowerShell tab</span></span>

<span data-ttu-id="22091-122">Az a **fájl** menüben kattintson a **új távoli PowerShell lapon** hozzon létre egy munkamenetet egy távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="22091-122">On the **File** menu, click **New Remote PowerShell Tab** to establish a session on a remote computer.</span></span>
<span data-ttu-id="22091-123">Egy párbeszédpanel jelenik meg, és megkéri, hogy adja meg a távoli kapcsolat létrehozásához szükséges adatokat.</span><span class="sxs-lookup"><span data-stu-id="22091-123">A dialog box appears and prompts you to enter details required to establish the remote connection.</span></span>
<span data-ttu-id="22091-124">A távoli lapon funkciók ugyanúgy, mint az egy helyi PowerShell lap, de a parancsok és parancsfájlok futnak a távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="22091-124">The remote tab functions just like a local PowerShell tab, but the commands and scripts are run on the remote computer.</span></span>

## <a name="to-close-a-powershell-tab"></a><span data-ttu-id="22091-125">A PowerShell lap bezárásához</span><span class="sxs-lookup"><span data-stu-id="22091-125">To close a PowerShell Tab</span></span>

<span data-ttu-id="22091-126">Zárja be a lapon, az alábbi módszerek bármelyikét használhatja:</span><span class="sxs-lookup"><span data-stu-id="22091-126">To close a tab, you can use any of the following techniques:</span></span>

- <span data-ttu-id="22091-127">Kattintson a bezárni kívánt fülre.</span><span class="sxs-lookup"><span data-stu-id="22091-127">Click the tab that you want to close.</span></span>

- <span data-ttu-id="22091-128">Az a **fájl** menüben kattintson a **PowerShell lap bezárása**, vagy kattintson a Bezárás gombra (**X**) egy aktív lapon a lap bezárásához.</span><span class="sxs-lookup"><span data-stu-id="22091-128">On the **File** menu, click **Close PowerShell Tab**, or click  the Close button  (**X**) on an active tab to close the tab.</span></span>

<span data-ttu-id="22091-129">Ha mentette a fájlok megnyitása a PowerShell lapon, hogy bezárja, mentse vagy vesse el őket kéri.</span><span class="sxs-lookup"><span data-stu-id="22091-129">If you have unsaved files open in the PowerShell tab that you are closing, you are prompted to save or discard them.</span></span>
<span data-ttu-id="22091-130">A parancsfájl mentése kapcsolatos további információkért lásd: [a parancsfájl mentése hogyan](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).</span><span class="sxs-lookup"><span data-stu-id="22091-130">For more information about how to save a script, see [How to Save a Script](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).</span></span>

## <a name="see-also"></a><span data-ttu-id="22091-131">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="22091-131">See Also</span></span>

- [<span data-ttu-id="22091-132">A Windows PowerShell ISE használatával</span><span class="sxs-lookup"><span data-stu-id="22091-132">Using the Windows PowerShell ISE</span></span>](Using-the-Windows-PowerShell-ISE.md)
- [<span data-ttu-id="22091-133">A konzol ablaktáblában a Windows PowerShell ISE használata</span><span class="sxs-lookup"><span data-stu-id="22091-133">How to Use the Console Pane in the Windows PowerShell ISE</span></span>](How-to-Use-the-Console-Pane-in-the-Windows-PowerShell-ISE.md)

