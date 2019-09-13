---
title: Parancsmag-paraméterek készletei | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f902fd4d-8f6e-4ef1-b07f-59983039a0d1
caps.latest.revision: 10
ms.openlocfilehash: d8c00c7ffd369a32af151836785a2c5f47b05a68
ms.sourcegitcommit: 889b93d170aeb3d444288e7ccf67e62ce822cb7c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/12/2019
ms.locfileid: "70936203"
---
# <a name="cmdlet-parameter-sets"></a><span data-ttu-id="dc8da-102">Parancsmag-paraméterek készletei</span><span class="sxs-lookup"><span data-stu-id="dc8da-102">Cmdlet parameter sets</span></span>

<span data-ttu-id="dc8da-103">A PowerShell paraméter-készleteket használva lehetővé teszi egy olyan parancsmag megírását, amely különböző műveleteket végezhet el különböző helyzetekben.</span><span class="sxs-lookup"><span data-stu-id="dc8da-103">PowerShell uses parameter sets to enable you to write a single cmdlet that can do different actions for different scenarios.</span></span> <span data-ttu-id="dc8da-104">A paraméterek lehetővé teszik, hogy különböző paramétereket tegyen elérhetővé a felhasználó számára.</span><span class="sxs-lookup"><span data-stu-id="dc8da-104">Parameter sets enable you to expose different parameters to the user.</span></span> <span data-ttu-id="dc8da-105">És ha a felhasználó által megadott paraméterek alapján különböző adatokat szeretne visszaadni.</span><span class="sxs-lookup"><span data-stu-id="dc8da-105">And, to return different information based on the parameters specified by the user.</span></span>

## <a name="examples-of-parameter-sets"></a><span data-ttu-id="dc8da-106">Példák a paraméterek készletére</span><span class="sxs-lookup"><span data-stu-id="dc8da-106">Examples of parameter sets</span></span>

<span data-ttu-id="dc8da-107">A PowerShell `Get-EventLog` -parancsmag például különböző adatokat ad vissza attól függően, hogy a felhasználó megadja-e a **listát** vagy a **LogName** paramétert.</span><span class="sxs-lookup"><span data-stu-id="dc8da-107">For example, the PowerShell `Get-EventLog` cmdlet returns different information depending on whether the user specifies the **List** or **LogName** parameter.</span></span> <span data-ttu-id="dc8da-108">Ha meg van adva a **List** paraméter, a parancsmag magára a naplófájlokra vonatkozó adatokat ad vissza, de nem tartalmazza a bennük lévő esemény adatait.</span><span class="sxs-lookup"><span data-stu-id="dc8da-108">If the **List** parameter is specified, the cmdlet returns information about the log files themselves but not the event information they contain.</span></span> <span data-ttu-id="dc8da-109">Ha a **LogName** paraméter meg van adva, a parancsmag adatokat ad vissza egy adott Eseménynapló eseményeiről.</span><span class="sxs-lookup"><span data-stu-id="dc8da-109">If the **LogName** parameter is specified, the cmdlet returns information about the events in a specific event log.</span></span> <span data-ttu-id="dc8da-110">A **lista** -és **LogName** paraméterek két különálló paramétert azonosítanak.</span><span class="sxs-lookup"><span data-stu-id="dc8da-110">The **List** and **LogName** parameters identify two separate parameter sets.</span></span>

## <a name="unique-parameter"></a><span data-ttu-id="dc8da-111">Egyedi paraméter</span><span class="sxs-lookup"><span data-stu-id="dc8da-111">Unique parameter</span></span>

<span data-ttu-id="dc8da-112">Minden paraméter-készletnek egyedi paraméterrel kell rendelkeznie, amelyet a PowerShell-futtatókörnyezet a megfelelő beállításhalmaz számára tesz elérhetővé.</span><span class="sxs-lookup"><span data-stu-id="dc8da-112">Each parameter set must have a unique parameter that the PowerShell runtime uses to expose the appropriate parameter set.</span></span> <span data-ttu-id="dc8da-113">Ha lehetséges, az egyedi paraméternek kötelező paraméternek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="dc8da-113">If possible, the unique parameter should be a mandatory parameter.</span></span> <span data-ttu-id="dc8da-114">Ha egy paraméter megadása kötelező, a felhasználónak meg kell adnia a paramétert, a PowerShell-futtatókörnyezet pedig ezt a paramétert használja a beállított paraméterek azonosítására.</span><span class="sxs-lookup"><span data-stu-id="dc8da-114">When a parameter is mandatory, the user must specify the parameter, and the PowerShell runtime uses that parameter to identify the parameter set.</span></span> <span data-ttu-id="dc8da-115">Az egyedi paraméter nem lehet kötelező, ha a parancsmagot paraméterek megadása nélkül tervezték futtatni.</span><span class="sxs-lookup"><span data-stu-id="dc8da-115">The unique parameter can't be mandatory if your cmdlet is designed to run without specifying any parameters.</span></span>

