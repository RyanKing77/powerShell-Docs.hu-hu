---
title: RunSpace03 (C#) kódminta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9ac8ab99-1856-4d6f-b30d-c0a18b8dd1fc
caps.latest.revision: 6
ms.openlocfilehash: d2e5b8c0a7622481bfca21d5c5b46afa01c02d2c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56852079"
---
# <a name="runspace03-c-code-sample"></a>Runspace03 (C#) – Kódminta

Íme a C# forráskódját el a konzolalkalmazást ismertetett [létrehozása egy Console Application, hogy fut a megadott parancsfájl](http://msdn.microsoft.com/en-us/a93e6006-36db-4bcc-b9da-c5bebf4ffd68). Ebben a példában a [System.Management.Automation.Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) osztály végrehajtani egy parancsfájlt, amely lekéri a szkriptbe folyamat Névlista használatával dolgozza fel adatokat. Bemutatja, hogyan adhatók át a bemeneti objektumok egy parancsfájlt, és hogyan kérheti le a hiba objektumokat, valamint a kimeneti objektumok.

> [!NOTE]
> Letöltheti a C# forrásfájl (runspace03.cs) ehhez a mintához a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
> Letöltheti a C# forrásfájl (runspace03.cs) ehhez a mintához a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
>
> A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.

## <a name="code-sample"></a>Kódminta

[!code-csharp[Runspace03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace03/Runspace03.cs#L11-L88 "Runspace03.cs")]

## <a name="see-also"></a>Lásd még:

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)