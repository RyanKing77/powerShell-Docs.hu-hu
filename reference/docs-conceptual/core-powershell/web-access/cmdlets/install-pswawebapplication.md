---
description: ''
ms.topic: article
ms.prod: powershell
keywords: PowerShell parancsmag
ms.date: 12/12/2016
title: pswawebapplication telepítése
ms.technology: powershell
ms.openlocfilehash: c7f7768a41b6784d8c29afa1fccf0b855160b777
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="install-pswawebapplication"></a><span data-ttu-id="a86ba-103">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="a86ba-103">Install-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="a86ba-104">SYNOPSIS</span><span class="sxs-lookup"><span data-stu-id="a86ba-104">SYNOPSIS</span></span>

<span data-ttu-id="a86ba-105">A Windows PowerShell® Web Access webalkalmazás konfigurálja az IIS-ben.</span><span class="sxs-lookup"><span data-stu-id="a86ba-105">Configures the Windows PowerShell® Web Access web application in IIS.</span></span>

## <a name="syntax"></a><span data-ttu-id="a86ba-106">SZINTAXIS</span><span class="sxs-lookup"><span data-stu-id="a86ba-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="a86ba-107">Alapértelmezett</span><span class="sxs-lookup"><span data-stu-id="a86ba-107">Default</span></span>
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="a86ba-108">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="a86ba-108">DESCRIPTION</span></span>

<span data-ttu-id="a86ba-109">A **Install-PswaWebApplication** parancsmag konfigurálja a Windows PowerShell Web Access webes alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="a86ba-109">The **Install-PswaWebApplication** cmdlet configures Windows PowerShell Web Access web application.</span></span> <span data-ttu-id="a86ba-110">Ez a parancsmag telepíti a webalkalmazás, társítja azt egy webhely, és választhatóan egy teszt SSL tanúsítvány használata a **useTestCertificate** paraméter.</span><span class="sxs-lookup"><span data-stu-id="a86ba-110">This cmdlet installs the web application, associates it with a web site, and optionally creates a test SSL certificate using the **useTestCertificate** parameter.</span></span> <span data-ttu-id="a86ba-111">Biztonsági okokból webes rendszergazdák ne használjon egy teszttanúsítványt éles környezetekben.</span><span class="sxs-lookup"><span data-stu-id="a86ba-111">For security reasons web administrators should not use a test certificate for production environments.</span></span>

## <a name="parameters"></a><span data-ttu-id="a86ba-112">PARAMÉTEREK</span><span class="sxs-lookup"><span data-stu-id="a86ba-112">PARAMETERS</span></span>

### <a name="-usetestcertificate"></a><span data-ttu-id="a86ba-113">-UseTestCertificate</span><span class="sxs-lookup"><span data-stu-id="a86ba-113">-UseTestCertificate</span></span>

<span data-ttu-id="a86ba-114">Meghatározza, hogy létrejött-e egy teszttanúsítványt.</span><span class="sxs-lookup"><span data-stu-id="a86ba-114">Specifies that a test certificate is created.</span></span> <span data-ttu-id="a86ba-115">Ha a paraméter értéke igaz, akkor ez a parancsmag létrehoz egy tesztelési tanúsítványt, és konfigurálja a Windows PowerShell Web Access webalkalmazás használhassa a tanúsítványt a HTTPS-kéréseket.</span><span class="sxs-lookup"><span data-stu-id="a86ba-115">If this parameter is set to true, then this cmdlet creates a test certificate and configures the Windows PowerShell Web Access web application to use the certificate for HTTPS requests.</span></span> <span data-ttu-id="a86ba-116">Ha ez a paraméter false értékre van beállítva, akkor nincs tanúsítvány vagy a kötés jön létre.</span><span class="sxs-lookup"><span data-stu-id="a86ba-116">If this parameter is set to false, then no certificate or binding is created.</span></span> <span data-ttu-id="a86ba-117">Állítsa be ezt az értéket az hamis, ha a Windows PowerShell Web Access egy másik tanúsítvánnyal.</span><span class="sxs-lookup"><span data-stu-id="a86ba-117">Set this value to false if another certificate is used for Windows PowerShell Web Access.</span></span>

