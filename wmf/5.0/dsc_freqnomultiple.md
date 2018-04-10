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
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a>RefreshMode és ConfigurationMode gyakoriságot nem kell lenniük minden más Többszörösök

A korábbi verziójában DSC, a LCM kezelni kellene `RefreshFrequencyMins` és `ConfigurationModeFrequencyMins` többszöröseként egymással. A WMF 5.0 RTM-re egymástól független dolgoznak fel ezeket a tulajdonságokat.

További információkért lásd: [konfigurálása a helyi Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).