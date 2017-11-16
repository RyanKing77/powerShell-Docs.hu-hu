---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 30055cff87159df98029e25409782e0fe2f0bae4
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a>RefreshMode és ConfigurationMode gyakoriságot nem kell lenniük minden más Többszörösök

A korábbi verziójában DSC, a LCM kezelni kellene `RefreshFrequencyMins` és `ConfigurationModeFrequencyMins` többszöröseként egymással. A WMF 5.0 RTM-re egymástól független dolgoznak fel ezeket a tulajdonságokat. 

További információkért lásd: [konfigurálása a helyi Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).

