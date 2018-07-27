---
ms.topic: reference
keywords: PowerShell, a parancsmag
ms.date: 12/12/2016
title: Install-PswaWebApplication
ms.openlocfilehash: 29e074b75eeb387640831229c63142e6dd5e991a
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268299"
---
# <a name="install-pswawebapplication"></a><span data-ttu-id="56fe4-103">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="56fe4-103">Install-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="56fe4-104">SYNOPSIS</span><span class="sxs-lookup"><span data-stu-id="56fe4-104">SYNOPSIS</span></span>

<span data-ttu-id="56fe4-105">Konfigurálja a Windows PowerShell-elérés webes alkalmazást az IIS-ben.</span><span class="sxs-lookup"><span data-stu-id="56fe4-105">Configures the Windows PowerShell Web Access web application in IIS.</span></span>

## <a name="syntax"></a><span data-ttu-id="56fe4-106">SZINTAXIS</span><span class="sxs-lookup"><span data-stu-id="56fe4-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="56fe4-107">Alapértelmezett</span><span class="sxs-lookup"><span data-stu-id="56fe4-107">Default</span></span>
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="56fe4-108">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="56fe4-108">DESCRIPTION</span></span>

<span data-ttu-id="56fe4-109">A **Install-PswaWebApplication** parancsmag konfigurálja a Windows PowerShell-elérés webes alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="56fe4-109">The **Install-PswaWebApplication** cmdlet configures Windows PowerShell Web Access web application.</span></span>
<span data-ttu-id="56fe4-110">Ez a parancsmag telepíti a webalkalmazás, hozzárendeli egy webhely, és igény szerint létrehoz egy tesztelési SSL tanúsítvány használatával a **useTestCertificate** paraméter.</span><span class="sxs-lookup"><span data-stu-id="56fe4-110">This cmdlet installs the web application, associates it with a web site, and optionally creates a test SSL certificate using the **useTestCertificate** parameter.</span></span> <span data-ttu-id="56fe4-111">Biztonsági okokból a webes rendszergazdák ne használjon egy tesztcélú tanúsítvánnyal az éles környezetekhez.</span><span class="sxs-lookup"><span data-stu-id="56fe4-111">For security reasons web administrators should not use a test certificate for production environments.</span></span>

## <a name="parameters"></a><span data-ttu-id="56fe4-112">PARAMÉTEREK</span><span class="sxs-lookup"><span data-stu-id="56fe4-112">PARAMETERS</span></span>

### <a name="-usetestcertificate"></a><span data-ttu-id="56fe4-113">-UseTestCertificate</span><span class="sxs-lookup"><span data-stu-id="56fe4-113">-UseTestCertificate</span></span>

<span data-ttu-id="56fe4-114">Megadja, hogy létrejött-e egy tesztcélú tanúsítvánnyal.</span><span class="sxs-lookup"><span data-stu-id="56fe4-114">Specifies that a test certificate is created.</span></span> <span data-ttu-id="56fe4-115">Ha ez a paraméter értéke true, akkor ez a parancsmag létrehoz egy tesztcélú tanúsítvánnyal, és konfigurálja a tanúsítványt használja a HTTPS-kéréseket a Windows PowerShell-elérés webes alkalmazást.</span><span class="sxs-lookup"><span data-stu-id="56fe4-115">If this parameter is set to true, then this cmdlet creates a test certificate and configures the Windows PowerShell Web Access web application to use the certificate for HTTPS requests.</span></span> <span data-ttu-id="56fe4-116">Ha ez a paraméter false értékre van állítva, akkor nincs tanúsítvány vagy kötési jön létre.</span><span class="sxs-lookup"><span data-stu-id="56fe4-116">If this parameter is set to false, then no certificate or binding is created.</span></span> <span data-ttu-id="56fe4-117">Ha egy másik tanúsítványt használ a Windows PowerShell-elérés "false" értékűre ezt az értéket.</span><span class="sxs-lookup"><span data-stu-id="56fe4-117">Set this value to false if another certificate is used for Windows PowerShell Web Access.</span></span>

