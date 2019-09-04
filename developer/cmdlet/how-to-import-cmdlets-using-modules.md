---
title: Parancsmagok importálása modulok használatával | Microsoft Docs
ms.custom: ''
ms.date: 08/28/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a41d9e5f-de6f-47b7-9601-c108609320d0
caps.latest.revision: 8
ms.openlocfilehash: 2f145795a57c988da0cb4ed294142aa141c53cae
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215273"
---
# <a name="how-to-import-cmdlets-using-modules"></a><span data-ttu-id="b6478-102">Parancsmagok importálása modulokkal</span><span class="sxs-lookup"><span data-stu-id="b6478-102">How to Import Cmdlets Using Modules</span></span>

<span data-ttu-id="b6478-103">Ez a cikk azt ismerteti, hogyan lehet parancsmagokat importálni egy PowerShell-munkamenetbe egy bináris modul használatával.</span><span class="sxs-lookup"><span data-stu-id="b6478-103">This article describes how to import cmdlets to a PowerShell session by using a binary module.</span></span>

> [!NOTE]
> <span data-ttu-id="b6478-104">A modulok tagjai lehetnek parancsmagok, szolgáltatók, függvények, változók, aliasok és sok más.</span><span class="sxs-lookup"><span data-stu-id="b6478-104">The members of modules can include cmdlets, providers, functions, variables, aliases, and much more.</span></span> <span data-ttu-id="b6478-105">A beépülő modulok csak parancsmagokat és szolgáltatókat tartalmazhatnak.</span><span class="sxs-lookup"><span data-stu-id="b6478-105">Snap-ins can contain only cmdlets and providers.</span></span>

## <a name="how-to-load-cmdlets-using-a-module"></a><span data-ttu-id="b6478-106">Parancsmagok betöltése modul használatával</span><span class="sxs-lookup"><span data-stu-id="b6478-106">How to load cmdlets using a module</span></span>

1. <span data-ttu-id="b6478-107">Hozzon létre egy modul-mappát, amelynek a neve megegyezik azzal a szerelvény-fájllal, amelyben a parancsmagok implementálva vannak.</span><span class="sxs-lookup"><span data-stu-id="b6478-107">Create a module folder that has the same name as the assembly file in which the cmdlets are implemented.</span></span> <span data-ttu-id="b6478-108">Ebben az eljárásban a modul mappáját a Windows mappában hozza `system32` létre a rendszer.</span><span class="sxs-lookup"><span data-stu-id="b6478-108">In this procedure, the module folder is created in the Windows `system32` folder.</span></span>

   `%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules\mymodule`

1. <span data-ttu-id="b6478-109">Győződjön meg arról, `PSModulePath` hogy a környezeti változó tartalmazza az új modul mappájának elérési útját.</span><span class="sxs-lookup"><span data-stu-id="b6478-109">Make sure that the `PSModulePath` environment variable includes the path to your new module folder.</span></span> <span data-ttu-id="b6478-110">Alapértelmezés szerint a rendszer mappa már hozzá van adva a `PSModulePath` környezeti változóhoz.</span><span class="sxs-lookup"><span data-stu-id="b6478-110">By default, the system folder is already added to the `PSModulePath` environment variable.</span></span> <span data-ttu-id="b6478-111">A (z `PSModulePath`) megtekintéséhez írja `$env:PSModulePath`be a következőt:.</span><span class="sxs-lookup"><span data-stu-id="b6478-111">To view the `PSModulePath`, type: `$env:PSModulePath`.</span></span>

1. <span data-ttu-id="b6478-112">Másolja a parancsmag szerelvényt a modul mappájába.</span><span class="sxs-lookup"><span data-stu-id="b6478-112">Copy the cmdlet assembly into the module folder.</span></span>

1. <span data-ttu-id="b6478-113">Adjon hozzá egy modul manifest-`.psd1`fájlt () a modul gyökérkönyvtárában.</span><span class="sxs-lookup"><span data-stu-id="b6478-113">Add a module manifest file (`.psd1`) in the module's root folder.</span></span> <span data-ttu-id="b6478-114">A PowerShell a modul jegyzékfájlját használja a modul importálásához.</span><span class="sxs-lookup"><span data-stu-id="b6478-114">PowerShell uses the module manifest to import your module.</span></span> <span data-ttu-id="b6478-115">További információ: [a PowerShell-modul írása](../module/how-to-write-a-powershell-module-manifest.md).</span><span class="sxs-lookup"><span data-stu-id="b6478-115">For more information, see [How to Write a PowerShell Module Manifest](../module/how-to-write-a-powershell-module-manifest.md).</span></span>

1. <span data-ttu-id="b6478-116">Futtassa a következő parancsot a parancsmagok a munkamenethez való hozzáadásához:</span><span class="sxs-lookup"><span data-stu-id="b6478-116">Run the following command to add the cmdlets to the session:</span></span>

   `Import-Module [Module_Name]`

   <span data-ttu-id="b6478-117">Ez az eljárás használható a parancsmagok tesztelésére.</span><span class="sxs-lookup"><span data-stu-id="b6478-117">This procedure can be used to test your cmdlets.</span></span> <span data-ttu-id="b6478-118">Hozzáadja a szerelvényben található összes parancsmagot a munkamenethez.</span><span class="sxs-lookup"><span data-stu-id="b6478-118">It adds all the cmdlets in the assembly to the session.</span></span> <span data-ttu-id="b6478-119">A modulokkal kapcsolatos további információkért lásd: [Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="b6478-119">For more information about modules, see [Writing a Windows PowerShell Module](../module/writing-a-windows-powershell-module.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b6478-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b6478-120">See also</span></span>

[<span data-ttu-id="b6478-121">PowerShell-modul jegyzékének írása</span><span class="sxs-lookup"><span data-stu-id="b6478-121">How to Write a PowerShell Module Manifest</span></span>](../module/how-to-write-a-powershell-module-manifest.md)

[<span data-ttu-id="b6478-122">PowerShell-modul importálása</span><span class="sxs-lookup"><span data-stu-id="b6478-122">Importing a PowerShell Module</span></span>](../module/importing-a-powershell-module.md)

[<span data-ttu-id="b6478-123">Importálás – modul</span><span class="sxs-lookup"><span data-stu-id="b6478-123">Import-Module</span></span>](/powershell/module/Microsoft.PowerShell.Core/Import-Module)

[<span data-ttu-id="b6478-124">Modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="b6478-124">Installing Modules</span></span>](../module/installing-a-powershell-module.md)

[<span data-ttu-id="b6478-125">A PSModulePath telepítési útvonalának módosítása</span><span class="sxs-lookup"><span data-stu-id="b6478-125">Modifying the PSModulePath Installation Path</span></span>](../module/modifying-the-psmodulepath-installation-path.md)

[<span data-ttu-id="b6478-126">Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="b6478-126">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
