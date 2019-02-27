---
title: Adjon meg szűrési paraméterekhez |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e45929d1-bbb4-4dc6-892f-f9eacdb1c84c
caps.latest.revision: 8
ms.openlocfilehash: 553878c34e74129f9876cca25a5393cb0d53445a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845737"
---
# <a name="input-filter-parameters"></a><span data-ttu-id="40f00-102">Bemeneti szűrőparaméterek</span><span class="sxs-lookup"><span data-stu-id="40f00-102">Input Filter Parameters</span></span>

<span data-ttu-id="40f00-103">A parancsmag definiálhat `Filter`, `Include`, és `Exclude` szűrése, amely befolyásolja a parancsmag bemeneti objektumok készlete paraméterek.</span><span class="sxs-lookup"><span data-stu-id="40f00-103">A cmdlet can define `Filter`, `Include`, and `Exclude` parameters that filter the set of input objects that the cmdlet affects.</span></span>

<span data-ttu-id="40f00-104">A bemeneti objektumok készlete által meghatározott általában egy `InputObject`, `Path`, vagy `Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="40f00-104">Typically, the set of input objects is specified by an `InputObject`, `Path`, or `Name` parameter.</span></span> <span data-ttu-id="40f00-105">A parancsmag lehet például egy `Path` paraméter, amely több elérési út elfogadja a helyettesítő karaktereket, és minden egyes bemeneti objektum elérési pontok használatával.</span><span class="sxs-lookup"><span data-stu-id="40f00-105">For example, a cmdlet can have a `Path` parameter that accepts multiple paths by using wildcard characters, and each path points to an input object.</span></span> <span data-ttu-id="40f00-106">Együttes, a `Filter`, `Include`, és `Exclude` további paraméterek minősítéséhez az elérési utakat, a parancsmag minden alkalommal, amikor indítva a működik.</span><span class="sxs-lookup"><span data-stu-id="40f00-106">Used together, the `Filter`, `Include`, and `Exclude` parameters further qualify the paths the cmdlet works on each time it is invoked.</span></span>

## <a name="include-and-exclude-parameters"></a><span data-ttu-id="40f00-107">Belefoglalása vagy kizárása a paraméterek</span><span class="sxs-lookup"><span data-stu-id="40f00-107">Include and Exclude Parameters</span></span>

<span data-ttu-id="40f00-108">A `Include` és `Exclude` paramétereket lévő vagy a készletből bemeneti objektumot a parancsmagnak átadott kizárt objektumok azonosítása.</span><span class="sxs-lookup"><span data-stu-id="40f00-108">The `Include` and `Exclude` parameters identify the objects that are included or excluded from the set of input objects passed to the cmdlet.</span></span> <span data-ttu-id="40f00-109">Akkor használja ezeket a paramétereket, ha a szűrőt a standard szintű helyettesítő nyelven lehet kifejezni.</span><span class="sxs-lookup"><span data-stu-id="40f00-109">Use these parameters when the filter can be expressed in the standard wildcard language.</span></span> <span data-ttu-id="40f00-110">(További információ a helyettesítő karakterek: [helyettesítő karaktereket támogató parancsmag-paraméterek](./supporting-wildcard-characters-in-cmdlet-parameters.md).) A `Include` paraméter nevében a belefoglalási szűrőnek megfelelő összes objektumot magában foglalja.</span><span class="sxs-lookup"><span data-stu-id="40f00-110">(For more information about wildcard characters, see [Supporting Wildcards in Cmdlet Parameters](./supporting-wildcard-characters-in-cmdlet-parameters.md).) The `Include` parameter includes all the objects whose names match the inclusion filter.</span></span> <span data-ttu-id="40f00-111">A `Exclude` paraméter nem tartalmazza a mappanevek megfelelnek a szűrőnek összes objektumot.</span><span class="sxs-lookup"><span data-stu-id="40f00-111">The `Exclude` parameter excludes all the objects whose names match the filter.</span></span>

## <a name="filter-parameter"></a><span data-ttu-id="40f00-112">Szűrési paraméterhez</span><span class="sxs-lookup"><span data-stu-id="40f00-112">Filter Parameter</span></span>

<span data-ttu-id="40f00-113">A `Filter` paraméterrel egy szűrőt, amely nem fejezzük ki a standard szintű helyettesítő nyelven.</span><span class="sxs-lookup"><span data-stu-id="40f00-113">The `Filter` parameter specifies a filter that is not expressed in the standard wildcard language.</span></span> <span data-ttu-id="40f00-114">Például az Active Directory Service Interfaces (ADSI) vagy az SQL-szűrők előfordulhat, hogy adható át a parancsmag segítségével a `Filter` paraméter.</span><span class="sxs-lookup"><span data-stu-id="40f00-114">For example, Active Directory Service Interfaces (ADSI) or SQL filters might be passed to the cmdlet through its `Filter` parameter.</span></span> <span data-ttu-id="40f00-115">A parancsmagok a Windows PowerShell által biztosított ezeket a szűrőket, amelyek a parancsmagot egy adattár eléréséhez használja a Windows PowerShell-szolgáltatók által vannak megadva.</span><span class="sxs-lookup"><span data-stu-id="40f00-115">In the cmdlets provided by Windows PowerShell, these filters are specified by the Windows PowerShell providers that use the cmdlet to access a data store.</span></span> <span data-ttu-id="40f00-116">Egyes szolgáltatók jellemzően a saját szűrő határozza meg.</span><span class="sxs-lookup"><span data-stu-id="40f00-116">Each provider typically defines its own filter.</span></span>

## <a name="filtering-if-no-set-of-input-objects-is-specified"></a><span data-ttu-id="40f00-117">Ha meg van adva a nincs megadva bemeneti objektumok szűrése</span><span class="sxs-lookup"><span data-stu-id="40f00-117">Filtering If No Set of Input Objects Is Specified</span></span>

<span data-ttu-id="40f00-118">Ha nincs megadva bemeneti objektumok van megadva, ez általában azt jelenti, szemben az összes objektum szűréséhez.</span><span class="sxs-lookup"><span data-stu-id="40f00-118">If no set of input objects is specified, this typically means to filter against all objects.</span></span> <span data-ttu-id="40f00-119">További információkért lásd:[Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process).</span><span class="sxs-lookup"><span data-stu-id="40f00-119">For more information, see[Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process).</span></span>

## <a name="see-also"></a><span data-ttu-id="40f00-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="40f00-120">See Also</span></span>

[<span data-ttu-id="40f00-121">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="40f00-121">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)