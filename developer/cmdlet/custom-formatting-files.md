---
title: Egyéni formázás fájlok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 85d27545-8097-4010-9947-6d8b3ce2eac0
caps.latest.revision: 15
ms.openlocfilehash: 71c1c181058c5646c817b90d9832976a78c6c7de
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850035"
---
# <a name="custom-formatting-files"></a><span data-ttu-id="2fb2d-102">Egyéni formázási fájlok</span><span class="sxs-lookup"><span data-stu-id="2fb2d-102">Custom Formatting Files</span></span>

<span data-ttu-id="2fb2d-103">A megjelenítési formátumának parancsmagok, függvények és parancsfájlok által visszaadott objektumokhoz definiált formázási fájlok (format.ps1xml) használatával.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-103">The display format for the objects returned by cmdlets, functions, and scripts are defined using formatting files (format.ps1xml files).</span></span> <span data-ttu-id="2fb2d-104">Ezek a fájlok számos Windows PowerShell használatával határozza meg azokat az objektumokat Windows PowerShell-parancsmagok által visszaadott alapértelmezett megjelenítési formátumát által biztosított.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-104">Several of these files are provided by Windows PowerShell to define the default display format for those objects returned by Windows PowerShell cmdlets.</span></span> <span data-ttu-id="2fb2d-105">Azonban a saját egyéni formázási fájlok felülírja az alapértelmezett megjelenítési formátum vagy meghatározásához a saját parancs által visszaadott objektumokhoz megjelenítését is létrehozhat.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-105">However, you can also create your own custom formatting files to overwrite the default display formats or to define the display of objects returned by your own commands.</span></span>

<span data-ttu-id="2fb2d-106">Windows PowerShell a formázási ezeket a fájlokat az adatok segítségével határozza meg, mi jelenjen meg, és az adatok formázását.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-106">Windows PowerShell uses the data in these formatting files to determine what is displayed and how the data is formatted.</span></span> <span data-ttu-id="2fb2d-107">A megjelenített adatok tartalmazhatnak egy objektum tulajdonságait, vagy parancsprogram-blokkot értékét.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-107">The displayed data can include the properties of an object or the value of a script block.</span></span>  <span data-ttu-id="2fb2d-108">Parancsfájl-blokkokban használhatók, ha azt szeretné, néhány érték, amely nem érhető el az objektum tulajdonságainak megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-108">Script blocks are used if you want to display some value that is not available directly from the properties of an object.</span></span> <span data-ttu-id="2fb2d-109">Például előfordulhat, hogy szeretné adjon hozzá egy objektum két tulajdonság értékét, és egy különálló adat, az eredményt jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-109">For example, you may want to add the value of two properties of an object and display the sum as a separate piece of data.</span></span> <span data-ttu-id="2fb2d-110">Saját formázás fájl írásakor meg kell határoznia *nézetek* megjeleníteni kívánt objektumokra vonatkozóan.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-110">When you write your own formatting file, you will need to define *views* for the objects that you want to display.</span></span> <span data-ttu-id="2fb2d-111">Megadhatja, hogy egyetlen nézetben minden objektum esetén, meghatározhatja, hogy egyetlen nézetben több objektumon, vagy megadhat több nézetet ugyanahhoz az objektumhoz.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-111">You can define a single view for each object, you can define a single view for multiple objects, or you can define multiple views for the same object.</span></span> <span data-ttu-id="2fb2d-112">Nincs nem definiálható nézetek száma nincs korlátozva.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-112">There is no limit to the number of views that you can define.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fb2d-113">Formázási fájlokat nem határozzák meg a folyamat visszaadott objektum elemét.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-113">Formatting files do not determine the elements of an object that are returned to the pipeline.</span></span> <span data-ttu-id="2fb2d-114">A folyamat számára ad vissza egy objektumot, amikor az objektum összes tagja érhetők el.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-114">When an object is returned to the pipeline, all members of that object are available.</span></span>

## <a name="format-views"></a><span data-ttu-id="2fb2d-115">Formátum nézetek</span><span class="sxs-lookup"><span data-stu-id="2fb2d-115">Format Views</span></span>

