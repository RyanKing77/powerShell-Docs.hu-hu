---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: db4543b788ad0a5c7aa32706246446533b901d09
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684506"
---
# <a name="deliver-a-configuration-document-without-applying"></a><span data-ttu-id="be6e9-102">Biztosít a konfigurációs dokumentum leadása alkalmazás nélkül</span><span class="sxs-lookup"><span data-stu-id="be6e9-102">Deliver a configuration document without applying</span></span>

<span data-ttu-id="be6e9-103">A [Publish-DscConfiguration](https://technet.microsoft.com/library/mt517875.aspx) parancsmag másolja át a konfigurációs MOF-fájlt, amely a cél-csomópontra, de nem vonatkozik a konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="be6e9-103">The [Publish-DscConfiguration](https://technet.microsoft.com/library/mt517875.aspx) cmdlet copies a configuration MOF file to a target node, but does not apply the configuration.</span></span>
<span data-ttu-id="be6e9-104">A konfiguráció alkalmazása a következő konzisztencia fázis során, vagy ha futtatja a [Update-DscConfiguration](https://technet.microsoft.com/library/mt143541.aspx) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="be6e9-104">This configuration is applied during the next consistency pass, or when you run the [Update-DscConfiguration](https://technet.microsoft.com/library/mt143541.aspx) cmdlet.</span></span>
