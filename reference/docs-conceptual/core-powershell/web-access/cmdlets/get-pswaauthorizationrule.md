---
description: ''
ms.topic: article
ms.prod: powershell
keywords: PowerShell parancsmag
ms.date: 12/12/2016
title: Get-pswaauthorizationrule
ms.technology: powershell
ms.openlocfilehash: 74c044c329d8b6a305b86c9056a7041fb5fd046b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="get-pswaauthorizationrule"></a><span data-ttu-id="1e9ad-103">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="1e9ad-103">Get-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="1e9ad-104">SYNOPSIS</span><span class="sxs-lookup"><span data-stu-id="1e9ad-104">SYNOPSIS</span></span>

<span data-ttu-id="1e9ad-105">A Windows PowerShell® Web Access-engedélyezési szabályok készletét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-105">Returns a set of the Windows PowerShell® Web Access authorization rules.</span></span>

## <a name="syntax"></a><span data-ttu-id="1e9ad-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="1e9ad-106">Syntax</span></span>

### <a name="id"></a><span data-ttu-id="1e9ad-107">ID</span><span class="sxs-lookup"><span data-stu-id="1e9ad-107">ID</span></span>
```
Get-PswaAuthorizationRule [[-Id] <Int32[]> ] [ <CommonParameters>]
```

### <a name="name"></a><span data-ttu-id="1e9ad-108">Név</span><span class="sxs-lookup"><span data-stu-id="1e9ad-108">Name</span></span>
```
Get-PswaAuthorizationRule [-RuleName] <String[]> [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="1e9ad-109">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="1e9ad-109">DESCRIPTION</span></span>

<span data-ttu-id="1e9ad-110">A **Get-PswaAuthorizationRule** parancsmag a Windows PowerShell® Web Access-engedélyezési szabályok készletét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-110">The **Get-PswaAuthorizationRule** cmdlet returns a set of the Windows PowerShell® Web Access authorization rules.</span></span>
<span data-ttu-id="1e9ad-111">Ha sem a **azonosító** paraméter, sem a **szabálynév** paraméter meg van adva, akkor ez a parancsmag az összes szabályokat sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-111">If neither the **Id** parameter nor the **RuleName** parameter is specified, then this cmdlet lists all rules.</span></span> <span data-ttu-id="1e9ad-112">A **azonosító** paraméter használható eredmények szűrésére.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-112">The **Id** parameter can be used to filter the results.</span></span>

## <a name="parameters"></a><span data-ttu-id="1e9ad-113">PARAMÉTEREK</span><span class="sxs-lookup"><span data-stu-id="1e9ad-113">PARAMETERS</span></span>

### <a name="-idltint32gt"></a><span data-ttu-id="1e9ad-114">-Id&lt;Int32\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="1e9ad-114">-Id&lt;Int32\[\]&gt;</span></span>

<span data-ttu-id="1e9ad-115">Adja meg a szabályokat, amelyek ennek a parancsmagnak kell kapnia a azonosítói (azonosítók).</span><span class="sxs-lookup"><span data-stu-id="1e9ad-115">Specifies the identifiers (IDs) of the rules that this cmdlet should get.</span></span> <span data-ttu-id="1e9ad-116">Ha nincs azonosítók meg van adva, ennek a parancsmagnak összes engedélyezési szabályt adja vissza.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-116">If no IDs are specified, then this cmdlet returns all authorization rules.</span></span>

|||
|-|-|
| <span data-ttu-id="1e9ad-117">Aliasok</span><span class="sxs-lookup"><span data-stu-id="1e9ad-117">Aliases</span></span>                              | <span data-ttu-id="1e9ad-118">nincs</span><span class="sxs-lookup"><span data-stu-id="1e9ad-118">none</span></span>                                 |
| <span data-ttu-id="1e9ad-119">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="1e9ad-119">Required?</span></span>                            | <span data-ttu-id="1e9ad-120">hamis</span><span class="sxs-lookup"><span data-stu-id="1e9ad-120">false</span></span>                                |
| <span data-ttu-id="1e9ad-121">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="1e9ad-121">Position?</span></span>                            | <span data-ttu-id="1e9ad-122">2</span><span class="sxs-lookup"><span data-stu-id="1e9ad-122">2</span></span>                                    |
| <span data-ttu-id="1e9ad-123">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="1e9ad-123">Default Value</span></span>                        | <span data-ttu-id="1e9ad-124">nincs</span><span class="sxs-lookup"><span data-stu-id="1e9ad-124">none</span></span>                                 |
| <span data-ttu-id="1e9ad-125">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="1e9ad-125">Accept Pipeline Input?</span></span>               | <span data-ttu-id="1e9ad-126">Igaz (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="1e9ad-126">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="1e9ad-127">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="1e9ad-127">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="1e9ad-128">hamis</span><span class="sxs-lookup"><span data-stu-id="1e9ad-128">false</span></span>                                |

### <a name="-rulenameltstringgt"></a><span data-ttu-id="1e9ad-129">-RuleName&lt;String\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="1e9ad-129">-RuleName&lt;String\[\]&gt;</span></span>

<span data-ttu-id="1e9ad-130">Meghatározza az engedélyezési szabályok beolvasása nevét.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-130">Specifies the names of authorization rules to retrieve.</span></span> <span data-ttu-id="1e9ad-131">Ez a paraméter a szabály a tömb karakterláncok szabály nevének pontosan egyeznie adja vissza.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-131">This parameter returns any rules that exactly match the rule names of the strings in this array.</span></span>

|||
|-|-|
| <span data-ttu-id="1e9ad-132">Aliasok</span><span class="sxs-lookup"><span data-stu-id="1e9ad-132">Aliases</span></span>                              | <span data-ttu-id="1e9ad-133">nincs</span><span class="sxs-lookup"><span data-stu-id="1e9ad-133">none</span></span>                                 |
| <span data-ttu-id="1e9ad-134">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="1e9ad-134">Required?</span></span>                            | <span data-ttu-id="1e9ad-135">Igaz</span><span class="sxs-lookup"><span data-stu-id="1e9ad-135">true</span></span>                                 |
| <span data-ttu-id="1e9ad-136">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="1e9ad-136">Position?</span></span>                            | <span data-ttu-id="1e9ad-137">2</span><span class="sxs-lookup"><span data-stu-id="1e9ad-137">2</span></span>                                    |
| <span data-ttu-id="1e9ad-138">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="1e9ad-138">Default Value</span></span>                        | <span data-ttu-id="1e9ad-139">nincs</span><span class="sxs-lookup"><span data-stu-id="1e9ad-139">none</span></span>                                 |
| <span data-ttu-id="1e9ad-140">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="1e9ad-140">Accept Pipeline Input?</span></span>               | <span data-ttu-id="1e9ad-141">Igaz (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="1e9ad-141">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="1e9ad-142">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="1e9ad-142">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="1e9ad-143">hamis</span><span class="sxs-lookup"><span data-stu-id="1e9ad-143">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="1e9ad-144">&lt;Általánosparaméterek&gt;</span><span class="sxs-lookup"><span data-stu-id="1e9ad-144">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="1e9ad-145">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-145">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="1e9ad-146">További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="1e9ad-146">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="1e9ad-147">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="1e9ad-147">INPUTS</span></span>

### <a name="int"></a><span data-ttu-id="1e9ad-148">int\[\]</span><span class="sxs-lookup"><span data-stu-id="1e9ad-148">int\[\]</span></span>

<span data-ttu-id="1e9ad-149">Ez a parancsmag egy számokból álló tömb vagy karakterlánc-értékek tömbje fogad el bemenetként.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-149">This cmdlet accepts an array of integers or an array of string values as input.</span></span>

### <a name="string"></a><span data-ttu-id="1e9ad-150">Karakterlánc\[\]</span><span class="sxs-lookup"><span data-stu-id="1e9ad-150">String\[\]</span></span>

<span data-ttu-id="1e9ad-151">Ez a parancsmag egy számokból álló tömb vagy karakterlánc-értékek tömbje fogad el bemenetként.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-151">This cmdlet accepts an array of integers or an array of string values as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="1e9ad-152">KIMENETEK</span><span class="sxs-lookup"><span data-stu-id="1e9ad-152">OUTPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="1e9ad-153">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="1e9ad-153">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="1e9ad-154">Ez a parancsmag kimeneteként hoz létre egy PswaAuthorizationRule objektum.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-154">This cmdlet produces a PswaAuthorizationRule object as output.</span></span>


## <a name="examples"></a><span data-ttu-id="1e9ad-155">EXAMPLES</span><span class="sxs-lookup"><span data-stu-id="1e9ad-155">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="1e9ad-156">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="1e9ad-156">EXAMPLE 1</span></span>

<span data-ttu-id="1e9ad-157">Ebben a példában az összes szabály lekérdezi.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-157">This example gets all of the rules.</span></span>

```PowerShell
    PS C:\> Get-PswaAuthorizationRule
