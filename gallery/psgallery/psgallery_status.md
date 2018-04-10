---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: psgallery_status
ms.openlocfilehash: 08d09ce83b5133598152186e12fc8ced90c36a88
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
<a name="powershell-gallery-status"></a><span data-ttu-id="eaa1d-103">PowerShell-galériában állapota</span><span class="sxs-lookup"><span data-stu-id="eaa1d-103">PowerShell Gallery Status</span></span>
=========================
## <a name="10102017---powershell-gallery-unavailable-for-2-hours-101017"></a><span data-ttu-id="eaa1d-104">10/10/2017-2 órán keresztül nem érhető el PowerShell-galériában 10/10/17</span><span class="sxs-lookup"><span data-stu-id="eaa1d-104">10/10/2017 - PowerShell Gallery unavailable for 2 hours 10/10/17</span></span>

<span data-ttu-id="eaa1d-105">__Összegző gyakorolt hatás__: A PowerShell-galériában észlelt egy adott időn nagyon nagy késleltetésű időszakos kapcsolattal kapcsolatos problémák, körülbelül délután 5 óra (CET) kezdődő eredményezve 10/10/17.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-105">__Summary of Impact__: The PowerShell Gallery experienced a period of very high latency, resulting in intermittent connection issues, beginning approximately 5pm (PDT) 10/10/17.</span></span> <span data-ttu-id="eaa1d-106">A probléma megoldását, miközben a hely offline állapotba kerül körülbelül 10 pm (CET) indítása 2 órán át.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-106">While resolving the issue, the site was taken offline for 2 hours starting approximately 10pm (PDT).</span></span> <span data-ttu-id="eaa1d-107">A hely lett visszaállítva hamarosan éjfél előtt 10/10/2017.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-107">The site was restored shortly before midnight 10/10/2017.</span></span>

<span data-ttu-id="eaa1d-108">__Alapvető oka__: továbbra is vizsgálni a nagy késleltetésű az okozza.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-108">__Root Cause__: The root cause of the high latency is still being investigated.</span></span>

<span data-ttu-id="eaa1d-109">__Megoldási__: A webes szolgáltatások kellett elérhetetlenné válhat, és vissza az elsődleges probléma megoldása érdekében.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-109">__Resolution__: The web services had to be taken offline and restored in order to address the primary issue.</span></span>

<span data-ttu-id="eaa1d-110">__További lépések__: az alapvető ok eredeti kiállításának ki.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-110">__Next Steps__: The root cause for the original issue is being investigated.</span></span>

## <a name="06012017---deploy-to-azure-automation-currently-unavailable"></a><span data-ttu-id="eaa1d-111">Jelenleg nem érhető el az Azure Automation 06/01/2017 - telepítése</span><span class="sxs-lookup"><span data-stu-id="eaa1d-111">06/01/2017 - Deploy to Azure Automation Currently Unavailable</span></span>

<span data-ttu-id="eaa1d-112">__Összegző gyakorolt hatás__: függőségekkel rendelkező elemek a PowerShell-galériából üzembe helyezése az Azure Automation jelenleg nem érhető el.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-112">__Summary of Impact__: Deploying items with dependencies to Azure Automation from the PowerShell Gallery is currently unavailable.</span></span>  <span data-ttu-id="eaa1d-113">A PowerShell-galériából elemek importálása belül Azure Automation nem továbbra is elérhető.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-113">Importing items from the PowerShell Gallery from inside Azure Automation is still available.</span></span>

<span data-ttu-id="eaa1d-114">__Alapvető OK__: tartalmazhat függőségeket, mások számára, és korábban már telepítették az Azure Automation elemek nem telepíti az Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-114">__Root Cause__: Items that have dependencies on others, and have been previously deployed to Azure Automation, will not be deployed to Azure Automation.</span></span> <span data-ttu-id="eaa1d-115">Mérnökök azonosította a problémát az ARM-sablonok létrehozásáról elemek függőségekkel rendelkező az Azure Automation-funkció telepítéséhez a.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-115">Engineers have identified an issue with how ARM templates are generated for items with dependencies for the Deploy to Azure Automation functionality.</span></span>

<span data-ttu-id="eaa1d-116">__Megoldási__: mérnökök arra törekednek, hogy a probléma megoldásához.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-116">__Resolution__: Engineers are working to resolve issue.</span></span>  <span data-ttu-id="eaa1d-117">Az aktuális megoldás a felhasználók számára, hogy a PowerShell-galériából importálása Azure Automation belül.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-117">The current workaround for users is to import the item from the PowerShell Gallery from inside Azure Automation.</span></span>

