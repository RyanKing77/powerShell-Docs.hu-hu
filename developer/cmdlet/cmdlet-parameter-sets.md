---
title: Parancsmag |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f902fd4d-8f6e-4ef1-b07f-59983039a0d1
caps.latest.revision: 10
ms.openlocfilehash: a5822ef1ed3c9efb5957c20255783d515de8957a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068526"
---
# <a name="cmdlet-parameter-sets"></a><span data-ttu-id="698da-102">Parancsmagok paraméterkészletei</span><span class="sxs-lookup"><span data-stu-id="698da-102">Cmdlet Parameter Sets</span></span>

<span data-ttu-id="698da-103">Windows PowerShell paraméterkészlettel használja ahhoz, hogy egyetlen parancsmag, amely a különböző helyzetekhez különböző műveleteket hajthat végre írási.</span><span class="sxs-lookup"><span data-stu-id="698da-103">Windows PowerShell uses parameter sets to enable you to write a single cmdlet that can perform different actions for different scenarios.</span></span> <span data-ttu-id="698da-104">A paraméter csoportok lehetővé teszik elérhetővé a felhasználó eltérő paraméterekkel, és a felhasználó által megadott paraméterek alapján különböző adatokat.</span><span class="sxs-lookup"><span data-stu-id="698da-104">Parameter sets enable you to expose different parameters to the user and to return different information based on the parameters specified by the user.</span></span>

## <a name="examples-of-parameter-sets"></a><span data-ttu-id="698da-105">Példák a paraméterkészlettel</span><span class="sxs-lookup"><span data-stu-id="698da-105">Examples of Parameter Sets</span></span>

