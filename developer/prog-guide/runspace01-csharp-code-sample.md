---
title: Runspace01 (C#) kódminta |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d59f8b7c-e800-4633-aa5b-74d4c57e2706
caps.latest.revision: 6
ms.openlocfilehash: ab067485d70523a16493eb57170615ab300eaa98
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67735051"
---
# <a name="runspace01-c-code-sample"></a>Runspace01 (C#) – Kódminta

Íme a mintakódokat, a futási térben ismertetett [létrehozása egy Console Application, hogy fut a megadott parancs](/dotnet/csharp/programming-guide/inside-a-program/hello-world-your-first-program). Ehhez az alkalmazás hív meg egy futási teret, és ezután meghívja a parancsot. (Vegye figyelembe, hogy az alkalmazás nem ad meg futási térben konfigurációs adatokat, és nem, explicit módon hozza létre folyamat). A parancs, amely meghívja a `Get-Process` parancsmagot.

> [!NOTE]
> Letöltheti a C# a futási teret a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői forrásfájl (runspace01.cs). Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
>
> A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.

## <a name="code-sample"></a>Kódminta

[!code-csharp[Runspace01.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace01/Runspace01.cs#L11-L62 "Runspace01.cs")]

## <a name="see-also"></a>Lásd még:

[Windows PowerShell programozói útmutató](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)