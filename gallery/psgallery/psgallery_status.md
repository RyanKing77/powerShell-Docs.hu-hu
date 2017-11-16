---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, a powershell, a parancsmag, a psgallery"
title: psgallery_status
ms.openlocfilehash: af6111d3c511273571bd978c6d0e7447726c2917
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/13/2017
---
<a name="powershell-gallery-status"></a>PowerShell-galériában állapota
=========================
## <a name="10102017---powershell-gallery-unavailable-for-2-hours-101017"></a>10/10/2017-2 órán keresztül nem érhető el PowerShell-galériában 10/10/17

__Összegző gyakorolt hatás__: A PowerShell-galériában észlelt egy adott időn nagyon nagy késleltetésű időszakos kapcsolattal kapcsolatos problémák, körülbelül délután 5 óra (CET) kezdődő eredményezve 10/10/17. A probléma megoldását, miközben a hely offline állapotba kerül körülbelül 10 pm (CET) indítása 2 órán át. A hely lett visszaállítva hamarosan éjfél előtt 10/10/2017. 
 
__Alapvető oka__: továbbra is vizsgálni a nagy késleltetésű az okozza.

__Megoldási__: A webes szolgáltatások kellett elérhetetlenné válhat, és vissza az elsődleges probléma megoldása érdekében. 

__További lépések__: az alapvető ok eredeti kiállításának ki.

## <a name="06012017---deploy-to-azure-automation-currently-unavailable"></a>Jelenleg nem érhető el az Azure Automation 06/01/2017 - telepítése

__Összegző gyakorolt hatás__: függőségekkel rendelkező elemek a PowerShell-galériából üzembe helyezése az Azure Automation jelenleg nem érhető el.  A PowerShell-galériából elemek importálása belül Azure Automation nem továbbra is elérhető.  
 
__Alapvető OK__: tartalmazhat függőségeket, mások számára, és korábban már telepítették az Azure Automation elemek nem telepíti az Azure Automation. Mérnökök azonosította a problémát az ARM-sablonok létrehozásáról elemek függőségekkel rendelkező az Azure Automation-funkció telepítéséhez a.

__Megoldási__: mérnökök arra törekednek, hogy a probléma megoldásához.  Az aktuális megoldás a felhasználók számára, hogy a PowerShell-galériából importálása Azure Automation belül. 

__További lépések__: mérnökök röviddel a javítás ad ki.  Addig is használja az ajánlott megoldás. 


## <a name="04112017---users-unable-to-log-in-with-azure-active-directory-aad-accounts"></a>04/11/2017 - felhasználók nem lehet bejelentkezni az Azure Active Directory (AAD) fiókok

__Összegző gyakorolt hatás__: néhány felhasználó nem tud bejelentkezni a PowerShell-galériában volt az Azure AD-fiókok használatát. 
 
__Alapvető OK__: együttműködhet biztonsága érdekében az aad-ben egy adott frissítés során egy beállítás módosításának kimaradt. A módosítás érvényesítéséhez végzett vizsgálat nem tartalmazza az AAD-fiókok, bizonyos típusú, a központi telepítés el.

__Megoldási__: mérnökök azonosítani a hiányzó beállítást, és javítani a hibát. 

__További lépések__: azt fogja módosítja az AAD-fiókok típusai szélesebb körű készletéhez felvenni tesztelés során.

## <a name="03272017---resolved-unable-to-see-individual-module-and-script-pages"></a>03/27/2017 - FELOLDVA: nem egyedi modul és a parancsfájl lap látható

__Összegző gyakorolt hatás__: közvetlen hivatkozások https://www.powershellgallery.com egyedi modul és a parancsfájl lapján hibás volt. Ez a régiók közötti történt alatt. Ez volt nincs hatással az PowerShellGet parancsmagokat ie., Install-modul, a telepítési parancsfájl, a frissítés-modul, frissítő parancsfájlt, Publish-modul, Publish-Scirpt továbbra is működik.

__Alapvető oka__: mérnökök okát azonosítottak hibát Tulajdonságkészítő közösségi gombok Facebook hasonlóan a lapra.  