|||
|-|-|
| <span data-ttu-id="a86ba-118">Aliasok</span><span class="sxs-lookup"><span data-stu-id="a86ba-118">Aliases</span></span>                              | <span data-ttu-id="a86ba-119">nincs</span><span class="sxs-lookup"><span data-stu-id="a86ba-119">none</span></span>                                 |
| <span data-ttu-id="a86ba-120">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="a86ba-120">Required?</span></span>                            | <span data-ttu-id="a86ba-121">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-121">false</span></span>                                |
| <span data-ttu-id="a86ba-122">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="a86ba-122">Position?</span></span>                            | <span data-ttu-id="a86ba-123">nevű</span><span class="sxs-lookup"><span data-stu-id="a86ba-123">named</span></span>                                |
| <span data-ttu-id="a86ba-124">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="a86ba-124">Default Value</span></span>                        | <span data-ttu-id="a86ba-125">Igaz</span><span class="sxs-lookup"><span data-stu-id="a86ba-125">true</span></span>                                 |
| <span data-ttu-id="a86ba-126">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="a86ba-126">Accept Pipeline Input?</span></span>               | <span data-ttu-id="a86ba-127">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-127">false</span></span>                                |
| <span data-ttu-id="a86ba-128">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="a86ba-128">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="a86ba-129">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-129">false</span></span>                                |

### <a name="-webapplicationnameltstringgt"></a><span data-ttu-id="a86ba-130">-WebApplicationName&lt;String&gt;</span><span class="sxs-lookup"><span data-stu-id="a86ba-130">-WebApplicationName&lt;String&gt;</span></span>

<span data-ttu-id="a86ba-131">Megadja a webalkalmazás nevét.</span><span class="sxs-lookup"><span data-stu-id="a86ba-131">Specifies the name for your web application.</span></span> <span data-ttu-id="a86ba-132">Ez a Windows PowerShell Web Access URL-cím utolsó részeként jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="a86ba-132">This is displayed as the last part of the Windows PowerShell Web Access URL.</span></span>

|||
|-|-|
| <span data-ttu-id="a86ba-133">Aliasok</span><span class="sxs-lookup"><span data-stu-id="a86ba-133">Aliases</span></span>                              | <span data-ttu-id="a86ba-134">nincs</span><span class="sxs-lookup"><span data-stu-id="a86ba-134">none</span></span>                                 |
| <span data-ttu-id="a86ba-135">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="a86ba-135">Required?</span></span>                            | <span data-ttu-id="a86ba-136">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-136">false</span></span>                                |
| <span data-ttu-id="a86ba-137">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="a86ba-137">Position?</span></span>                            | <span data-ttu-id="a86ba-138">1</span><span class="sxs-lookup"><span data-stu-id="a86ba-138">1</span></span>                                    |
| <span data-ttu-id="a86ba-139">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="a86ba-139">Default Value</span></span>                        | <span data-ttu-id="a86ba-140">pswa</span><span class="sxs-lookup"><span data-stu-id="a86ba-140">pswa</span></span>                                 |
| <span data-ttu-id="a86ba-141">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="a86ba-141">Accept Pipeline Input?</span></span>               | <span data-ttu-id="a86ba-142">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-142">false</span></span>                                |
| <span data-ttu-id="a86ba-143">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="a86ba-143">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="a86ba-144">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-144">false</span></span>                                |

### <a name="-websitenameltstringgt"></a><span data-ttu-id="a86ba-145">-WebSiteName&lt;String&gt;</span><span class="sxs-lookup"><span data-stu-id="a86ba-145">-WebSiteName&lt;String&gt;</span></span>

<span data-ttu-id="a86ba-146">Adja meg a webkiszolgáló (IIS) webhely telepítéséhez a Windows PowerShell Web Access webes alkalmazás neve.</span><span class="sxs-lookup"><span data-stu-id="a86ba-146">Specifies the name of the Web Server (IIS) website on which to install this Windows PowerShell Web Access web application.</span></span>

|||
|-|-|
| <span data-ttu-id="a86ba-147">Aliasok</span><span class="sxs-lookup"><span data-stu-id="a86ba-147">Aliases</span></span>                              | <span data-ttu-id="a86ba-148">nincs</span><span class="sxs-lookup"><span data-stu-id="a86ba-148">none</span></span>                                 |
| <span data-ttu-id="a86ba-149">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="a86ba-149">Required?</span></span>                            | <span data-ttu-id="a86ba-150">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-150">false</span></span>                                |
| <span data-ttu-id="a86ba-151">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="a86ba-151">Position?</span></span>                            | <span data-ttu-id="a86ba-152">nevű</span><span class="sxs-lookup"><span data-stu-id="a86ba-152">named</span></span>                                |
| <span data-ttu-id="a86ba-153">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="a86ba-153">Default Value</span></span>                        | <span data-ttu-id="a86ba-154">Alapértelmezett webhely</span><span class="sxs-lookup"><span data-stu-id="a86ba-154">Default Web Site</span></span>                     |
| <span data-ttu-id="a86ba-155">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="a86ba-155">Accept Pipeline Input?</span></span>               | <span data-ttu-id="a86ba-156">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-156">false</span></span>                                |
| <span data-ttu-id="a86ba-157">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="a86ba-157">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="a86ba-158">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-158">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="a86ba-159">-Confirm</span><span class="sxs-lookup"><span data-stu-id="a86ba-159">-Confirm</span></span>

