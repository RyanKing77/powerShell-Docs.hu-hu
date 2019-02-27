---
title: Kódminta RunSpace05 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9688cd69-07ea-4ea0-8822-0a4850bcf86c
caps.latest.revision: 7
ms.openlocfilehash: 2b5ac097e8a52832b0f8cfb93b84eef56fc64858
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845828"
---
# <a name="runspace05-code-sample"></a>Runspace05 – Kódminta

Íme a forráskódot a Runspace05 minta leírt [konfigurálása a futási teret használ RunspaceConfiguration](http://msdn.microsoft.com/en-us/42681d19-2d05-4975-befd-afb1990e79b2). Ez a példa bemutatja, hogyan létrehozása a futási térben konfigurációs adatokat, hozzon létre egy futási teret, hozzon létre egy folyamatot egyetlen paranccsal és ezután hajtsa végre a folyamat. A végrehajtott parancs a `Get-Process` parancsmagot.

> [!NOTE]
> Letöltheti a C# forrásfájl (runspace05.cs) a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
> Letöltheti a C# forrásfájl (runspace05.cs) a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
>
> A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.

## <a name="code-sample"></a>Kódminta

[!code-csharp[Runspace05.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace05/Runspace05.cs#L11-L86 "Runspace05.cs")]

## <a name="see-also"></a>Lásd még:

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)