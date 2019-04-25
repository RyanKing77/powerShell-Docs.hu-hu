---
title: Futási terek létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 17f323c3-e873-449e-8a28-477f1c6b5e12
caps.latest.revision: 6
ms.openlocfilehash: b4e61600f68521e4e7ab56ceae3349381e88a70a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082940"
---
# <a name="creating-runspaces"></a><span data-ttu-id="a23c0-102">Futási terek létrehozása</span><span class="sxs-lookup"><span data-stu-id="a23c0-102">Creating Runspaces</span></span>

<span data-ttu-id="a23c0-103">A futási térben egy fogadó alkalmazás által elindított a parancsok a működési környezetben.</span><span class="sxs-lookup"><span data-stu-id="a23c0-103">A runspace is the operating environment for the commands that are invoked by a host application.</span></span> <span data-ttu-id="a23c0-104">Ebben a környezetben a parancsokat és adatok, amelyek jelenleg találhatók és minden olyan nyelvi korlátozások jelenleg tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="a23c0-104">This environment includes the commands and data that are currently present, and any language restrictions that currently apply.</span></span>

 <span data-ttu-id="a23c0-105">Alkalmazások üzemeltetése használhatja a Windows PowerShell-lel, az összes elérhető a core-parancsokat is tartalmaz, ami által biztosított alapértelmezett futási térben vagy hozzon létre egy egyéni futási teret, amely a rendelkezésre álló parancsokat csak egy részhalmazát tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="a23c0-105">Host applications can use the default runspace that is provided by Windows PowerShell, which includes all available core commands, or create a custom runspace that includes only a subset of the available commands.</span></span> <span data-ttu-id="a23c0-106">Hozzon létre egy testre szabott futási teret, hozzon létre egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) objektumra, és rendelje hozzá a futási térben.</span><span class="sxs-lookup"><span data-stu-id="a23c0-106">To create a customized runspace, you create an [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) object and assign it to your runspace.</span></span>

## <a name="runspace-tasks"></a><span data-ttu-id="a23c0-107">Futási térben feladatok</span><span class="sxs-lookup"><span data-stu-id="a23c0-107">Runspace tasks</span></span>

1. [<span data-ttu-id="a23c0-108">Egy InitialSessionState létrehozása</span><span class="sxs-lookup"><span data-stu-id="a23c0-108">Creating an InitialSessionState</span></span>](./creating-an-initialsessionstate.md)

2. [<span data-ttu-id="a23c0-109">Egy korlátozott futási térrel létrehozása</span><span class="sxs-lookup"><span data-stu-id="a23c0-109">Creating a constrained runspace</span></span>](./creating-a-constrained-runspace.md)

3. [<span data-ttu-id="a23c0-110">Több futási terek létrehozása</span><span class="sxs-lookup"><span data-stu-id="a23c0-110">Creating multiple runspaces</span></span>](./creating-multiple-runspaces.md)

## <a name="see-also"></a><span data-ttu-id="a23c0-111">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a23c0-111">See Also</span></span>
