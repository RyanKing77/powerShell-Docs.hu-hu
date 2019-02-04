---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Továbbfejlesztett DSC-készítés összeállításhoz és együttműködéshez
ms.openlocfilehash: 3e40ba94de0a53c1c9663553c4ec443b5e0df3fd
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687173"
---
# <a name="advanced-dsc-authoring-for-composition-and-collaboration"></a>Továbbfejlesztett DSC-készítés összeállításhoz és együttműködéshez

Ez a cikk ismerteti a típusú megközelítések is elérhetők a konfigurációkat és erőforrásokat.
A cél az egyes forgatókönyvek megegyezik, ha több konfigurációt elérni a kiszolgáló telepítési befejezési állapota előnyben részesített csökkenthető.
Ilyen például a server-telepítés, például egy alkalmazás tulajdonosa, az alkalmazás állapotának és a egy központi csapat ad ki a változások a biztonsági előírások fenntartja eredményét hozzájáruló több csapat lenne.
Mindegyik megközelítésnek, beleértve az előnyökről és kockázatokról képességeiben részletes leírást talál itt.

![Folyamat](../images/Pipeline.jpg)

## <a name="types-of-collaborative-authoring-techniques"></a>Együttműködésen alapuló szerzői technikák típusai

Nincsenek a helyi Configuration Manager engedélyezéséhez a fogalom a beépített két megoldást:

| Koncepció | Részletes információk
|-|-
| Részleges konfigurációk | [Dokumentáció](../pull-server/partialConfigs.md)
| Összetett erőforrások | [Dokumentáció](../resources/authoringResourceComposite.md)

## <a name="understanding-the-impact-of-each-approach"></a>Mindegyik megközelítésnek hatásának ismertetése

Ezek a megoldások valamelyikét server-telepítés eredményét kezelésére használható.
Van azonban jelentős eltérés az egyes megközelítéssel hatását.

## <a name="partial-configurations"></a>Részleges konfigurációk

Részleges konfigurációk használata esetén a helyi Configuration Manager egymástól függetlenül kezelheti a több-konfiguráció van konfigurálva.
Konfigurációk lefordított egymástól függetlenül, és hozzárendeli a csomópontra.
Ehhez LCM előzetesen kell konfigurálni az egyes konfigurációkhoz nevére.

![PartialConfiguration](../images/PartialConfiguration.jpg)

Részleges konfigurációk biztosít két vagy több, a teams teljes a konfigurációs kiszolgáló, gyakran az az előnye, hogy a kommunikációs és együttműködési nélkül irányítására.

Ügyfeleknek adott arról, hogy az erőforrás-ütközéseket, véletlen felülbírálások és végső soron az eszköz irányítását valós konfigurációs elvesztését vezet.

Ezenkívül ügyfelek megadott visszajelzés, hogy ez a modell használata esetén minden egyes ellenőrző csapatok konfigurációs módosítások valószínűleg nem kell lett teljes körűen tesztelve keresztül egy kiadási folyamatot, éles környezetben váratlan eredményekhez vezet.

**Rendkívül fontos, hogy annak minden módosítások üzembehelyezési kiszolgálók ellenőrzésére használ, egyetlen folyamatot.**

Az alábbi ábrán a csapat B-csapat A. csapat A részleges konfigurációjuk kiadások, majd a saját teszteket futtat olyan kiszolgálón, mindkét konfigurációval a alkalmazni.
Ebben a modellben csak egy szolgáltató jogosult módosításokat éles környezetben.

![PartialSinglePipeline](../images/PartialSinglePipeline.jpg)

Ha módosítások szükségesek a csapat B, azok küldjön egy lekérési kérelmet csapat az A forrás-ellenőrzési környezet ellen.
Team A ezután lenne tekintse át a módosításokat, teszt automatizálással és kiadási éles bizalom, hogy a módosítások nem okoz hibák az alkalmazások vagy a kiszolgáló által üzemeltetett szolgáltatások esetén.

## <a name="composite-resources"></a>Összetett erőforrások

