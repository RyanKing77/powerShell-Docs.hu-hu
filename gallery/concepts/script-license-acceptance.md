---
ms.date: 06/09/2017
schema: 2.0.0
keywords: PowerShell
title: Licencfeltételek elfogadását igénylő parancsprogramok
ms.openlocfilehash: e7101eb6a480dd87965b7b9be9d49583042b603f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684212"
---
# <a name="requiring-license-acceptance-for-scripts"></a><span data-ttu-id="822d0-103">Licencfeltételek elfogadását igénylő parancsprogramok</span><span class="sxs-lookup"><span data-stu-id="822d0-103">Requiring license acceptance for scripts</span></span>

<span data-ttu-id="822d0-104">Licencfeltételek elfogadásának parancsfájlok nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="822d0-104">License Acceptance is not supported for scripts.</span></span> <span data-ttu-id="822d0-105">Azonban a forgatókönyvet, ahol a parancsfájl attól függ, a licencfeltételek elfogadását igénylő moduljára támogatott.</span><span class="sxs-lookup"><span data-stu-id="822d0-105">However, the scenario where a script depends on a module that requires license acceptance is supported.</span></span>

<span data-ttu-id="822d0-106">Parancsfájl commands(Install-Script/Save-Script/Update-Script) támogatásához új paraméter, amely viselkedik, mintha a felhasználó látott a licenc - AcceptLicense.</span><span class="sxs-lookup"><span data-stu-id="822d0-106">Script commands(Install-Script/Save-Script/Update-Script) support a new parameter -AcceptLicense that behaves as though user saw the license.</span></span> <span data-ttu-id="822d0-107">Ha nincs megadva - AcceptLicense; a felhasználó a licenc elfogadására kéri a rendszer és a függő modul license.txt megjelenítendő.</span><span class="sxs-lookup"><span data-stu-id="822d0-107">If -AcceptLicense is not specified; the user will be shown license.txt for dependent module and prompted to accept the license.</span></span>

## <a name="examples"></a><span data-ttu-id="822d0-108">EXAMPLES</span><span class="sxs-lookup"><span data-stu-id="822d0-108">EXAMPLES</span></span>

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="822d0-109">1. példa: Licencfeltételek elfogadását igénylő függőségekkel parancsfájl telepítése</span><span class="sxs-lookup"><span data-stu-id="822d0-109">Example 1: Install Script with dependencies requiring license acceptance</span></span>

<span data-ttu-id="822d0-110">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span><span class="sxs-lookup"><span data-stu-id="822d0-110">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="822d0-111">Licenc fogadja el a rendszer kéri.</span><span class="sxs-lookup"><span data-stu-id="822d0-111">User is prompted to Accept License.</span></span>

```PowerShell
PS> Install-Script -Name ScriptRequireLicenseAcceptance

License Acceptance
MIT License 2.0
Copyright (c) 2016 PowerShell Team
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software.

Do you accept the license terms for module 'ModuleRequireLicenseAcceptance'.
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="822d0-112">2. példa: Licencfeltételek elfogadásának és - AcceptLicense függőségekkel parancsfájl telepítése</span><span class="sxs-lookup"><span data-stu-id="822d0-112">Example 2: Install Script with dependencies requiring license acceptance and -AcceptLicense</span></span>

<span data-ttu-id="822d0-113">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span><span class="sxs-lookup"><span data-stu-id="822d0-113">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="822d0-114">Fogadja el a licenc - AcceptLicense van megadva, az nem kéri a felhasználótól.</span><span class="sxs-lookup"><span data-stu-id="822d0-114">User is not prompted to accept license as -AcceptLicense is specified.</span></span>

```PowerShell
PS> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a><span data-ttu-id="822d0-115">További részletek</span><span class="sxs-lookup"><span data-stu-id="822d0-115">More details</span></span>

- [<span data-ttu-id="822d0-116">Licencfeltételek elfogadásának támogatást igénylő modulok</span><span class="sxs-lookup"><span data-stu-id="822d0-116">Require License Acceptance support for Modules</span></span>](module-license-acceptance.md)
- [<span data-ttu-id="822d0-117">A PowerShell-Galériabeli licencfeltételek elfogadását támogatásra van szüksége</span><span class="sxs-lookup"><span data-stu-id="822d0-117">Require License Acceptance support on PowerShellGallery</span></span>](../how-to/working-with-packages/packages-that-require-license-acceptance.md)
- [<span data-ttu-id="822d0-118">Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez</span><span class="sxs-lookup"><span data-stu-id="822d0-118">Require License Acceptance on Deploy to Azure Automation</span></span>](../how-to/working-with-packages/deploy-to-azure-automation.md)
