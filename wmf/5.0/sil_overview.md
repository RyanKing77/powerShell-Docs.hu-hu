---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 7e87ed4bc9a86be52d4d06d3e87386a1111227c5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686935"
---
# <a name="software-inventory-logging-sil"></a>Szoftverleltár-naplózás (SIL)

**FONTOS:** *A WMF 5.0 telepíti egy Windows Server 2012 R2 kiszolgálóra, a szoftverleltár-Naplózás már fut, esetén szükségesek, hogy a Start-SilLogging parancsmag egyszeri futtatás után telepítse a WMF, mivel a telepítési folyamat protokollüzenetet le fog állni a szoftverleltár-naplózás funkció.*

A szoftverleltár-naplózás segít helyben telepítve a kiszolgálón, de különösen környezetekben, sok kiszolgálón egy informatikai környezetben (feltéve, hogy a szoftver telepítve van és fut a Microsoft-szoftverekkel kapcsolatos pontos információk kezdeti üzemeltetési költségeinek csökkentése teljes informatikai környezet). A megadott egyet be van állítva, az adatok összesítő kiszolgálóra továbbítja, és egy egységes és automatikus folyamat segítségével egy helyen a naplóadatok gyűjtése.

Szoftverleltározási adatok minden olyan számítógépen közvetlen lekérdezésével is bejelentkezhet, amíg a szoftverleltár-naplózás, egy minden kiszolgáló által kezdeményezett (a hálózaton kívül) továbbítási architektúra alkalmazásával-szel kiküszöbölhetők a jellemző számos kiszolgáló felfedezésének kihívásai szoftver szoftverleltárazási és felügyeleti forgatókönyvek. A szoftverleltár-naplózás SSL használatával biztonságos HTTPS-kapcsolaton keresztül egy összesítő kiszolgálónak továbbított adatokat. Az adatok tárolása egyetlen helyen megkönnyíti az adatok elemzéséhez, módosítására és szükség esetén megoszthatja.

Semmilyen adatot küld a Microsoftnak a szolgáltatás funkcióinak részeként. A Szoftverleltár-naplózás adatait és funkcióit kizárólag a kiszolgálószoftver licencelt tulajdonosa és rendszergazdái használhatják.

További információkért és a szoftverleltár-naplózási parancsmagok kapcsolatban, tekintse meg az online erőforrások Windows Server 2012 R2 <http://technet.microsoft.com/library/dn383584.aspx>.
