---
title: Attribútum Deklarace parametru |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes, Parameter
- Parameter attribute, described
- Parameter attribute
ms.assetid: 08433d0b-169b-42c8-9335-2881d9034698
caps.latest.revision: 13
ms.openlocfilehash: a3488d5fb3f7eb3df28d0242d6c39d07145a3c8d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067552"
---
# <a name="parameter-attribute-declaration"></a><span data-ttu-id="88482-102">Paraméterek attribútumdeklarációja</span><span class="sxs-lookup"><span data-stu-id="88482-102">Parameter Attribute Declaration</span></span>

<span data-ttu-id="88482-103">A paraméter-attribútumhoz azonosítja a parancsmag osztály nyilvános tulajdonsága parancsmag-paraméterként.</span><span class="sxs-lookup"><span data-stu-id="88482-103">The Parameter attribute identifies a public property of the cmdlet class as a cmdlet parameter.</span></span>

## <a name="syntax"></a><span data-ttu-id="88482-104">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="88482-104">Syntax</span></span>

```csharp
[Parameter()]
[Parameter(Named Parameters...)]
```

#### <a name="parameters"></a><span data-ttu-id="88482-105">Paraméterek</span><span class="sxs-lookup"><span data-stu-id="88482-105">Parameters</span></span>

<span data-ttu-id="88482-106">`Mandatory` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="88482-106">`Mandatory` ([System.Boolean](/dotnet/api/System.Boolean)) Optional named parameter.</span></span> <span data-ttu-id="88482-107">`True` azt jelzi, hogy a parancsmag paraméter megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="88482-107">`True` indicates the cmdlet parameter is required.</span></span> <span data-ttu-id="88482-108">Ha egy kötelező paraméter nincs megadva, a parancsmag meghívása, a Windows PowerShell bekéri a felhasználótól a paraméter értékét.</span><span class="sxs-lookup"><span data-stu-id="88482-108">If a required parameter is not provided when the cmdlet is invoked, Windows PowerShell prompts the user for a parameter value.</span></span> <span data-ttu-id="88482-109">Az alapértelmezett érték `false`.</span><span class="sxs-lookup"><span data-stu-id="88482-109">The default is `false`.</span></span>

<span data-ttu-id="88482-110">`ParameterSetName` ([System.String](/dotnet/api/System.String)) nevű paraméter nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="88482-110">`ParameterSetName` ([System.String](/dotnet/api/System.String)) Optional named parameter.</span></span> <span data-ttu-id="88482-111">Adja meg a paraméter beállítása, hogy ez a parancsmag a paraméter tartozik.</span><span class="sxs-lookup"><span data-stu-id="88482-111">Specifies the parameter set that this cmdlet parameter belongs to.</span></span> <span data-ttu-id="88482-112">Ha nincs paraméterkészletet van megadva, a paraméter az összes paraméterkészlettel tartozik.</span><span class="sxs-lookup"><span data-stu-id="88482-112">If no parameter set is specified, the parameter belongs to all parameter sets.</span></span>

<span data-ttu-id="88482-113">`Position` ([System.Integer](/dotnet/api/System.Integer)) nevű paraméter nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="88482-113">`Position` ([System.Integer](/dotnet/api/System.Integer)) Optional named parameter.</span></span> <span data-ttu-id="88482-114">Megadja az a paraméter egy Windows PowerShell-parancsot.</span><span class="sxs-lookup"><span data-stu-id="88482-114">Specifies the position of the parameter within a Windows PowerShell command.</span></span>

<span data-ttu-id="88482-115">`ValueFromPipeline` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="88482-115">`ValueFromPipeline` ([System.Boolean](/dotnet/api/System.Boolean)) Optional named parameter.</span></span> <span data-ttu-id="88482-116">`True` azt jelzi, hogy a parancsmag paraméterrel egy folyamat objektumot az értékét.</span><span class="sxs-lookup"><span data-stu-id="88482-116">`True` indicates that the cmdlet parameter takes its value from a pipeline object.</span></span> <span data-ttu-id="88482-117">Adja meg ezt a kulcsszót, ha a parancsmag fér hozzá a teljes objektumot, nem csak az objektum osztályát.</span><span class="sxs-lookup"><span data-stu-id="88482-117">Specify this keyword if the cmdlet accesses the complete object, not just a property of the object.</span></span> <span data-ttu-id="88482-118">Az alapértelmezett érték `false`.</span><span class="sxs-lookup"><span data-stu-id="88482-118">The default is `false`.</span></span>

