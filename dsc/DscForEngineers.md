---
ms.date: 2017-10-13
author: eslesar;mgreenegit
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Szükségeskonfiguráció-State konfigurálása – áttekintés döntéshozók számára"
ms.openlocfilehash: 66822d9a60f98aab3d4f27d14b27ebc6ec90b2c9
ms.sourcegitcommit: 9a5da3f739b1eebb81ede58bd4fc8037bad87224
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/16/2017
---
# <a name="desired-state-configuration-overview-for-engineers"></a><span data-ttu-id="d6ac6-103">A mérnökök szükségeskonfiguráció-State konfigurálása – áttekintés</span><span class="sxs-lookup"><span data-stu-id="d6ac6-103">Desired State Configuration Overview for Engineers</span></span>

<span data-ttu-id="d6ac6-104">Ez a dokumentum célja a fejlesztői és a műveletek a csapatok tájékozódjon a PowerShell szükséges konfiguráló (DSC).</span><span class="sxs-lookup"><span data-stu-id="d6ac6-104">This document is intended for developer and operations teams to understand the benefits of PowerShell Desired State Configuration (DSC).</span></span>
<span data-ttu-id="d6ac6-105">A DSC értéke magasabb szintű nézetét biztosítja, lásd: [kívánt állapot beállítása – áttekintés döntéshozók számára](decisionMaker.md)</span><span class="sxs-lookup"><span data-stu-id="d6ac6-105">For a higher level view of the value DSC provides, please see [Desired State Configuration Overview for Decision Makers](decisionMaker.md)</span></span>

## <a name="benefits-of-desired-state-configuration"></a><span data-ttu-id="d6ac6-106">Célállapot-konfiguráció előnyei</span><span class="sxs-lookup"><span data-stu-id="d6ac6-106">Benefits of Desired State Configuration</span></span>

<span data-ttu-id="d6ac6-107">A DSC-ből van:</span><span class="sxs-lookup"><span data-stu-id="d6ac6-107">DSC exists to:</span></span>

- <span data-ttu-id="d6ac6-108">A Windows scripting összetettsége csökkentése</span><span class="sxs-lookup"><span data-stu-id="d6ac6-108">Decrease the complexity of scripting in Windows</span></span>
- <span data-ttu-id="d6ac6-109">Iteráció sebességének növelése</span><span class="sxs-lookup"><span data-stu-id="d6ac6-109">Increase the speed of iteration</span></span>

<span data-ttu-id="d6ac6-110">A "folyamatos üzembe helyezés" fogalmát egyre fontosabbá válik.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-110">The concept of "continuous deployment" is becoming more important.</span></span>
<span data-ttu-id="d6ac6-111">Folyamatos üzembe helyezés azt jelenti, hogy lehetővé teszi naponta sokszor gyakran, és eközben telepítését.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-111">Continuous deployment means the ability to deploy frequently, potentially many times per day.</span></span>
<span data-ttu-id="d6ac6-112">A következő központi telepítések célja nem javítsa ki a valami, hanem valami gyorsan közzétett beolvasása.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-112">The purpose of these deployments are not to fix something but to get something published quickly.</span></span>
<span data-ttu-id="d6ac6-113">Új szolgáltatások első működésbe fejlesztési keresztül lehető legzökkenőmentesebben és megbízhatóan, lehető, idő-az-értéket az új üzleti logika csökken.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-113">By getting new features through development into operation as smoothly and reliably as possible, you reduce time-to-value of new business logic.</span></span>

<span data-ttu-id="d6ac6-114">Az áthelyezés felhőre, magában foglalja a központi telepítési megoldás, amely használja az "deklaratív" sablon modell, ahol egy befejezési állapotot környezet deklarálva szöveg, és egy központi telepítési motor közzétett felé.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-114">The move towards cloud computing implies a deployment solution that utilizes a "declarative" template model, where an end state environment is declared as text and published to a deployment engine.</span></span>
<span data-ttu-id="d6ac6-115">Ez a telepítési módszer lehetővé teszi a gyors módosítása, a méretezés, a rugalmasság hiba fenyegetés elleni mert tetszőleges időpontban a központi telepítés is egységesen megismételhető befejezési állapota nem biztosítására.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-115">This deployment technique allows for rapid change, at scale, with resilience against threat of failure because at any time the deployment can be consistently repeated to guarantee an end state.</span></span>
<span data-ttu-id="d6ac6-116">Eszközök és szolgáltatások, amely támogatja az ilyen stílusú műveletek az automatizálás létrehozását módosítások választ.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-116">The creation of tools and services that support this style of operations through automation is a response to these changes.</span></span>

