---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: PowerShell parancsmag
ms.date: 2016-12-12
title: test-pswaauthorizationrule
ms.technology: powershell
ms.openlocfilehash: 900547301c815ba6fe3a9507f975503fec864e4e
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="test-pswaauthorizationrule"></a><span data-ttu-id="9c8c2-103">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="9c8c2-103">Test-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="9c8c2-104">ÖSSZEGZÉST</span><span class="sxs-lookup"><span data-stu-id="9c8c2-104">SYNOPSIS</span></span>

<span data-ttu-id="9c8c2-105">Ellenőrzi, hogy létezik-e szabály egy adott felhasználó, számítógép vagy végpont.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-105">Verifies whether a rule exists for a specified user, computer, or endpoint.</span></span>

## <a name="syntax"></a><span data-ttu-id="9c8c2-106">SZINTAXIS</span><span class="sxs-lookup"><span data-stu-id="9c8c2-106">SYNTAX</span></span>

### <a name="computername"></a><span data-ttu-id="9c8c2-107">ComputerName</span><span class="sxs-lookup"><span data-stu-id="9c8c2-107">ComputerName</span></span>
```
Test-PswaAuthorizationRule [-UserName] <String> [-ComputerName] <String> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

### <a name="connectionuri"></a><span data-ttu-id="9c8c2-108">ConnectionUri</span><span class="sxs-lookup"><span data-stu-id="9c8c2-108">ConnectionUri</span></span>
```
Test-PswaAuthorizationRule [-UserName] <String> [-ConnectionUri] <Uri> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="9c8c2-109">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="9c8c2-109">DESCRIPTION</span></span>

<span data-ttu-id="9c8c2-110">A **Test-PswaAuthorizationRule** parancsmag ellenőrzi, hogy létezik-e szabály egy adott felhasználó, számítógép vagy végpont.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-110">The **Test-PswaAuthorizationRule** cmdlet verifies whether a rule exists for a specified user, computer, or endpoint.</span></span>
<span data-ttu-id="9c8c2-111">Ez a parancsmag is használható engedélyezési szabályokat, ellenőrizze, hogy engedélyezve van-e egy adott felhasználó, számítógép vagy a végpont a hozzáférési kérelem teszteléséhez.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-111">This cmdlet can also be used to test authorization rules, to validate that a particular user, computer or endpoint access request is authorized.</span></span>
<span data-ttu-id="9c8c2-112">Alapértelmezés szerint ez a parancsmag a hitelesítési fájlhoz az összes szabályt kiértékeli.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-112">By default, this cmdlet evaluates all rules in the authorization file.</span></span>
<span data-ttu-id="9c8c2-113">A vizsgálandó szabályok részhalmazát is megadhat.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-113">However, you can specify a subset of rules to test.</span></span>

<span data-ttu-id="9c8c2-114">Ez a parancsmag segítségével hitelesítési hibák elhárítása.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-114">You can use this cmdlet to help troubleshoot authentication failures.</span></span>

<span data-ttu-id="9c8c2-115">Ez a parancsmag paramétereit felel meg a Windows PowerShell® Web Access bejelentkezési oldalra mezőket.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-115">The parameters for this cmdlet correspond to fields on the Windows PowerShell® Web Access sign-on page.</span></span>

## <a name="parameters"></a><span data-ttu-id="9c8c2-116">PARAMÉTEREK</span><span class="sxs-lookup"><span data-stu-id="9c8c2-116">PARAMETERS</span></span>

### <a name="-computername-ltstringgt"></a><span data-ttu-id="9c8c2-117">-ComputerName &lt;karakterlánc&gt;</span><span class="sxs-lookup"><span data-stu-id="9c8c2-117">-ComputerName &lt;String&gt;</span></span>

