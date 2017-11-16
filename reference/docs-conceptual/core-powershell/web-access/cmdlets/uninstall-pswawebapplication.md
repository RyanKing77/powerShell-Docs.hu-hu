---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: PowerShell parancsmag
ms.date: 2016-12-12
title: "Távolítsa el a pswawebapplication"
ms.technology: powershell
ms.openlocfilehash: 5fe608b3bfbb90f842f16c1f5a8c51879589cf6d
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="uninstall-pswawebapplication"></a><span data-ttu-id="a86a3-103">Távolítsa el PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="a86a3-103">Uninstall-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="a86a3-104">ÖSSZEGZÉST</span><span class="sxs-lookup"><span data-stu-id="a86a3-104">SYNOPSIS</span></span>

<span data-ttu-id="a86a3-105">Eltávolítja a Windows PowerShell® webalkalmazás.</span><span class="sxs-lookup"><span data-stu-id="a86a3-105">Uninstalls the Windows PowerShell® web application.</span></span>

## <a name="syntax"></a><span data-ttu-id="a86a3-106">SZINTAXIS</span><span class="sxs-lookup"><span data-stu-id="a86a3-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="a86a3-107">Alapértelmezett</span><span class="sxs-lookup"><span data-stu-id="a86a3-107">Default</span></span>
```
Uninstall-PswaWebApplication [[-WebApplicationName] <String> ] [-DeleteTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="a86a3-108">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="a86a3-108">DESCRIPTION</span></span>

<span data-ttu-id="a86a3-109">A **Uninstall-PswaWebApplication** parancsmag eltávolítja a Windows PowerShell-webalkalmazáshoz, és eltávolítja a webhely az IIS.</span><span class="sxs-lookup"><span data-stu-id="a86a3-109">The **Uninstall-PswaWebApplication** cmdlet uninstalls the Windows PowerShell web application and removes the website from IIS.</span></span> <span data-ttu-id="a86a3-110">A parancsmag nem távolítja el az IIS vagy bármely más, mert nem voltak Windows PowerShell futtatásához szükséges telepített szolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="a86a3-110">The cmdlet does not uninstall IIS, or any other features installed because they were required for Windows PowerShell to run.</span></span>

## <a name="parameters"></a><span data-ttu-id="a86a3-111">PARAMÉTEREK</span><span class="sxs-lookup"><span data-stu-id="a86a3-111">PARAMETERS</span></span>

### <a name="-deletetestcertificate"></a><span data-ttu-id="a86a3-112">-DeleteTestCertificate</span><span class="sxs-lookup"><span data-stu-id="a86a3-112">-DeleteTestCertificate</span></span>

<span data-ttu-id="a86a3-113">Azt jelzi, hogy a teszt tanúsítványok által a **telepítése\_PswaWebApplication** parancsmag (az a **UseTestCertificate** paraméter) törlődik.</span><span class="sxs-lookup"><span data-stu-id="a86a3-113">Indicates that the test certificates created by the **Install\_PswaWebApplication** cmdlet (with the **UseTestCertificate** parameter) is deleted.</span></span>
<span data-ttu-id="a86a3-114">Csak a tanúsítvány azonos nevű megegyezik a hozta létre a **Install-PswaWebApplication** parancsmag törlődik.</span><span class="sxs-lookup"><span data-stu-id="a86a3-114">Only the test certificate with the same name as the one created by the **Install-PswaWebApplication** cmdlet is removed.</span></span>

|||  
|-|-|
| <span data-ttu-id="a86a3-115">Aliasok</span><span class="sxs-lookup"><span data-stu-id="a86a3-115">Aliases</span></span>                              | <span data-ttu-id="a86a3-116">nincs</span><span class="sxs-lookup"><span data-stu-id="a86a3-116">none</span></span>                                 |
| <span data-ttu-id="a86a3-117">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="a86a3-117">Required?</span></span>                            | <span data-ttu-id="a86a3-118">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-118">false</span></span>                                |
| <span data-ttu-id="a86a3-119">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="a86a3-119">Position?</span></span>                            | <span data-ttu-id="a86a3-120">nevű</span><span class="sxs-lookup"><span data-stu-id="a86a3-120">named</span></span>                                |
| <span data-ttu-id="a86a3-121">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="a86a3-121">Default Value</span></span>                        | <span data-ttu-id="a86a3-122">Igaz</span><span class="sxs-lookup"><span data-stu-id="a86a3-122">true</span></span>                                 |
| <span data-ttu-id="a86a3-123">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="a86a3-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="a86a3-124">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-124">false</span></span>                                |
| <span data-ttu-id="a86a3-125">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="a86a3-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="a86a3-126">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-126">false</span></span>                                |

### <a name="-webapplicationname-ltstringgt"></a><span data-ttu-id="a86a3-127">-WebApplicationName &lt;karakterlánc&gt;</span><span class="sxs-lookup"><span data-stu-id="a86a3-127">-WebApplicationName &lt;String&gt;</span></span>

<span data-ttu-id="a86a3-128">A webes alkalmazás eltávolítása a nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="a86a3-128">Specifies the name of the web application to uninstall.</span></span>

|||  
|-|-|
| <span data-ttu-id="a86a3-129">Aliasok</span><span class="sxs-lookup"><span data-stu-id="a86a3-129">Aliases</span></span>                              | <span data-ttu-id="a86a3-130">nincs</span><span class="sxs-lookup"><span data-stu-id="a86a3-130">none</span></span>                                 |
| <span data-ttu-id="a86a3-131">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="a86a3-131">Required?</span></span>                            | <span data-ttu-id="a86a3-132">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-132">false</span></span>                                |
| <span data-ttu-id="a86a3-133">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="a86a3-133">Position?</span></span>                            | <span data-ttu-id="a86a3-134">1</span><span class="sxs-lookup"><span data-stu-id="a86a3-134">1</span></span>                                    |
| <span data-ttu-id="a86a3-135">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="a86a3-135">Default Value</span></span>                        | <span data-ttu-id="a86a3-136">pswa</span><span class="sxs-lookup"><span data-stu-id="a86a3-136">pswa</span></span>                                 |
| <span data-ttu-id="a86a3-137">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="a86a3-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="a86a3-138">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-138">false</span></span>                                |
| <span data-ttu-id="a86a3-139">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="a86a3-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="a86a3-140">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-140">false</span></span>                                |

### <a name="-websitename-ltstringgt"></a><span data-ttu-id="a86a3-141">-WebSiteName &lt;karakterlánc&gt;</span><span class="sxs-lookup"><span data-stu-id="a86a3-141">-WebSiteName &lt;String&gt;</span></span>

<span data-ttu-id="a86a3-142">Megadja a nevét, a webhely, ahol a webes alkalmazás telepítve van.</span><span class="sxs-lookup"><span data-stu-id="a86a3-142">Specifies the name of the web site where the web application is installed.</span></span>

|||  
|-|-|
| <span data-ttu-id="a86a3-143">Aliasok</span><span class="sxs-lookup"><span data-stu-id="a86a3-143">Aliases</span></span>                              | <span data-ttu-id="a86a3-144">nincs</span><span class="sxs-lookup"><span data-stu-id="a86a3-144">none</span></span>                                 |
| <span data-ttu-id="a86a3-145">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="a86a3-145">Required?</span></span>                            | <span data-ttu-id="a86a3-146">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-146">false</span></span>                                |
| <span data-ttu-id="a86a3-147">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="a86a3-147">Position?</span></span>                            | <span data-ttu-id="a86a3-148">nevű</span><span class="sxs-lookup"><span data-stu-id="a86a3-148">named</span></span>                                |
| <span data-ttu-id="a86a3-149">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="a86a3-149">Default Value</span></span>                        | <span data-ttu-id="a86a3-150">Alapértelmezett webhely</span><span class="sxs-lookup"><span data-stu-id="a86a3-150">Default Web Site</span></span>                     |
| <span data-ttu-id="a86a3-151">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="a86a3-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="a86a3-152">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-152">false</span></span>                                |
| <span data-ttu-id="a86a3-153">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="a86a3-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="a86a3-154">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="a86a3-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="a86a3-155">-Confirm</span></span>

<span data-ttu-id="a86a3-156">Jóváhagyást kér a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="a86a3-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="a86a3-157">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="a86a3-157">Required?</span></span>                            | <span data-ttu-id="a86a3-158">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-158">false</span></span>                                |
| <span data-ttu-id="a86a3-159">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="a86a3-159">Position?</span></span>                            | <span data-ttu-id="a86a3-160">nevű</span><span class="sxs-lookup"><span data-stu-id="a86a3-160">named</span></span>                                |
| <span data-ttu-id="a86a3-161">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="a86a3-161">Default Value</span></span>                        | <span data-ttu-id="a86a3-162">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-162">false</span></span>                                |
| <span data-ttu-id="a86a3-163">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="a86a3-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="a86a3-164">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-164">false</span></span>                                |
| <span data-ttu-id="a86a3-165">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="a86a3-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="a86a3-166">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="a86a3-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="a86a3-167">-WhatIf</span></span>

<span data-ttu-id="a86a3-168">Bemutatja, mi történne a parancsmag futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="a86a3-168">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="a86a3-169">A parancsmag nem fut.</span><span class="sxs-lookup"><span data-stu-id="a86a3-169">The cmdlet is not run.</span></span>

|||  
|-|-|
| <span data-ttu-id="a86a3-170">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="a86a3-170">Required?</span></span>                            | <span data-ttu-id="a86a3-171">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-171">false</span></span>                                |
| <span data-ttu-id="a86a3-172">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="a86a3-172">Position?</span></span>                            | <span data-ttu-id="a86a3-173">nevű</span><span class="sxs-lookup"><span data-stu-id="a86a3-173">named</span></span>                                |
| <span data-ttu-id="a86a3-174">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="a86a3-174">Default Value</span></span>                        | <span data-ttu-id="a86a3-175">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-175">false</span></span>                                |
| <span data-ttu-id="a86a3-176">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="a86a3-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="a86a3-177">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-177">false</span></span>                                |
| <span data-ttu-id="a86a3-178">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="a86a3-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="a86a3-179">hamis</span><span class="sxs-lookup"><span data-stu-id="a86a3-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="a86a3-180">&lt;Általánosparaméterek&gt;</span><span class="sxs-lookup"><span data-stu-id="a86a3-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="a86a3-181">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="a86a3-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="a86a3-182">További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="a86a3-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="a86a3-183">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="a86a3-183">INPUTS</span></span>

<span data-ttu-id="a86a3-184">Ez a parancsmag nem bemenetből fogad adatokat.</span><span class="sxs-lookup"><span data-stu-id="a86a3-184">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="a86a3-185">KIMENETEK</span><span class="sxs-lookup"><span data-stu-id="a86a3-185">OUTPUTS</span></span>

<span data-ttu-id="a86a3-186">Ez a parancsmag nem-kimenet visszaadása.</span><span class="sxs-lookup"><span data-stu-id="a86a3-186">This cmdlet returns no output.</span></span>

## <a name="examples"></a><span data-ttu-id="a86a3-187">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="a86a3-187">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="a86a3-188">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="a86a3-188">EXAMPLE 1</span></span>

<span data-ttu-id="a86a3-189">Ez a parancs eltávolítja a Windows PowerShell webalkalmazás.</span><span class="sxs-lookup"><span data-stu-id="a86a3-189">This command uninstalls the Windows PowerShell Web Application.</span></span>
<span data-ttu-id="a86a3-190">Ez a parancsmag segítségével távolítsa el a Windows PowerShell webalkalmazás, ha telepítette az alapértelmezett értékekkel.</span><span class="sxs-lookup"><span data-stu-id="a86a3-190">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values.</span></span>

```PowerShell
Uninstall-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="a86a3-191">2. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="a86a3-191">EXAMPLE 2</span></span>