<span data-ttu-id="a86ba-160">Jóváhagyást kér a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="a86ba-160">Prompts you for confirmation before running the cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="a86ba-161">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="a86ba-161">Required?</span></span>                            | <span data-ttu-id="a86ba-162">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-162">false</span></span>                                |
| <span data-ttu-id="a86ba-163">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="a86ba-163">Position?</span></span>                            | <span data-ttu-id="a86ba-164">nevű</span><span class="sxs-lookup"><span data-stu-id="a86ba-164">named</span></span>                                |
| <span data-ttu-id="a86ba-165">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="a86ba-165">Default Value</span></span>                        | <span data-ttu-id="a86ba-166">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-166">false</span></span>                                |
| <span data-ttu-id="a86ba-167">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="a86ba-167">Accept Pipeline Input?</span></span>               | <span data-ttu-id="a86ba-168">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-168">false</span></span>                                |
| <span data-ttu-id="a86ba-169">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="a86ba-169">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="a86ba-170">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-170">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="a86ba-171">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="a86ba-171">-WhatIf</span></span>

<span data-ttu-id="a86ba-172">Bemutatja, mi történne a parancsmag futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="a86ba-172">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="a86ba-173">A parancsmag nem fut.</span><span class="sxs-lookup"><span data-stu-id="a86ba-173">The cmdlet is not run.</span></span>

|||
|-|-|
| <span data-ttu-id="a86ba-174">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="a86ba-174">Required?</span></span>                            | <span data-ttu-id="a86ba-175">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-175">false</span></span>                                |
| <span data-ttu-id="a86ba-176">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="a86ba-176">Position?</span></span>                            | <span data-ttu-id="a86ba-177">nevű</span><span class="sxs-lookup"><span data-stu-id="a86ba-177">named</span></span>                                |
| <span data-ttu-id="a86ba-178">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="a86ba-178">Default Value</span></span>                        | <span data-ttu-id="a86ba-179">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-179">false</span></span>                                |
| <span data-ttu-id="a86ba-180">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="a86ba-180">Accept Pipeline Input?</span></span>               | <span data-ttu-id="a86ba-181">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-181">false</span></span>                                |
| <span data-ttu-id="a86ba-182">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="a86ba-182">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="a86ba-183">hamis</span><span class="sxs-lookup"><span data-stu-id="a86ba-183">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="a86ba-184">&lt;Általánosparaméterek&gt;</span><span class="sxs-lookup"><span data-stu-id="a86ba-184">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="a86ba-185">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="a86ba-185">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="a86ba-186">További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="a86ba-186">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="a86ba-187">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="a86ba-187">INPUTS</span></span>

<span data-ttu-id="a86ba-188">Ez a parancsmag nem bemenetből fogad adatokat.</span><span class="sxs-lookup"><span data-stu-id="a86ba-188">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="a86ba-189">KIMENETEK</span><span class="sxs-lookup"><span data-stu-id="a86ba-189">OUTPUTS</span></span>

<span data-ttu-id="a86ba-190">Ez a parancsmag nem kimenetet hoz létre.</span><span class="sxs-lookup"><span data-stu-id="a86ba-190">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="a86ba-191">EXAMPLES</span><span class="sxs-lookup"><span data-stu-id="a86ba-191">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="a86ba-192">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="a86ba-192">EXAMPLE 1</span></span>

<span data-ttu-id="a86ba-193">Ebben a példában a PSWA webes alkalmazás alapértelmezett értékeinek használatával telepíti a **WebApplicationName** (*pswa*) és **WebSiteName** (*alapértelmezett webhelyen* ) paraméterek.</span><span class="sxs-lookup"><span data-stu-id="a86ba-193">This example installs the PSWA web application using the default values for the **WebApplicationName** (*pswa*) and **WebSiteName** (*Default Web Site*) parameters .</span></span>

```
Install-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="a86ba-194">2. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="a86ba-194">EXAMPLE 2</span></span>

<span data-ttu-id="a86ba-195">Ebben a példában a PSWA webalkalmazás telepíti egy teszttanúsítványt, és az alapértelmezett értékeit használatával a **WebApplicationName** és **WebSiteName** paraméterek.</span><span class="sxs-lookup"><span data-stu-id="a86ba-195">This example installs the PSWA web application with a test certificate, and using the default values for the **WebApplicationName** and **WebSiteName** parameters.</span></span>

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="a86ba-196">Kapcsolódó témakörök</span><span class="sxs-lookup"><span data-stu-id="a86ba-196">Related topics</span></span>

- [<span data-ttu-id="a86ba-197">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="a86ba-197">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="a86ba-198">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="a86ba-198">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="a86ba-199">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="a86ba-199">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="a86ba-200">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="a86ba-200">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)