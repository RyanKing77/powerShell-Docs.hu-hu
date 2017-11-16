---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: psget_moduledependencypopulation
ms.openlocfilehash: 126cd65ac35a31f4118474bc36dac1836ec0f22e
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="logic-for-preparing-the-module-dependencies-during-publish-operation"></a>Logikát a közzététel művelet során a modul függőségek előkészítése
1.  RequiredModules részeként felsorolt függőségei számít.
2.  NestedModules, amelynek modul alapja nem a megadott modul alábbi alatt áll, részeként felsorolt függőségei számít.

3.  Függőségek fent kell érhető el a azonos cél-tárházban, ellenkező esetben közzététele művelet hibát eredményez.
    Például: "SnippetPx" nem érhető el a tárházban, ha alább hibát fog jelezni.
    ```powershell
    Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent
    'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```
4.  Néhány modul függőségek külsőleg kezelheti, ebben az esetben kell adni őket a moduljegyzékben PSData szakaszában ExternalModuleDependencies-bejegyzést.
    A fenti hibaüzenet rész alatt
    ```powershell
    If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```

*A modul telepítése során fent előkészített függőségek lista szolgál a függőségek telepítése.*

*Győződjön meg arról, hogy a modul függőségek alatt érhetők el $env: PSModulePath során a rendszer közzéteszi a műveletet.*