<span data-ttu-id="2fb2d-116">Formázási nézetek objektumokat megjelenítheti táblázatos formában, a lista formájában, a széles formátumban és a egy egyéni formátum.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-116">Formatting views can display objects in a table format, a list format, a wide format, and a custom format.</span></span> <span data-ttu-id="2fb2d-117">Az esetek többségében minden egyes formázási definíció nézet leíró XML-címkék csoportja által leírása.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-117">For the most part, each formatting definition is described by a set of XML tags that describe a view.</span></span> <span data-ttu-id="2fb2d-118">Mindegyik nézetről tartalmaz a nézet nevét az objektumok, amelyek a nézet és az elemek a nézetet, például az oszlopok és sorok információk a táblázatos nézetre.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-118">Each view contains the name of the view, the objects that use the view, and the elements of the view, such as the column and row information for a table view.</span></span>

<span data-ttu-id="2fb2d-119">A következő nézetek érhetők el.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-119">The following views are available.</span></span>

<span data-ttu-id="2fb2d-120">Tábla nézet egy objektum vagy egy parancsfájl blokk értéket egy vagy több oszlop tulajdonságai szerepelnek.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-120">Table view Lists the properties of an object or a script block value in one or more columns.</span></span> <span data-ttu-id="2fb2d-121">Minden oszlop egy tulajdonság az objektum vagy egy parancsfájl blokk értéket képvisel.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-121">Each column represents a property of the object or a script block value.</span></span> <span data-ttu-id="2fb2d-122">Egy objektum vagy a tulajdonságok és parancsfájl-blokk értékek kombinációjának a tulajdonságok egy részének objektum tulajdonságait megjelenítő táblázat nézet határozhatja meg.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-122">You can define a table view that displays all the properties of an object, a subset of the properties of an object, or a combination of properties and script block values.</span></span> <span data-ttu-id="2fb2d-123">A táblázat minden egyes sorára jelenti. a visszaadott objektum.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-123">Each row of the table represents a returned object.</span></span> <span data-ttu-id="2fb2d-124">Ez a nézet kapcsolatos további információkért lásd: [táblázatos nézetre](../format/creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="2fb2d-124">For more information about this view, see [Table View](../format/creating-a-table-view.md).</span></span>

<span data-ttu-id="2fb2d-125">Listanézet-objektum vagy egy parancsfájl blokk érték csak egy oszlop tulajdonságok listája.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-125">List view Lists the properties of an object or a script block value in a single column.</span></span> <span data-ttu-id="2fb2d-126">A lista minden egyes sorára egy nem kötelező címke vagy a tulajdonságot vagy parancsfájl-blokk értékét a tulajdonság nevét jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-126">Each row of the list displays an optional label or the property name followed by the value of the property or script block.</span></span> <span data-ttu-id="2fb2d-127">Ez a nézet kapcsolatos további információkért lásd: [listanézet](../format/creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="2fb2d-127">For more information about this view, see [List View](../format/creating-a-list-view.md).</span></span>

<span data-ttu-id="2fb2d-128">Széles nézet egy objektum vagy egy parancsfájl blokk értéket egy vagy több oszlop egyetlen tulajdonságát sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-128">Wide view Lists a single property of an object or a script block value in one or more columns.</span></span> <span data-ttu-id="2fb2d-129">Nincs címke vagy fejléc ehhez a nézethez.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-129">There is no label or header for this view.</span></span> <span data-ttu-id="2fb2d-130">Ez a nézet kapcsolatos további információkért lásd: [széles nézet](../format/creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="2fb2d-130">For more information about this view, see [Wide View](../format/creating-a-wide-view.md).</span></span>

<span data-ttu-id="2fb2d-131">Egyéni nézet nézetet jelenít meg egy testre szabható objektum tulajdonságai vagy parancsfájl-blokk értékek, amelyek nem követi a nézetek, a nézetek és a széles körű nézetek merev struktúráját.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-131">Custom view Displays a customizable view of object properties or script block values that does not adhere to the rigid structure of table views, list views, or wide views.</span></span> <span data-ttu-id="2fb2d-132">Meghatározhat egy különálló egyéni nézetet, vagy megadhat egy egyéni nézet, amelyet egy másik nézetre, például egy táblázat vagy lista nézetben.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-132">You can define a standalone custom view, or you can define a custom view that is used by another view, such as a table view or list view.</span></span> <span data-ttu-id="2fb2d-133">Ez a nézet kapcsolatos további információkért lásd: [egyéni nézet](../format/creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="2fb2d-133">For more information about this view, see [Custom View](../format/creating-custom-controls.md).</span></span>

## <a name="view-xml-elements"></a><span data-ttu-id="2fb2d-134">XML-elemek megtekintése</span><span class="sxs-lookup"><span data-stu-id="2fb2d-134">View XML Elements</span></span>

<span data-ttu-id="2fb2d-135">Az alábbi példa bemutatja a táblázatos nézetre, amely tartalmazza a két oszlopot definiáló XML-címkéket.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-135">The following example shows the XML tags used to define a table view that contains two columns.</span></span> <span data-ttu-id="2fb2d-136">A [ViewDefinitions](../format/viewdefinitions-element-format.md) elem a tároló eleme a formázási fájlban meghatározott összes nézetben megtekinthetők.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-136">The [ViewDefinitions](../format/viewdefinitions-element-format.md) element is the container element for all the views defined in the formatting file.</span></span> <span data-ttu-id="2fb2d-137">A [nézet](../format/view-element-format.md) elem definiálja az adott tábla, list, szélesre vagy egyéni nézet.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-137">The [View](../format/view-element-format.md) element defines the specific table, list, wide, or custom view.</span></span> <span data-ttu-id="2fb2d-138">Minden egyes nézetben a [neve](../format/name-element-for-view-format.md) elem nevét adja meg a nézet a [ViewSelectedBy](../format/viewselectedby-element-format.md) elem definiálja, amelyek a nézetet, és a más típusú vezérlőelem elemeket az objektumok (például a `TableControl` elem) határozza meg a nézet formátumát.</span><span class="sxs-lookup"><span data-stu-id="2fb2d-138">Within each view, the [Name](../format/name-element-for-view-format.md) element specifies the name of the view, the [ViewSelectedBy](../format/viewselectedby-element-format.md) element defines the objects that use the view, and the different control elements (such as the `TableControl` element) define the format of the view.</span></span>

```xml
ViewDefinitions
  <View>
    <Name>Name of View</Name>
    <ViewSelectedBy>
      <TypeName>Object to display using this view</TypeName>
      <TypeName>Object to display using this view</TypeName>
    </ViewSelectedBy>
    <TableControl>
      <TableHeaders>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
      </TableHeaders>
      <TableRowEntries>
        <TableRowEntry>
          <TableColumnItems>
            <TableColumnItem>
              <PropertyName>Header for column 1</PropertyName>
            </TableColumnItem>
            <TableColumnItem>
              <PropertyName>Header for column 2</PropertyName>
            </TableColumnItem>
          </TableColumnItems>
        </TableRowEntry>
      </TableRowEntries>
    </TableControl)
  </View>
</ViewDefinitions>

```

## <a name="see-also"></a><span data-ttu-id="2fb2d-139">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2fb2d-139">See Also</span></span>

[<span data-ttu-id="2fb2d-140">Tábla nézet</span><span class="sxs-lookup"><span data-stu-id="2fb2d-140">Table View</span></span>](../format/creating-a-table-view.md)

[<span data-ttu-id="2fb2d-141">Listanézet</span><span class="sxs-lookup"><span data-stu-id="2fb2d-141">List View</span></span>](../format/creating-a-list-view.md)

[<span data-ttu-id="2fb2d-142">Széles nézet</span><span class="sxs-lookup"><span data-stu-id="2fb2d-142">Wide View</span></span>](../format/creating-a-wide-view.md)

[<span data-ttu-id="2fb2d-143">Egyéni nézet</span><span class="sxs-lookup"><span data-stu-id="2fb2d-143">Custom View</span></span>](../format/creating-custom-controls.md)

[<span data-ttu-id="2fb2d-144">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="2fb2d-144">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)
