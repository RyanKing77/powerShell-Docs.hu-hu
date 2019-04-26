---
title: Windows PowerShell-munkafolyamat írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2551ceed-836f-4275-9fc0-ea68446d6a35
caps.latest.revision: 7
ms.openlocfilehash: 4f0be193fb5b5c753d040a48e5f49235ece11708
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62080322"
---
# <a name="writing-a-windows-powershell-workflow"></a><span data-ttu-id="985ef-102">Windows PowerShell-munkafolyamat írása</span><span class="sxs-lookup"><span data-stu-id="985ef-102">Writing a Windows PowerShell Workflow</span></span>

<span data-ttu-id="985ef-103">Létrehozhat egy XAML munkafolyamat adja hozzá a Windows PowerShell szerelvények a Visual Studio munkafolyamat-tervező által elérhetővé tett tevékenységeket.</span><span class="sxs-lookup"><span data-stu-id="985ef-103">You can create a XAML workflow by adding activities exposed by Windows PowerShell assemblies to the Workflow designer in Visual Studio.</span></span> <span data-ttu-id="985ef-104">A következő Windows PowerShell-szerelvények elérhetővé teszik a tevékenységek munkafolyamat-kompatibilis.</span><span class="sxs-lookup"><span data-stu-id="985ef-104">The following Windows PowerShell assemblies expose workflow-enabled activities.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="985ef-105">Egy XAML-munkafolyamatot modulként be kell csomagolni, ha lehetővé szeretné tenni a munkafolyamathoz tartozó súgó.</span><span class="sxs-lookup"><span data-stu-id="985ef-105">A XAML workflow must be packaged as a module if you want to provide help for the workflow.</span></span> <span data-ttu-id="985ef-106">Modulok kapcsolatos információkért lásd: [Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="985ef-106">For information about modules, see [Writing a Windows PowerShell Module](../module/writing-a-windows-powershell-module.md).</span></span>

- [<span data-ttu-id="985ef-107">Microsoft.Powershell.Activities</span><span class="sxs-lookup"><span data-stu-id="985ef-107">Microsoft.Powershell.Activities</span></span>](/dotnet/api/Microsoft.PowerShell.Activities)

- [<span data-ttu-id="985ef-108">Microsoft.Powershell.Core.Activities</span><span class="sxs-lookup"><span data-stu-id="985ef-108">Microsoft.Powershell.Core.Activities</span></span>](/dotnet/api/Microsoft.PowerShell.Core.Activities)

- [<span data-ttu-id="985ef-109">Microsoft.Powershell.Diagnostics.Activities</span><span class="sxs-lookup"><span data-stu-id="985ef-109">Microsoft.Powershell.Diagnostics.Activities</span></span>](/dotnet/api/Microsoft.PowerShell.Diagnostics.Activities)

- [<span data-ttu-id="985ef-110">Microsoft.Powershell.Management.Activities</span><span class="sxs-lookup"><span data-stu-id="985ef-110">Microsoft.Powershell.Management.Activities</span></span>](/dotnet/api/Microsoft.PowerShell.Management.Activities)

- [<span data-ttu-id="985ef-111">Microsoft.Powershell.Security.Activities</span><span class="sxs-lookup"><span data-stu-id="985ef-111">Microsoft.Powershell.Security.Activities</span></span>](/dotnet/api/Microsoft.PowerShell.Security.Activities)

- [<span data-ttu-id="985ef-112">Microsoft.Powershell.Utility.Activities</span><span class="sxs-lookup"><span data-stu-id="985ef-112">Microsoft.Powershell.Utility.Activities</span></span>](/dotnet/api/Microsoft.PowerShell.Utility.Activities)

  <span data-ttu-id="985ef-113">A következő témakörök bemutatják, hogyan hozhat létre egy munkafolyamat tevékenységek Windows PowerShell használatával.</span><span class="sxs-lookup"><span data-stu-id="985ef-113">The following topics describe how to create a Workflow by using Windows PowerShell activities.</span></span>

- [<span data-ttu-id="985ef-114">Windows PowerShell-tevékenységek hozzáadása a Visual Studio-eszközkészlet</span><span class="sxs-lookup"><span data-stu-id="985ef-114">Adding Windows PowerShell Activities to the Visual Studio Toolbox</span></span>](./adding-windows-powershell-activities-to-the-visual-studio-toolbox.md)

- [<span data-ttu-id="985ef-115">Tevékenységek feldolgozása Windows PowerShell-munkafolyamat létrehozása</span><span class="sxs-lookup"><span data-stu-id="985ef-115">Creating a Workflow with Windows PowerShell Activities</span></span>](./creating-a-workflow-with-windows-powershell-activities.md)

- [<span data-ttu-id="985ef-116">A munkafolyamatok létrehozása a Windows PowerShell parancsfájl használatával</span><span class="sxs-lookup"><span data-stu-id="985ef-116">Creating a Workflow by Using a Windows PowerShell Script</span></span>](./creating-a-workflow-by-using-a-windows-powershell-script.md)

- [<span data-ttu-id="985ef-117">Importálás és a egy Windows PowerShell-munkafolyamat meghívása</span><span class="sxs-lookup"><span data-stu-id="985ef-117">Importing and Invoking a Windows PowerShell Workflow</span></span>](./importing-and-invoking-a-windows-powershell-workflow.md)

- [<span data-ttu-id="985ef-118">Egy munkafolyamat-tevékenységet hoz létre egy Windows PowerShell-parancsmag</span><span class="sxs-lookup"><span data-stu-id="985ef-118">Creating a Workflow Activity from a Windows PowerShell Cmdlet</span></span>](./creating-a-workflow-activity-from-a-windows-powershell-cmdlet.md)