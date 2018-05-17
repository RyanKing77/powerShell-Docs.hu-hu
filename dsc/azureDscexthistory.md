---
description: Az Azure-ban a kívánt állapot konfigurációs szolgáltatása (DSC) bővítmény korábbi verzióinak megismerése.
ms.date: 05/09/2018
keywords: a DSC, az azure powershell-bővítmény
title: Azure DSC-bővítményt verziójának előzményei
ms.openlocfilehash: 81dfcf81bd8f8685a0c8c81cd07bc5447e1abf94
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="azure-desired-state-configuration-extension-version-history"></a>Azure kívánt állapot konfigurációs bővítmény verziójának előzményei

Az Azure kívánt állapot konfigurációs szolgáltatása (DSC) Virtuálisgép-bővítmény frissül, szükség szerint fejlesztéseket és új képességek érhetők el Azure, a Windows Server és a Windows Management Framework (WMF), amely tartalmazza a Windows PowerShell támogatása.

Ez a cikk az Azure DSC Virtuálisgép-bővítmény, az egyes verziójával kapcsolatos tájékoztatást fogunk adni azt támogatja, és a megjegyzések, és új szolgáltatásokat vagy módosításokat megjegyzések milyen környezetekben.

## <a name="latest-versions"></a>Legújabb verzió

### <a name="version-276"></a>2.76 verziója

- **Kiadás dátuma:**
  - 2018. május 9.
- **Az operációs rendszer támogatása:**
  - Windows Server 2016
  - Windows Server 2012 R2
  - Windows Server 2012
  - Windows Server 2008 R2 SP1
  - Windows-ügyfeleken 7/8.1/10
  - Nano Server
- **WMF támogatják:**
  - WMF 5.1
  - WMF 5.0 RTM
  - WMF 4.0 frissítése
  - WMF 4.0
- **Rendelkező környezetben:**
  - Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális Gépen.
- **Új funkciók:**
  - A részállapot és egyéb kisebb hibák javításával bővítmény metaadatait javítása.

### <a name="version-219"></a>2.19 verziója

- **Kiadás dátuma:**
  - 2016. június 3.
- **Az operációs rendszer támogatása:**
  - Windows Server 2016 Technical Preview
  - Windows Server 2012 R2
  - Windows Server 2012
  - Windows Server 2008 R2 SP1
- **WMF támogatják:**
  - WMF 5.0 RTM
  - WMF 4.0 frissítése
  - WMF 4.0
- **Rendelkező környezetben:**
  - Azure
  - Azure China
  - Az Azure Government
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016 Technical Preview; más operációs rendszerei között, az telepíti a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - A DSC-bővítményt van most az előre telepített Azure Kína felé. Ebben a verzióban elsősorban a bővítmény futtatása Azure Kína javításait tartalmazzák.

## <a name="supported-versions"></a>Támogatott verziók

