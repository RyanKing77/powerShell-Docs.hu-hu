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
# <a name="accessdbprovidersample01-code-sample"></a><span data-ttu-id="9565c-102">AccessDbProviderSample01 – kódminta</span><span class="sxs-lookup"><span data-stu-id="9565c-102">AccessDbProviderSample01 Code Sample</span></span>

<span data-ttu-id="9565c-103">A következő kód bemutatja a Windows PowerShell-szolgáltatóban ismertetett végrehajtásának [alapvető Windows PowerShell-szolgáltató létrehozása](./creating-a-basic-windows-powershell-provider.md).</span><span class="sxs-lookup"><span data-stu-id="9565c-103">The following code shows the implementation of the Windows PowerShell provider described in [Creating a Basic Windows PowerShell Provider](./creating-a-basic-windows-powershell-provider.md).</span></span> <span data-ttu-id="9565c-104">Ez a megvalósítás indítása és leállítása a szolgáltató módszert biztosít, és bár nem biztosít egy azt jelenti, hogy egy adattár eléréséhez, vagy a, vagy állítsa be az adatokat az adattárban, azt adja meg az összes szükséges alapvető funkciókkal.</span><span class="sxs-lookup"><span data-stu-id="9565c-104">This implementation provides methods for starting and stopping the provider, and although it does not provide a means to access a data store or to get or set the data in the data store, it does provide the basic functionality that is required by all providers.</span></span>

> [!NOTE]
> <span data-ttu-id="9565c-105">Letöltheti a C# forrásfájl (AccessDBSampleProvider01.cs) a szolgáltató Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="9565c-105">You can download the C# source file (AccessDBSampleProvider01.cs) for this provider by using the Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="9565c-106">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="9565c-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="9565c-107">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="9565c-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>
>
> <span data-ttu-id="9565c-108">Más Windows PowerShell-szolgáltató esetében kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).</span><span class="sxs-lookup"><span data-stu-id="9565c-108">For more information about other Windows PowerShell provider implementations, see [Designing Your Windows PowerShell Provider](./designing-your-windows-powershell-provider.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="9565c-109">Kódminta</span><span class="sxs-lookup"><span data-stu-id="9565c-109">Code Sample</span></span>

[!code-csharp[AccessDBProviderSample01.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample01/AccessDBProviderSample01.cs#L11-L30 "AccessDBProviderSample01.cs")]

## <a name="see-also"></a><span data-ttu-id="9565c-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9565c-110">See Also</span></span>

[<span data-ttu-id="9565c-111">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="9565c-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="9565c-112">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="9565c-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)