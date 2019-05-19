---
title: A Windows PowerShell-gazdagépet alkalmazás írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81aeafad-dbc3-4712-8bb9-e6a417be260f
caps.latest.revision: 15
ms.openlocfilehash: 1aaf936aa22af5c4a4b8c2fa4e6b3bbd2cff6d20
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65855084"
---
# <a name="writing-a-windows-powershell-host-application"></a><span data-ttu-id="b140f-102">Windows PowerShelles gazdaalkalmazás írása</span><span class="sxs-lookup"><span data-stu-id="b140f-102">Writing a Windows PowerShell Host Application</span></span>

<span data-ttu-id="b140f-103">Az alkalmazás a Windows PowerShell is üzemeltethet.</span><span class="sxs-lookup"><span data-stu-id="b140f-103">You can host Windows PowerShell in your application.</span></span> <span data-ttu-id="b140f-104">A gazdaalkalmazást adhatja meg a futási térrel, ahol parancsok futtatását, nyissa meg a helyi vagy távoli számítógép-munkamenetek és a szinkron vagy aszinkron módon alapján, az alkalmazás igényeinek parancsokat hívhatnak meg-e.</span><span class="sxs-lookup"><span data-stu-id="b140f-104">The host application can define the runspace where commands are run, open sessions on a local or remote computer, and invoke the commands either synchronously or asynchronously based on the needs of the application.</span></span>

<span data-ttu-id="b140f-105">A következő témakörök azt ismertetik, hogyan hozhat létre egy alkalmazást üzemeltető Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b140f-105">The following topics explain how to create an application that hosts Windows PowerShell.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="b140f-106">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="b140f-106">In This Section</span></span>

<span data-ttu-id="b140f-107">[Windows PowerShell-gazdagép gyors](./windows-powershell-host-quickstart.md) nyújt útmutatást és Kódminták az első lépések a gazdagép-alkalmazások létrehozása.</span><span class="sxs-lookup"><span data-stu-id="b140f-107">[Windows PowerShell Host Quickstart](./windows-powershell-host-quickstart.md) Provides instructions and code samples to get you started creating host applications.</span></span>

<span data-ttu-id="b140f-108">[Futási terek létrehozása](./creating-runspaces.md) -készlet létrehozása a Windows PowerShell-parancs futtatása egy fogadó alkalmazás futási terek ismertetik.</span><span class="sxs-lookup"><span data-stu-id="b140f-108">[Creating Runspaces](./creating-runspaces.md) A set of topics that explain how to create runspaces to run Windows PowerShell command in a host application.</span></span>

<span data-ttu-id="b140f-109">[Hozzáadásával és a parancsok meghívása](./adding-and-invoking-commands.md) azt ismerteti, hogyan hozhat létre és futtassa a parancsot a gazdaalkalmazásban...</span><span class="sxs-lookup"><span data-stu-id="b140f-109">[Adding and invoking commands](./adding-and-invoking-commands.md) Explains how to create and run a command pipeline in your host application..</span></span>

<span data-ttu-id="b140f-110">[Távoli futási terek létrehozása](./creating-remote-runspaces.md) azt ismerteti, hogyan lehet egy futási teret csatlakozni egy távoli számítógépen.</span><span class="sxs-lookup"><span data-stu-id="b140f-110">[Creating remote runspaces](./creating-remote-runspaces.md) Explains how to connect a runspace to a remote computer.</span></span>

<span data-ttu-id="b140f-111">[Egyéni felhasználói felület létrehozása](./creating-a-custom-user-interface.md) Introduces egyéni felhasználói felületek és példák mutató hivatkozásokat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="b140f-111">[Creating a custom user interface](./creating-a-custom-user-interface.md) Introduces custom user interfaces and provides links to examples.</span></span>

<span data-ttu-id="b140f-112">[Gazdagép Alkalmazásminták](./host-application-samples.md) Ez a szakasz tartalmazza a teljes gazdagép alkalmazások fejlesztésére.</span><span class="sxs-lookup"><span data-stu-id="b140f-112">[Host Application Samples](./host-application-samples.md) This section includes samples of complete host applications.</span></span>

## <a name="see-also"></a><span data-ttu-id="b140f-113">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b140f-113">See Also</span></span>

[<span data-ttu-id="b140f-114">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b140f-114">Windows PowerShell</span></span>](http://msdn.microsoft.com/en-us/b41a2af3-aec1-402d-8e18-c2c26be461ff)
