---
ms.date: 08/23/2017
keywords: PowerShell parancsmag
title: telepítheti és használhatja a windows powershell web access
ms.openlocfilehash: 8f140e73ce833fd1cfadbe1d8ee0fe0bb2d08873
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953922"
---
# <a name="install-and-use-windows-powershell-web-access"></a>Webes Windows PowerShell-elérés telepítése és használata

Frissített: 5, a 2013. novemberi (szerkeszthető: 2017. augusztus 23.)

Vonatkozik: Windows Server 2012 R2, Windows Server 2012-ben

## <a name="introduction"></a>Bevezetés

A Windows PowerShell Web Access, először a Windows Server 2012-ben bevezetett átjáróként működik, a Windows PowerShell, és webes Windows PowerShell konzolt, amely egy távoli számítógépre irányul. Ez lehetővé teszi az informatikai szakemberek egy webböngészőben, nem a Windows PowerShell, a távoli felügyeleti szoftver vagy a böngésző beépülő modul telepítése szükséges az ügyféleszközön Windows PowerShell-konzolban a Windows PowerShell-parancsokat és a parancsfájlok futtatásához. A webes Windows PowerShell konzol futtatásához szükséges egy megfelelően konfigurált Windows PowerShell Web Access-átjáró és egy eszköz ügyfélböngésző, amely támogatja a JavaScript és elfogadja a cookie-kat.

Az ügyféleszköz lehet laptop, nem munkára használt vagy kölcsönbe kapott számítógép, táblagép, webterminál, nem Windows-alapú operációs rendszert futtató számítógép vagy mobiltelefonos böngésző. Az informatikai szakemberek kritikus fontosságú kezelési műveleteket végezhetnek távoli Windows-alapú kiszolgálókon egy internetkapcsolattal rendelkező eszköz és egy webböngésző használatával.

Átjáró sikeres beállítása és konfigurációja után felhasználók férhetnek hozzá a Windows PowerShell-konzolban webböngésző segítségével. Amikor a felhasználók megnyitják a biztonságos Windows PowerShell Web Access webhely, a sikeres hitelesítés után futtathatják a webalapú Windows PowerShell-konzolban.

A Windows PowerShell Web Access beállítása és konfigurációja egy három lépéses folyamat a következő:

