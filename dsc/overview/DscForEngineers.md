---
ms.date: 10/13/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A célállapot-konfiguráció áttekintése mérnökök számára
ms.openlocfilehash: 0e599c2218cd2df29dbd0529006be5e1ef17ce5f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62079982"
---
# <a name="desired-state-configuration-overview-for-engineers"></a><span data-ttu-id="ec887-103">A célállapot-konfiguráció áttekintése mérnökök számára</span><span class="sxs-lookup"><span data-stu-id="ec887-103">Desired State Configuration Overview for Engineers</span></span>

<span data-ttu-id="ec887-104">Ez a dokumentum célja fejlesztői és műveleti csapatok, hogy tájékozódjon a PowerShell Desired State Configuration (DSC).</span><span class="sxs-lookup"><span data-stu-id="ec887-104">This document is intended for developer and operations teams to understand the benefits of PowerShell Desired State Configuration (DSC).</span></span>
<span data-ttu-id="ec887-105">A DSC értéke magasabb szintű nézetét biztosítja, lásd: [Desired State Configuration áttekintése döntéshozók számára](decisionMaker.md)</span><span class="sxs-lookup"><span data-stu-id="ec887-105">For a higher level view of the value DSC provides, please see [Desired State Configuration Overview for Decision Makers](decisionMaker.md)</span></span>

## <a name="benefits-of-desired-state-configuration"></a><span data-ttu-id="ec887-106">Desired State Configuration előnyei</span><span class="sxs-lookup"><span data-stu-id="ec887-106">Benefits of Desired State Configuration</span></span>

<span data-ttu-id="ec887-107">DSC létezik:</span><span class="sxs-lookup"><span data-stu-id="ec887-107">DSC exists to:</span></span>

- <span data-ttu-id="ec887-108">Parancsprogramok használata a Windows a összetettségének csökkentése</span><span class="sxs-lookup"><span data-stu-id="ec887-108">Decrease the complexity of scripting in Windows</span></span>
- <span data-ttu-id="ec887-109">Ismétlés sebességének növelése</span><span class="sxs-lookup"><span data-stu-id="ec887-109">Increase the speed of iteration</span></span>

<span data-ttu-id="ec887-110">"Folyamatos üzembe helyezés" fogalma egyre fontosabbá válik.</span><span class="sxs-lookup"><span data-stu-id="ec887-110">The concept of "continuous deployment" is becoming more important.</span></span>
<span data-ttu-id="ec887-111">Folyamatos üzembe helyezés helyezheti üzembe az alkalmazásokat gyakran, esetleg naponta többször jelenti.</span><span class="sxs-lookup"><span data-stu-id="ec887-111">Continuous deployment means the ability to deploy frequently, potentially many times per day.</span></span>
<span data-ttu-id="ec887-112">Ezeket az üzemelő példányokat célját olyan nem hibajavítási, de valami gyorsan beolvasása.</span><span class="sxs-lookup"><span data-stu-id="ec887-112">The purpose of these deployments are not to fix something but to get something published quickly.</span></span>
<span data-ttu-id="ec887-113">Új funkciók első keresztül fejlesztést, a művelet legzökkenőmentesebben és megbízhatóan, amennyire csak lehetséges, csökkenti a idő teremthet értéket az új üzleti logikát.</span><span class="sxs-lookup"><span data-stu-id="ec887-113">By getting new features through development into operation as smoothly and reliably as possible, you reduce time-to-value of new business logic.</span></span>

<span data-ttu-id="ec887-114">Az áthelyezés a felhő-számítástechnika azt jelenti, egy központi telepítési megoldás, amely már használja egy "deklaratív" sablon modell, ahol befejezési állapota környezet deklarálva szöveget, és egy üzembe helyezési motorban közzétett felé.</span><span class="sxs-lookup"><span data-stu-id="ec887-114">The move towards cloud computing implies a deployment solution that utilizes a "declarative" template model, where an end state environment is declared as text and published to a deployment engine.</span></span>
<span data-ttu-id="ec887-115">Ez a telepítési módszer lehetővé teszi, hogy gyors változások, ipari méretekben, és meghibásodási fenyegetés elleni ezzel járó rugalmasságot mivel bármikor az üzemelő példány folyamatosan megismételhető biztosításához egy befejezési állapotot.</span><span class="sxs-lookup"><span data-stu-id="ec887-115">This deployment technique allows for rapid change, at scale, with resilience against threat of failure because at any time the deployment can be consistently repeated to guarantee an end state.</span></span>
<span data-ttu-id="ec887-116">Eszközöket és szolgáltatásokat, amelyek támogatják ezt az automatizálás operations stílusát létrehozása adott válasz ezeket a módosításokat.</span><span class="sxs-lookup"><span data-stu-id="ec887-116">The creation of tools and services that support this style of operations through automation is a response to these changes.</span></span>

