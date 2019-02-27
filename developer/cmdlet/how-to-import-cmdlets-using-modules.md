---
title: Parancsmagok modulok importálása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a41d9e5f-de6f-47b7-9601-c108609320d0
caps.latest.revision: 8
ms.openlocfilehash: c007bb11324e10ffd100797dccd9e6ab0d09a73e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849013"
---
# <a name="how-to-import-cmdlets-using-modules"></a><span data-ttu-id="703b9-102">Parancsmagok importálása modulokkal</span><span class="sxs-lookup"><span data-stu-id="703b9-102">How to Import Cmdlets Using Modules</span></span>

<span data-ttu-id="703b9-103">Ez a témakör ismerteti a parancsmagok importálása a Windows PowerShell-munkamenethez bináris modul használatával.</span><span class="sxs-lookup"><span data-stu-id="703b9-103">This topic describes how to import cmdlets to a Windows PowerShell session by using a binary module.</span></span>

> [!NOTE]
> <span data-ttu-id="703b9-104">Modulok tagjai lehetnek parancsmagok, szolgáltatók, függvények, változókat, aliasok és még sok más.</span><span class="sxs-lookup"><span data-stu-id="703b9-104">The members of modules can include cmdlets, providers, functions, variables, aliases, and much more.</span></span> <span data-ttu-id="703b9-105">Beépülő modulok csak parancsmagok és szolgáltatók tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="703b9-105">Snap-ins can contain only cmdlets and providers.</span></span>

## <a name="how-to-load-cmdlets-using-a-module"></a><span data-ttu-id="703b9-106">Betöltés parancsmagok egy modul használatával</span><span class="sxs-lookup"><span data-stu-id="703b9-106">How to load cmdlets using a module</span></span>

1. <span data-ttu-id="703b9-107">Hozzon létre egy modul, amely ugyanazzal a névvel rendelkezik a szerelvényfájl, amelyben a parancsmagok vannak megvalósítva.</span><span class="sxs-lookup"><span data-stu-id="703b9-107">Create a module folder that has the same name as the assembly file in which the cmdlets are implemented.</span></span> <span data-ttu-id="703b9-108">Ebben az eljárásban a modul mappában jön létre a a `system32` mappát.</span><span class="sxs-lookup"><span data-stu-id="703b9-108">In this procedure, the module folder is created in the `system32` folder.</span></span>

   `%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules\mymodule`

2. <span data-ttu-id="703b9-109">Győződjön meg arról, hogy a `PSModulePath` környezeti változó tartalmazza az új modul mappa elérési útját.</span><span class="sxs-lookup"><span data-stu-id="703b9-109">Make sure that the `PSModulePath` environment variable includes the path to your new module folder.</span></span> <span data-ttu-id="703b9-110">Alapértelmezés szerint a mappa már része a `PSModulePath` környezeti változót.</span><span class="sxs-lookup"><span data-stu-id="703b9-110">By default, the system folder is already added to the `PSModulePath` environment variable.</span></span>

3. <span data-ttu-id="703b9-111">A modul a parancsmag szerelvény másolja.</span><span class="sxs-lookup"><span data-stu-id="703b9-111">Copy the cmdlet assembly into the module folder.</span></span>

4. <span data-ttu-id="703b9-112">Futtassa a következő parancsot, adja hozzá a munkamenet a parancsmagokat:</span><span class="sxs-lookup"><span data-stu-id="703b9-112">Run the following command to add the cmdlets to the session:</span></span>

   `import-module [Module_Name]`

   <span data-ttu-id="703b9-113">Ez az eljárás használható a parancsmagok teszteléséhez.</span><span class="sxs-lookup"><span data-stu-id="703b9-113">This procedure can be used to test your cmdlets.</span></span> <span data-ttu-id="703b9-114">Minden parancsmag hozzáadja a szerelvényben a munkamenethez.</span><span class="sxs-lookup"><span data-stu-id="703b9-114">It adds all the cmdlets in the assembly to the session.</span></span> <span data-ttu-id="703b9-115">Modulok, a különböző módokon betölteni a modulok és a egy modul exportálja, elemeinek korlátozása a különböző típusú modulokkal kapcsolatos további információkért lásd [Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="703b9-115">For more information about modules, the different types of modules, the different ways to load modules, and how to restrict the elements of a module that are exported, see [Writing a Windows PowerShell Module](../module/writing-a-windows-powershell-module.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="703b9-116">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="703b9-116">See Also</span></span>

[<span data-ttu-id="703b9-117">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="703b9-117">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="703b9-118">Modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="703b9-118">Installing Modules</span></span>](../module/installing-a-powershell-module.md)