|||
|-|-|
| <span data-ttu-id="56fe4-118">Aliasok</span><span class="sxs-lookup"><span data-stu-id="56fe4-118">Aliases</span></span>                              | <span data-ttu-id="56fe4-119">nincs</span><span class="sxs-lookup"><span data-stu-id="56fe4-119">none</span></span>                                 |
| <span data-ttu-id="56fe4-120">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="56fe4-120">Required?</span></span>                            | <span data-ttu-id="56fe4-121">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-121">false</span></span>                                |
| <span data-ttu-id="56fe4-122">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="56fe4-122">Position?</span></span>                            | <span data-ttu-id="56fe4-123">nevű</span><span class="sxs-lookup"><span data-stu-id="56fe4-123">named</span></span>                                |
| <span data-ttu-id="56fe4-124">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="56fe4-124">Default Value</span></span>                        | <span data-ttu-id="56fe4-125">Igaz</span><span class="sxs-lookup"><span data-stu-id="56fe4-125">true</span></span>                                 |
| <span data-ttu-id="56fe4-126">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="56fe4-126">Accept Pipeline Input?</span></span>               | <span data-ttu-id="56fe4-127">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-127">false</span></span>                                |
| <span data-ttu-id="56fe4-128">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="56fe4-128">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="56fe4-129">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-129">false</span></span>                                |

### <a name="-webapplicationname"></a><span data-ttu-id="56fe4-130">-WebApplicationName</span><span class="sxs-lookup"><span data-stu-id="56fe4-130">-WebApplicationName</span></span>

<span data-ttu-id="56fe4-131">Megadja a webalkalmazás nevét.</span><span class="sxs-lookup"><span data-stu-id="56fe4-131">Specifies the name for your web application.</span></span> <span data-ttu-id="56fe4-132">Ez a Windows PowerShell Web Access URL-cím utolsó része jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="56fe4-132">This is displayed as the last part of the Windows PowerShell Web Access URL.</span></span>

|||
|-|-|
| <span data-ttu-id="56fe4-133">Aliasok</span><span class="sxs-lookup"><span data-stu-id="56fe4-133">Aliases</span></span>                              | <span data-ttu-id="56fe4-134">nincs</span><span class="sxs-lookup"><span data-stu-id="56fe4-134">none</span></span>                                 |
| <span data-ttu-id="56fe4-135">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="56fe4-135">Required?</span></span>                            | <span data-ttu-id="56fe4-136">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-136">false</span></span>                                |
| <span data-ttu-id="56fe4-137">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="56fe4-137">Position?</span></span>                            | <span data-ttu-id="56fe4-138">1</span><span class="sxs-lookup"><span data-stu-id="56fe4-138">1</span></span>                                    |
| <span data-ttu-id="56fe4-139">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="56fe4-139">Default Value</span></span>                        | <span data-ttu-id="56fe4-140">pswa</span><span class="sxs-lookup"><span data-stu-id="56fe4-140">pswa</span></span>                                 |
| <span data-ttu-id="56fe4-141">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="56fe4-141">Accept Pipeline Input?</span></span>               | <span data-ttu-id="56fe4-142">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-142">false</span></span>                                |
| <span data-ttu-id="56fe4-143">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="56fe4-143">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="56fe4-144">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-144">false</span></span>                                |

### <a name="-websitename"></a><span data-ttu-id="56fe4-145">-Webhelynév helyére írja be</span><span class="sxs-lookup"><span data-stu-id="56fe4-145">-WebSiteName</span></span>

<span data-ttu-id="56fe4-146">Megadja a nevét a webkiszolgáló (IIS) webhely, amelyen a Windows PowerShell-elérés webes alkalmazás telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="56fe4-146">Specifies the name of the Web Server (IIS) website on which to install this Windows PowerShell Web Access web application.</span></span>

|||
|-|-|
| <span data-ttu-id="56fe4-147">Aliasok</span><span class="sxs-lookup"><span data-stu-id="56fe4-147">Aliases</span></span>                              | <span data-ttu-id="56fe4-148">nincs</span><span class="sxs-lookup"><span data-stu-id="56fe4-148">none</span></span>                                 |
| <span data-ttu-id="56fe4-149">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="56fe4-149">Required?</span></span>                            | <span data-ttu-id="56fe4-150">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-150">false</span></span>                                |
| <span data-ttu-id="56fe4-151">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="56fe4-151">Position?</span></span>                            | <span data-ttu-id="56fe4-152">nevű</span><span class="sxs-lookup"><span data-stu-id="56fe4-152">named</span></span>                                |
| <span data-ttu-id="56fe4-153">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="56fe4-153">Default Value</span></span>                        | <span data-ttu-id="56fe4-154">Alapértelmezett webhely</span><span class="sxs-lookup"><span data-stu-id="56fe4-154">Default Web Site</span></span>                     |
| <span data-ttu-id="56fe4-155">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="56fe4-155">Accept Pipeline Input?</span></span>               | <span data-ttu-id="56fe4-156">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-156">false</span></span>                                |
| <span data-ttu-id="56fe4-157">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="56fe4-157">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="56fe4-158">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-158">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="56fe4-159">-Confirm</span><span class="sxs-lookup"><span data-stu-id="56fe4-159">-Confirm</span></span>

