---
ms.topic: reference
keywords: PowerShell parancsmag
ms.date: 12/12/2016
title: Távolítsa el PswaWebApplication
ms.openlocfilehash: b2a3e4d584fd04ee49e1e6408dba39fd8bc555dc
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34221918"
---
# <a name="uninstall-pswawebapplication"></a><span data-ttu-id="8e4d0-103">Távolítsa el PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="8e4d0-103">Uninstall-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="8e4d0-104">ÖSSZEGZÉST</span><span class="sxs-lookup"><span data-stu-id="8e4d0-104">SYNOPSIS</span></span>

<span data-ttu-id="8e4d0-105">Eltávolítja a Windows PowerShell® webalkalmazás.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-105">Uninstalls the Windows PowerShell® web application.</span></span>

## <a name="syntax"></a><span data-ttu-id="8e4d0-106">SZINTAXIS</span><span class="sxs-lookup"><span data-stu-id="8e4d0-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="8e4d0-107">Alapértelmezett</span><span class="sxs-lookup"><span data-stu-id="8e4d0-107">Default</span></span>
```
Uninstall-PswaWebApplication [[-WebApplicationName] <String> ] [-DeleteTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="8e4d0-108">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="8e4d0-108">DESCRIPTION</span></span>

<span data-ttu-id="8e4d0-109">A **Uninstall-PswaWebApplication** parancsmag eltávolítja a Windows PowerShell-webalkalmazáshoz, és eltávolítja a webhely az IIS.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-109">The **Uninstall-PswaWebApplication** cmdlet uninstalls the Windows PowerShell web application and removes the website from IIS.</span></span> <span data-ttu-id="8e4d0-110">A parancsmag nem távolítja el az IIS vagy bármely más, mert nem voltak Windows PowerShell futtatásához szükséges telepített szolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-110">The cmdlet does not uninstall IIS, or any other features installed because they were required for Windows PowerShell to run.</span></span>

## <a name="parameters"></a><span data-ttu-id="8e4d0-111">PARAMÉTEREK</span><span class="sxs-lookup"><span data-stu-id="8e4d0-111">PARAMETERS</span></span>

### <a name="-deletetestcertificate"></a><span data-ttu-id="8e4d0-112">-DeleteTestCertificate</span><span class="sxs-lookup"><span data-stu-id="8e4d0-112">-DeleteTestCertificate</span></span>

<span data-ttu-id="8e4d0-113">Azt jelzi, hogy a teszt tanúsítványok által a **telepítése\_PswaWebApplication** parancsmag (az a **UseTestCertificate** paraméter) törlődik.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-113">Indicates that the test certificates created by the **Install\_PswaWebApplication** cmdlet (with the **UseTestCertificate** parameter) is deleted.</span></span>
<span data-ttu-id="8e4d0-114">Csak a tanúsítvány azonos nevű megegyezik a hozta létre a **Install-PswaWebApplication** parancsmag törlődik.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-114">Only the test certificate with the same name as the one created by the **Install-PswaWebApplication** cmdlet is removed.</span></span>

|||
|-|-|
| <span data-ttu-id="8e4d0-115">Aliasok</span><span class="sxs-lookup"><span data-stu-id="8e4d0-115">Aliases</span></span>                              | <span data-ttu-id="8e4d0-116">nincs</span><span class="sxs-lookup"><span data-stu-id="8e4d0-116">none</span></span>                                 |
| <span data-ttu-id="8e4d0-117">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-117">Required?</span></span>                            | <span data-ttu-id="8e4d0-118">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-118">false</span></span>                                |
| <span data-ttu-id="8e4d0-119">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-119">Position?</span></span>                            | <span data-ttu-id="8e4d0-120">nevű</span><span class="sxs-lookup"><span data-stu-id="8e4d0-120">named</span></span>                                |
| <span data-ttu-id="8e4d0-121">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="8e4d0-121">Default Value</span></span>                        | <span data-ttu-id="8e4d0-122">Igaz</span><span class="sxs-lookup"><span data-stu-id="8e4d0-122">true</span></span>                                 |
| <span data-ttu-id="8e4d0-123">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="8e4d0-124">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-124">false</span></span>                                |
| <span data-ttu-id="8e4d0-125">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="8e4d0-126">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-126">false</span></span>                                |

### <a name="-webapplicationname-ltstringgt"></a><span data-ttu-id="8e4d0-127">-WebApplicationName &lt;karakterlánc&gt;</span><span class="sxs-lookup"><span data-stu-id="8e4d0-127">-WebApplicationName &lt;String&gt;</span></span>

<span data-ttu-id="8e4d0-128">A webes alkalmazás eltávolítása a nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-128">Specifies the name of the web application to uninstall.</span></span>

|||
|-|-|
| <span data-ttu-id="8e4d0-129">Aliasok</span><span class="sxs-lookup"><span data-stu-id="8e4d0-129">Aliases</span></span>                              | <span data-ttu-id="8e4d0-130">nincs</span><span class="sxs-lookup"><span data-stu-id="8e4d0-130">none</span></span>                                 |
| <span data-ttu-id="8e4d0-131">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-131">Required?</span></span>                            | <span data-ttu-id="8e4d0-132">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-132">false</span></span>                                |
| <span data-ttu-id="8e4d0-133">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-133">Position?</span></span>                            | <span data-ttu-id="8e4d0-134">1</span><span class="sxs-lookup"><span data-stu-id="8e4d0-134">1</span></span>                                    |
| <span data-ttu-id="8e4d0-135">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="8e4d0-135">Default Value</span></span>                        | <span data-ttu-id="8e4d0-136">pswa</span><span class="sxs-lookup"><span data-stu-id="8e4d0-136">pswa</span></span>                                 |
| <span data-ttu-id="8e4d0-137">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="8e4d0-138">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-138">false</span></span>                                |
| <span data-ttu-id="8e4d0-139">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="8e4d0-140">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-140">false</span></span>                                |

### <a name="-websitename-ltstringgt"></a><span data-ttu-id="8e4d0-141">-WebSiteName &lt;karakterlánc&gt;</span><span class="sxs-lookup"><span data-stu-id="8e4d0-141">-WebSiteName &lt;String&gt;</span></span>

<span data-ttu-id="8e4d0-142">Megadja a nevét, a webhely, ahol a webes alkalmazás telepítve van.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-142">Specifies the name of the web site where the web application is installed.</span></span>

|||
|-|-|
| <span data-ttu-id="8e4d0-143">Aliasok</span><span class="sxs-lookup"><span data-stu-id="8e4d0-143">Aliases</span></span>                              | <span data-ttu-id="8e4d0-144">nincs</span><span class="sxs-lookup"><span data-stu-id="8e4d0-144">none</span></span>                                 |
| <span data-ttu-id="8e4d0-145">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-145">Required?</span></span>                            | <span data-ttu-id="8e4d0-146">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-146">false</span></span>                                |
| <span data-ttu-id="8e4d0-147">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-147">Position?</span></span>                            | <span data-ttu-id="8e4d0-148">nevű</span><span class="sxs-lookup"><span data-stu-id="8e4d0-148">named</span></span>                                |
| <span data-ttu-id="8e4d0-149">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="8e4d0-149">Default Value</span></span>                        | <span data-ttu-id="8e4d0-150">Alapértelmezett webhely</span><span class="sxs-lookup"><span data-stu-id="8e4d0-150">Default Web Site</span></span>                     |
| <span data-ttu-id="8e4d0-151">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="8e4d0-152">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-152">false</span></span>                                |
| <span data-ttu-id="8e4d0-153">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="8e4d0-154">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="8e4d0-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="8e4d0-155">-Confirm</span></span>

<span data-ttu-id="8e4d0-156">Jóváhagyást kér a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="8e4d0-157">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-157">Required?</span></span>                            | <span data-ttu-id="8e4d0-158">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-158">false</span></span>                                |
| <span data-ttu-id="8e4d0-159">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-159">Position?</span></span>                            | <span data-ttu-id="8e4d0-160">nevű</span><span class="sxs-lookup"><span data-stu-id="8e4d0-160">named</span></span>                                |
| <span data-ttu-id="8e4d0-161">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="8e4d0-161">Default Value</span></span>                        | <span data-ttu-id="8e4d0-162">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-162">false</span></span>                                |
| <span data-ttu-id="8e4d0-163">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="8e4d0-164">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-164">false</span></span>                                |
| <span data-ttu-id="8e4d0-165">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="8e4d0-166">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="8e4d0-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="8e4d0-167">-WhatIf</span></span>

<span data-ttu-id="8e4d0-168">Bemutatja, mi történne a parancsmag futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-168">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="8e4d0-169">A parancsmag nem fut.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-169">The cmdlet is not run.</span></span>

|||
|-|-|
| <span data-ttu-id="8e4d0-170">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-170">Required?</span></span>                            | <span data-ttu-id="8e4d0-171">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-171">false</span></span>                                |
| <span data-ttu-id="8e4d0-172">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-172">Position?</span></span>                            | <span data-ttu-id="8e4d0-173">nevű</span><span class="sxs-lookup"><span data-stu-id="8e4d0-173">named</span></span>                                |
| <span data-ttu-id="8e4d0-174">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="8e4d0-174">Default Value</span></span>                        | <span data-ttu-id="8e4d0-175">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-175">false</span></span>                                |
| <span data-ttu-id="8e4d0-176">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="8e4d0-177">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-177">false</span></span>                                |
| <span data-ttu-id="8e4d0-178">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="8e4d0-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="8e4d0-179">hamis</span><span class="sxs-lookup"><span data-stu-id="8e4d0-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="8e4d0-180">&lt;Általánosparaméterek&gt;</span><span class="sxs-lookup"><span data-stu-id="8e4d0-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="8e4d0-181">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="8e4d0-182">További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="8e4d0-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="8e4d0-183">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="8e4d0-183">INPUTS</span></span>

<span data-ttu-id="8e4d0-184">Ez a parancsmag nem bemenetből fogad adatokat.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-184">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="8e4d0-185">KIMENETEK</span><span class="sxs-lookup"><span data-stu-id="8e4d0-185">OUTPUTS</span></span>

<span data-ttu-id="8e4d0-186">Ez a parancsmag nem-kimenet visszaadása.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-186">This cmdlet returns no output.</span></span>

## <a name="examples"></a><span data-ttu-id="8e4d0-187">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="8e4d0-187">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="8e4d0-188">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="8e4d0-188">EXAMPLE 1</span></span>

<span data-ttu-id="8e4d0-189">Ez a parancs eltávolítja a Windows PowerShell webalkalmazás.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-189">This command uninstalls the Windows PowerShell Web Application.</span></span>
<span data-ttu-id="8e4d0-190">Ez a parancsmag segítségével távolítsa el a Windows PowerShell webalkalmazás, ha telepítette az alapértelmezett értékekkel.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-190">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values.</span></span>

```PowerShell
Uninstall-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="8e4d0-191">2. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="8e4d0-191">EXAMPLE 2</span></span>

