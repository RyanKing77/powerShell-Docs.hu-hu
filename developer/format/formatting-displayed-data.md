---
title: Adatok formázása jelenik meg |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 38971643-2a3d-4f5b-a1fa-6334c162b8ed
caps.latest.revision: 4
ms.openlocfilehash: e915ac71feb50cb58cfa9195f0de94763affdb77
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846101"
---
# <a name="formatting-displayed-data"></a><span data-ttu-id="e0e16-102">Megjelenített adatok formázása</span><span class="sxs-lookup"><span data-stu-id="e0e16-102">Formatting Displayed Data</span></span>

<span data-ttu-id="e0e16-103">Megadhatja, hogy hogyan jelenjenek meg az egyes adatpontok a lista, táblázat vagy széles nézet.</span><span class="sxs-lookup"><span data-stu-id="e0e16-103">You can specify how the individual data points in your List, Table, or Wide view are displayed.</span></span> <span data-ttu-id="e0e16-104">Használhatja a `FormatString` elem a nézetet, vagy a cikkek meghatározásakor használhatja a `ScriptBlock` elem hívja a `FormatString` metódus az adatokon.</span><span class="sxs-lookup"><span data-stu-id="e0e16-104">You can use the `FormatString` element when defining the items of your view, or you can use the `ScriptBlock` element to call the `FormatString` method on the data.</span></span>

## <a name="using-the-formatstring-element"></a><span data-ttu-id="e0e16-105">A FormatString elem használatával</span><span class="sxs-lookup"><span data-stu-id="e0e16-105">Using the FormatString Element</span></span>

<span data-ttu-id="e0e16-106">Az alábbi példában az értéket, a `TotalProcessorTime` tulajdonságát a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum FormatString elemmel van formázva.</span><span class="sxs-lookup"><span data-stu-id="e0e16-106">In the following example the value of the `TotalProcessorTime` property of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object is formatted using the FormatString element.</span></span> <span data-ttu-id="e0e16-107">a `TotalProcessorTime` tulajdonság</span><span class="sxs-lookup"><span data-stu-id="e0e16-107">the `TotalProcessorTime` property</span></span>

```
<TableColumnItem>
  <PropertyName>TotalProcessorTime</PropertyName>
  <FormatString>{0:MMM}{0:dd}{0:HH}:{0:mm}</FormatString>
</TableColumnItem>
```



