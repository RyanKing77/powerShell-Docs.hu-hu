---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Továbbfejlesztett DSC-készítés összeállításhoz és együttműködéshez
ms.openlocfilehash: 3e40ba94de0a53c1c9663553c4ec443b5e0df3fd
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404424"
---
# <a name="advanced-dsc-authoring-for-composition-and-collaboration"></a><span data-ttu-id="4f7aa-103">Továbbfejlesztett DSC-készítés összeállításhoz és együttműködéshez</span><span class="sxs-lookup"><span data-stu-id="4f7aa-103">Advanced DSC Authoring for Composition and Collaboration</span></span>

<span data-ttu-id="4f7aa-104">Ez a cikk ismerteti a típusú megközelítések is elérhetők a konfigurációkat és erőforrásokat.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-104">This article describes the types of approaches available for combining configurations and resources.</span></span>
<span data-ttu-id="4f7aa-105">A cél az egyes forgatókönyvek megegyezik, ha több konfigurációt elérni a kiszolgáló telepítési befejezési állapota előnyben részesített csökkenthető.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-105">The goal for each scenario is the same, to reduce complexity when multiple configurations are preferred to reach a server deployment end state.</span></span>
<span data-ttu-id="4f7aa-106">Ilyen például a server-telepítés, például egy alkalmazás tulajdonosa, az alkalmazás állapotának és a egy központi csapat ad ki a változások a biztonsági előírások fenntartja eredményét hozzájáruló több csapat lenne.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-106">An example of this would be multiple teams contributing to the outcome of a server deployment, such as an application owner maintaining the application state and a central team releasing changes to security baselines.</span></span>
<span data-ttu-id="4f7aa-107">Mindegyik megközelítésnek, beleértve az előnyökről és kockázatokról képességeiben részletes leírást talál itt.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-107">The nuances of each approach including the benefits and risks are detailed here.</span></span>

![Folyamat](../images/Pipeline.jpg)

## <a name="types-of-collaborative-authoring-techniques"></a><span data-ttu-id="4f7aa-109">Együttműködésen alapuló szerzői technikák típusai</span><span class="sxs-lookup"><span data-stu-id="4f7aa-109">Types of Collaborative Authoring Techniques</span></span>

<span data-ttu-id="4f7aa-110">Nincsenek a helyi Configuration Manager engedélyezéséhez a fogalom a beépített két megoldást:</span><span class="sxs-lookup"><span data-stu-id="4f7aa-110">There are two solutions built in to Local Configuration Manager to enable this concept:</span></span>

| <span data-ttu-id="4f7aa-111">Koncepció</span><span class="sxs-lookup"><span data-stu-id="4f7aa-111">Concept</span></span> | <span data-ttu-id="4f7aa-112">Részletes információk</span><span class="sxs-lookup"><span data-stu-id="4f7aa-112">Detailed Information</span></span>
|-|-
| <span data-ttu-id="4f7aa-113">Részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="4f7aa-113">Partial Configurations</span></span> | [<span data-ttu-id="4f7aa-114">Dokumentáció</span><span class="sxs-lookup"><span data-stu-id="4f7aa-114">Documentation</span></span>](../pull-server/partialConfigs.md)
| <span data-ttu-id="4f7aa-115">Összetett erőforrások</span><span class="sxs-lookup"><span data-stu-id="4f7aa-115">Composite Resources</span></span> | [<span data-ttu-id="4f7aa-116">Dokumentáció</span><span class="sxs-lookup"><span data-stu-id="4f7aa-116">Documentation</span></span>](../resources/authoringResourceComposite.md)

## <a name="understanding-the-impact-of-each-approach"></a><span data-ttu-id="4f7aa-117">Mindegyik megközelítésnek hatásának ismertetése</span><span class="sxs-lookup"><span data-stu-id="4f7aa-117">Understanding The Impact of Each Approach</span></span>

<span data-ttu-id="4f7aa-118">Ezek a megoldások valamelyikét server-telepítés eredményét kezelésére használható.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-118">Either of these solutions can be used to manage the outcome of a server deployment.</span></span>
<span data-ttu-id="4f7aa-119">Van azonban jelentős eltérés az egyes megközelítéssel hatását.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-119">However, there is significant difference in the impact of using each approach.</span></span>