<span data-ttu-id="9c8c2-118">Adja meg a vizsgálandó számítógép nevét.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-118">Specifies the name of the computer to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="9c8c2-119">Aliasok</span><span class="sxs-lookup"><span data-stu-id="9c8c2-119">Aliases</span></span>                              | <span data-ttu-id="9c8c2-120">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-120">none</span></span>                                 |
| <span data-ttu-id="9c8c2-121">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-121">Required?</span></span>                            | <span data-ttu-id="9c8c2-122">Igaz</span><span class="sxs-lookup"><span data-stu-id="9c8c2-122">true</span></span>                                 |
| <span data-ttu-id="9c8c2-123">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-123">Position?</span></span>                            | <span data-ttu-id="9c8c2-124">2</span><span class="sxs-lookup"><span data-stu-id="9c8c2-124">2</span></span>                                    |
| <span data-ttu-id="9c8c2-125">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="9c8c2-125">Default Value</span></span>                        | <span data-ttu-id="9c8c2-126">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-126">none</span></span>                                 |
| <span data-ttu-id="9c8c2-127">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-127">Accept Pipeline Input?</span></span>               | <span data-ttu-id="9c8c2-128">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-128">false</span></span>                                |
| <span data-ttu-id="9c8c2-129">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-129">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="9c8c2-130">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-130">false</span></span>                                |

### <a name="-configurationname-ltstringgt"></a><span data-ttu-id="9c8c2-131">-ConfigurationName &lt;karakterlánc&gt;</span><span class="sxs-lookup"><span data-stu-id="9c8c2-131">-ConfigurationName &lt;String&gt;</span></span>

<span data-ttu-id="9c8c2-132">Megadja a nevét, a Windows PowerShell munkamenet-konfiguráció, más néven a végpont vagy a futási térből, teszteléséhez.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-132">Specifies the name of the Windows PowerShell session configuration, also known as endpoint or runspace, to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="9c8c2-133">Aliasok</span><span class="sxs-lookup"><span data-stu-id="9c8c2-133">Aliases</span></span>                              | <span data-ttu-id="9c8c2-134">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-134">none</span></span>                                 |
| <span data-ttu-id="9c8c2-135">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-135">Required?</span></span>                            | <span data-ttu-id="9c8c2-136">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-136">false</span></span>                                |
| <span data-ttu-id="9c8c2-137">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-137">Position?</span></span>                            | <span data-ttu-id="9c8c2-138">3</span><span class="sxs-lookup"><span data-stu-id="9c8c2-138">3</span></span>                                    |
| <span data-ttu-id="9c8c2-139">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="9c8c2-139">Default Value</span></span>                        | <span data-ttu-id="9c8c2-140">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-140">none</span></span>                                 |
| <span data-ttu-id="9c8c2-141">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-141">Accept Pipeline Input?</span></span>               | <span data-ttu-id="9c8c2-142">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-142">false</span></span>                                |
| <span data-ttu-id="9c8c2-143">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-143">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="9c8c2-144">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-144">false</span></span>                                |

### <a name="-connectionuri-lturigt"></a><span data-ttu-id="9c8c2-145">-ConnectionUri &lt;Uri&gt;</span><span class="sxs-lookup"><span data-stu-id="9c8c2-145">-ConnectionUri &lt;Uri&gt;</span></span>

<span data-ttu-id="9c8c2-146">Megadja a kapcsolat tesztelése URI.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-146">Specifies the connection URI to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="9c8c2-147">Aliasok</span><span class="sxs-lookup"><span data-stu-id="9c8c2-147">Aliases</span></span>                              | <span data-ttu-id="9c8c2-148">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-148">none</span></span>                                 |
| <span data-ttu-id="9c8c2-149">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-149">Required?</span></span>                            | <span data-ttu-id="9c8c2-150">Igaz</span><span class="sxs-lookup"><span data-stu-id="9c8c2-150">true</span></span>                                 |
| <span data-ttu-id="9c8c2-151">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-151">Position?</span></span>                            | <span data-ttu-id="9c8c2-152">2</span><span class="sxs-lookup"><span data-stu-id="9c8c2-152">2</span></span>                                    |
| <span data-ttu-id="9c8c2-153">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="9c8c2-153">Default Value</span></span>                        | <span data-ttu-id="9c8c2-154">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-154">none</span></span>                                 |
| <span data-ttu-id="9c8c2-155">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-155">Accept Pipeline Input?</span></span>               | <span data-ttu-id="9c8c2-156">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-156">false</span></span>                                |
| <span data-ttu-id="9c8c2-157">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-157">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="9c8c2-158">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-158">false</span></span>                                |

### <a name="-credential-ltpscredentialgt"></a><span data-ttu-id="9c8c2-159">-Credential &lt;PSCredential&gt;</span><span class="sxs-lookup"><span data-stu-id="9c8c2-159">-Credential &lt;PSCredential&gt;</span></span>

