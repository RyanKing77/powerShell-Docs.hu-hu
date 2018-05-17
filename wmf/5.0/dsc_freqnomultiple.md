---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: a3ac215396206fba62bce303733429d60722ee6b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a>RefreshMode és ConfigurationMode gyakoriságot nem kell lenniük minden más Többszörösök

A korábbi verziójában DSC, a LCM kezelni kellene `RefreshFrequencyMins` és `ConfigurationModeFrequencyMins` többszöröseként egymással. A WMF 5.0 RTM-re egymástól független dolgoznak fel ezeket a tulajdonságokat.

További információkért lásd: [konfigurálása a helyi Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).
