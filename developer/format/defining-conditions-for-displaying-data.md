---
title: Adatok megjelenítése feltételek meghatározása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c1e05821-6aec-437b-84a5-218a5727f88b
caps.latest.revision: 10
ms.openlocfilehash: 8a5b84b6a461e9fc340a5981578d95ca2ac6b9f7
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066328"
---
# <a name="defining-conditions-for-displaying-data"></a><span data-ttu-id="fa808-102">Adatok megjelenítésére vonatkozó feltételek definiálása</span><span class="sxs-lookup"><span data-stu-id="fa808-102">Defining Conditions for Displaying Data</span></span>

<span data-ttu-id="fa808-103">Nézet vagy egy vezérlőelem által megjelenített adatok meghatározásakor megadhat egy feltételt, amely a megjeleníteni kívánt adatok léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="fa808-103">When defining what data is displayed by a view or a control, you can specify a condition that must exist for the data to be displayed.</span></span> <span data-ttu-id="fa808-104">A feltétel is elindítható, egy adott tulajdonság, vagy ha egy parancsfájl vagy tulajdonság-érték kiértékelésének `true`.</span><span class="sxs-lookup"><span data-stu-id="fa808-104">The condition can be triggered by a specific property, or when a script or property value evaluates to `true`.</span></span> <span data-ttu-id="fa808-105">Amikor a kiválasztási feltétel teljesül, a nézet vagy a definíció szolgál.</span><span class="sxs-lookup"><span data-stu-id="fa808-105">When the selection condition is met, the definition of the view or control is used.</span></span>

## <a name="specifying-a-selection-condition-for-a-definition"></a><span data-ttu-id="fa808-106">Adja meg a definíciófrissítés számára kijelölt feltétel</span><span class="sxs-lookup"><span data-stu-id="fa808-106">Specifying a Selection Condition for a Definition</span></span>

<span data-ttu-id="fa808-107">Nézet vagy vezérlőben definícióját létrehozásakor a `EntrySelectedBy` elem azt adhatja meg, hogy mely objektumok fogja használni a definíció, vagy milyen feltételt a definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="fa808-107">When creating a definition for a view or control, the `EntrySelectedBy` element is used to specify which objects will use the definition or what condition must exist for the definition to be used.</span></span> <span data-ttu-id="fa808-108">A feltétel szerint van megadva a `SelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="fa808-108">The condition is specified by the `SelectionCondition` element.</span></span>

<span data-ttu-id="fa808-109">A következő példában egy táblázat nézet definíciójának kiválasztási feltétel van megadva.</span><span class="sxs-lookup"><span data-stu-id="fa808-109">In the following example, a selection condition is specified for a definition of a table view.</span></span> <span data-ttu-id="fa808-110">Ebben a példában a definíció használt, csak akkor, ha a megadott parancsfájl kiértékelése `true`.</span><span class="sxs-lookup"><span data-stu-id="fa808-110">In this example, the definition is used only when the specified script is evaluated to `true`.</span></span>

```xml
<TableRowEntry>
  <EntrySelectedBy>
    <SelectionCondition>
      <ScriptBlock>ScriptToEvaluate</ScriptBlock>
    </SelectionCondition>
  </EntrySelectedBy>
  <TableColumnItems>
  </TableColumnItems>
</TableRowEntry>

```

<span data-ttu-id="fa808-111">Kiválasztási feltételek definícióját a nézet vagy vezérlő megadható száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="fa808-111">There is no limit to the number of selection conditions that you can specify for a definition of a view or control.</span></span> <span data-ttu-id="fa808-112">A csak követelmények a következők:</span><span class="sxs-lookup"><span data-stu-id="fa808-112">The only requirements are the following:</span></span>

- <span data-ttu-id="fa808-113">A kiválasztási feltétel egy tulajdonság neve vagy a feltétel indítható parancsfájlt kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="fa808-113">The selection condition must specify one property name or script to trigger the condition, but cannot specify both.</span></span>

- <span data-ttu-id="fa808-114">A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="fa808-114">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

## <a name="specifying-a-selection-condition-for-an-item"></a><span data-ttu-id="fa808-115">Egy elem kiválasztási feltétel megadása</span><span class="sxs-lookup"><span data-stu-id="fa808-115">Specifying a Selection Condition for an Item</span></span>

<span data-ttu-id="fa808-116">Megadhatja azt is, ha egy elem a lista nézet vagy a vezérlő használja többek között a `ItemSelectionCondition` elem a cikk definíciójában.</span><span class="sxs-lookup"><span data-stu-id="fa808-116">You can also specify when an item of a list view or control is used by including the `ItemSelectionCondition` element in the item definition.</span></span> <span data-ttu-id="fa808-117">A következő példában egy elem a lista nézet kiválasztási feltétel van megadva.</span><span class="sxs-lookup"><span data-stu-id="fa808-117">In the following example, a selection condition is specified for an item of a list view.</span></span> <span data-ttu-id="fa808-118">Ebben a példában az elem csak akkor, ha a parancsfájl kiértékelése használt `true`.</span><span class="sxs-lookup"><span data-stu-id="fa808-118">In this example, the item is used only when the script is evaluated to `true`.</span></span>

```xml
<ListItem>
  <ItemSelectionCondition>
    <ScriptBlock>ScriptToEvaluate</ScriptBlock>
  </ItemSelectionCondition>