<span data-ttu-id="a86a3-192">A parancs eltávolítja a Windows PowerShell webalkalmazás, és törli az alkalmazáshoz kapcsolódó teszttanúsítványt.</span><span class="sxs-lookup"><span data-stu-id="a86a3-192">This command uninstalls the Windows PowerShell Web Application, and deletes the test certificate associated with the application.</span></span>
<span data-ttu-id="a86a3-193">Ez a parancsmag segítségével távolítsa el a Windows PowerShell webalkalmazás, ha telepítették őket az alapértelmezett értékekkel, és létrehozott egy teszttanúsítványt.</span><span class="sxs-lookup"><span data-stu-id="a86a3-193">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values and created a test certificate.</span></span>

```PowerShell
Uninstall-PswaWebApplication -DeleteTestCertificate
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="a86a3-194">{#Example-3 .subHeading} 3. példa</span><span class="sxs-lookup"><span data-stu-id="a86a3-194">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="a86a3-195">Ez a parancs eltávolítja a Windows PowerShell webalkalmazás, ha egy egyéni webhelyet és alkalmazást a telepítés során megadott.</span><span class="sxs-lookup"><span data-stu-id="a86a3-195">This command uninstalls the Windows PowerShell Web Application when a custom website and application were specified during the install.</span></span>
<span data-ttu-id="a86a3-196">A parancs eltávolítja a webhely nevű *saját webhely* és a nevű alkalmazást *Tesztalkalmazás kategóriában* és megadja, hogy a teszt tanúsítványokat, az alkalmazással társított is törlődnek.</span><span class="sxs-lookup"><span data-stu-id="a86a3-196">The command removes the website named *MySite* and the application named *TestApplication* and specifies that the test certificates associated with the application are also deleted.</span></span>

```
Uninstall-PswaWebApplication -WebApplicationName TestApplication -WebsiteName MySite -DeleteTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="a86a3-197">Kapcsolódó témakörök</span><span class="sxs-lookup"><span data-stu-id="a86a3-197">Related topics</span></span>

- [<span data-ttu-id="a86a3-198">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="a86a3-198">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="a86a3-199">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="a86a3-199">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="a86a3-200">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="a86a3-200">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="a86a3-201">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="a86a3-201">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="a86a3-202">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="a86a3-202">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