<span data-ttu-id="88482-119">`ValueFromPipelineByPropertyName` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="88482-119">`ValueFromPipelineByPropertyName` ([System.Boolean](/dotnet/api/System.Boolean)) Optional named parameter.</span></span> <span data-ttu-id="88482-120">`True` azt jelzi, hogy a parancsmag paraméterrel az egyik tulajdonsága egy folyamat objektumot, amely rendelkezik ugyanazzal a névvel vagy az azonos alias, ez a paraméter értékét.</span><span class="sxs-lookup"><span data-stu-id="88482-120">`True` indicates that the cmdlet parameter takes its value from a property of a pipeline object that has either the same name or the same alias as this parameter.</span></span> <span data-ttu-id="88482-121">Például, ha a parancsmag rendelkezik egy `Name` paraméter és a folyamat objektumot is rendelkezik egy `Name` tulajdonság, az értékét a `Name` tulajdonság be van-e rendelve a `Name` a parancsmag.</span><span class="sxs-lookup"><span data-stu-id="88482-121">For example, if the cmdlet has a `Name` parameter and the pipeline object also has a `Name` property, the value of the `Name` property is assigned to the `Name` parameter of the cmdlet.</span></span> <span data-ttu-id="88482-122">Az alapértelmezett érték `false`.</span><span class="sxs-lookup"><span data-stu-id="88482-122">The default is `false`.</span></span>

<span data-ttu-id="88482-123">`ValueFromRemainingArguments` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="88482-123">`ValueFromRemainingArguments` ([System.Boolean](/dotnet/api/System.Boolean)) Optional named parameter.</span></span> <span data-ttu-id="88482-124">`True` azt jelzi, hogy a parancsmag paraméter elfogadja a parancsmagnak átadott összes többi argumentum.</span><span class="sxs-lookup"><span data-stu-id="88482-124">`True` indicates that the cmdlet parameter accepts all remaining arguments that are passed to the cmdlet.</span></span> <span data-ttu-id="88482-125">Az alapértelmezett érték `false`.</span><span class="sxs-lookup"><span data-stu-id="88482-125">The default is `false`.</span></span>

<span data-ttu-id="88482-126">`HelpMessage` Nem kötelező paraméter neve.</span><span class="sxs-lookup"><span data-stu-id="88482-126">`HelpMessage` Optional named parameter.</span></span> <span data-ttu-id="88482-127">Adja meg a paraméter egy rövid leírása.</span><span class="sxs-lookup"><span data-stu-id="88482-127">Specifies a short description of the parameter.</span></span> <span data-ttu-id="88482-128">Windows PowerShell jeleníti meg ezt az üzenetet, amikor a parancsmag futtatása és a egy kötelező paraméter nincs megadva.</span><span class="sxs-lookup"><span data-stu-id="88482-128">Windows PowerShell displays this message when a cmdlet is run and a mandatory parameter is not specified.</span></span>

<span data-ttu-id="88482-129">`HelpMessageBaseName` Nem kötelező paraméter neve. Itt adhatja meg a helyet, ahol az erőforrás-azonosítók találhatók.</span><span class="sxs-lookup"><span data-stu-id="88482-129">`HelpMessageBaseName` Optional named parameter.Specifies the location where resource identifiers reside.</span></span> <span data-ttu-id="88482-130">Ez a paraméter sikerült adja meg például egy erőforrás megkeresni a kívánt súgó üzeneteket tartalmazó szerelvény.</span><span class="sxs-lookup"><span data-stu-id="88482-130">For example, this parameter could specify a resource assembly that contains Help messages that you want to localize.</span></span>

<span data-ttu-id="88482-131">`HelpMessageResourceId` Nem kötelező paraméter neve. Itt adhatja meg az erőforrás-azonosítója egy súgóüzenetet.</span><span class="sxs-lookup"><span data-stu-id="88482-131">`HelpMessageResourceId` Optional named parameter.Specifies the resource identifier for a Help message.</span></span>

## <a name="remarks"></a><span data-ttu-id="88482-132">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="88482-132">Remarks</span></span>

