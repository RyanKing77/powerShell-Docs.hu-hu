---
title: Súgó fájlok elnevezési |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bf54eac7-88c6-4108-a5f6-2f0906d1662b
caps.latest.revision: 5
ms.openlocfilehash: 06281a1260dbdc120867fce89e6d5c8dd0754b87
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847277"
---
# <a name="naming-help-files"></a><span data-ttu-id="98a06-102">Elnevezési súgófájlok</span><span class="sxs-lookup"><span data-stu-id="98a06-102">Naming Help Files</span></span>

<span data-ttu-id="98a06-103">Ez a témakör azt ismerteti, hogyan egy XML-alapú súgófájl neve úgy, hogy a [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) parancsmag is megtalálhatják azt.</span><span class="sxs-lookup"><span data-stu-id="98a06-103">This topic explains how to name an XML-based help file so that the [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) cmdlet can find it.</span></span> <span data-ttu-id="98a06-104">A vonatkozó követelményeknek eltérőek az egyes parancsot.</span><span class="sxs-lookup"><span data-stu-id="98a06-104">The name requirements differ for each command type.</span></span>
<span data-ttu-id="98a06-105">Ez a témakör azt ismerteti, hogyan egy XML-alapú súgófájl neve úgy, hogy a [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) parancsmag is megtalálhatják azt.</span><span class="sxs-lookup"><span data-stu-id="98a06-105">This topic explains how to name an XML-based help file so that the [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) cmdlet can find it.</span></span> <span data-ttu-id="98a06-106">A vonatkozó követelményeknek eltérőek az egyes parancsot.</span><span class="sxs-lookup"><span data-stu-id="98a06-106">The name requirements differ for each command type.</span></span>

## <a name="cmdlet-help-files"></a><span data-ttu-id="98a06-107">A parancsmag Súgó-fájlok</span><span class="sxs-lookup"><span data-stu-id="98a06-107">Cmdlet Help Files</span></span>

<span data-ttu-id="98a06-108">A súgófájlban talál egy C# parancsmag névvel kell rendelkeznie a szerelvény, amelyben a parancsmag definiálva van.</span><span class="sxs-lookup"><span data-stu-id="98a06-108">The help file for a C# cmdlet must be named for the assembly in which the cmdlet is defined.</span></span> <span data-ttu-id="98a06-109">Használja a következő fájl nevének formátuma:</span><span class="sxs-lookup"><span data-stu-id="98a06-109">Use the following file name format:</span></span>

```
<AssemblyName>.dll-help.xml
```

<span data-ttu-id="98a06-110">A szerelvény neve formátumra szükség, akkor is, ha a szerelvény egy beágyazott modul.</span><span class="sxs-lookup"><span data-stu-id="98a06-110">The assembly name format is required even when the assembly is a nested module.</span></span>

<span data-ttu-id="98a06-111">Ha például a [Get-WinEvent; PSITPro5_Diagnostic; ](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent) parancsmag Microsoft.PowerShell.Diagnostics.dll szerelvény van definiálva.</span><span class="sxs-lookup"><span data-stu-id="98a06-111">For example, the [Get-WinEvent;PSITPro5_Diagnostic;](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent) cmdlet is defined in the Microsoft.PowerShell.Diagnostics.dll assembly.</span></span> <span data-ttu-id="98a06-112">A `Get-Help` parancsmag keres egy Súgó-témakör a `Get-WinEvent` parancsmag csak az modulkönyvtárat Microsoft.PowerShell.Diagnostics.dll-help.xml fájlban.</span><span class="sxs-lookup"><span data-stu-id="98a06-112">The `Get-Help` cmdlet looks for a help topic for the `Get-WinEvent` cmdlet only in the Microsoft.PowerShell.Diagnostics.dll-help.xml file in the module directory.</span></span>
<span data-ttu-id="98a06-113">Ha például a [Get-WinEvent; PSITPro5_Diagnostic; ](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent) parancsmag Microsoft.PowerShell.Diagnostics.dll szerelvény van definiálva.</span><span class="sxs-lookup"><span data-stu-id="98a06-113">For example, the [Get-WinEvent;PSITPro5_Diagnostic;](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent) cmdlet is defined in the Microsoft.PowerShell.Diagnostics.dll assembly.</span></span> <span data-ttu-id="98a06-114">A `Get-Help` parancsmag keres egy Súgó-témakör a `Get-WinEvent` parancsmag csak az modulkönyvtárat Microsoft.PowerShell.Diagnostics.dll-help.xml fájlban.</span><span class="sxs-lookup"><span data-stu-id="98a06-114">The `Get-Help` cmdlet looks for a help topic for the `Get-WinEvent` cmdlet only in the Microsoft.PowerShell.Diagnostics.dll-help.xml file in the module directory.</span></span>

## <a name="provider-help-files"></a><span data-ttu-id="98a06-115">Szolgáltató súgófájlok</span><span class="sxs-lookup"><span data-stu-id="98a06-115">Provider Help files</span></span>

