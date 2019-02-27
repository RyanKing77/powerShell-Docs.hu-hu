---
title: Hogyan frissíthető a súgófájlok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 495869a6-080e-4401-9ddc-16edd2f86857
caps.latest.revision: 6
ms.openlocfilehash: 2c1fbd70aab1f65f33ea206b7ab1e2bd3dfd8c7a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846479"
---
# <a name="how-to-update-help-files"></a><span data-ttu-id="5fcd3-102">Súgófájlok frissítése</span><span class="sxs-lookup"><span data-stu-id="5fcd3-102">How to Update Help Files</span></span>

<span data-ttu-id="5fcd3-103">Ez a témakör bemutatja, hogyan súgófájlokat a modul, amely támogatja a frissíthető súgójának frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-103">This topic explains how to update help files for a module that supports Updatable Help.</span></span>

## <a name="updating-help-files"></a><span data-ttu-id="5fcd3-104">Súgó fájlok frissítése</span><span class="sxs-lookup"><span data-stu-id="5fcd3-104">Updating Help Files</span></span>

<span data-ttu-id="5fcd3-105">Súgófájlokat, például a hibák javítása, egy fogalom megértéséhez tisztázhassuk, gyakran feltett kérdés megválaszolásával, új fájlok hozzáadásával vagy hozzáadása az új és hatékonyabb példák számos oka lehet.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-105">There are many reasons to update help files, such as correcting errors, clarifying a concept, answering a frequently-asked question, adding new files, or adding new and better examples.</span></span>

<span data-ttu-id="5fcd3-106">A súgófájl frissítése:</span><span class="sxs-lookup"><span data-stu-id="5fcd3-106">To update a help file:</span></span>

1. <span data-ttu-id="5fcd3-107">Módosíthatja a fájlokat.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-107">Change the files.</span></span>

2. <span data-ttu-id="5fcd3-108">A fájlok lefordítása más felhasználói felületi kulturális környezetek.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-108">Translate the files into other UI cultures.</span></span>

3. <span data-ttu-id="5fcd3-109">Az összes Súgó-fájlok gyűjtése (új, módosított és változatlan) modul az egyes felhasználói felület kultúrafüggő részletei.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-109">Collect all help files (new, changed, and unchanged) for the module in each UI culture.</span></span>

4. <span data-ttu-id="5fcd3-110">A fájlok ellen az XML-séma érvényesítése.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-110">Validate the files against the XML schema.</span></span>

5. <span data-ttu-id="5fcd3-111">Építse újra a CAB-fájlok az egyes felhasználói felület kultúrafüggő részletei.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-111">Rebuild the CAB files for each UI culture.</span></span>

6. <span data-ttu-id="5fcd3-112">A HelpInfo XML-fájlban a verziószámok, a CAB-fájl számára minden egyes felhasználói felület kultúrafüggő részletei növelni.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-112">In the HelpInfo XML file, increment the version numbers of the CAB file for each UI culture.</span></span>

7. <span data-ttu-id="5fcd3-113">Az új CAB-fájlok feltöltése a értéke által meghatározott helyre a **HelpContentUri** elem a HelpInfo XML-fájlban.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-113">Upload the new CAB files to the location that is specified by the value of the **HelpContentUri** element in the HelpInfo XML file.</span></span> <span data-ttu-id="5fcd3-114">Cserélje le a régebbi CAB-fájlok az új CAB-fájlok.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-114">Replace the older CAB files with the new CAB files.</span></span>

8. <span data-ttu-id="5fcd3-115">Töltse fel a frissített HelpInfo XML-fájlt a hely által meghatározott a **HelpInfoUri** kulcsfontosságú a moduljegyzékben.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-115">Upload the updated HelpInfo XML file to the location that is specified by the **HelpInfoUri** key in the module manifest.</span></span> <span data-ttu-id="5fcd3-116">Cserélje le a régebbi HelpInfo XML-fájlt az új fájlt.</span><span class="sxs-lookup"><span data-stu-id="5fcd3-116">Replace the older HelpInfo XML file with the new file.</span></span>