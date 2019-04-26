---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Lekérési kiszolgáló – ajánlott eljárások
ms.openlocfilehash: fe483a487f85f2e4edb0928fccfe98746ae11231
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079200"
---
# <a name="pull-server-best-practices"></a><span data-ttu-id="bdd0d-103">Lekérési kiszolgáló – ajánlott eljárások</span><span class="sxs-lookup"><span data-stu-id="bdd0d-103">Pull server best practices</span></span>

<span data-ttu-id="bdd0d-104">A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="bdd0d-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bdd0d-105">A lekéréses kiszolgálón (Windows-szolgáltatás *DSC-szolgáltatás*), a Windows Server támogatott összetevője létezik azonban tervekben sem funkciókat és képességeket kínálnak.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="bdd0d-106">Javasoljuk, hogy helyeződnek felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (beleértve a lekéréses kiszolgálón a Windows Server csomagban) vagy a közösségi megoldások felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="bdd0d-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="bdd0d-107">Összefoglalás: Ez a dokumentum célja a folyamat és bővíthetőség felhőkarrierre készítik megoldás-mérnökök segítségét.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-107">Summary: This document is intended to include process and extensibility to assist engineers who are preparing for the solution.</span></span> <span data-ttu-id="bdd0d-108">Részletek ajánlott eljárásokat kell biztosítania, ügyfél által azonosított, és a termék csapatától javaslatok jövőbeli irányuló és stabil tekinthető majd érvényesíteni.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-108">Details should provide best practices as identified by customers and then validated by the product team to ensure recommendations are future facing and considered stable.</span></span>

| |<span data-ttu-id="bdd0d-109">Dokumentum adatai</span><span class="sxs-lookup"><span data-stu-id="bdd0d-109">Doc Info</span></span>|
|:---|:---|
<span data-ttu-id="bdd0d-110">Szerző</span><span class="sxs-lookup"><span data-stu-id="bdd0d-110">Author</span></span> | <span data-ttu-id="bdd0d-111">Michael Greene</span><span class="sxs-lookup"><span data-stu-id="bdd0d-111">Michael Greene</span></span>
<span data-ttu-id="bdd0d-112">Lektorok</span><span class="sxs-lookup"><span data-stu-id="bdd0d-112">Reviewers</span></span> | <span data-ttu-id="bdd0d-113">Ben Gelens, Ravikanth Chaganti, Aleksandar Nikolic</span><span class="sxs-lookup"><span data-stu-id="bdd0d-113">Ben Gelens, Ravikanth Chaganti, Aleksandar Nikolic</span></span>
<span data-ttu-id="bdd0d-114">Közzétett</span><span class="sxs-lookup"><span data-stu-id="bdd0d-114">Published</span></span> | <span data-ttu-id="bdd0d-115">2015. április</span><span class="sxs-lookup"><span data-stu-id="bdd0d-115">April, 2015</span></span>

## <a name="abstract"></a><span data-ttu-id="bdd0d-116">Absztrakt</span><span class="sxs-lookup"><span data-stu-id="bdd0d-116">Abstract</span></span>

<span data-ttu-id="bdd0d-117">Jelen dokumentum célja, hogy mindenkinek, aki egy Windows PowerShell Desired State Configuration lekéréses kiszolgálón megvalósítás hivatalos útmutatást.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-117">This document is designed to provide official guidance for anyone planning for a Windows PowerShell Desired State Configuration pull server implementation.</span></span> <span data-ttu-id="bdd0d-118">Egy lekéréses kiszolgálót az egyszerű szolgáltatás csak perc alatt üzembe helyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-118">A pull server is a simple service that should take only minutes to deploy.</span></span> <span data-ttu-id="bdd0d-119">Bár ez a dokumentum műszaki útmutatókról, a központi telepítés használható tartalmazni fogja, ez a dokumentum értéke az ajánlott eljárásokat, és milyen üzembe helyezése előtt gondolja át hivatkozásként.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-119">Although this document will offer technical how-to guidance that can be used in a deployment, the value of this document is as a reference for best practices and what to think about before deploying.</span></span>
<span data-ttu-id="bdd0d-120">Olvasói rendelkeznie kell a DSC alapszintű ismeretét, és az összetevők leírására szolgáló a feltételeket, amelyek központi telepítésben lévő a DSC.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-120">Readers should have basic familiarity with DSC, and the terms used to describe the components that are included in a DSC deployment.</span></span> <span data-ttu-id="bdd0d-121">További információkért lásd: a [Windows PowerShell Desired State Configuration áttekintése](/powershell/dsc/overview) témakör.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-121">For more information, see the [Windows PowerShell Desired State Configuration Overview](/powershell/dsc/overview)  topic.</span></span>
<span data-ttu-id="bdd0d-122">DSC elvárt való összpontosításnak köszönhetően felhőalapú kiadása ütemben történik, az alapul szolgáló technológiát, beleértve a lekéréses kiszolgálón is várható fejlődnek, és új lehetőségeket biztosítanak.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-122">As DSC is expected to evolve at cloud cadence, the underlying technology including pull server is also expected to evolve and to introduce new capabilities.</span></span> <span data-ttu-id="bdd0d-123">Ez a dokumentum egy verzió tábla tartalmaz, amely a korábbi kiadásokban mutató hivatkozások és a jövőbeli akik megoldások előretekintő tervek ösztönzése mutató hivatkozásokat biztosít a függelékben.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-123">This document includes a version table in the appendix that provides references to previous releases and references to future looking solutions to encourage forward-looking designs.</span></span>

<span data-ttu-id="bdd0d-124">A két fő szakasz ebben a dokumentumban:</span><span class="sxs-lookup"><span data-stu-id="bdd0d-124">The two major sections of this document:</span></span>

- <span data-ttu-id="bdd0d-125">Konfiguráció tervezése</span><span class="sxs-lookup"><span data-stu-id="bdd0d-125">Configuration Planning</span></span>
- <span data-ttu-id="bdd0d-126">Telepítési útmutató</span><span class="sxs-lookup"><span data-stu-id="bdd0d-126">Installation Guide</span></span>

### <a name="versions-of-the-windows-management-framework"></a><span data-ttu-id="bdd0d-127">A Windows Management Framework verziói</span><span class="sxs-lookup"><span data-stu-id="bdd0d-127">Versions of the Windows Management Framework</span></span>

<span data-ttu-id="bdd0d-128">A jelen dokumentumban lévő információk célja a alkalmazni a Windows Management Framework 5.0.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-128">The information in this document is intended to apply to Windows Management Framework 5.0.</span></span> <span data-ttu-id="bdd0d-129">Bár a WMF 5.0 nem kötelező központi telepítésére és a egy lekéréses kiszolgálót működő, a 5.0-s verzió a lépéseknek az ismertetése, ez a dokumentum.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-129">While WMF 5.0 is not required for deploying and operating a pull server, version 5.0 is the focus of this document.</span></span>

### <a name="windows-powershell-desired-state-configuration"></a><span data-ttu-id="bdd0d-130">Windows PowerShell Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="bdd0d-130">Windows PowerShell Desired State Configuration</span></span>

