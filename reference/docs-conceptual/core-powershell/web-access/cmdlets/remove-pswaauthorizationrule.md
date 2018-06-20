---
ms.topic: reference
keywords: PowerShell parancsmag
ms.date: 12/12/2016
title: Remove-PswaAuthorizationRule
ms.openlocfilehash: 6a3720bb9b8df3e1c6bb9f4a6196c9868b85b67d
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189033"
---
# <a name="remove-pswaauthorizationrule"></a><span data-ttu-id="4d256-103">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4d256-103">Remove-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="4d256-104">SYNOPSIS</span><span class="sxs-lookup"><span data-stu-id="4d256-104">SYNOPSIS</span></span>

<span data-ttu-id="4d256-105">A megadott engedélyezési szabály eltávolítása a Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="4d256-105">Removes a specified authorization rule from Windows PowerShell® Web Access.</span></span>

## <a name="syntax"></a><span data-ttu-id="4d256-106">SZINTAXIS</span><span class="sxs-lookup"><span data-stu-id="4d256-106">SYNTAX</span></span>

### <a name="id"></a><span data-ttu-id="4d256-107">Id</span><span class="sxs-lookup"><span data-stu-id="4d256-107">Id</span></span>
```
Remove-PswaAuthorizationRule [-Id] <Int32[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

### <a name="rule"></a><span data-ttu-id="4d256-108">A szabály</span><span class="sxs-lookup"><span data-stu-id="4d256-108">Rule</span></span>
```
Remove-PswaAuthorizationRule [-Rule] <PswaAuthorizationRule[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="4d256-109">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="4d256-109">DESCRIPTION</span></span>

<span data-ttu-id="4d256-110">A megadott engedélyezési szabály eltávolítása a Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="4d256-110">Removes a specified authorization rule from Windows PowerShell Web Access.</span></span>

## <a name="parameters"></a><span data-ttu-id="4d256-111">PARAMÉTEREK</span><span class="sxs-lookup"><span data-stu-id="4d256-111">PARAMETERS</span></span>

### <a name="-force"></a><span data-ttu-id="4d256-112">-Force</span><span class="sxs-lookup"><span data-stu-id="4d256-112">-Force</span></span>

<span data-ttu-id="4d256-113">A parancsmagot futtatja a jóváhagyás kérése nélkül.</span><span class="sxs-lookup"><span data-stu-id="4d256-113">Runs the cmdlet without prompting for confirmation.</span></span> <span data-ttu-id="4d256-114">Alapértelmezés szerint a parancsmag a folytatás előtt megerősítést kér.</span><span class="sxs-lookup"><span data-stu-id="4d256-114">By default the cmdlet asks for confirmation before proceeding.</span></span>

|||
|-|-|
| <span data-ttu-id="4d256-115">Aliasok</span><span class="sxs-lookup"><span data-stu-id="4d256-115">Aliases</span></span>                              | <span data-ttu-id="4d256-116">nincs</span><span class="sxs-lookup"><span data-stu-id="4d256-116">none</span></span>                                 |
| <span data-ttu-id="4d256-117">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="4d256-117">Required?</span></span>                            | <span data-ttu-id="4d256-118">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-118">false</span></span>                                |
| <span data-ttu-id="4d256-119">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="4d256-119">Position?</span></span>                            | <span data-ttu-id="4d256-120">nevű</span><span class="sxs-lookup"><span data-stu-id="4d256-120">named</span></span>                                |
| <span data-ttu-id="4d256-121">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="4d256-121">Default Value</span></span>                        | <span data-ttu-id="4d256-122">nincs</span><span class="sxs-lookup"><span data-stu-id="4d256-122">none</span></span>                                 |
| <span data-ttu-id="4d256-123">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="4d256-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4d256-124">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-124">false</span></span>                                |
| <span data-ttu-id="4d256-125">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="4d256-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4d256-126">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-126">false</span></span>                                |

### <a name="-id-ltint32gt"></a><span data-ttu-id="4d256-127">-Id &lt;Int32\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="4d256-127">-Id &lt;Int32\[\]&gt;</span></span>

<span data-ttu-id="4d256-128">Megadja a azonosítói (azonosítók) egy vagy több szabály eltávolításához.</span><span class="sxs-lookup"><span data-stu-id="4d256-128">Specifies the identifiers (IDs) of one or more rules to remove.</span></span>

|||
|-|-|
| <span data-ttu-id="4d256-129">Aliasok</span><span class="sxs-lookup"><span data-stu-id="4d256-129">Aliases</span></span>                              | <span data-ttu-id="4d256-130">nincs</span><span class="sxs-lookup"><span data-stu-id="4d256-130">none</span></span>                                 |
| <span data-ttu-id="4d256-131">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="4d256-131">Required?</span></span>                            | <span data-ttu-id="4d256-132">Igaz</span><span class="sxs-lookup"><span data-stu-id="4d256-132">true</span></span>                                 |
| <span data-ttu-id="4d256-133">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="4d256-133">Position?</span></span>                            | <span data-ttu-id="4d256-134">2</span><span class="sxs-lookup"><span data-stu-id="4d256-134">2</span></span>                                    |
| <span data-ttu-id="4d256-135">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="4d256-135">Default Value</span></span>                        | <span data-ttu-id="4d256-136">nincs</span><span class="sxs-lookup"><span data-stu-id="4d256-136">none</span></span>                                 |
| <span data-ttu-id="4d256-137">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="4d256-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4d256-138">Igaz (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="4d256-138">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="4d256-139">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="4d256-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4d256-140">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-140">false</span></span>                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a><span data-ttu-id="4d256-141">-Szabály &lt;PswaAuthorizationRule\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="4d256-141">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span></span>

<span data-ttu-id="4d256-142">Megadja a szabály eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="4d256-142">Specifies the rules to remove.</span></span>

|||
|-|-|
| <span data-ttu-id="4d256-143">Aliasok</span><span class="sxs-lookup"><span data-stu-id="4d256-143">Aliases</span></span>                              | <span data-ttu-id="4d256-144">nincs</span><span class="sxs-lookup"><span data-stu-id="4d256-144">none</span></span>                                 |
| <span data-ttu-id="4d256-145">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="4d256-145">Required?</span></span>                            | <span data-ttu-id="4d256-146">Igaz</span><span class="sxs-lookup"><span data-stu-id="4d256-146">true</span></span>                                 |
| <span data-ttu-id="4d256-147">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="4d256-147">Position?</span></span>                            | <span data-ttu-id="4d256-148">2</span><span class="sxs-lookup"><span data-stu-id="4d256-148">2</span></span>                                    |
| <span data-ttu-id="4d256-149">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="4d256-149">Default Value</span></span>                        | <span data-ttu-id="4d256-150">nincs</span><span class="sxs-lookup"><span data-stu-id="4d256-150">none</span></span>                                 |
| <span data-ttu-id="4d256-151">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="4d256-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4d256-152">Igaz (ByValue)</span><span class="sxs-lookup"><span data-stu-id="4d256-152">True (ByValue)</span></span>                       |
| <span data-ttu-id="4d256-153">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="4d256-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4d256-154">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="4d256-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="4d256-155">-Confirm</span></span>

<span data-ttu-id="4d256-156">Jóváhagyást kér a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="4d256-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="4d256-157">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="4d256-157">Required?</span></span>                            | <span data-ttu-id="4d256-158">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-158">false</span></span>                                |
| <span data-ttu-id="4d256-159">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="4d256-159">Position?</span></span>                            | <span data-ttu-id="4d256-160">nevű</span><span class="sxs-lookup"><span data-stu-id="4d256-160">named</span></span>                                |
| <span data-ttu-id="4d256-161">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="4d256-161">Default Value</span></span>                        | <span data-ttu-id="4d256-162">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-162">false</span></span>                                |
| <span data-ttu-id="4d256-163">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="4d256-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4d256-164">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-164">false</span></span>                                |
| <span data-ttu-id="4d256-165">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="4d256-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4d256-166">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="4d256-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="4d256-167">-WhatIf</span></span>

<span data-ttu-id="4d256-168">Bemutatja, mi történne a parancsmag futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="4d256-168">Shows what would happen if the cmdlet runs.</span></span> <span data-ttu-id="4d256-169">A parancsmag nem fut.</span><span class="sxs-lookup"><span data-stu-id="4d256-169">The cmdlet is not run.</span></span>

|||
|-|-|
| <span data-ttu-id="4d256-170">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="4d256-170">Required?</span></span>                            | <span data-ttu-id="4d256-171">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-171">false</span></span>                                |
| <span data-ttu-id="4d256-172">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="4d256-172">Position?</span></span>                            | <span data-ttu-id="4d256-173">nevű</span><span class="sxs-lookup"><span data-stu-id="4d256-173">named</span></span>                                |
| <span data-ttu-id="4d256-174">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="4d256-174">Default Value</span></span>                        | <span data-ttu-id="4d256-175">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-175">false</span></span>                                |
| <span data-ttu-id="4d256-176">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="4d256-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4d256-177">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-177">false</span></span>                                |
| <span data-ttu-id="4d256-178">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="4d256-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4d256-179">hamis</span><span class="sxs-lookup"><span data-stu-id="4d256-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="4d256-180">&lt;Általánosparaméterek&gt;</span><span class="sxs-lookup"><span data-stu-id="4d256-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="4d256-181">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="4d256-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="4d256-182">További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="4d256-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="4d256-183">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="4d256-183">INPUTS</span></span>

### <a name="int"></a><span data-ttu-id="4d256-184">int\[\]</span><span class="sxs-lookup"><span data-stu-id="4d256-184">int\[\]</span></span>

<span data-ttu-id="4d256-185">Ez a parancsmag fogad el, vagy egy számokból álló tömb, vagy PswaAuthorizationRule objektumokból álló tömb.</span><span class="sxs-lookup"><span data-stu-id="4d256-185">This cmdlet accepts either an array of integers or an array of PswaAuthorizationRule objects.</span></span>

### <a name="pswaauthorizationrule"></a><span data-ttu-id="4d256-186">PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="4d256-186">PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="4d256-187">Ez a parancsmag fogad el, vagy egy számokból álló tömb, vagy PswaAuthorizationRule objektumokból álló tömb.</span><span class="sxs-lookup"><span data-stu-id="4d256-187">This cmdlet accepts either an array of integers or an array of PswaAuthorizationRule objects.</span></span>

## <a name="outputs"></a><span data-ttu-id="4d256-188">KIMENETEK</span><span class="sxs-lookup"><span data-stu-id="4d256-188">OUTPUTS</span></span>

<span data-ttu-id="4d256-189">Ez a parancsmag nem kimenetet hoz létre.</span><span class="sxs-lookup"><span data-stu-id="4d256-189">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="4d256-190">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="4d256-190">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="4d256-191">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="4d256-191">EXAMPLE 1</span></span>

<span data-ttu-id="4d256-192">Ez a példa eltávolítja az engedélyezési szabály azonosítójú *2*.</span><span class="sxs-lookup"><span data-stu-id="4d256-192">This example removes the authorization rule with an ID of *2*.</span></span>

```
Remove-PswaAuthorizationRule –Id 2
```

### <a name="example-2-example-2-subheading"></a><span data-ttu-id="4d256-193">{#Example-2 .subHeading} 2. példa</span><span class="sxs-lookup"><span data-stu-id="4d256-193">EXAMPLE 2 {#example-2 .subHeading}</span></span>

<span data-ttu-id="4d256-194">Ez a példa eltávolítja az összes engedélyezési szabályt, és is az a felhasználó jóváhagyást igényel.</span><span class="sxs-lookup"><span data-stu-id="4d256-194">This example removes all authorization rules and also requires confirmation by the user.</span></span>

```
Get-PswaAuthorizationRule | Remove-PswaAuthorizationRule -Confirm
```

## <a name="related-topics"></a><span data-ttu-id="4d256-195">Kapcsolódó témakörök</span><span class="sxs-lookup"><span data-stu-id="4d256-195">Related topics</span></span>

- [<span data-ttu-id="4d256-196">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4d256-196">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="4d256-197">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4d256-197">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="4d256-198">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="4d256-198">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="4d256-199">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4d256-199">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)