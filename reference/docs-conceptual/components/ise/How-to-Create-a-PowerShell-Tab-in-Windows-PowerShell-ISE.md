---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: PowerShell-lap létrehozása a Windows PowerShell ISE-ben
ms.assetid: c10c18c7-9ece-4fd0-83dc-a19c53d4fd83
ms.openlocfilehash: 080fe89bf1443f51460589b445431913fa20b4b8
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057740"
---
# <a name="how-to-create-a-powershell-tab-in-windows-powershell-ise"></a><span data-ttu-id="437e9-103">PowerShell-lap létrehozása a Windows PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="437e9-103">How to Create a PowerShell Tab in Windows PowerShell ISE</span></span>

<span data-ttu-id="437e9-104">Lapok a a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) lehetővé teszi, hogy egyszerre hozzon létre, és használja ugyanazt az alkalmazást belül több végrehajtási környezet.</span><span class="sxs-lookup"><span data-stu-id="437e9-104">Tabs in the Windows PowerShell Integrated Scripting Environment (ISE) allow you to simultaneously create and use several execution environments within the same application.</span></span>
<span data-ttu-id="437e9-105">Egyes PowerShell-lap egy különálló környezetben vagy a munkamenet felel meg.</span><span class="sxs-lookup"><span data-stu-id="437e9-105">Each PowerShell tab corresponds to a separate execution environment or session.</span></span>

> [!NOTE]
> <span data-ttu-id="437e9-106">Változók, a functions és a aliasról, amelyek egy lapot hoz létre a másikra nem kerülnek át.</span><span class="sxs-lookup"><span data-stu-id="437e9-106">Variables, functions, and aliases that you create in one tab do not carry over to another.</span></span> <span data-ttu-id="437e9-107">Azok a különböző Windows PowerShell-munkameneteket.</span><span class="sxs-lookup"><span data-stu-id="437e9-107">They are different Windows PowerShell sessions.</span></span>