<span data-ttu-id="9c8c2-160">Megadja a **PSCredential** egy felhasználói fiókot, amely a Windows PowerShell Web Access engedélyezési szabályok teszteléséhez használni kívánt objektumot.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-160">Specifies a **PSCredential** object for a user account that you want to use to test Windows PowerShell Web Access authorization rules.</span></span> <span data-ttu-id="9c8c2-161">Ha nem adja hozzá ezt a paramétert, a parancsmag használja az aktuálisan bejelentkezett felhasználói fiók.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-161">If you do not add this parameter, the cmdlet uses the currently logged-on user account.</span></span> <span data-ttu-id="9c8c2-162">A beolvasandó egy **PSCredential** objektum, amely pedig szükséges engedélyezési szabályok távolról tesztelése, futtassa a [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-162">To get a **PSCredential** object, which is required to test authorization rules remotely, run the [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936) cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="9c8c2-163">Aliasok</span><span class="sxs-lookup"><span data-stu-id="9c8c2-163">Aliases</span></span>                              | <span data-ttu-id="9c8c2-164">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-164">none</span></span>                                 |
| <span data-ttu-id="9c8c2-165">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-165">Required?</span></span>                            | <span data-ttu-id="9c8c2-166">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-166">false</span></span>                                |
| <span data-ttu-id="9c8c2-167">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-167">Position?</span></span>                            | <span data-ttu-id="9c8c2-168">nevű</span><span class="sxs-lookup"><span data-stu-id="9c8c2-168">named</span></span>                                |
| <span data-ttu-id="9c8c2-169">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="9c8c2-169">Default Value</span></span>                        | <span data-ttu-id="9c8c2-170">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-170">none</span></span>                                 |
| <span data-ttu-id="9c8c2-171">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-171">Accept Pipeline Input?</span></span>               | <span data-ttu-id="9c8c2-172">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-172">false</span></span>                                |
| <span data-ttu-id="9c8c2-173">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-173">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="9c8c2-174">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-174">false</span></span>                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a><span data-ttu-id="9c8c2-175">-Szabály &lt;PswaAuthorizationRule\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="9c8c2-175">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span></span>

<span data-ttu-id="9c8c2-176">Megadja a teszteléséhez szabályok részhalmazát.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-176">Specifies a subset of rules to test.</span></span> <span data-ttu-id="9c8c2-177">Ha ez a paraméter nincs megadva, majd a teszteli, szemben az összes engedélyezési szabályt.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-177">If this parameter is not specified, then this cmdlet tests against all authorization rules.</span></span>

|||  
|-|-|
| <span data-ttu-id="9c8c2-178">Aliasok</span><span class="sxs-lookup"><span data-stu-id="9c8c2-178">Aliases</span></span>                              | <span data-ttu-id="9c8c2-179">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-179">none</span></span>                                 |
| <span data-ttu-id="9c8c2-180">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-180">Required?</span></span>                            | <span data-ttu-id="9c8c2-181">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-181">false</span></span>                                |
| <span data-ttu-id="9c8c2-182">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-182">Position?</span></span>                            | <span data-ttu-id="9c8c2-183">nevű</span><span class="sxs-lookup"><span data-stu-id="9c8c2-183">named</span></span>                                |
| <span data-ttu-id="9c8c2-184">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="9c8c2-184">Default Value</span></span>                        | <span data-ttu-id="9c8c2-185">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-185">none</span></span>                                 |
| <span data-ttu-id="9c8c2-186">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-186">Accept Pipeline Input?</span></span>               | <span data-ttu-id="9c8c2-187">Igaz (ByValue)</span><span class="sxs-lookup"><span data-stu-id="9c8c2-187">True (ByValue)</span></span>                       |
| <span data-ttu-id="9c8c2-188">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-188">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="9c8c2-189">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-189">false</span></span>                                |

### <a name="-username-ltstringgt"></a><span data-ttu-id="9c8c2-190">-UserName &lt;karakterlánc&gt;</span><span class="sxs-lookup"><span data-stu-id="9c8c2-190">-UserName &lt;String&gt;</span></span>

<span data-ttu-id="9c8c2-191">Megadja a tesztelni kívánt felhasználó nevét.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-191">Specifies the name of the user to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="9c8c2-192">Aliasok</span><span class="sxs-lookup"><span data-stu-id="9c8c2-192">Aliases</span></span>                              | <span data-ttu-id="9c8c2-193">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-193">none</span></span>                                 |
| <span data-ttu-id="9c8c2-194">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-194">Required?</span></span>                            | <span data-ttu-id="9c8c2-195">Igaz</span><span class="sxs-lookup"><span data-stu-id="9c8c2-195">true</span></span>                                 |
| <span data-ttu-id="9c8c2-196">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-196">Position?</span></span>                            | <span data-ttu-id="9c8c2-197">1</span><span class="sxs-lookup"><span data-stu-id="9c8c2-197">1</span></span>                                    |
| <span data-ttu-id="9c8c2-198">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="9c8c2-198">Default Value</span></span>                        | <span data-ttu-id="9c8c2-199">nincs</span><span class="sxs-lookup"><span data-stu-id="9c8c2-199">none</span></span>                                 |
| <span data-ttu-id="9c8c2-200">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-200">Accept Pipeline Input?</span></span>               | <span data-ttu-id="9c8c2-201">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-201">false</span></span>                                |
| <span data-ttu-id="9c8c2-202">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="9c8c2-202">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="9c8c2-203">hamis</span><span class="sxs-lookup"><span data-stu-id="9c8c2-203">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="9c8c2-204">&lt;Általánosparaméterek&gt;</span><span class="sxs-lookup"><span data-stu-id="9c8c2-204">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="9c8c2-205">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-205">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="9c8c2-206">További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="9c8c2-206">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="9c8c2-207">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="9c8c2-207">INPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="9c8c2-208">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="9c8c2-208">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="9c8c2-209">Ez a parancsmag PswaAuthorizationRule objektumokból álló tömb fogad el bemenetként.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-209">This cmdlet accepts an array of PswaAuthorizationRule objects as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="9c8c2-210">KIMENETEK</span><span class="sxs-lookup"><span data-stu-id="9c8c2-210">OUTPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="9c8c2-211">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="9c8c2-211">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="9c8c2-212">Ez a parancsmag kimeneteként hoz létre PswaAuthorizationRule objektumokból álló tömb.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-212">This cmdlet produces an array of PswaAuthorizationRule objects as output.</span></span>

## <a name="examples"></a><span data-ttu-id="9c8c2-213">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="9c8c2-213">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="9c8c2-214">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="9c8c2-214">EXAMPLE 1</span></span>

<span data-ttu-id="9c8c2-215">Ebben a példában minden engedélyezési szabályok teszteli a szabályok, amelyek lehetővé teszik a felhasználó megjelenítéséhez *contoso\\mhanson* kapcsolódni a számítógéphez *KISZ2* és a Windows PowerShell-munkamenetet használjon nevű *tesztelése*.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-215">This example tests all authorization rules in order to display all the rules that allow the user *contoso\\mhanson* to connect to the computer *srv2* and use a Windows PowerShell session configuration named *test*.</span></span>

```
Test-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserName contoso\mhanson -ConfigurationName test
```

### <a name="example-2"></a><span data-ttu-id="9c8c2-216">2. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="9c8c2-216">EXAMPLE 2</span></span>

<span data-ttu-id="9c8c2-217">A példa tesztek összes engedélyezési szabályokat, hogy ellenőrizze, melyik engedélyezési szabályok vonatkoznak a felhasználói *contoso\\mhanson*.</span><span class="sxs-lookup"><span data-stu-id="9c8c2-217">This example tests all authorization rules to check which authorization rules apply to the user *contoso\\mhanson*.</span></span>

```
Test-PswaAuthorizationRule -UserName contoso\mhanson -ComputerName *
```

## <a name="related-topics"></a><span data-ttu-id="9c8c2-218">Kapcsolódó témakörök</span><span class="sxs-lookup"><span data-stu-id="9c8c2-218">Related topics</span></span>

- [<span data-ttu-id="9c8c2-219">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="9c8c2-219">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="9c8c2-220">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="9c8c2-220">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="9c8c2-221">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="9c8c2-221">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="9c8c2-222">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="9c8c2-222">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