## <a name="multiple-parameter-sets"></a><span data-ttu-id="dc8da-116">Több paraméter-készlet</span><span class="sxs-lookup"><span data-stu-id="dc8da-116">Multiple parameter sets</span></span>

<span data-ttu-id="dc8da-117">A következő ábrán a bal oldali oszlop három érvényes paraméter-készletet jelenít meg.</span><span class="sxs-lookup"><span data-stu-id="dc8da-117">In the following illustration, the left column shows three valid parameter sets.</span></span> <span data-ttu-id="dc8da-118">Az **a paraméter** az első beállításhalmaz esetében egyedi, a **B paraméter** egyedi a második paraméter számára, és a **C paraméter** egyedi a harmadik paraméter készletében.</span><span class="sxs-lookup"><span data-stu-id="dc8da-118">**Parameter A** is unique to the first parameter set, **parameter B** is unique to the second parameter set, and **parameter C** is unique to the third parameter set.</span></span> <span data-ttu-id="dc8da-119">A jobb oldali oszlopban a paraméterek nem rendelkeznek egyedi paraméterrel.</span><span class="sxs-lookup"><span data-stu-id="dc8da-119">In the right column, the parameter sets don't have a unique parameter.</span></span>

![ps_parametersets](../media/ps-parametersets.gif)

## <a name="parameter-set-requirements"></a><span data-ttu-id="dc8da-121">Paraméterek beállítása – követelmények</span><span class="sxs-lookup"><span data-stu-id="dc8da-121">Parameter set requirements</span></span>

<span data-ttu-id="dc8da-122">Az alábbi követelmények minden paraméter-készletre érvényesek.</span><span class="sxs-lookup"><span data-stu-id="dc8da-122">The following requirements apply to all parameter sets.</span></span>

- <span data-ttu-id="dc8da-123">Minden paraméter-készletnek legalább egy egyedi paraméterrel kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="dc8da-123">Each parameter set must have at least one unique parameter.</span></span> <span data-ttu-id="dc8da-124">Ha lehetséges, ezt a paramétert kötelező paraméterként hajtsa végre.</span><span class="sxs-lookup"><span data-stu-id="dc8da-124">If possible, make this parameter a mandatory parameter.</span></span>

- <span data-ttu-id="dc8da-125">A több pozíciós paramétert tartalmazó paraméterérték egyedi pozíciókat kell meghatároznia az egyes paraméterekhez.</span><span class="sxs-lookup"><span data-stu-id="dc8da-125">A parameter set that contains multiple positional parameters must define unique positions for each parameter.</span></span> <span data-ttu-id="dc8da-126">A két pozíciós paraméter nem adhat meg ugyanazt a pozíciót.</span><span class="sxs-lookup"><span data-stu-id="dc8da-126">No two positional parameters can specify the same position.</span></span>

- <span data-ttu-id="dc8da-127">Egy készleten belül csak egy paraméter deklarálhatja a `ValueFromPipeline` kulcsszót a következő `true`értékkel:.</span><span class="sxs-lookup"><span data-stu-id="dc8da-127">Only one parameter in a set can declare the `ValueFromPipeline` keyword with a value of `true`.</span></span>
  <span data-ttu-id="dc8da-128">Több paraméter is meghatározhatja `ValueFromPipelineByPropertyName` a kulcsszó `true`értékét.</span><span class="sxs-lookup"><span data-stu-id="dc8da-128">Multiple parameters can define the `ValueFromPipelineByPropertyName` keyword with a value of `true`.</span></span>

- <span data-ttu-id="dc8da-129">Ha nem ad meg paramétert egy paraméterhez, a paraméter az összes paraméter-készlethez tartozik.</span><span class="sxs-lookup"><span data-stu-id="dc8da-129">If no parameter set is specified for a parameter, the parameter belongs to all parameter sets.</span></span>

> [!NOTE]
> <span data-ttu-id="dc8da-130">Parancsmagok vagy függvények esetén a 32-es paraméterek száma korlátozott.</span><span class="sxs-lookup"><span data-stu-id="dc8da-130">For a cmdlet or function, there is a limit of 32 parameter sets.</span></span>

