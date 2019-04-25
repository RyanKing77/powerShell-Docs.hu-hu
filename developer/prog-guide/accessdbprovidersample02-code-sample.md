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
ms.openlocfilehash: 67a169bfac0b0fc90e6ccd276d3d3592d1b70bb0
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082028"
---
# <a name="accessdbprovidersample02-code-sample"></a><span data-ttu-id="08739-102">AccessDbProviderSample02 – kódminta</span><span class="sxs-lookup"><span data-stu-id="08739-102">AccessDbProviderSample02 Code Sample</span></span>

<span data-ttu-id="08739-103">A következő kód bemutatja a Windows PowerShell-szolgáltatóban ismertetett végrehajtásának [egy Windows PowerShell-meghajtó szolgáltató létrehozása](./creating-a-windows-powershell-drive-provider.md).</span><span class="sxs-lookup"><span data-stu-id="08739-103">The following code shows the implementation of the Windows PowerShell provider described in [Creating a Windows PowerShell Drive Provider](./creating-a-windows-powershell-drive-provider.md).</span></span> <span data-ttu-id="08739-104">Ez a megvalósítás egy elérési utat hoz létre, az Access-adatbázisok kapcsolatot hoz létre, és majd eltávolítja a meghajtó.</span><span class="sxs-lookup"><span data-stu-id="08739-104">This implementation creates a path, makes a connection to an Access database, and then removes the drive.</span></span>

> [!NOTE]
> <span data-ttu-id="08739-105">Letöltheti a C# forrásfájl (AccessDBSampleProvider02.cs) a szolgáltató a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="08739-105">You can download the C# source file (AccessDBSampleProvider02.cs) for this provider using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="08739-106">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="08739-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="08739-107">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="08739-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>
>
> <span data-ttu-id="08739-108">Más Windows PowerShell-szolgáltató esetében kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).</span><span class="sxs-lookup"><span data-stu-id="08739-108">For more information about other Windows PowerShell provider implementations, see [Designing Your Windows PowerShell Provider](./designing-your-windows-powershell-provider.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="08739-109">Kódminta</span><span class="sxs-lookup"><span data-stu-id="08739-109">Code Sample</span></span>

[!code-csharp[AccessDBProviderSample02.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs#L11-L154 "AccessDBProviderSample02.cs")]


## <a name="see-also"></a><span data-ttu-id="08739-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="08739-110">See Also</span></span>

[<span data-ttu-id="08739-111">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="08739-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="08739-112">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="08739-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)