<span data-ttu-id="98a06-116">A szerelvény, amelyben a szolgáltató van definiálva a súgófájlban talál egy Windows PowerShell-szolgáltatóban névvel kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="98a06-116">The help file for a Windows PowerShell provider must be named for the assembly in which the provider is defined.</span></span> <span data-ttu-id="98a06-117">Használja a következő fájl nevének formátuma:</span><span class="sxs-lookup"><span data-stu-id="98a06-117">Use the following file name format:</span></span>

```
<AssemblyName>.dll-help.xml
```

<span data-ttu-id="98a06-118">A szerelvény neve formátumra szükség, akkor is, ha a szerelvény egy beágyazott modul.</span><span class="sxs-lookup"><span data-stu-id="98a06-118">The assembly name format is required even when the assembly is a nested module.</span></span>

<span data-ttu-id="98a06-119">Ha például a tanúsítványszolgáltató Microsoft.PowerShell.Security.dll szerelvény van meghatározva.</span><span class="sxs-lookup"><span data-stu-id="98a06-119">For example, the Certificate provider is defined in the Microsoft.PowerShell.Security.dll assembly.</span></span> <span data-ttu-id="98a06-120">A `Get-Help` parancsmag a tanúsítvány-szolgáltató csak az modulkönyvtárat Microsoft.PowerShell.Security.dll-help.xml fájlban keres egy Súgó-témakört.</span><span class="sxs-lookup"><span data-stu-id="98a06-120">The `Get-Help` cmdlet looks for a help topic for the Certificate provider only in the Microsoft.PowerShell.Security.dll-help.xml file in the module directory.</span></span>

## <a name="function-help-files"></a><span data-ttu-id="98a06-121">Függvény súgófájlok</span><span class="sxs-lookup"><span data-stu-id="98a06-121">Function Help Files</span></span>

<span data-ttu-id="98a06-122">Függvények használatával dokumentálni kell [Megjegyzés-alapú súgó](/powershell/module/microsoft.powershell.core/about/about_comment_based_help) vagy dokumentált súgó XML-fájlban.</span><span class="sxs-lookup"><span data-stu-id="98a06-122">Functions can be documented by using [comment-based help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help) or documented in an XML help file.</span></span> <span data-ttu-id="98a06-123">Ha a funkció leírása itt található egy XML-fájlt, a következő függvénynek rendelkeznie kell egy `.ExternalHelp` kulcsszó, amely összekapcsolja az XML-fájlt a funkciót megjegyzéseket.</span><span class="sxs-lookup"><span data-stu-id="98a06-123">When the function is documented in an XML file, the function must have an `.ExternalHelp` comment keyword that associates the function with the XML file.</span></span> <span data-ttu-id="98a06-124">Ellenkező esetben a `Get-Help` parancsmag nem találja a súgófájlt.</span><span class="sxs-lookup"><span data-stu-id="98a06-124">Otherwise, the `Get-Help` cmdlet cannot find the help file.</span></span>
<span data-ttu-id="98a06-125">Függvények használatával dokumentálni kell [Megjegyzés-alapú súgó](/powershell/module/microsoft.powershell.core/about/about_comment_based_help) vagy dokumentált súgó XML-fájlban.</span><span class="sxs-lookup"><span data-stu-id="98a06-125">Functions can be documented by using [comment-based help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help) or documented in an XML help file.</span></span> <span data-ttu-id="98a06-126">Ha a funkció leírása itt található egy XML-fájlt, a következő függvénynek rendelkeznie kell egy `.ExternalHelp` kulcsszó, amely összekapcsolja az XML-fájlt a funkciót megjegyzéseket.</span><span class="sxs-lookup"><span data-stu-id="98a06-126">When the function is documented in an XML file, the function must have an `.ExternalHelp` comment keyword that associates the function with the XML file.</span></span> <span data-ttu-id="98a06-127">Ellenkező esetben a `Get-Help` parancsmag nem találja a súgófájlt.</span><span class="sxs-lookup"><span data-stu-id="98a06-127">Otherwise, the `Get-Help` cmdlet cannot find the help file.</span></span>

<span data-ttu-id="98a06-128">Nem vonatkoznak technikai követelmények nevéhez egy függvény súgófájl.</span><span class="sxs-lookup"><span data-stu-id="98a06-128">There are no technical requirements for the name of a function help file.</span></span> <span data-ttu-id="98a06-129">Azonban ajánlott eljárás, hogy nevezze el a súgófájlban a parancsfájl-modul, amely a függvény definiálva van.</span><span class="sxs-lookup"><span data-stu-id="98a06-129">However, a best practice is to name the help file for the script module in which the function is defined.</span></span> <span data-ttu-id="98a06-130">Például a következő függvényt a MyModule.psm1 fájlban van definiálva.</span><span class="sxs-lookup"><span data-stu-id="98a06-130">For example, the following function is defined in the MyModule.psm1 file.</span></span>

