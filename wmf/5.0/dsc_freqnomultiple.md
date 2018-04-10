---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: e1faf71436c8ba0ae02a166ce06d03de9f66f094
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a><span data-ttu-id="c136f-102">RefreshMode és ConfigurationMode gyakoriságot nem kell lenniük minden más Többszörösök</span><span class="sxs-lookup"><span data-stu-id="c136f-102">Frequencies for RefreshMode and ConfigurationMode don't need to be multiples of each other</span></span>

<span data-ttu-id="c136f-103">A korábbi verziójában DSC, a LCM kezelni kellene `RefreshFrequencyMins` és `ConfigurationModeFrequencyMins` többszöröseként egymással.</span><span class="sxs-lookup"><span data-stu-id="c136f-103">In the previous version of DSC, the LCM would treat `RefreshFrequencyMins` and `ConfigurationModeFrequencyMins` as multiples of each other.</span></span> <span data-ttu-id="c136f-104">A WMF 5.0 RTM-re egymástól független dolgoznak fel ezeket a tulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="c136f-104">In WMF 5.0 RTM, these properties are processed independent of each other.</span></span>

<span data-ttu-id="c136f-105">További információkért lásd: [konfigurálása a helyi Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span><span class="sxs-lookup"><span data-stu-id="c136f-105">For more information, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span></span>