## <a name="partial-configurations"></a><span data-ttu-id="4f7aa-120">Részleges konfigurációk</span><span class="sxs-lookup"><span data-stu-id="4f7aa-120">Partial Configurations</span></span>

<span data-ttu-id="4f7aa-121">Részleges konfigurációk használata esetén a helyi Configuration Manager egymástól függetlenül kezelheti a több-konfiguráció van konfigurálva.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-121">When using Partial Configurations, Local Configuration Manager is configured to manage multiple configurations independently.</span></span>
<span data-ttu-id="4f7aa-122">Konfigurációk lefordított egymástól függetlenül, és hozzárendeli a csomópontra.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-122">Configurations are compiled independently and then assigned to the node.</span></span>
<span data-ttu-id="4f7aa-123">Ehhez LCM előzetesen kell konfigurálni az egyes konfigurációkhoz nevére.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-123">This requires LCM to be configured in advance with the name of each configuration.</span></span>

![PartialConfiguration](../images/PartialConfiguration.jpg)

<span data-ttu-id="4f7aa-125">Részleges konfigurációk biztosít két vagy több, a teams teljes a konfigurációs kiszolgáló, gyakran az az előnye, hogy a kommunikációs és együttműködési nélkül irányítására.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-125">Partial Configurations provide two, or more, teams complete control over configuration of a server, often without the benefit of communication or collaboration.</span></span>

<span data-ttu-id="4f7aa-126">Ügyfeleknek adott arról, hogy az erőforrás-ütközéseket, véletlen felülbírálások és végső soron az eszköz irányítását valós konfigurációs elvesztését vezet.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-126">Customers have provided feedback that this can lead to resource conflicts, unintentional overrides, and ultimately loss of true configuration control of the asset.</span></span>

<span data-ttu-id="4f7aa-127">Ezenkívül ügyfelek megadott visszajelzés, hogy ez a modell használata esetén minden egyes ellenőrző csapatok konfigurációs módosítások valószínűleg nem kell lett teljes körűen tesztelve keresztül egy kiadási folyamatot, éles környezetben váratlan eredményekhez vezet.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-127">Additionally, customers have provided feedback that when using this model, each controlling teams configuration changes are unlikely to be fully tested through a release pipeline, leading to unexpected results in production.</span></span>

<span data-ttu-id="4f7aa-128">**Rendkívül fontos, hogy annak minden módosítások üzembehelyezési kiszolgálók ellenőrzésére használ, egyetlen folyamatot.**</span><span class="sxs-lookup"><span data-stu-id="4f7aa-128">**It is critical that a single pipeline be used to evaluate all changes release to servers.**</span></span>

<span data-ttu-id="4f7aa-129">Az alábbi ábrán a csapat B-csapat A. csapat A részleges konfigurációjuk kiadások, majd a saját teszteket futtat olyan kiszolgálón, mindkét konfigurációval a alkalmazni.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-129">In the illustration below, Team B releases their partial configuration to Team A. Team A then runs their tests against a server with both configurations applied.</span></span>
<span data-ttu-id="4f7aa-130">Ebben a modellben csak egy szolgáltató jogosult módosításokat éles környezetben.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-130">In this model, only one authority has permission to make changes in production.</span></span>

![PartialSinglePipeline](../images/PartialSinglePipeline.jpg)

<span data-ttu-id="4f7aa-132">Ha módosítások szükségesek a csapat B, azok küldjön egy lekérési kérelmet csapat az A forrás-ellenőrzési környezet ellen.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-132">When changes are required from Team B, they should submit a Pull Request against Team A's source control environment.</span></span>
<span data-ttu-id="4f7aa-133">Team A ezután lenne tekintse át a módosításokat, teszt automatizálással és kiadási éles bizalom, hogy a módosítások nem okoz hibák az alkalmazások vagy a kiszolgáló által üzemeltetett szolgáltatások esetén.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-133">Team A would then review the changes using test automation and release to production when there is confidence that the changes will not cause errors in the applications or services hosted by the server.</span></span>

