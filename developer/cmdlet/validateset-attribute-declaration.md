---
title: ValidateSet típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes, ValidateSet
- ValidateSet attribute, described
- ValidateSet attribute
ms.assetid: 4a6f97ab-45b2-4f3d-84d4-30acf8e074d0
caps.latest.revision: 12
ms.openlocfilehash: b036f39cd01ffe4b4ce7db9627cb6da0d5327190
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067067"
---
# <a name="validateset-attribute-declaration"></a><span data-ttu-id="f770c-102">ValidateSet attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="f770c-102">ValidateSet Attribute Declaration</span></span>

<span data-ttu-id="f770c-103">A ValidateSetAttribute attribútum egy parancsmag paraméterargumentum a lehetséges értékek egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="f770c-103">The ValidateSetAttribute attribute specifies a set of possible values for a cmdlet parameter argument.</span></span> <span data-ttu-id="f770c-104">Ez az attribútum is használható Windows PowerShell-függvényekkel.</span><span class="sxs-lookup"><span data-stu-id="f770c-104">This attribute can also be used by Windows PowerShell functions.</span></span>

<span data-ttu-id="f770c-105">Ha ez az attribútum meg van adva, a Windows PowerShell-modul határozza meg, hogy a parancsmag-paraméterben megadott argumentum megegyezik-e a megadott elem beállítása egy eleme.</span><span class="sxs-lookup"><span data-stu-id="f770c-105">When this attribute is specified, the Windows PowerShell runtime determines whether the supplied argument for the cmdlet parameter matches an element in the supplied element set.</span></span> <span data-ttu-id="f770c-106">A parancsmag csak akkor, ha a paraméterargumentum megegyezik a készletben lévő elem futtatja.</span><span class="sxs-lookup"><span data-stu-id="f770c-106">The cmdlet is run only if the parameter argument matches an element in the set.</span></span> <span data-ttu-id="f770c-107">Ha nem talál egyezést, egy hiba lépett fel a Windows PowerShell-modul által.</span><span class="sxs-lookup"><span data-stu-id="f770c-107">If no match is found, an error is thrown by the Windows PowerShell runtime.</span></span>

## <a name="syntax"></a><span data-ttu-id="f770c-108">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="f770c-108">Syntax</span></span>

```csharp
[ValidateSetAttribute(params string[] validValues)]
[ValidateSetAttribute(params string[] validValues, Named Parameters)]
```

#### <a name="parameters"></a><span data-ttu-id="f770c-109">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="f770c-109">Parameters</span></span>

<span data-ttu-id="f770c-110">`ValidValues` ([System.String](/dotnet/api/System.String)) szükséges.</span><span class="sxs-lookup"><span data-stu-id="f770c-110">`ValidValues` ([System.String](/dotnet/api/System.String)) Required.</span></span> <span data-ttu-id="f770c-111">Megadja az elem érvényes paraméterértékeket.</span><span class="sxs-lookup"><span data-stu-id="f770c-111">Specifies the valid parameter element values.</span></span> <span data-ttu-id="f770c-112">A következő minta bemutatja, hogyan elem egy vagy több olyan elemet adja meg.</span><span class="sxs-lookup"><span data-stu-id="f770c-112">The following sample shows how to specify one element or multiple elements.</span></span>

```csharp
[ValidateSetAttribute("Steve")]
[ValidateSetAttribute("Steve","Mary")]
```

<span data-ttu-id="f770c-113">`IgnoreCase` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="f770c-113">`IgnoreCase` ([System.Boolean](/dotnet/api/System.Boolean)) Optional named parameter.</span></span> <span data-ttu-id="f770c-114">Az alapértelmezett érték `true` azt jelzi, hogy eset rendszer figyelmen kívül hagyja.</span><span class="sxs-lookup"><span data-stu-id="f770c-114">The default value of `true` indicates that case is ignored.</span></span> <span data-ttu-id="f770c-115">Érték `false` lehetővé teszi a parancsmag kis-és nagybetűket.</span><span class="sxs-lookup"><span data-stu-id="f770c-115">A value of `false` makes the cmdlet case-sensitive.</span></span>

## <a name="remarks"></a><span data-ttu-id="f770c-116">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="f770c-116">Remarks</span></span>

- <span data-ttu-id="f770c-117">Ez az attribútum csak egyszer használható paraméterenként.</span><span class="sxs-lookup"><span data-stu-id="f770c-117">This attribute can be used only once per parameter.</span></span>

- <span data-ttu-id="f770c-118">Ha a paraméter értéke egy tömb, a tömb összes elemét meg kell egyeznie az attribútum a beállított eleme.</span><span class="sxs-lookup"><span data-stu-id="f770c-118">If the parameter value is an array, every element of the array must match an element of the attribute set.</span></span>

- <span data-ttu-id="f770c-119">A ValidateSetAttribute attribútum határozza meg a [System.Management.Automation.Validatesetattribute](/dotnet/api/System.Management.Automation.ValidateSetAttribute) osztály.</span><span class="sxs-lookup"><span data-stu-id="f770c-119">The ValidateSetAttribute attribute is defined by the [System.Management.Automation.Validatesetattribute](/dotnet/api/System.Management.Automation.ValidateSetAttribute) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="f770c-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f770c-120">See Also</span></span>

[<span data-ttu-id="f770c-121">System.Management.Automation.Validatesetattribute</span><span class="sxs-lookup"><span data-stu-id="f770c-121">System.Management.Automation.Validatesetattribute</span></span>](/dotnet/api/System.Management.Automation.ValidateSetAttribute)

[<span data-ttu-id="f770c-122">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="f770c-122">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
