---
ms.date: 06/09/2017
schema: 2.0.0
keywords: PowerShell
title: Licenc elfogadása igénylő parancsfájlok
ms.openlocfilehash: 6374c8c8536dd0c8f27580a5b8895b8db18424f9
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
ms.locfileid: "34048884"
---
# <a name="requiring-license-acceptance-for-scripts"></a><span data-ttu-id="c2eb1-103">Licenc elfogadása igénylő parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="c2eb1-103">Requiring license acceptance for scripts</span></span>

<span data-ttu-id="c2eb1-104">Licenc elfogadása parancsfájlok nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="c2eb1-104">License Acceptance is not supported for scripts.</span></span> <span data-ttu-id="c2eb1-105">Azonban a forgatókönyvet, ahol egy parancsfájl attól függ, a modul, amely licencszerződés elfogadását igényli támogatott.</span><span class="sxs-lookup"><span data-stu-id="c2eb1-105">However, the scenario where a script depends on a module that requires license acceptance is supported.</span></span>

<span data-ttu-id="c2eb1-106">Parancsfájl commands(Install-Script/Save-Script/Update-Script) támogatja az új paramétert, amely úgy viselkedik, mintha a felhasználói látta a licenc - AcceptLicense.</span><span class="sxs-lookup"><span data-stu-id="c2eb1-106">Script commands(Install-Script/Save-Script/Update-Script) support a new parameter -AcceptLicense that behaves as though user saw the license.</span></span> <span data-ttu-id="c2eb1-107">Ha nincs megadva a - AcceptLicense; a felhasználó kéri, hogy elfogadja a licencfeltételeket és a függő modul license.txt megjelenítendő.</span><span class="sxs-lookup"><span data-stu-id="c2eb1-107">If -AcceptLicense is not specified; the user will be shown license.txt for dependent module and prompted to accept the license.</span></span>

## <a name="examples"></a><span data-ttu-id="c2eb1-108">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="c2eb1-108">EXAMPLES</span></span>

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="c2eb1-109">1. példa: Telepítési parancsfájl licenc elfogadása igénylő függőségekkel rendelkező</span><span class="sxs-lookup"><span data-stu-id="c2eb1-109">Example 1: Install Script with dependencies requiring license acceptance</span></span>

<span data-ttu-id="c2eb1-110">Parancsfájl "ScriptRequireLicenseAcceptance" modul "ModuleRequireLicenseAcceptance" függ.</span><span class="sxs-lookup"><span data-stu-id="c2eb1-110">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="c2eb1-111">Licenc elfogadása felhasználótól.</span><span class="sxs-lookup"><span data-stu-id="c2eb1-111">User is prompted to Accept License.</span></span>

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

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="c2eb1-112">2. példa: Telepítési parancsfájl licenc elfogadása és - AcceptLicense függőségekkel rendelkező</span><span class="sxs-lookup"><span data-stu-id="c2eb1-112">Example 2: Install Script with dependencies requiring license acceptance and -AcceptLicense</span></span>

<span data-ttu-id="c2eb1-113">Parancsfájl "ScriptRequireLicenseAcceptance" modul "ModuleRequireLicenseAcceptance" függ.</span><span class="sxs-lookup"><span data-stu-id="c2eb1-113">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="c2eb1-114">Nem felhasználótól fogadnia a licencfeltételeket, mert - AcceptLicense sincs megadva.</span><span class="sxs-lookup"><span data-stu-id="c2eb1-114">User is not prompted to accept license as -AcceptLicense is specified.</span></span>

```PowerShell
PS> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a><span data-ttu-id="c2eb1-115">További részletekért</span><span class="sxs-lookup"><span data-stu-id="c2eb1-115">More details</span></span>

- [<span data-ttu-id="c2eb1-116">Licenc elfogadása támogatásra van szüksége a modulok</span><span class="sxs-lookup"><span data-stu-id="c2eb1-116">Require License Acceptance support for Modules</span></span>](module-license-acceptance.md)
- [<span data-ttu-id="c2eb1-117">A PowerShellGallery licenc elfogadása támogatásra van szüksége</span><span class="sxs-lookup"><span data-stu-id="c2eb1-117">Require License Acceptance support on PowerShellGallery</span></span>](../how-to/working-with-items/items-that-require-license-acceptance.md)
- [<span data-ttu-id="c2eb1-118">Licencfeltételek elfogadásának kérése az Azure Automation szolgáltatásban való üzembe helyezéshez</span><span class="sxs-lookup"><span data-stu-id="c2eb1-118">Require License Acceptance on Deploy to Azure Automation</span></span>](../how-to/working-with-items/deploy-to-azure-automation.md)