<span data-ttu-id="8e4d0-192">A parancs eltávolítja a Windows PowerShell webalkalmazás, és törli az alkalmazáshoz kapcsolódó teszttanúsítványt.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-192">This command uninstalls the Windows PowerShell Web Application, and deletes the test certificate associated with the application.</span></span>
<span data-ttu-id="8e4d0-193">Ez a parancsmag segítségével távolítsa el a Windows PowerShell webalkalmazás, ha telepítették őket az alapértelmezett értékekkel, és létrehozott egy teszttanúsítványt.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-193">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values and created a test certificate.</span></span>

```PowerShell
Uninstall-PswaWebApplication -DeleteTestCertificate
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="8e4d0-194">{#Example-3 .subHeading} 3. példa</span><span class="sxs-lookup"><span data-stu-id="8e4d0-194">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="8e4d0-195">Ez a parancs eltávolítja a Windows PowerShell webalkalmazás, ha egy egyéni webhelyet és alkalmazást a telepítés során megadott.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-195">This command uninstalls the Windows PowerShell Web Application when a custom website and application were specified during the install.</span></span>
<span data-ttu-id="8e4d0-196">A parancs eltávolítja a webhely nevű *saját webhely* és a nevű alkalmazást *Tesztalkalmazás kategóriában* és megadja, hogy a teszt tanúsítványokat, az alkalmazással társított is törlődnek.</span><span class="sxs-lookup"><span data-stu-id="8e4d0-196">The command removes the website named *MySite* and the application named *TestApplication* and specifies that the test certificates associated with the application are also deleted.</span></span>

```
Uninstall-PswaWebApplication -WebApplicationName TestApplication -WebsiteName MySite -DeleteTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="8e4d0-197">Kapcsolódó témakörök</span><span class="sxs-lookup"><span data-stu-id="8e4d0-197">Related topics</span></span>

- [<span data-ttu-id="8e4d0-198">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="8e4d0-198">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="8e4d0-199">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="8e4d0-199">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="8e4d0-200">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="8e4d0-200">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="8e4d0-201">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="8e4d0-201">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="8e4d0-202">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="8e4d0-202">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)