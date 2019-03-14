---
title: Hogyan lehet egy HelpInfo XML-fájl neve |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 64e85b53-5aeb-4d6c-903c-af4ab62f11c1
caps.latest.revision: 7
ms.openlocfilehash: 462cd7bd486a5924bb2bc43e0ac8d1558e30e657
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794807"
---
# <a name="how-to-name-a-helpinfo-xml-file"></a><span data-ttu-id="886e0-102">HelpInfo XML-fájl elnevezése</span><span class="sxs-lookup"><span data-stu-id="886e0-102">How to Name a HelpInfo XML File</span></span>

<span data-ttu-id="886e0-103">Ez a témakör ismerteti a szükséges nevének formátuma a frissíthető súgó információkat fájlok, gyakran nevezik HelpInfo XML-fájlok számára.</span><span class="sxs-lookup"><span data-stu-id="886e0-103">This topic explains the required name format for the Updatable Help Information files, commonly known as HelpInfo XML files.</span></span>

## <a name="how-to-name-a-helpinfo-xml-file"></a><span data-ttu-id="886e0-104">HelpInfo XML-fájl elnevezése</span><span class="sxs-lookup"><span data-stu-id="886e0-104">How to Name a HelpInfo XML File</span></span>

<span data-ttu-id="886e0-105">Egy HelpInfo XML-fájl nevét a következő formátummal kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="886e0-105">A HelpInfo XML file must have a name with the following format.</span></span>

`<ModuleName>_<ModuleGUID>_HelpInfo.xml`

<span data-ttu-id="886e0-106">A név az elemek a következők.</span><span class="sxs-lookup"><span data-stu-id="886e0-106">The elements of the name are as follows.</span></span>

<span data-ttu-id="886e0-107">Modulnév értéke az a **neve** tulajdonságát a **ModuleInfo** objektum, amely a [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) parancsmag adja vissza.</span><span class="sxs-lookup"><span data-stu-id="886e0-107">ModuleName The value of the **Name** property of the **ModuleInfo** object that the [Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) cmdlet returns.</span></span>

<span data-ttu-id="886e0-108">ModuleGUID az értéket, a **GUID** kulcsfontosságú a moduljegyzékben.</span><span class="sxs-lookup"><span data-stu-id="886e0-108">ModuleGUID The value of the **GUID** key in the module manifest.</span></span>

<span data-ttu-id="886e0-109">Például ha a modul neve "TestModule" és a modul GUID 9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9, a modul HelpInfo XML-fájljának nevét a következő lesz:</span><span class="sxs-lookup"><span data-stu-id="886e0-109">For example, if the module name is "TestModule" and the module GUID is 9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9, the name of the HelpInfo XML file for the module would be:</span></span>

`TestModule_9cabb9ad-f2ac-4914-a46b-bfc1bebf07f9_HelpInfo.xml`