<span data-ttu-id="d6ac6-117">A DSC platform, amely biztosítja a deklaratív és idempotent (ismételhető) központi telepítés, konfigurációs és megfelelési.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-117">DSC is a platform that provides declarative and idempotent (repeatable) deployment, configuration and conformance.</span></span>
<span data-ttu-id="d6ac6-118">A DSC-platform lehetővé teszi, hogy biztosítsa, hogy az Adatközpont összetevői a helyes konfiguráció, ezzel elkerülheti a hibákat, és megakadályozza, hogy a költséges telepítési hibákat.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-118">The DSC platform enables you to ensure that the components of your data center have the correct configuration, which avoids errors and prevents costly deployment failures.</span></span>
<span data-ttu-id="d6ac6-119">A DSC-konfigurációk kezelésének alkalmazáskód részeként, DSC engedélyezi a folyamatos üzembe helyezés.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-119">By treating DSC configurations as part of application code, DSC enables continuous deployment.</span></span>
<span data-ttu-id="d6ac6-120">A DSC-konfiguráció az alkalmazást, amely biztosítja, hogy az alkalmazás telepítéséhez szükséges a Tudásbázis mindig naprakész és használatra kész részeként frissíteni kell.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-120">The DSC configuration should be updated as a part of the application, ensuring that the knowledge needed to deploy the application is always up-to-date and ready to be used.</span></span>

## <a name="i-have-powershell-why-do-i-need-desired-state-configuration"></a><span data-ttu-id="d6ac6-121">"Kell PowerShell, miért szükséges a célállapot-konfiguráció?"</span><span class="sxs-lookup"><span data-stu-id="d6ac6-121">"I have PowerShell, why do I need Desired State Configuration?"</span></span>

<span data-ttu-id="d6ac6-122">A DSC-konfigurációk külön leképezés, vagy "Mi szeretnék", a végrehajtási, vagy a "hogyan szeretnék teheti meg."</span><span class="sxs-lookup"><span data-stu-id="d6ac6-122">DSC configurations separate intent, or "what I want to do", from execution, or "how I want to do it."</span></span>
<span data-ttu-id="d6ac6-123">Ez azt jelenti, hogy az erőforrások végrehajtási logikáját tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-123">This means the logic of execution is contained within the resources.</span></span>
<span data-ttu-id="d6ac6-124">Felhasználóknak nem kell tudja, hogyan kell megvalósítani, vagy egy szolgáltatás telepítéséhez, ha az adott funkcióhoz tartozó DSC erőforrás érhető el.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-124">Users do not have to know how to implement or deploy a feature when a DSC resource for that feature is available.</span></span>
<span data-ttu-id="d6ac6-125">Ez lehetővé teszi a felhasználó számára a központi telepítés szerkezete összpontosítanak.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-125">This allows the user to focus on the structure of their deployment.</span></span>

<span data-ttu-id="d6ac6-126">Tegyük fel PowerShell-parancsfájlok kell kinéznie:</span><span class="sxs-lookup"><span data-stu-id="d6ac6-126">As an example, PowerShell scripts should look like this:</span></span>
```powershell
# Create a share in Windows Server 8
New-SmbShare -Name MyShare -Path C:\Demo\Temp -FullAccess Alice -ReadAccess Bob
```
<span data-ttu-id="d6ac6-127">Ez a parancsfájl az egyszerű, érthető és magától értetődő.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-127">This script is simple, comprehensible, and straightforward.</span></span>
<span data-ttu-id="d6ac6-128">Azonban ha kísérli meg, hogy a parancsfájl üzembe helyezésre, futtatja a több problémák.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-128">However, if you try putting that script into production, you will run into several issues.</span></span>
<span data-ttu-id="d6ac6-129">Mi történik, ha futtatott parancsfájl kétszer szerepel egy sor?</span><span class="sxs-lookup"><span data-stu-id="d6ac6-129">What happens if that script is run twice in a row?</span></span>
<span data-ttu-id="d6ac6-130">Mi történik, ha Bálint korábban teljes hozzáféréssel a megosztáshoz való?</span><span class="sxs-lookup"><span data-stu-id="d6ac6-130">What happens if Bob previously had Full Access to the share?</span></span>

<span data-ttu-id="d6ac6-131">Kiegyensúlyozása érdekében ezeket a problémákat, a parancsfájl "tényleges" verziója közelebb valahogy fog kinézni:</span><span class="sxs-lookup"><span data-stu-id="d6ac6-131">To compensate for these issues, a "real" version of the script will look closer to something like:</span></span>
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

<span data-ttu-id="d6ac6-132">Ez a parancsfájl bőven logika és hibakezelés összetettebb.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-132">This script is more complex, with plenty of logic and error handling.</span></span>
<span data-ttu-id="d6ac6-133">A parancsfájl nem összetettebb, mert, amelyek már nem figyelmezteti a felhasználókat arra mit kész, de *menete*.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-133">The script is more complex because you are no longer stating what you want done, but *how to do it*.</span></span>

