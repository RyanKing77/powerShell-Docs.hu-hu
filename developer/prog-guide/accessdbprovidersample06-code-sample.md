---
title: Kódminta AccessDbProviderSample06 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: baab6a56-c199-48d7-a03e-a904b1bb1baa
caps.latest.revision: 7
ms.openlocfilehash: 2798e8b542b2f06247955409118e75c5652b644c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850161"
---
# <a name="accessdbprovidersample06-code-sample"></a><span data-ttu-id="cebf0-102">AccessDbProviderSample06 – kódminta</span><span class="sxs-lookup"><span data-stu-id="cebf0-102">AccessDbProviderSample06 Code Sample</span></span>

<span data-ttu-id="cebf0-103">A következő kód bemutatja a tartalomszolgáltató ismertetett Windows PowerShell végrehajtásának [létrehozása a Windows PowerShell tartalomszolgáltató](./creating-a-windows-powershell-content-provider.md).</span><span class="sxs-lookup"><span data-stu-id="cebf0-103">The following code shows the implementation of the Windows PowerShell content provider described in [Creating a Windows PowerShell Content Provider](./creating-a-windows-powershell-content-provider.md).</span></span> <span data-ttu-id="cebf0-104">Ez a szolgáltató lehetővé teszi, hogy a felhasználó a adattárban lévő elemek tartalmának módosítására.</span><span class="sxs-lookup"><span data-stu-id="cebf0-104">This provider enables the user to manipulate the contents of the items in a data store.</span></span>

> [!NOTE]
> <span data-ttu-id="cebf0-105">Letöltheti a C# forrásfájl (AccessDBSampleProvider06.cs) a szolgáltató a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="cebf0-105">You can download the C# source file (AccessDBSampleProvider06.cs) for this provider by using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="cebf0-106">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="cebf0-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="cebf0-107">Letöltheti a C# forrásfájl (AccessDBSampleProvider06.cs) a szolgáltató a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="cebf0-107">You can download the C# source file (AccessDBSampleProvider06.cs) for this provider by using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="cebf0-108">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="cebf0-108">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="cebf0-109">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="cebf0-109">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>
>
> <span data-ttu-id="cebf0-110">Más Windows PowerShell-szolgáltató esetében kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).</span><span class="sxs-lookup"><span data-stu-id="cebf0-110">For more information about other Windows PowerShell provider implementations, see [Designing Your Windows PowerShell Provider](./designing-your-windows-powershell-provider.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="cebf0-111">Kódminta</span><span class="sxs-lookup"><span data-stu-id="cebf0-111">Code Sample</span></span>

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L11-L2399 "AccessDBProviderSample06.cs")]

## <a name="see-also"></a><span data-ttu-id="cebf0-112">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cebf0-112">See Also</span></span>

[<span data-ttu-id="cebf0-113">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="cebf0-113">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="cebf0-114">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="cebf0-114">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)