1. [Windows PowerShell Web Access telepítése](#install-windows-powershell-web-access)
1. [Az átjáró konfigurálása](#configure-the-gateway)
1. [Korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule)

Mielőtt telepítése és konfigurálása a Windows PowerShell Web Access, azt javasoljuk, hogy elolvasta a teljes útmutató, amely telepítésével kapcsolatos utasításokat tartalmaz, biztonságos, és távolítsa el a Windows PowerShell Web Access.
A [a webes Windows PowerShell konzol használata](https://technet.microsoft.com/library/hh831417(v=ws.11).aspx) a témakör bemutatja, hogyan jelentkeznek be a webalapú konzolba, és korlátozások és a webes Windows PowerShell konzol közötti különbségeket tartalmazza, és a  **PowerShell.exe** konzol. Olvassa el a végfelhasználók számára a webalapú konzol [használja a Web-alapú Windows PowerShell konzol](use-the-web-based-windows-powershell-console.md), de nem szükséges ez az útmutató többi részétől.

Ez a témakör nem ad részletes IIS-webkiszolgáló műveletek útmutatást; Ez a témakör csak a a Windows PowerShell Web Access-átjáró konfigurálásához szükséges lépéseket ismerteti. A webhelyek IIS-ben való konfigurálásával és biztonságossá tételével kapcsolatos további információkért tekintse meg az IIS dokumentációs forrásanyagait a Lásd még szakaszban.

Az alábbi ábrán látható, hogyan működik a Windows PowerShell Web Access.

![A Webes Windows PowerShell-elérés diagramja](images/Windows-PowerShell-Web-Access-diagram.jpg)

## <a name="requirements-for-running-windows-powershell-web-access"></a>A webes Windows PowerShell-elérés futtatásának követelményei

A Windows PowerShell Web Access szükséges a webkiszolgáló (IIS), a .NET-keretrendszer 4.5, és a Windows PowerShell 3.0 vagy a Windows PowerShell 4.0 a kiszolgálón, amelyen az átjáró futtatni kívánt futnia kell. A szerepkörök hozzáadása és a varázsló a Kiszolgálókezelő vagy a Windows PowerShell telepítési parancsmagok a Kiszolgálókezelő használatával telepítheti a Windows PowerShell Web Access Windows Server 2012 R2 rendszert futtató kiszolgálón vagy a Windows Server 2012. A Windows PowerShell Web Access telepítésekor a Kiszolgálókezelő vagy a központi telepítés parancsmagokkal szükséges szerepkörök és szolgáltatások rendszer automatikusan hozzáadja a telepítési folyamat részeként.

A Windows PowerShell Web Access lehetővé teszi, hogy a távoli felhasználók férhetnek hozzá a szervezet számítógépeinek webböngészőben a Windows PowerShell használatával. Bár a Windows PowerShell Web Access egy kényelmes és hatékony kezelőeszköz, a webalapú hozzáférés biztonsági kockázatot is jelent, és a lehető biztonságos helyen kell konfigurálni. Azt javasoljuk, hogy a Windows PowerShell Web Access-átjáró konfiguráló rendszergazdák számára elérhető biztonsági rétegek használatához a Parancsmagalapú hitelesítési szabályokat is részét képező Windows PowerShell Web Access és biztonsági réteg, amely elérhető a Web Server) Az IIS) és a harmadik felektől származó alkalmazásokat. Ebben a dokumentációban szerepelnek példák a csak tesztkörnyezetben ajánlott, nem biztonságos konfigurációkra, valamint biztonságos telepítéshez ajánlott konfigurációkra is.

## <a name="browser-and-client-device-support"></a>Támogatott böngészők és ügyféleszközök

A Windows PowerShell Web Access a következő webböngészőket támogatja.
Bár a mobilböngészők hivatalosan nem támogatottak, számos mobilböngésző képes a webalapú Windows PowerShell konzol futtatásához. Egyéb, cookie-kat elfogadó, JavaScriptet és HTTPS-webhelyeket futtató böngészők valószínűleg képesek a konzol használatára, de hivatalosan még nem lettek tesztelve.

### <a name="supported-desktop-computer-browsers"></a>Támogatott asztali számítógépes böngészők

- Windows Internet Explorer alkalmazás Microsoft Windows 8.0, 9.0, 10.0 és 11.0
- Mozilla Firefox 10.0.2
- Google Chrome-17.0.963.56m Windows
- Apple Safari 5.1.2 Windows rendszerhez
- Apple Safari 5.1.2 Mac OS

### <a name="minimally-tested-mobile-devices-or-browsers"></a>Minimális tesztelésen átesett mobileszközök és böngészők

- Windows Phone 7 és 7.5
- Google Android WebKit 3.1 böngésző Android 2.2.1-en (Kernel 2.6)
- Apple Safari 5.0.1-es iPhone operációs rendszerhez
- Apple Safari 5.0.1-es iPad 2 operációs rendszerhez

### <a name="browser-requirements"></a>Böngészőkre vonatkozó követelmények

A Windows PowerShell Web Access webalapú konzol használatához böngészők a következőket kell tennie.

- A Windows PowerShell Web Access-átjáró webhelyéről cookie-k engedélyezése.
- HTTPS-lapok megnyitása és olvasása.
- JavaScriptet használó webhelyek megnyitása és futtatása.

## <a name="recommended-quick-deployment"></a>Javasolt a gyors telepítéshez

A Windows PowerShell Web Access átjárót telepítheti a Windows Server 2012 R2 rendszert futtató kiszolgálón vagy a Windows Server 2012 vagy Windows PowerShell-parancsmagok használatával, vagy a hozzáadása szerepkörök és szolgáltatások varázsló, amely meg van nyitva a Kiszolgálókezelő használatával. Gyors telepítése és konfigurálása használja a Windows PowerShell-parancsmagok, ebben a szakaszban leírtak szerint.

1. [Windows PowerShell Web Access telepítése](#install-Windows-powershell-web-access)
1. [Az átjáró konfigurálása](#configure-the-gateway)
1. [Korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule)

### <a name="install-windows-powershell-web-access"></a>Webes Windows PowerShell-elérés telepítése

#### <a name="to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets"></a>Webes Windows PowerShell-elérés telepítése a Windows PowerShell-parancsmagok használatával

1. Hajtsa végre az alábbi Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultsággal nyissa meg.
    - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán, és kattintson a **Futtatás rendszergazdaként**.
    - A Windows **Start** kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

    >**![Megjegyzés:](images/note.jpeg) Megjegyzés** Windows PowerShell 3.0 és 4.0-s verzióját, nincs szükség a Kiszolgálókezelő parancsmag modul importálása a Windows PowerShell-munkamenetbe, a modul részét képező parancsmagok futtatása előtt. A rendszer automatikusan importál egy modult a modul részét képező parancsmag első futtatásakor. A Windows PowerShell-parancsmagok is nem kis-és nagybetűket.

1. Írja be a következőt, és nyomja le az **Enter**, ahol *számítógép_neve* jelöli egy távoli számítógépen, amelyen szeretné telepíteni a Windows PowerShell Web Access, ha van ilyen. A `-Restart` paraméter automatikusan újraindítja a célkiszolgálókat, ha az szükséges.

   `Install-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -IncludeManagementTools -Restart`

   >**![Megjegyzés:](images/note.jpeg) Megjegyzés**
   >
   >A Windows PowerShell-parancsmagok használatával történő telepítése a Windows PowerShell Web Access nem ad hozzá webkiszolgáló (IIS) felügyeleti eszközök alapértelmezés szerint. Ha szeretné telepíteni a kezelőeszközöket ugyanarra a kiszolgálóra, mint a Windows PowerShell Web Access-átjáró, vegye fel a `-IncludeManagementTools` paramétert a telepítési parancshoz (ebben a lépésben ismertetett). Ha a Windows PowerShell Web Access webhely távoli számítógépről kezeli, telepítse az IIS-kezelő beépülő modul telepítésével [távoli kiszolgáló felügyeleti Toolsfor Windows 8.1](http://go.microsoft.com/fwlink/?LinkID=304145) vagy [távoli kiszolgáló felügyelete Windows 8-eszközök](http://go.microsoft.com/fwlink/p/?LinkID=238560) , amelyből az átjáró kezelni kívánt számítógépen.

   Szerepkörök és szolgáltatások offline virtuális merevlemezen történő telepítéséhez hozzá kell adnia a `-ComputerName` és a `-VHD` paramétert is. A(z) `-ComputerName` paraméter a kiszolgáló nevét tartalmazza, amelyhez a VHD-t csatlakoztatni kívánja, a(z) `-VHD` paraméter pedig a VHD-fájl elérési útvonalát tartalmazza a megadott kiszolgálón.

   `Install-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -IncludeManagementTools -Restart`

1. Ha telepítés befejeződött, győződjön meg arról, hogy a Windows PowerShell Web Access telepítette a célkiszolgálón fut a **Get-WindowsFeature** parancsmagot a célkiszolgálón, megnyitott Windows PowerShell-konzolban emelt szintű felhasználói jogosultságokkal. Azt is ellenőrizheti, hogy a Windows PowerShell Web Access lett telepítve a Kiszolgálókezelő konzol választva módosíthatja a célkiszolgáló a **összes kiszolgáló** lapot, és tekintse meg a **szerepkörök és szolgáltatások** a kiválasztott kiszolgálóhoz tartozó csempére. Az információs fájl Windows PowerShell Web Access is megtekintheti.

1. A Windows PowerShell Web Access telepítése után a rendszer kéri a tekintse át az információs fájl, amely az átjáró alapvető és szükséges beállítási utasításait tartalmazza. A telepítési utasításokat is szerepelnek a következő szakaszban [az átjáró konfigurálása](#configure-the-gateway). Az információs fájl elérési útja **C:\\Windows\\webes\\PowerShellWebAccess\\wwwroot\\README.txt**.

### <a name="configure-the-gateway"></a>Az átjáró konfigurálása

A **Install-PswaWebApplication** parancsmag egy gyors módja a Windows PowerShell Web Access konfigurálva. Bár hozzáadhatja a `UseTestCertificate` paramétert az `Install-PswaWebApplication` parancsmaghoz egy önaláírt SSL-tanúsítvány tesztelés céljából történő telepítéséhez, ez nem biztonságos. A biztonságos éles környezethez mindig érvényes, hitelesítésszolgáltató (CA) által aláírt SSL-tanúsítványt használjon.
A rendszergazdák kicserélhetik a tesztcélú tanúsítványt az IIS-kezelő konzolján egy tetszőleges aláírt tanúsítványra.

A Windows PowerShell Web Access webes alkalmazás konfigurálását hajthatja végre a `Install-PswaWebApplication` parancsmag vagy az IIS-kezelőben GUI-alapú konfigurációs lépések elvégzésével. Alapértelmezés szerint a parancsmag telepíti a webes alkalmazás **pswa** (és egy alkalmazáskészletet, **pswa_pool**), a a **Default Web Site** tároló, ahogy az IIS-kezelőben; Ha szükség esetén utasíthatja a parancsmagot a webalkalmazás alapértelmezett helytárolójának módosítására. Az IIS-kezelő webalkalmazásokhoz elérhető konfigurációs beállításokat kínál, például a portszám vagy az SSL-tanúsítvány módosítását.

>**![Biztonsági megjegyzés](images/securitynote.jpeg) biztonsági Megjegyzés**
>
>Erősen ajánlott, hogy a rendszergazdák az átjárót egy érvényes, hitelesítésszolgáltató által aláírt tanúsítvány használatára konfigurálják.

#### <a name="to-configure-the-windows-powershell-web-access-gateway-with-a-test-certificate-by-using-install-pswawebapplication"></a>A Webes Windows PowerShell-elérési átjáró konfigurálása egy tesztcélú tanúsítvánnyal az Install-PswaWebApplication használatával

1. Hajtsa végre az alábbi Windows PowerShell-munkamenet megnyitásához.

    - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán.

    - A Windows **Start** kattintson **Windows PowerShell**.

2. Írja be a következőt, és nyomja le az **Enter**.

    **Install-PswaWebApplication - UseTestCertificate**

  >**![Biztonsági megjegyzés](images/securitynote.jpeg) biztonsági Megjegyzés**
  >
  >A `UseTestCertificate` paramétert csak privát tesztkörnyezetben szabad használni. A biztonságos éles környezet érdekében javasoljuk egy érvényes, hitelesítésszolgáltató által aláírt tanúsítványt használatát.

A parancsmag futtatása telepíti a Windows PowerShell Web Access webalkalmazást az IIS alapértelmezett webhely tárolóján belül. A parancsmag létrehozza az alapértelmezett webhelyen a Windows PowerShell Web Access futtatásához szükséges infrastruktúra `https://<server_name>/pswa`. A webalkalmazás egy másik webhelyre történő telepítéséhez adja meg a webhely nevét a `WebSiteName` paraméter hozzáadásával. A webalkalmazás nevének módosításához (alapértelmezés szerint `pswa`) adja hozzá a `WebApplicationName` paramétert.

A következő beállítások a parancsmag futtatásával konfigurálhatók. Ezeket az adatokat, ha szükséges, az IIS-kezelő konzolján manuálisan módosítani tudja.

- Path: /pswa
- ApplicationPool: pswa_pool
- EnabledProtocols: http
- PhysicalPath: %*windir*%/Web/PowerShellWebAccess/wwwroot

**Példa**: `Install-PswaWebApplication -webApplicationName myWebApp -useTestCertificate`

Ebben a példában az eredményül kapott webhelye a Windows PowerShell Web Access https://\<*kiszolgáló_neve*\>/myWebApp.

>**![Megjegyzés:](images/note.jpeg) Megjegyzés**
>
>Addig nem jelentkezhet be, amíg engedélyezési szabályok hozzáadásával nem biztosít hozzáférést a felhasználók számára a webhelyhez. További információkért lásd: [korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule) és [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="to-configure-the-windows-powershell-web-access-gateway-with-a-genuine-certificate-by-using-install-pswawebapplication-and-iis-manager"></a>A Webes Windows PowerShell-elérési átjáró konfigurálása egy eredeti tanúsítvánnyal az Install-PswaWebApplication parancsmag és az IIS-kezelő használatával

1. Hajtsa végre az alábbi Windows PowerShell-munkamenet megnyitásához.

    - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán.

    - A Windows **Start** kattintson **Windows PowerShell**.

2. Írja be a következőt, és nyomja le az **Enter**.

    **Install-PswaWebApplication**

    A következő átjáróbeállítások a parancsmag futtatásával konfigurálhatók.
    Ezeket az adatokat, ha szükséges, az IIS-kezelő konzolján manuálisan módosítani tudja.
    Megadhat értékeket az `Install-PswaWebApplication` parancsmag `WebsiteName` és `WebApplicationName` paramétereihez is.

    - Path: /pswa

    - ApplicationPool: pswa_pool

    - EnabledProtocols: http

    - PhysicalPath: %*windir*%/Web/PowerShellWebAccess/wwwroot

3. Nyissa meg az IIS-kezelő konzolját a következő módszerek valamelyikével.

    - A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán. Az a **eszközök** a Kiszolgálókezelő menüjében kattintson **Internet Information Services (IIS) Manager**.

    - A Windows **Start** kattintson **Kiszolgálókezelő**.

4. Az IIS-kezelő fát megjelenítő ablaktáblán, bontsa ki a csomópontot, a kiszolgáló, amelyen a Windows PowerShell Web Access telepítve van, amíg a **helyek** mappa meg nem jelenik. Bontsa ki a **helyek** mappát.

5. Válassza ki a webhely, ahol a Windows PowerShell Web Access webalkalmazás telepítése. Az a **műveletek** ablaktáblán kattintson a **kötések**.

6. Az a **hely kötésének** párbeszédpanel, kattintson a **Hozzáadás**.

7. Az a **hely kötésének hozzáadása** párbeszédpanel a **típus** mezőben válassza **https**.

8. Az a **SSL-tanúsítvány** mező mellett válassza ki a megfelelő aláírt tanúsítványt a legördülő menüből. Kattintson az **OK** gombra. Lásd: [SSL-tanúsítvány konfigurálása az IIS-kezelőben](#to-configure-an-ssl-certificate-in-iis-Manager) tanúsítvány beszerzéséről további információt ebben a témakörben.

    A Windows PowerShell Web Access webalkalmazás az aláírt SSL-tanúsítvány használatára konfigurálta.

    A Windows PowerShell Web Access férhetnek megnyitása **https://\<kiszolgáló_neve\>/pswa** egy böngészőablakban.

>**![Megjegyzés:](images/note.jpeg) Megjegyzés**
>
>Addig nem jelentkezhet be, amíg engedélyezési szabályok hozzáadásával nem biztosít hozzáférést a felhasználók számára a webhelyhez.
>További információkért lásd: [korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule), ebben a témakörben és [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

### <a name="configure-a-restrictive-authorization-rule"></a>Korlátozó engedélyezési szabály konfigurálása

Miután a Windows PowerShell Web Access telepítve van, és az átjáró, felhasználó meg tudja nyitni a böngészőben a bejelentkezési oldal, de azok nem tud bejelentkezni, amíg a Windows PowerShell Web Access rendszergazdai hozzáférést biztosít a felhasználónak explicit módon. A következő táblázat ismerteti a Windows PowerShell-parancsmagok használatával a Windows PowerShell Web Access hozzáférés-vezérlés kezeli. Engedélyezési szabályok hozzáadásához és kezeléséhez nincs hasonló grafikus felhasználói felület. További részletes információk a Windows PowerShell Web Access parancsmagokról, lásd a parancsmagokkal kapcsolatos témaköröket [Windows PowerShell Web Access parancsmagok](cmdlets/web-access-cmdlets.md).

További információt a Windows PowerShell Web Access engedélyezési szabályairól és biztonságáról lásd: [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="to-add-a-restrictive-authorization-rule"></a>Korlátozó engedélyezési szabály hozzáadása

1. Hajtsa végre az alábbi Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultsággal nyissa meg.

    - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán, és kattintson a **Futtatás rendszergazdaként**.

    - A Windows **Start** kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

2. Opcionális megoldás a felhasználói hozzáférés korlátozására munkamenet-konfigurációk használatával: Győződjön meg arról, hogy munkamenet-konfigurációk, a használni kívánt a szabályokban már léteznek. Azok rendelkezik még nem jött létre, ha a munkamenet-konfigurációk létrehozásához használja utasításokat [about_Session_Configuration_Files](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_session_configurations).

3. Írja be a következőt, és nyomja le az **Enter**.

   `Add-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>`

   Ez az engedélyezési szabály lehetővé teszi, hogy egy adott felhasználó hozzáférést egy számítógéphez a hálózaton, amelyhez általában hozzáférhetnek, hozzáférést egy adott munkamenet-konfiguráció, ami a felhasználó szokásos parancsfájl-kezelési és parancsmag-igényeihez.

   A következő példában a `Contoso` tartomány `JSmith` nevű felhasználója hozzáférést kap a `Contoso_214` számítógép kezeléséhez, és egy `NewAdminsOnly` nevű munkamenet-konfiguráció használatához.

   `Add-PswaAuthorizationRule -UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly`

4. Győződjön meg arról, hogy létrejött-e a szabály futtatásával a `Get-PswaAuthorizationRule` parancsmagot, vagy `Test-PswaAuthorizationRule -UserName <domain\user> -ComputerName <computer-name>`

5. Például: `Test-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214`.

Az engedélyezési szabály konfigurálása után készen áll az engedélyezett felhasználók jelentkezzen be a webalapú konzol, és megkezdheti a Windows PowerShell Web Access használatát.

## <a name="custom-deployment"></a>Egyéni központi telepítés

A szerepkörök hozzáadása és szolgáltatások varázsló a Kiszolgálókezelő használatával telepítheti a Windows PowerShell Web Access-átjáró Windows Server 2012 R2 rendszert futtató kiszolgálón vagy a Windows Server 2012. A Windows PowerShell Web Access telepítése után testre szabhatja a az átjáró konfigurációját az IIS-kezelőben.

### <a name="install-windows-powershell-web-access"></a>Webes Windows PowerShell-elérés telepítése

#### <a name="to-install-windows-powershell-web-access-by-using-the-add-roles-and-features-wizard"></a>A Webes Windows PowerShell-elérés telepítése a Szerepkörök és szolgáltatások hozzáadása varázsló segítségével

1. Ha a Kiszolgálókezelő már meg nyitva, folytassa a következő lépéssel. Ha a Kiszolgálókezelő még nincs megnyitva, nyissa meg a következő módszerek valamelyikével.

    - A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán.

    - A Windows **Start** kattintson **Kiszolgálókezelő**.

2. Az a **kezelése** menüben kattintson a **szerepkörök és szolgáltatások hozzáadása**.

3. Az a **telepítés típusának kiválasztása** lapon, hogy melyik **szerepköralapú vagy szolgáltatásalapú telepítés**. Kattintson a **Tovább** gombra.

4. Az a **jelölje be a célkiszolgáló** lapon jelöljön ki egy kiszolgálót a kiszolgálókészletből, vagy válasszon egy offline VHD-t. Offline VHD célkiszolgálóként történő kiválasztásához először válassza ki a kiszolgálót, amelyhez csatlakoztatni kívánja a VHD-t, majd válassza ki a VHD-fájlt. Kiszolgálók a kiszolgálókészlethez adásával kapcsolatos információkért lásd: a Kiszolgálókezelő segítségével. Miután kiválasztotta a célkiszolgálón, kattintson a **következő**.

5. Az a **szolgáltatások kiválasztása** lapon bontsa ki a varázsló **Windows PowerShell**, majd válassza ki **Windows PowerShell Web Access**.

6. A rendszer a szükséges szolgáltatások, például a .NET keretrendszer 4.5-ös verziójának és a Webkiszolgáló (IIS) szerepkör-szolgáltatásainak hozzáadását kéri. Adja hozzá a szükséges szolgáltatásokat, és lépjen tovább.

    >**![Megjegyzés:](images/note.jpeg) Megjegyzés**
    >
    >Is Windows PowerShell Web Access telepítése a szerepkörök hozzáadása és szolgáltatások varázsló használatával telepíti a webkiszolgáló (IIS), beleértve az IIS-kezelő beépülő modul. A beépülő modul és egyéb IIS felügyeleti eszközök alapértelmezés szerint telepítendő hozzáadása szerepkörök és szolgáltatások varázsló használatakor. Ha a Windows PowerShell Web Access telepítése Windows PowerShell-parancsmagok használatával, a következő eljárásban leírtak szerint, a felügyeleti eszközök nem lettek hozzáadva alapértelmezés szerint.

7. Az a **erősítse meg a telepítendő** lapon, ha a szolgáltatásfájlokat a Windows PowerShell Web Access nem tárolja a 4. lépésben kiválasztott célkiszolgálón kattintson **adjon meg egy alternatív forrásútvonal**, és adja meg a szolgáltatásfájlok elérési útvonalát. Ellenkező esetben kattintson a **telepítése**.

8. Miután rákattintott **telepítése**, a **telepítési folyamat** lap megjeleníti a telepítés folyamatát, eredményeit és üzeneteket a figyelmeztetésekkel, vagy a telepítés utáni konfigurációs lépésekkel, amelyek például a Windows PowerShell Web Access szükséges. A Windows PowerShell Web Access telepítése után a rendszer kéri a tekintse át az információs fájl, amely az átjáró alapvető és szükséges beállítási utasításait tartalmazza. Ezek az utasítások is megtalálhatók ebben a témakörben. Az információs fájl elérési útja `C:\Windows\Web\PowerShellWebAccess\wwwroot\README.txt`.

### <a name="configure-the-gateway"></a>Az átjáró konfigurálása

Ebben a szakaszban található utasítások szolgálnak a Windows PowerShell Web Access webalkalmazás telepítése egy alkönyvtárában található cikkre hivatkozik, és nem a webhely gyökérkönyvtárában található. Ez az eljárás az `Install-PswaWebApplication` parancsmag által végrehajtott műveletek megfelelői a grafikus felhasználói felületen. Ebben a szakaszban az IIS-kezelő segítségével konfigurálhatja a Windows PowerShell Web Access-átjáró gyökérwebhelyként útmutatást is tartalmaz.

#### <a name="to-use-iis-manager-to-configure-the-gateway-in-an-existing-website"></a>Az IIS-kezelő használata az átjáró egy meglévő webhelyen történő konfigurálására

1. Nyissa meg az IIS-kezelő konzolját a következő módszerek valamelyikével.

    - A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán. Az a **eszközök** a Kiszolgálókezelő menüjében kattintson **Internet Information Services (IIS) Manager**.

    - A Windows **Start** írja be a nevek **Internet Information Services (IIS) Manager**. Kattintson a parancsikonra, amikor az megjelenik a **alkalmazások** eredmények.

2. Új alkalmazáskészlet létrehozása a Windows PowerShell Web Access. Bontsa ki az átjárókiszolgáló, az IIS-kezelő fát megjelenítő ablaktáblán válassza ki a csomópontot **alkalmazáskészletek**, és kattintson a **alkalmazáskészlet hozzáadása** a a **műveletek** ablaktáblán.

3. Nevű új alkalmazáskészlet hozzáadása **pswa_pool**, vagy adjon meg egy másik nevet. Kattintson az **OK** gombra.

4. Az IIS-kezelő fát megjelenítő ablaktáblán, bontsa ki a csomópontot, a kiszolgáló, amelyen a Windows PowerShell Web Access telepítve van, amíg a **helyek** mappa meg nem jelenik. Válassza ki a **helyek** mappát.

5. Kattintson a jobb gombbal a webhelyet (például **alapértelmezett webhely**) szeretné a Windows PowerShell Web Access webhely hozzáadása, és kattintson a **alkalmazás hozzáadása**.

6. Az a **Alias** mezőben írja be a pswa, vagy adjon meg egy másik aliast. Az alias lesz a virtuális könyvtár neve. Például **pswa** a következő URL-címben ebben a lépésben aliast jelenti: **https://\<kiszolgálónév\>/pswa**.

7. Az a **alkalmazáskészlet** mező mellett válassza ki a 3. lépésben létrehozott alkalmazáskészletet.

8. Az a **fizikai elérési út** mezőben tallózással keresse meg az alkalmazás helyét. Használhatja az alapértelmezett helyet: %windir%/Web/PowerShellWebAccess/wwwroot. Kattintson az **OK** gombra.

9. Az SSL-tanúsítvány konfigurálása IIS manager](#to-configure-an-ssl-certificate-in-iis-Manager) ebben a témakörben szereplő eljárás lépéseit kövesse.

10. ![](images/SecurityNote.jpeg) Nem kötelező biztonsági lépés:

    A webhelyet a fát megjelenítő ablaktáblán kattintson duplán a **SSL-beállítások** a tartalompanelen.
Válassza ki **SSL megkövetelése**, majd a **műveletek** ablaktáblában kattintson **alkalmaz**.
Nem kötelező a **SSL-beállítások** ablaktáblán megkövetelheti, hogy a Windows PowerShell Web Access webhely csatlakozó felhasználók rendelkezzenek ügyféltanúsítványokkal. Az ügyféltanúsítványok segítségével ellenőrizheti az ügyféleszközök felhasználóinak identitását.
Hogyan Ügyféltanúsítványok megkövetelése hogy növelni a Windows PowerShell Web Access biztonsági kapcsolatos további információkért lásd: [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md) az útmutatóban.

11. Nyisson meg egy böngésző-munkamenetet egy ügyféleszközön. Támogatott böngészőkkel és eszközökkel kapcsolatos további információkért lásd: [böngészőből, és támogatja az ügyféleszközön](#browser-and-client-device-support) ebben a témakörben.

12. Nyissa meg az új Windows PowerShell Web Access webhely **https://\<*átjáró kiszolgálónév*\>/pswa**.

    A böngésző megjelenjen-e a Windows PowerShell Web Access konzol bejelentkezési oldal.

    >**![Megjegyzés:](images/note.jpeg) Megjegyzés**
    >
    >Addig nem jelentkezhet be, amíg engedélyezési szabályok hozzáadásával nem biztosít hozzáférést a felhasználók számára a webhelyhez.
    >További információkért lásd: [korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule), ebben a témakörben és [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

13. Egy emelt szintű felhasználói jogosultságokkal (Futtatás rendszergazdaként) megnyitott Windows PowerShell-munkamenetben futtassa a következő parancsfájlt, amelyben *application_pool_name* a 3. lépésben létrehozott alkalmazáskészlet nevét jelöli a adjon az alkalmazáskészletnek a hitelesítési fájlhoz hozzáférési jogosultsága.

        $applicationPoolName = "<application_pool_name>"
        $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
        c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null

    Futtassa a következő parancsot a meglévő hozzáférési jogosultságok megtekintéséhez az engedélyezési fájlon:

        c:\windows\system32\icacls.exe $authorizationFile

#### <a name="to-use-iis-manager-to-configure-the-gateway-as-a-root-website-with-a-test-certificate"></a>Az IIS-kezelő használata az átjáró gyökérwebhelyként való konfigurálásához teszttanúsítvány segítéségével

1. Nyissa meg az IIS-kezelő konzolját a következő módszerek valamelyikével.

    - A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán. Az a **eszközök** a Kiszolgálókezelő menüjében kattintson **Internet Information Services (IIS) Manager**.

    - A Windows **Start** írja be a nevek **Internet Information Services (IIS) Manager**. Kattintson a parancsikonra, amikor az megjelenik a **alkalmazások** eredmények.

2. Az IIS-kezelő fát megjelenítő ablaktáblán, bontsa ki a csomópontot, a kiszolgáló, amelyen a Windows PowerShell Web Access telepítve van, amíg a **helyek** mappa meg nem jelenik. Válassza ki a **helyek** mappát.

3. Az a **műveletek** ablaktáblán kattintson a **webhely hozzáadása**.

4. Írjon be egy nevet a webhelyhez, például **Windows PowerShell Web Access**.

5. A rendszer automatikusan létrehoz egy alkalmazáskészletet az új webhelyhez. Másik alkalmazáskészlet használatához kattintson **válasszon** az új webhelyhez társítandó alkalmazáskészlet kiválasztásához. Válassza ki a másik alkalmazáskészletet az a **alkalmazáskészlet kiválasztása** párbeszédpanel, és kattintson **OK**.

6. Az a **fizikai elérési út** szöveg navigáljon a %*windir*wwwroot % / webes/PowerShellWebAccess.

7. Az a **típus** mezőjét a **kötés** területen válassza **https**.

8. Rendeljen hozzá egy más hely vagy alkalmazás által még nem használt portszámot a webhelyhez. Megnyitott portok megkereséséhez futtathatja a **netstat** parancsot egy parancssori ablakot. Az alapértelmezett portszám 443.

    Módosítsa az alapértelmezett portot, ha egy másik webhely már használja a 443-ast, vagy ha egyéb biztonsági okokból módosítani szeretné a portszámot. Ha az átjárókiszolgálón egy másik webhely használja a kiválasztott portot, figyelmeztetés jelenik meg kattintva **OK** a a **webhely hozzáadása** párbeszédpanel megnyitásához. A Windows PowerShell Web Access futtatásához egy nem használt portot kell használnia.

9. Ha a szervezet számára szükséges, megadhat egy állomásnevet, amely a szervezet és a felhasználók, például a **www.contoso.com**. Kattintson az **OK** gombra.

10. A biztonságosabb éles környezet érdekében határozottan javasoljuk egy érvényes, hitelesítésszolgáltató által aláírt tanúsítványt biztosítását. Meg kell adnia egy SSL-tanúsítvány, mert a felhasználók kapcsolódhatnak a Windows PowerShell Web Access csak egy HTTPS-webhelyen. Lásd: [SSL-tanúsítvány konfigurálása az IIS-kezelőben](#to-configure-an-ssl-certificate-in-iis-Manager) tanúsítvány beszerzéséről további információt ebben a témakörben.

11. Kattintson a **OK** bezárásához a **webhely hozzáadása** párbeszédpanel megnyitásához.

12. Egy emelt szintű felhasználói jogosultságokkal (Futtatás rendszergazdaként) megnyitott Windows PowerShell-munkamenetben futtassa a következő parancsfájlt, amelyben *application_pool_name* 4,. lépésben létrehozott alkalmazáskészlet nevét jelöli a adjon az alkalmazáskészletnek a hitelesítési fájlhoz hozzáférési jogosultsága.

        $applicationPoolName = "<application_pool_name>"
        $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
        c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null

    Futtassa a következő parancsot a meglévő hozzáférési jogosultságok megtekintéséhez az engedélyezési fájlon:

        c:\windows\system32\icacls.exe $authorizationFile

13. Az új webhelyet az IIS-kezelő fát megjelenítő ablaktábláján, és kattintson **Start** a a **műveletek** ablaktáblán a webhely elindításához.

14. Nyisson meg egy böngésző-munkamenetet egy ügyféleszközön. Támogatott böngészőkkel és eszközökkel kapcsolatos további információkért lásd: [böngészőből, és támogatja az ügyféleszközön](#browser-and-client-device-support) ebben a dokumentumban.

15. Nyissa meg az új Windows PowerShell Web Access webhely.

    Mivel a gyökérwebhely a Windows PowerShell Web Access mappába, a böngésző megjelenjen-e a Windows PowerShell Web Access bejelentkezési oldal, megnyitásakor **https://\<*átjárókiszolgáló_neve* \>**. Nem kell hozzáadni **/pswa** URL-címét.

    >**![Megjegyzés:](images/note.jpeg) Megjegyzés**
    >
    >Addig nem jelentkezhet be, amíg engedélyezési szabályok hozzáadásával nem biztosít hozzáférést a felhasználók számára a webhelyhez.
    >További információkért lásd: [korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule), ebben a témakörben és [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

### <a name="configure-a-restrictive-authorization-rule"></a>Korlátozó engedélyezési szabály konfigurálása

Miután a Windows PowerShell Web Access telepítve van, és az átjáró, felhasználó meg tudja nyitni a böngészőben a bejelentkezési oldal, de azok nem tud bejelentkezni, amíg a Windows PowerShell Web Access rendszergazdai hozzáférést biztosít a felhasználónak explicit módon. A következő táblázat ismerteti a Windows PowerShell-parancsmagok használatával a Windows PowerShell Web Access hozzáférés-vezérlés kezeli. Engedélyezési szabályok hozzáadásához és kezeléséhez nincs hasonló grafikus felhasználói felület. További részletes információk a Windows PowerShell Web Access parancsmagokról, lásd a parancsmagokkal kapcsolatos témaköröket [Windows PowerShell Web Access parancsmagok](cmdlets/web-access-cmdlets.md).

További információt a Windows PowerShell Web Access engedélyezési szabályairól és biztonságáról lásd: [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="to-add-a-restrictive-authorization-rule"></a>Korlátozó engedélyezési szabály hozzáadása

1. Hajtsa végre az alábbi Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultsággal nyissa meg.

    - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán, és kattintson a **Futtatás rendszergazdaként**.

    - A Windows **Start** kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

2. ![Biztonsági Megjegyzés](images/SecurityNote.jpeg) Opcionális megoldás a felhasználói hozzáférés korlátozására munkamenet-konfigurációk használatával:

    Ellenőrizze, hogy léteznek-e már azok a munkamenet-konfigurációk, amelyeket használni szeretne a szabályokban. Azok rendelkezik még nem jött létre, ha a munkamenet-konfigurációk létrehozásához használja utasításokat [about_Session_Configuration_Files](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_session_configurations).

3. Írja be a következőt, és nyomja le az **Enter**.

        Add-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>

    Ez az engedélyezési szabály lehetővé teszi, hogy a számítógépek egy adott felhasználó hozzáférését a hálózaton, amelyhez általában hozzáférhetnek, egy adott munkamenet-konfiguráció, ami a felhasználó hozzáférést "™ s szokásos parancsfájl-kezelési és parancsmag igényeinek.

    A következő példában a `Contoso` tartomány `JSmith` nevű felhasználója hozzáférést kap a `Contoso_214` számítógép kezeléséhez, és egy `NewAdminsOnly` nevű munkamenet-konfiguráció használatához.

        Add-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly

4. Győződjön meg arról, hogy létrejött-e a szabály futtatásával a `Get-PswaAuthorizationRule` parancsmagot, vagy `Test-PswaAuthorizationRule -UserName '<domain\user>' -ComputerName <computer-name>`.

    Például: `Test-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214`.

Az engedélyezési szabály konfigurálása után készen áll az engedélyezett felhasználók jelentkezzen be a webalapú konzol, és megkezdheti a Windows PowerShell Web Access használatát.

## <a name="configure-a-genuine-certificate"></a>Eredeti tanúsítvány konfigurálása

A biztonságos éles környezethez mindig érvényes, hitelesítésszolgáltató (CA) által aláírt SSL-tanúsítványt használjon. Az ebben a szakaszban leírt eljárás bemutatja, hogyan szerezhet be egy érvényes SSL-tanúsítványt egy hitelesítésszolgáltatótól, valamint hogyan alkalmazhatja azt.

### <a name="to-configure-an-ssl-certificate-in-iis-manager"></a>SSL-tanúsítvány konfigurálása az IIS-kezelőben

1. Az IIS-kezelő fát megjelenítő ablaktáblán válassza ki a kiszolgálót, amelyen telepítve van a Windows PowerShell Web Access.

2. A tartalom ablaktáblában kattintson duplán a **kiszolgálótanúsítványok**.

3. Az a **műveletek** ablaktáblán, tegye a következők valamelyikét. További információ a Kiszolgálótanúsítványok konfigurálása az IIS: [Kiszolgálótanúsítványok konfigurálása az IIS 7](https://technet.microsoft.com/library/cc732230.aspx).

    - Kattintson a **importálása** egy meglévő, érvényes tanúsítvány importálásához a hálózat egy helyéről.

    - Kattintson a **tanúsítványkérelem létrehozása** tanúsítvány kérése a hitelesítésszolgáltatótól, mint [VeriSign](http://www.verisign.com/), [Thawte](https://www.thawte.com/), vagy [GeoTrust](https://www.geotrust.com/). A tanúsítvány köznapi nevének egyeznie kell a kérésben szereplő állomás fejlécével.

      Például, ha az ügyfél böngészője kérelmek http://www.contoso.com/, akkor a köznapi név is meg kell http://www.contoso.com/. Ez a lehetőség a legbiztonságosabb és ajánlott a Windows PowerShell Web Access-átjáró biztosítani a tanúsítványhoz.

    - Kattintson a **önaláírt tanúsítvány létrehozása** egy azonnal használható, és rendelkezik később egy hitelesítésszolgáltató által aláírt szükség tanúsítvány létrehozásához. Adjon meg egy rövid nevet az önaláírt tanúsítvány, például **Windows PowerShell Web Access**. Ez a lehetőség nem tekinthető biztonságosnak, és csak privát tesztkörnyezetben ajánlott.

4. Miután létrehozott vagy beszerzett egy tanúsítványt, válassza ki a webhelyet, amelyhez a tanúsítványt alkalmazni kívánja (például **alapértelmezett webhely**) az IIS-kezelő fát ablaktáblán, és kattintson a **kötések** a a**Műveletek** ablaktáblán.

5. Az a **hely kötésének hozzáadása** párbeszédpanelen adjon hozzá egy **https** kötést a helyhez, ha egy már nem jelenik meg. Ha nem önaláírt tanúsítványt használ, adja meg az eljárás 3. lépésében megadott állomás nevét. Ha önaláírt tanúsítványt használ, ez a lépés nem szükséges.

6. Válassza ki a beszerzett, vagy ez az eljárás 3. lépésében létrehozott tanúsítványt, és kattintson **OK**.

## <a name="using-the-web-based-windows-powershell-console"></a>A webalapú Windows PowerShell konzol használata

Miután a Windows PowerShell Web Access telepítve van, és az átjáró konfigurálásának befejezése ebben a témakörben ismertetett módon, a Windows PowerShell webalapú konzol használatra készen áll. További információ az első lépések a webalapú konzolon, a következő témakörben: [a webes Windows PowerShell konzol használata](use-the-web-based-windows-powershell-console.md).

## <a name="see-also"></a>Lásd még:

- [Internet Information Services (IIS) 7.0 dokumentációja](https://technet.microsoft.com/library/cc753433.aspx)
- [Az IIS-kezelő 7.0 súgó](https://technet.microsoft.com/library/cc732664.aspx)
- [Webkiszolgáló (IIS 7) biztonságának konfigurálása](https://technet.microsoft.com/library/cc731278.aspx)
- [Az IPsec telepítési erőforrásai](https://technet.microsoft.com/network/bb531150)