<span data-ttu-id="56fe4-160">Jóváhagyást kér a parancsmag futtatása előtt.</span><span class="sxs-lookup"><span data-stu-id="56fe4-160">Prompts you for confirmation before running the cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="56fe4-161">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="56fe4-161">Required?</span></span>                            | <span data-ttu-id="56fe4-162">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-162">false</span></span>                                |
| <span data-ttu-id="56fe4-163">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="56fe4-163">Position?</span></span>                            | <span data-ttu-id="56fe4-164">nevű</span><span class="sxs-lookup"><span data-stu-id="56fe4-164">named</span></span>                                |
| <span data-ttu-id="56fe4-165">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="56fe4-165">Default Value</span></span>                        | <span data-ttu-id="56fe4-166">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-166">false</span></span>                                |
| <span data-ttu-id="56fe4-167">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="56fe4-167">Accept Pipeline Input?</span></span>               | <span data-ttu-id="56fe4-168">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-168">false</span></span>                                |
| <span data-ttu-id="56fe4-169">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="56fe4-169">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="56fe4-170">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-170">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="56fe4-171">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="56fe4-171">-WhatIf</span></span>

<span data-ttu-id="56fe4-172">Bemutatja, mi történne a parancsmag futtatásakor.</span><span class="sxs-lookup"><span data-stu-id="56fe4-172">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="56fe4-173">A parancsmag nem fut.</span><span class="sxs-lookup"><span data-stu-id="56fe4-173">The cmdlet is not run.</span></span>

|||
|-|-|
| <span data-ttu-id="56fe4-174">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="56fe4-174">Required?</span></span>                            | <span data-ttu-id="56fe4-175">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-175">false</span></span>                                |
| <span data-ttu-id="56fe4-176">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="56fe4-176">Position?</span></span>                            | <span data-ttu-id="56fe4-177">nevű</span><span class="sxs-lookup"><span data-stu-id="56fe4-177">named</span></span>                                |
| <span data-ttu-id="56fe4-178">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="56fe4-178">Default Value</span></span>                        | <span data-ttu-id="56fe4-179">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-179">false</span></span>                                |
| <span data-ttu-id="56fe4-180">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="56fe4-180">Accept Pipeline Input?</span></span>               | <span data-ttu-id="56fe4-181">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-181">false</span></span>                                |
| <span data-ttu-id="56fe4-182">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="56fe4-182">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="56fe4-183">hamis</span><span class="sxs-lookup"><span data-stu-id="56fe4-183">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="56fe4-184">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="56fe4-184">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="56fe4-185">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="56fe4-185">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span> <span data-ttu-id="56fe4-186">További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="56fe4-186">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="56fe4-187">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="56fe4-187">INPUTS</span></span>

<span data-ttu-id="56fe4-188">Ennél a parancsmagnál nincs bemenet.</span><span class="sxs-lookup"><span data-stu-id="56fe4-188">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="56fe4-189">KIMENETEK</span><span class="sxs-lookup"><span data-stu-id="56fe4-189">OUTPUTS</span></span>

<span data-ttu-id="56fe4-190">Ez a parancsmag nem hoz létre kimenetet.</span><span class="sxs-lookup"><span data-stu-id="56fe4-190">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="56fe4-191">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="56fe4-191">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="56fe4-192">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="56fe4-192">EXAMPLE 1</span></span>

<span data-ttu-id="56fe4-193">Ebben a példában a PSWA webes alkalmazás alapértelmezett értékeinek használatával telepíti a **WebApplicationName** (*pswa*) és **Webhelynév helyére írja be** (*Default Web Site* ) paramétereket.</span><span class="sxs-lookup"><span data-stu-id="56fe4-193">This example installs the PSWA web application using the default values for the **WebApplicationName** (*pswa*) and **WebSiteName** (*Default Web Site*) parameters .</span></span>

```
Install-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="56fe4-194">2. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="56fe4-194">EXAMPLE 2</span></span>

<span data-ttu-id="56fe4-195">Ebben a példában a PSWA webalkalmazás telepítése egy tesztcélú tanúsítvánnyal, és a tartozó alapértelmezett értékeket használ a **WebApplicationName** és **Webhelynév helyére írja be** paramétereket.</span><span class="sxs-lookup"><span data-stu-id="56fe4-195">This example installs the PSWA web application with a test certificate, and using the default values for the **WebApplicationName** and **WebSiteName** parameters.</span></span>

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="56fe4-196">Kapcsolódó témakörök</span><span class="sxs-lookup"><span data-stu-id="56fe4-196">Related topics</span></span>

- [<span data-ttu-id="56fe4-197">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="56fe4-197">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="56fe4-198">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="56fe4-198">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="56fe4-199">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="56fe4-199">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="56fe4-200">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="56fe4-200">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)