<span data-ttu-id="ec887-117">DSC platform, amely biztosítja a deklaratív és idempotens (megismételhető) telepítési, konfigurációs és irányítópultja.</span><span class="sxs-lookup"><span data-stu-id="ec887-117">DSC is a platform that provides declarative and idempotent (repeatable) deployment, configuration and conformance.</span></span>
<span data-ttu-id="ec887-118">A DSC-platform segítségével győződjön meg arról, hogy az Adatközpont alkotóelemei rendelkezik-e a megfelelő konfigurációt, mivel ezzel elkerülheti a hibákat, és megakadályozza a költséges telepítési hibákat.</span><span class="sxs-lookup"><span data-stu-id="ec887-118">The DSC platform enables you to ensure that the components of your data center have the correct configuration, which avoids errors and prevents costly deployment failures.</span></span>
<span data-ttu-id="ec887-119">DSC-konfigurációk kezelésére az alkalmazás kódjának részeként, DSC folyamatos üzembe helyezés lehetővé teszi.</span><span class="sxs-lookup"><span data-stu-id="ec887-119">By treating DSC configurations as part of application code, DSC enables continuous deployment.</span></span>
<span data-ttu-id="ec887-120">A DSC-konfiguráció az alkalmazást, amely biztosítja, hogy a ismereteket szerezhet az alkalmazás központi telepítése mindig naprakész, és készen áll a használatra részeként kell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="ec887-120">The DSC configuration should be updated as a part of the application, ensuring that the knowledge needed to deploy the application is always up-to-date and ready to be used.</span></span>

## <a name="i-have-powershell-why-do-i-need-desired-state-configuration"></a><span data-ttu-id="ec887-121">"PowerShell-lel, miért szükséges a Desired State Configuration van szükségem?"</span><span class="sxs-lookup"><span data-stu-id="ec887-121">"I have PowerShell, why do I need Desired State Configuration?"</span></span>

<span data-ttu-id="ec887-122">DSC-konfigurációk külön szándékot, vagy a "mit szeretne ehhez", a végrehajtási, vagy a "hogyan szeretnék működtet."</span><span class="sxs-lookup"><span data-stu-id="ec887-122">DSC configurations separate intent, or "what I want to do", from execution, or "how I want to do it."</span></span>
<span data-ttu-id="ec887-123">Ez azt jelenti, hogy az erőforrások végrehajtási logikájának tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="ec887-123">This means the logic of execution is contained within the resources.</span></span>
<span data-ttu-id="ec887-124">Útmutató megvalósítása vagy üzembe helyezése egy funkció, ha egy adott szolgáltatáshoz tartozó DSC erőforrás érhető el a felhasználók nem rendelkeznek.</span><span class="sxs-lookup"><span data-stu-id="ec887-124">Users do not have to know how to implement or deploy a feature when a DSC resource for that feature is available.</span></span>
<span data-ttu-id="ec887-125">Ez lehetővé teszi a felhasználó számára a központi telepítés összpontosítanak.</span><span class="sxs-lookup"><span data-stu-id="ec887-125">This allows the user to focus on the structure of their deployment.</span></span>