## <a name="default-parameter-sets"></a><span data-ttu-id="dc8da-131">Alapértelmezett paraméter-készletek</span><span class="sxs-lookup"><span data-stu-id="dc8da-131">Default parameter sets</span></span>

<span data-ttu-id="dc8da-132">Ha több paraméterérték van definiálva, `DefaultParameterSetName` a **parancsmag** attribútum kulcsszava segítségével megadhatja az alapértelmezett paramétert.</span><span class="sxs-lookup"><span data-stu-id="dc8da-132">When multiple parameter sets are defined, you can use the `DefaultParameterSetName` keyword of the **Cmdlet** attribute to specify the default parameter set.</span></span> <span data-ttu-id="dc8da-133">A PowerShell az alapértelmezett paramétert használja, ha nem tudja meghatározni a használni kívánt paramétert a parancs által megadott információk alapján.</span><span class="sxs-lookup"><span data-stu-id="dc8da-133">PowerShell uses the default parameter set if it can't determine the parameter set to use based on the information provided by the command.</span></span> <span data-ttu-id="dc8da-134">További információ a **parancsmag** attribútumáról: parancsmag- [attribútum deklarációja](./cmdlet-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="dc8da-134">For more information about the **Cmdlet** attribute, see [Cmdlet Attribute Declaration](./cmdlet-attribute-declaration.md).</span></span>

## <a name="declaring-parameter-sets"></a><span data-ttu-id="dc8da-135">Paraméter-készletek deklarálása</span><span class="sxs-lookup"><span data-stu-id="dc8da-135">Declaring parameter sets</span></span>

<span data-ttu-id="dc8da-136">A beállításhalmaz létrehozásához meg kell adnia a `ParameterSetName` kulcsszót, amikor deklarálja a paraméter **attribútumot** a paraméterben szereplő minden paraméterhez.</span><span class="sxs-lookup"><span data-stu-id="dc8da-136">To create a parameter set, you must specify the `ParameterSetName` keyword when you declare the **Parameter** attribute for every parameter in the parameter set.</span></span> <span data-ttu-id="dc8da-137">Több paraméterhez **tartozó paramétereknél adjon hozzá egy Parameters** attribútumot az egyes paraméterekhez.</span><span class="sxs-lookup"><span data-stu-id="dc8da-137">For parameters that belong to multiple parameter sets, add a **Parameter** attribute for each parameter set.</span></span> <span data-ttu-id="dc8da-138">Ez az attribútum lehetővé teszi, hogy a paramétert az egyes beállított paraméterektől eltérően határozza meg.</span><span class="sxs-lookup"><span data-stu-id="dc8da-138">This attribute enables you to define the parameter differently for each parameter set.</span></span> <span data-ttu-id="dc8da-139">Megadhat például egy paramétert kötelezőként egy készletben, és opcionálisan egy másikban.</span><span class="sxs-lookup"><span data-stu-id="dc8da-139">For example, you can define a parameter as mandatory in one set and optional in another.</span></span> <span data-ttu-id="dc8da-140">Azonban minden egyes paraméternek egy egyedi paramétert kell tartalmaznia.</span><span class="sxs-lookup"><span data-stu-id="dc8da-140">However, each parameter set must contain one unique parameter.</span></span> <span data-ttu-id="dc8da-141">További információ: paraméter- [attribútum deklarációja](parameter-attribute-declaration.md).</span><span class="sxs-lookup"><span data-stu-id="dc8da-141">For more information, see [Parameter Attribute Declaration](parameter-attribute-declaration.md).</span></span>

<span data-ttu-id="dc8da-142">A következő példában a **username** paraméter a set `Test01` paraméter egyedi paramétere, a **számítógépnév** paraméter `Test02` pedig a beállított paraméter egyedi paramétere.</span><span class="sxs-lookup"><span data-stu-id="dc8da-142">In the following example, the **UserName** parameter is the unique parameter of the `Test01` parameter set, and the **ComputerName** parameter is the unique parameter of the `Test02` parameter set.</span></span> <span data-ttu-id="dc8da-143">A **SharedParam** paraméter mindkét készlethez tartozik, és kötelező `Test01` megadni a paramétert, `Test02` de a paraméter értéke nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="dc8da-143">The **SharedParam** parameter belongs to both sets and is mandatory for the `Test01` parameter set but optional for the `Test02` parameter set.</span></span>

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
private string sharedParam;
```
