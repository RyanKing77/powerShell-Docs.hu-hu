---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: a3ac215396206fba62bce303733429d60722ee6b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218382"
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a><span data-ttu-id="10ec0-102">RefreshMode és ConfigurationMode gyakoriságot nem kell lenniük minden más Többszörösök</span><span class="sxs-lookup"><span data-stu-id="10ec0-102">Frequencies for RefreshMode and ConfigurationMode don't need to be multiples of each other</span></span>

<span data-ttu-id="10ec0-103">A korábbi verziójában DSC, a LCM kezelni kellene `RefreshFrequencyMins` és `ConfigurationModeFrequencyMins` többszöröseként egymással.</span><span class="sxs-lookup"><span data-stu-id="10ec0-103">In the previous version of DSC, the LCM would treat `RefreshFrequencyMins` and `ConfigurationModeFrequencyMins` as multiples of each other.</span></span> <span data-ttu-id="10ec0-104">A WMF 5.0 RTM-re egymástól független dolgoznak fel ezeket a tulajdonságokat.</span><span class="sxs-lookup"><span data-stu-id="10ec0-104">In WMF 5.0 RTM, these properties are processed independent of each other.</span></span>

<span data-ttu-id="10ec0-105">További információkért lásd: [konfigurálása a helyi Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span><span class="sxs-lookup"><span data-stu-id="10ec0-105">For more information, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span></span>