<span data-ttu-id="ec887-126">Tegyük fel PowerShell-parancsfájlokat kell kinéznie:</span><span class="sxs-lookup"><span data-stu-id="ec887-126">As an example, PowerShell scripts should look like this:</span></span>
```powershell
# Create a share in Windows Server 8
New-SmbShare -Name MyShare -Path C:\Demo\Temp -FullAccess Alice -ReadAccess Bob
```
<span data-ttu-id="ec887-127">Ez a szkript akkor egyszerű, érthető és könnyen érthető megjegyzésblokkok írására.</span><span class="sxs-lookup"><span data-stu-id="ec887-127">This script is simple, comprehensible, and straightforward.</span></span>
<span data-ttu-id="ec887-128">Azonban ha a szkript üzembe helyezése éles környezetben, fog futtatni több problémákat.</span><span class="sxs-lookup"><span data-stu-id="ec887-128">However, if you try putting that script into production, you will run into several issues.</span></span>
<span data-ttu-id="ec887-129">Mi történik, amely kétszer egy sort a szkript futása?</span><span class="sxs-lookup"><span data-stu-id="ec887-129">What happens if that script is run twice in a row?</span></span>
<span data-ttu-id="ec887-130">Mi történik, ha Bob korábban hozzáférhettek a megosztást?</span><span class="sxs-lookup"><span data-stu-id="ec887-130">What happens if Bob previously had Full Access to the share?</span></span>

<span data-ttu-id="ec887-131">A meghiúsult lépések kompenzációjához ezeket a problémákat, a parancsfájl egy "valódi" verzióját közelebb a következőhöz hasonlóan fog kinézni:</span><span class="sxs-lookup"><span data-stu-id="ec887-131">To compensate for these issues, a "real" version of the script will look closer to something like:</span></span>
```powershell
# But actually creating a share in an idempotent way would be

$shareExists = $false
$smbShare = Get-SmbShare -Name $Name -ErrorAction SilentlyContinue
if($smbShare -ne $null)
{
    Write-Verbose -Message "Share with name $Name exists"
    $shareExists = $true
}

if ($shareExists -eq $false)
{
    Write-Verbose "Creating share $Name to ensure it is Present"
    New-SmbShare @psboundparameters
}
else
{
    # Need to call either Set-SmbShare or *ShareAccess cmdlets
    if ($psboundparameters.ContainsKey("ChangeAccess"))
    {
       #...etc, etc, etc
    }
}
```

<span data-ttu-id="ec887-132">Ez a szkript akkor bőven logikai és a hibakezelés összetettebb.</span><span class="sxs-lookup"><span data-stu-id="ec887-132">This script is more complex, with plenty of logic and error handling.</span></span>
<span data-ttu-id="ec887-133">A parancsfájl összetettebb, mert meg van már nem figyelmezteti a szándékainak kész, de *menete*.</span><span class="sxs-lookup"><span data-stu-id="ec887-133">The script is more complex because you are no longer stating what you want done, but *how to do it*.</span></span>

<span data-ttu-id="ec887-134">DSC lehetővé teszi, hogy tegyük fel, hogy mit szeretne kész, és az alapul szolgáló logikai azonnal emeli ki.</span><span class="sxs-lookup"><span data-stu-id="ec887-134">DSC allows you to say what you want done, and the underlying logic is abstracted away.</span></span>

```powershell
# A configuration is a special kind of PowerShell function
Configuration Sample_Share
{
   Import-DscResource -Module xSmbShare
   # Nodes are the endpoint we wish to configure
   # A Configuration block can have zero or more Node blocks
   Node $NodeName
   {
      # Next, specify one or more resource blocks
      # Resources are simply PowerShell modules that
      # implement the logic of "how" to execute a task
      xSmbShare MySMBShare
      {
          Ensure      = "Present"
          Name        = "MyShare"
          Path        = "C:\Demo\Temp"
          ReadAccess  = "Bob"
          FullAccess  = "Alice"
          Description = "This is an updated description for this share"
      }
   }
}
#Run the function to compile the configuration
Sample_Share
#Pass the configuration to the nodes we defined and configure them
Start-DscConfiguration Sample_Share
```

<span data-ttu-id="ec887-135">Ez a szkript akkor tisztán formázott és könnyen érthető megjegyzésblokkok írására olvasni.</span><span class="sxs-lookup"><span data-stu-id="ec887-135">This script is cleanly formatted and straightforward to read.</span></span>
<span data-ttu-id="ec887-136">A logikai elérési utak és a hibakezelés is jelen a [erőforrás](../resources/resources.md) végrehajtására, de a parancsfájlt a szerzője, láthatatlan.</span><span class="sxs-lookup"><span data-stu-id="ec887-136">The logic paths and error handling are still present in the [resource](../resources/resources.md) implementation, but invisible to the script author.</span></span>

