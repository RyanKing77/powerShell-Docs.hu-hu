---
description: További információ az Azure-ban a Desired State Configuration (DSC) bővítmény a korábbi verziók.
ms.date: 06/21/2018
keywords: dsc, powershell, azure, extension
title: Az Azure DSC-bővítmény a korábbi verziók
ms.openlocfilehash: 6d821e53e9206d99425e8c83f6d90986c7c28b63
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734664"
---
# <a name="azure-desired-state-configuration-extension-version-history"></a>Azure Desired State Configuration bővítmény korábbi verziók

Az Azure Desired State Configuration (DSC) Virtuálisgép-bővítmény frissül, igény szerint fejlesztéseket és új képességek érhetők el az Azure, a Windows Server és a Windows Management Framework (WMF), amely tartalmazza a Windows PowerShell támogatása.

Ez a cikk az Azure DSC Virtuálisgép-bővítmény, az egyes verziójával kapcsolatos információkkal szolgálnak a milyen környezetek azt támogatja, és a megjegyzések, és új funkciók és módosítások megjegyzések.

## <a name="latest-version"></a>Legújabb verziója

### <a name="version-276"></a>Verzió 2.76

- **Kiadás dátuma:**
  - 2018. május 9,. (Azure) |} 21 2018 június (az Azure China, az Azure Government)
- **Operációsrendszer-támogatást:**
  - Windows Server 2016
  - Windows Server 2012 R2
  - Windows Server 2012
  - Windows Server 2008 R2 SP1
  - Windows ügyfél 7/8.1/10
  - Nano Server
- **A WMF-támogatás:**
  - WMF 5.1
  - A WMF 5.0 RTM
  - WMF 4.0 Update
  - WMF 4.0
- **Környezet:**
  - Azure
  - Azure China
  - Azure Government
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális gépen.
- **Új funkciók:**
  - A bővítmény-metaadatok substatus és további kisebb hibajavítások továbbfejlesztése.

## <a name="supported-versions"></a>Támogatott verziók