<span data-ttu-id="437e9-108">A következő lépések segítségével megnyitása vagy bezárása egy lapon, a Windows PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="437e9-108">Use the following steps to open or close a tab in Windows PowerShell.</span></span>
<span data-ttu-id="437e9-109">Nevezze át a lapon, állítsa be a [DisplayName](object-model/The-PowerShellTab-Object.md#displayname) a Windows PowerShell-lap scripting objektum tulajdonságának.</span><span class="sxs-lookup"><span data-stu-id="437e9-109">To rename a tab, set the [DisplayName](object-model/The-PowerShellTab-Object.md#displayname) property on the Windows PowerShell Tab scripting object.</span></span>

## <a name="to-create-and-use-a-new-powershell-tab"></a><span data-ttu-id="437e9-110">Hozhat létre és használhat egy új PowerShell-lap</span><span class="sxs-lookup"><span data-stu-id="437e9-110">To create and use a new PowerShell Tab</span></span>

<span data-ttu-id="437e9-111">Az a **fájl** menüben kattintson a **új PowerShell-lap**. Az új PowerShell-lap mindig az aktív ablak nyílik meg.</span><span class="sxs-lookup"><span data-stu-id="437e9-111">On the **File** menu, click **New PowerShell Tab**. The new PowerShell tab always opens as the active window.</span></span>
<span data-ttu-id="437e9-112">PowerShell-lapok növekményes számozása ahhoz, hogy meg vannak nyitva.</span><span class="sxs-lookup"><span data-stu-id="437e9-112">PowerShell tabs are incrementally numbered in the order that they are opened.</span></span>
<span data-ttu-id="437e9-113">Minden lap társítva a saját Windows PowerShell-konzolablakot.</span><span class="sxs-lookup"><span data-stu-id="437e9-113">Each tab is associated with its own Windows PowerShell console window.</span></span>
<span data-ttu-id="437e9-114">Legfeljebb 32 PowerShell lapokat, egyszerre (Ez a korlátozott, a Windows PowerShell ISE 2.0 8-ra.) nyissa meg a saját munkamenettel is rendelkezhet</span><span class="sxs-lookup"><span data-stu-id="437e9-114">You can have up to 32 PowerShell tabs with their own session open at a time (this is limited to 8 on Windows PowerShell ISE 2.0.)</span></span>

<span data-ttu-id="437e9-115">Vegye figyelembe, hogy kattint a **új** vagy **nyílt** az eszköztár ikonjainak hozzon létre egy új lap egy külön munkamenetben.</span><span class="sxs-lookup"><span data-stu-id="437e9-115">Note that clicking the **New** or **Open** icons on the toolbar does not create a new tab with a separate session.</span></span>
<span data-ttu-id="437e9-116">Ehelyett ezekre a gombokra nyisson meg egy új vagy meglévő parancsfájl a jelenleg aktív lapon egy munkamenetet.</span><span class="sxs-lookup"><span data-stu-id="437e9-116">Instead, those buttons open a new or existing script file on the currently active tab with a session.</span></span>
<span data-ttu-id="437e9-117">Fájlok meg minden egyes lapon és a munkamenet több szkript is rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="437e9-117">You can have multiple script files open with each tab and session.</span></span>
<span data-ttu-id="437e9-118">A munkamenet a parancsfájl lapok csak alatt jelennek meg a munkamenet-lapok Ha a társított munkamenet aktív.</span><span class="sxs-lookup"><span data-stu-id="437e9-118">The script tabs for a session only appear below the session tabs when the associated session is active.</span></span>

<span data-ttu-id="437e9-119">Ahhoz, hogy aktív PowerShell-lap, kattintson a lap. Jelölje be minden megnyitott, a PowerShell-lap a **nézet** menüben kattintson a használni kívánt PowerShell fülre.</span><span class="sxs-lookup"><span data-stu-id="437e9-119">To make a PowerShell tab active, click the tab. To select from all PowerShell tabs that are open, on the **View** menu, click the PowerShell tab you want to use.</span></span>

## <a name="to-create-and-use-a-new-remote-powershell-tab"></a><span data-ttu-id="437e9-120">Hozhat létre és használhat egy új távoli PowerShell-lap</span><span class="sxs-lookup"><span data-stu-id="437e9-120">To create and use a new Remote PowerShell tab</span></span>

<span data-ttu-id="437e9-121">Az a **fájl** menüben kattintson a **új távoli PowerShell-lap** hozzon létre egy munkamenetet egy távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="437e9-121">On the **File** menu, click **New Remote PowerShell Tab** to establish a session on a remote computer.</span></span>
<span data-ttu-id="437e9-122">Egy párbeszédpanel jelenik meg, és megkéri, hogy adja meg a távoli kapcsolat létrehozásához szükséges adatokat.</span><span class="sxs-lookup"><span data-stu-id="437e9-122">A dialog box appears and prompts you to enter details required to establish the remote connection.</span></span>
<span data-ttu-id="437e9-123">A Távoli használat lapról funkciók ugyanúgy mint egy helyi PowerShell-lap, de a parancsokat és szkripteket a távoli számítógépen futnak.</span><span class="sxs-lookup"><span data-stu-id="437e9-123">The remote tab functions just like a local PowerShell tab, but the commands and scripts are run on the remote computer.</span></span>

## <a name="to-close-a-powershell-tab"></a><span data-ttu-id="437e9-124">PowerShell-lap bezárása</span><span class="sxs-lookup"><span data-stu-id="437e9-124">To close a PowerShell Tab</span></span>

<span data-ttu-id="437e9-125">A lap bezárásához, az alábbi módszerek bármelyikét használhatja:</span><span class="sxs-lookup"><span data-stu-id="437e9-125">To close a tab, you can use any of the following techniques:</span></span>

- <span data-ttu-id="437e9-126">Kattintson a gombra kattintva zárja be a kívánt lapra.</span><span class="sxs-lookup"><span data-stu-id="437e9-126">Click the tab that you want to close.</span></span>

- <span data-ttu-id="437e9-127">Az a **fájl** menüben kattintson a **PowerShell-lap bezárásához**, vagy kattintson a Bezárás gombra (**X**) egy aktív lapon a lap bezárásához.</span><span class="sxs-lookup"><span data-stu-id="437e9-127">On the **File** menu, click **Close PowerShell Tab**, or click  the Close button  (**X**) on an active tab to close the tab.</span></span>

<span data-ttu-id="437e9-128">Ha mentette a fájlokat nyissa meg a PowerShell-lap, hogy bezárásakor, mentse vagy vesse el azokat kéri.</span><span class="sxs-lookup"><span data-stu-id="437e9-128">If you have unsaved files open in the PowerShell tab that you are closing, you are prompted to save or discard them.</span></span>
<span data-ttu-id="437e9-129">Mentse a parancsfájlt kapcsolatos további információkért lásd: [egy parancsfájl mentése hogyan](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).</span><span class="sxs-lookup"><span data-stu-id="437e9-129">For more information about how to save a script, see [How to Save a Script](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).</span></span>

## <a name="see-also"></a><span data-ttu-id="437e9-130">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="437e9-130">See Also</span></span>

- [<span data-ttu-id="437e9-131">A Windows PowerShell ISE bemutatása</span><span class="sxs-lookup"><span data-stu-id="437e9-131">Introducing the Windows PowerShell ISE</span></span>](Introducing-the-Windows-PowerShell-ISE.md)
- [<span data-ttu-id="437e9-132">A konzol panel használata a Windows PowerShell ISE-ben</span><span class="sxs-lookup"><span data-stu-id="437e9-132">How to Use the Console Pane in the Windows PowerShell ISE</span></span>](How-to-Use-the-Console-Pane-in-the-Windows-PowerShell-ISE.md)