## <a name="separating-environment-from-structure"></a><span data-ttu-id="ec887-137">Struktúra környezetben szétválasztása</span><span class="sxs-lookup"><span data-stu-id="ec887-137">Separating Environment from Structure</span></span>

<span data-ttu-id="ec887-138">A fejlesztési és üzemeltetési egyik központi telepítés több környezetet.</span><span class="sxs-lookup"><span data-stu-id="ec887-138">A common pattern in DevOps is to have multiple environments for deployment.</span></span>
<span data-ttu-id="ec887-139">Előfordulhat például, a "fejlesztés" környezet segítségével gyorsan prototípus új kódot.</span><span class="sxs-lookup"><span data-stu-id="ec887-139">For example, there might be a "dev" environment used to quickly prototype new code.</span></span>
<span data-ttu-id="ec887-140">A kód a "fejlesztés" környezetből kerül egy "teszt" környezetben, ahol mások ellenőrizze-e az új funkciókat.</span><span class="sxs-lookup"><span data-stu-id="ec887-140">The code from the "dev" environment goes into a "test" environment, where other people verify the new functionality.</span></span>
<span data-ttu-id="ec887-141">Végül a kód az "éles", vagy az élő webhelyet éles környezetbe kerül.</span><span class="sxs-lookup"><span data-stu-id="ec887-141">Finally, the code goes into "prod", or the live site production environment.</span></span>

<span data-ttu-id="ec887-142">DSC-konfigurációk megfeleljen a dev-test-éles folyamat használatával [konfigurációs adatok](../configurations/configData.md).</span><span class="sxs-lookup"><span data-stu-id="ec887-142">DSC configurations accommodate this dev-test-prod pipeline through the use of [configuration data](../configurations/configData.md).</span></span>
<span data-ttu-id="ec887-143">Ez további kivonatolja a struktúra a konfiguráció a kezelt csomópontok közötti különbség.</span><span class="sxs-lookup"><span data-stu-id="ec887-143">This further abstracts the difference between the structure of the configuration from the nodes that are managed.</span></span>
<span data-ttu-id="ec887-144">Például megadhat egy-egy SQL server, az IIS-kiszolgáló és egy középső rétegbeli kiszolgáló szükséges konfigurációját.</span><span class="sxs-lookup"><span data-stu-id="ec887-144">For example, you can define a configuration that requires a SQL server, an IIS server, and a middle-tier server.</span></span>
<span data-ttu-id="ec887-145">Függetlenül attól, hogy milyen csomópontok a konfiguráció a különböző darabok kapja ezek három elem mindig lesz található.</span><span class="sxs-lookup"><span data-stu-id="ec887-145">Regardless of what nodes receive the different pieces of this configuration, those three elements will always be present.</span></span>
<span data-ttu-id="ec887-146">Konfigurációs adatok segítségével pont felé ugyanarra a gépre a tesztkörnyezetben, három különböző gépek ki a három elem külön fejlesztési környezetre vonatkozó összes három elemet, és végül az éles környezet összes az éles kiszolgálók felé.</span><span class="sxs-lookup"><span data-stu-id="ec887-146">You can use configuration data to point all three elements towards the same machine for a dev environment, separate out the three elements to three different machines for a test environment, and finally towards all your production servers for the prod environment.</span></span>
<span data-ttu-id="ec887-147">A különböző környezetekben való üzembe helyezéséhez hívhat **Start-DscConfiguration** -célozni kívánt környezetre a megfelelő konfigurációs adatokat.</span><span class="sxs-lookup"><span data-stu-id="ec887-147">To deploy to the different environments, you can invoke **Start-DscConfiguration** with the correct configuration data for the environment you want to target.</span></span>

## <a name="see-also"></a><span data-ttu-id="ec887-148">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ec887-148">See Also</span></span>

[<span data-ttu-id="ec887-149">Konfigurációk</span><span class="sxs-lookup"><span data-stu-id="ec887-149">Configurations</span></span>](../configurations/configurations.md)

[<span data-ttu-id="ec887-150">Konfigurációs adatok</span><span class="sxs-lookup"><span data-stu-id="ec887-150">Configuration Data</span></span>](../configurations/configData.md)

[<span data-ttu-id="ec887-151">Erőforrások</span><span class="sxs-lookup"><span data-stu-id="ec887-151">Resources</span></span>](../resources/resources.md)
