---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: PowerShell parancsmag
ms.date: 2016-12-12
title: "Távolítsa el a pswaauthorizationrule"
ms.technology: powershell
ms.openlocfilehash: a8304b68a446de0be98aa732304c71302fb8389e
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="remove-pswaauthorizationrule"></a><span data-ttu-id="80f8f-103">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="80f8f-103">Remove-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="80f8f-104">ÖSSZEGZÉST</span><span class="sxs-lookup"><span data-stu-id="80f8f-104">SYNOPSIS</span></span>

<span data-ttu-id="80f8f-105">A megadott engedélyezési szabály eltávolítása a Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="80f8f-105">Removes a specified authorization rule from Windows PowerShell® Web Access.</span></span>

## <a name="syntax"></a><span data-ttu-id="80f8f-106">SZINTAXIS</span><span class="sxs-lookup"><span data-stu-id="80f8f-106">SYNTAX</span></span>

### <a name="id"></a><span data-ttu-id="80f8f-107">Id</span><span class="sxs-lookup"><span data-stu-id="80f8f-107">Id</span></span>
```
Remove-PswaAuthorizationRule [-Id] <Int32[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

### <a name="rule"></a><span data-ttu-id="80f8f-108">A szabály</span><span class="sxs-lookup"><span data-stu-id="80f8f-108">Rule</span></span>
```
Remove-PswaAuthorizationRule [-Rule] <PswaAuthorizationRule[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="80f8f-109">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="80f8f-109">DESCRIPTION</span></span>

<span data-ttu-id="80f8f-110">A megadott engedélyezési szabály eltávolítása a Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="80f8f-110">Removes a specified authorization rule from Windows PowerShell Web Access.</span></span>

## <a name="parameters"></a><span data-ttu-id="80f8f-111">PARAMÉTEREK</span><span class="sxs-lookup"><span data-stu-id="80f8f-111">PARAMETERS</span></span>

### <a name="-force"></a><span data-ttu-id="80f8f-112">-Force</span><span class="sxs-lookup"><span data-stu-id="80f8f-112">-Force</span></span>

<span data-ttu-id="80f8f-113">A parancsmagot futtatja a jóváhagyás kérése nélkül.</span><span class="sxs-lookup"><span data-stu-id="80f8f-113">Runs the cmdlet without prompting for confirmation.</span></span> <span data-ttu-id="80f8f-114">Alapértelmezés szerint a parancsmag a folytatás előtt megerősítést kér.</span><span class="sxs-lookup"><span data-stu-id="80f8f-114">By default the cmdlet asks for confirmation before proceeding.</span></span>

|||  
|-|-|
| <span data-ttu-id="80f8f-115">Aliasok</span><span class="sxs-lookup"><span data-stu-id="80f8f-115">Aliases</span></span>                              | <span data-ttu-id="80f8f-116">nincs</span><span class="sxs-lookup"><span data-stu-id="80f8f-116">none</span></span>                                 |
| <span data-ttu-id="80f8f-117">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="80f8f-117">Required?</span></span>                            | <span data-ttu-id="80f8f-118">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-118">false</span></span>                                |
| <span data-ttu-id="80f8f-119">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="80f8f-119">Position?</span></span>                            | <span data-ttu-id="80f8f-120">nevű</span><span class="sxs-lookup"><span data-stu-id="80f8f-120">named</span></span>                                |
| <span data-ttu-id="80f8f-121">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="80f8f-121">Default Value</span></span>                        | <span data-ttu-id="80f8f-122">nincs</span><span class="sxs-lookup"><span data-stu-id="80f8f-122">none</span></span>                                 |
| <span data-ttu-id="80f8f-123">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="80f8f-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="80f8f-124">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-124">false</span></span>                                |
| <span data-ttu-id="80f8f-125">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="80f8f-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="80f8f-126">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-126">false</span></span>                                |

### <a name="-id-ltint32gt"></a><span data-ttu-id="80f8f-127">-Id &lt;Int32\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="80f8f-127">-Id &lt;Int32\[\]&gt;</span></span>

<span data-ttu-id="80f8f-128">Megadja a azonosítói (azonosítók) egy vagy több szabály eltávolításához.</span><span class="sxs-lookup"><span data-stu-id="80f8f-128">Specifies the identifiers (IDs) of one or more rules to remove.</span></span>

|||  
|-|-|
| <span data-ttu-id="80f8f-129">Aliasok</span><span class="sxs-lookup"><span data-stu-id="80f8f-129">Aliases</span></span>                              | <span data-ttu-id="80f8f-130">nincs</span><span class="sxs-lookup"><span data-stu-id="80f8f-130">none</span></span>                                 |
| <span data-ttu-id="80f8f-131">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="80f8f-131">Required?</span></span>                            | <span data-ttu-id="80f8f-132">Igaz</span><span class="sxs-lookup"><span data-stu-id="80f8f-132">true</span></span>                                 |
| <span data-ttu-id="80f8f-133">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="80f8f-133">Position?</span></span>                            | <span data-ttu-id="80f8f-134">2</span><span class="sxs-lookup"><span data-stu-id="80f8f-134">2</span></span>                                    |
| <span data-ttu-id="80f8f-135">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="80f8f-135">Default Value</span></span>                        | <span data-ttu-id="80f8f-136">nincs</span><span class="sxs-lookup"><span data-stu-id="80f8f-136">none</span></span>                                 |
| <span data-ttu-id="80f8f-137">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="80f8f-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="80f8f-138">Igaz (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="80f8f-138">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="80f8f-139">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="80f8f-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="80f8f-140">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-140">false</span></span>                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a><span data-ttu-id="80f8f-141">-Szabály &lt;PswaAuthorizationRule\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="80f8f-141">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span></span>

<span data-ttu-id="80f8f-142">Megadja a szabály eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="80f8f-142">Specifies the rules to remove.</span></span>

|||  
|-|-|
| <span data-ttu-id="80f8f-143">Aliasok</span><span class="sxs-lookup"><span data-stu-id="80f8f-143">Aliases</span></span>                              | <span data-ttu-id="80f8f-144">nincs</span><span class="sxs-lookup"><span data-stu-id="80f8f-144">none</span></span>                                 |
| <span data-ttu-id="80f8f-145">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="80f8f-145">Required?</span></span>                            | <span data-ttu-id="80f8f-146">Igaz</span><span class="sxs-lookup"><span data-stu-id="80f8f-146">true</span></span>                                 |
| <span data-ttu-id="80f8f-147">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="80f8f-147">Position?</span></span>                            | <span data-ttu-id="80f8f-148">2</span><span class="sxs-lookup"><span data-stu-id="80f8f-148">2</span></span>                                    |
| <span data-ttu-id="80f8f-149">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="80f8f-149">Default Value</span></span>                        | <span data-ttu-id="80f8f-150">nincs</span><span class="sxs-lookup"><span data-stu-id="80f8f-150">none</span></span>                                 |
| <span data-ttu-id="80f8f-151">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="80f8f-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="80f8f-152">Igaz (ByValue)</span><span class="sxs-lookup"><span data-stu-id="80f8f-152">True (ByValue)</span></span>                       |
| <span data-ttu-id="80f8f-153">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="80f8f-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="80f8f-154">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="80f8f-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="80f8f-155">-Confirm</span></span>

<span data-ttu-id="80f8f-156">Jóváhagyást kér a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="80f8f-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="80f8f-157">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="80f8f-157">Required?</span></span>                            | <span data-ttu-id="80f8f-158">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-158">false</span></span>                                |
| <span data-ttu-id="80f8f-159">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="80f8f-159">Position?</span></span>                            | <span data-ttu-id="80f8f-160">nevű</span><span class="sxs-lookup"><span data-stu-id="80f8f-160">named</span></span>                                |
| <span data-ttu-id="80f8f-161">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="80f8f-161">Default Value</span></span>                        | <span data-ttu-id="80f8f-162">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-162">false</span></span>                                |
| <span data-ttu-id="80f8f-163">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="80f8f-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="80f8f-164">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-164">false</span></span>                                |
| <span data-ttu-id="80f8f-165">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="80f8f-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="80f8f-166">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="80f8f-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="80f8f-167">-WhatIf</span></span>

<span data-ttu-id="80f8f-168">Bemutatja, mi történne a parancsmag futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="80f8f-168">Shows what would happen if the cmdlet runs.</span></span> <span data-ttu-id="80f8f-169">A parancsmag nem fut.</span><span class="sxs-lookup"><span data-stu-id="80f8f-169">The cmdlet is not run.</span></span>

|||  
|-|-|
| <span data-ttu-id="80f8f-170">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="80f8f-170">Required?</span></span>                            | <span data-ttu-id="80f8f-171">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-171">false</span></span>                                |
| <span data-ttu-id="80f8f-172">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="80f8f-172">Position?</span></span>                            | <span data-ttu-id="80f8f-173">nevű</span><span class="sxs-lookup"><span data-stu-id="80f8f-173">named</span></span>                                |
| <span data-ttu-id="80f8f-174">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="80f8f-174">Default Value</span></span>                        | <span data-ttu-id="80f8f-175">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-175">false</span></span>                                |
| <span data-ttu-id="80f8f-176">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="80f8f-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="80f8f-177">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-177">false</span></span>                                |
| <span data-ttu-id="80f8f-178">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="80f8f-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="80f8f-179">hamis</span><span class="sxs-lookup"><span data-stu-id="80f8f-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="80f8f-180">&lt;Általánosparaméterek&gt;</span><span class="sxs-lookup"><span data-stu-id="80f8f-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="80f8f-181">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="80f8f-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="80f8f-182">További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="80f8f-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="80f8f-183">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="80f8f-183">INPUTS</span></span>

### <a name="int"></a><span data-ttu-id="80f8f-184">int\[\]</span><span class="sxs-lookup"><span data-stu-id="80f8f-184">int\[\]</span></span>

<span data-ttu-id="80f8f-185">Ez a parancsmag fogad el, vagy egy számokból álló tömb, vagy PswaAuthorizationRule objektumokból álló tömb.</span><span class="sxs-lookup"><span data-stu-id="80f8f-185">This cmdlet accepts either an array of integers or an array of PswaAuthorizationRule objects.</span></span>

### <a name="pswaauthorizationrule"></a><span data-ttu-id="80f8f-186">PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="80f8f-186">PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="80f8f-187">Ez a parancsmag fogad el, vagy egy számokból álló tömb, vagy PswaAuthorizationRule objektumokból álló tömb.</span><span class="sxs-lookup"><span data-stu-id="80f8f-187">This cmdlet accepts either an array of integers or an array of PswaAuthorizationRule objects.</span></span>

## <a name="outputs"></a><span data-ttu-id="80f8f-188">KIMENETEK</span><span class="sxs-lookup"><span data-stu-id="80f8f-188">OUTPUTS</span></span>

<span data-ttu-id="80f8f-189">Ez a parancsmag nem kimenetet hoz létre.</span><span class="sxs-lookup"><span data-stu-id="80f8f-189">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="80f8f-190">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="80f8f-190">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="80f8f-191">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="80f8f-191">EXAMPLE 1</span></span>

<span data-ttu-id="80f8f-192">Ez a példa eltávolítja az engedélyezési szabály azonosítójú *2*.</span><span class="sxs-lookup"><span data-stu-id="80f8f-192">This example removes the authorization rule with an ID of *2*.</span></span>

```
Remove-PswaAuthorizationRule –Id 2
```

### <a name="example-2-example-2-subheading"></a><span data-ttu-id="80f8f-193">{#Example-2 .subHeading} 2. példa</span><span class="sxs-lookup"><span data-stu-id="80f8f-193">EXAMPLE 2 {#example-2 .subHeading}</span></span>

<span data-ttu-id="80f8f-194">Ez a példa eltávolítja az összes engedélyezési szabályt, és is az a felhasználó jóváhagyást igényel.</span><span class="sxs-lookup"><span data-stu-id="80f8f-194">This example removes all authorization rules and also requires confirmation by the user.</span></span>

```
Get-PswaAuthorizationRule | Remove-PswaAuthorizationRule -Confirm
```

## <a name="related-topics"></a><span data-ttu-id="80f8f-195">Kapcsolódó témakörök</span><span class="sxs-lookup"><span data-stu-id="80f8f-195">Related topics</span></span>

- [<span data-ttu-id="80f8f-196">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="80f8f-196">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="80f8f-197">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="80f8f-197">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="80f8f-198">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="80f8f-198">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="80f8f-199">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="80f8f-199">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