> [!WARNING]
> 2.4 keresztül 2.13 verziók WMF 5.0 Public Preview amelyek aláíró tanúsítványa lejárt 2016 augusztusában használja.  A problémával kapcsolatos további információkért lásd: [blogbejegyzés](https://blogs.msdn.microsoft.com/powershell/2016/05/24/azure-dsc-extension-versions-2-4-up-to-2-13-will-retire-in-august/).

### <a name="version-275"></a>2.75 verziója

- **Kiadás dátuma:** 2018. március 5.
- **Az operációs rendszer támogatási:** Windows Server 2016-os, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows ügyfél 7/8.1/10, Nano Server
- **WMF támogatási:** WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális Gépen.
- **Új funkciók:**
  - GitHub legutóbbi helyezze át a TLS 1.2, után bevezetésében Azure Automation DSC Azure piactéren elérhető DIY Resource Manager-sablonok használatával egy virtuális Gépet nem, vagy DSC-bővítményt használja a konfiguráció a Githubon található. A bővítmény telepítése során a következőhöz hasonló hiba jelenik meg:

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

  - A bővítmény új verziójában a TLS 1.2 kényszerítése megtörtént. A bővítmény telepítésekor, ha már a AutoUpgradeMinorVersion = true a Resource Manager-sablon, majd a bővítmény a 2.75 autoupgraded fogja kapni. A manuális frissítéseket, adja meg `TypeHandlerVersion = 2.75` az erőforrás-kezelő sablonban.

### <a name="version-270---272"></a>2.70. bekezdés-2.72 verziója

- **Kiadás dátuma:** 2017. November 13.
- **Az operációs rendszer támogatási:** Windows Server 2016-os, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows ügyfél 7/8.1/10, Nano Server
- **WMF támogatási:** WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális Gépen.
- **Új funkciók:**
  - Programhiba javítások & fejlesztései, amely leegyszerűsíti az Azure Automation DSC a a felhasználói felület portálon keresztül, valamint a Resource Manager-sablon használatával.  További információkért lásd: [alapértelmezett konfigurációs parancsfájl](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/extensions-dsc-overview#default-configuration-script) a DSC-bővítményt dokumentációjában.

### <a name="version-226"></a>2.26 pontban verziója

- **Kiadás dátuma:** 2017. június 9-es.
- **Az operációs rendszer támogatási:** Windows Server 2016-os, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows ügyfél 7/8.1/10, Nano Server
- **WMF támogatási:** WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális Gépen.
- **Új funkciók:**
  - Továbbfejlesztett telemetria.

### <a name="version-225"></a>2.25 verziója

- **Kiadás dátuma:** 2017. június 2.
- **Az operációs rendszer támogatási:** Windows Server 2016-os, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows ügyfél 7/8.1/10, Nano Server
- **WMF támogatási:** WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális Gépen.
- **Új funkciók:**
  - Számos hibajavítást és egyéb kisebb fejlesztések lettek hozzáadva.

### <a name="version-224"></a>2,24 verzió

- **Kiadás dátuma:** 2017. április 13.
- **Az operációs rendszer támogatási:** Windows Server 2016-ot, a Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **WMF támogatási:** WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális Gépen.
- **Új funkciók:**
  - Virtuális gép UUID & DSC ügynök azonosító bővítmény metaadatok mutatja. Egyéb kisebb fejlesztések lettek hozzáadva.

### <a name="version-223"></a>2.23 verzió

- **Kiadás dátuma:** 2017. március 15.
- **Az operációs rendszer támogatási:** Windows Server 2016-ot, a Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **WMF támogatási:** WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális Gépen.
- **Új funkciók:**
  - Nagy mennyiségű hibajavításokat és egyéb fejlesztések lettek hozzáadva.

### <a name="version-222"></a>2.22 verzió

- **Kiadás dátuma:** 2017. február 8.
- **Az operációs rendszer támogatási:** Windows Server 2016-ot, a Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **WMF támogatási:** WMF 5.1, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális Gépen.
- **Új funkciók:**
  - A DSC-bővítmény most már a WMF 5.1 támogatása.
  - Kisebb egyéb fejlesztések lettek hozzáadva.

### <a name="version-221"></a>2.21 verziója

- **Kiadás dátuma:** 2016. December 2.
- **Az operációs rendszer támogatási:** Windows Server 2016-ot, a Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **WMF támogatási:** WMF 5.1 Preview, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése). A Nano Server a DSC szerepkör telepítve van a virtuális Gépen.
- **Új funkciók:**
  - A DSC-bővítményt a Nano Server most érhető el. Ebben a verzióban elsősorban a bővítmény futtatása Nano Server kódmódosításokat tartalmazza.
  - Kisebb egyéb fejlesztések lettek hozzáadva.

### <a name="version-220"></a>Verzió 2.20.

- **Kiadás dátuma:** 2016 augusztusától 2
- **Az operációs rendszer támogatási:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **WMF támogatási:** WMF 5.1 Preview, a WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016 Technical Preview; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - A WMF 5.1 Preview támogatja. Első közzétételekor, ebben a verzióban lett-e a nem kötelező frissítés, és Wmfversion meg kellett = "5.1PP' a Resource Manager-sablonok WMF 5.1 előzetes verzió telepítéséhez. Wmfversion = "legújabb" továbbra is telepíti a [WMF 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/). További információ a WMF 5.1 Preview-ban: [ebben a blogban]( https://blogs.msdn.microsoft.com/powershell/2016/07/16/announcing-windows-management-framework-wmf-5-1-preview/).
  - Alverziószám egyéb javításai, és fejlesztések lettek hozzáadva.

### <a name="version--219"></a>2.19 verziója

- **Kiadás dátuma:** 2016. június 3.
- **Az operációs rendszer támogatási:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **WMF támogatási:** WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure Government Azure, az Azure Kínában
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016 Technical Preview; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - A DSC-bővítmény már Azure Kína felé előkészítve. Ebben a verzióban elsősorban a bővítmény futtatása Azure Kína javításait tartalmazzák.

### <a name="version-218"></a>Verzió 2.18.

- **Kiadás dátuma:** 2016. június 3.
- **Az operációs rendszer támogatási:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **WMF támogatási:** WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016 Technical Preview; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - Ellenőrizze a telemetriai adatok nem blokkoló hiba esetén telemetriai gyorsjavítás letöltése (ismert Azure DNS-probléma) vagy a telepítés során.
  - Javítsa ki az időszakos probléma, ahol a bővítmény leállítja a rendszer újraindítása után konfigurációjának feldolgozása. Ennek következtében a DSC-bővítményt "váltás" állapotban marad.
  - Alverziószám egyéb javításai, és fejlesztések lettek hozzáadva.

### <a name="version-217"></a>2.17 verziója

- **Kiadás dátuma:** 2016. április 26.
- **Az operációs rendszer támogatási:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **WMF támogatási:** WMF 5.0 RTM-re, a WMF 4.0 frissítést, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016 Technical Preview; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - Támogatja a WMF 4.0 frissítést. WMF 4.0 frissítési további információkért lásd: [ebben a blogban](https://blogs.msdn.microsoft.com/powershell/2016/01/19/windows-management-framework-wmf-4-0-update-now-available-for-windows-server-2012-windows-server-2008-r2-sp1-and-windows-7-sp1/).
  - Újrapróbálkozási logika, amelyek a DSC-bővítmény telepítése során, vagy a DSC-konfiguráció alkalmazása közben utáni bővítmény telepítése. Ez a változás részeként a bővítmény próbálja meg újra a telepítést, ha egy korábbi telepítés nem sikerült, vagy újra életbe a DSC-konfiguráció, amely korábban nem tudta, legfeljebb három alkalommal nem éri a befejezési állapotban (sikeres vagy hiba), vagy ha új kérelem érkezik. Ha a kiterjesztés érvénytelen felhasználói beállítások vagy felhasználói adatbevitelt miatt meghiúsul, akkor nem próbálja meg újra. Ebben az esetben a bővítmény hívható meg újra egy új kérelmet, és javítsa ki a felhasználói beállítások kell. Megjegyzés: Az Azure Virtuálisgép-ügynök a próbálkozások a függ a DSC-bővítményt. Az Azure Virtuálisgép-ügynök a bővítményt a legutolsó sikertelen kérelem hív meg, nem éri a sikeres vagy kritikus állapotot.

### <a name="version-216"></a>2.16 verziója

- **Kiadás dátuma:** 2016. április 21.
- **Az operációs rendszer támogatási:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **WMF támogatási:** WMF 5.0 RTM-re, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016 Technical Preview; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - Hibakezelés és egyéb kisebb hibák javításával javításához.
  - A DSC-bővítmény beállításai új tulajdonság. AdvancedOptions "ForcePullAndApply" hozzáadódik a DSC-bővítmény engedélyezése a DSC-konfigurációk kihirdeti, ha a frissítési mód lekéréses (nem az alapértelmezett leküldéses üzemmód). További információkért tekintse meg [ebben a blogban](https://blogs.msdn.microsoft.com/powershell/2016/02/26/arm-dsc-extension-settings/) további információkat a DSC-bővítmény beállításai.

### <a name="version-215"></a>2.15 verziója

- **Kiadás dátuma:** 2016. március 14.
- **Az operációs rendszer támogatási:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **WMF támogatási:** WMF 5.0 RTM-re, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016 Technical Preview; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - Bővítmény verziójában 2.14 telepítse a WMF RTM változtatásainak tartalmazza. 2.13.2.0 való 2.14.0.0 bővítmény verziójáról a frissítés során azt tapasztalhatja, hogy néhány DSC parancsmaggal sikertelen vagy a konfigurációs hiba miatt sikertelen – "Példány nem található a megadott tulajdonság értékek". További információkért lásd: a [DSC kibocsátási megjegyzések](https://msdn.microsoft.com/en-us/powershell/wmf/limitation_dsc). Ezek a problémák megoldásai 2.15 verziójában váltak elérhetővé.
  - Sajnos Ha már telepített verzió 2.14, és azokat a fenti két problémák egyike fut, akkor a következő lépésekkel manuálisan.  Egy rendszergazda jogú PowerShell-munkamenetben:
    - `Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof`
    - `mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof`

### <a name="version-214"></a>2.14 verziója

- **Kiadás dátuma:** 2016. február 25.
- **Az operációs rendszer támogatási:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **WMF támogatási:** WMF 5.0 RTM-re, a WMF 4.0
- **Környezet:** Azure
- **Megjegyzés:** ebben a verzióban DSC használ, a csomag részeként a Windows Server 2016 Technical Preview; az egyéb Windows operációs rendszer telepítése a [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (újraindítást igényel WMF telepítése).
- **Új funkciók:**
  - WMF RTM használja.
  - Lehetővé teszi, hogy az adatok gyűjtését a DSC-bővítményt minőségének javítása érdekében. További információkért lásd: [a blog](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/).
  - A Resource Manager-sablon a bővítmény frissített beállításokkal formátumú biztosít. További információkért lásd: [a blog](https://blogs.msdn.microsoft.com/powershell/2016/02/26/arm-dsc-extension-settings/).
  - Hibajavításokat tartalmaz, és más fejlesztései.

## <a name="next-steps"></a>További lépések

- A PowerShell DSC kapcsolatos további információkért lásd a [PowerShell dokumentációs központban](overview.md).
- Vizsgálja meg a [Resource Manager-sablon a DSC-bővítmény](/azure/virtual-machines/windows/extensions-dsc-template).
- A PowerShell DSC használatával felügyelhető további funkciókat, és további DSC-erőforrásokat, keresse meg a [PowerShell-galériában](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0).
- További információk a konfigurációk a bizalmas paraméterek átadása: [biztonságosan a DSC-bővítmény kezelő a hitelesítő adatok kezelése](/azure/virtual-machines/windows/extensions-dsc-credentials).