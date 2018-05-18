---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Lekérési kiszolgáló – ajánlott eljárások
ms.openlocfilehash: 1efc016df6882fa962f59dfd3e53eaa6d6b0c121
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="pull-server-best-practices"></a><span data-ttu-id="3ac6d-103">Lekérési kiszolgáló – ajánlott eljárások</span><span class="sxs-lookup"><span data-stu-id="3ac6d-103">Pull server best practices</span></span>

><span data-ttu-id="3ac6d-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="3ac6d-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ac6d-105">A lekéréses kiszolgáló (Windows-szolgáltatás *DSC-szolgáltatás*), Windows Server támogatott összetevője létezik azonban a következők: nem tervezi, hogy új funkciók és képességek kínálnak.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-105">The Pull Server (Windows Feature *DSC-Service*) is a supported component of Windows Server however there are no plans to offer new features or capabilities.</span></span> <span data-ttu-id="3ac6d-106">Javasoljuk, hogy kezdje a Váltás felügyelt ügyfelek [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (tartalmazza a Windows Server-kiszolgáló lekéréses is) vagy a közösségi megoldásoknak a valamelyikét felsorolt [Itt](pullserver.md#community-solutions-for-pull-service).</span><span class="sxs-lookup"><span data-stu-id="3ac6d-106">It is recommended to begin transitioning managed clients to [Azure Automation DSC](/azure/automation/automation-dsc-getting-started) (includes features beyond Pull Server on Windows Server) or one of the community solutions listed [here](pullserver.md#community-solutions-for-pull-service).</span></span>

<span data-ttu-id="3ac6d-107">Összefoglalás: Ez a dokumentum célja, hogy folyamata, és segít a mérnökök számára készül a megoldás bővítési tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-107">Summary: This document is intended to include process and extensibility to assist engineers who are preparing for the solution.</span></span> <span data-ttu-id="3ac6d-108">Részletek kell ajánlott eljárások nyújtása a felhasználók által meghatározott, és a termék csapatától javaslatok jövőbeli számára is elérhető, és figyelembe veendő stabil majd érvényesíteni.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-108">Details should provide best practices as identified by customers and then validated by the product team to ensure recommendations are future facing and considered stable.</span></span>

| |<span data-ttu-id="3ac6d-109">DOC adatai</span><span class="sxs-lookup"><span data-stu-id="3ac6d-109">Doc Info</span></span>|
|:---|:---|
<span data-ttu-id="3ac6d-110">Szerző</span><span class="sxs-lookup"><span data-stu-id="3ac6d-110">Author</span></span> | <span data-ttu-id="3ac6d-111">Michael Greene</span><span class="sxs-lookup"><span data-stu-id="3ac6d-111">Michael Greene</span></span>
<span data-ttu-id="3ac6d-112">Lektorok</span><span class="sxs-lookup"><span data-stu-id="3ac6d-112">Reviewers</span></span> | <span data-ttu-id="3ac6d-113">Ben Gelens, Ravikanth Chaganti Aleksandar Nikolic</span><span class="sxs-lookup"><span data-stu-id="3ac6d-113">Ben Gelens, Ravikanth Chaganti, Aleksandar Nikolic</span></span>
<span data-ttu-id="3ac6d-114">Közzétett</span><span class="sxs-lookup"><span data-stu-id="3ac6d-114">Published</span></span> | <span data-ttu-id="3ac6d-115">2015. április</span><span class="sxs-lookup"><span data-stu-id="3ac6d-115">April, 2015</span></span>

## <a name="abstract"></a><span data-ttu-id="3ac6d-116">Absztrakt</span><span class="sxs-lookup"><span data-stu-id="3ac6d-116">Abstract</span></span>

<span data-ttu-id="3ac6d-117">Jelen dokumentum célja, hogy bárki a Windows PowerShell célállapot-konfiguráció lekéréses kiszolgáló megvalósításának tervezési hivatalos útmutatást.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-117">This document is designed to provide official guidance for anyone planning for a Windows PowerShell Desired State Configuration pull server implementation.</span></span> <span data-ttu-id="3ac6d-118">A lekérési kiszolgálójával egy olyan egyszerű szolgáltatás, hajtson végre központi telepítéséhez csak perc.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-118">A pull server is a simple service that should take only minutes to deploy.</span></span> <span data-ttu-id="3ac6d-119">Bár ez a dokumentum műszaki útmutató útmutatást, amelyek a központi telepítés is használható lesz kínálnak, ez a dokumentum értéke az ajánlott eljárásokat, és milyen üzembe helyezése előtt gondolja hivatkozásként.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-119">Although this document will offer technical how-to guidance that can be used in a deployment, the value of this document is as a reference for best practices and what to think about before deploying.</span></span>
<span data-ttu-id="3ac6d-120">Olvasók kell rendelkeznie a DSC alapszintű ismeretét, és az összetevők leíró feltételeket, amelyek központi telepítésben lévő egy DSC.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-120">Readers should have basic familiarity with DSC, and the terms used to describe the components that are included in a DSC deployment.</span></span> <span data-ttu-id="3ac6d-121">További információkért lásd: a [Windows PowerShell kívánt állapot beállítása – áttekintés](https://technet.microsoft.com/library/dn249912.aspx) témakör.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-121">For more information, see the [Windows PowerShell Desired State Configuration Overview](https://technet.microsoft.com/library/dn249912.aspx)  topic.</span></span>
<span data-ttu-id="3ac6d-122">DSC elvárt azt fejleszteni a felhő ütemben történik az alapul szolgáló technológiát, beleértve a lekérési kiszolgálón is várt fejlődnek, és amelyek új lehetőségeket biztosítanak.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-122">As DSC is expected to evolve at cloud cadence, the underlying technology including pull server is also expected to evolve and to introduce new capabilities.</span></span> <span data-ttu-id="3ac6d-123">Ez a dokumentum egy verzió táblázatot, amely korábbi kiadásokban mutató hivatkozásokat és előretekintő tervek bátorítva jövőbeli kinézetű megoldások mutató hivatkozásokat biztosít a függelékben tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-123">This document includes a version table in the appendix that provides references to previous releases and references to future looking solutions to encourage forward-looking designs.</span></span>

<span data-ttu-id="3ac6d-124">A két fő szakasz ebben a dokumentumban:</span><span class="sxs-lookup"><span data-stu-id="3ac6d-124">The two major sections of this document:</span></span>

 - <span data-ttu-id="3ac6d-125">Konfiguráció tervezése</span><span class="sxs-lookup"><span data-stu-id="3ac6d-125">Configuration Planning</span></span>
 - <span data-ttu-id="3ac6d-126">A telepítési útmutató</span><span class="sxs-lookup"><span data-stu-id="3ac6d-126">Installation Guide</span></span>

### <a name="versions-of-the-windows-management-framework"></a><span data-ttu-id="3ac6d-127">Windows Management Framework verziói</span><span class="sxs-lookup"><span data-stu-id="3ac6d-127">Versions of the Windows Management Framework</span></span>
<span data-ttu-id="3ac6d-128">A jelen dokumentumban szereplő információk alkalmazása a Windows Management Framework 5.0-ra készült.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-128">The information in this document is intended to apply to Windows Management Framework 5.0.</span></span> <span data-ttu-id="3ac6d-129">WMF 5.0 nincs szükség, telepítéséhez és működtetéséhez egy lekérési kiszolgálójával, amíg a 5.0-s verziója a fókusz ezen dokumentum.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-129">While WMF 5.0 is not required for deploying and operating a pull server, version 5.0 is the focus of this document.</span></span>

### <a name="windows-powershell-desired-state-configuration"></a><span data-ttu-id="3ac6d-130">A Windows PowerShell célállapot konfiguráló</span><span class="sxs-lookup"><span data-stu-id="3ac6d-130">Windows PowerShell Desired State Configuration</span></span>
<span data-ttu-id="3ac6d-131">A keresett konfiguráló (DSC) az olyan felügyeleti platform, amely lehetővé teszi a konfigurációs adatok telepítését és kezelését ismertetik a Common Information Model (CIM) egy iparági szintaxis a Managed Object Format (MOF) nevű használatával.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-131">Desired State Configuration (DSC) is a management platform that enables deploying and managing configuration data by using an industry syntax named the Managed Object Format (MOF) to describe the Common Information Model (CIM).</span></span> <span data-ttu-id="3ac6d-132">Ezeknek a szabványoknak fejlesztésének tovább a különböző platformokon, beleértve a Linux és a hálózati hardver operációs rendszerek van nyílt forráskódú projektként, nyissa meg a Management Infrastructure (OMI).</span><span class="sxs-lookup"><span data-stu-id="3ac6d-132">An open source project, Open Management Infrastructure (OMI), exists to further development of these standards across platforms including Linux and network hardware operating systems.</span></span> <span data-ttu-id="3ac6d-133">További információkért lásd: a [MOF specifikációk csatolása DMTF lap](http://dmtf.org/standards/cim), és [OMI dokumentumokat és a forrás](https://collaboration.opengroup.org/omi/documents.php).</span><span class="sxs-lookup"><span data-stu-id="3ac6d-133">For more information, see the [DMTF page linking to MOF specifications](http://dmtf.org/standards/cim), and [OMI Documents and Source](https://collaboration.opengroup.org/omi/documents.php).</span></span>

<span data-ttu-id="3ac6d-134">A Windows PowerShell célállapot-konfiguráció, amely hozhat létre és kezelhet deklaratív konfigurációk biztosít a a nyelvi kiterjesztés-készlet.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-134">Windows PowerShell provides a set of language extensions for Desired State Configuration that you can use to create and manage declarative configurations.</span></span>

### <a name="pull-server-role"></a><span data-ttu-id="3ac6d-135">Lekéréses kiszolgálói szerepkör</span><span class="sxs-lookup"><span data-stu-id="3ac6d-135">Pull server role</span></span>
<span data-ttu-id="3ac6d-136">A lekérési kiszolgálójával hozzáférhető a célcsomópontokat konfigurációk tárolásához egy központosított szolgáltatást biztosít.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-136">A pull server provides a centralized service to store configurations that will be accessible to target nodes.</span></span>

<span data-ttu-id="3ac6d-137">A lekéréses kiszolgálói szerepkör vagy a Web Server-példányt, vagy SMB-fájlmegosztásra is telepíthető.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-137">The pull server role can be deployed as either a Web Server instance or an SMB file share.</span></span> <span data-ttu-id="3ac6d-138">A webes képesség OData illesztőfelület tartalmazza, és visszaküldi megerősítése sikeres vagy sikertelen volt, a konfiguráció alkalmazása a célcsomópontokat képességeket választhatóan is.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-138">The web server capability includes an OData interface and can optionally include capabilities for target nodes to report back confirmation of success or failure as configurations are applied.</span></span> <span data-ttu-id="3ac6d-139">Ez a funkció olyan környezetben hasznos, ahol nagyszámú célcsomópontokat.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-139">This functionality is useful in environments where there are a large number of target nodes.</span></span>
<span data-ttu-id="3ac6d-140">Egy célcsomóponttal (más néven ügyfél) konfigurálását, hogy a lekéréses kiszolgálóra mutasson a legfrissebb konfigurációt követő adatok és a szükséges parancsfájlokat vannak letöltésére és alkalmazására.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-140">After configuring a target node (also referred to as a client) to point to the pull server the latest configuration data and any required scripts are downloaded and applied.</span></span> <span data-ttu-id="3ac6d-141">Ez akkor fordulhat elő, egy egyszeri központi telepítést, vagy egy újra előforduló is lehetővé teszi a lekérési kiszolgálójával lényeges módosítása a méretezés kezelésére szolgáló feladat.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-141">This can happen as a one-time deployment or as a re-occurring job which also makes the pull server an important asset for managing change at scale.</span></span> <span data-ttu-id="3ac6d-142">További információkért lásd: [Windows PowerShell kívánt állapot konfigurációs lekéréses kiszolgálók](https://technet.microsoft.com/library/dn249913.aspx) és [leküldéses és lekéréses konfigurációs módjai](https://technet.microsoft.com/library/dn249913.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ac6d-142">For more information, see [Windows PowerShell Desired State Configuration Pull Servers](https://technet.microsoft.com/library/dn249913.aspx) and [Push and Pull Configuration Modes](https://technet.microsoft.com/library/dn249913.aspx).</span></span>

## <a name="configuration-planning"></a><span data-ttu-id="3ac6d-143">Konfiguráció tervezése</span><span class="sxs-lookup"><span data-stu-id="3ac6d-143">Configuration planning</span></span>

<span data-ttu-id="3ac6d-144">Az összes vállalati szoftver központi telepítése nincs információ előre gyűjtendő megtervezheti a megfelelő architektúra és elő kell készíteni a központi telepítés befejezéséhez szükséges lépéseket a.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-144">For any enterprise software deployment there is information that can be collected in advance to help plan for the correct architecture and to be prepared for the steps required to complete the deployment.</span></span> <span data-ttu-id="3ac6d-145">A következő szakaszokban előkészítése és a szervezeti kapcsolatok, valószínűleg létre fordulhat elő, előre kell vonatkozó információk.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-145">The following sections provide information regarding how to prepare and the organizational connections that will likely need to happen in advance.</span></span>

### <a name="software-requirements"></a><span data-ttu-id="3ac6d-146">Szoftverkövetelmények</span><span class="sxs-lookup"><span data-stu-id="3ac6d-146">Software requirements</span></span>

<span data-ttu-id="3ac6d-147">A lekéréses kiszolgáló telepítéséhez a DSC szolgáltatás a Windows Server szükséges.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-147">Deployment of a pull server requires the DSC Service feature of Windows Server.</span></span> <span data-ttu-id="3ac6d-148">Ez a funkció a Windows Server 2012-ben bevezetett, és folyamatban lévő kiadásokban Windows Management Framework (WMF) keresztül frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-148">This feature was introduced in Windows Server 2012, and has been updated through ongoing releases of Windows Management Framework (WMF).</span></span>

### <a name="software-downloads"></a><span data-ttu-id="3ac6d-149">Szoftver letöltése</span><span class="sxs-lookup"><span data-stu-id="3ac6d-149">Software downloads</span></span>

<span data-ttu-id="3ac6d-150">Telepíti a legújabb tartalom a Windows Update-ről, kívül ajánlott eljárás a DSC lekérési kiszolgálójával telepítése két letöltések: A legújabb Windows Management Framework, és a DSC-modulok lekéréses kiszolgáló kiépítés automatizálásához.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-150">In addition to installing the latest content from Windows Update, there are two downloads considered best practice to deploy a DSC pull server: The latest version of Windows Management Framework, and a DSC module to automate pull server provisioning.</span></span>

### <a name="wmf"></a><span data-ttu-id="3ac6d-151">WMF</span><span class="sxs-lookup"><span data-stu-id="3ac6d-151">WMF</span></span>

<span data-ttu-id="3ac6d-152">Windows Server 2012 R2 magában foglalja a DSC szolgáltatás nevű szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-152">Windows Server 2012 R2 includes a feature named the DSC Service.</span></span> <span data-ttu-id="3ac6d-153">A DSC szolgáltatás lekéréses kiszolgáló funkciókat, beleértve a bináris fájlok, amelyek támogatják az OData-végpont biztosítja.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-153">The DSC Service feature provides the pull server functionality, including the binaries that support the OData endpoint.</span></span>
<span data-ttu-id="3ac6d-154">WMF része a Windows Server, és egy, a Windows Server között gyors ütemben történik frissül.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-154">WMF is included in Windows Server and is updated on an agile cadence between Windows Server releases.</span></span> <span data-ttu-id="3ac6d-155">[WMF 5.0 új verzióit](http://aka.ms/wmf5latest) tartalmazhatják a DSC szolgáltatás számára.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-155">[New versions of WMF 5.0](http://aka.ms/wmf5latest)  can include updates to the DSC Service feature.</span></span> <span data-ttu-id="3ac6d-156">Ezért ajánlott letölteni a WMF legújabb kiadása, és tekintse át a kibocsátási megjegyzéseket határozza meg, ha a kiadás egy frissítést adunk ki a DSC szolgáltatás is.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-156">For this reason, it is a best practice to download the latest release of WMF and to review the release notes to determine if the release includes an update to the DSC service feature.</span></span> <span data-ttu-id="3ac6d-157">Emellett tekintse át a kibocsátási megjegyzéseket, amely jelzi, hogy a frissítés vagy forgatókönyv tervezési állapottal jelenik meg stabil vagy kísérleti szakasza.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-157">You should also review the section of the release notes that indicates whether the design status for an update or scenario is listed as stable or experimental.</span></span>
<span data-ttu-id="3ac6d-158">Szeretné engedélyezni az Agilis kiadási ciklus egyes szolgáltatások stabil deklarálható, ami azt jelenti, hogy a szolgáltatás készen áll a WMF felszabadul Preview közben is az éles környezetben használható.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-158">To allow for an agile release cycle, individual features can be declared stable, which indicates the feature is ready to be used in a production environment even while WMF is released in preview.</span></span>
<span data-ttu-id="3ac6d-159">Egyéb szolgáltatások hagyományosan frissített által WMF kiadások (lásd a további részletek a WMF kibocsátási megjegyzései):</span><span class="sxs-lookup"><span data-stu-id="3ac6d-159">Other features that have historically been updated by WMF releases (see the WMF Release Notes for further detail):</span></span>

 - <span data-ttu-id="3ac6d-160">A Windows PowerShell Windows PowerShell integrált parancsfájlkezelési</span><span class="sxs-lookup"><span data-stu-id="3ac6d-160">Windows PowerShell Windows PowerShell Integrated Scripting</span></span>
 - <span data-ttu-id="3ac6d-161">Környezet (ISE) a Windows PowerShell webszolgáltatások (felügyeleti OData</span><span class="sxs-lookup"><span data-stu-id="3ac6d-161">Environment (ISE) Windows PowerShell Web Services (Management OData</span></span>
 - <span data-ttu-id="3ac6d-162">IIS-bővítmény) a Windows PowerShell célállapot konfiguráló (DSC)</span><span class="sxs-lookup"><span data-stu-id="3ac6d-162">IIS Extension)  Windows PowerShell Desired State Configuration (DSC)</span></span>
 - <span data-ttu-id="3ac6d-163">Windows Rendszerfelügyeleti (webszolgáltatások WinRM) a Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="3ac6d-163">Windows Remote Management (WinRM) Windows Management Instrumentation (WMI)</span></span>

### <a name="dsc-resource"></a><span data-ttu-id="3ac6d-164">A DSC-erőforrás</span><span class="sxs-lookup"><span data-stu-id="3ac6d-164">DSC resource</span></span>

<span data-ttu-id="3ac6d-165">A lekéréses kiszolgálói telepítése által DSC konfigurációs parancsfájl használata a szolgáltatás kiépítését egyszerűsíthető.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-165">A pull server deployment can be simplified by provisioning the service using a DSC configuration script.</span></span> <span data-ttu-id="3ac6d-166">Ez a dokumentum tartalmaz, amelyek segítségével központi telepítése az üzemi kiszolgáló készen áll a csomópont konfigurációs parancsfájlokat.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-166">This document includes configuration scripts that can be used to deploy a production ready server node.</span></span> <span data-ttu-id="3ac6d-167">A konfigurációs parancsfájlok használatához egy DSC modulra lenne szükség, amely nem a Windows Serverben megtalálható.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-167">To use the configuration scripts, a DSC module is required that is not included in Windows Server.</span></span> <span data-ttu-id="3ac6d-168">A szükséges modulnév **xPSDesiredStateConfiguration**, mely tartalmazza a DSC-erőforrás **xDscWebService**.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-168">The required module name is **xPSDesiredStateConfiguration**, which includes the DSC resource **xDscWebService**.</span></span> <span data-ttu-id="3ac6d-169">A xPSDesiredStateConfiguration modul letölthető [Itt](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).</span><span class="sxs-lookup"><span data-stu-id="3ac6d-169">The xPSDesiredStateConfiguration module can be downloaded [here](https://gallery.technet.microsoft.com/xPSDesiredStateConfiguratio-417dc71d).</span></span>

<span data-ttu-id="3ac6d-170">Használja a **Install-modul** parancsmag a **PowerShellGet** modul.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-170">Use the **Install-Module** cmdlet from the **PowerShellGet** module.</span></span>

```powershell
Install-Module xPSDesiredStateConfiguration
```

<span data-ttu-id="3ac6d-171">A **PowerShellGet** modul modul tölti le:</span><span class="sxs-lookup"><span data-stu-id="3ac6d-171">The **PowerShellGet** module will download the module to:</span></span>

`C:\Program Files\Windows PowerShell\Modules`

<span data-ttu-id="3ac6d-172">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="3ac6d-172">Planning task</span></span>|
---|
<span data-ttu-id="3ac6d-173">Rendelkezik hozzáféréssel a telepítési fájlok a Windows Server 2012 R2 rendszerben?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-173">Do you have access to the installation files for Windows Server 2012 R2?</span></span>|
<span data-ttu-id="3ac6d-174">A telepítési környezet kell WMF és a modul letöltése az online katalógusból Internet-hozzáférés?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-174">Will the deployment environment have Internet access to download WMF and the module from the online gallery?</span></span>|
<span data-ttu-id="3ac6d-175">Hogyan telepíti az operációs rendszer telepítése után a legújabb biztonsági frissítéseket?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-175">How will you install the latest security updates after installing the operating system?</span></span>|
<span data-ttu-id="3ac6d-176">A frissítések letöltése érdekében Internet-hozzáféréssel kell a környezetben, vagy fog rendelkezni a helyi Windows Server Update Services (WSUS) kiszolgáló?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-176">Will the environment have Internet access to obtain updates, or will it have a local Windows Server Update Services (WSUS) server?</span></span>|
<span data-ttu-id="3ac6d-177">Rendelkezik hozzáféréssel, amely már tartalmazza az offline injektálási a frissítéseket a Windows Server telepítési fájlok?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-177">Do you have access to Windows Server installation files that already include updates through offline injection?</span></span>|

### <a name="hardware-requirements"></a><span data-ttu-id="3ac6d-178">Hardverkövetelmények</span><span class="sxs-lookup"><span data-stu-id="3ac6d-178">Hardware requirements</span></span>

<span data-ttu-id="3ac6d-179">Lekérési telepítések támogatottak a virtuális és fizikai kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-179">Pull server deployments are supported on both physical and virtual servers.</span></span> <span data-ttu-id="3ac6d-180">A méretezési követelmények lekérési kiszolgálójával összhangba kerüljenek a Windows Server 2012 R2 követelményei.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-180">The sizing requirements for pull server align with the requirements for Windows Server 2012 R2.</span></span>

<span data-ttu-id="3ac6d-181">CPU: 1,4 GHz-es 64 bites processzor memória: 512 MB szabad lemezterület: 32 GB-os hálózati: Gigabit Ethernet-Adapter</span><span class="sxs-lookup"><span data-stu-id="3ac6d-181">CPU: 1.4 GHz 64-bit processor Memory: 512 MB Disk Space: 32 GB Network: Gigabit Ethernet Adapter</span></span>

<span data-ttu-id="3ac6d-182">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="3ac6d-182">Planning task</span></span>|
---|
<span data-ttu-id="3ac6d-183">Telepíti a fizikai hardverek vagy olyan virtualizációs platformon?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-183">Will you deploy on physical hardware or on a virtualization platform?</span></span>|
<span data-ttu-id="3ac6d-184">Mi az a folyamatot követve kérjen a a célkörnyezet új kiszolgálót?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-184">What is the process to request a new server for your target environment?</span></span>|
<span data-ttu-id="3ac6d-185">Mi az a kiszolgáló elérhető legyen, az átlagos válaszidő?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-185">What is the average turnaround time for a server to become available?</span></span>|
<span data-ttu-id="3ac6d-186">Milyen mérete server kérés?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-186">What size server will you request?</span></span>|

### <a name="accounts"></a><span data-ttu-id="3ac6d-187">Fiókok</span><span class="sxs-lookup"><span data-stu-id="3ac6d-187">Accounts</span></span>

<span data-ttu-id="3ac6d-188">Nincsenek service fiókot egy lekéréses server-példány telepítése.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-188">There are no service account requirements to deploy a pull server instance.</span></span>
<span data-ttu-id="3ac6d-189">Vannak azonban forgatókönyvek, ahol a webhely egy helyi felhasználói fiók kontextusában futtathat.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-189">However, there are scenarios where the website could run in the context of a local user account.</span></span>
<span data-ttu-id="3ac6d-190">Például ha egy szükséges hozzáférését a storage-megosztásban webhelytartalmat és a Windows Server vagy az eszköz a storage-megosztás üzemeltetési nincsenek tartományhoz.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-190">For example, if there is a need to access a storage share for website content and either the Windows Server or the device hosting the storage share are not domain joined.</span></span>

### <a name="dns-records"></a><span data-ttu-id="3ac6d-191">DNS records</span><span class="sxs-lookup"><span data-stu-id="3ac6d-191">DNS records</span></span>

<span data-ttu-id="3ac6d-192">Szüksége lesz a kiszolgáló nevét használja, ha az ügyfelek egy lekéréses kiszolgálói környezetben használható.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-192">You will need a server name to use when configuring clients to work with a pull server environment.</span></span>
<span data-ttu-id="3ac6d-193">Tesztelési környezetben jellemzően akkor alkalmazzák a kiszolgáló állomásneve, vagy a kiszolgáló IP-címe használható, ha a DNS-név feloldása nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-193">In test environments, typically the server hostname is used, or the IP address for the server can be used if DNS name resolution is not available.</span></span>
<span data-ttu-id="3ac6d-194">Éles környezetben, amely az éles környezet jelöl laborkörnyezetben, az ajánlott eljárás akkor DNS CNAME rekordot kell létrehozni.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-194">In production environments or in a lab environment that is intended to represent a production deployment, the best practice is to create a DNS CNAME record.</span></span>

<span data-ttu-id="3ac6d-195">DNS CNAME rekord lehet hivatkozni az állomás (A) rekordot alias létrehozását teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-195">A DNS CNAME allows you to create an alias to refer to your host (A) record.</span></span>
<span data-ttu-id="3ac6d-196">A további rekordhoz célja rugalmasabb kell változás szükség lehet a jövőben.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-196">The intent of the additional name record is to increase flexibility should a change be required in the future.</span></span>
<span data-ttu-id="3ac6d-197">Egy olyan CNAME REKORDOT segít elkülöníteni az ügyfél-konfigurációt, hogy a kiszolgáló környezet, például egy lekéréses kiszolgáló cseréje vagy lekéréses további kiszolgálók hozzáadásával módosításai nem kell az ügyfél-konfigurációhoz megfelelő megváltoztatása.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-197">A CNAME can help to isolate the client configuration so that changes to the server environment, such as replacing a pull server or adding additional pull servers, will not require a corresponding change to the client configuration.</span></span>

<span data-ttu-id="3ac6d-198">A DNS-rekord nevét kiválasztásakor tartsa szem előtt a megoldás architektúrája.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-198">When choosing a name for the DNS record, keep the solution architecture in mind.</span></span>
<span data-ttu-id="3ac6d-199">Ha használatával terheléselosztás, a tanúsítvány használatával teszi biztonságossá a HTTPS-KAPCSOLATON keresztül a forgalom kell neve megegyezik a DNS-rekord.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-199">If using load balancing, the certificate used to secure traffic over HTTPS will need to share the same name as the DNS record.</span></span>

<span data-ttu-id="3ac6d-200">Forgatókönyv</span><span class="sxs-lookup"><span data-stu-id="3ac6d-200">Scenario</span></span> |<span data-ttu-id="3ac6d-201">Ajánlott eljárás</span><span class="sxs-lookup"><span data-stu-id="3ac6d-201">Best Practice</span></span>
:---|:---
<span data-ttu-id="3ac6d-202">Tesztkörnyezet</span><span class="sxs-lookup"><span data-stu-id="3ac6d-202">Test Environment</span></span> |<span data-ttu-id="3ac6d-203">Ha lehetséges Reprodukálja a tervezett éles környezetben.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-203">Reproduce the planned production environment, if possible.</span></span> <span data-ttu-id="3ac6d-204">A kiszolgáló állomásneve egyszerű konfigurációk alkalmas.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-204">A server hostname is suitable for simple configurations.</span></span> <span data-ttu-id="3ac6d-205">Ha a DNS nem érhető el, IP-címet az állomásnév helyett használható.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-205">If DNS is not available, an IP address may be used in lieu of a hostname.</span></span>|
<span data-ttu-id="3ac6d-206">Egyetlen csomópont telepítése</span><span class="sxs-lookup"><span data-stu-id="3ac6d-206">Single Node Deployment</span></span> |<span data-ttu-id="3ac6d-207">A kiszolgáló állomásneve mutató DNS CNAME rekordot kell létrehozni.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-207">Create a DNS CNAME record that points to the server hostname.</span></span>|

<span data-ttu-id="3ac6d-208">További információkért lásd: [DNS ciklikus multiplexelés konfigurálása a Windows Server](https://technet.microsoft.com/en-us/library/cc787484(v=ws.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="3ac6d-208">For more information, see [Configuring DNS Round Robin in Windows Server](https://technet.microsoft.com/en-us/library/cc787484(v=ws.10).aspx).</span></span>

<span data-ttu-id="3ac6d-209">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="3ac6d-209">Planning task</span></span>|
---|
<span data-ttu-id="3ac6d-210">Tudja Megadja annak a személynek a DNS-rekordok létrehozott és módosított?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-210">Do you know who to contact to have DNS records created and changed?</span></span>|
<span data-ttu-id="3ac6d-211">Újdonságok a DNS-rekord a kérelmek átlagos esetenként?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-211">What is the average turnaround for a request for a DNS record?</span></span>|
<span data-ttu-id="3ac6d-212">Meg kell igényelnie a kiszolgálók statikus állomásnév (A) rekordot?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-212">Do you need to request static Hostname (A) records for servers?</span></span>|
<span data-ttu-id="3ac6d-213">Mit fog kér, egy olyan CNAME REKORDOT?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-213">What will you request as a CNAME?</span></span>|
<span data-ttu-id="3ac6d-214">Ha szükséges, terheléselosztás megoldás fog használhatja a?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-214">If needed, what type of Load Balancing solution will you utilize?</span></span> <span data-ttu-id="3ac6d-215">(című terheléselosztás részletekért lásd:)</span><span class="sxs-lookup"><span data-stu-id="3ac6d-215">(see section titled Load Balancing for details)</span></span>|

### <a name="public-key-infrastructure"></a><span data-ttu-id="3ac6d-216">Nyilvános kulcsokra épülő infrastruktúra</span><span class="sxs-lookup"><span data-stu-id="3ac6d-216">Public Key Infrastructure</span></span>

<span data-ttu-id="3ac6d-217">A legtöbb szervezet ma igényelnek, hálózati forgalom, különösen az, hogy a kiszolgálók konfigurálva vannak, például bizalmas adatokat tartalmazó forgalom ellenőrizni kell, illetve átvitel során titkosítva.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-217">Most organizations today require that network traffic, especially traffic that includes such sensitive data as how servers are configured, must be validated and/or encrypted during transit.</span></span>
<span data-ttu-id="3ac6d-218">Bár a lekéréses kiszolgáló, amely elősegíti a HTTP-n keresztül telepítéséhez az ügyfélkérelmek törölje a szöveget, a HTTPS protokoll használatával biztonságos forgalom ajánlott.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-218">While it is possible to deploy a pull server using HTTP which facilitates client requests in clear text, it is a best practice to secure traffic using HTTPS.</span></span> <span data-ttu-id="3ac6d-219">A szolgáltatás beállítható úgy, hogy használja a HTTPS-kapcsolaton paraméterek a DSC-erőforrás **xPSDesiredStateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-219">The service can be configured to use HTTPS using a set of parameters in the DSC resource **xPSDesiredStateConfiguration**.</span></span>

<span data-ttu-id="3ac6d-220">A tanúsítványokkal szemben támasztott követelmények biztonságossá a HTTPS-forgalmat a lekérési kiszolgálójával nincsenek különböző, mint bármely más HTTPS webhely biztonságossá tételéhez.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-220">The certificate requirements to secure HTTPS traffic for pull server are not different than securing any other HTTPS web site.</span></span> <span data-ttu-id="3ac6d-221">A **webkiszolgáló** egy Windows Server tanúsítványszolgáltatási sablon megfelel a szükséges képességek.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-221">The **Web Server** template in a Windows Server Certificate Services satisfies the required capabilities.</span></span>

<span data-ttu-id="3ac6d-222">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="3ac6d-222">Planning task</span></span>|
---|
<span data-ttu-id="3ac6d-223">Ha tanúsítványkérelmek nem automatizált, ki kell a kérelmekre, forduljon a tanúsítványt?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-223">If certificate requests are not automated, who will you need to contact to requests a certificate?</span></span>|
<span data-ttu-id="3ac6d-224">Mi az a kérelem esetenként átlagosan?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-224">What is the average turnaround for the request?</span></span>|
<span data-ttu-id="3ac6d-225">Hogyan a Tanúsítványfájl használatával lesz áthelyezve meg?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-225">How will the certificate file be transferred to you?</span></span>|
<span data-ttu-id="3ac6d-226">Hogyan a tanúsítvány titkos kulcsa használatával lesz áthelyezve meg?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-226">How will the certificate private key be transferred to you?</span></span>|
<span data-ttu-id="3ac6d-227">Milyen hosszú legyen az alapértelmezett lejárati idő?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-227">How long is the default expiration time?</span></span>|
<span data-ttu-id="3ac6d-228">Rendelkezik elszámolása meg egy DNS-nevet az lekéréses kiszolgáló környezetben, használhatja a tanúsítvány neve?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-228">Have you settled on a DNS name for the pull server environment, that you can use for the certificate name?</span></span>|

### <a name="choosing-an-architecture"></a><span data-ttu-id="3ac6d-229">Az architektúrát kiválasztása</span><span class="sxs-lookup"><span data-stu-id="3ac6d-229">Choosing an architecture</span></span>

<span data-ttu-id="3ac6d-230">A lekérési kiszolgálójával vagy webszolgáltatás IIS vagy SMB-fájlmegosztásra is telepíthető.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-230">A pull server can be deployed using either a web service hosted on IIS, or an SMB file share.</span></span> <span data-ttu-id="3ac6d-231">A legtöbb esetben a webes szolgáltatás lehetőség nagyobb rugalmasságot biztosítja.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-231">In most situations, the web service option will provide greater flexibility.</span></span> <span data-ttu-id="3ac6d-232">Nincs ritka, hogy HTTPS-forgalom haladnak át a hálózati határok, mivel SMB-forgalom gyakran szűrt vagy letiltott hálózatok között.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-232">It is not uncommon for HTTPS traffic to traverse network boundaries, whereas SMB traffic is often filtered or blocked between networks.</span></span> <span data-ttu-id="3ac6d-233">A webszolgáltatás is biztosít, a megfelelési kiszolgáló vagy a webes Reporting Manager (mindkét figyelembe venni a jelen dokumentum egy jövőbeli verziójában témakörök), amely egy olyan mechanizmus biztosítása az ügyfelek egy kiszolgálóra a központi látható az állapot jelentése érdekében lehetősége.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-233">The web service also offers the option to include a Conformance Server or Web Reporting Manager (both topics to be addressed in a future version of this document) that provide a mechanism for clients to report status back to a server for centralized visibility.</span></span>
<span data-ttu-id="3ac6d-234">SMB környezetekben, ahol házirend szerint, hogy a webkiszolgáló nem állítható be, és más környezeti követelmények, amelyek a webkiszolgálói szerepkör nemkívánatos lehetőséget biztosít.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-234">SMB provides an option for environments where policy dictates that a web server should not be utilized, and for other environmental requirements that make a web server role undesirable.</span></span>
<span data-ttu-id="3ac6d-235">Mindkét esetben ne felejtse el az aláíráshoz és a forgalom titkosításának követelmények kiértékeléséhez.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-235">In either case, remember to evaluate the requirements for signing and encrypting traffic.</span></span> <span data-ttu-id="3ac6d-236">IPSEC-házirendek, HTTPS és SMB-aláírást érdemes fontolóra veheti, hogy minden opció.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-236">HTTPS, SMB signing, and IPSEC policies are all options worth considering.</span></span>

#### <a name="load-balancing"></a><span data-ttu-id="3ac6d-237">Terheléselosztás</span><span class="sxs-lookup"><span data-stu-id="3ac6d-237">Load balancing</span></span>
<span data-ttu-id="3ac6d-238">A webszolgáltatáshoz való interakció ügyfelek egyetlen válaszként visszaküldött adatokat kérhet.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-238">Clients interacting with the web service make a request for information that is returned in a single response.</span></span> <span data-ttu-id="3ac6d-239">Szekvenciális kérelmek nem szükségesek, így nincs szükség a terheléselosztási platform munkamenetek karbantartása bármikor egy kiszolgálón az idő biztosításához.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-239">No sequential requests are required, so it is not necessary for the load balancing platform to ensure sessions are maintained on a single server at any point in time.</span></span>

<span data-ttu-id="3ac6d-240">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="3ac6d-240">Planning task</span></span>|
---|
<span data-ttu-id="3ac6d-241">Melyik megoldás a kiszolgálók közötti terheléselosztás forgalom fog használni?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-241">What solution will be used for load balancing traffic across servers?</span></span>|
<span data-ttu-id="3ac6d-242">Ha használja a hardveres terheléselosztót, aki a kérést vegyen fel új konfigurációt az eszközön érvénybe?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-242">If using a hardware load balancer, who will take a request to add a new configuration to the device?</span></span>|
<span data-ttu-id="3ac6d-243">Mi az, hogy egy új terheléselosztási konfigurálja a kérelmek átlagos esetenként elosztott terhelésű webszolgáltatás?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-243">What is the average turnaround for a request to configure a new load balanced web service?</span></span>|
<span data-ttu-id="3ac6d-244">Milyen információkat kell a kérelem?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-244">What information will be required for the request?</span></span>|
<span data-ttu-id="3ac6d-245">Meg kell kérnie olyan további IP-címet, vagy a terheléselosztás felelős csapat kezelnek, amelyek?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-245">Will you need to request an additional IP or will the team responsible for load balancing handle that?</span></span>|
<span data-ttu-id="3ac6d-246">Rendelkezik a szükséges DNS-rekordokat, és ez szükség lesz a terheléselosztási megoldás konfigurálása felelős csapat?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-246">Do you have the DNS records needed, and will this be required by the team responsible for configuring the load balancing solution?</span></span>|
<span data-ttu-id="3ac6d-247">A betöltési terheléselosztási megoldást igényel, hogy a nyilvános kulcsokra épülő infrastruktúra elvégezhető-e az eszköz vagy is azt a terhelést HTTPS forgalmat, mindaddig, amíg nincsenek munkamenet követelmények?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-247">Does the load balancing solution require that PKI be handled by the device or can it load balance HTTPS traffic as long as there are no session requirements?</span></span>|

### <a name="staging-configurations-and-modules-on-the-pull-server"></a><span data-ttu-id="3ac6d-248">Átmeneti konfigurációk és a modulok a lekérési kiszolgálón</span><span class="sxs-lookup"><span data-stu-id="3ac6d-248">Staging configurations and modules on the pull server</span></span>

<span data-ttu-id="3ac6d-249">A konfiguráció tervezése részeként szüksége lesz gondolja, hogy melyik DSC kapcsolatos modulok és konfigurációk tárolható a lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-249">As part of configuration planning, you will need to think about which DSC modules and configurations will be hosted by the pull server.</span></span> <span data-ttu-id="3ac6d-250">Céljából konfigurációs tervezési fontos, hogy alapszinten megértse, hogyan lehet előkészíteni és telepítse központilag a tartalmakat egy lekérési kiszolgálójával.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-250">For the purpose of configuration planning it is important to have a basic understanding of how to prepare and deploy content to a pull server.</span></span>

<span data-ttu-id="3ac6d-251">A jövőben ez a szakasz kibontva lesz, és az üzemeltetési útmutatóban DSC lekéréses kiszolgáló tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-251">In the future, this section will be expanded and included in an Operations Guide for DSC Pull Server.</span></span>  <span data-ttu-id="3ac6d-252">Az útmutatóban modulok és konfigurációk kezelése az Automation szolgáltatásban, időbeli napi folyamatát ismertetik.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-252">The guide will discuss the day to day process for managing modules and configurations over time with automation.</span></span>

#### <a name="dsc-modules"></a><span data-ttu-id="3ac6d-253">A DSC-modulok</span><span class="sxs-lookup"><span data-stu-id="3ac6d-253">DSC modules</span></span>
<span data-ttu-id="3ac6d-254">Egy konfigurációs kérő ügyfelek kell a szükséges DSC-modulokat.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-254">Clients that request a configuration will need the required DSC modules.</span></span> <span data-ttu-id="3ac6d-255">A lekéréses kiszolgáló egy funkciójának automatizálhatja a DSC-modulokat az ügyfelek számára az igény szerinti terjesztési.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-255">A functionality of the pull server is to automate distribution on demand of DSC modules to clients.</span></span> <span data-ttu-id="3ac6d-256">Ha telepít egy lekérési kiszolgálójával először, lehet, hogy egy laboratóriumi vagy a koncepció igazolása, valószínűleg fog függ, például a PowerShell-galériában nyilvános adattárak vagy a DSC-modulok PowerShell.org GitHub-adattárak rendelkezésre álló DSC-modulok .</span><span class="sxs-lookup"><span data-stu-id="3ac6d-256">If you are deploying a pull server for the first time, perhaps as a lab or proof of concept, you are likely going to depend on DSC modules that are available from public repositories such as the PowerShell Gallery or the PowerShell.org GitHub repositories for DSC modules.</span></span>

<span data-ttu-id="3ac6d-257">Nagyon fontos megjegyezni, hogy még a megbízható online források, például a PowerShell-galériában, bármely modul, egy nyilvános tárházból letöltött felül kell vizsgálni valaki PowerShell élmény és a környezetben, ahol a modulok fog ismerete éles környezetben használt előtt használt.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-257">It is critical to remember that even for trusted online sources such as the PowerShell Gallery, any module that is downloaded from a public repository should be reviewed by someone with PowerShell experience and knowledge of the environment where the modules will be used prior to being used in production.</span></span> <span data-ttu-id="3ac6d-258">Ez a feladat végrehajtása közben, akkor egy időben semmilyen további hasznos a modul, például a dokumentáció és például parancsfájlok eltávolítható kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-258">While completing this task it is a good time to check for any additional payload in the module that can be removed such as documentation and example scripts.</span></span> <span data-ttu-id="3ac6d-259">Ez csökkenti a hálózati sávszélesség az első kérelem ügyfelenként, amikor modulok letölti az ügyfél-kiszolgálóról a hálózaton keresztül.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-259">This will reduce the network bandwidth per client in their first request, when modules will be downloaded over the network from server to client.</span></span>

<span data-ttu-id="3ac6d-260">Minden modul be kell csomagolni, egy meghatározott formátumban, nevű ModuleName_Version.zip, a modul forgalma tartalmazó ZIP-fájl.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-260">Each module must be packaged in a specific format, a ZIP file named ModuleName_Version.zip that contains the module payload.</span></span> <span data-ttu-id="3ac6d-261">Miután a rendszer átmásolja a fájlt a kiszolgálóra egy ellenőrzőösszeg-fájl jön létre.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-261">After the file is copied to the server a checksum file must be created.</span></span> <span data-ttu-id="3ac6d-262">Ha az ügyfelek csatlakoznak a kiszolgálóhoz, győződjön meg arról közzététele óta a DSC-modul tartalma nem módosult. az ellenőrzőösszeg szolgál.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-262">When clients connect to the server, the checksum is used to verify the content of the DSC module has not changed since it was published.</span></span>

```powershell
New-DscCheckSum -ConfigurationPath .\ -OutPath .\
```

<span data-ttu-id="3ac6d-263">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="3ac6d-263">Planning task</span></span>|
---|
<span data-ttu-id="3ac6d-264">Ha azt tervezi, a vizsgálat vagy a laboratóriumi környezet változatok kulcsával ellenőrzi?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-264">If you are planning a test or lab environment which scenarios are key to validate?</span></span>|
<span data-ttu-id="3ac6d-265">Vannak-e nyilvánosan elérhető, amelyek minden szükséges erőforrásokat tartalmazó modulok, vagy meg kell ahhoz, hogy saját erőforrásokat?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-265">Are there publicly available modules that contain resources to cover everything you need or will you need to author your own resources?</span></span>|
<span data-ttu-id="3ac6d-266">A környezet lesz nyilvános modulok beolvasása Internet-hozzáférést?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-266">Will your environment have Internet access to retrieve public modules?</span></span>|
<span data-ttu-id="3ac6d-267">Ki kell konfigurálnia a DSC-modulok áttekintése?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-267">Who will be responsible for reviewing DSC modules?</span></span>|
<span data-ttu-id="3ac6d-268">Ha azt tervezi, éles környezetben mi fog használni, a helyi tárház DSC modulok tárolása?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-268">If you are planning a production environment what will you use as a local repository for storing DSC modules?</span></span>|
<span data-ttu-id="3ac6d-269">Egy központi munkacsoport elfogadja a DSC-modulok az alkalmazásokat fejlesztő csapatoknak együtt?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-269">Will a central team accept DSC modules from application teams?</span></span> <span data-ttu-id="3ac6d-270">Mi lesz a folyamatot?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-270">What will the process be?</span></span>|
<span data-ttu-id="3ac6d-271">Csomagolására, másolása és éles használatra kész DSC modulok ellenőrzőösszeg létrehozása a kiszolgálón, a forrás tárházból fog automatizálni?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-271">Will you automate packaging, copying, and creating a checksum for production-ready DSC modules to the server, from your source repo?</span></span>|
<span data-ttu-id="3ac6d-272">A csapat felelős kezelése, valamint az automatizálási platform?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-272">Will your team be responsible for managing the automation platform as well?</span></span>|

#### <a name="dsc-configurations"></a><span data-ttu-id="3ac6d-273">A DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="3ac6d-273">DSC configurations</span></span>

<span data-ttu-id="3ac6d-274">A lekérési kiszolgálójával célja ügyfél csomópontokhoz DSC-konfigurációk kiosztása során egy olyan központi mechanizmus biztosítása.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-274">The purpose of a pull server is to provide a centralized mechanism for distributing DSC configurations to client nodes.</span></span> <span data-ttu-id="3ac6d-275">A konfigurációk MOF-dokumentumokként tárolása a kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-275">The configurations are stored on the server as MOF documents.</span></span>
<span data-ttu-id="3ac6d-276">Egyes dokumentumok egyedi GUID azonosítója lesznek elnevezve.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-276">Each document will be named with a unique GUID.</span></span> <span data-ttu-id="3ac6d-277">Ha az ügyfelek csatlakozhatnak a lekérési kiszolgálójával vannak beállítva, is számukra a globálisan egyedi Azonosítót a konfiguráció kérelmeznie kell.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-277">When clients are configured to connect with a pull server, they are also given the GUID for the configuration they should request.</span></span> <span data-ttu-id="3ac6d-278">A rendszer a konfigurációk GUID alapján hivatkozik biztosítja, hogy a globális egyediségi és rugalmas úgy, hogy egy konfiguráció alkalmazható lépésköz csomópontonként, vagy egy szerepkör-konfigurációja is sok kiszolgálók, amelyek azonos beállításokkal kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-278">This system of referencing configurations by GUID guarantees global uniqueness and is flexible such that a configuration can be applied with granularity per node, or as a role configuration that spans many servers that should have identical configurations.</span></span>

#### <a name="guids"></a><span data-ttu-id="3ac6d-279">GUID azonosítók</span><span class="sxs-lookup"><span data-stu-id="3ac6d-279">GUIDs</span></span>

<span data-ttu-id="3ac6d-280">Konfigurációs GUID tervezése ér további figyelmet egy lekéréses server központi végezni.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-280">Planning for configuration GUIDs is worth additional attention when thinking through a pull server deployment.</span></span> <span data-ttu-id="3ac6d-281">Nincs olyan GUID kezelését az adott követelmény, és a folyamat valószínű környezetben egyedinek kell lennie.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-281">There is no specific requirement for how to handle GUIDs and the process is likely to be unique for each environment.</span></span> <span data-ttu-id="3ac6d-282">A folyamat egyszerű és közötti összetett: központilag tárolt CSV-fájl, egyszerű SQL táblázat, a CMDB vagy egy másik eszközt vagy a szoftver megoldással való integráció igénylő összetett megoldás.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-282">The process can range from simple to complex: a centrally stored CSV file, a simple SQL table, a CMDB, or a complex solution requiring integration with another tool or software solution.</span></span> <span data-ttu-id="3ac6d-283">Kétféleképpen általános:</span><span class="sxs-lookup"><span data-stu-id="3ac6d-283">There are two general approaches:</span></span>

 - <span data-ttu-id="3ac6d-284">**GUID azonosítók hozzárendelése kiszolgálónként** – biztosítása, hogy minden kiszolgáló konfigurációs egyénileg szabályozott biztosítékot nyújt.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-284">**Assigning GUIDs per server** — Provides a measure of assurance that every server configuration is controlled individually.</span></span> <span data-ttu-id="3ac6d-285">Ez biztosít, a pontosság frissítések körül, és néhány kiszolgálókkal környezetekben is használhatók.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-285">This provides a level of precision around updates and can work well in environments with few servers.</span></span>
 - <span data-ttu-id="3ac6d-286">**GUID azonosítók hozzárendelése egy kiszolgálói szerepkör** – minden kiszolgálón, amely ugyanazt a funkciót, például a webkiszolgálók, ugyanaz a GUID segítségével a szükséges konfigurációs adatokra hivatkoztak.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-286">**Assigning GUIDs per server role** — All servers that perform the same function, such as web servers, use the same GUID to reference the required configuration data.</span></span>  <span data-ttu-id="3ac6d-287">Vegye figyelembe, hogy sok kiszolgálók megosztják a ugyanaz a GUID azonosítója, ha az összes kellene frissítésekor egyidejűleg a konfiguráció módosításait.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-287">Be aware that if many servers share the same GUID, all of them would be updated simultaneously when the configuration changes.</span></span>

<span data-ttu-id="3ac6d-288">A GUID-azonosító, amelyet érdemes figyelembe venni bizalmas adatokat, mert valaki rosszindulatú ahhoz, hogy a kiszolgálók telepítve és konfigurálva a környezetben az eszközintelligencia sikerült javítható.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-288">The GUID is something that should be considered sensitive data because it could be leveraged by someone with malicious intent to gain intelligence about how servers are deployed and configured in your environment.</span></span> <span data-ttu-id="3ac6d-289">További információkért lásd: [biztonságosan a PowerShell kívánt állapot konfigurációs módban lekéréses GUID azonosítók lefoglalásával](http://blogs.msdn.com/b/powershell/archive/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ac6d-289">For more information, see [Securely allocating GUIDs in PowerShell Desired State Configuration Pull Mode](http://blogs.msdn.com/b/powershell/archive/2014/12/31/securely-allocating-guids-in-powershell-desired-state-configuration-pull-mode.aspx).</span></span>

<span data-ttu-id="3ac6d-290">A tervezési feladat</span><span class="sxs-lookup"><span data-stu-id="3ac6d-290">Planning task</span></span>|
---|
<span data-ttu-id="3ac6d-291">Ki kell konfigurálnia a konfigurációk másolása a lekérési kiszolgálón mappába, amikor azok készen állnak?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-291">Who will be responsible for copying configurations in to the pull server folder when they are ready?</span></span>|
<span data-ttu-id="3ac6d-292">Ha egy alkalmazás csapat konfigurációk hoztak létre, mely a folyamat kell kiosztják azokat a?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-292">If Configurations are authored by an application team, what will the process be to hand them off?</span></span>|
<span data-ttu-id="3ac6d-293">Kihasználhatja a tárház konfigurációk tárolja az azok alatt hoztak létre, csapatok?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-293">Will you leverage a repository to store configurations as they are being authored, across teams?</span></span>|
<span data-ttu-id="3ac6d-294">Automatizálható a folyamat-konfigurációk másolása a kiszolgálóra, és ellenőrzőösszeg létrehozása, amikor azok készen állnak?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-294">Will you automate the process of copying configurations to the server and creating a checksum when they are ready?</span></span>|
<span data-ttu-id="3ac6d-295">Hogyan fogja leképez GUID kiszolgálók vagy szerepkörök, és ez tárolására szolgáló?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-295">How will you map GUIDs to servers or roles, and where will this be stored?</span></span>|
<span data-ttu-id="3ac6d-296">Mi használatával folyamatként ügyfél gépet állíthat be, és hogyan fogja azt integrálása a folyamat létrehozása és tárolása konfigurációs GUID?</span><span class="sxs-lookup"><span data-stu-id="3ac6d-296">What will you use as a process to configure client machines, and how will it integrate with your process for creating and storing Configuration GUIDs?</span></span>|

## <a name="installation-guide"></a><span data-ttu-id="3ac6d-297">A telepítési útmutató</span><span class="sxs-lookup"><span data-stu-id="3ac6d-297">Installation Guide</span></span>

<span data-ttu-id="3ac6d-298">*Ebben a dokumentumban megadott parancsfájlok példák stabil. Mindig parancsfájlok célszerű gondosan felülvizsgálni őket éles környezetben végrehajtása előtt.*</span><span class="sxs-lookup"><span data-stu-id="3ac6d-298">*Scripts given in this document are stable examples. Always review scripts carefully before executing them in a production environment.*</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3ac6d-299">Előfeltételek</span><span class="sxs-lookup"><span data-stu-id="3ac6d-299">Prerequisites</span></span>

<span data-ttu-id="3ac6d-300">Győződjön meg arról, hogy a PowerShell verzióját a kiszolgálón a következő paranccsal.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-300">To verify the version of PowerShell on your server use the following command.</span></span>

```powershell
$PSVersionTable.PSVersion
```

<span data-ttu-id="3ac6d-301">Ha lehetséges frissítsen a legújabb Windows Management Framework.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-301">If possible, upgrade to the latest version of Windows Management Framework.</span></span>
<span data-ttu-id="3ac6d-302">Ezt követően töltse le a `xPsDesiredStateConfiguration` modul a következő parancsot.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-302">Next, download the `xPsDesiredStateConfiguration` module using the following command.</span></span>


```powershell
Install-Module xPSDesiredStateConfiguration
```

<span data-ttu-id="3ac6d-303">A parancs a modul letöltése előtt jóváhagyásra fogja kérni.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-303">The command will ask for your approval before downloading the module.</span></span>

### <a name="installation-and-configuration-scripts"></a><span data-ttu-id="3ac6d-304">Telepítési és konfigurációs parancsfájlokat</span><span class="sxs-lookup"><span data-stu-id="3ac6d-304">Installation and configuration scripts</span></span>
-

<span data-ttu-id="3ac6d-305">A legjobb módszere a DSC lekérési kiszolgálójával, hogy a DSC-konfigurációs parancsprogram használja.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-305">The best method to deploy a DSC pull server is to use a DSC configuration script.</span></span> <span data-ttu-id="3ac6d-306">Ez a dokumentum bemutatja a parancsfájlok mindkét alapszintű beállításokat, amelyek csak a DSC-webszolgáltatás kell konfigurálni, és speciális kell konfigurálni a Windows Server-végpontok közötti többek között a következőket DSC webszolgáltatás beállításokat is beleértve.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-306">This document will present scripts including both basic settings that would configure only the DSC web service and advanced settings that would configure a Windows Server end-to-end including DSC web service.</span></span>

<span data-ttu-id="3ac6d-307">Megjegyzés: Jelenleg a `xPSDesiredStateConfiguation` DSC module használatához a kiszolgálónak EN-US területi beállítás.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-307">Note:  Currently the `xPSDesiredStateConfiguation` DSC module requires the server to be EN-US locale.</span></span>

### <a name="basic-configuration-for-windows-server-2012"></a><span data-ttu-id="3ac6d-308">A Windows Server 2012 alapvető konfiguráció</span><span class="sxs-lookup"><span data-stu-id="3ac6d-308">Basic configuration for Windows Server 2012</span></span>
-------------------------------------------
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

### <a name="advanced-configuration-for-windows-server-2012-r2"></a><span data-ttu-id="3ac6d-309">A Windows Server 2012 R2 rendszerben speciális konfiguráció</span><span class="sxs-lookup"><span data-stu-id="3ac6d-309">Advanced configuration for Windows Server 2012 R2</span></span>

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


### <a name="verify-pull-server-functionality"></a><span data-ttu-id="3ac6d-310">Lekéréses kiszolgálói funkciók ellenőrzése</span><span class="sxs-lookup"><span data-stu-id="3ac6d-310">Verify pull server functionality</span></span>

```powershell
# This function is meant to simplify a check against a DSC pull server. If you do not use the default service URL, you will need to adjust accordingly.
function Verify-DSCPullServer ($fqdn) {
    ([xml](invoke-webrequest "https://$($fqdn):8080/psdscpullserver.svc" | % Content)).service.workspace.collection.href
}
Verify-DSCPullServer 'INSERT SERVER FQDN'

Expected Result:
Action
Module
StatusReport
Node
```

### <a name="configure-clients"></a><span data-ttu-id="3ac6d-311">Ügyfelek konfigurálása</span><span class="sxs-lookup"><span data-stu-id="3ac6d-311">Configure clients</span></span>

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


## <a name="additional-references-snippets-and-examples"></a><span data-ttu-id="3ac6d-312">További hivatkozások kódtöredékek és példák</span><span class="sxs-lookup"><span data-stu-id="3ac6d-312">Additional references, snippets, and examples</span></span>

<span data-ttu-id="3ac6d-313">Ez a példa bemutatja, hogyan manuálisan (WMF5 igényel) ügyfél kapcsolatot kezdeményez teszteléshez.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-313">This example shows how to manually initiate a client connection (requires WMF5) for testing.</span></span>

```powershell
Update-DSCConfiguration –Wait -Verbose
```

<span data-ttu-id="3ac6d-314">A [Add-DnsServerResourceRecordName](http://bit.ly/1G1H31L) parancsmag segítségével egy típus CNAME rekord hozzáadása a DNS-zónából.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-314">The [Add-DnsServerResourceRecordName](http://bit.ly/1G1H31L) cmdlet is used to add a type CNAME record to a DNS zone.</span></span>

<span data-ttu-id="3ac6d-315">A PowerShell függvényt [hozzon létre egy ellenőrzőösszeg és DSC MOF közzététele a SMB lekérési kiszolgálójával](http://bit.ly/1E46BhI) , és automatikusan létrehozza a szükséges ellenőrzőösszeg, majd másolja az SMB-lekérési kiszolgálójával MOF-konfigurációt és ellenőrzőösszeg-fájlok.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-315">The PowerShell Function to [Create a Checksum and Publish DSC MOF to SMB Pull Server](http://bit.ly/1E46BhI) automatically generates the required checksum, and then copies both the MOF configuration and checksum files to the SMB pull server.</span></span>

## <a name="appendix---understanding-odata-service-data-file-types"></a><span data-ttu-id="3ac6d-316">Függelék – ismertetése ODATA szolgáltatás adatainak fájltípusok</span><span class="sxs-lookup"><span data-stu-id="3ac6d-316">Appendix - Understanding ODATA service data file types</span></span>

<span data-ttu-id="3ac6d-317">Egy adatfájlt létrehozása, amely tartalmazza az OData webszolgáltatást lekéréses kiszolgáló üzembe helyezése során információkat tárolja.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-317">A data file is stored to create information during deployment of a pull server that includes the OData web service.</span></span> <span data-ttu-id="3ac6d-318">A fájl típusát attól függ, az operációs rendszer az alább ismertetett.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-318">The type of file depends on the operating system, as described below.</span></span>

 - <span data-ttu-id="3ac6d-319">**Windows Server 2012** mindig lesz a fájltípus .mdb</span><span class="sxs-lookup"><span data-stu-id="3ac6d-319">**Windows Server 2012** The file type will always be   .mdb</span></span>
 - <span data-ttu-id="3ac6d-320">**Windows Server 2012 R2** a fájl típusa alapértelmezett .edb egy .mdb Ha nincs megadva a konfigurációban</span><span class="sxs-lookup"><span data-stu-id="3ac6d-320">**Windows Server 2012 R2** The file type will default to .edb unless a .mdb is specified in the configuration</span></span>

<span data-ttu-id="3ac6d-321">Az a [példa parancsfájl speciális](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) egy lekéréses kiszolgáló telepítésekor is talál arról, hogyan automatikusan vezérlőket a web.config fájl bármely fájltípus által okozott hiba esélyét megelőzése érdekében.</span><span class="sxs-lookup"><span data-stu-id="3ac6d-321">In the [Advanced example script](https://github.com/mgreenegit/Whitepapers/blob/Dev/PullServerCPIG.md#installation-and-configuration-scripts) for installing a Pull Server, you will also find an example of how to automatically control the web.config file settings to prevent any chance of error caused by file type.</span></span>