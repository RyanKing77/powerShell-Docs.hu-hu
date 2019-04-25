---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 23a5c8832f7c2888880a1ee846d75feaa95ebe47
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058403"
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a>RefreshMode és a ConfigurationMode nem kell minden más Többszörösök

DSC korábbi verziójában, az LCM kezelni kellene `RefreshFrequencyMins` és `ConfigurationModeFrequencyMins` többszöröseként egymással. A WMF 5.0 RTM-re ezek a Tulajdonságok feldolgozása egymástól független.

További információkért lásd: [a Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).