<span data-ttu-id="698da-106">Ha például a `Get-EventLog` (a Windows PowerShell által biztosított) parancsmag adja vissza attól függően, hogy a felhasználó adja meg a különböző adatokat a `List` vagy `LogName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="698da-106">For example, the `Get-EventLog` cmdlet (provided by Windows PowerShell) returns different information depending on whether the user specifies the `List` or `LogName` parameter.</span></span> <span data-ttu-id="698da-107">Ha a `List` paraméter meg van adva, a parancsmag a naplófájlok kapcsolatos információkat ad vissza, magukat, de nem az események adatait tartalmazzák.</span><span class="sxs-lookup"><span data-stu-id="698da-107">If the `List` parameter is specified, the cmdlet returns information about the log files themselves but not the event information they contain.</span></span> <span data-ttu-id="698da-108">Ha a `LogName` paraméter meg van adva, a parancsmag adott eseménynaplóból eseményekkel kapcsolatos információkat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="698da-108">If the `LogName` parameter is specified, the cmdlet returns information about the events in a specific event log.</span></span> <span data-ttu-id="698da-109">A `List` és `LogName` paraméterek két külön paraméterkészlettel azonosításához.</span><span class="sxs-lookup"><span data-stu-id="698da-109">The `List` and `LogName` parameters identify two separate parameter sets.</span></span>

## <a name="unique-parameter"></a><span data-ttu-id="698da-110">Az egyedi paramétereket</span><span class="sxs-lookup"><span data-stu-id="698da-110">Unique Parameter</span></span>

<span data-ttu-id="698da-111">Minden egyes paraméterkészletet rendelkeznie kell egy egyedi paraméter, amely a Windows PowerShell-modul segítségével teszi közzé a megfelelő paraméterkészletet.</span><span class="sxs-lookup"><span data-stu-id="698da-111">Each parameter set must have a unique parameter that the Windows PowerShell runtime can use to expose the appropriate parameter set.</span></span> <span data-ttu-id="698da-112">Ha lehetséges az egyedi paramétereket egy kötelező paraméter kell lennie.</span><span class="sxs-lookup"><span data-stu-id="698da-112">If possible, the unique parameter should be a mandatory parameter.</span></span> <span data-ttu-id="698da-113">Egy paraméter megadása kötelező, ha a felhasználónak a paraméter megadása kötelező, és a Windows PowerShell-modul a arra a paraméterre segítségével azonosíthatja a paramétert használja.</span><span class="sxs-lookup"><span data-stu-id="698da-113">When a parameter is mandatory, the user is forced to specify the parameter, and the Windows PowerShell runtime can use that parameter to identify the parameter set to use.</span></span> <span data-ttu-id="698da-114">Az egyedi paraméter kötelező, ha a parancsmagot paraméterek megadása nélkül futtatni célja nem lehet.</span><span class="sxs-lookup"><span data-stu-id="698da-114">The unique parameter cannot be mandatory if your cmdlet is designed to be run without specifying any parameters.</span></span>

## <a name="multiple-parameter-sets"></a><span data-ttu-id="698da-115">Több paraméterkészlettel</span><span class="sxs-lookup"><span data-stu-id="698da-115">Multiple Parameter Sets</span></span>

<span data-ttu-id="698da-116">Az alábbi ábrán a bal oldali oszlopban látható a három érvényes paraméterkészlettel.</span><span class="sxs-lookup"><span data-stu-id="698da-116">In the following illustration, the left column shows three valid parameter sets.</span></span> <span data-ttu-id="698da-117">Paraméter A az első paraméterkészletet egyedi, B paraméter a második paraméterkészletet egyedi, és C paraméter értéke egyedi a harmadik paraméter-készlethez.</span><span class="sxs-lookup"><span data-stu-id="698da-117">Parameter A is unique to the first parameter set, parameter B is unique to the second parameter set, and parameter C is unique to the third parameter set.</span></span> <span data-ttu-id="698da-118">Azonban a jobb oldali oszlopban, a paraméterkészlettel rendelkezik egy egyedi paramétereket.</span><span class="sxs-lookup"><span data-stu-id="698da-118">However, in the right column, the parameter sets do not have a unique parameter.</span></span>

![ps_parametersets](../media/ps-parametersets.gif)

## <a name="parameter-set-requirements"></a><span data-ttu-id="698da-120">Paraméterkészlet követelmények</span><span class="sxs-lookup"><span data-stu-id="698da-120">Parameter Set Requirements</span></span>

<span data-ttu-id="698da-121">Az alábbi követelmények minden paraméterkészlettel vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="698da-121">The following requirements apply to all parameter sets.</span></span>

- <span data-ttu-id="698da-122">Minden egyes paraméterkészletet rendelkeznie kell legalább egy egyedi paramétereket.</span><span class="sxs-lookup"><span data-stu-id="698da-122">Each parameter set must have at least one unique parameter.</span></span> <span data-ttu-id="698da-123">Ha lehetséges győződjön meg arról, ez a paraméter egy kötelező paraméter.</span><span class="sxs-lookup"><span data-stu-id="698da-123">If possible, make this parameter a mandatory parameter.</span></span>

- <span data-ttu-id="698da-124">Egy több pozícióparaméterek tartalmazó paraméterkészletet meg kell határoznia, hogy az egyes paraméterekhez tartozó egyedi pozíciók.</span><span class="sxs-lookup"><span data-stu-id="698da-124">A parameter set that contains multiple positional parameters must define unique positions for each parameter.</span></span> <span data-ttu-id="698da-125">Nincs két pozicionális paramétereknél is adja meg az ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="698da-125">No two positional parameters can specify the same position.</span></span>

- <span data-ttu-id="698da-126">A csoportban csak egy paraméter deklarálhatnak a `ValueFromPipeline` kulcsszó és a egy értéke `true`.</span><span class="sxs-lookup"><span data-stu-id="698da-126">Only one parameter in a set can declare the `ValueFromPipeline` keyword with a value of `true`.</span></span> <span data-ttu-id="698da-127">Több paramétereket adhatja meg a `ValueFromPipelineByPropertyName` kulcsszó és a egy értéke `true`.</span><span class="sxs-lookup"><span data-stu-id="698da-127">Multiple parameters can define the `ValueFromPipelineByPropertyName` keyword with a value of `true`.</span></span>

- <span data-ttu-id="698da-128">Ha nincs paraméterkészletet egy paraméter van megadva, a paraméter paraméterkészlettel összes tartozik.</span><span class="sxs-lookup"><span data-stu-id="698da-128">If no parameter set is specified for a parameter, the parameter belongs to all parameter sets.</span></span>

## <a name="default-parameter-sets"></a><span data-ttu-id="698da-129">Alapértelmezett paraméterkészlettel</span><span class="sxs-lookup"><span data-stu-id="698da-129">Default Parameter Sets</span></span>

<span data-ttu-id="698da-130">Ha több paraméterkészlettel vannak definiálva, használhatja a `DefaultParameterSetName` kulcsszó a parancsmag attribútum, az alapértelmezett paraméter megadását.</span><span class="sxs-lookup"><span data-stu-id="698da-130">When multiple parameter sets are defined, you can use the `DefaultParameterSetName` keyword of the Cmdlet attribute to specify the default parameter set.</span></span> <span data-ttu-id="698da-131">Windows PowerShell használja az alapértelmezett paraméter beállítása, ha nem tudja meghatározni a paraméter használatához állítsa be a parancs által biztosított információk alapján.</span><span class="sxs-lookup"><span data-stu-id="698da-131">Windows PowerShell uses the default parameter set if it cannot determine the parameter set to use based on the information provided by the command.</span></span> <span data-ttu-id="698da-132">A parancsmag attribútum kapcsolatos további információkért lásd: [parancsmag típusattribútum-deklaráció](./cmdlet-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="698da-132">For more information about the Cmdlet attribute, see [Cmdlet Attribute Declaration](./cmdlet-attribute-declaration.md).</span></span>

## <a name="declaring-parameter-sets"></a><span data-ttu-id="698da-133">Jelentést készítő paraméterkészlettel</span><span class="sxs-lookup"><span data-stu-id="698da-133">Declaring Parameter Sets</span></span>

<span data-ttu-id="698da-134">Paraméterkészlet létrehozásához meg kell adnia a `ParameterSetName` minden paramétert a paraméterkészletet paraméter attribútumát deklarálásakor kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="698da-134">To create a parameter set, you must specify the `ParameterSetName` keyword when you declare the Parameter attribute for every parameter in the parameter set.</span></span> <span data-ttu-id="698da-135">Több paraméterkészlettel tartozó paramétereket adjon hozzá egy paraméter attribútum az egyes paraméter.</span><span class="sxs-lookup"><span data-stu-id="698da-135">For parameters that belong to multiple parameter sets, add a Parameter attribute for each parameter set.</span></span> <span data-ttu-id="698da-136">Ez lehetővé teszi, hogy a paraméter eltérően az egyes paraméter meghatározza.</span><span class="sxs-lookup"><span data-stu-id="698da-136">This enables you to define the parameter differently for each parameter set.</span></span> <span data-ttu-id="698da-137">Egy paraméter definiálhat például egy kötelező és választható egy másik.</span><span class="sxs-lookup"><span data-stu-id="698da-137">For example, you can define a parameter as mandatory in one set and optional in another.</span></span> <span data-ttu-id="698da-138">Azonban minden egyes paraméterkészletet tartalmaznia kell egy egyedi paramétert.</span><span class="sxs-lookup"><span data-stu-id="698da-138">However, each parameter set must contain one unique parameter.</span></span>

<span data-ttu-id="698da-139">A következő példában a `UserName` Test01 paraméter beállított, az egyedi paraméter és a `ComputerName` az egyedi paraméter, a Test02 paraméterkészletet.</span><span class="sxs-lookup"><span data-stu-id="698da-139">In the following example, the `UserName` parameter is the unique parameter of the Test01 parameter set, and the `ComputerName` parameter is the unique parameter of the Test02 parameter set.</span></span> <span data-ttu-id="698da-140">A `SharedParam` paraméter mindkét tartozik, és állítsa be a Test02 paraméterkészletet választható Test01 paraméter megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="698da-140">The `SharedParam` parameter belongs to both sets and is mandatory for the Test01 parameter set but optional for the Test02 parameter set.</span></span>

```csharp
[Parameter(Position = 0, Mandatory = true,
           ParameterSetName = "Test01")]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;

[Parameter(Position = 0, Mandatory = true,
           ParameterSetName = "Test02")]
public string ComputerName
{
  get { return computerName; }
  set { computerName = value; }
}
private string computerName;

[Parameter(Mandatory= true, ParameterSetName = "Test01")]
[Parameter(ParameterSetName = "Test02")]
public string SharedParam
{
    get { return sharedParam; }
    set { sharedParam = value; }
}
private string sharedParam;    [Parameter(Position = 0, Mandatory = true,
           ParameterSetName = "Test01")]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```