---
title: Kódminta RunSpace08 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0f286201-8a02-4b00-9a2c-1b833ccdbdbf
caps.latest.revision: 7
ms.openlocfilehash: ec6aae544eafea1dedc1379dab00beeed2c7c436
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734916"
---
# <a name="runspace08-code-sample"></a>Runspace08 – Kódminta

Itt van a forráskódot a Runspace08 minta ismertetett [létrehozása egy Console Application, hogy hozzáadja a parancs paraméterei](https://msdn.microsoft.com/en-us/848b2b46-60f1-4a86-b448-cfc7c0cccfba). Ez a mintaalkalmazás egy futási teret hoz létre, létrehoz egy folyamatot, két parancsot a folyamat hozzáadja, két paramétert ad hozzá a második parancs és a folyamat végrehajtja. A folyamat hozzáadott parancsai a `Get-Process` és `Sort-Object` parancsmagok.

## <a name="code-sample"></a>Kódminta

[!code-csharp[Runspace08.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace08/Runspace08.cs#L11-L86 "Runspace08.cs")]

## <a name="see-also"></a>Lásd még:

[Windows PowerShell SDK](../windows-powershell-reference.md)