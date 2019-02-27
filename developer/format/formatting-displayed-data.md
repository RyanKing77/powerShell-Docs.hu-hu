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
# <a name="formatting-displayed-data"></a>Megjelenített adatok formázása

Megadhatja, hogy hogyan jelenjenek meg az egyes adatpontok a lista, táblázat vagy széles nézet. Használhatja a `FormatString` elem a nézetet, vagy a cikkek meghatározásakor használhatja a `ScriptBlock` elem hívja a `FormatString` metódus az adatokon.

## <a name="using-the-formatstring-element"></a>A FormatString elem használatával

Az alábbi példában az értéket, a `TotalProcessorTime` tulajdonságát a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum FormatString elemmel van formázva. a `TotalProcessorTime` tulajdonság

```
<TableColumnItem>
  <PropertyName>TotalProcessorTime</PropertyName>
  <FormatString>{0:MMM}{0:dd}{0:HH}:{0:mm}</FormatString>
</TableColumnItem>
```



