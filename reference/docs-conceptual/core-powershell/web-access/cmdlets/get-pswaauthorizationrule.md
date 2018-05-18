---
ms.topic: reference
keywords: PowerShell parancsmag
ms.date: 12/12/2016
title: Get-PswaAuthorizationRule
ms.openlocfilehash: d61dce18e87311d7d815a689ba675db44aaec3cb
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="get-pswaauthorizationrule"></a><span data-ttu-id="af3f8-103">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="af3f8-103">Get-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="af3f8-104">SYNOPSIS</span><span class="sxs-lookup"><span data-stu-id="af3f8-104">SYNOPSIS</span></span>

<span data-ttu-id="af3f8-105">A Windows PowerShell® Web Access-engedélyezési szabályok készletét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="af3f8-105">Returns a set of the Windows PowerShell® Web Access authorization rules.</span></span>

## <a name="syntax"></a><span data-ttu-id="af3f8-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="af3f8-106">Syntax</span></span>

### <a name="id"></a><span data-ttu-id="af3f8-107">ID</span><span class="sxs-lookup"><span data-stu-id="af3f8-107">ID</span></span>
```
Get-PswaAuthorizationRule [[-Id] <Int32[]> ] [ <CommonParameters>]
```

### <a name="name"></a><span data-ttu-id="af3f8-108">Név</span><span class="sxs-lookup"><span data-stu-id="af3f8-108">Name</span></span>
```
Get-PswaAuthorizationRule [-RuleName] <String[]> [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="af3f8-109">LEÍRÁS</span><span class="sxs-lookup"><span data-stu-id="af3f8-109">DESCRIPTION</span></span>

<span data-ttu-id="af3f8-110">A **Get-PswaAuthorizationRule** parancsmag a Windows PowerShell® Web Access-engedélyezési szabályok készletét adja vissza.</span><span class="sxs-lookup"><span data-stu-id="af3f8-110">The **Get-PswaAuthorizationRule** cmdlet returns a set of the Windows PowerShell® Web Access authorization rules.</span></span>
<span data-ttu-id="af3f8-111">Ha sem a **azonosító** paraméter, sem a **szabálynév** paraméter meg van adva, akkor ez a parancsmag az összes szabályokat sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="af3f8-111">If neither the **Id** parameter nor the **RuleName** parameter is specified, then this cmdlet lists all rules.</span></span> <span data-ttu-id="af3f8-112">A **azonosító** paraméter használható eredmények szűrésére.</span><span class="sxs-lookup"><span data-stu-id="af3f8-112">The **Id** parameter can be used to filter the results.</span></span>

## <a name="parameters"></a><span data-ttu-id="af3f8-113">PARAMÉTEREK</span><span class="sxs-lookup"><span data-stu-id="af3f8-113">PARAMETERS</span></span>

### <a name="-idltint32gt"></a><span data-ttu-id="af3f8-114">-Id&lt;Int32\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="af3f8-114">-Id&lt;Int32\[\]&gt;</span></span>

<span data-ttu-id="af3f8-115">Adja meg a szabályokat, amelyek ennek a parancsmagnak kell kapnia a azonosítói (azonosítók).</span><span class="sxs-lookup"><span data-stu-id="af3f8-115">Specifies the identifiers (IDs) of the rules that this cmdlet should get.</span></span> <span data-ttu-id="af3f8-116">Ha nincs azonosítók meg van adva, ennek a parancsmagnak összes engedélyezési szabályt adja vissza.</span><span class="sxs-lookup"><span data-stu-id="af3f8-116">If no IDs are specified, then this cmdlet returns all authorization rules.</span></span>

|||
|-|-|
| <span data-ttu-id="af3f8-117">Aliasok</span><span class="sxs-lookup"><span data-stu-id="af3f8-117">Aliases</span></span>                              | <span data-ttu-id="af3f8-118">nincs</span><span class="sxs-lookup"><span data-stu-id="af3f8-118">none</span></span>                                 |
| <span data-ttu-id="af3f8-119">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="af3f8-119">Required?</span></span>                            | <span data-ttu-id="af3f8-120">hamis</span><span class="sxs-lookup"><span data-stu-id="af3f8-120">false</span></span>                                |
| <span data-ttu-id="af3f8-121">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="af3f8-121">Position?</span></span>                            | <span data-ttu-id="af3f8-122">2</span><span class="sxs-lookup"><span data-stu-id="af3f8-122">2</span></span>                                    |
| <span data-ttu-id="af3f8-123">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="af3f8-123">Default Value</span></span>                        | <span data-ttu-id="af3f8-124">nincs</span><span class="sxs-lookup"><span data-stu-id="af3f8-124">none</span></span>                                 |
| <span data-ttu-id="af3f8-125">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="af3f8-125">Accept Pipeline Input?</span></span>               | <span data-ttu-id="af3f8-126">Igaz (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="af3f8-126">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="af3f8-127">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="af3f8-127">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="af3f8-128">hamis</span><span class="sxs-lookup"><span data-stu-id="af3f8-128">false</span></span>                                |

### <a name="-rulenameltstringgt"></a><span data-ttu-id="af3f8-129">-RuleName&lt;karakterlánc\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="af3f8-129">-RuleName&lt;String\[\]&gt;</span></span>

<span data-ttu-id="af3f8-130">Meghatározza az engedélyezési szabályok beolvasása nevét.</span><span class="sxs-lookup"><span data-stu-id="af3f8-130">Specifies the names of authorization rules to retrieve.</span></span> <span data-ttu-id="af3f8-131">Ez a paraméter a szabály a tömb karakterláncok szabály nevének pontosan egyeznie adja vissza.</span><span class="sxs-lookup"><span data-stu-id="af3f8-131">This parameter returns any rules that exactly match the rule names of the strings in this array.</span></span>

|||
|-|-|
| <span data-ttu-id="af3f8-132">Aliasok</span><span class="sxs-lookup"><span data-stu-id="af3f8-132">Aliases</span></span>                              | <span data-ttu-id="af3f8-133">nincs</span><span class="sxs-lookup"><span data-stu-id="af3f8-133">none</span></span>                                 |
| <span data-ttu-id="af3f8-134">Kötelező?</span><span class="sxs-lookup"><span data-stu-id="af3f8-134">Required?</span></span>                            | <span data-ttu-id="af3f8-135">Igaz</span><span class="sxs-lookup"><span data-stu-id="af3f8-135">true</span></span>                                 |
| <span data-ttu-id="af3f8-136">Pozíció?</span><span class="sxs-lookup"><span data-stu-id="af3f8-136">Position?</span></span>                            | <span data-ttu-id="af3f8-137">2</span><span class="sxs-lookup"><span data-stu-id="af3f8-137">2</span></span>                                    |
| <span data-ttu-id="af3f8-138">Alapértelmezett érték</span><span class="sxs-lookup"><span data-stu-id="af3f8-138">Default Value</span></span>                        | <span data-ttu-id="af3f8-139">nincs</span><span class="sxs-lookup"><span data-stu-id="af3f8-139">none</span></span>                                 |
| <span data-ttu-id="af3f8-140">Láncbemenet fogadása?</span><span class="sxs-lookup"><span data-stu-id="af3f8-140">Accept Pipeline Input?</span></span>               | <span data-ttu-id="af3f8-141">Igaz (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="af3f8-141">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="af3f8-142">Helyettesítő karakterek elfogadása?</span><span class="sxs-lookup"><span data-stu-id="af3f8-142">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="af3f8-143">hamis</span><span class="sxs-lookup"><span data-stu-id="af3f8-143">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="af3f8-144">&lt;Általánosparaméterek&gt;</span><span class="sxs-lookup"><span data-stu-id="af3f8-144">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="af3f8-145">Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="af3f8-145">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="af3f8-146">További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="af3f8-146">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="af3f8-147">BEMENETEK</span><span class="sxs-lookup"><span data-stu-id="af3f8-147">INPUTS</span></span>

### <a name="int"></a><span data-ttu-id="af3f8-148">int\[\]</span><span class="sxs-lookup"><span data-stu-id="af3f8-148">int\[\]</span></span>

<span data-ttu-id="af3f8-149">Ez a parancsmag egy számokból álló tömb vagy karakterlánc-értékek tömbje fogad el bemenetként.</span><span class="sxs-lookup"><span data-stu-id="af3f8-149">This cmdlet accepts an array of integers or an array of string values as input.</span></span>

### <a name="string"></a><span data-ttu-id="af3f8-150">Karakterlánc\[\]</span><span class="sxs-lookup"><span data-stu-id="af3f8-150">String\[\]</span></span>

<span data-ttu-id="af3f8-151">Ez a parancsmag egy számokból álló tömb vagy karakterlánc-értékek tömbje fogad el bemenetként.</span><span class="sxs-lookup"><span data-stu-id="af3f8-151">This cmdlet accepts an array of integers or an array of string values as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="af3f8-152">KIMENETEK</span><span class="sxs-lookup"><span data-stu-id="af3f8-152">OUTPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="af3f8-153">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="af3f8-153">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="af3f8-154">Ez a parancsmag kimeneteként hoz létre egy PswaAuthorizationRule objektum.</span><span class="sxs-lookup"><span data-stu-id="af3f8-154">This cmdlet produces a PswaAuthorizationRule object as output.</span></span>


## <a name="examples"></a><span data-ttu-id="af3f8-155">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="af3f8-155">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="af3f8-156">1. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="af3f8-156">EXAMPLE 1</span></span>

<span data-ttu-id="af3f8-157">Ebben a példában az összes szabály lekérdezi.</span><span class="sxs-lookup"><span data-stu-id="af3f8-157">This example gets all of the rules.</span></span>

```PowerShell
    PS C:\> Get-PswaAuthorizationRule
