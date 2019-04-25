---
title: Windows PowerShell API-minták |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 82df2cde-ba12-46d2-b6ec-da5455fd9b57
caps.latest.revision: 8
ms.openlocfilehash: a472f07cb24b0de8e5dcdfcaddd2802575318d7a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082583"
---
# <a name="windows-powershell-api-samples"></a>Windows PowerSheles API-minták

Ez a szakasz tartalmazza, amely bemutatja, hogyan hozhat létre, amelyek korlátozzák a funkciók futási terek, és hogyan aszinkron módon futtathat parancsokat a futási térben készlet használatával adja meg a futási terek mintakódot. Microsoft Visual Studio segítségével hozzon létre egy konzolalkalmazást, majd a kódot bemásolhatja a témakörei ebben a szakaszban a gazdaalkalmazást.

## <a name="in-this-section"></a>A szakasz tartalma

[PowerShell01 minta](./windows-powershell01-sample.md) Ez a példa bemutatja, hogyan használhatja egy [System.Management.Automation.Runspaces.Initialsessionstate](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) egy futási teret funkcióinak objektumot. Ez a minta kimenete bemutatja, hogyan korlátozhatja a nyelvmód futási térben személyes parancsmag megjelölni, hozzáadása és eltávolítása parancsmagok és szolgáltatók, a proxy parancsot, és további hozzáadása.

[PowerShell02 minta](./windows-powershell02-sample.md) Ez a példa bemutatja, hogyan futtathat parancsokat aszinkron módon történik a futási terek futási térben készlet használatával. A minta parancsok álló listát hoz létre, és majd futtatja azokat a parancsokat, amíg a Windows PowerShell motor megnyílik egy futási teret a készletből, szükség esetén.