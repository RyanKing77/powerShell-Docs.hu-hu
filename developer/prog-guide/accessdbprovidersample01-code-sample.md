---
title: Kódminta AccessDbProviderSample01 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 35540d2a-c18f-4179-b869-1a3dc5a8c1bd
caps.latest.revision: 6
ms.openlocfilehash: 01b95e18794501c2aff13d1e51b7400ae6fb8730
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849377"
---
# <a name="accessdbprovidersample01-code-sample"></a>AccessDbProviderSample01 – kódminta

A következő kód bemutatja a Windows PowerShell-szolgáltatóban ismertetett végrehajtásának [alapvető Windows PowerShell-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md). Ez a megvalósítás indítása és leállítása a szolgáltató módszert biztosít, és bár nem biztosít egy azt jelenti, hogy egy adattár eléréséhez, vagy a, vagy állítsa be az adatokat az adattárban, azt adja meg az összes szükséges alapvető funkciókkal.

> [!NOTE]
> Letöltheti a C# forrásfájl (AccessDBSampleProvider01.cs) a szolgáltató Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
>
> A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.
>
> Más Windows PowerShell-szolgáltató esetében kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).

## <a name="code-sample"></a>Kódminta

[!code-csharp[AccessDBProviderSample01.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample01/AccessDBProviderSample01.cs#L11-L30 "AccessDBProviderSample01.cs")]

## <a name="see-also"></a>Lásd még:

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)