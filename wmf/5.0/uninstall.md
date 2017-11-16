---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 3392db954c22030bb64ae5093619d23952e1fcdb
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="uninstallation-instructions"></a><span data-ttu-id="876bd-102">Az eltávolítás utasításokat</span><span class="sxs-lookup"><span data-stu-id="876bd-102">Uninstallation Instructions</span></span>

## <a name="using-command-prompt"></a><span data-ttu-id="876bd-103">Parancssor használatával</span><span class="sxs-lookup"><span data-stu-id="876bd-103">Using Command Prompt</span></span>
1.  <span data-ttu-id="876bd-104">Nyissa meg **parancssort.**</span><span class="sxs-lookup"><span data-stu-id="876bd-104">Open **Command Prompt.**</span></span>
2.  <span data-ttu-id="876bd-105">Futtassa a [Windows Update önálló indító](https://support.microsoft.com/en-us/kb/934307) alább látható módon:</span><span class="sxs-lookup"><span data-stu-id="876bd-105">Run the [Windows Update Standalone Launcher](https://support.microsoft.com/en-us/kb/934307) as shown below:</span></span>

<span data-ttu-id="876bd-106">A Windows Server 2012 R2 és Windows 8.1:</span><span class="sxs-lookup"><span data-stu-id="876bd-106">On Windows Server 2012 R2 and Windows 8.1:</span></span>
```powershell
wusa /uninstall /kb:3134758
```
<span data-ttu-id="876bd-107">A Windows Server 2012:</span><span class="sxs-lookup"><span data-stu-id="876bd-107">On Windows Server 2012:</span></span>
```powershell
wusa /uninstall /kb:3134759
```
<span data-ttu-id="876bd-108">A Windows Server 2008 R2 SP1 és Windows 7 SP1:</span><span class="sxs-lookup"><span data-stu-id="876bd-108">On Windows Server 2008 R2 SP1 and Windows 7 SP1:</span></span>
```powershell
wusa /uninstall /kb:3134760
```

## <a name="using-control-panel"></a><span data-ttu-id="876bd-109">Vezérlőpult segítségével</span><span class="sxs-lookup"><span data-stu-id="876bd-109">Using Control Panel</span></span>
1.  <span data-ttu-id="876bd-110">Nyissa meg **vezérlőpultot.**</span><span class="sxs-lookup"><span data-stu-id="876bd-110">Open **Control Panel.**</span></span>
2.  <span data-ttu-id="876bd-111">Nyissa meg a **programok**, majd nyissa meg **program eltávolítása.**</span><span class="sxs-lookup"><span data-stu-id="876bd-111">Open **Programs**, then open **Uninstall a program.**</span></span>
3.  <span data-ttu-id="876bd-112">Kattintson a **telepített frissítések megjelenítése.**</span><span class="sxs-lookup"><span data-stu-id="876bd-112">Click **View installed updates.**</span></span>
4.  <span data-ttu-id="876bd-113">Válassza ki **Windows Management Framework 5.0** telepített frissítések a listából.</span><span class="sxs-lookup"><span data-stu-id="876bd-113">Select **Windows Management Framework 5.0** from the list of installed updates.</span></span> <span data-ttu-id="876bd-114">Ez megfelel *KB3134758*, *KB3134759*, vagy *KB3134760*.</span><span class="sxs-lookup"><span data-stu-id="876bd-114">This corresponds to *KB3134758*, *KB3134759*, or *KB3134760*.</span></span> <span data-ttu-id="876bd-115">Kattintson a **eltávolítása.**</span><span class="sxs-lookup"><span data-stu-id="876bd-115">Click **Uninstall.**</span></span>

