---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 385bb7223b19c8ace8088ba469e543721a527b99
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688524"
---
# <a name="uninstallation-instructions"></a><span data-ttu-id="bf4f9-102">Az Eltávolítás utasítások</span><span class="sxs-lookup"><span data-stu-id="bf4f9-102">Uninstallation Instructions</span></span>

## <a name="using-command-prompt"></a><span data-ttu-id="bf4f9-103">Parancssor használatával</span><span class="sxs-lookup"><span data-stu-id="bf4f9-103">Using Command Prompt</span></span>
1.  <span data-ttu-id="bf4f9-104">Nyissa meg **parancssort.**</span><span class="sxs-lookup"><span data-stu-id="bf4f9-104">Open **Command Prompt.**</span></span>
2.  <span data-ttu-id="bf4f9-105">Futtassa a [Windows Update önálló indítója](https://support.microsoft.com/en-us/kb/934307) alább látható módon:</span><span class="sxs-lookup"><span data-stu-id="bf4f9-105">Run the [Windows Update Standalone Launcher](https://support.microsoft.com/en-us/kb/934307) as shown below:</span></span>

<span data-ttu-id="bf4f9-106">A Windows Server 2012 R2 és Windows 8.1:</span><span class="sxs-lookup"><span data-stu-id="bf4f9-106">On Windows Server 2012 R2 and Windows 8.1:</span></span>
```powershell
wusa /uninstall /kb:3134758
```
<span data-ttu-id="bf4f9-107">A Windows Server 2012:</span><span class="sxs-lookup"><span data-stu-id="bf4f9-107">On Windows Server 2012:</span></span>
```powershell
wusa /uninstall /kb:3134759
```
<span data-ttu-id="bf4f9-108">A Windows Server 2008 R2 SP1 és Windows 7 SP1 esetén:</span><span class="sxs-lookup"><span data-stu-id="bf4f9-108">On Windows Server 2008 R2 SP1 and Windows 7 SP1:</span></span>
```powershell
wusa /uninstall /kb:3134760
```

## <a name="using-control-panel"></a><span data-ttu-id="bf4f9-109">Vezérlőpult használatával</span><span class="sxs-lookup"><span data-stu-id="bf4f9-109">Using Control Panel</span></span>
1.  <span data-ttu-id="bf4f9-110">Nyissa meg **vezérlőpultot.**</span><span class="sxs-lookup"><span data-stu-id="bf4f9-110">Open **Control Panel.**</span></span>
2.  <span data-ttu-id="bf4f9-111">Nyissa meg a **programok**, majd nyissa meg **program eltávolítása lehetőségre.**</span><span class="sxs-lookup"><span data-stu-id="bf4f9-111">Open **Programs**, then open **Uninstall a program.**</span></span>
3.  <span data-ttu-id="bf4f9-112">Kattintson a **telepített frissítések megjelenítése.**</span><span class="sxs-lookup"><span data-stu-id="bf4f9-112">Click **View installed updates.**</span></span>
4.  <span data-ttu-id="bf4f9-113">Válassza ki **Windows Management Framework 5.0** telepített frissítések listájából.</span><span class="sxs-lookup"><span data-stu-id="bf4f9-113">Select **Windows Management Framework 5.0** from the list of installed updates.</span></span> <span data-ttu-id="bf4f9-114">Ez megfelel *KB3134758*, *KB3134759*, vagy *KB3134760*.</span><span class="sxs-lookup"><span data-stu-id="bf4f9-114">This corresponds to *KB3134758*, *KB3134759*, or *KB3134760*.</span></span> <span data-ttu-id="bf4f9-115">Kattintson a **eltávolítása.**</span><span class="sxs-lookup"><span data-stu-id="bf4f9-115">Click **Uninstall.**</span></span>
