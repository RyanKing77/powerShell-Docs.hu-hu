---
title: RunSpace03 (C#) kód minta | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9ac8ab99-1856-4d6f-b30d-c0a18b8dd1fc
caps.latest.revision: 6
ms.openlocfilehash: 9afdb97b8ae2919f091ca5bacccedbe37c2e1584
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848026"
---
# <a name="runspace03-c-code-sample"></a>Runspace03 (C#) – Kódminta

Itt látható a C# "megadott parancsfájlt futtató konzolszoftver létrehozása" című témakörben ismertetett konzolos alkalmazás forráskódja. Ez a példa a [System. Management. Automation. Runspaceinvoke](/dotnet/api/System.Management.Automation.RunspaceInvoke) osztályt használja egy olyan parancsfájl végrehajtásához, amely lekéri a folyamat adatait a parancsfájlba átadott folyamat-nevek listájának használatával. Bemutatja, hogyan adhatók át bemeneti objektumok egy parancsfájlnak, valamint hogyan lehet lekérdezni a hibákat, valamint a kimeneti objektumokat.

> [!NOTE]
> A minta C# forrásfájljait (runspace03.cs) a Microsoft Windows szoftverfejlesztői készlettel töltheti le a Windows Vista és Microsoft .NET Framework 3,0 Runtime Components szolgáltatáshoz. A letöltési utasításokért lásd: a [Windows PowerShell telepítése és a Windows POWERSHELL SDK letöltése](/powershell/developer/installing-the-windows-powershell-sdk).
> A letöltött forrásfájlok a  **\<PowerShell-minták >** könyvtárban érhetők el.

## <a name="code-sample"></a>Mintakód

[!code-csharp[Runspace03.cs](../../powershell-sdk-samples/SDK-2.0/csharp/Runspace03/Runspace03.cs#L11-L88 "Runspace03.cs")]

## <a name="see-also"></a>Lásd még:

[A Windows PowerShell programozói útmutatója](./windows-powershell-programmer-s-guide.md)

[Windows PowerShell SDK](../windows-powershell-reference.md)