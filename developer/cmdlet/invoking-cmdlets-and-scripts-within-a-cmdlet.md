---
title: Parancsmagokkal és parancsfájlokkal belül egy parancsmag meghívása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e7040a5c-4a47-42df-a2ea-96b134a4ed9b
caps.latest.revision: 10
ms.openlocfilehash: f20708ff41d9a6de90090997a875ba5371eccd74
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067671"
---
# <a name="invoking-cmdlets-and-scripts-within-a-cmdlet"></a>Parancsmagok és szkriptek meghívása parancsmagokon belül

A parancsmag hívhat meg más parancsmagok és parancsfájlok a feldolgozási mód a parancsmag bemeneti adatban. Ez lehetővé teszi, hogy a meglévő parancsmagokkal és parancsfájlokkal funkcióit a parancsmaghoz a kód nélkül.

## <a name="the-invoke-method"></a>A metódus meghívása

Minden parancsmag hívhat meg egy meglévő parancsmag meghívásával a [System.Management.Automation.Cmdlet.Invoke](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) metodu z pracovního módszer, például a feldolgozása egy bemeneti [ System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing), amely pedig a parancsmag által felülbírálható. Csak azok a parancsmagok, amelyek közvetlenül az hajthatók ugyanakkor a [System.Management.Automation.Cmdlet](/dotnet/api/System.Management.Automation.Cmdlet) osztály. Nelze vyvolat származó parancsmag a [System.Management.Automation.PSCmdlet](/dotnet/api/System.Management.Automation.PSCmdlet) osztály.

A [System.Management.Automation.Cmdlet.Invoke*](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) módszernek a következő variantní hodnoty.

[System.Management.Automation.Cmdlet.Invoke](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) ez változat hívja meg a parancsmag objektum és a "T" típusú objektumok gyűjteményét adja vissza.

[System.Management.Automation.Cmdlet.Invoke](/dotnet/api/System.Management.Automation.Cmdlet.Invoke) a változat a parancsmag objektumot hív meg, és egy szigorúan típusos emumerator adja vissza. Ez a változó lehetővé teszi, hogy a felhasználó használja az objektumok a gyűjteményben lévő egyéni műveletek végrehajtásához.

## <a name="examples"></a>Példák

|Példa|Leírás|
|-------------|-----------------|
|[Parancsmagok belül egy parancsmag meghívása](./how-to-invoke-a-cmdlet-from-within-a-cmdlet.md)|Ez a példa bemutatja, hogyan belül egy másik parancsmag a parancsmag meghívása.|
|[Parancsfájlok belül egy parancsmag meghívása](./how-to-invoke-scripts-within-a-cmdlet.md)|Ez a példa bemutatja, hogyan meghívni a parancsmagnak a belül egy másik parancsmag megadott parancsfájl.|

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