<span data-ttu-id="eaa1d-118">__További lépések__: mérnökök röviddel a javítás ad ki.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-118">__Next Steps__: Engineers will release the fix shortly.</span></span>  <span data-ttu-id="eaa1d-119">Addig is használja az ajánlott megoldás.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-119">In the meantime, please use the recommended workaround.</span></span>


## <a name="04112017---users-unable-to-log-in-with-azure-active-directory-aad-accounts"></a><span data-ttu-id="eaa1d-120">04/11/2017 - felhasználók nem lehet bejelentkezni az Azure Active Directory (AAD) fiókok</span><span class="sxs-lookup"><span data-stu-id="eaa1d-120">04/11/2017 - Users unable to log in with Azure Active Directory (AAD) accounts</span></span>

<span data-ttu-id="eaa1d-121">__Összegző gyakorolt hatás__: néhány felhasználó nem tud bejelentkezni a PowerShell-galériában volt az Azure AD-fiókok használatát.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-121">__Summary of Impact__: Some users were unable to log in to the PowerShell Gallery using Azure AD Accounts.</span></span>

<span data-ttu-id="eaa1d-122">__Alapvető OK__: együttműködhet biztonsága érdekében az aad-ben egy adott frissítés során egy beállítás módosításának kimaradt.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-122">__Root Cause__: During an update to interact more securely with AAD, a setting change was missed.</span></span>
<span data-ttu-id="eaa1d-123">A módosítás érvényesítéséhez végzett vizsgálat nem tartalmazza az AAD-fiókok, bizonyos típusú, a központi telepítés el.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-123">The testing done to validate the change did not include certain types of AAD accounts, so the deployment proceeded.</span></span>

<span data-ttu-id="eaa1d-124">__Megoldási__: mérnökök azonosítani a hiányzó beállítást, és javítani a hibát.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-124">__Resolution__: Engineers identified the missing setting and corrected the problem.</span></span>

<span data-ttu-id="eaa1d-125">__További lépések__: azt fogja módosítja az AAD-fiókok típusai szélesebb körű készletéhez felvenni tesztelés során.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-125">__Next Steps__: We will be modifying our testing to include a broader set of AAD account types.</span></span>

## <a name="03272017---resolved-unable-to-see-individual-module-and-script-pages"></a><span data-ttu-id="eaa1d-126">03/27/2017 - FELOLDVA: nem egyedi modul és a parancsfájl lap látható</span><span class="sxs-lookup"><span data-stu-id="eaa1d-126">03/27/2017 - RESOLVED: Unable to see individual module and script pages</span></span>

<span data-ttu-id="eaa1d-127">__Összegző gyakorolt hatás__: egyedi modul és a parancsfájl hivatkozásokat közvetlen https://www.powershellgallery.com megszakadt.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-127">__Summary of Impact__: Direct links to individual module and script pages on https://www.powershellgallery.com were broken.</span></span> <span data-ttu-id="eaa1d-128">Ez a régiók közötti történt alatt.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-128">This was being reported across all the regions.</span></span> <span data-ttu-id="eaa1d-129">Ez volt nincs hatással az PowerShellGet parancsmagokat ie., Install-modul, a telepítési parancsfájl, a frissítés-modul, frissítő parancsfájlt, Publish-modul, Publish-Scirpt továbbra is működik.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-129">This did not impact any of the PowerShellGet cmdlets ie., Install-Module, Install-Script, Update-Module, Update-Script, Publish-Module, Publish-Scirpt continued to work.</span></span>

<span data-ttu-id="eaa1d-130">__Alapvető oka__: mérnökök okát azonosítottak hibát Tulajdonságkészítő közösségi gombok Facebook hasonlóan a lapra.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-130">__Root Cause__: Engineers identified the cause as an issue bringing up social media buttons like Facebook onto the page.</span></span>

<span data-ttu-id="eaa1d-131">__Megoldási__: mérnökök megoldotta a problémát a Facebook számlálóadatok letiltásával.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-131">__Resolution__: Engineers fixed the problem by disabling the Facebook count information.</span></span>

<span data-ttu-id="eaa1d-132">__További lépések__: belső követési hibát javítsa ki a használati Facebook API megnyitni azt.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-132">__Next Steps__: We opened an internal tracking issue to fix our usage of Facebook API.</span></span>

## <a name="12152016---unable-to-send-emails-via-powershellgallery-website"></a><span data-ttu-id="eaa1d-133">12/15/2016 – nem lehet elküldeni az e-mailek PowerShellGallery webhelyen keresztül</span><span class="sxs-lookup"><span data-stu-id="eaa1d-133">12/15/2016 - Unable to send emails via PowerShellGallery website</span></span>

