---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: psget_moduledependencypopulation
ms.openlocfilehash: c4c9f203e9c526ff532c2388acb6334515d66934
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="logic-for-preparing-the-module-dependencies-during-publish-operation"></a><span data-ttu-id="d61c8-103">Logikát a közzététel művelet során a modul függőségek előkészítése</span><span class="sxs-lookup"><span data-stu-id="d61c8-103">Logic for preparing the module dependencies during Publish operation</span></span>
1.  <span data-ttu-id="d61c8-104">RequiredModules részeként felsorolt függőségei számít.</span><span class="sxs-lookup"><span data-stu-id="d61c8-104">Modules listed as part of RequiredModules are considered as dependencies.</span></span>
2.  <span data-ttu-id="d61c8-105">NestedModules, amelynek modul alapja nem a megadott modul alábbi alatt áll, részeként felsorolt függőségei számít.</span><span class="sxs-lookup"><span data-stu-id="d61c8-105">Modules listed as part of NestedModules, whose module base is not under the specified module base, are considered as dependencies.</span></span>

3.  <span data-ttu-id="d61c8-106">Függőségek fent kell érhető el a azonos cél-tárházban, ellenkező esetben közzététele művelet hibát eredményez.</span><span class="sxs-lookup"><span data-stu-id="d61c8-106">Above dependencies should be available on the same target repository, otherwise publish operation will result in an error.</span></span>
    <span data-ttu-id="d61c8-107">Például: "SnippetPx" nem érhető el a tárházban, ha alább hibát fog jelezni.</span><span class="sxs-lookup"><span data-stu-id="d61c8-107">For example: If 'SnippetPx' is not available on the repository, below error will be thrown.</span></span>
    ```powershell
    Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent
    'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```
4.  <span data-ttu-id="d61c8-108">Néhány modul függőségek külsőleg kezelheti, ebben az esetben kell adni őket a moduljegyzékben PSData szakaszában ExternalModuleDependencies-bejegyzést.</span><span class="sxs-lookup"><span data-stu-id="d61c8-108">Some module dependencies can be managed externally, in that case they should be added to the ExternalModuleDependencies entry in the PSData section of the module manifest.</span></span>
    <span data-ttu-id="d61c8-109">A fenti hibaüzenet rész alatt</span><span class="sxs-lookup"><span data-stu-id="d61c8-109">Below part in the above error message</span></span>
    ```powershell
    If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```

<span data-ttu-id="d61c8-110">*A modul telepítése során fent előkészített függőségek lista szolgál a függőségek telepítése.*</span><span class="sxs-lookup"><span data-stu-id="d61c8-110">*During the module installation, above prepared dependencies list is used for installing the dependencies.*</span></span>

<span data-ttu-id="d61c8-111">*Győződjön meg arról, hogy a modul függőségek alatt érhetők el $env: PSModulePath során a rendszer közzéteszi a műveletet.*</span><span class="sxs-lookup"><span data-stu-id="d61c8-111">*Please ensure that your module’s dependencies are available under $env:PSModulePath on your system during publish operation.*</span></span>