```csharp
#.ExternalHelp MyModule.psm1-help.xml
function Test-Function { ... }
```

## <a name="cim-command-help-files"></a><span data-ttu-id="98a06-131">A CIM-parancs súgófájlok</span><span class="sxs-lookup"><span data-stu-id="98a06-131">CIM Command Help Files</span></span>

<span data-ttu-id="98a06-132">A súgófájl a CIM-parancshoz névvel kell rendelkeznie a CDXML-fájlt, amelyben a CIM-parancs van definiálva.</span><span class="sxs-lookup"><span data-stu-id="98a06-132">The help file for a CIM command must be named for the CDXML file in which the CIM command is defined.</span></span> <span data-ttu-id="98a06-133">Használja a következő fájl nevének formátuma:</span><span class="sxs-lookup"><span data-stu-id="98a06-133">Use the following file name format:</span></span>

```
<FileName>.cdxml-help.xml
```

<span data-ttu-id="98a06-134">A CIM-parancsok beágyazott modulként modulokban szereplő CDXML fájlban vannak definiálva.</span><span class="sxs-lookup"><span data-stu-id="98a06-134">CIM commands are defined in CDXML files that can be included in modules as nested modules.</span></span> <span data-ttu-id="98a06-135">A CIM-parancs a munkamenet függvényében való importálásakor, a Windows PowerShell ad hozzá egy `.ExternalHelp` Megjegyzés kulcsszó használatával a függvény definícióját, amely összekapcsolja a függvény egy XML-súgó-fájlba, amelyben a CIM-parancs van definiálva CDXML-fájl neve.</span><span class="sxs-lookup"><span data-stu-id="98a06-135">When the CIM command is imported into the session as a function, Windows PowerShell adds an `.ExternalHelp` comment keyword to the function definition that associates the function with an XML help file that is named for the CDXML file in which the CIM command is defined.</span></span>

## <a name="script-workflow-help-files"></a><span data-ttu-id="98a06-136">Parancsfájl-munkafolyamat súgófájlok</span><span class="sxs-lookup"><span data-stu-id="98a06-136">Script Workflow Help Files</span></span>

<span data-ttu-id="98a06-137">XML-alapú súgófájlokat, amelyek szerepelnek a modulok a parancsfájl-munkafolyamatok is dokumentálni.</span><span class="sxs-lookup"><span data-stu-id="98a06-137">Script workflows that are included in modules can be documented in XML-based help files.</span></span> <span data-ttu-id="98a06-138">Nem vonatkoznak technikai követelmények a neve, a súgófájlt.</span><span class="sxs-lookup"><span data-stu-id="98a06-138">There are no technical requirements for the name of the help file.</span></span> <span data-ttu-id="98a06-139">Azonban ajánlott eljárás, hogy nevezze el a súgófájlban a parancsfájl modul, amely a parancsfájl-munkafolyamathoz definiálva van.</span><span class="sxs-lookup"><span data-stu-id="98a06-139">However, a best practice is to name the help file for the script module in which the script workflow is defined.</span></span> <span data-ttu-id="98a06-140">Például:</span><span class="sxs-lookup"><span data-stu-id="98a06-140">For example:</span></span>

```
<ScriptModule>.psm1-help.xml
```

<span data-ttu-id="98a06-141">Ellentétben más parancsfájlalapú parancsok parancsfájl-munkafolyamatokban nem szükséges egy `.ExternalHelp` kulcsszó használatával társíthatja azokat a súgófájlban megjegyzéseket.</span><span class="sxs-lookup"><span data-stu-id="98a06-141">Unlike other scripted commands, script workflows do not require an `.ExternalHelp` comment keyword to associate them with a help file.</span></span> <span data-ttu-id="98a06-142">Ehelyett Windows PowerShell a felhasználói felület kulturális környezet-specifikus alkönyvtárát modul XML-alapú súgó fájlokat keres, és megkeresi az összes fájlt a parancsfájl-munkafolyamathoz tartozó súgó.</span><span class="sxs-lookup"><span data-stu-id="98a06-142">Instead, Windows PowerShell searches the UI-Culture-specific subdirectories of the module directory for XML-based help files and looks for help for the script workflow in all the files.</span></span> <span data-ttu-id="98a06-143">`.ExternalHelp` Megjegyzés kulcsszót a rendszer figyelmen kívül hagyja.</span><span class="sxs-lookup"><span data-stu-id="98a06-143">`.ExternalHelp` comment keyword are ignored.</span></span>

<span data-ttu-id="98a06-144">Mivel a `.ExternalHelp` Megjegyzés kulcsszót a rendszer figyelmen kívül hagyja, a `Get-Help` parancsmag talál segítséget a parancsfájl-munkafolyamatokban csak akkor, ha a modulok szerepelnek.</span><span class="sxs-lookup"><span data-stu-id="98a06-144">Because the `.ExternalHelp` comment keyword is ignored, the `Get-Help` cmdlet can find help for script workflows only when they are included in modules.</span></span>