<span data-ttu-id="eaa1d-134">__Összegző gyakorolt hatás__: 12/13/2016 és a 12/15/2016 közötti bármely ügyfél tulajdonosok, -tulajdonosok kezelése, forduljon a támogatási szolgálathoz vagy a jelentés visszaélés küldött üzenetek nem érkezett a PowerShell-Galériabeli rendszergazdái.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-134">__Summary of Impact__: Between 12/13/2016 and 12/15/2016, any messages sent via Contact Owners, Manage Owners, Contact Support, or Report Abuse were not received by the PowerShell Gallery Administrators.</span></span>
<span data-ttu-id="eaa1d-135">__Alapvető oka__: mérnökök azonosítottak okát hitelesítési problémát az SMTP-kiszolgálóhoz.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-135">__Root Cause__: Engineers identified the cause as an authentication issue with the SMTP server.</span></span>
<span data-ttu-id="eaa1d-136">__Megoldási__: mérnökök sikerült megoldani a hitelesítési problémát, és állítsa vissza a kapcsolatot az SMTP-kiszolgálóhoz.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-136">__Resolution__: Engineers were able to resolve the authentication issue and restore connection to the SMTP server.</span></span>
<span data-ttu-id="eaa1d-137">__További lépések__: Ha az ügyfél-tulajdonosok, -tulajdonosok kezelése, forduljon a támogatási szolgálathoz vagy jelentés visszaélés hivatkozások használatával az e-mailek küldését cgadmin@microsoft.com során ez idő, és azt a még nem válaszolt, próbálja meg újból.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-137">__Next Steps__: If you used the Contact Owners, Manage Owners, Contact Support, or Report Abuse links to send mail to cgadmin@microsoft.com during this time and we have not responded, please try again.</span></span> <span data-ttu-id="eaa1d-138">Elnézést kérünk a kellemetlenségért.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-138">We apologize for the inconvenience.</span></span>



## <a name="8102016---resolved-unable-to-send-emails-to-cgadminmicrosoftcom"></a><span data-ttu-id="eaa1d-139">8/10/2016 - feloldva: nem sikerült elküldeni az e-maileket cgadmin@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="eaa1d-139">8/10/2016 - Resolved: Unable to send emails to cgadmin@microsoft.com</span></span>

<span data-ttu-id="eaa1d-140">__Összegző gyakorolt hatás__: 8/5/2016 és 8/10/2016, az ügyfelek tudtuk elküldeni az e-maileket cgadmin@microsoft.com, vagy használja a kapcsolatfelvétel a szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-140">__Summary of Impact__: Between 8/5/2016 and 8/10/2016, customers were unable to send emails to cgadmin@microsoft.com, or use the Contact Us feature.</span></span>
<span data-ttu-id="eaa1d-141">__Alapvető oka__: mérnökök okát azonosítottak az e-mail fiók módosításait.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-141">__Root Cause__: Engineers identified the cause as a configuration change of the email account.</span></span>
<span data-ttu-id="eaa1d-142">__Megoldási__: mérnökök működött a konfigurációs probléma megoldása érdekében.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-142">__Resolution__: Engineers worked to resolve the configuration issue.</span></span>
<span data-ttu-id="eaa1d-143">__További lépések__: Ha a kapcsolatfelvétel hivatkozás használt, vagy el, hogy cgadmin@microsoft.com során ez idő, és azt a még nem válaszolt, próbálja meg újból.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-143">__Next Steps__: If you used the Contact Us link or sent mail to cgadmin@microsoft.com during this time and we have not responded, please try again.</span></span> <span data-ttu-id="eaa1d-144">Köszönjük türelmét.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-144">Thank you for your patience.</span></span>



## <a name="7132016---download-items-failed"></a><span data-ttu-id="eaa1d-145">7/13/2016 - elemeket nem sikerült letölteni</span><span class="sxs-lookup"><span data-stu-id="eaa1d-145">7/13/2016 - Download Items Failed</span></span>

<span data-ttu-id="eaa1d-146">__Összegző gyakorolt hatás__: közötti 7/11/2016 és 7/13/2016, az ügyfelek egy részét észlelt elemek letöltése a PowerShell-galériából problémákat.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-146">__Summary of Impact__: Between 7/11/2016 and 7/13/2016, a subset of customers experienced issues downloading items from the PowerShell Gallery.</span></span> <span data-ttu-id="eaa1d-147">A probléma valószínűleg lemezegység jelenik meg magát a következő telepítési-modul/Install-parancsfájlt és a mentés-modul, mentés-parancsfájl által visszaadott hibaüzenet:</span><span class="sxs-lookup"><span data-stu-id="eaa1d-147">The issue likely manifested itself in the following error message returned from Install-Module/Install-Script and Save-Module/Save-Script:</span></span>

