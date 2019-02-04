---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 7a1725e3858c59a6d31699add22b042359c48463
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685759"
---
# <a name="separation-of-node-and-configuration-ids"></a><span data-ttu-id="1698e-102">Csomópont- és konfigurációazonosítók szétválasztása</span><span class="sxs-lookup"><span data-stu-id="1698e-102">Separation of Node and Configuration IDs</span></span>

## <a name="overview"></a><span data-ttu-id="1698e-103">Áttekintés</span><span class="sxs-lookup"><span data-stu-id="1698e-103">Overview</span></span>

<span data-ttu-id="1698e-104">Annak érdekében, hogy egy rugalmasabb és zökkenőmentes élményt DSC lekéréses módban használatakor, ebben a kiadásban számos szolgáltatást hozzáadtuk.</span><span class="sxs-lookup"><span data-stu-id="1698e-104">In order to provide a more flexible and streamlined experience when using DSC in Pull mode, we have added a number of features in this release.</span></span> <span data-ttu-id="1698e-105">Ezeket a funkciókat, hogy könnyen beállítása és konfigurációk üzembe helyezése több csomóponton, miközben továbbra is állapotának nyomon követése az egyes csomópontok állapotinformációit reporting külön-külön is szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="1698e-105">These features are intended to allow you to have the flexibility to easily setup and deploy configurations across multiple nodes, while still tracking status and reporting information for each node individually.</span></span>
<span data-ttu-id="1698e-106">Ezek a funkciók a következők:</span><span class="sxs-lookup"><span data-stu-id="1698e-106">These features are as follows:</span></span>

* <span data-ttu-id="1698e-107">A konfiguráció nevét, amely azonosítja a számítógép konfigurációja.</span><span class="sxs-lookup"><span data-stu-id="1698e-107">A configuration name which identifies the configuration for a computer.</span></span> <span data-ttu-id="1698e-108">Ez a név megosztható több cél csomópont</span><span class="sxs-lookup"><span data-stu-id="1698e-108">This name can be shared by multiple target nodes</span></span>
* <span data-ttu-id="1698e-109">Egy ügynök azonosítója, amely egyértelműen azonosít egy egycsomópontos</span><span class="sxs-lookup"><span data-stu-id="1698e-109">An agent ID which uniquely identifies a single node</span></span>
* <span data-ttu-id="1698e-110">Egy regisztrációs lépésre, amely csak akkor történik meg az első alkalommal egy célcsomóponttal csatlakozik egy lekéréses kiszolgálót</span><span class="sxs-lookup"><span data-stu-id="1698e-110">A registration step which only occurs the first time a target node connects to a pull server</span></span>

<span data-ttu-id="1698e-111">**Megjegyzés:** Ezek a szolgáltatások és funkciók lettek hozzáadva, és cserélje le a meglévő pull-szolgáltatások és fogalmak.</span><span class="sxs-lookup"><span data-stu-id="1698e-111">**Note:** These features and functionality have been added and do not replace the existing pull features and concepts.</span></span> <span data-ttu-id="1698e-112">Használhatja az új funkciók vagy az új lekéréses kiszolgálóval szállítási ebben a kiadásban a régieket.</span><span class="sxs-lookup"><span data-stu-id="1698e-112">You can use these new features or the older ones with the new pull server shipping in this release.</span></span>

<span data-ttu-id="1698e-113">További információkért lásd: [konfigurációs nevek lekérési ügyfél beállítása](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)</span><span class="sxs-lookup"><span data-stu-id="1698e-113">For more information, see [Setting up a pull client using configuration names](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)</span></span>
