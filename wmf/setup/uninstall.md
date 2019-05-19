---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: Távolítsa el a WMF 5.0
ms.openlocfilehash: f562a4a4506bfdede6b23bd186b80f40cc9e45ca
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856188"
---
# <a name="uninstallation-instructions"></a><span data-ttu-id="a163f-103">Az Eltávolítás utasítások</span><span class="sxs-lookup"><span data-stu-id="a163f-103">Uninstallation Instructions</span></span>

## <a name="using-command-prompt"></a><span data-ttu-id="a163f-104">Parancssor használatával</span><span class="sxs-lookup"><span data-stu-id="a163f-104">Using Command Prompt</span></span>

1. <span data-ttu-id="a163f-105">Nyissa meg **parancssort.**</span><span class="sxs-lookup"><span data-stu-id="a163f-105">Open **Command Prompt.**</span></span>
2. <span data-ttu-id="a163f-106">Futtassa a [Windows Update önálló indítója](https://support.microsoft.com/en-us/kb/934307) alább látható módon:</span><span class="sxs-lookup"><span data-stu-id="a163f-106">Run the [Windows Update Standalone Launcher](https://support.microsoft.com/en-us/kb/934307) as shown below:</span></span>

<span data-ttu-id="a163f-107">A Windows Server 2012 R2 és Windows 8.1:</span><span class="sxs-lookup"><span data-stu-id="a163f-107">On Windows Server 2012 R2 and Windows 8.1:</span></span>

```powershell
wusa /uninstall /kb:3134758
```

<span data-ttu-id="a163f-108">A Windows Server 2012:</span><span class="sxs-lookup"><span data-stu-id="a163f-108">On Windows Server 2012:</span></span>

```powershell
wusa /uninstall /kb:3134759
```

<span data-ttu-id="a163f-109">A Windows Server 2008 R2 SP1 és Windows 7 SP1 esetén:</span><span class="sxs-lookup"><span data-stu-id="a163f-109">On Windows Server 2008 R2 SP1 and Windows 7 SP1:</span></span>

```powershell
wusa /uninstall /kb:3134760
```

## <a name="using-control-panel"></a><span data-ttu-id="a163f-110">Vezérlőpult használatával</span><span class="sxs-lookup"><span data-stu-id="a163f-110">Using Control Panel</span></span>

1. <span data-ttu-id="a163f-111">Nyissa meg **vezérlőpultot.**</span><span class="sxs-lookup"><span data-stu-id="a163f-111">Open **Control Panel.**</span></span>
2. <span data-ttu-id="a163f-112">Nyissa meg a **programok**, majd nyissa meg **program eltávolítása lehetőségre.**</span><span class="sxs-lookup"><span data-stu-id="a163f-112">Open **Programs**, then open **Uninstall a program.**</span></span>
3. <span data-ttu-id="a163f-113">Kattintson a **telepített frissítések megjelenítése.**</span><span class="sxs-lookup"><span data-stu-id="a163f-113">Click **View installed updates.**</span></span>
4. <span data-ttu-id="a163f-114">Válassza ki **Windows Management Framework 5.0** telepített frissítések listájából.</span><span class="sxs-lookup"><span data-stu-id="a163f-114">Select **Windows Management Framework 5.0** from the list of installed updates.</span></span> <span data-ttu-id="a163f-115">Ez megfelel *KB3134758*, *KB3134759*, vagy *KB3134760*.</span><span class="sxs-lookup"><span data-stu-id="a163f-115">This corresponds to *KB3134758*, *KB3134759*, or *KB3134760*.</span></span> <span data-ttu-id="a163f-116">Kattintson a **eltávolítása.**</span><span class="sxs-lookup"><span data-stu-id="a163f-116">Click **Uninstall.**</span></span>
