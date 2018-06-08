---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: e7198999c17b5c0d77724a82b322e6485065225e
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/07/2018
ms.locfileid: "34482845"
---
# <a name="software-inventory-logging-sil"></a>Szoftverleltár-naplózás (SIL)

**Fontos:** *WMF 5.0 telepíti egy Windows Server 2012 R2-kiszolgáló, hogy a szoftverleltár-Naplózás már fut, amikor szükség a WMF telepítése után egyszer a Start-SilLogging parancsmag futtatásához a telepítési folyamat protokollüzenetet leáll a Szoftver szoftverleltár-naplózási szolgáltatás.*

A szoftverleltár-naplózás segít csökkenteni az első olyan kiszolgálón, de különösen környezetekben, sok kiszolgálón (feltéve, hogy a szoftver telepítve van és fut, az informatikai környezetben található helyileg telepített Microsoft szoftverekkel kapcsolatos pontos információk lekérdezésének működési költségeit teljes informatikai környezet). Megadott beállított egyet, ezen adatok elküldhetők egy összesítő kiszolgálónak, és a naplózási adatok egy helyen gyűjtése egy egységes és automatikus folyamattal.

A szoftverleltáradatok számítógépenként közvetlen lekérdezésével is bejelentkezhet, a szoftverleltár-naplózás, egyes kiszolgálók által kezdeményezett, a továbbítási (a hálózaton kívül) küldési architektúra alkalmazásával leküzdheti de kapcsolatos számos jellemző server felfedezésének kihívásai szoftverleltárazási és eszközfelügyeleti forgatókönyvben. Védett adatok elküldhetők egy összesítő kiszolgálónak HTTPS-KAPCSOLATON keresztül továbbított szoftverleltár-naplózás SSL használatával. Az adatok tárolása egy helyen, könnyebben elemezhetők, módosíthatók és megoszthatja, ha szükséges.

Ezeket az adatokat a rendszer nem küldi el a Microsoft részére a szolgáltatás funkcióinak részeként. A Szoftverleltár-naplózás adatait és funkcióit kizárólag a kiszolgálószoftver licencelt tulajdonosa és rendszergazdái használhatják.

További információk és a szoftverleltár-naplózási parancsmagok vonatkozó dokumentációt, tekintse meg a Windows Server 2012 R2 online erőforrásokat érhet el <http://technet.microsoft.com/library/dn383584.aspx>.
