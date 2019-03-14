---
title: Hogyan lehet egy frissíthető súgó CAB-fájl neve |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: de302da0-c17a-4d31-a8ef-14a626738993
caps.latest.revision: 7
ms.openlocfilehash: 0b58d5ee19a85bed26bc6549ced48b890cd62f64
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794757"
---
# <a name="how-to-name-an-updatable-help-cab-file"></a><span data-ttu-id="071af-102">Frissíthető CAB-súgófájlok elnevezése</span><span class="sxs-lookup"><span data-stu-id="071af-102">How to Name an Updatable Help CAB File</span></span>

<span data-ttu-id="071af-103">Ez a témakör ismerteti a frissíthető súgó kabinet szükséges név formátuma (. CAB-fájl) fájlok.</span><span class="sxs-lookup"><span data-stu-id="071af-103">This topic explains the required name format for the Updatable Help cabinet (.CAB) files.</span></span>

## <a name="how-to-name-an-updatable-help-cab-file"></a><span data-ttu-id="071af-104">Frissíthető CAB-súgófájlok elnevezése</span><span class="sxs-lookup"><span data-stu-id="071af-104">How to Name an Updatable Help CAB File</span></span>

<span data-ttu-id="071af-105">Frissíthető kabinet (. CAB-fájl) fájlt a következő formátumú névvel kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="071af-105">A Updatable cabinet (.CAB) file must have a name with the following format.</span></span>

`<ModuleName>_<ModuleGUID>_<UICulture>_HelpContent.cab`

<span data-ttu-id="071af-106">A név az elemek a következők.</span><span class="sxs-lookup"><span data-stu-id="071af-106">The elements of the name are as follows.</span></span>

<span data-ttu-id="071af-107">Modulnév értéke az a **neve** tulajdonságát a **ModuleInfo** objektum, amely a [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) parancsmag adja vissza.</span><span class="sxs-lookup"><span data-stu-id="071af-107">ModuleName The value of the **Name** property of the **ModuleInfo** object that the [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) cmdlet returns.</span></span>

<span data-ttu-id="071af-108">ModuleGUID az értéket, a **GUID** kulcsfontosságú a moduljegyzékben.</span><span class="sxs-lookup"><span data-stu-id="071af-108">ModuleGUID The value of the **GUID** key in the module manifest.</span></span>

<span data-ttu-id="071af-109">A CAB-fájl a súgófájlt UICulture a felhasználói felület kulturális környezet.</span><span class="sxs-lookup"><span data-stu-id="071af-109">UICulture The UI culture of the help files in the CAB file.</span></span> <span data-ttu-id="071af-110">Ezt az értéket meg kell egyeznie az egyik értékét a **UICulture** elemek modul HelpInfo XML-fájlban.</span><span class="sxs-lookup"><span data-stu-id="071af-110">This value must match the value of one of the **UICulture** elements in the HelpInfo XML file for the module.</span></span>

<span data-ttu-id="071af-111">Például ha a modul neve "TestModule", a modul GUID 9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9 és a felhasználói felület kultúrafüggő részletei az "en-US", a CAB-fájl neve:</span><span class="sxs-lookup"><span data-stu-id="071af-111">For example, if the module name is "TestModule," the module GUID is 9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9, and the UI culture is "en-US", the name of the CAB file would be:</span></span>

`TestModule_9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9_en-US_HelpContent.cab`