<span data-ttu-id="bdd0d-131">Desired State Configuration (DSC) egy felügyeleti platform, amely lehetővé teszi a konfigurációs adatokat, üzembe helyezése és felügyelete egy ipar szintaxisa a Managed Object Format (MOF) nevű leíró a Common Information Model (CIM) használatával.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-131">Desired State Configuration (DSC) is a management platform that enables deploying and managing configuration data by using an industry syntax named the Managed Object Format (MOF) to describe the Common Information Model (CIM).</span></span> <span data-ttu-id="bdd0d-132">Egy nyílt forráskódú projekt, nyissa meg a Management Infrastructure (OMI) további ezeknek a szabványoknak a fejlesztés különböző platformokon, beleértve a Linux és a hálózati hardverek, operációs rendszerek létezik.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-132">An open source project, Open Management Infrastructure (OMI), exists to further development of these standards across platforms including Linux and network hardware operating systems.</span></span> <span data-ttu-id="bdd0d-133">További információkért lásd: a [összekapcsolása a MOF-specifikációk DMTF lap](https://www.dmtf.org/standards/cim), és [OMI a következő dokumentumok és a forrás](https://collaboration.opengroup.org/omi/documents.php).</span><span class="sxs-lookup"><span data-stu-id="bdd0d-133">For more information, see the [DMTF page linking to MOF specifications](https://www.dmtf.org/standards/cim), and [OMI Documents and Source](https://collaboration.opengroup.org/omi/documents.php).</span></span>

<span data-ttu-id="bdd0d-134">Windows PowerShell egy nyelvet bővítménycsomag biztosít a Desired State Configuration, amellyel létrehozása és kezelése a deklaratív konfigurációkat.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-134">Windows PowerShell provides a set of language extensions for Desired State Configuration that you can use to create and manage declarative configurations.</span></span>

### <a name="pull-server-role"></a><span data-ttu-id="bdd0d-135">Kérje le a kiszolgálói szerepkör</span><span class="sxs-lookup"><span data-stu-id="bdd0d-135">Pull server role</span></span>

<span data-ttu-id="bdd0d-136">Egy lekéréses kiszolgálót biztosít lesznek elérhetőek a célcsomópontokat konfigurációk tárolásához egy központosított szolgáltatásba.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-136">A pull server provides a centralized service to store configurations that will be accessible to target nodes.</span></span>

<span data-ttu-id="bdd0d-137">A pull-kiszolgálói szerepkör egy Web Server-példányt vagy SMB-fájlmegosztásra is telepíthető.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-137">The pull server role can be deployed as either a Web Server instance or an SMB file share.</span></span> <span data-ttu-id="bdd0d-138">A web server funkció OData illesztőfelületet tartalmazza, és szükség esetén belefoglalhatja vissza erősítse meg a sikeres vagy sikertelen jelentés, mivel a beállítások vannak érvényben a célcsomópontokat képességeit.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-138">The web server capability includes an OData interface and can optionally include capabilities for target nodes to report back confirmation of success or failure as configurations are applied.</span></span> <span data-ttu-id="bdd0d-139">Ez a funkció olyan környezetben hasznos, ahol sok célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-139">This functionality is useful in environments where there are a large number of target nodes.</span></span>
<span data-ttu-id="bdd0d-140">Egy célcsomóponttal (más néven ügyfél) konfigurálását, hogy a lekéréses kiszolgálóra mutasson a legújabb konfigurációt követő adatokat, és minden szükséges szkriptek vannak letöltésére és alkalmazására.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-140">After configuring a target node (also referred to as a client) to point to the pull server the latest configuration data and any required scripts are downloaded and applied.</span></span> <span data-ttu-id="bdd0d-141">Ez akkor fordulhat elő, egy egyszeri központi telepítést, vagy egy újra előforduló feladatot, amely is lehetővé teszi a lekéréses kiszolgálón fontos eszközt nagy mennyiségű módosítás kezeléséhez.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-141">This can happen as a one-time deployment or as a re-occurring job which also makes the pull server an important asset for managing change at scale.</span></span> <span data-ttu-id="bdd0d-142">További információkért lásd: [Windows PowerShell Desired State Configuration lekéréses kiszolgálók](/powershell/dsc/pullServer) és</span><span class="sxs-lookup"><span data-stu-id="bdd0d-142">For more information, see [Windows PowerShell Desired State Configuration Pull Servers](/powershell/dsc/pullServer) and</span></span>

<span data-ttu-id="bdd0d-143">[Leküldéses és lekéréses konfigurációs módjai](/powershell/dsc/pullServer).</span><span class="sxs-lookup"><span data-stu-id="bdd0d-143">[Push and Pull Configuration Modes](/powershell/dsc/pullServer).</span></span>

## <a name="configuration-planning"></a><span data-ttu-id="bdd0d-144">Konfiguráció tervezése</span><span class="sxs-lookup"><span data-stu-id="bdd0d-144">Configuration planning</span></span>

<span data-ttu-id="bdd0d-145">Minden vállalati szoftverek központi telepítéséhez nincs információ előre gyűjtött a megfelelő architektúra tervezésének segítéséhez és elő kell készíteni a a telepítés befejezéséhez szükséges lépéseket.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-145">For any enterprise software deployment there is information that can be collected in advance to help plan for the correct architecture and to be prepared for the steps required to complete the deployment.</span></span> <span data-ttu-id="bdd0d-146">A következő szakaszok előkészítése és a szervezeti kapcsolatokat, amelyek valószínűleg fordulhat elő, előre kell kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-146">The following sections provide information regarding how to prepare and the organizational connections that will likely need to happen in advance.</span></span>

### <a name="software-requirements"></a><span data-ttu-id="bdd0d-147">Szoftverkövetelmények</span><span class="sxs-lookup"><span data-stu-id="bdd0d-147">Software requirements</span></span>

<span data-ttu-id="bdd0d-148">Egy lekéréses kiszolgálót telepítése a DSC szolgáltatás Windows Server igényel.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-148">Deployment of a pull server requires the DSC Service feature of Windows Server.</span></span> <span data-ttu-id="bdd0d-149">Ez a funkció a Windows Server 2012-ben jelent meg, és folyamatban lévő verziók Windows Management Framework (WMF) keresztül frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-149">This feature was introduced in Windows Server 2012, and has been updated through ongoing releases of Windows Management Framework (WMF).</span></span>

### <a name="software-downloads"></a><span data-ttu-id="bdd0d-150">Az ügyfélszoftver-letöltési</span><span class="sxs-lookup"><span data-stu-id="bdd0d-150">Software downloads</span></span>

<span data-ttu-id="bdd0d-151">Telepíti a legújabb tartalom a Windows Update, kívül két letöltések üzembe helyezése egy DSC lekéréses kiszolgálót célszerű figyelembe venni: A Windows Management Framework, és a DSC-modul a pull-kiszolgáló üzembe helyezésének automatizálása legújabb verzióját.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-151">In addition to installing the latest content from Windows Update, there are two downloads considered best practice to deploy a DSC pull server: The latest version of Windows Management Framework, and a DSC module to automate pull server provisioning.</span></span>

### <a name="wmf"></a><span data-ttu-id="bdd0d-152">WMF</span><span class="sxs-lookup"><span data-stu-id="bdd0d-152">WMF</span></span>

<span data-ttu-id="bdd0d-153">A Windows Server 2012 R2 tartalmaz egy a DSC szolgáltatás nevű funkciót.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-153">Windows Server 2012 R2 includes a feature named the DSC Service.</span></span> <span data-ttu-id="bdd0d-154">A DSC szolgáltatás lekéréses server funkciókat, beleértve a bináris fájlokat, amelyek támogatják az OData-végpont biztosítja.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-154">The DSC Service feature provides the pull server functionality, including the binaries that support the OData endpoint.</span></span>
<span data-ttu-id="bdd0d-155">A WMF része a Windows Server, és a egy Agilis kiadása ütemben történik a Windows Server-kiadások között frissül.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-155">WMF is included in Windows Server and is updated on an agile cadence between Windows Server releases.</span></span> <span data-ttu-id="bdd0d-156">[A WMF 5.0 új verzióinak](https://www.microsoft.com/en-us/download/details.aspx?id=54616) a DSC szolgáltatás frissítéseket is tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-156">[New versions of WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=54616)  can include updates to the DSC Service feature.</span></span> <span data-ttu-id="bdd0d-157">Emiatt tanácsos egy töltse le a WMF legújabb kiadását, és tekintse át a kibocsátási megjegyzéseket határozza meg, ha a kiadás a DSC szolgáltatás frissítését tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-157">For this reason, it is a best practice to download the latest release of WMF and to review the release notes to determine if the release includes an update to the DSC service feature.</span></span> <span data-ttu-id="bdd0d-158">Emellett tekintse át a kibocsátási megjegyzések a szakaszában, amely azt jelzi-e egy update vagy a forgatókönyv tervezési állapota stabil vagy kísérleti szerepel a listán.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-158">You should also review the section of the release notes that indicates whether the design status for an update or scenario is listed as stable or experimental.</span></span>
<span data-ttu-id="bdd0d-159">Ahhoz, hogy egy Agilis kiadási ciklus egyes funkciókat is deklarálni stabil, ami azt jelenti, hogy a szolgáltatás készen áll az előzetes verzióban jelent meg a WMF közben is az éles környezetben használható.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-159">To allow for an agile release cycle, individual features can be declared stable, which indicates the feature is ready to be used in a production environment even while WMF is released in preview.</span></span>
<span data-ttu-id="bdd0d-160">Egyéb szolgáltatások hagyományosan frissítve lett-e a WMF-verziók (lásd a további részletek a WMF kibocsátási megjegyzései):</span><span class="sxs-lookup"><span data-stu-id="bdd0d-160">Other features that have historically been updated by WMF releases (see the WMF Release Notes for further detail):</span></span>

- <span data-ttu-id="bdd0d-161">Windows PowerShell Windows PowerShell integrált parancsfájlkezelési</span><span class="sxs-lookup"><span data-stu-id="bdd0d-161">Windows PowerShell Windows PowerShell Integrated Scripting</span></span>
- <span data-ttu-id="bdd0d-162">Környezet (ISE) Windows PowerShell webszolgáltatások (Management OData</span><span class="sxs-lookup"><span data-stu-id="bdd0d-162">Environment (ISE) Windows PowerShell Web Services (Management OData</span></span>
- <span data-ttu-id="bdd0d-163">IIS-bővítmény) Windows PowerShell Desired State Configuration (DSC)</span><span class="sxs-lookup"><span data-stu-id="bdd0d-163">IIS Extension)  Windows PowerShell Desired State Configuration (DSC)</span></span>
- <span data-ttu-id="bdd0d-164">Windows Rendszerfelügyeleti (webszolgáltatások WinRM) Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="bdd0d-164">Windows Remote Management (WinRM) Windows Management Instrumentation (WMI)</span></span>

### <a name="dsc-resource"></a><span data-ttu-id="bdd0d-165">DSC-erőforrás</span><span class="sxs-lookup"><span data-stu-id="bdd0d-165">DSC resource</span></span>

<span data-ttu-id="bdd0d-166">Egy lekéréses kiszolgálót üzembe helyezési is egyszerűbb legyen a létesítési DSC konfigurációs parancsfájl használata a szolgáltatás által.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-166">A pull server deployment can be simplified by provisioning the service using a DSC configuration script.</span></span> <span data-ttu-id="bdd0d-167">Ez a dokumentum tartalmaz egy éles készen áll a kiszolgáló-csomóponton üzembe helyezéséhez használható konfigurációs parancsfájlokat.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-167">This document includes configuration scripts that can be used to deploy a production ready server node.</span></span> <span data-ttu-id="bdd0d-168">A konfigurációs parancsfájlokat használ, a DSC-modul szükség, amely nem tartalmazza a Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-168">To use the configuration scripts, a DSC module is required that is not included in Windows Server.</span></span> <span data-ttu-id="bdd0d-169">A szükséges modulnév **xPSDesiredStateConfiguration**, amely tartalmazza a DSC-erőforrás **xDscWebService**.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-169">The required module name is **xPSDesiredStateConfiguration**, which includes the DSC resource **xDscWebService**.</span></span> <span data-ttu-id="bdd0d-170">A xPSDesiredStateConfiguration modul letölthető [Itt](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).</span><span class="sxs-lookup"><span data-stu-id="bdd0d-170">The xPSDesiredStateConfiguration module can be downloaded [here](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).</span></span>

<span data-ttu-id="bdd0d-171">Használja a `Install-Module` parancsmagot a **PowerShellGet** modul.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-171">Use the `Install-Module` cmdlet from the **PowerShellGet** module.</span></span>

```powershell
Install-Module xPSDesiredStateConfiguration
```

<span data-ttu-id="bdd0d-172">A **PowerShellGet** modul tölti le a modult:</span><span class="sxs-lookup"><span data-stu-id="bdd0d-172">The **PowerShellGet** module will download the module to:</span></span>

`C:\Program Files\Windows PowerShell\Modules`

<span data-ttu-id="bdd0d-173">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="bdd0d-173">Planning task</span></span>|
---|
<span data-ttu-id="bdd0d-174">Rendelkezik hozzáféréssel a telepítési fájlok, Windows Server 2012 R2?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-174">Do you have access to the installation files for Windows Server 2012 R2?</span></span>|
<span data-ttu-id="bdd0d-175">Töltse le a WMF és a modul az online katalógusból internetes hozzáférést kap az üzembehelyezési környezetet?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-175">Will the deployment environment have Internet access to download WMF and the module from the online gallery?</span></span>|
<span data-ttu-id="bdd0d-176">Hogyan telepíti az operációs rendszer telepítése után a legújabb biztonsági frissítéseket?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-176">How will you install the latest security updates after installing the operating system?</span></span>|
<span data-ttu-id="bdd0d-177">A környezet van Internet-hozzáférés frissítések beszerzésére, vagy fog rendelkezni a helyi Windows Server Update Services (WSUS) kiszolgáló?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-177">Will the environment have Internet access to obtain updates, or will it have a local Windows Server Update Services (WSUS) server?</span></span>|
<span data-ttu-id="bdd0d-178">Rendelkeznek hozzáféréssel a Windows Server telepítési fájlok, amelyek már tartalmazzák az offline injektálási frissítéseit?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-178">Do you have access to Windows Server installation files that already include updates through offline injection?</span></span>|

### <a name="hardware-requirements"></a><span data-ttu-id="bdd0d-179">Hardverkövetelmények</span><span class="sxs-lookup"><span data-stu-id="bdd0d-179">Hardware requirements</span></span>

<span data-ttu-id="bdd0d-180">Kérje le a telepítések támogatottak a fizikai és virtuális kiszolgáló.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-180">Pull server deployments are supported on both physical and virtual servers.</span></span> <span data-ttu-id="bdd0d-181">A lekéréses kiszolgálón méretezési követelményei összhangba kerüljenek a Windows Server 2012 R2 követelményei.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-181">The sizing requirements for pull server align with the requirements for Windows Server 2012 R2.</span></span>

<span data-ttu-id="bdd0d-182">CPU: 1,4 GHz-es 64 bites processzor, memória: 512 MB szabad lemezterület: 32 GB-os hálózati: Gigabit Ethernet Adapter</span><span class="sxs-lookup"><span data-stu-id="bdd0d-182">CPU: 1.4 GHz 64-bit processor Memory: 512 MB Disk Space: 32 GB Network: Gigabit Ethernet Adapter</span></span>

<span data-ttu-id="bdd0d-183">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="bdd0d-183">Planning task</span></span>|
---|
<span data-ttu-id="bdd0d-184">Telepíti a fizikai hardver- vagy virtualizációs platformon?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-184">Will you deploy on physical hardware or on a virtualization platform?</span></span>|
<span data-ttu-id="bdd0d-185">Mi az a folyamat egy új kiszolgálót a célkörnyezethez kéréséhez?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-185">What is the process to request a new server for your target environment?</span></span>|
<span data-ttu-id="bdd0d-186">Mi az a kiszolgáló elérhető legyen, az átlagos válaszidő?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-186">What is the average turnaround time for a server to become available?</span></span>|
<span data-ttu-id="bdd0d-187">Milyen méretű server kérés?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-187">What size server will you request?</span></span>|

### <a name="accounts"></a><span data-ttu-id="bdd0d-188">Fiókok</span><span class="sxs-lookup"><span data-stu-id="bdd0d-188">Accounts</span></span>

<span data-ttu-id="bdd0d-189">Nem vonatkoznak szolgáltatási fiók követelmények egy lekéréses kiszolgálót példány üzembe helyezéséhez.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-189">There are no service account requirements to deploy a pull server instance.</span></span>
<span data-ttu-id="bdd0d-190">Vannak azonban forgatókönyvek, ahol a webhely futhat egy helyi felhasználói fiók kontextusában.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-190">However, there are scenarios where the website could run in the context of a local user account.</span></span>
<span data-ttu-id="bdd0d-191">Például ha egy szükséges hozzáférést egy storage-megosztásban webhely tartalmát, és a Windows Server vagy az eszköz, a storage-megosztás üzemeltetési nem lesznek tartományhoz.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-191">For example, if there is a need to access a storage share for website content and either the Windows Server or the device hosting the storage share are not domain joined.</span></span>

### <a name="dns-records"></a><span data-ttu-id="bdd0d-192">DNS records</span><span class="sxs-lookup"><span data-stu-id="bdd0d-192">DNS records</span></span>

<span data-ttu-id="bdd0d-193">Szüksége lesz a kívánt kiszolgáló nevét használja, ha az ügyfelek egy lekéréses kiszolgálót környezetben dolgozhat.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-193">You will need a server name to use when configuring clients to work with a pull server environment.</span></span>
<span data-ttu-id="bdd0d-194">A tesztelési jellemzően a kiszolgáló állomásnevét vagy a kiszolgáló IP-címét is használható, ha a DNS-névfeloldás nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-194">In test environments, typically the server hostname is used, or the IP address for the server can be used if DNS name resolution is not available.</span></span>
<span data-ttu-id="bdd0d-195">Az éles környezetben, vagy egy laborkörnyezetben, amelyek célja, hogy az éles környezet jelölik az ajánlott eljárás az hozzon létre egy DNS CNAME-rekordot.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-195">In production environments or in a lab environment that is intended to represent a production deployment, the best practice is to create a DNS CNAME record.</span></span>

<span data-ttu-id="bdd0d-196">Egy DNS CNAME rekord lehetővé teszi, hogy hozzon létre egy alias tekintse meg a gazdagép (A) rekordot.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-196">A DNS CNAME allows you to create an alias to refer to your host (A) record.</span></span>
<span data-ttu-id="bdd0d-197">A további rekordhoz célja egy módosítást kell kérni a jövőben rugalmasság növelésére.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-197">The intent of the additional name record is to increase flexibility should a change be required in the future.</span></span>
<span data-ttu-id="bdd0d-198">Egy olyan CNAME REKORDOT segít elkülöníteni az ügyfél-konfiguráció, így, például kicserél egy lekéréses kiszolgálót, vagy további pull-kiszolgálók hozzáadása a kiszolgálói környezet módosításai nem követeli meg az ügyfél-konfiguráció megfelelő módosítása.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-198">A CNAME can help to isolate the client configuration so that changes to the server environment, such as replacing a pull server or adding additional pull servers, will not require a corresponding change to the client configuration.</span></span>

<span data-ttu-id="bdd0d-199">Egy nevet a DNS-rekord kiválasztásakor tartsa szem előtt a megoldásarchitektúra.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-199">When choosing a name for the DNS record, keep the solution architecture in mind.</span></span>
<span data-ttu-id="bdd0d-200">Ha használ terheléselosztási funkciók, a HTTPS-kapcsolaton keresztül a forgalom védelmére használt tanúsítvány neve megegyezik a DNS-rekord kell.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-200">If using load balancing, the certificate used to secure traffic over HTTPS will need to share the same name as the DNS record.</span></span>

<span data-ttu-id="bdd0d-201">Forgatókönyv</span><span class="sxs-lookup"><span data-stu-id="bdd0d-201">Scenario</span></span> |<span data-ttu-id="bdd0d-202">Ajánlott eljárás</span><span class="sxs-lookup"><span data-stu-id="bdd0d-202">Best Practice</span></span>
:---|:---
<span data-ttu-id="bdd0d-203">Tesztkörnyezet</span><span class="sxs-lookup"><span data-stu-id="bdd0d-203">Test Environment</span></span> |<span data-ttu-id="bdd0d-204">Reprodukálja a tervezett éles környezetben, ha lehetséges.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-204">Reproduce the planned production environment, if possible.</span></span> <span data-ttu-id="bdd0d-205">A kiszolgáló állomásnevét egyszerű konfigurációk esetén ideális választás.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-205">A server hostname is suitable for simple configurations.</span></span> <span data-ttu-id="bdd0d-206">DNS nem érhető el, ha egy IP-címet egy állomásnév helyett használhatók.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-206">If DNS is not available, an IP address may be used in lieu of a hostname.</span></span>|
<span data-ttu-id="bdd0d-207">Egy csomópontos központi telepítés</span><span class="sxs-lookup"><span data-stu-id="bdd0d-207">Single Node Deployment</span></span> |<span data-ttu-id="bdd0d-208">Hozzon létre egy DNS CNAME-rekordot, amely a kiszolgáló állomásnevét.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-208">Create a DNS CNAME record that points to the server hostname.</span></span>|

<span data-ttu-id="bdd0d-209">További információkért lásd: [DNS ciklikus időszeletelés konfigurálása a Windows Server](/previous-versions/windows/it-pro/windows-server-2003/cc787484(v=ws.10)).</span><span class="sxs-lookup"><span data-stu-id="bdd0d-209">For more information, see [Configuring DNS Round Robin in Windows Server](/previous-versions/windows/it-pro/windows-server-2003/cc787484(v=ws.10)).</span></span>

<span data-ttu-id="bdd0d-210">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="bdd0d-210">Planning task</span></span>|
---|
<span data-ttu-id="bdd0d-211">Tudta, hogy kihez kell fordulnia, hogy a DNS-rekordok létrehozott és módosított?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-211">Do you know who to contact to have DNS records created and changed?</span></span>|
<span data-ttu-id="bdd0d-212">Mi a DNS-rekordra vonatkozó kérelmek átlagos felülvizsgálatának?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-212">What is the average turnaround for a request for a DNS record?</span></span>|
<span data-ttu-id="bdd0d-213">Szükséges a kiszolgálók statikus állomásnevet (A) rekordok kérelem?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-213">Do you need to request static Hostname (A) records for servers?</span></span>|
<span data-ttu-id="bdd0d-214">Mit fog kér, egy CNAME rekord?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-214">What will you request as a CNAME?</span></span>|
<span data-ttu-id="bdd0d-215">Ha szükséges, hogy milyen típusú terheléselosztási megoldás, felhasznál?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-215">If needed, what type of Load Balancing solution will you utilize?</span></span> <span data-ttu-id="bdd0d-216">(lásd a részre terheléselosztás részletekért)</span><span class="sxs-lookup"><span data-stu-id="bdd0d-216">(see section titled Load Balancing for details)</span></span>|

### <a name="public-key-infrastructure"></a><span data-ttu-id="bdd0d-217">Nyilvános kulcsokra épülő infrastruktúra</span><span class="sxs-lookup"><span data-stu-id="bdd0d-217">Public Key Infrastructure</span></span>

<span data-ttu-id="bdd0d-218">A legtöbb szervezet ma szükséges, hogy hálózati forgalmat, különösen olyan forgalmat, hogy hogyan kiszolgálók konfigurálva vannak, például bizalmas adatokat tartalmazó ellenőrizni kell, illetve átvitel során titkosítva vannak.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-218">Most organizations today require that network traffic, especially traffic that includes such sensitive data as how servers are configured, must be validated and/or encrypted during transit.</span></span>
<span data-ttu-id="bdd0d-219">Bár egy lekéréses kiszolgálót, amely elősegíti a HTTP-n keresztül telepíthető az ügyfélkérelmek törölje a szöveget, hogy az ajánlott eljárás a HTTPS PROTOKOLLT használó biztonságos forgalom.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-219">While it is possible to deploy a pull server using HTTP which facilitates client requests in clear text, it is a best practice to secure traffic using HTTPS.</span></span> <span data-ttu-id="bdd0d-220">A szolgáltatás beállítható úgy, hogy a különböző paraméterek használatával a DSC-erőforrás a HTTPS használatára **xPSDesiredStateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-220">The service can be configured to use HTTPS using a set of parameters in the DSC resource **xPSDesiredStateConfiguration**.</span></span>

<span data-ttu-id="bdd0d-221">A tanúsítványokra vonatkozó követelményeket a biztonságos HTTPS-forgalmat a lekéréses kiszolgálón eltérése nem mint bármely más HTTPS webhely biztonságossá tételéhez.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-221">The certificate requirements to secure HTTPS traffic for pull server are not different than securing any other HTTPS web site.</span></span> <span data-ttu-id="bdd0d-222">A **webkiszolgáló** egy Windows Server tanúsítványszolgáltatási sablon megfelel a szükséges képességek.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-222">The **Web Server** template in a Windows Server Certificate Services satisfies the required capabilities.</span></span>

<span data-ttu-id="bdd0d-223">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="bdd0d-223">Planning task</span></span>|
---|
<span data-ttu-id="bdd0d-224">Ha eszköztanúsítvány-kérelmeket a rendszer nem automatikus, akik szükség lesz egy tanúsítványt a kérelmekre kapcsolódni?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-224">If certificate requests are not automated, who will you need to contact to requests a certificate?</span></span>|
<span data-ttu-id="bdd0d-225">Mi az a kérelem az átlagos válaszidejű, optimalizált?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-225">What is the average turnaround for the request?</span></span>|
<span data-ttu-id="bdd0d-226">Hogyan fogja a tanúsítványfájl adni az Ön számára?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-226">How will the certificate file be transferred to you?</span></span>|
<span data-ttu-id="bdd0d-227">Hogyan fogja a tanúsítvány titkos kulcsa adni az Ön számára?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-227">How will the certificate private key be transferred to you?</span></span>|
<span data-ttu-id="bdd0d-228">Mennyi ideig tart az alapértelmezett lejárati idő?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-228">How long is the default expiration time?</span></span>|
<span data-ttu-id="bdd0d-229">Rendelkezik, a DNS-nevet a pull-kiszolgálói környezet, a tanúsítvány neve használható elszámolása?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-229">Have you settled on a DNS name for the pull server environment, that you can use for the certificate name?</span></span>|

### <a name="choosing-an-architecture"></a><span data-ttu-id="bdd0d-230">Az architektúra kiválasztása</span><span class="sxs-lookup"><span data-stu-id="bdd0d-230">Choosing an architecture</span></span>

<span data-ttu-id="bdd0d-231">Egy lekéréses kiszolgálót is telepíthető, vagy egy webes üzemeltetett szolgáltatás az IIS- vagy SMB-fájlmegosztás segítségével.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-231">A pull server can be deployed using either a web service hosted on IIS, or an SMB file share.</span></span> <span data-ttu-id="bdd0d-232">A legtöbb esetben nagyobb rugalmasságot biztosít a web service lehetőséget.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-232">In most situations, the web service option will provide greater flexibility.</span></span> <span data-ttu-id="bdd0d-233">Már nem ritka, hogy HTTPS-forgalmat haladnak át a hálózati határok, mivel az SMB-forgalom gyakran szűrt vagy letiltott hálózatok között.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-233">It is not uncommon for HTTPS traffic to traverse network boundaries, whereas SMB traffic is often filtered or blocked between networks.</span></span> <span data-ttu-id="bdd0d-234">A web service is lehetősége a megfelelési kiszolgáló vagy a webes Reporting Manager (mindkét ezeket egy jövőbeli verziójában ez a dokumentum az témakörök), amely az ügyfelek állapot jelentése egy központi látható-e a kiszolgálóra egy olyan mechanizmust kínál.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-234">The web service also offers the option to include a Conformance Server or Web Reporting Manager (both topics to be addressed in a future version of this document) that provide a mechanism for clients to report status back to a server for centralized visibility.</span></span>
<span data-ttu-id="bdd0d-235">SMB környezetekben, ahol házirend előírja, hogy a webkiszolgáló nem használhatók fel, és az egyéb környezeti követelményeket, amelyek elérhetőbbé teszik a webkiszolgálói szerepkör nemkívánatos lehetőséget biztosít.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-235">SMB provides an option for environments where policy dictates that a web server should not be utilized, and for other environmental requirements that make a web server role undesirable.</span></span>
<span data-ttu-id="bdd0d-236">Mindkét esetben ne felejtse el a követelményeknek, az aláíráshoz és a forgalom titkosítása értékelheti ki.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-236">In either case, remember to evaluate the requirements for signing and encrypting traffic.</span></span> <span data-ttu-id="bdd0d-237">IPSEC-házirendek, HTTPS és SMB-aláírást mellett szóló érvek összes módon.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-237">HTTPS, SMB signing, and IPSEC policies are all options worth considering.</span></span>

#### <a name="load-balancing"></a><span data-ttu-id="bdd0d-238">Terheléselosztás</span><span class="sxs-lookup"><span data-stu-id="bdd0d-238">Load balancing</span></span>

<span data-ttu-id="bdd0d-239">A web service kommunikáló ügyfelek indítson egy információt, amely egy választ adott vissza.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-239">Clients interacting with the web service make a request for information that is returned in a single response.</span></span> <span data-ttu-id="bdd0d-240">Nem egymást követő kéréseket szükségesek, így nem szükséges a terheléselosztási platform munkamenetek karbantartása bármikor egyetlen kiszolgálón az idő biztosítása érdekében.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-240">No sequential requests are required, so it is not necessary for the load balancing platform to ensure sessions are maintained on a single server at any point in time.</span></span>

<span data-ttu-id="bdd0d-241">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="bdd0d-241">Planning task</span></span>|
---|
<span data-ttu-id="bdd0d-242">Milyen megoldás elosztja a forgalmat kiszolgálók használható?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-242">What solution will be used for load balancing traffic across servers?</span></span>|
<span data-ttu-id="bdd0d-243">Ha hardveres terheléselosztót, akik tart egy új konfiguráció hozzáadása az eszközre irányuló kérelem használatával?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-243">If using a hardware load balancer, who will take a request to add a new configuration to the device?</span></span>|
<span data-ttu-id="bdd0d-244">Mi az a konfigurálása egy új betöltés kérelmek átlagos felülvizsgálatának elosztott terhelésű webszolgáltatást?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-244">What is the average turnaround for a request to configure a new load balanced web service?</span></span>|
<span data-ttu-id="bdd0d-245">Milyen információt szükséges a kérelem lesz?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-245">What information will be required for the request?</span></span>|
<span data-ttu-id="bdd0d-246">Meg kell kérnie egy további IP-cím, vagy a terheléselosztás felelős csapat kezeli, amely?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-246">Will you need to request an additional IP or will the team responsible for load balancing handle that?</span></span>|
<span data-ttu-id="bdd0d-247">Rendelkezik a szükséges DNS-rekordokat, és ez szükség lesz a terheléselosztási megoldás konfigurálása felelős csapat?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-247">Do you have the DNS records needed, and will this be required by the team responsible for configuring the load balancing solution?</span></span>|
<span data-ttu-id="bdd0d-248">A teherelosztási szolgáltatás nem követeli meg, hogy a nyilvános kulcsokra épülő infrastruktúra kell kezelnie a az eszközt, vagy tudja azt terheléselosztása HTTPS-forgalmat, mindaddig, amíg nem vonatkoznak munkamenet követelmények?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-248">Does the load balancing solution require that PKI be handled by the device or can it load balance HTTPS traffic as long as there are no session requirements?</span></span>|

### <a name="staging-configurations-and-modules-on-the-pull-server"></a><span data-ttu-id="bdd0d-249">Átmeneti konfigurációk és a modulok a lekérési kiszolgálón</span><span class="sxs-lookup"><span data-stu-id="bdd0d-249">Staging configurations and modules on the pull server</span></span>

<span data-ttu-id="bdd0d-250">A konfiguráció tervezése részeként szüksége lesz úgy gondolja, hogy mely DSC kapcsolatos modulok és konfigurációk üzemeltetett a lekéréses kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-250">As part of configuration planning, you will need to think about which DSC modules and configurations will be hosted by the pull server.</span></span> <span data-ttu-id="bdd0d-251">Konfiguráció tervezése szempontjából fontos alapfokon bemutatja, hogyan készítheti elő és a egy lekéréses kiszolgálót telepít tartalmat.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-251">For the purpose of configuration planning it is important to have a basic understanding of how to prepare and deploy content to a pull server.</span></span>

<span data-ttu-id="bdd0d-252">A jövőben ez a szakasz kiterjesztett lesz, és az DSC lekéréses kiszolgálón található az üzemeltetési útmutatóban.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-252">In the future, this section will be expanded and included in an Operations Guide for DSC Pull Server.</span></span>  <span data-ttu-id="bdd0d-253">Útmutató a modulok és konfigurációk kezelése az automation idővel napi folyamatát ismertetik.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-253">The guide will discuss the day to day process for managing modules and configurations over time with automation.</span></span>

#### <a name="dsc-modules"></a><span data-ttu-id="bdd0d-254">DSC-modulok</span><span class="sxs-lookup"><span data-stu-id="bdd0d-254">DSC modules</span></span>

<span data-ttu-id="bdd0d-255">Egy konfigurációs kérő ügyfelek kell a szükséges modulok DSC.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-255">Clients that request a configuration will need the required DSC modules.</span></span> <span data-ttu-id="bdd0d-256">A lekéréses kiszolgálón egy funkciója, automatizálhatja a DSC-modulok az ügyfelek igény szerinti eloszlása.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-256">A functionality of the pull server is to automate distribution on demand of DSC modules to clients.</span></span> <span data-ttu-id="bdd0d-257">Ha helyez üzembe egy lekéréses kiszolgálót az első alkalommal esetleg labor vagy a koncepció igazolása, valószínűleg fog függenek a DSC-modulok által biztosított nyilvános adattár, például a PowerShell-Galériával vagy a modulok DSC PowerShell.org GitHub-adattárak .</span><span class="sxs-lookup"><span data-stu-id="bdd0d-257">If you are deploying a pull server for the first time, perhaps as a lab or proof of concept, you are likely going to depend on DSC modules that are available from public repositories such as the PowerShell Gallery or the PowerShell.org GitHub repositories for DSC modules.</span></span>

<span data-ttu-id="bdd0d-258">Fontos megjegyezni, hogy még a megbízható online forrásokból, például a PowerShell-galériából, egy nyilvános-tárházból letölti modulok át kell tekintenie valaki a PowerShell és a környezetben, ahol a modulok lesz ismerete éles környezetben használt előtt használt.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-258">It is critical to remember that even for trusted online sources such as the PowerShell Gallery, any module that is downloaded from a public repository should be reviewed by someone with PowerShell experience and knowledge of the environment where the modules will be used prior to being used in production.</span></span> <span data-ttu-id="bdd0d-259">Ez a feladat végrehajtása során, egy jó ideje a modul, amely például a dokumentáció és szkriptek eltávolítható minden olyan további hasznos kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-259">While completing this task it is a good time to check for any additional payload in the module that can be removed such as documentation and example scripts.</span></span> <span data-ttu-id="bdd0d-260">Ez csökkenti a hálózati sávszélesség, az első kérelem ügyfelenként amikor modulok letölti az ügyfél-kiszolgálóról a hálózaton keresztül.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-260">This will reduce the network bandwidth per client in their first request, when modules will be downloaded over the network from server to client.</span></span>

<span data-ttu-id="bdd0d-261">Minden modul be kell csomagolni, egy meghatározott formátumban, egy ZIP-fájlt, amely tartalmazza a modul hasznos ModuleName_Version.zip nevű.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-261">Each module must be packaged in a specific format, a ZIP file named ModuleName_Version.zip that contains the module payload.</span></span> <span data-ttu-id="bdd0d-262">Miután a kiszolgálóra, létre kell hozni egy ellenőrzőösszeg fájlt másolja a fájlt.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-262">After the file is copied to the server a checksum file must be created.</span></span> <span data-ttu-id="bdd0d-263">Amikor az ügyfelek csatlakoznak a kiszolgálóhoz, ellenőrizze, hogy a tartalom a DSC-modul közzététele óta nem módosult az ellenőrzőösszeg szolgál.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-263">When clients connect to the server, the checksum is used to verify the content of the DSC module has not changed since it was published.</span></span>

```powershell
New-DscChecksum -ConfigurationPath .\ -OutPath .\
```

<span data-ttu-id="bdd0d-264">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="bdd0d-264">Planning task</span></span>|
---|
<span data-ttu-id="bdd0d-265">Ha azt tervezi, milyen forgatókönyvekre kulcsával ellenőrzi egy teszt vagy a labor környezetben?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-265">If you are planning a test or lab environment which scenarios are key to validate?</span></span>|
<span data-ttu-id="bdd0d-266">Vannak-e, amit fedezésére erőforrásait tartalmazó nyilvánosan elérhető modulok vagy lesz szüksége ahhoz, hogy saját erőforrásokat?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-266">Are there publicly available modules that contain resources to cover everything you need or will you need to author your own resources?</span></span>|
<span data-ttu-id="bdd0d-267">Nyilvános modulok beolvasása internetes hozzáférést kap a környezet?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-267">Will your environment have Internet access to retrieve public modules?</span></span>|
<span data-ttu-id="bdd0d-268">Ki legyen a felelős a DSC-modulok áttekintése?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-268">Who will be responsible for reviewing DSC modules?</span></span>|
<span data-ttu-id="bdd0d-269">Ha azt tervezi, hogy éles környezetben mit fog használni mint egy helyi tárház tárolására a modulok DSC?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-269">If you are planning a production environment what will you use as a local repository for storing DSC modules?</span></span>|
<span data-ttu-id="bdd0d-270">A központi csapat elfogadja a alkalmazásfejlesztő csapatok dolgoznak a DSC-modulok?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-270">Will a central team accept DSC modules from application teams?</span></span> <span data-ttu-id="bdd0d-271">Mi lesz a folyamat?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-271">What will the process be?</span></span>|
<span data-ttu-id="bdd0d-272">Csomagolás, a másolás és a egy éles használatra kész DSC modulok ellenőrzőösszeg létrehozása a kiszolgálóra, a forrás-adattárból fogja automatizálni?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-272">Will you automate packaging, copying, and creating a checksum for production-ready DSC modules to the server, from your source repo?</span></span>|
<span data-ttu-id="bdd0d-273">A csapat lesz az automatizálási platform, valamint kezeléséért?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-273">Will your team be responsible for managing the automation platform as well?</span></span>|

#### <a name="dsc-configurations"></a><span data-ttu-id="bdd0d-274">DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="bdd0d-274">DSC configurations</span></span>

<span data-ttu-id="bdd0d-275">Egy lekéréses kiszolgálót az a célja, hogy központi DSC-konfigurációk ügyfél csomópontokra terjesztése mechanizmus biztosítására.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-275">The purpose of a pull server is to provide a centralized mechanism for distributing DSC configurations to client nodes.</span></span> <span data-ttu-id="bdd0d-276">A konfigurációk tárolása a kiszolgálón a MOF-dokumentumok formájában.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-276">The configurations are stored on the server as MOF documents.</span></span>
<span data-ttu-id="bdd0d-277">Egyes dokumentumok egyedi lesznek elnevezve **Guid**.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-277">Each document will be named with a unique **Guid**.</span></span> <span data-ttu-id="bdd0d-278">Ha az ügyfelek csatlakozni egy lekérési kiszolgálóval van konfigurálva, akkor is kapnak a **Guid** kérelmeznie kell a konfiguráció.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-278">When clients are configured to connect with a pull server, they are also given the **Guid** for the configuration they should request.</span></span> <span data-ttu-id="bdd0d-279">A rendszer konfigurációinak konfigurációk szerinti hivatkozó **Guid** garantálja a globális egyedi-e, és rugalmas, hogy egy konfiguráció alkalmazható granularitással csomópontonként, illetve a kiszolgálók számát, amely elvben kiterjedő szerepkör konfigurálása azonos konfigurációkat.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-279">This system of referencing configurations by **Guid** guarantees global uniqueness and is flexible such that a configuration can be applied with granularity per node, or as a role configuration that spans many servers that should have identical configurations.</span></span>

#### <a name="guids"></a><span data-ttu-id="bdd0d-280">GUID-azonosítói</span><span class="sxs-lookup"><span data-stu-id="bdd0d-280">Guids</span></span>

<span data-ttu-id="bdd0d-281">Konfiguráció tervezése **GUID** egy lekéréses kiszolgálót fejlesztésig fájlszerkesztés további figyelmet ér.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-281">Planning for configuration **Guids** is worth additional attention when thinking through a pull server deployment.</span></span> <span data-ttu-id="bdd0d-282">Nem adott követelmény, hogy hogyan kezelje **GUID** és a folyamat valószínű oka az, hogy az egyes környezetekhez egyedi legyen.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-282">There is no specific requirement for how to handle **Guids** and the process is likely to be unique for each environment.</span></span> <span data-ttu-id="bdd0d-283">A folyamat között lehet egyszerű egészen az összetettekig: központilag tárolt CSV-fájlba, egy egyszerű SQL-táblára, a CMDB vagy egy másik eszköz vagy szoftver megoldás integrációt igénylő összetett megoldás.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-283">The process can range from simple to complex: a centrally stored CSV file, a simple SQL table, a CMDB, or a complex solution requiring integration with another tool or software solution.</span></span> <span data-ttu-id="bdd0d-284">Kétféleképpen általános:</span><span class="sxs-lookup"><span data-stu-id="bdd0d-284">There are two general approaches:</span></span>

- <span data-ttu-id="bdd0d-285">**GUID-ok hozzárendelése kiszolgálónként** – mérhető, hogy minden kiszolgáló konfigurációs külön-külön szabályozott alkalmazunk.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-285">**Assigning Guids per server** — Provides a measure of assurance that every server configuration is controlled individually.</span></span> <span data-ttu-id="bdd0d-286">Ez pontosság körül frissítéseket biztosít, és jól néhány kiszolgálókkal környezetben is működik.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-286">This provides a level of precision around updates and can work well in environments with few servers.</span></span>
- <span data-ttu-id="bdd0d-287">**GUID-ok hozzárendelése egy kiszolgálói szerepkör** – minden kiszolgálón, amely ugyanazt a funkciót, például a webkiszolgálók, ugyanaz a GUID azonosító használatával a szükséges konfigurációs adatokra hivatkoznak.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-287">**Assigning Guids per server role** — All servers that perform the same function, such as web servers, use the same GUID to reference the required configuration data.</span></span>  <span data-ttu-id="bdd0d-288">Vegye figyelembe, hogy ha ugyanaz a GUID kiszolgálók számát, ezek mindegyike frissülnek egyszerre a konfiguráció módosításakor.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-288">Be aware that if many servers share the same GUID, all of them would be updated simultaneously when the configuration changes.</span></span>

  <span data-ttu-id="bdd0d-289">A globálisan egyedi Azonosítót a bizalmas adatok tekintendők, mert sikerült adatbáziscsoportok próbál a jeggyel intelligencia kiszolgálók üzembe helyezve és konfigurálva a környezetben az illető ártó szándékkal rendelkező bármely személy.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-289">The GUID is something that should be considered sensitive data because it could be leveraged by someone with malicious intent to gain intelligence about how servers are deployed and configured in your environment.</span></span> <span data-ttu-id="bdd0d-290">További információkért lásd: [biztonságosan lefoglalása a PowerShell Desired State Configuration lekéréses módban GUID](https://blogs.msdn.microsoft.com/powershell/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode/).</span><span class="sxs-lookup"><span data-stu-id="bdd0d-290">For more information, see [Securely allocating Guids in PowerShell Desired State Configuration Pull Mode](https://blogs.msdn.microsoft.com/powershell/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode/).</span></span>

<span data-ttu-id="bdd0d-291">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="bdd0d-291">Planning task</span></span>|
---|
<span data-ttu-id="bdd0d-292">Ki legyen a felelős, amikor készen állnak a konfigurációk a másolási a lekéréses kiszolgálón mappát?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-292">Who will be responsible for copying configurations in to the pull server folder when they are ready?</span></span>|
<span data-ttu-id="bdd0d-293">Ha konfigurációk egy alkalmazás csapat munkafolyamatokba(n), mi a folyamat lesz kiosztják őket?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-293">If Configurations are authored by an application team, what will the process be to hand them off?</span></span>|
<span data-ttu-id="bdd0d-294">Kihasználhatja a tárház konfigurációk tárolását azok alatt munkafolyamatokba(n), különböző csapatokkal?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-294">Will you leverage a repository to store configurations as they are being authored, across teams?</span></span>|
<span data-ttu-id="bdd0d-295">Automatizálhatja a folyamat konfigurációk másolása a kiszolgálóhoz és a egy ellenőrzőösszeg létrehozása, ha készen áll?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-295">Will you automate the process of copying configurations to the server and creating a checksum when they are ready?</span></span>|
<span data-ttu-id="bdd0d-296">Hogyan fogja leképez GUID szerverek és szerepkörök, és ez helyét?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-296">How will you map Guids to servers or roles, and where will this be stored?</span></span>|
<span data-ttu-id="bdd0d-297">Mit fog használni egy folyamatot, az ügyfélgépek konfigurálása, és hogyan fogja azt integrálása a folyamat létrehozása és tárolása a konfigurációs GUID?</span><span class="sxs-lookup"><span data-stu-id="bdd0d-297">What will you use as a process to configure client machines, and how will it integrate with your process for creating and storing Configuration Guids?</span></span>|

## <a name="installation-guide"></a><span data-ttu-id="bdd0d-298">Telepítési útmutató</span><span class="sxs-lookup"><span data-stu-id="bdd0d-298">Installation Guide</span></span>

<span data-ttu-id="bdd0d-299">*Ebben a dokumentumban megadott parancsfájlok használata a stabil példákat. Mindig tekintse át parancsfájl alaposan azokat éles környezetben a végrehajtása előtt.*</span><span class="sxs-lookup"><span data-stu-id="bdd0d-299">*Scripts given in this document are stable examples. Always review scripts carefully before executing them in a production environment.*</span></span>

### <a name="prerequisites"></a><span data-ttu-id="bdd0d-300">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="bdd0d-300">Prerequisites</span></span>

<span data-ttu-id="bdd0d-301">A következő parancs használatával ellenőrizze a PowerShell verzióját a kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-301">To verify the version of PowerShell on your server use the following command.</span></span>

```powershell
$PSVersionTable.PSVersion
```

<span data-ttu-id="bdd0d-302">Ha lehetséges frissítse a legújabb Windows Management Framework.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-302">If possible, upgrade to the latest version of Windows Management Framework.</span></span>
<span data-ttu-id="bdd0d-303">Ezután töltse le a `xPsDesiredStateConfiguration` modul a következő paranccsal.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-303">Next, download the `xPsDesiredStateConfiguration` module using the following command.</span></span>

```powershell
Install-Module xPSDesiredStateConfiguration
```

<span data-ttu-id="bdd0d-304">A parancs a modul letöltése előtt a jóváhagyását kéri.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-304">The command will ask for your approval before downloading the module.</span></span>

### <a name="installation-and-configuration-scripts"></a><span data-ttu-id="bdd0d-305">Telepítés és konfigurálás parancsfájlok</span><span class="sxs-lookup"><span data-stu-id="bdd0d-305">Installation and configuration scripts</span></span>

<span data-ttu-id="bdd0d-306">A DSC lekéréses kiszolgálón telepítendő a legjobb módszer, hogy a DSC-konfigurációs parancsprogram használata.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-306">The best method to deploy a DSC pull server is to use a DSC configuration script.</span></span> <span data-ttu-id="bdd0d-307">Ez a dokumentum bemutatja a parancsfájlok, beleértve a két alapszintű beállítás, amely csak a DSC-webszolgáltatás konfigurálására és a speciális beállításokat, amelyeket szeretne egy Windows Server teljes körű többek között DSC webszolgáltatás konfigurálása.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-307">This document will present scripts including both basic settings that would configure only the DSC web service and advanced settings that would configure a Windows Server end-to-end including DSC web service.</span></span>

<span data-ttu-id="bdd0d-308">Megjegyzés:  Jelenleg a `xPSDesiredStateConfiguration` DSC modulnak szüksége van a kiszolgálóra, hogy EN-US területi beállítás.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-308">Note:  Currently the `xPSDesiredStateConfiguration` DSC module requires the server to be EN-US locale.</span></span>

### <a name="basic-configuration-for-windows-server-2012"></a><span data-ttu-id="bdd0d-309">A Windows Server 2012 alapvető konfigurációs</span><span class="sxs-lookup"><span data-stu-id="bdd0d-309">Basic configuration for Windows Server 2012</span></span>

```powershell
# This is a very basic Configuration to deploy a pull server instance in a lab environment on Windows Server 2012.

Configuration PullServer {
Import-DscResource -ModuleName xPSDesiredStateConfiguration

        # Load the Windows Server DSC Service feature
        WindowsFeature DSCServiceFeature
        {
          Ensure = 'Present'
          Name = 'DSC-Service'
        }

        # Use the DSC Resource to simplify deployment of the web service
        xDSCWebService PSDSCPullServer
        {
          Ensure = 'Present'
          EndpointName = 'PSDSCPullServer'
          Port = 8080
          PhysicalPath = "$env:SYSTEMDRIVE\inetpub\wwwroot\PSDSCPullServer"
          CertificateThumbPrint = 'AllowUnencryptedTraffic'
          ModulePath = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
          ConfigurationPath = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
          State = 'Started'
          DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
}
PullServer -OutputPath 'C:\PullServerConfig\'
Start-DscConfiguration -Wait -Force -Verbose -Path 'C:\PullServerConfig\'
```

### <a name="advanced-configuration-for-windows-server-2012-r2"></a><span data-ttu-id="bdd0d-310">A Windows Server 2012 R2 speciális konfiguráció</span><span class="sxs-lookup"><span data-stu-id="bdd0d-310">Advanced configuration for Windows Server 2012 R2</span></span>

```powershell
# This is an advanced Configuration example for Pull Server production deployments on Windows Server 2012 R2.
# Many of the features demonstrated are optional and provided to demonstrate how to adapt the Configuration for multiple scenarios
# Select the needed resources based on the requirements for each environment.
# Optional scenarios include:
#      * Reduce footprint to Server Core
#      * Rename server and join domain
#      * Switch from SSL to TLS for HTTPS
#      * Automatically load certificate from Certificate Authority
#      * Locate Modules and Configuration data on remote SMB share
#      * Manage state of default websites in IIS

param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [System.String] $ServerName,
        [System.String] $DomainName,
        [System.String] $CARootName,
        [System.String] $CAServerFQDN,
        [System.String] $CertSubject,
        [System.String] $SMBShare,
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PsCredential] $Credential
    )

Configuration PullServer {
    Import-DscResource -ModuleName xPSDesiredStateConfiguration, xWebAdministration, xCertificate, xComputerManagement
    Node localhost
    {

        # Configure the server to automatically corret configuration drift including reboots if needed.
        LocalConfigurationManager
        {
            ConfigurationMode = 'ApplyAndAutoCorrect'
            RebootNodeifNeeded = $node.RebootNodeifNeeded
            CertificateId = $node.Thumbprint
        }

        # Remove all GUI interfaces so the server has minimum running footprint.
        WindowsFeature ServerCore
        {
            Ensure = 'Absent'
            Name = 'User-Interfaces-Infra'
        }

        # Set the server name and if needed, join a domain. If not joining a domain, remove the DomainName parameter.
        xComputer DomainJoin
        {
            Name = $Node.ServerName
            DomainName = $Node.DomainName
            Credential = $Node.Credential
        }

        # The next series of settings disable SSL and enable TLS, for environments where that is required by policy.
        Registry TLS1_2ServerEnabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'
            ValueName = 'Enabled'
            ValueData = 1
            ValueType = 'Dword'
        }

        Registry TLS1_2ServerDisabledByDefault
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server'
            ValueName = 'DisabledByDefault'
            ValueData = 0
            ValueType = 'Dword'
        }

        Registry TLS1_2ClientEnabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'
            ValueName = 'Enabled'
            ValueData = 1
            ValueType = 'Dword'
        }

        Registry TLS1_2ClientDisabledByDefault
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client'
            ValueName = 'DisabledByDefault'
            ValueData = 0
            ValueType = 'Dword'
        }

        Registry SSL2ServerDisabled
        {
            Ensure = 'Present'
            Key = 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server'
            ValueName = 'Enabled'
            ValueData = 0
            ValueType = 'Dword'
        }

        # Install the Windows Server DSC Service feature
        WindowsFeature DSCServiceFeature
        {
            Ensure = 'Present'
            Name = 'DSC-Service'
        }

        # If using a certificate from a local Active Directory Enterprise Root Certificate Authority, complete a request and install the certificate
        xCertReq SSLCert
        {
            CARootName = $Node.CARootName
            CAServerFQDN = $Node.CAServerFQDN
            Subject = $Node.CertSubject
            AutoRenew = $Node.AutoRenew
            Credential = $Node.Credential
        }

        # Use the DSC resource to simplify deployment of the web service.  You might also consider modifying the default port, possibly leveraging port 443 in environments where that is enforced as a standard.
        xDSCWebService PSDSCPullServer
        {
            Ensure = 'Present'
            EndpointName = 'PSDSCPullServer'
            Port = 8080
            PhysicalPath = "$env:SYSTEMDRIVE\inetpub\wwwroot\PSDSCPullServer"
            CertificateThumbPrint = 'CertificateSubject'
            CertificateSubject = $Node.CertSubject
            ModulePath = "$($Node.SMBShare)\DscService\Modules"
            ConfigurationPath = "$($Node.SMBShare)\DscService\Configuration"
            State = 'Started'
            DependsOn = '[WindowsFeature]DSCServiceFeature'
        }

        # Validate web config file contains current DB settings
        xWebConfigKeyValue CorrectDBProvider
        {
            ConfigSection = 'AppSettings'
            Key = 'dbprovider'
            Value = 'System.Data.OleDb'
            WebsitePath = 'IIS:\sites\PSDSCPullServer'
            DependsOn = '[xDSCWebService]PSDSCPullServer'
        }
        xWebConfigKeyValue CorrectDBConnectionStr
        {
            ConfigSection = 'AppSettings'
            Key = 'dbconnectionstr'
            Value = 'Provider=Microsoft.Jet.OLEDB.4.0;Data Source=C:\Program Files\WindowsPowerShell\DscService\Devices.mdb;'
            WebsitePath = 'IIS:\sites\PSDSCPullServer'
            DependsOn = '[xDSCWebService]PSDSCPullServer'
        }

        # Stop the default website
        xWebsite StopDefaultSite
        {
            Ensure = 'Present'
            Name = 'Default Web Site'
            State = 'Stopped'
            PhysicalPath = 'C:\inetpub\wwwroot'
            DependsOn = '[WindowsFeature]DSCServiceFeature'
        }
    }
}

$configData = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            ServerName = $ServerName
            DomainName = $DomainName
            CARootName = $CARootName
            CAServerFQDN = $CAServerFQDN
            CertSubject = $CertSubject
            AutoRenew = $true
            SMBShare = $SMBShare
            Credential = $Credential
            RebootNodeifNeeded = $true
            CertificateFile = 'c:\PullServerConfig\Cert.cer'
            Thumbprint = 'B9A39921918B466EB1ADF2509E00F5DECB2EFDA9'
            }
        )
    }

PullServer -ConfigurationData $configData -OutputPath 'C:\PullServerConfig\'
Set-DscLocalConfigurationManager -ComputerName localhost -Path 'C:\PullServerConfig\'
Start-DscConfiguration -Wait -Force -Verbose -Path 'C:\PullServerConfig\'

# .\Script.ps1 -ServerName web1 -domainname 'test.pha' -carootname 'test-dc01-ca' -caserverfqdn 'dc01.test.pha' -certsubject 'CN=service.test.pha' -smbshare '\\sofs1.test.pha\share'
```

### <a name="verify-pull-server-functionality"></a><span data-ttu-id="bdd0d-311">Lekéréses kiszolgálói funkciók ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="bdd0d-311">Verify pull server functionality</span></span>

```powershell
# This function is meant to simplify a check against a DSC pull server. If you do not use the default service URL, you will need to adjust accordingly.
function Verify-DSCPullServer ($fqdn) {
    ([xml](Invoke-WebRequest "https://$($fqdn):8080/psdscpullserver.svc" | % Content)).service.workspace.collection.href
}

Verify-DSCPullServer 'INSERT SERVER FQDN'
```

```output
Expected Result:
Action
Module
StatusReport
Node
```

### <a name="configure-clients"></a><span data-ttu-id="bdd0d-312">Ügyfelek konfigurálása</span><span class="sxs-lookup"><span data-stu-id="bdd0d-312">Configure clients</span></span>

```powershell
Configuration PullClient {
    param(
    $ID,
    $Server
    )
        LocalConfigurationManager
                {
                    ConfigurationID = $ID;
                    RefreshMode = 'PULL';
                    DownloadManagerName = 'WebDownloadManager';
                    RebootNodeIfNeeded = $true;
                    RefreshFrequencyMins = 30;
                    ConfigurationModeFrequencyMins = 15;
                    ConfigurationMode = 'ApplyAndAutoCorrect';
                    DownloadManagerCustomData = @{ServerUrl = "http://"+$Server+":8080/PSDSCPullServer.svc"; AllowUnsecureConnection = $true}
                }
}

PullClient -ID 'INSERTGUID' -Server 'INSERTSERVER' -Output 'C:\DSCConfig\'
Set-DscLocalConfigurationManager -ComputerName 'Localhost' -Path 'C:\DSCConfig\' -Verbose
```

## <a name="additional-references-snippets-and-examples"></a><span data-ttu-id="bdd0d-313">További hivatkozások kódrészletek és példák</span><span class="sxs-lookup"><span data-stu-id="bdd0d-313">Additional references, snippets, and examples</span></span>

<span data-ttu-id="bdd0d-314">Ez a példa bemutatja, hogyan manuálisan (WMF5 igényel) ügyfél kapcsolatot kezdeményez teszteléséhez.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-314">This example shows how to manually initiate a client connection (requires WMF5) for testing.</span></span>

```powershell
Update-DscConfiguration –Wait -Verbose
```

<span data-ttu-id="bdd0d-315">A [Add-DnsServerResourceRecordName](http://bit.ly/1G1H31L) parancsmag segítségével adjon hozzá egy CNAME-rekord típust a DNS-zónához.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-315">The [Add-DnsServerResourceRecordName](http://bit.ly/1G1H31L) cmdlet is used to add a type CNAME record to a DNS zone.</span></span>

<span data-ttu-id="bdd0d-316">A PowerShell-függvény, amely [ellenőrzőösszeg és DSC MOF közzététele az SMB-lekérési kiszolgálójának létrehozása](https://gallery.technet.microsoft.com/scriptcenter/PowerShell-Function-to-3bc4b7f0) automatikusan létrehozza a szükséges ellenőrzőösszeg, és ezután átmásolja az SMB-lekérési kiszolgálójának MOF-konfigurációt és ellenőrzőösszeg-fájlokat.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-316">The PowerShell Function to [Create a Checksum and Publish DSC MOF to SMB Pull Server](https://gallery.technet.microsoft.com/scriptcenter/PowerShell-Function-to-3bc4b7f0) automatically generates the required checksum, and then copies both the MOF configuration and checksum files to the SMB pull server.</span></span>

## <a name="appendix---understanding-odata-service-data-file-types"></a><span data-ttu-id="bdd0d-317">A függelék – ismertetése ODATA szolgáltatás adatainak fájltípusok</span><span class="sxs-lookup"><span data-stu-id="bdd0d-317">Appendix - Understanding ODATA service data file types</span></span>

<span data-ttu-id="bdd0d-318">Egy adatfájlt egy lekéréses kiszolgálót, amely tartalmazza az OData webszolgáltatást üzembe helyezése során az adatok létrehozásához tárolódik.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-318">A data file is stored to create information during deployment of a pull server that includes the OData web service.</span></span> <span data-ttu-id="bdd0d-319">A fájl típusa attól függ, az operációs rendszer, az alább ismertetett.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-319">The type of file depends on the operating system, as described below.</span></span>

- <span data-ttu-id="bdd0d-320">**A Windows Server 2012** a fájl típusa mindig lesz .mdb</span><span class="sxs-lookup"><span data-stu-id="bdd0d-320">**Windows Server 2012** The file type will always be   .mdb</span></span>
- <span data-ttu-id="bdd0d-321">**A Windows Server 2012 R2** a fájl típusa alapértelmezett .edb-.mdb Ha nincs megadva a konfigurációban</span><span class="sxs-lookup"><span data-stu-id="bdd0d-321">**Windows Server 2012 R2** The file type will default to .edb unless a .mdb is specified in the configuration</span></span>

<span data-ttu-id="bdd0d-322">Az a [példa parancsfájl komplex](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) egy lekéréses kiszolgálót telepíti, a is talál egy példát automatikusan kezelheti a web.config fájl beállításait, hogy bármilyen fájltípus által okozott hiba esélyét.</span><span class="sxs-lookup"><span data-stu-id="bdd0d-322">In the [Advanced example script](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) for installing a Pull Server, you will also find an example of how to automatically control the web.config file settings to prevent any chance of error caused by file type.</span></span>
