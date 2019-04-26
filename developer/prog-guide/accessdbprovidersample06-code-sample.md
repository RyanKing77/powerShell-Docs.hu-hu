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
ms.openlocfilehash: 6e86318573df92b9ec84056631843e0efa096a3b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081937"
---
# <a name="accessdbprovidersample06-code-sample"></a><span data-ttu-id="13363-102">AccessDbProviderSample06 – kódminta</span><span class="sxs-lookup"><span data-stu-id="13363-102">AccessDbProviderSample06 Code Sample</span></span>

<span data-ttu-id="13363-103">A következő kód bemutatja a tartalomszolgáltató ismertetett Windows PowerShell végrehajtásának [létrehozása a Windows PowerShell tartalomszolgáltató](./creating-a-windows-powershell-content-provider.md).</span><span class="sxs-lookup"><span data-stu-id="13363-103">The following code shows the implementation of the Windows PowerShell content provider described in [Creating a Windows PowerShell Content Provider](./creating-a-windows-powershell-content-provider.md).</span></span> <span data-ttu-id="13363-104">Ez a szolgáltató lehetővé teszi, hogy a felhasználó a adattárban lévő elemek tartalmának módosítására.</span><span class="sxs-lookup"><span data-stu-id="13363-104">This provider enables the user to manipulate the contents of the items in a data store.</span></span>

> [!NOTE]
> <span data-ttu-id="13363-105">Letöltheti a C# forrásfájl (AccessDBSampleProvider06.cs) a szolgáltató a Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a Microsoft .NET Framework 3.0 futtatási összetevői.</span><span class="sxs-lookup"><span data-stu-id="13363-105">You can download the C# source file (AccessDBSampleProvider06.cs) for this provider by using the Microsoft Windows Software Development Kit for Windows Vista and Microsoft .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="13363-106">Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).</span><span class="sxs-lookup"><span data-stu-id="13363-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="13363-107">A letöltött forrásfájlok érhetők el a  **\<PowerShell-minták >** könyvtár.</span><span class="sxs-lookup"><span data-stu-id="13363-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>
>
> <span data-ttu-id="13363-108">Más Windows PowerShell-szolgáltató esetében kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).</span><span class="sxs-lookup"><span data-stu-id="13363-108">For more information about other Windows PowerShell provider implementations, see [Designing Your Windows PowerShell Provider](./designing-your-windows-powershell-provider.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="13363-109">Kódminta</span><span class="sxs-lookup"><span data-stu-id="13363-109">Code Sample</span></span>

[!code-csharp[AccessDBProviderSample06.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample06/AccessDBProviderSample06.cs#L11-L2399 "AccessDBProviderSample06.cs")]

## <a name="see-also"></a><span data-ttu-id="13363-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="13363-110">See Also</span></span>

[<span data-ttu-id="13363-111">Windows PowerShell programozói útmutató</span><span class="sxs-lookup"><span data-stu-id="13363-111">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="13363-112">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="13363-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)