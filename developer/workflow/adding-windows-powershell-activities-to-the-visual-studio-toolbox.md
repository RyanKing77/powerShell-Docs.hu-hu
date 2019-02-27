---
title: Windows PowerShell-tevékenységek hozzáadása a Visual Studio-eszközkészlet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9c8ef289-0659-42d1-9976-044b144201eb
caps.latest.revision: 6
ms.openlocfilehash: 2a8372d937fc3c959f7d829bb52495048423d506
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56852107"
---
# <a name="adding-windows-powershell-activities-to-the-visual-studio-toolbox"></a><span data-ttu-id="bc6c9-102">Windows PowerShell-tevékenységek hozzáadása a Visual Studio Toolboxhoz</span><span class="sxs-lookup"><span data-stu-id="bc6c9-102">Adding Windows PowerShell Activities to the Visual Studio Toolbox</span></span>

<span data-ttu-id="bc6c9-103">Mielőtt egy PowerShell-munkafolyamat munkafolyamat-Tervező használatával hoz létre, először hozzá kell adnia a PowerShell-tevékenységek, egy Visual Studio munkafolyamat Konzolalkalmazás-projektet az eszközkészlet.</span><span class="sxs-lookup"><span data-stu-id="bc6c9-103">Before you author a PowerShell Workflow using Workflow Designer, you must first add the PowerShell Activities to the Toolbox in a Visual Studio Workflow console application project.</span></span> <span data-ttu-id="bc6c9-104">Az alábbi eljárás bemutatja, hogyan Microsoft.PowerShell.Core.Activities szerelvény a tevékenységek hozzáadása a Visual Studio-eszközkészlet.</span><span class="sxs-lookup"><span data-stu-id="bc6c9-104">The following procedure shows how to add the activities from the Microsoft.PowerShell.Core.Activities assembly to the Visual Studio toolbox.</span></span>

### <a name="adding-windows-powershell-activities-to-the-toolbox"></a><span data-ttu-id="bc6c9-105">Windows PowerShell-tevékenységek hozzáadása az eszközkészlethez</span><span class="sxs-lookup"><span data-stu-id="bc6c9-105">Adding Windows PowerShell Activities to the Toolbox</span></span>

1. <span data-ttu-id="bc6c9-106">Hozzon létre egy új munkafolyamat Konzolalkalmazás-projektet a Visual Studióban.</span><span class="sxs-lookup"><span data-stu-id="bc6c9-106">Create a new Workflow console application project in Visual Studio.</span></span>

2. <span data-ttu-id="bc6c9-107">Az a **nézet** menüben kattintson a **eszközkészlet**.</span><span class="sxs-lookup"><span data-stu-id="bc6c9-107">On the **View** menu, click **Toolbox**.</span></span>

3. <span data-ttu-id="bc6c9-108">Egy új lap hozzáadása az eszköztáron kattintson a jobb gombbal az eszközkészlet belül, és kattintson a **lap hozzáadása**, és az új lapon adjon meg egy nevet, például "PowerShell tevékenységek".</span><span class="sxs-lookup"><span data-stu-id="bc6c9-108">Add a new tab in the Toolbox by right-clicking inside the Toolbox and clicking **Add Tab**, and give the new tab a name such as "PowerShell Activities".</span></span>

   <span data-ttu-id="bc6c9-109">Egy lap hozzáadása lehetővé teszi, hogy a PowerShell tevékenységek eszközkészlet más eszközökből külön csoportot.</span><span class="sxs-lookup"><span data-stu-id="bc6c9-109">Adding a tab allows you to group the PowerShell Activities separate from other tools in the Toolbox.</span></span>

4. <span data-ttu-id="bc6c9-110">Az eszközkészlet új lapon kattintson a **elemek kiválasztása...** . A **eszközkészlet elemek kiválasztása** párbeszédpanel jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="bc6c9-110">On the new Toolbox tab, click **Choose Items...**. The **Choose Toolbox Items** dialog appears.</span></span>

5. <span data-ttu-id="bc6c9-111">Az a **eszközkészlet elemek kiválasztása** párbeszédpanelen kattintson a **System.Activities** fülre.</span><span class="sxs-lookup"><span data-stu-id="bc6c9-111">In the **Choose Toolbox Items** dialog, click the **System.Activities** tab.</span></span>

6. <span data-ttu-id="bc6c9-112">Kattintson a **Tallózás**.</span><span class="sxs-lookup"><span data-stu-id="bc6c9-112">Click **Browse**.</span></span>

7. <span data-ttu-id="bc6c9-113">Keresse meg a %WINDIR%\Microsoft.NET\assembly\GAC_MSIL\Microsoft.PowerShell.Core.Activities\v4.0_3.0.0.0__31bf3856ad364e mappát, és kattintson duplán a Microsoft.PowerShell.Core.Activities.dll.</span><span class="sxs-lookup"><span data-stu-id="bc6c9-113">Navigate to the %WINDIR%\Microsoft.NET\assembly\GAC_MSIL\Microsoft.PowerShell.Core.Activities\v4.0_3.0.0.0__31bf3856ad364e folder and double-click Microsoft.PowerShell.Core.Activities.dll.</span></span>

8. <span data-ttu-id="bc6c9-114">Kattintson az **OK** gombra.</span><span class="sxs-lookup"><span data-stu-id="bc6c9-114">Click **OK**.</span></span> <span data-ttu-id="bc6c9-115">A tevékenységek által a Microsoft.PowerShell.Core.Activities szerelvényben definiált mostantól elérhetők az eszközkészlet.</span><span class="sxs-lookup"><span data-stu-id="bc6c9-115">The activities defined by the Microsoft.PowerShell.Core.Activities assembly are now available in the toolbox.</span></span>

## <a name="see-also"></a><span data-ttu-id="bc6c9-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="bc6c9-116">See Also</span></span>

[<span data-ttu-id="bc6c9-117">Windows PowerShell-munkafolyamat írása</span><span class="sxs-lookup"><span data-stu-id="bc6c9-117">Writing a Windows PowerShell Workflow</span></span>](./writing-a-windows-powershell-workflow.md)

[<span data-ttu-id="bc6c9-118">Tevékenységek feldolgozása Windows PowerShell-munkafolyamat létrehozása</span><span class="sxs-lookup"><span data-stu-id="bc6c9-118">Creating a Workflow with Windows PowerShell Activities</span></span>](./creating-a-workflow-with-windows-powershell-activities.md)