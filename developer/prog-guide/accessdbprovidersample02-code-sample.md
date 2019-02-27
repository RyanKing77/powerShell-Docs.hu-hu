---
title: Kódminta AccessDbProviderSample02 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b89a4903-3efc-4b08-9b20-2baadf1d1b66
caps.latest.revision: 6
ms.openlocfilehash: 22a7bdf43a294d1e28f78ccf3412173892fdd53e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847270"
---
# <a name="accessdbprovidersample02-code-sample"></a>AccessDbProviderSample02 – kódminta

A következő kód bemutatja a Windows PowerShell-szolgáltatóban ismertetett végrehajtásának [egy Windows PowerShell-meghajtó szolgáltató létrehozása](./creating-a-windows-powershell-drive-provider.md). Ez a megvalósítás egy elérési utat hoz létre, az Access-adatbázisok kapcsolatot hoz létre, és majd eltávolítja a meghajtó.

> [!NOTE]
> Letöltheti a C# forrásfájl (AccessDBSampleProvider02.cs) a szolgáltató a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
> Letöltheti a C# forrásfájl (AccessDBSampleProvider02.cs) a szolgáltató a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
>
> A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.
>
> Más Windows PowerShell-szolgáltató esetében kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).

## <a name="code-sample"></a>Kódminta

[!code-csharp[AccessDBProviderSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs#L11-L154 "AccessDBProviderSample02.cs")]


## <a name="see-also"></a>Lásd még:

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)