## <a name="composite-resources"></a><span data-ttu-id="4f7aa-134">Összetett erőforrások</span><span class="sxs-lookup"><span data-stu-id="4f7aa-134">Composite Resources</span></span>

<span data-ttu-id="4f7aa-135">Egy összetett erőforrás egyszerűen egy alkalmazáscsomag-erőforrásként DSC-konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-135">A composite resource is simply a DSC Configuration packaged as a resource.</span></span>
<span data-ttu-id="4f7aa-136">Nem vonatkoznak külön követelmények LCM konfigurálása az összetett erőforrások fogadására.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-136">There are no special requirements for configuring LCM to accept composite resources.</span></span>
<span data-ttu-id="4f7aa-137">Új konfiguráció belül az erőforrásokat használják, és egy egyszerű fordítási eredményezi egy MOF-fájlt.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-137">The resources are used within a new configuration and a single compilation results in one MOF file.</span></span>

![CompositeResource](../images/CompositeResource.jpg)

<span data-ttu-id="4f7aa-139">Összetett erőforrások két gyakori forgatókönyv közül választhat.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-139">There are two common scenarios for composite resources.</span></span>
<span data-ttu-id="4f7aa-140">Az első az összetettséget és a absztrakt egyedi fogalmai csökkentése érdekében.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-140">The first is to reduce complexity and abstract unique concepts.</span></span>
<span data-ttu-id="4f7aa-141">A második pedig az, hogy az alapkonfigurációk csomagolható az alkalmazás csapatához biztonságosan a kibocsátási folyamat az éles környezetben keresztül üzembe, melyeknél sikeres az összes teszt után.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-141">The second is to allow baselines to be packaged for an application team to safely deploy through their release pipeline to production after all tests have passed.</span></span>

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

<span data-ttu-id="4f7aa-142">Összetett erőforrások támogatása az összeállítás és a folyamat használatával működési lejárat kiépítésekor együttműködés</span><span class="sxs-lookup"><span data-stu-id="4f7aa-142">Composite resources promote both composition and collaboration using a pipeline while building operational maturity</span></span>

<span data-ttu-id="4f7aa-143">Előfordulhat, hogy már használni összetett erőforrások nélkül működnek együtt az azt.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-143">You might be already using composite resources without realizing it.</span></span>
<span data-ttu-id="4f7aa-144">Például **ServiceSet**.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-144">An example is **ServiceSet**.</span></span>
<span data-ttu-id="4f7aa-145">Ehhez az erőforráshoz nélkül ajánlati őket egyenként több Windows-szolgáltatás állapotát kezeli.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-145">This resource manages the state of multiple Windows Services without listing them individually.</span></span>
<span data-ttu-id="4f7aa-146">A Name tulajdonság fogadja el a nevét, az egyes szolgáltatások karakterláncok tömbje.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-146">The Name property accepts an array of strings to provide the name of each service.</span></span>
<span data-ttu-id="4f7aa-147">A konfiguráció fordítása, amikor a MOF egy egyedi Service szolgáltatásról szóló szakasz fogja tartalmazni az egyes ServiceSet átadott neve.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-147">When the configuration is compiled, the MOF will contain a unique Service section for each of the Names passed to ServiceSet.</span></span>

<span data-ttu-id="4f7aa-148">Előfordulhat, hogy a szervezetek számára "az ügynökök" vagy "közbenső", amely minden olyan kiszolgálóra kell telepíteni.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-148">Organizations might have "agents" or "middleware" that should be installed on every server.</span></span>
<span data-ttu-id="4f7aa-149">Egy összetett erőforrás a legjobb választ a függőségeket, a telepítő és az ilyen eszközök és segédprogramok kezelése.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-149">A composite resource is the best answer to managing the dependencies, setup, and configuration of any such tools and utilities.</span></span>

