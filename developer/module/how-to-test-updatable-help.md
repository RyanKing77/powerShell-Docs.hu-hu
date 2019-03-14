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
ms.openlocfilehash: cecc6c26ccaece06462ddd74b53534137fcf3037
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794263"
---
# <a name="how-to-test-updatable-help"></a><span data-ttu-id="67128-102">Frissíthető súgó tesztelése</span><span class="sxs-lookup"><span data-stu-id="67128-102">How to Test Updatable Help</span></span>

<span data-ttu-id="67128-103">Ez a témakör ismerteti a frissíthető súgó tesztelését egy modul megközelítést.</span><span class="sxs-lookup"><span data-stu-id="67128-103">This topic describes approaches to testing Updatable Help for a module.</span></span>

## <a name="using-verbose-to-detect-errors"></a><span data-ttu-id="67128-104">Hibák észlelése részletes használatával</span><span class="sxs-lookup"><span data-stu-id="67128-104">Using Verbose to Detect Errors</span></span>

<span data-ttu-id="67128-105">A HelpInfo XML-fájlt, és a CAB-fájlok a modul feltöltés után tesztelheti a fájlok futtatásával egy [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsot a **részletes** paraméter.</span><span class="sxs-lookup"><span data-stu-id="67128-105">After uploading the HelpInfo XML file and CAB files for your module, test the files by running an [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) command with the **Verbose** parameter.</span></span> <span data-ttu-id="67128-106">A **részletes** paraméter arra utasítja a `Update-Help` jelenteni a kritikus lépések a műveletek, az olvasó a **HelpInfoUri** kulcsfontosságú a moduljegyzékben, hogy a fájltípus esetében a kicsomagolt CAB-fájl és a nyelvspecifikus modulkönyvtárat helyezi el a fájlokat.</span><span class="sxs-lookup"><span data-stu-id="67128-106">The **Verbose** parameter directs `Update-Help` to report the critical steps in its actions, from reading the **HelpInfoUri** key in the module manifest to validating the file types in the unpacked CAB file and placing the files in the language-specific module directory.</span></span>

<span data-ttu-id="67128-107">Ha az összes részletes üzenetek oldva, futtassa egy `Update-Help` parancsot a **Debug** paraméter.</span><span class="sxs-lookup"><span data-stu-id="67128-107">When all verbose messages are resolved, run an `Update-Help` command with the **Debug** parameter.</span></span> <span data-ttu-id="67128-108">Ezt a paramétert kell talált a frissíthető Súgó fájlok fennmaradó hibát.</span><span class="sxs-lookup"><span data-stu-id="67128-108">This parameter should detect any remaining problems with the Updatable Help files.</span></span>