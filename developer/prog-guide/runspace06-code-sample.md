---
title: Kódminta RunSpace06 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d71f86d5-eb62-4b16-aa95-5fd3f314ffd3
caps.latest.revision: 6
ms.openlocfilehash: b6fdad90f7339e941d77646936b1b5952cd65500
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734931"
---
# <a name="runspace06-code-sample"></a>Runspace06 – Kódminta

Itt van a forráskódot a Runspace06 minta ismertetett [konfigurálása egy futási teret egy Windows PowerShell beépülő modullal](https://msdn.microsoft.com/en-us/a7289ee8-9732-49ee-91c7-d533e9538b83). Ez a mintaalkalmazás egy futási teret egy Windows PowerShell beépülő modul, amely majd használható egy folyamat futtatása egyetlen paranccsal alapján hoz létre. Ehhez az alkalmazás a futási térben konfigurációs adatokat hoz létre, létrehoz egy futási teret, létrehoz egy folyamatot egyetlen paranccsal és a folyamat végrehajtja.

> [!NOTE]
> Letöltheti a C# forrásfájl (runspace06.cs) a Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
>
> A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.

## <a name="code-sample"></a>Kódminta

[!code-csharp[Runspace06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace06/Runspace06.cs#L11-L85 "Runspace06.cs")]

## <a name="see-also"></a>Lásd még:

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)