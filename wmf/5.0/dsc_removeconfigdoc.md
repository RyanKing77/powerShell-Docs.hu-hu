---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: af16ce7c5d97731581aa3393a70aba672244c9d8
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187085"
---
# <a name="remove-dsc-documents"></a><span data-ttu-id="934de-102">A DSC-dokumentumok törlése</span><span class="sxs-lookup"><span data-stu-id="934de-102">Remove DSC documents</span></span>

<span data-ttu-id="934de-103">Amikor egy konfigurációs dokumentum DSC érkeznek, a dokumentum végighalad különböző szakaszaiban (függőben lévő, aktuális, előző).</span><span class="sxs-lookup"><span data-stu-id="934de-103">When a configuration document is delivered to DSC, the document goes through various stages (pending, current, previous).</span></span> <span data-ttu-id="934de-104">A DSC-ből a Windows PowerShell 4.0, azt hozzá egy új parancsmagot `Remove-DscConfigurationDocument`, részeként [2014. novemberben kiadott kumulatív frissítés a Windows RT 8.1, Windows 8.1 és Windows Server 2012 R2](https://support.microsoft.com/kb/3000850).</span><span class="sxs-lookup"><span data-stu-id="934de-104">We added a new cmdlet to DSC in Windows PowerShell 4.0, `Remove-DscConfigurationDocument`, as part of [November 2014 update rollup for Windows RT 8.1, Windows 8.1, and Windows Server 2012 R2](https://support.microsoft.com/kb/3000850).</span></span>
