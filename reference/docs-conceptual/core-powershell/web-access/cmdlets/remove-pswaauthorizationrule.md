---
description: 
ms.topic: article
ms.prod: powershell
keywords: PowerShell parancsmag
ms.date: 2016-12-12
title: "Távolítsa el a pswaauthorizationrule"
ms.technology: powershell
ms.openlocfilehash: 4d039e7e00f87bc7aebb89217251edbbb5c3f5be
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="remove-pswaauthorizationrule"></a><span data-ttu-id="5e0e0-103">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="5e0e0-103">Remove-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="5e0e0-104">SYNOPSIS</span><span class="sxs-lookup"><span data-stu-id="5e0e0-104">SYNOPSIS</span></span>

<span data-ttu-id="5e0e0-105">A megadott engedélyezési szabály eltávolítása a Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-105">Removes a specified authorization rule from Windows PowerShell® Web Access.</span></span>

## <a name="syntax"></a><span data-ttu-id="5e0e0-106">SZINTAXIS</span><span class="sxs-lookup"><span data-stu-id="5e0e0-106">SYNTAX</span></span>

### <a name="id"></a><span data-ttu-id="5e0e0-107">Id</span><span class="sxs-lookup"><span data-stu-id="5e0e0-107">Id</span></span>
```
Remove-PswaAuthorizationRule [-Id] <Int32[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

### <a name="rule"></a><span data-ttu-id="5e0e0-108">A szabály</span><span class="sxs-lookup"><span data-stu-id="5e0e0-108">Rule</span></span>
```
Remove-PswaAuthorizationRule [-Rule] <PswaAuthorizationRule[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="5e0e0-109">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="5e0e0-109">DESCRIPTION</span></span>

<span data-ttu-id="5e0e0-110">A megadott engedélyezési szabály eltávolítása a Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-110">Removes a specified authorization rule from Windows PowerShell Web Access.</span></span>

## <a name="parameters"></a><span data-ttu-id="5e0e0-111">PARAMÉTEREK</span><span class="sxs-lookup"><span data-stu-id="5e0e0-111">PARAMETERS</span></span>

### <a name="-force"></a><span data-ttu-id="5e0e0-112">-Force</span><span class="sxs-lookup"><span data-stu-id="5e0e0-112">-Force</span></span>

<span data-ttu-id="5e0e0-113">A parancsmagot futtatja a jóváhagyás kérése nélkül.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-113">Runs the cmdlet without prompting for confirmation.</span></span> <span data-ttu-id="5e0e0-114">Alapértelmezés szerint a parancsmag a folytatás előtt megerősítést kér.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-114">By default the cmdlet asks for confirmation before proceeding.</span></span>

|||  
|-|-|
| <span data-ttu-id="5e0e0-115">Aliasok</span><span class="sxs-lookup"><span data-stu-id="5e0e0-115">Aliases</span></span>                              | <span data-ttu-id="5e0e0-116">nincs</span><span class="sxs-lookup"><span data-stu-id="5e0e0-116">none</span></span>                                 |
| <span data-ttu-id="5e0e0-117">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-117">Required?</span></span>                            | <span data-ttu-id="5e0e0-118">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-118">false</span></span>                                |
| <span data-ttu-id="5e0e0-119">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-119">Position?</span></span>                            | <span data-ttu-id="5e0e0-120">nevű</span><span class="sxs-lookup"><span data-stu-id="5e0e0-120">named</span></span>                                |
| <span data-ttu-id="5e0e0-121">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="5e0e0-121">Default Value</span></span>                        | <span data-ttu-id="5e0e0-122">nincs</span><span class="sxs-lookup"><span data-stu-id="5e0e0-122">none</span></span>                                 |
| <span data-ttu-id="5e0e0-123">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="5e0e0-124">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-124">false</span></span>                                |
| <span data-ttu-id="5e0e0-125">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="5e0e0-126">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-126">false</span></span>                                |

### <a name="-id-ltint32gt"></a><span data-ttu-id="5e0e0-127">-Id &lt;Int32\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="5e0e0-127">-Id &lt;Int32\[\]&gt;</span></span>

<span data-ttu-id="5e0e0-128">Megadja a azonosítói (azonosítók) egy vagy több szabály eltávolításához.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-128">Specifies the identifiers (IDs) of one or more rules to remove.</span></span>

|||  
|-|-|
| <span data-ttu-id="5e0e0-129">Aliasok</span><span class="sxs-lookup"><span data-stu-id="5e0e0-129">Aliases</span></span>                              | <span data-ttu-id="5e0e0-130">nincs</span><span class="sxs-lookup"><span data-stu-id="5e0e0-130">none</span></span>                                 |
| <span data-ttu-id="5e0e0-131">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-131">Required?</span></span>                            | <span data-ttu-id="5e0e0-132">Igaz</span><span class="sxs-lookup"><span data-stu-id="5e0e0-132">true</span></span>                                 |
| <span data-ttu-id="5e0e0-133">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-133">Position?</span></span>                            | <span data-ttu-id="5e0e0-134">2</span><span class="sxs-lookup"><span data-stu-id="5e0e0-134">2</span></span>                                    |
| <span data-ttu-id="5e0e0-135">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="5e0e0-135">Default Value</span></span>                        | <span data-ttu-id="5e0e0-136">nincs</span><span class="sxs-lookup"><span data-stu-id="5e0e0-136">none</span></span>                                 |
| <span data-ttu-id="5e0e0-137">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="5e0e0-138">Igaz (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="5e0e0-138">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="5e0e0-139">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="5e0e0-140">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-140">false</span></span>                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a><span data-ttu-id="5e0e0-141">-Szabály &lt;PswaAuthorizationRule\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="5e0e0-141">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span></span>

<span data-ttu-id="5e0e0-142">Megadja a szabály eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-142">Specifies the rules to remove.</span></span>

|||  
|-|-|
| <span data-ttu-id="5e0e0-143">Aliasok</span><span class="sxs-lookup"><span data-stu-id="5e0e0-143">Aliases</span></span>                              | <span data-ttu-id="5e0e0-144">nincs</span><span class="sxs-lookup"><span data-stu-id="5e0e0-144">none</span></span>                                 |
| <span data-ttu-id="5e0e0-145">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-145">Required?</span></span>                            | <span data-ttu-id="5e0e0-146">Igaz</span><span class="sxs-lookup"><span data-stu-id="5e0e0-146">true</span></span>                                 |
| <span data-ttu-id="5e0e0-147">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-147">Position?</span></span>                            | <span data-ttu-id="5e0e0-148">2</span><span class="sxs-lookup"><span data-stu-id="5e0e0-148">2</span></span>                                    |
| <span data-ttu-id="5e0e0-149">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="5e0e0-149">Default Value</span></span>                        | <span data-ttu-id="5e0e0-150">nincs</span><span class="sxs-lookup"><span data-stu-id="5e0e0-150">none</span></span>                                 |
| <span data-ttu-id="5e0e0-151">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="5e0e0-152">Igaz (ByValue)</span><span class="sxs-lookup"><span data-stu-id="5e0e0-152">True (ByValue)</span></span>                       |
| <span data-ttu-id="5e0e0-153">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="5e0e0-154">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="5e0e0-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="5e0e0-155">-Confirm</span></span>

<span data-ttu-id="5e0e0-156">Jóváhagyást kér a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="5e0e0-157">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-157">Required?</span></span>                            | <span data-ttu-id="5e0e0-158">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-158">false</span></span>                                |
| <span data-ttu-id="5e0e0-159">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-159">Position?</span></span>                            | <span data-ttu-id="5e0e0-160">nevű</span><span class="sxs-lookup"><span data-stu-id="5e0e0-160">named</span></span>                                |
| <span data-ttu-id="5e0e0-161">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="5e0e0-161">Default Value</span></span>                        | <span data-ttu-id="5e0e0-162">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-162">false</span></span>                                |
| <span data-ttu-id="5e0e0-163">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="5e0e0-164">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-164">false</span></span>                                |
| <span data-ttu-id="5e0e0-165">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="5e0e0-166">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="5e0e0-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="5e0e0-167">-WhatIf</span></span>

<span data-ttu-id="5e0e0-168">Bemutatja, mi történne a parancsmag futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-168">Shows what would happen if the cmdlet runs.</span></span> <span data-ttu-id="5e0e0-169">A parancsmag nem fut.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-169">The cmdlet is not run.</span></span>

|||  
|-|-|
| <span data-ttu-id="5e0e0-170">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-170">Required?</span></span>                            | <span data-ttu-id="5e0e0-171">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-171">false</span></span>                                |
| <span data-ttu-id="5e0e0-172">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-172">Position?</span></span>                            | <span data-ttu-id="5e0e0-173">nevű</span><span class="sxs-lookup"><span data-stu-id="5e0e0-173">named</span></span>                                |
| <span data-ttu-id="5e0e0-174">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="5e0e0-174">Default Value</span></span>                        | <span data-ttu-id="5e0e0-175">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-175">false</span></span>                                |
| <span data-ttu-id="5e0e0-176">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="5e0e0-177">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-177">false</span></span>                                |
| <span data-ttu-id="5e0e0-178">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="5e0e0-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="5e0e0-179">hamis</span><span class="sxs-lookup"><span data-stu-id="5e0e0-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="5e0e0-180">&lt;Általánosparaméterek&gt;</span><span class="sxs-lookup"><span data-stu-id="5e0e0-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="5e0e0-181">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="5e0e0-182">További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="5e0e0-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="5e0e0-183">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="5e0e0-183">INPUTS</span></span>

### <a name="int"></a><span data-ttu-id="5e0e0-184">int\[\]</span><span class="sxs-lookup"><span data-stu-id="5e0e0-184">int\[\]</span></span>

<span data-ttu-id="5e0e0-185">Ez a parancsmag fogad el, vagy egy számokból álló tömb, vagy PswaAuthorizationRule objektumokból álló tömb.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-185">This cmdlet accepts either an array of integers or an array of PswaAuthorizationRule objects.</span></span>

### <a name="pswaauthorizationrule"></a><span data-ttu-id="5e0e0-186">PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="5e0e0-186">PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="5e0e0-187">Ez a parancsmag fogad el, vagy egy számokból álló tömb, vagy PswaAuthorizationRule objektumokból álló tömb.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-187">This cmdlet accepts either an array of integers or an array of PswaAuthorizationRule objects.</span></span>

## <a name="outputs"></a><span data-ttu-id="5e0e0-188">KIMENETEK</span><span class="sxs-lookup"><span data-stu-id="5e0e0-188">OUTPUTS</span></span>

<span data-ttu-id="5e0e0-189">Ez a parancsmag nem kimenetet hoz létre.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-189">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="5e0e0-190">EXAMPLES</span><span class="sxs-lookup"><span data-stu-id="5e0e0-190">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="5e0e0-191">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="5e0e0-191">EXAMPLE 1</span></span>

<span data-ttu-id="5e0e0-192">Ez a példa eltávolítja az engedélyezési szabály azonosítójú *2*.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-192">This example removes the authorization rule with an ID of *2*.</span></span>

```
Remove-PswaAuthorizationRule –Id 2
```

### <a name="example-2-example-2-subheading"></a><span data-ttu-id="5e0e0-193">{#Example-2 .subHeading} 2. példa</span><span class="sxs-lookup"><span data-stu-id="5e0e0-193">EXAMPLE 2 {#example-2 .subHeading}</span></span>

<span data-ttu-id="5e0e0-194">Ez a példa eltávolítja az összes engedélyezési szabályt, és is az a felhasználó jóváhagyást igényel.</span><span class="sxs-lookup"><span data-stu-id="5e0e0-194">This example removes all authorization rules and also requires confirmation by the user.</span></span>

```
Get-PswaAuthorizationRule | Remove-PswaAuthorizationRule -Confirm
```

## <a name="related-topics"></a><span data-ttu-id="5e0e0-195">Kapcsolódó témakörök</span><span class="sxs-lookup"><span data-stu-id="5e0e0-195">Related topics</span></span>

- [<span data-ttu-id="5e0e0-196">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="5e0e0-196">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="5e0e0-197">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="5e0e0-197">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="5e0e0-198">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="5e0e0-198">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="5e0e0-199">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="5e0e0-199">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
