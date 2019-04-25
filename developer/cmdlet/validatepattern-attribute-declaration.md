---
title: ValidatePattern típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes, ValidatePattern
- ValidatePattern attribute, described
- ValidatePattern attribute
ms.assetid: 87b811be-6d93-4e7d-b9d0-c567a19bb0ef
caps.latest.revision: 13
ms.openlocfilehash: 5edcb65a6fbe1cb2fe2d0efe3f763fb84628b049
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067127"
---
# <a name="validatepattern-attribute-declaration"></a><span data-ttu-id="ec938-102">ValidatePattern attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="ec938-102">ValidatePattern Attribute Declaration</span></span>

<span data-ttu-id="ec938-103">A ValidatePattern attribútum határozza meg, amely ellenőrzi az argumentuma egy parancsmag-paraméterben Reguláriskifejezés-mintának.</span><span class="sxs-lookup"><span data-stu-id="ec938-103">The ValidatePattern attribute specifies a regular expression pattern that validates the argument of a cmdlet parameter.</span></span> <span data-ttu-id="ec938-104">Ez az attribútum is használható Windows PowerShell-függvényekkel.</span><span class="sxs-lookup"><span data-stu-id="ec938-104">This attribute can also be used by Windows PowerShell functions.</span></span>

<span data-ttu-id="ec938-105">ValidatePattern belül egy parancsmag meghívása, amikor a Windows PowerShell-modul alakítja át a parancsmag-paraméterben argumentuma egy karakterlánc, és összehasonlítja az, hogy a minta az ValidatePattern attribútum által megadott karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="ec938-105">When ValidatePattern is invoked within a cmdlet, the Windows PowerShell runtime converts the argument of the cmdlet parameter to a string and then compares that string to the pattern supplied by the ValidatePattern attribute.</span></span> <span data-ttu-id="ec938-106">Csak akkor, ha az argumentum, és a megadott mintának konvertált karakteres formáját egyezik a parancsmagot futtatja.</span><span class="sxs-lookup"><span data-stu-id="ec938-106">The cmdlet is run only if the converted string representation of the argument and the supplied pattern match.</span></span> <span data-ttu-id="ec938-107">Ha nem egyeznek, a Windows PowerShell-modul által egy hiba lépett fel.</span><span class="sxs-lookup"><span data-stu-id="ec938-107">If they do not match, an error is thrown by the Windows PowerShell runtime.</span></span>

## <a name="syntax"></a><span data-ttu-id="ec938-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ec938-108">Syntax</span></span>

```csharp
[ValidatePattern(string regexString)]
[ValidatePattern(string regexString, Named Parameters)]
```

#### <a name="parameters"></a><span data-ttu-id="ec938-109">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="ec938-109">Parameters</span></span>

<span data-ttu-id="ec938-110">`RegexString` ([System.String](/dotnet/api/System.String)) szükséges.</span><span class="sxs-lookup"><span data-stu-id="ec938-110">`RegexString` ([System.String](/dotnet/api/System.String)) Required.</span></span> <span data-ttu-id="ec938-111">Itt adhatja meg, amely ellenőrzi a paraméterargumentum reguláris kifejezést.</span><span class="sxs-lookup"><span data-stu-id="ec938-111">Specifies a regular expression that validates the parameter argument.</span></span>

<span data-ttu-id="ec938-112">Beállítások ([System.Text.Regularexpressions.Regexoptions](/dotnet/api/System.Text.RegularExpressions.RegexOptions)) nevű paraméter nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="ec938-112">Options ([System.Text.Regularexpressions.Regexoptions](/dotnet/api/System.Text.RegularExpressions.RegexOptions)) Optional named parameter.</span></span> <span data-ttu-id="ec938-113">Adja meg a bitenkénti kombinációját [System.Text.Regularexpressions.Regexoptions](/dotnet/api/System.Text.RegularExpressions.RegexOptions) reguláris kifejezés beállítások meghatározó jelzők.</span><span class="sxs-lookup"><span data-stu-id="ec938-113">Specifies a bitwise combination of [System.Text.Regularexpressions.Regexoptions](/dotnet/api/System.Text.RegularExpressions.RegexOptions) flags that specify regular expression options.</span></span>

## <a name="remarks"></a><span data-ttu-id="ec938-114">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="ec938-114">Remarks</span></span>

- <span data-ttu-id="ec938-115">Ez az attribútum csak egyszer használható paraméterenként.</span><span class="sxs-lookup"><span data-stu-id="ec938-115">This attribute can be used only once per parameter.</span></span>

- <span data-ttu-id="ec938-116">Használhatja a `Option` paraméter az attribútum a minta még jobban meghatározhatja.</span><span class="sxs-lookup"><span data-stu-id="ec938-116">You can use the `Option` parameter of the attribute to further define the pattern.</span></span> <span data-ttu-id="ec938-117">Például hogy a minta kis-és nagybetűket.</span><span class="sxs-lookup"><span data-stu-id="ec938-117">For example, you can make the pattern case sensitive.</span></span>

- <span data-ttu-id="ec938-118">Ez az attribútum egy gyűjtemény alkalmazza, ha minden elem a gyűjteményben lévő meg kell egyeznie a minta.</span><span class="sxs-lookup"><span data-stu-id="ec938-118">If this attribute is applied to a collection, each element in the collection must match the pattern.</span></span>

- <span data-ttu-id="ec938-119">A ValidatePattern attribútum határozza meg a [System.Management.Automation.Validatepatternattribute](/dotnet/api/System.Management.Automation.ValidatePatternAttribute) osztály.</span><span class="sxs-lookup"><span data-stu-id="ec938-119">The ValidatePattern attribute is defined by the [System.Management.Automation.Validatepatternattribute](/dotnet/api/System.Management.Automation.ValidatePatternAttribute) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="ec938-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ec938-120">See Also</span></span>

[<span data-ttu-id="ec938-121">System.Management.Automation.Validatepatternattribute</span><span class="sxs-lookup"><span data-stu-id="ec938-121">System.Management.Automation.Validatepatternattribute</span></span>](/dotnet/api/System.Management.Automation.ValidatePatternAttribute)

[<span data-ttu-id="ec938-122">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="ec938-122">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
