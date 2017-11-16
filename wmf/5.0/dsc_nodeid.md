---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 5b9eea1c90bfd5a8cee3897d832bf7775a750308
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="separation-of-node-and-configuration-ids"></a><span data-ttu-id="722eb-102">Csomópont- és konfigurációs azonosítókat elkülönítése</span><span class="sxs-lookup"><span data-stu-id="722eb-102">Separation of Node and Configuration IDs</span></span>

## <a name="overview"></a><span data-ttu-id="722eb-103">Áttekintés</span><span class="sxs-lookup"><span data-stu-id="722eb-103">Overview</span></span>

<span data-ttu-id="722eb-104">Ahhoz, hogy adjon meg egy rugalmas, és zökkenőmentes élményt, lekéréses módban a DSC használata esetén, ebben a kiadásban jelentek meg számos funkciót tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="722eb-104">In order to provide a more flexible and streamlined experience when using DSC in Pull mode, we have added a number of features in this release.</span></span> <span data-ttu-id="722eb-105">Ezek a szolgáltatások célja, hogy engedélyezi, hogy könnyen beállítása beállításokat és telepíthet az csomópontokon, miközben továbbra is nyomon követési állapot külön-külön jelentési adatok az egyes csomópontok rugalmasan.</span><span class="sxs-lookup"><span data-stu-id="722eb-105">These features are intended to allow you to have the flexibility to easily setup and deploy configurations across multiple nodes, while still tracking status and reporting information for each node individually.</span></span> <span data-ttu-id="722eb-106">Ezek a funkciók a következők:</span><span class="sxs-lookup"><span data-stu-id="722eb-106">These features are as follows:</span></span>

* <span data-ttu-id="722eb-107">A konfiguráció nevét, amely azonosítja a számítógép konfigurációja.</span><span class="sxs-lookup"><span data-stu-id="722eb-107">A configuration name which identifies the configuration for a computer.</span></span> <span data-ttu-id="722eb-108">Ez a név több célcsomópontokat megoszthatók</span><span class="sxs-lookup"><span data-stu-id="722eb-108">This name can be shared by multiple target nodes</span></span> 
* <span data-ttu-id="722eb-109">Egy ügynök azonosítója, amely egyedileg azonosítja az egyetlen csomópont</span><span class="sxs-lookup"><span data-stu-id="722eb-109">An agent ID which uniquely identifies a single node</span></span>
* <span data-ttu-id="722eb-110">A lekérési kiszolgálójával csatlakozik egy regisztrációs lépés, amely csak akkor fordul elő, amikor első alkalommal egy célcsomóponttal</span><span class="sxs-lookup"><span data-stu-id="722eb-110">A registration step which only occurs the first time a target node connects to a pull server</span></span>

<span data-ttu-id="722eb-111">**Megjegyzés:** ezeket a szolgáltatásokat és funkciókat hozzá vannak adva, és nem váltják ki a meglévő lekéréses funkciók és fogalmak.</span><span class="sxs-lookup"><span data-stu-id="722eb-111">**Note:** These features and functionality have been added and do not replace the existing pull features and concepts.</span></span> <span data-ttu-id="722eb-112">Használhatja az új szolgáltatásokat vagy az új lekéréses kiszolgálóval szállítási ebben a kiadásban a régieket.</span><span class="sxs-lookup"><span data-stu-id="722eb-112">You can use these new features or the older ones with the new pull server shipping in this release.</span></span>

<span data-ttu-id="722eb-113">További információkért lásd: [konfigurációs nevek használatával lekéréses ügyfél beállítása](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)</span><span class="sxs-lookup"><span data-stu-id="722eb-113">For more information, see [Setting up a pull client using configuration names](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)</span></span>

