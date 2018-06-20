---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 6c036c2d8f97e559d20dd3ac40133fa06f5dab08
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188285"
---
# <a name="separation-of-node-and-configuration-ids"></a>Csomópont- és konfigurációazonosítók szétválasztása

## <a name="overview"></a>Áttekintés

Ahhoz, hogy adjon meg egy rugalmas, és zökkenőmentes élményt, lekéréses módban a DSC használata esetén, ebben a kiadásban jelentek meg számos funkciót tartalmaz. Ezek a szolgáltatások célja, hogy engedélyezi, hogy könnyen beállítása beállításokat és telepíthet az csomópontokon, miközben továbbra is nyomon követési állapot külön-külön jelentési adatok az egyes csomópontok rugalmasan.
Ezek a funkciók a következők:

* A konfiguráció nevét, amely azonosítja a számítógép konfigurációja. Ez a név több célcsomópontokat megoszthatók
* Egy ügynök azonosítója, amely egyedileg azonosítja az egyetlen csomópont
* A lekérési kiszolgálójával csatlakozik egy regisztrációs lépés, amely csak akkor fordul elő, amikor első alkalommal egy célcsomóponttal

**Megjegyzés:** ezeket a szolgáltatásokat és funkciókat hozzá vannak adva, és nem váltják ki a meglévő lekéréses funkciók és fogalmak. Használhatja az új szolgáltatásokat vagy az új lekéréses kiszolgálóval szállítási ebben a kiadásban a régieket.

További információkért lásd: [konfigurációs nevek használatával lekéréses ügyfél beállítása](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)