</ListItem>

```

<span data-ttu-id="fa808-119">Egy elem csak egy kijelölés feltételt is megadhat.</span><span class="sxs-lookup"><span data-stu-id="fa808-119">You can specify only one selection condition for an item.</span></span> <span data-ttu-id="fa808-120">És a feltétel egy tulajdonság neve vagy a feltétel indítható parancsfájlt kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="fa808-120">And the condition must specify one property name or script to trigger the condition, but cannot specify both.</span></span>

## <a name="xml-elements"></a><span data-ttu-id="fa808-121">XML-elemek</span><span class="sxs-lookup"><span data-stu-id="fa808-121">XML Elements</span></span>

 <span data-ttu-id="fa808-122">A következő XML-elemeket hozhat létre egy kiválasztási feltétel szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="fa808-122">The following XML elements are used to create a selection condition.</span></span>

- <span data-ttu-id="fa808-123">A következő elemeket adja meg a nézet definíciói kiválasztási feltételek:</span><span class="sxs-lookup"><span data-stu-id="fa808-123">The following elements specify selection conditions for view definitions:</span></span>

    - [<span data-ttu-id="fa808-124">A TableControl (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fa808-124">SelectionCondition Element for EntrySelectedBy for TableControl (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)

    - [<span data-ttu-id="fa808-125">A ListControl (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fa808-125">SelectionCondition Element for EntrySelectedBy for ListControl (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

    - [<span data-ttu-id="fa808-126">A WideControl (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fa808-126">SelectionCondition Element for EntrySelectedBy for WideControl (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

    - [<span data-ttu-id="fa808-127">A CustomControl (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fa808-127">SelectionCondition Element for EntrySelectedBy for CustomControl (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)

- <span data-ttu-id="fa808-128">A következő elemeket adja meg a kiválasztási feltételek a gyakori és a nézet definíciók szabályozhatja:</span><span class="sxs-lookup"><span data-stu-id="fa808-128">The following elements specify selection conditions for common and view control definitions:</span></span>

    - [<span data-ttu-id="fa808-129">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fa808-129">SelectionCondition Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-configuration-format.md)

    - [<span data-ttu-id="fa808-130">Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fa808-130">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)

- <span data-ttu-id="fa808-131">A következő elem azt határozza meg, a kiválasztási feltétel bővített gyűjtemény objektumok:</span><span class="sxs-lookup"><span data-stu-id="fa808-131">The following element specifies the selection condition for expanding collection objects:</span></span>

    - [<span data-ttu-id="fa808-132">A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fa808-132">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

- <span data-ttu-id="fa808-133">A következő elemet a kiválasztási feltétel az adatok új csoport megjelenítéséhez adja meg:</span><span class="sxs-lookup"><span data-stu-id="fa808-133">The following element specifies the selection condition for displaying a new group of data:</span></span>

    - [<span data-ttu-id="fa808-134">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fa808-134">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)

- <span data-ttu-id="fa808-135">A következő elem azt határozza meg, az adott nézet egy elem kiválasztási feltétel:</span><span class="sxs-lookup"><span data-stu-id="fa808-135">The following element specifies an item selection condition for a list view:</span></span>

    - [<span data-ttu-id="fa808-136">A ListControl (formátum) ListItem ItemSelectionCondition eleme</span><span class="sxs-lookup"><span data-stu-id="fa808-136">ItemSelectionCondition Element for ListItem for ListControl (Format)</span></span>](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md)

- <span data-ttu-id="fa808-137">A következő elemeket adja meg, hogy egy elem kiválasztási feltétel vezérlők:</span><span class="sxs-lookup"><span data-stu-id="fa808-137">The following elements specify an item selection condition for controls:</span></span>

    - [<span data-ttu-id="fa808-138">Konfiguráció (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fa808-138">ItemSelectionCondition Element for ExpressionBinding for Controls for Configuration (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-configuration-format.md)

    - [<span data-ttu-id="fa808-139">Nézet (formátum) vezérlők ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fa808-139">ItemSelectionCondition Element for ExpressionBinding for Controls for View (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-controls-for-view-format.md)

    - [<span data-ttu-id="fa808-140">A CustomControl (formátum) ExpressionBinding ItemSelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fa808-140">ItemSelectionCondition Element for ExpressionBinding for CustomControl (Format)</span></span>](./itemselectioncondition-element-for-expressionbinding-for-customcontrol-format.md)

## <a name="see-also"></a><span data-ttu-id="fa808-141">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="fa808-141">See Also</span></span>

[<span data-ttu-id="fa808-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="fa808-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
