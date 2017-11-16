---
ms.date: 2017-06-09
schema: 2.0.0
keywords: PowerShell
title: RequireLicenseAcceptanceScript
ms.openlocfilehash: 7092fb2e63b9e2b1eca59cd418317631bff8b172
ms.sourcegitcommit: cd66d4f49ea762a31887af2c72d087b219ddbe10
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/11/2017
---
# <a name="requiring-license-acceptance-for-scripts"></a><span data-ttu-id="340b6-103">Licenc elfogadása igénylő parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="340b6-103">Requiring License Acceptance for Scripts</span></span>

<span data-ttu-id="340b6-104">Licenc elfogadása parancsfájlok nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="340b6-104">License Acceptance is not supported for scripts.</span></span> <span data-ttu-id="340b6-105">Azonban a forgatókönyvet, ahol egy parancsfájl attól függ, a modul, amely licencszerződés elfogadását igényli támogatott.</span><span class="sxs-lookup"><span data-stu-id="340b6-105">However, the scenario where a script depends on a module that requires license acceptance is supported.</span></span>

<span data-ttu-id="340b6-106">Parancsfájl commands(Install-Script/Save-Script/Update-Script) támogatja az új paramétert, amely úgy viselkedik, mintha a felhasználói látta a licenc - AcceptLicense.</span><span class="sxs-lookup"><span data-stu-id="340b6-106">Script commands(Install-Script/Save-Script/Update-Script) support a new parameter -AcceptLicense that behaves as though user saw the license.</span></span> <span data-ttu-id="340b6-107">Ha nincs megadva a - AcceptLicense; a felhasználó kéri, hogy elfogadja a licencfeltételeket és a függő modul license.txt megjelenítendő.</span><span class="sxs-lookup"><span data-stu-id="340b6-107">If -AcceptLicense is not specified; the user will be shown license.txt for dependent module and prompted to accept the license.</span></span>

## <a name="examples"></a><span data-ttu-id="340b6-108">PÉLDÁK</span><span class="sxs-lookup"><span data-stu-id="340b6-108">EXAMPLES</span></span>

### <a name="example-1-install-script-with-dependencies-requiring-license-acceptance"></a><span data-ttu-id="340b6-109">1. példa: Telepítési parancsfájl licenc elfogadása igénylő függőségekkel rendelkező</span><span class="sxs-lookup"><span data-stu-id="340b6-109">Example 1: Install Script with dependencies requiring license acceptance</span></span>
<span data-ttu-id="340b6-110">Parancsfájl "ScriptRequireLicenseAcceptance" modul "ModuleRequireLicenseAcceptance" függ.</span><span class="sxs-lookup"><span data-stu-id="340b6-110">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="340b6-111">Licenc elfogadása felhasználótól.</span><span class="sxs-lookup"><span data-stu-id="340b6-111">User is prompted to Accept License.</span></span>
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance

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

### <a name="example-2-install-script-with-dependencies-requiring-license-acceptance-and--acceptlicense"></a><span data-ttu-id="340b6-112">2. példa: Telepítési parancsfájl licenc elfogadása és - AcceptLicense függőségekkel rendelkező</span><span class="sxs-lookup"><span data-stu-id="340b6-112">Example 2: Install Script with dependencies requiring license acceptance and -AcceptLicense</span></span>
<span data-ttu-id="340b6-113">Parancsfájl "ScriptRequireLicenseAcceptance" modul "ModuleRequireLicenseAcceptance" függ.</span><span class="sxs-lookup"><span data-stu-id="340b6-113">Script 'ScriptRequireLicenseAcceptance' depends on module 'ModuleRequireLicenseAcceptance'.</span></span> <span data-ttu-id="340b6-114">Nem felhasználótól fogadnia a licencfeltételeket, mert - AcceptLicense sincs megadva.</span><span class="sxs-lookup"><span data-stu-id="340b6-114">User is not prompted to accept license as -AcceptLicense is specified.</span></span>
```PowerShell
PS C:\> Install-Script -Name ScriptRequireLicenseAcceptance -AcceptLicense
```

## <a name="more-details"></a><span data-ttu-id="340b6-115">További részletekért</span><span class="sxs-lookup"><span data-stu-id="340b6-115">More details</span></span>
### <a name="require-license-acceptance-support-for-modulesmodulerequirelicenseacceptancemd"></a>[<span data-ttu-id="340b6-116">Licenc elfogadása támogatásra van szüksége a modulok</span><span class="sxs-lookup"><span data-stu-id="340b6-116">Require License Acceptance support for Modules</span></span>](../module/RequireLicenseAcceptance.md)

### <a name="require-license-acceptance-support-on-powershellgallerypsgallerypsgalleryrequireslicenseacceptancemd"></a>[<span data-ttu-id="340b6-117">A PowerShellGallery licenc elfogadása támogatásra van szüksége</span><span class="sxs-lookup"><span data-stu-id="340b6-117">Require License Acceptance support on PowerShellGallery</span></span>](../../psgallery/psgallery_requires_license_acceptance.md)

### <a name="require-license-acceptance-on-deploy-to-azure-automationpsgallerypsgallerydeploytoazureautomationrequirelicenseacceptancemd"></a>[<span data-ttu-id="340b6-118">Licenc elfogadására van szükség az Azure Automation szolgáltatásbeli központi telepítése</span><span class="sxs-lookup"><span data-stu-id="340b6-118">Require License Acceptance on Deploy to Azure Automation</span></span>](../../psgallery/psgallery_deploy_to_azure_automation_requireLicenseAcceptance.md)