__Megoldási__: mérnökök megoldotta a problémát a Facebook számlálóadatok letiltásával.

__További lépések__: belső követési hibát javítsa ki a használati Facebook API megnyitni azt.

## <a name="12152016---unable-to-send-emails-via-powershellgallery-website"></a>12/15/2016 – nem lehet elküldeni az e-mailek PowerShellGallery webhelyen keresztül

__Összegző gyakorolt hatás__: 12/13/2016 és a 12/15/2016 közötti bármely ügyfél tulajdonosok, -tulajdonosok kezelése, forduljon a támogatási szolgálathoz vagy a jelentés visszaélés küldött üzenetek nem érkezett a PowerShell-Galériabeli rendszergazdái.  
__Alapvető oka__: mérnökök azonosítottak okát hitelesítési problémát az SMTP-kiszolgálóhoz.  
__Megoldási__: mérnökök sikerült megoldani a hitelesítési problémát, és állítsa vissza a kapcsolatot az SMTP-kiszolgálóhoz.  
__További lépések__: Ha az ügyfél-tulajdonosok, -tulajdonosok kezelése, forduljon a támogatási szolgálathoz vagy jelentés visszaélés hivatkozások használatával az e-mailek küldését cgadmin@microsoft.com során ez idő, és azt a még nem válaszolt, próbálja meg újból. Elnézést kérünk a kellemetlenségért.  



## <a name="8102016---resolved-unable-to-send-emails-to-cgadminmicrosoftcom"></a>8/10/2016 - feloldva: nem sikerült elküldeni az e-maileketcgadmin@microsoft.com

__Összegző gyakorolt hatás__: 8/5/2016 és 8/10/2016, az ügyfelek tudtuk elküldeni az e-maileket cgadmin@microsoft.com, vagy használja a kapcsolatfelvétel a szolgáltatást.  
__Alapvető oka__: mérnökök okát azonosítottak az e-mail fiók módosításait.  
__Megoldási__: mérnökök működött a konfigurációs probléma megoldása érdekében.  
__További lépések__: Ha a kapcsolatfelvétel hivatkozás használt, vagy el, hogy cgadmin@microsoft.com során ez idő, és azt a még nem válaszolt, próbálja meg újból. Köszönjük türelmét.



## <a name="7132016---download-items-failed"></a>7/13/2016 - elemeket nem sikerült letölteni

__Összegző gyakorolt hatás__: közötti 7/11/2016 és 7/13/2016, az ügyfelek egy részét észlelt elemek letöltése a PowerShell-galériából problémákat. A probléma valószínűleg lemezegység jelenik meg magát a következő telepítési-modul/Install-parancsfájlt és a mentés-modul, mentés-parancsfájl által visszaadott hibaüzenet:

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

__Előzetes alapvető OK__: mérnökök azonosított problémát az Azure Content biztosításához Network (CDN), amely 7/11/2016 telepítve van a PowerShell-galériában.  
__Megoldás__: mérnökök Azure CDN-t a PowerShell-galériában letiltva.  
__További lépések__: alapul szolgáló alapvető okát, és a jövőbeli újraindulások valószínűségét megelőzése érdekében megoldás kifejlesztése.


## <a name="5192016---download-items-failed"></a>5/19/2016 - elemeket nem sikerült letölteni
__Összegző gyakorolt hatás__: közötti 5 17/2016 és 5/19/2016, az ügyfelek egy részhalmazát észlelt elemek letöltése a PowerShell-galériából problémákat. A probléma valószínűleg lemezegység jelenik meg magát a következő telepítési-modul/Install-parancsfájlt és a mentés-modul, mentés-parancsfájl által visszaadott hibaüzenet:

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

__Előzetes alapvető OK__: mérnökök azonosítani az alapul szolgáló szolgáltató az Azure Content biztosításához Network (CDN), amely 5/17/2016 telepítve van a PowerShell-galériában kimaradás.  
__Megoldás__: mérnökök Azure CDN-t a PowerShell-galériában letiltva.  
__További lépések__: alapul szolgáló alapvető okát, és a jövőbeli újraindulások valószínűségét megelőzése érdekében megoldás kifejlesztése.