<span data-ttu-id="d6ac6-134">Az alapul szolgáló logikai kiveszik számítógépnél, és DSC teszi tetszés kész.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-134">DSC allows you to say what you want done, and the underlying logic is abstracted away.</span></span>

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
          ReadAccess  = "Alice"
          FullAccess  = "Bob"
          Description = "This is an updated description for this share"
      }
   }
} 
#Run the function to compile the configuration
Sample_Share
#Pass the configuration to the nodes we defined and configure them
Start-DscConfiguration Sample_Share
```

<span data-ttu-id="d6ac6-135">Ez a parancsfájl megfelelően formázott és magától értetődő olvasási.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-135">This script is cleanly formatted and straightforward to read.</span></span>
<span data-ttu-id="d6ac6-136">A logikai elágazások és hibakezelés is jelen a [erőforrás](resources.md) végrehajtására, de a parancsfájl készítője láthatatlan.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-136">The logic paths and error handling are still present in the [resource](resources.md) implementation, but invisible to the script author.</span></span>

## <a name="separating-environment-from-structure"></a><span data-ttu-id="d6ac6-137">Elválasztó struktúra környezete</span><span class="sxs-lookup"><span data-stu-id="d6ac6-137">Separating Environment from Structure</span></span>

<span data-ttu-id="d6ac6-138">DevOps közös mintát, hogy több környezet központi telepítéshez.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-138">A common pattern in DevOps is to have multiple environments for deployment.</span></span>
<span data-ttu-id="d6ac6-139">Előfordulhat például, a "fejlesztői" környezetében gyorsan prototípus új kódot használja.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-139">For example, there might be a "dev" environment used to quickly prototype new code.</span></span>
<span data-ttu-id="d6ac6-140">A kód a "fejlesztői" környezetből kerül, a "test" környezetbe, ahol mások új működésének ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-140">The code from the "dev" environment goes into a "test" environment, where other people verify the new functionality.</span></span>
<span data-ttu-id="d6ac6-141">Végezetül a kód "termék", vagy az élő webhelyet éles környezetben állapotba kerül.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-141">Finally, the code goes into "prod", or the live site production environment.</span></span>

<span data-ttu-id="d6ac6-142">A DSC-konfigurációk megfeleljen a fejlesztői-teszt-termék folyamat használatával [konfigurációs adatok](configData.md).</span><span class="sxs-lookup"><span data-stu-id="d6ac6-142">DSC configurations accommodate this dev-test-prod pipeline through the use of [configuration data](configData.md).</span></span>
<span data-ttu-id="d6ac6-143">Ez további kivonatolja a struktúra a konfigurációját a felügyelt csomópontok közötti különbség.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-143">This further abstracts the difference between the structure of the configuration from the nodes that are managed.</span></span>
<span data-ttu-id="d6ac6-144">Például megadhatja a konfigurációkat, amelyek egy SQL server, az IIS-kiszolgáló és egy középső rétegbeli kiszolgáló szükséges.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-144">For example, you can define a configuration that requires a SQL server, an IIS server, and a middle-tier server.</span></span>
<span data-ttu-id="d6ac6-145">Függetlenül attól, milyen csomópont ebben a konfigurációban a különböző adatra kap három elemek mindig jelen lesznek.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-145">Regardless of what nodes receive the different pieces of this configuration, those three elements will always be present.</span></span>
<span data-ttu-id="d6ac6-146">Konfigurációs adatok segítségével pont összes három elem ugyanahhoz a géphez, külön, a három elemek egy tesztkörnyezetben, a három különböző gépek fejlesztői környezet felé, és végül a termék környezet mindegyik üzemi kiszolgáló felé.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-146">You can use configuration data to point all three elements towards the same machine for a dev environment, separate out the three elements to three different machines for a test environment, and finally towards all your production servers for the prod environment.</span></span>
<span data-ttu-id="d6ac6-147">A különböző környezetekben való központi telepítéséhez hívhat meg **Start-DscConfiguration** a megfelelő konfigurációs adatokkal a cél környezet.</span><span class="sxs-lookup"><span data-stu-id="d6ac6-147">To deploy to the different environments, you can invoke **Start-DscConfiguration** with the correct configuration data for the environment you want to target.</span></span>

## <a name="see-also"></a><span data-ttu-id="d6ac6-148">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d6ac6-148">See Also</span></span>

[<span data-ttu-id="d6ac6-149">Konfigurációk</span><span class="sxs-lookup"><span data-stu-id="d6ac6-149">Configurations</span></span>](configurations.md)

[<span data-ttu-id="d6ac6-150">Konfigurációs adatok</span><span class="sxs-lookup"><span data-stu-id="d6ac6-150">Configuration Data</span></span>](configData.md)

[<span data-ttu-id="d6ac6-151">Erőforrások</span><span class="sxs-lookup"><span data-stu-id="d6ac6-151">Resources</span></span>](resources.md)