```

### <a name="example-2"></a><span data-ttu-id="af3f8-158">2. PÉLDA</span><span class="sxs-lookup"><span data-stu-id="af3f8-158">EXAMPLE 2</span></span>

<span data-ttu-id="af3f8-159">Ebben a példában az ID változója szabály lekérdezi *2*.</span><span class="sxs-lookup"><span data-stu-id="af3f8-159">This example gets a rule with an ID of *2*.</span></span>

```PowerShell
    PS C:\> Get-PswaAuthorizationRule –Id 2
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="af3f8-160">{#Example-3 .subHeading} 3. példa</span><span class="sxs-lookup"><span data-stu-id="af3f8-160">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="af3f8-161">Ez a példa bemutatja, hogyan a parancsmag elfogadja láncból értéket.</span><span class="sxs-lookup"><span data-stu-id="af3f8-161">This example illustrates how the cmdlet accepts a value from pipeline.</span></span>
<span data-ttu-id="af3f8-162">A szabály azonosítót és egy szabálynevet átadott ebben a parancsmagban.</span><span class="sxs-lookup"><span data-stu-id="af3f8-162">A rule id and a rule name are passed in this cmdlet.</span></span>

```PowerShell
    PS C:\> "rule1",0 | Get-PswaAuthorizationRule
```

## <a name="related-topics"></a><span data-ttu-id="af3f8-163">Kapcsolódó témakörök</span><span class="sxs-lookup"><span data-stu-id="af3f8-163">Related topics</span></span>

- [<span data-ttu-id="af3f8-164">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="af3f8-164">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="af3f8-165">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="af3f8-165">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="af3f8-166">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="af3f8-166">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
- [<span data-ttu-id="af3f8-167">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="af3f8-167">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)