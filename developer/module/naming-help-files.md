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
ms.openlocfilehash: f65a90023df88fceafae1d1875ddf46b9088e2b8
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082178"
---
# <a name="naming-help-files"></a><span data-ttu-id="24971-102">Elnevezési súgófájlok</span><span class="sxs-lookup"><span data-stu-id="24971-102">Naming Help Files</span></span>

<span data-ttu-id="24971-103">Ez a témakör azt ismerteti, hogyan egy XML-alapú súgófájl neve úgy, hogy a [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) parancsmag is megtalálhatják azt.</span><span class="sxs-lookup"><span data-stu-id="24971-103">This topic explains how to name an XML-based help file so that the [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) cmdlet can find it.</span></span> <span data-ttu-id="24971-104">A vonatkozó követelményeknek eltérőek az egyes parancsot.</span><span class="sxs-lookup"><span data-stu-id="24971-104">The name requirements differ for each command type.</span></span>

## <a name="cmdlet-help-files"></a><span data-ttu-id="24971-105">A parancsmag Súgó-fájlok</span><span class="sxs-lookup"><span data-stu-id="24971-105">Cmdlet Help Files</span></span>

<span data-ttu-id="24971-106">A súgófájlban talál egy C# parancsmag névvel kell rendelkeznie a szerelvény, amelyben a parancsmag definiálva van.</span><span class="sxs-lookup"><span data-stu-id="24971-106">The help file for a C# cmdlet must be named for the assembly in which the cmdlet is defined.</span></span> <span data-ttu-id="24971-107">Használja a következő fájl nevének formátuma:</span><span class="sxs-lookup"><span data-stu-id="24971-107">Use the following file name format:</span></span>

```
<AssemblyName>.dll-help.xml
```

<span data-ttu-id="24971-108">A szerelvény neve formátumra szükség, akkor is, ha a szerelvény egy beágyazott modul.</span><span class="sxs-lookup"><span data-stu-id="24971-108">The assembly name format is required even when the assembly is a nested module.</span></span>

<span data-ttu-id="24971-109">Ha például a [Get-WinEvent; PSITPro5_Diagnostic; ](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent) parancsmag Microsoft.PowerShell.Diagnostics.dll szerelvény van definiálva.</span><span class="sxs-lookup"><span data-stu-id="24971-109">For example, the [Get-WinEvent;PSITPro5_Diagnostic;](/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent) cmdlet is defined in the Microsoft.PowerShell.Diagnostics.dll assembly.</span></span> <span data-ttu-id="24971-110">A `Get-Help` parancsmag keres egy Súgó-témakör a `Get-WinEvent` parancsmag csak az modulkönyvtárat Microsoft.PowerShell.Diagnostics.dll-help.xml fájlban.</span><span class="sxs-lookup"><span data-stu-id="24971-110">The `Get-Help` cmdlet looks for a help topic for the `Get-WinEvent` cmdlet only in the Microsoft.PowerShell.Diagnostics.dll-help.xml file in the module directory.</span></span>

## <a name="provider-help-files"></a><span data-ttu-id="24971-111">Szolgáltató súgófájlok</span><span class="sxs-lookup"><span data-stu-id="24971-111">Provider Help files</span></span>

<span data-ttu-id="24971-112">A szerelvény, amelyben a szolgáltató van definiálva a súgófájlban talál egy Windows PowerShell-szolgáltatóban névvel kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="24971-112">The help file for a Windows PowerShell provider must be named for the assembly in which the provider is defined.</span></span> <span data-ttu-id="24971-113">Használja a következő fájl nevének formátuma:</span><span class="sxs-lookup"><span data-stu-id="24971-113">Use the following file name format:</span></span>

```
<AssemblyName>.dll-help.xml
```

<span data-ttu-id="24971-114">A szerelvény neve formátumra szükség, akkor is, ha a szerelvény egy beágyazott modul.</span><span class="sxs-lookup"><span data-stu-id="24971-114">The assembly name format is required even when the assembly is a nested module.</span></span>