```powershell
PS C:\> Install-Module xStorage
PackageManagement\Install-Package : Package 'xStorage' failed to be installed because:
End of Central Directory record could not be found. At C:\Program
Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1375 char:21 + ...
$null = PackageManagement\Install-Package @PSBoundParameters +
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ + CategoryInfo : InvalidResult:
(xStorage:String) [Install-Package], Exception + FullyQualifiedErrorId : Package '{0}'
failed to be installed because: {1},Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage
```

<span data-ttu-id="eaa1d-148">__Előzetes alapvető OK__: mérnökök azonosított problémát az Azure Content biztosításához Network (CDN), amely 7/11/2016 telepítve van a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-148">__Preliminary root cause__: Engineers identified an issue with Azure Content Deliver Network (CDN), which was deployed to the PowerShell Gallery on 7/11/2016.</span></span>
<span data-ttu-id="eaa1d-149">__Megoldás__: mérnökök Azure CDN-t a PowerShell-galériában letiltva.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-149">__Mitigation__: Engineers disabled Azure CDN in the PowerShell Gallery.</span></span>
<span data-ttu-id="eaa1d-150">__További lépések__: alapul szolgáló alapvető okát, és a jövőbeli újraindulások valószínűségét megelőzése érdekében megoldás kifejlesztése.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-150">__Next Steps__: Investigate the underlying root cause and developing a solution to prevent future occurrences.</span></span>


## <a name="5192016---download-items-failed"></a><span data-ttu-id="eaa1d-151">5/19/2016 - elemeket nem sikerült letölteni</span><span class="sxs-lookup"><span data-stu-id="eaa1d-151">5/19/2016 - Download Items Failed</span></span>
<span data-ttu-id="eaa1d-152">__Összegző gyakorolt hatás__: közötti 5 17/2016 és 5/19/2016, az ügyfelek egy részhalmazát észlelt elemek letöltése a PowerShell-galériából problémákat.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-152">__Summary of Impact__: Between 5/17/2016 and 5/19/2016, a subset of customers experienced issues downloading items from the PowerShell Gallery.</span></span> <span data-ttu-id="eaa1d-153">A probléma valószínűleg lemezegység jelenik meg magát a következő telepítési-modul/Install-parancsfájlt és a mentés-modul, mentés-parancsfájl által visszaadott hibaüzenet:</span><span class="sxs-lookup"><span data-stu-id="eaa1d-153">The issue likely manifested itself in the following error message returned from Install-Module/Install-Script and Save-Module/Save-Script:</span></span>

```powershell
VERBOSE: Hash for package 'AzureRM.OperationalInsights' does not match hash provided from the server.
VERBOSE: InstallPackageLocal' - name='AzureRM.OperationalInsights', version='1.0.8',
destination='C:\Users\jbritt\AppData\Local\Temp\2\1741355729'
WARNING: Package 'AzureRM.OperationalInsights' failed to be installed because:
End of Central Directory record could not be found.
WARNING: Dependent Package 'AzureRM.OperationalInsights' failed to install.
WARNING: Package 'AzureRM' failed to install.
VERBOSE: Module 'AzureRM.Network' was saved successfully.
VERBOSE: Saving the dependency module 'AzureRM.NotificationHubs' with version '1.0.8' for the
module 'AzureRM'.
VERBOSE: Module 'AzureRM.NotificationHubs' was saved successfully.
PackageManagement\Save-Package : Unable to save the module 'AzureRM'. At C:\Program
Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1187 char:21 +
$null = PackageManagement\Save-Package @PSBoundParameters +
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ +
CategoryInfo : InvalidOperation: (Microsoft.Power...ets.SavePackage:SavePackage)
[Save-Package], Exception + FullyQualifiedErrorId : ProviderFailToDownloadFile,
Microsoft.PowerShell.PackageManagement.Cmdlets.SavePackage
```

<span data-ttu-id="eaa1d-154">__Előzetes alapvető OK__: mérnökök azonosítani az alapul szolgáló szolgáltató az Azure Content biztosításához Network (CDN), amely 5/17/2016 telepítve van a PowerShell-galériában kimaradás.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-154">__Preliminary root cause__: Engineers identified an outage in the underlying provider of Azure Content Deliver Network (CDN), which was deployed to the PowerShell Gallery on 5/17/2016.</span></span>
<span data-ttu-id="eaa1d-155">__Megoldás__: mérnökök Azure CDN-t a PowerShell-galériában letiltva.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-155">__Mitigation__: Engineers disabled Azure CDN in the PowerShell Gallery.</span></span>
<span data-ttu-id="eaa1d-156">__További lépések__: alapul szolgáló alapvető okát, és a jövőbeli újraindulások valószínűségét megelőzése érdekében megoldás kifejlesztése.</span><span class="sxs-lookup"><span data-stu-id="eaa1d-156">__Next Steps__: Investigate the underlying root cause and developing a solution to prevent future occurrences.</span></span>