> [!WARNING]
> Verziók 2.4 2.13 keresztül használja a WMF 5.0-s nyilvános előzetes amelyek aláíró tanúsítványa lejárt, a 2016. augusztus.  A problémával kapcsolatos további információkért lásd: [blogbejegyzés](https://blogs.msdn.microsoft.com/powershell/2016/05/24/azure-dsc-extension-versions-2-4-up-to-2-13-will-retire-in-august/).

### <a name="version-275"></a>Verzió 2,75

- **Kiadás dátuma:** 2018. március 5.
- **Operációsrendszer-támogatást:** A Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows-ügyfél 7/8.1/10, a Nano Server
- **A WMF-támogatás:** A WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális gépen.
- **Új funkciók:**
  - A GitHub legutóbbi, hogy áttért a TLS 1.2-es után nem lehet előkészíteni egy virtuális Gépet az Azure Automation DSC az Azure piactéren elérhető házi KÉSZÍTÉSŰ Resource Manager-sablonok használatával, vagy DSC-bővítmény használatával bármely konfigurációs Githubon található. A bővítmény telepítése során az alábbihoz hasonló hibaüzenetet jelenik meg:

    ```json
    {
        "code": "DeploymentFailed",
        "message": "At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/arm-debug for usage details.",
        "details": [{
            "code": "Conflict",
            "message": "{
                \"status\": \"Failed\",
                \"error\": {
                    \"code\": \"ResourceDeploymentFailure\",
                    \"message\": \"The resource operation completed with terminal provisioning state 'Failed'.\",
                    \"details\": [ {
                        \"code\": \"VMExtensionProvisioningError\",
                        \"message\": \"VM has reported a failure when processing extension 'Microsoft.Powershell.DSC'.
                        Error message: \\\"The DSC Extension failed to execute: Error downloading
                        https://github.com/Azure/azure-quickstart-templates/raw/master/dsc-extension-azure-automation-pullserver/UpdateLCMforAAPull.zip
                        after 29 attempts: The request was aborted: Could not create SSL/TLS secure channel..\\nMore information about the failure can
                        be found in the logs located under 'C:\\\\WindowsAzure\\\\Logs\\\\Plugins\\\\Microsoft.Powershell.DSC\\\\2.74.0.0' on the VM.\\\".\"
                    } ]
                }
            }"
        }]
    }
    ```

  - A bővítmény új verziója, a TLS 1.2 kényszerítése megtörtént. Üzembe helyezése a bővítményt, ha már használta az AutoUpgradeMinorVersion során = TRUE értékre a Resource Manager-sablonja, akkor a bővítményt a 2,75 autoupgraded fog kapni. Manuális frissítések, adja meg a `TypeHandlerVersion = 2.75` a Resource Manager-sablonban.

### <a name="version-270---272"></a>Verzió 2.70-2.72

- **Kiadás dátuma:** 2017. november 13.
- **Operációsrendszer-támogatást:** A Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows-ügyfél 7/8.1/10, a Nano Server
- **A WMF-támogatás:** A WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális gépen.
- **Új funkciók:**
  - Hiba a javításokat és javítását, amely leegyszerűsíti az Azure Automation DSC a felhasználói felület a portálon, valamint a Resource Manager-sablon használatával.  További információkért lásd: [alapértelmezett konfigurációs parancsfájl](/azure/virtual-machines/extensions/dsc-overview) a DSC-bővítmény dokumentációjában.

### <a name="version-226"></a>Verzió 2.26 pontban

- **Kiadás dátuma:** 2017. június 9-es.
- **Operációsrendszer-támogatást:** A Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows-ügyfél 7/8.1/10, a Nano Server
- **A WMF-támogatás:** A WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális gépen.
- **Új funkciók:**
  - Telemetria fejlesztései.

### <a name="version-225"></a>Verzió 2.25

- **Kiadás dátuma:** 2017. június 2.
- **Operációsrendszer-támogatást:** A Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows-ügyfél 7/8.1/10, a Nano Server
- **A WMF-támogatás:** A WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális gépen.
- **Új funkciók:**
  - Számos hibajavítást és egyéb kisebb fejlesztések lettek hozzáadva.

### <a name="version-224"></a>Verzió 2.24

- **Kiadás dátuma:** 2017. április 13.
- **Operációsrendszer-támogatást:** Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **A WMF-támogatás:** A WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális gépen.
- **Új funkciók:**
  - Virtuális gép UUID azonosítója és a DSC-ügynök azonosítója bővítmény-metaadatok mutatja. Más kisebb fejlesztések lettek hozzáadva.

### <a name="version-223"></a>Verzió 2.23

- **Kiadás dátuma:** 2017. március 15.
- **Operációsrendszer-támogatást:** Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **A WMF-támogatás:** A WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális gépen.
- **Új funkciók:**
  - Számos hibajavítás és egyéb fejlesztések lettek hozzáadva.

### <a name="version-222"></a>Verzió 2.22

- **Kiadás dátuma:** 2017. február 8.
- **Operációsrendszer-támogatást:** Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **A WMF-támogatás:** A WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális gépen.
- **Új funkciók:**
  - A DSC-bővítmény most már támogatják a WMF 5.1 támogatása.
  - Kisebb egyéb fejlesztések lettek hozzáadva.

### <a name="version-221"></a>Verzió 2.21

- **Kiadás dátuma:** 2016. december 2
- **Operációsrendszer-támogatást:** Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **A WMF-támogatás:** A WMF 5.1-es előzetes verzió, a WMF 5.0 RTM-re, a WMF 4.0-s verzióját frissíti, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális gépen.
- **Új funkciók:**
  - A DSC-bővítmény már elérhető a Nano Serveren. Ez a verzió elsősorban a bővítményt futtató Nano Serveren a kód módosításait tartalmazza.
  - Kisebb egyéb fejlesztések lettek hozzáadva.

### <a name="version-220"></a>Verzió 2.20.

- **Kiadás dátuma:** 2016. augusztus 2.
- **Operációsrendszer-támogatást:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **A WMF-támogatás:** A WMF 5.1-es előzetes verzió, a WMF 5.0 RTM-re, a WMF 4.0-s verzióját frissíti, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016 Technical Preview; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - Támogatják a WMF 5.1-es előzetes verzió. Az első közzététel, amikor ez a verzió lett-e a nem kötelező frissítés, és adja meg a Wmfversion kellett = "5.1PP' a Resource Manager-sablonok a WMF 5.1-es előzetes verzió telepítéséhez. Wmfversion = "latest" továbbra is telepíti a [WMF 5.0 RTM-re](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/). További információ a WMF 5.1-es előzetes verzió: [ebben a blogbejegyzésben](https://blogs.msdn.microsoft.com/powershell/2016/07/16/announcing-windows-management-framework-wmf-5-1-preview/).
  - Kisebb más javításokat, és fejlesztések lettek hozzáadva.

### <a name="version--219"></a>Verzió 2.19

- **Kiadás dátuma:** 2016. június 3.
- **Operációsrendszer-támogatást:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **A WMF-támogatás:** A WMF 5.0 RTM-re, a WMF 4.0-s frissítéssel, a WMF 4.0
- **Környezet:** Azure, Azure China, Azure Government
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016 Technical Preview; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - A DSC-bővítmény már előkészítve az Azure China. Ebben a verzióban elsősorban a bővítményt futtató az Azure China javításait tartalmazza.

### <a name="version-218"></a>Verzió 2.18.

- **Kiadás dátuma:** 2016. június 3.
- **Operációsrendszer-támogatást:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **A WMF-támogatás:** A WMF 5.0 RTM-re, a WMF 4.0-s frissítéssel, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016 Technical Preview; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - Győződjön meg a telemetriai adatokat a nem blokkoló hiba esetén telemetriai gyorsjavításhoz (ismert probléma az Azure DNS) vagy a telepítés során.
  - Javítsa ki az időszakos probléma, ahol a bővítmény konfigurációjának feldolgozása a számítógép újraindítása után leállítja. Ennek következtében a DSC-bővítmény "Moore" állapotban marad.
  - Kisebb más javításokat, és fejlesztések lettek hozzáadva.

### <a name="version-217"></a>Verzió 2.17

- **Kiadás dátuma:** 2016. április 26.
- **Operációsrendszer-támogatást:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **A WMF-támogatás:** A WMF 5.0 RTM-re, a WMF 4.0-s frissítéssel, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016 Technical Preview; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - Támogatja a WMF 4.0 frissítést. A WMF 4.0 frissítési további információkért lásd: [ebben a blogbejegyzésben](https://blogs.msdn.microsoft.com/powershell/2016/01/19/windows-management-framework-wmf-4-0-update-now-available-for-windows-server-2012-windows-server-2008-r2-sp1-and-windows-7-sp1/).
  - Újrapróbálkozási logika, a hibákat, a DSC-bővítmény telepítése során, és a DSC-konfiguráció alkalmazása közben küldeni a bővítmény telepítése. Ez a változás részeként a bővítmény próbálja megismételni a telepítést, ha egy korábbi telepítése nem sikerült, vagy újra életbe a DSC-konfiguráció korában meghiúsult, legfeljebb három alkalommal addig a befejezési állapota (sikeres/meghiúsult), vagy ha új kérelem érkezik. Ha a kiterjesztés érvénytelen felhasználói beállítások vagy felhasználói adatbevitelt miatt hiúsul meg, hogy nem próbálja meg újra. Ebben az esetben a bővítmény kell újra hívható meg egy új kérelmet, és javítsa ki a felhasználói beállítások. Megjegyzés: A DSC-bővítmény szolgáltatás az Azure-beli Virtuálisgép-ügynök az újrapróbálkozások függ. Az Azure Virtuálisgép-ügynök a bővítményt a legutóbbi sikertelen kérelem hív meg, addig a sikeres vagy kritikus állapotot.

### <a name="version-216"></a>Verzió 2.16

- **Kiadás dátuma:** 2016. április 21-én
- **Operációsrendszer-támogatást:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **A WMF-támogatás:** A WMF 5.0 RTM, A WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016 Technical Preview; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - Hibakezelés és további kisebb hibajavítások javításához.
  - DSC-bővítmény beállításai az új tulajdonság. A DSC-bővítmény engedélyezéséhez AdvancedOptions "ForcePullAndApply" adnak kihirdeti DSC-konfigurációk, ha a frissítési mód lekéréses (szemben az alapértelmezett leküldéses módban). További információkért tekintse meg [ebben a blogbejegyzésben](https://blogs.msdn.microsoft.com/powershell/2016/02/26/arm-dsc-extension-settings/) további információért a DSC-bővítmény beállításai.

### <a name="version-215"></a>Verzió 2.15

- **Kiadás dátuma:** 2016. március 14-én
- **Operációsrendszer-támogatást:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **A WMF-támogatás:** A WMF 5.0 RTM, A WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016 Technical Preview; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - Bővítmény verziója 2.14 telepítse a WMF RTM módosításai szerepeltek. A bővítmény verziója 2.13.2.0 való 2.14.0.0 a frissítés során, Észreveheti, hogy egyes DSC parancsmagok sikertelen, vagy a konfigurációs hiba miatt nem sikerül – "Példány nem található a megadott tulajdonság értékek". További információkért lásd: a [DSC kibocsátási megjegyzések](https://msdn.microsoft.com/en-us/powershell/wmf/limitation_dsc). Ezek a problémák megoldásai 2.15 verzióban lettek hozzáadva.
  - Sajnos, ha már telepített verzió 2.14, és azokat a fenti két problémák egyike fut, meg kell ezeket a lépéseket manuálisan.  Egy rendszergazda jogú PowerShell-munkamenetben:
    - `Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof`
    - `mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof`

### <a name="version-214"></a>Verzió 2.14

- **Kiadás dátuma:** 2016. február 25-én
- **Operációsrendszer-támogatást:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **A WMF-támogatás:** A WMF 5.0 RTM, A WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** Ez a verzió DSC használ, a Windows Server 2016 Technical Preview; részeként a többi Windows OSE-kre, telepíti a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - A WMF RTM használ.
  - Engedélyezi az adatgyűjtést a DSC-bővítmény minőségének javítása érdekében. További információkért lásd: [a blogon](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/).
  - A bővítmény a Resource Manager-sablonnal biztosít egy frissített beállítások formátuma. További információkért lásd: [a blogon](https://blogs.msdn.microsoft.com/powershell/2016/02/26/arm-dsc-extension-settings/).
  - Hibajavításokat tartalmaz, és további fejlesztést.

## <a name="next-steps"></a>További lépések

- További információ a PowerShell DSC, nyissa meg a [PowerShell dokumentációs központban](../overview/overview.md).
- Vizsgálja meg a [Resource Manager-sablon a DSC-bővítmény](/azure/virtual-machines/extensions/dsc-template).
- A további funkciókat, amelyeket felügyelhet a PowerShell DSC használatával, és további DSC-erőforrásokat, keresse meg a [PowerShell-galériából](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0).
- Bizalmas paraméterek átadása az konfigurációk kapcsolatos részletekért lásd: [biztonságosan a DSC-kiterjesztés kezelő a hitelesítő adatok kezelése](/azure/virtual-machines/extensions/dsc-credentials).
