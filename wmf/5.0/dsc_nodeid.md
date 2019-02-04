---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 7a1725e3858c59a6d31699add22b042359c48463
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685759"
---
# <a name="separation-of-node-and-configuration-ids"></a>Csomópont- és konfigurációazonosítók szétválasztása

## <a name="overview"></a>Áttekintés

Annak érdekében, hogy egy rugalmasabb és zökkenőmentes élményt DSC lekéréses módban használatakor, ebben a kiadásban számos szolgáltatást hozzáadtuk. Ezeket a funkciókat, hogy könnyen beállítása és konfigurációk üzembe helyezése több csomóponton, miközben továbbra is állapotának nyomon követése az egyes csomópontok állapotinformációit reporting külön-külön is szolgálnak.
Ezek a funkciók a következők:

* A konfiguráció nevét, amely azonosítja a számítógép konfigurációja. Ez a név megosztható több cél csomópont
* Egy ügynök azonosítója, amely egyértelműen azonosít egy egycsomópontos
* Egy regisztrációs lépésre, amely csak akkor történik meg az első alkalommal egy célcsomóponttal csatlakozik egy lekéréses kiszolgálót

**Megjegyzés:** Ezek a szolgáltatások és funkciók lettek hozzáadva, és cserélje le a meglévő pull-szolgáltatások és fogalmak. Használhatja az új funkciók vagy az új lekéréses kiszolgálóval szállítási ebben a kiadásban a régieket.

További információkért lásd: [konfigurációs nevek lekérési ügyfél beállítása](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)