- <span data-ttu-id="88482-133">Ezt az attribútumot deklarálni kapcsolatos további információkért lásd: [deklarálja parancsmag-paraméterek hogyan](./how-to-declare-cmdlet-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="88482-133">For more information about how to declare this attribute, see [How to Declare Cmdlet Parameters](./how-to-declare-cmdlet-parameters.md).</span></span>

- <span data-ttu-id="88482-134">A parancsmag paraméterei tetszőleges számú rendelkezhet.</span><span class="sxs-lookup"><span data-stu-id="88482-134">A cmdlet can have any number of parameters.</span></span> <span data-ttu-id="88482-135">A jobb felhasználói élményt, azonban a paraméterek számát, korlátozza.</span><span class="sxs-lookup"><span data-stu-id="88482-135">However, for a better user experience, limit the number of parameters.</span></span>

- <span data-ttu-id="88482-136">Paraméterek deklarálni kell a nyilvános nem statikus mezők vagy tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="88482-136">Parameters must be declared on public non-static fields or properties.</span></span> <span data-ttu-id="88482-137">A Tulajdonságok je nutné deklarovat paramétereket.</span><span class="sxs-lookup"><span data-stu-id="88482-137">Parameters should be declared on properties.</span></span> <span data-ttu-id="88482-138">A tulajdonság rendelkeznie kell egy nyilvános hozzáférő, ha a `ValueFromPipeline` vagy `ValueFromPipelineByPropertyName` kulcsszó, a tulajdonság rendelkeznie kell egy nyilvános get hozzáférő.</span><span class="sxs-lookup"><span data-stu-id="88482-138">The property must have a public set accessor, and if the `ValueFromPipeline` or `ValueFromPipelineByPropertyName` keyword is specified, the property must have a public get accessor.</span></span>

- <span data-ttu-id="88482-139">Pozícióparaméterek megadása esetén egy paraméterben, kevesebb mint öt pozícióparaméterek számának korlátozásához.</span><span class="sxs-lookup"><span data-stu-id="88482-139">When you specify positional parameters,  limit the number of positional parameters in a parameter set to less than five.</span></span> <span data-ttu-id="88482-140">És pozícióparaméterek nem kell összefüggőnek lennie.</span><span class="sxs-lookup"><span data-stu-id="88482-140">And, positional parameters do not have to be contiguous.</span></span> <span data-ttu-id="88482-141">5., 100, és 250 azonos működik, mint 0, 1 és 2.</span><span class="sxs-lookup"><span data-stu-id="88482-141">Positions 5, 100, and 250 work the same as positions 0, 1, and 2.</span></span>

- <span data-ttu-id="88482-142">Ha a `Position` kulcsszó nincs megadva, a parancsmag-paraméterrel lehet hivatkozni a neve.</span><span class="sxs-lookup"><span data-stu-id="88482-142">When the `Position` keyword is not specified, the cmdlet parameter must be referenced by its name.</span></span>

- <span data-ttu-id="88482-143">Paraméterkészlettel használatakor vegye figyelembe a következőket:</span><span class="sxs-lookup"><span data-stu-id="88482-143">When you use parameter sets, note the following:</span></span>

    - <span data-ttu-id="88482-144">Minden egyes paraméterkészletet rendelkeznie kell legalább egy egyedi paramétereket.</span><span class="sxs-lookup"><span data-stu-id="88482-144">Each parameter set must have at least one unique parameter.</span></span> <span data-ttu-id="88482-145">Jó parancsmag tervezési azt jelzi, hogy ez az egyedi paramétereket is kötelező legyen, ha lehetséges.</span><span class="sxs-lookup"><span data-stu-id="88482-145">Good cmdlet design indicates this unique parameter should also be mandatory if possible.</span></span> <span data-ttu-id="88482-146">Ha a parancsmagot paraméterek nélkül futtatásra tervezték, az egyedi paraméter nem kötelező lehet.</span><span class="sxs-lookup"><span data-stu-id="88482-146">If your cmdlet is designed to be run without parameters, the unique parameter cannot be mandatory.</span></span>

    - <span data-ttu-id="88482-147">Nincs paraméterkészletet ugyanazon a helyen egynél több Helyzetbeállító paramétert kell tartalmaznia.</span><span class="sxs-lookup"><span data-stu-id="88482-147">No parameter set should contain more than one positional parameter with the same position.</span></span>

    - <span data-ttu-id="88482-148">Csak egy paramétere paraméterkészlet deklarálnia kell `ValueFromPipeline = true`.</span><span class="sxs-lookup"><span data-stu-id="88482-148">Only one parameter in a parameter set should declare `ValueFromPipeline = true`.</span></span> <span data-ttu-id="88482-149">Több paramétereket adhatja meg `ValueFromPipelineByPropertyName = true`.</span><span class="sxs-lookup"><span data-stu-id="88482-149">Multiple parameters can define `ValueFromPipelineByPropertyName = true`.</span></span>

    - <span data-ttu-id="88482-150">Több paramétereket adhatja meg `ValueFromPipelineByPropertyName = true`.</span><span class="sxs-lookup"><span data-stu-id="88482-150">Multiple parameters can define `ValueFromPipelineByPropertyName = true`.</span></span>

- <span data-ttu-id="88482-151">Az útmutató a paraméterek nevei kapcsolatos további információkért lásd: [parancsmag-paraméterek nevei](standard-cmdlet-parameter-names-and-types.md).</span><span class="sxs-lookup"><span data-stu-id="88482-151">For more information about the guidelines for parameter names, see [Cmdlet Parameter Names](standard-cmdlet-parameter-names-and-types.md).</span></span>

- <span data-ttu-id="88482-152">A paraméter attribútum határozza meg a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) osztály.</span><span class="sxs-lookup"><span data-stu-id="88482-152">The parameter attribute is defined by the [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="88482-153">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="88482-153">See Also</span></span>

[<span data-ttu-id="88482-154">System.Management.Automation.Parameterattribute</span><span class="sxs-lookup"><span data-stu-id="88482-154">System.Management.Automation.Parameterattribute</span></span>](/dotnet/api/System.Management.Automation.ParameterAttribute)

[<span data-ttu-id="88482-155">Parancsmag-paraméterek nevei</span><span class="sxs-lookup"><span data-stu-id="88482-155">Cmdlet Parameter Names</span></span>](standard-cmdlet-parameter-names-and-types.md)

[<span data-ttu-id="88482-156">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="88482-156">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