<span data-ttu-id="24971-115">Ha például a tanúsítványszolgáltató Microsoft.PowerShell.Security.dll szerelvény van meghatározva.</span><span class="sxs-lookup"><span data-stu-id="24971-115">For example, the Certificate provider is defined in the Microsoft.PowerShell.Security.dll assembly.</span></span> <span data-ttu-id="24971-116">A `Get-Help` parancsmag a tanúsítvány-szolgáltató csak az modulkönyvtárat Microsoft.PowerShell.Security.dll-help.xml fájlban keres egy Súgó-témakört.</span><span class="sxs-lookup"><span data-stu-id="24971-116">The `Get-Help` cmdlet looks for a help topic for the Certificate provider only in the Microsoft.PowerShell.Security.dll-help.xml file in the module directory.</span></span>

## <a name="function-help-files"></a><span data-ttu-id="24971-117">Függvény súgófájlok</span><span class="sxs-lookup"><span data-stu-id="24971-117">Function Help Files</span></span>

<span data-ttu-id="24971-118">Függvények használatával dokumentálni kell [Megjegyzés-alapú súgó](/powershell/module/microsoft.powershell.core/about/about_comment_based_help) vagy dokumentált súgó XML-fájlban.</span><span class="sxs-lookup"><span data-stu-id="24971-118">Functions can be documented by using [comment-based help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help) or documented in an XML help file.</span></span> <span data-ttu-id="24971-119">Ha a funkció leírása itt található egy XML-fájlt, a következő függvénynek rendelkeznie kell egy `.ExternalHelp` kulcsszó, amely összekapcsolja az XML-fájlt a funkciót megjegyzéseket.</span><span class="sxs-lookup"><span data-stu-id="24971-119">When the function is documented in an XML file, the function must have an `.ExternalHelp` comment keyword that associates the function with the XML file.</span></span> <span data-ttu-id="24971-120">Ellenkező esetben a `Get-Help` parancsmag nem találja a súgófájlt.</span><span class="sxs-lookup"><span data-stu-id="24971-120">Otherwise, the `Get-Help` cmdlet cannot find the help file.</span></span>

<span data-ttu-id="24971-121">Nem vonatkoznak technikai követelmények nevéhez egy függvény súgófájl.</span><span class="sxs-lookup"><span data-stu-id="24971-121">There are no technical requirements for the name of a function help file.</span></span> <span data-ttu-id="24971-122">Azonban ajánlott eljárás, hogy nevezze el a súgófájlban a parancsfájl-modul, amely a függvény definiálva van.</span><span class="sxs-lookup"><span data-stu-id="24971-122">However, a best practice is to name the help file for the script module in which the function is defined.</span></span> <span data-ttu-id="24971-123">Például a következő függvényt a MyModule.psm1 fájlban van definiálva.</span><span class="sxs-lookup"><span data-stu-id="24971-123">For example, the following function is defined in the MyModule.psm1 file.</span></span>

```csharp
#.ExternalHelp MyModule.psm1-help.xml
function Test-Function { ... }
```

## <a name="cim-command-help-files"></a><span data-ttu-id="24971-124">A CIM-parancs súgófájlok</span><span class="sxs-lookup"><span data-stu-id="24971-124">CIM Command Help Files</span></span>

<span data-ttu-id="24971-125">A súgófájl a CIM-parancshoz névvel kell rendelkeznie a CDXML-fájlt, amelyben a CIM-parancs van definiálva.</span><span class="sxs-lookup"><span data-stu-id="24971-125">The help file for a CIM command must be named for the CDXML file in which the CIM command is defined.</span></span> <span data-ttu-id="24971-126">Használja a következő fájl nevének formátuma:</span><span class="sxs-lookup"><span data-stu-id="24971-126">Use the following file name format:</span></span>

```
<FileName>.cdxml-help.xml
```

