---
title: Frissíthető súgó tesztelése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3e064048-2b94-4365-bdb7-f1ee7c0a7fd7
caps.latest.revision: 6
ms.openlocfilehash: f2f319a3cab4b4bd91e9b634dda57d58a6476b62
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845926"
---
# <a name="how-to-test-updatable-help"></a><span data-ttu-id="af468-102">Frissíthető súgó tesztelése</span><span class="sxs-lookup"><span data-stu-id="af468-102">How to Test Updatable Help</span></span>

<span data-ttu-id="af468-103">Ez a témakör ismerteti a frissíthető súgó tesztelését egy modul megközelítést.</span><span class="sxs-lookup"><span data-stu-id="af468-103">This topic describes approaches to testing Updatable Help for a module.</span></span>

## <a name="using-verbose-to-detect-errors"></a><span data-ttu-id="af468-104">Hibák észlelése részletes használatával</span><span class="sxs-lookup"><span data-stu-id="af468-104">Using Verbose to Detect Errors</span></span>

<span data-ttu-id="af468-105">A HelpInfo XML-fájlt, és a CAB-fájlok a modul feltöltés után tesztelheti a fájlok futtatásával egy [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsot a **részletes** paraméter.</span><span class="sxs-lookup"><span data-stu-id="af468-105">After uploading the HelpInfo XML file and CAB files for your module, test the files by running an [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) command with the **Verbose** parameter.</span></span> <span data-ttu-id="af468-106">A **részletes** paraméter arra utasítja a `Update-Help` jelenteni a kritikus lépések a műveletek, az olvasó a **HelpInfoUri** kulcsfontosságú a moduljegyzékben, hogy a fájltípus esetében a kicsomagolt CAB-fájl és a nyelvspecifikus modulkönyvtárat helyezi el a fájlokat.</span><span class="sxs-lookup"><span data-stu-id="af468-106">The **Verbose** parameter directs `Update-Help` to report the critical steps in its actions, from reading the **HelpInfoUri** key in the module manifest to validating the file types in the unpacked CAB file and placing the files in the language-specific module directory.</span></span>
<span data-ttu-id="af468-107">A HelpInfo XML-fájlt, és a CAB-fájlok a modul feltöltés után tesztelheti a fájlok futtatásával egy [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsot a **részletes** paraméter.</span><span class="sxs-lookup"><span data-stu-id="af468-107">After uploading the HelpInfo XML file and CAB files for your module, test the files by running an [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) command with the **Verbose** parameter.</span></span> <span data-ttu-id="af468-108">A **részletes** paraméter arra utasítja a `Update-Help` jelenteni a kritikus lépések a műveletek, az olvasó a **HelpInfoUri** kulcsfontosságú a moduljegyzékben, hogy a fájltípus esetében a kicsomagolt CAB-fájl és a nyelvspecifikus modulkönyvtárat helyezi el a fájlokat.</span><span class="sxs-lookup"><span data-stu-id="af468-108">The **Verbose** parameter directs `Update-Help` to report the critical steps in its actions, from reading the **HelpInfoUri** key in the module manifest to validating the file types in the unpacked CAB file and placing the files in the language-specific module directory.</span></span>

<span data-ttu-id="af468-109">Ha az összes részletes üzenetek oldva, futtassa egy `Update-Help` parancsot a **Debug** paraméter.</span><span class="sxs-lookup"><span data-stu-id="af468-109">When all verbose messages are resolved, run an `Update-Help` command with the **Debug** parameter.</span></span> <span data-ttu-id="af468-110">Ezt a paramétert kell talált a frissíthető Súgó fájlok fennmaradó hibát.</span><span class="sxs-lookup"><span data-stu-id="af468-110">This parameter should detect any remaining problems with the Updatable Help files.</span></span>