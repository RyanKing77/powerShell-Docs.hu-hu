---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: Szoftverleltár-naplózás (SIL)
ms.openlocfilehash: b12cfc4ae1e505bbc4d47596bed9352ce53a98f2
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856167"
---
# <a name="software-inventory-logging-sil"></a>Szoftverleltár-naplózás (SIL)

> [!IMPORTANT]
> A WMF telepítése során egy Windows Server 2012 R2 kiszolgálóra, a szoftverleltár-Naplózás már fut a 5.x, szükség a Start-SilLogging parancsmag futtatása után a WMF telepítése után a telepítési folyamat protokollüzenetet le fog állni a szoftverleltár-naplózás funkció.

A szoftverleltár-naplózás segít helyben telepítve a kiszolgálón, de különösen környezetekben, sok kiszolgálón egy informatikai környezetben (feltéve, hogy a szoftver telepítve van és fut a Microsoft-szoftverekkel kapcsolatos pontos információk kezdeti üzemeltetési költségeinek csökkentése teljes informatikai környezet). A megadott egyet be van állítva, az adatok összesítő kiszolgálóra továbbítja, és egy egységes és automatikus folyamat segítségével egy helyen a naplóadatok gyűjtése.

Szoftverleltározási adatok minden olyan számítógépen közvetlen lekérdezésével is bejelentkezhet, amíg a szoftverleltár-naplózás, egy minden kiszolgáló által kezdeményezett (a hálózaton kívül) továbbítási architektúra alkalmazásával-szel kiküszöbölhetők a jellemző számos kiszolgáló felfedezésének kihívásai szoftver szoftverleltárazási és felügyeleti forgatókönyvek. A szoftverleltár-naplózás SSL használatával biztonságos HTTPS-kapcsolaton keresztül egy összesítő kiszolgálónak továbbított adatokat. Az adatok tárolása egyetlen helyen megkönnyíti az adatok elemzéséhez, módosítására és szükség esetén megoszthatja.

Semmilyen adatot küld a Microsoftnak a szolgáltatás funkcióinak részeként. A Szoftverleltár-naplózás adatait és funkcióit kizárólag a kiszolgálószoftver licencelt tulajdonosa és rendszergazdái használhatják.

További információkért és a szoftverleltár-naplózási parancsmagok kapcsolatban, tekintse meg a [kezelése a szoftverleltár-naplózás a Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383584(v=ws.11)).