Egy összetett erőforrás egyszerűen egy alkalmazáscsomag-erőforrásként DSC-konfiguráció.
Nem vonatkoznak külön követelmények LCM konfigurálása az összetett erőforrások fogadására.
Új konfiguráció belül az erőforrásokat használják, és egy egyszerű fordítási eredményezi egy MOF-fájlt.

![CompositeResource](../images/CompositeResource.jpg)

Összetett erőforrások két gyakori forgatókönyv közül választhat.
Az első az összetettséget és a absztrakt egyedi fogalmai csökkentése érdekében.
A második pedig az, hogy az alapkonfigurációk csomagolható az alkalmazás csapatához biztonságosan a kibocsátási folyamat az éles környezetben keresztül üzembe, melyeknél sikeres az összes teszt után.

```PowerShell
Configuration Name
{
  File 1
  {
    Ensure = “Present”
    Path = “c:\inetpub\file1.zip”
    Source = “http://uri/file1.zip”
  }
  Service A
  {
    Ensure = “Present”
    Name = “ServiceA”
    Status = “Running”
  }
  SecurityBaseline Settings
  {
    Ensure = “Present”
    Datacenter = “NorthAmerica”
  }
}
```

Összetett erőforrások támogatása az összeállítás és a folyamat használatával működési lejárat kiépítésekor együttműködés

Előfordulhat, hogy már használni összetett erőforrások nélkül működnek együtt az azt.
Például **ServiceSet**.
Ehhez az erőforráshoz nélkül ajánlati őket egyenként több Windows-szolgáltatás állapotát kezeli.
A Name tulajdonság fogadja el a nevét, az egyes szolgáltatások karakterláncok tömbje.
A konfiguráció fordítása, amikor a MOF egy egyedi Service szolgáltatásról szóló szakasz fogja tartalmazni az egyes ServiceSet átadott neve.

Előfordulhat, hogy a szervezetek számára "az ügynökök" vagy "közbenső", amely minden olyan kiszolgálóra kell telepíteni.
Egy összetett erőforrás a legjobb választ a függőségeket, a telepítő és az ilyen eszközök és segédprogramok kezelése.

Az olyan személyt vagy csapatot, amelyek több kiszolgáló megoldásokért felelős készít egy rájuk vonatkozó követelményeket tartalmazó konfigurációt.
Ezután a konfiguráció lenne csomagolva, az összetett erőforrás dokumentáció utasításai összetett erőforrásként.
Végül közzé kell tenni az új összetett erőforrás, például a fájlmegosztást egy olyan helyre, vagy a NuGet hírcsatorna, ahol a alkalmazásfejlesztő csapat a konfigurációját felhasználását.

A csapat kiadott egy új verziót, valahányszor, akkor növelje a verziószámot a moduljegyzékben azok összetett erőforrás.
A alkalmazásfejlesztő csapatok dolgoznak a összetett erőforrás felvétel a konfigurációt, szerzői alkalmazásfüggőségek kezeléséhez.
Ha a műveletek vagy biztonsági csoportokkal az erőforrás egy új verziója engedje, értesítik a alkalmazásfejlesztő csapatok dolgoznak a módosítást.

A alkalmazásfejlesztő csapatok dolgoznak előfordulhat, hogy az éles környezetben, ahol az egyetlen változás az, hogy alaptervek kiadás indítása.
Azonban ez hatással van a alkalmazást, mielőtt egy szolgáltatás-kimaradás kockázatát kiértékelheti, hogy lehetőséget nyújt.

Megjegyzés – visszajelzés összetett erőforrások használatával kapcsolatban, hogy módosításokat igényel a kódja lefordításának és közzétesz egy új MOF kritika rendelkezik tartalmazza.
Ez az elvárt működés.
Minden új konfigurációs kiadás tartalmaznia kell egy statikus hivatkozás az egyes erőforrások egy meghatározott verzióra, és a vizsgálatokkal üzemi kiszolgáló-csomópontok elérése előtt ellenőrizni kell.
A folyamat tesztelése és a módosítások a forráskezelőből felszabadítása kis, de a gyakori kötegekben módosítása kiadása egy biztonságos környezetben hoz létre.

Alapvető infrastruktúra kezelése kiadási folyamatok használatával kapcsolatos további információkért lásd: [A kiadási adatfolyamat-modell](../further-reading/whitepapers.md).