<span data-ttu-id="24971-127">A CIM-parancsok beágyazott modulként modulokban szereplő CDXML fájlban vannak definiálva.</span><span class="sxs-lookup"><span data-stu-id="24971-127">CIM commands are defined in CDXML files that can be included in modules as nested modules.</span></span> <span data-ttu-id="24971-128">A CIM-parancs a munkamenet függvényében való importálásakor, a Windows PowerShell ad hozzá egy `.ExternalHelp` Megjegyzés kulcsszó használatával a függvény definícióját, amely összekapcsolja a függvény egy XML-súgó-fájlba, amelyben a CIM-parancs van definiálva CDXML-fájl neve.</span><span class="sxs-lookup"><span data-stu-id="24971-128">When the CIM command is imported into the session as a function, Windows PowerShell adds an `.ExternalHelp` comment keyword to the function definition that associates the function with an XML help file that is named for the CDXML file in which the CIM command is defined.</span></span>

## <a name="script-workflow-help-files"></a><span data-ttu-id="24971-129">Parancsfájl-munkafolyamat súgófájlok</span><span class="sxs-lookup"><span data-stu-id="24971-129">Script Workflow Help Files</span></span>

<span data-ttu-id="24971-130">XML-alapú súgófájlokat, amelyek szerepelnek a modulok a parancsfájl-munkafolyamatok is dokumentálni.</span><span class="sxs-lookup"><span data-stu-id="24971-130">Script workflows that are included in modules can be documented in XML-based help files.</span></span> <span data-ttu-id="24971-131">Nem vonatkoznak technikai követelmények a neve, a súgófájlt.</span><span class="sxs-lookup"><span data-stu-id="24971-131">There are no technical requirements for the name of the help file.</span></span> <span data-ttu-id="24971-132">Azonban ajánlott eljárás, hogy nevezze el a súgófájlban a parancsfájl modul, amely a parancsfájl-munkafolyamathoz definiálva van.</span><span class="sxs-lookup"><span data-stu-id="24971-132">However, a best practice is to name the help file for the script module in which the script workflow is defined.</span></span> <span data-ttu-id="24971-133">Például:</span><span class="sxs-lookup"><span data-stu-id="24971-133">For example:</span></span>

```
<ScriptModule>.psm1-help.xml
```

<span data-ttu-id="24971-134">Ellentétben más parancsfájlalapú parancsok parancsfájl-munkafolyamatokban nem szükséges egy `.ExternalHelp` kulcsszó használatával társíthatja azokat a súgófájlban megjegyzéseket.</span><span class="sxs-lookup"><span data-stu-id="24971-134">Unlike other scripted commands, script workflows do not require an `.ExternalHelp` comment keyword to associate them with a help file.</span></span> <span data-ttu-id="24971-135">Ehelyett Windows PowerShell a felhasználói felület kulturális környezet-specifikus alkönyvtárát modul XML-alapú súgó fájlokat keres, és megkeresi az összes fájlt a parancsfájl-munkafolyamathoz tartozó súgó.</span><span class="sxs-lookup"><span data-stu-id="24971-135">Instead, Windows PowerShell searches the UI-Culture-specific subdirectories of the module directory for XML-based help files and looks for help for the script workflow in all the files.</span></span> <span data-ttu-id="24971-136">`.ExternalHelp` Megjegyzés kulcsszót a rendszer figyelmen kívül hagyja.</span><span class="sxs-lookup"><span data-stu-id="24971-136">`.ExternalHelp` comment keyword are ignored.</span></span>

<span data-ttu-id="24971-137">Mivel a `.ExternalHelp` Megjegyzés kulcsszót a rendszer figyelmen kívül hagyja, a `Get-Help` parancsmag talál segítséget a parancsfájl-munkafolyamatokban csak akkor, ha a modulok szerepelnek.</span><span class="sxs-lookup"><span data-stu-id="24971-137">Because the `.ExternalHelp` comment keyword is ignored, the `Get-Help` cmdlet can find help for script workflows only when they are included in modules.</span></span>