```

### <a name="example-2"></a><span data-ttu-id="1e9ad-158">2. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="1e9ad-158">EXAMPLE 2</span></span>

<span data-ttu-id="1e9ad-159">Ebben a példában az ID változója szabály lekérdezi *2*.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-159">This example gets a rule with an ID of *2*.</span></span>

```PowerShell
    PS C:\> Get-PswaAuthorizationRule –Id 2
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="1e9ad-160">{#Example-3 .subHeading} 3. példa</span><span class="sxs-lookup"><span data-stu-id="1e9ad-160">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="1e9ad-161">Ez a példa bemutatja, hogyan a parancsmag elfogadja láncból értéket.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-161">This example illustrates how the cmdlet accepts a value from pipeline.</span></span>
<span data-ttu-id="1e9ad-162">A szabály azonosítót és egy szabálynevet átadott ebben a parancsmagban.</span><span class="sxs-lookup"><span data-stu-id="1e9ad-162">A rule id and a rule name are passed in this cmdlet.</span></span>

```PowerShell
    PS C:\> "rule1",0 | Get-PswaAuthorizationRule
```

## <a name="related-topics"></a><span data-ttu-id="1e9ad-163">Kapcsolódó témakörök</span><span class="sxs-lookup"><span data-stu-id="1e9ad-163">Related topics</span></span>

- [<span data-ttu-id="1e9ad-164">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="1e9ad-164">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="1e9ad-165">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="1e9ad-165">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="1e9ad-166">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="1e9ad-166">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
- [<span data-ttu-id="1e9ad-167">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="1e9ad-167">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)