---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-erőforrások"
ms.openlocfilehash: 0994616673b5e447c69c09154bfdb9b9126a88c8
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-resources"></a><span data-ttu-id="4ebda-103">A DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="4ebda-103">DSC Resources</span></span>

><span data-ttu-id="4ebda-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="4ebda-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="4ebda-105">A kívánt állapot konfigurációs szolgáltatása (DSC) forrásokban a építőelemeket DSC-konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="4ebda-105">Desired State Configuration (DSC) Resources provide the building blocks for a DSC configuration.</span></span> <span data-ttu-id="4ebda-106">Egy erőforrás konfigurált (séma), valamint a PowerShell parancsfájl olyan függvényeket tartalmaz, hogy "," meghívja a helyi Configuration Manager (LCM) tulajdonságok közzététele.</span><span class="sxs-lookup"><span data-stu-id="4ebda-106">A resource exposes properties that can be configured (schema) and contains the PowerShell script functions that the Local Configuration Manager (LCM) calls to "make it so".</span></span>

<span data-ttu-id="4ebda-107">Egy erőforrás modellezhető valamilyen általános fájlként, vagy egy olyan IIS-kiszolgálói beállítást legpontosabb.</span><span class="sxs-lookup"><span data-stu-id="4ebda-107">A resource can model something as generic as a file or as specific as an IIS server setting.</span></span>  <span data-ttu-id="4ebda-108">Például erőforrások csoportja, amelyek rendszerezi az összes szükséges fájlt a hordozható, és a metaadatok azonosítására, hogyan a az erőforrásokhoz való használatra készült tartalmazó struktúrára DSC modulra van összevonva.</span><span class="sxs-lookup"><span data-stu-id="4ebda-108">Groups of like resources are combined in to a DSC Module, which organizes all the required files in to a structure that is portable and includes metadata to identify how the resources are intended to be used.</span></span>  

<span data-ttu-id="4ebda-109">A következő témakörök ismertetik a DSC-erőforrások:</span><span class="sxs-lookup"><span data-stu-id="4ebda-109">The following topics describe DSC resources:</span></span>

- [<span data-ttu-id="4ebda-110">Beépített DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="4ebda-110">Built-In DSC resources</span></span>](builtInResource.md)
- [<span data-ttu-id="4ebda-111">Egyéni DSC-erőforrások létrehozása</span><span class="sxs-lookup"><span data-stu-id="4ebda-111">Build custom DSC resources</span></span>](authoringResource.md)
- [<span data-ttu-id="4ebda-112">Linux beépített DSC-erőforrások</span><span class="sxs-lookup"><span data-stu-id="4ebda-112">Built-In DSC resources for Linux</span></span>](lnxBuiltInResources.md)

