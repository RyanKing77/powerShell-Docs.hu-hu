---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 5b9eea1c90bfd5a8cee3897d832bf7775a750308
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="separation-of-node-and-configuration-ids"></a>Csomópont- és konfigurációs azonosítókat elkülönítése

## <a name="overview"></a>Áttekintés

Ahhoz, hogy adjon meg egy rugalmas, és zökkenőmentes élményt, lekéréses módban a DSC használata esetén, ebben a kiadásban jelentek meg számos funkciót tartalmaz. Ezek a szolgáltatások célja, hogy engedélyezi, hogy könnyen beállítása beállításokat és telepíthet az csomópontokon, miközben továbbra is nyomon követési állapot külön-külön jelentési adatok az egyes csomópontok rugalmasan. Ezek a funkciók a következők:

* A konfiguráció nevét, amely azonosítja a számítógép konfigurációja. Ez a név több célcsomópontokat megoszthatók 
* Egy ügynök azonosítója, amely egyedileg azonosítja az egyetlen csomópont
* A lekérési kiszolgálójával csatlakozik egy regisztrációs lépés, amely csak akkor fordul elő, amikor első alkalommal egy célcsomóponttal

**Megjegyzés:** ezeket a szolgáltatásokat és funkciókat hozzá vannak adva, és nem váltják ki a meglévő lekéréses funkciók és fogalmak. Használhatja az új szolgáltatásokat vagy az új lekéréses kiszolgálóval szállítási ebben a kiadásban a régieket.

További információkért lásd: [konfigurációs nevek használatával lekéréses ügyfél beállítása](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)