<span data-ttu-id="4f7aa-150">Az olyan személyt vagy csapatot, amelyek több kiszolgáló megoldásokért felelős készít egy rájuk vonatkozó követelményeket tartalmazó konfigurációt.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-150">The person or team responsible for solutions that span multiple servers authors a configuration containing their requirements.</span></span>
<span data-ttu-id="4f7aa-151">Ezután a konfiguráció lenne csomagolva, az összetett erőforrás dokumentáció utasításai összetett erőforrásként.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-151">Next, the configuration would be packaged as a composite resource using instructions provided in the composite resource documentation.</span></span>
<span data-ttu-id="4f7aa-152">Végül közzé kell tenni az új összetett erőforrás, például a fájlmegosztást egy olyan helyre, vagy a NuGet hírcsatorna, ahol a alkalmazásfejlesztő csapat a konfigurációját felhasználását.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-152">Finally, the new composite resource should be published to a location such as a file share or NuGet feed where application teams can consume it in their configurations.</span></span>

<span data-ttu-id="4f7aa-153">A csapat kiadott egy új verziót, valahányszor, akkor növelje a verziószámot a moduljegyzékben azok összetett erőforrás.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-153">Each time the team releases a new version, they would increment the version number in the module manifest for their composite resource.</span></span>
<span data-ttu-id="4f7aa-154">A alkalmazásfejlesztő csapatok dolgoznak a összetett erőforrás felvétel a konfigurációt, szerzői alkalmazásfüggőségek kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-154">The application teams include the composite resource in the configuration they author for managing application dependencies.</span></span>
<span data-ttu-id="4f7aa-155">Ha a műveletek vagy biztonsági csoportokkal az erőforrás egy új verziója engedje, értesítik a alkalmazásfejlesztő csapatok dolgoznak a módosítást.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-155">When the Operations/Security teams release a new version of their resource, they notify the application teams of a new change.</span></span>

<span data-ttu-id="4f7aa-156">A alkalmazásfejlesztő csapatok dolgoznak előfordulhat, hogy az éles környezetben, ahol az egyetlen változás az, hogy alaptervek kiadás indítása.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-156">The application teams might trigger a release to production where the only change is to baselines.</span></span>
<span data-ttu-id="4f7aa-157">Azonban ez hatással van a alkalmazást, mielőtt egy szolgáltatás-kimaradás kockázatát kiértékelheti, hogy lehetőséget nyújt.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-157">However, this provides an opportunity to evaluate impact to applications before risk of a service outage.</span></span>

<span data-ttu-id="4f7aa-158">Megjegyzés – visszajelzés összetett erőforrások használatával kapcsolatban, hogy módosításokat igényel a kódja lefordításának és közzétesz egy új MOF kritika rendelkezik tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-158">Note - Feedback regarding the use of composite resources has included criticism that making changes requires compiling and releasing a new MOF.</span></span>
<span data-ttu-id="4f7aa-159">Ez az elvárt működés.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-159">This is by design.</span></span>
<span data-ttu-id="4f7aa-160">Minden új konfigurációs kiadás tartalmaznia kell egy statikus hivatkozás az egyes erőforrások egy meghatározott verzióra, és a vizsgálatokkal üzemi kiszolgáló-csomópontok elérése előtt ellenőrizni kell.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-160">Each new configuration release should include a static reference to a specific version of each resource, and should be validated by tests before reaching production server nodes.</span></span>
<span data-ttu-id="4f7aa-161">A folyamat tesztelése és a módosítások a forráskezelőből felszabadítása kis, de a gyakori kötegekben módosítása kiadása egy biztonságos környezetben hoz létre.</span><span class="sxs-lookup"><span data-stu-id="4f7aa-161">The process of testing and releasing changes from source control creates a safe environment for releasing change in small but frequent batches.</span></span>

<span data-ttu-id="4f7aa-162">Alapvető infrastruktúra kezelése kiadási folyamatok használatával kapcsolatos további információkért lásd: [A kiadási adatfolyamat-modell](../further-reading/whitepapers.md).</span><span class="sxs-lookup"><span data-stu-id="4f7aa-162">For more information about using release pipelines to manage core infrastructure, see the whitepaper: [The Release Pipeline Model](../further-reading/whitepapers.md).</span></span>
