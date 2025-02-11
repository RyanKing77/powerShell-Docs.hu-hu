---
ms.date: 08/23/2017
keywords: PowerShell, a parancsmag
title: telepítheti és használhatja a windows powershell-elérés
ms.openlocfilehash: 53558f9be5065c7f630f06e535ddab4d7ad72d9e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058578"
---
# <a name="install-and-use-windows-powershell-web-access"></a>Telepítheti és használhatja a Windows PowerShell-Elérésbe

Frissítve: 2013. novemberi 5 (szerkesztett: 2017. augusztus 23.)

A következőkre vonatkozik: Windows Server 2012 R2, Windows Server 2012

## <a name="introduction"></a>Bevezetés

Windows PowerShell-elérés, a Windows Server 2012 rendszerben bevezetett egy Windows PowerShell átjáróként működik, így a webes Windows PowerShell-konzolt, amely egy távoli számítógépre irányul. Lehetővé teszi az informatikai szakemberek egy webböngészőben, nem Windows PowerShell, a távfelügyeleti szoftvereket vagy a böngésző beépülő modul telepítése szükséges az ügyféleszközön, a Windows PowerShell-konzolt a Windows PowerShell-parancsok és szkriptek futtatásához. Szükséges a webes Windows PowerShell-konzol futtatásához csak egy Windows PowerShell-elérés megfelelően konfigurált átjáró és a egy eszköz ügyfélböngészőnek, amely támogatja a JavaScript, és elfogadja a cookie-k.

Ügyféleszközök például laptopokat, munkaidőn kívüli személyi számítógépek, webterminál, táblagépről, webes kioszkok, egy Windows-alapú operációs rendszert, és a mobiltelefonos böngésző nem futtató számítógépeken. Informatikai szakemberek kritikus fontosságú kezelési feladatok végrehajtására a távoli Windows-alapú kiszolgálókon, amely hozzáféréssel rendelkezik internetkapcsolattal és a egy webes böngésző eszközökről.

Átjáró sikeres beállítása és konfigurációja után felhasználók férhetnek hozzá a Windows PowerShell-konzolt egy webböngésző használatával. A biztonságos Windows PowerShell-elérés webhely megnyitásakor a sikeres hitelesítés után futtathatják a webalapú Windows PowerShell-konzolt.

Windows PowerShell-elérés beállítása és konfigurációja egy három lépéses folyamat a következő:

1. [Windows PowerShell-elérés telepítése](#install-windows-powershell-web-access-using-powershell-cmdlets)
1. [Az átjáró konfigurálása](#configure-the-gateway)
1. [Korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule)

Mielőtt telepítése és konfigurálása a Windows PowerShell-elérés, azt javasoljuk, hogy a teljes útmutató, amely telepítésével kapcsolatos utasításokat tartalmazza, biztonságos, és távolítsa el a Windows PowerShell-elérés. A [a webes Windows PowerShell-konzol használata](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831417(v=ws.11)) a témakör azt ismerteti, hogyan jelentkeznek be a webalapú konzol, és a korlátozások és a webes Windows PowerShell-konzol közötti különbségeket ismerteti, és a  **PowerShell.exe** konzolon. Olvassa el a végfelhasználók a webalapú konzol [webalapú Windows PowerShell konzol használata a](use-the-web-based-windows-powershell-console.md), de ez az útmutató további részének olvasása nem szükséges.

Ez a témakör nem ad részletes IIS-webkiszolgáló műveletek útmutatást; Ez a témakör csak azokat a Windows PowerShell-elérés átjáró konfigurálásához szükséges lépéseket ismerteti. Konfigurálásával és webhelyek IIS-ben biztonságossá tételével kapcsolatos további információkért lásd: az IIS dokumentációs forrásanyagait a Lásd még szakaszban.

Az alábbi ábrán látható, hogyan működik a Windows PowerShell-elérés.

![Windows PowerShell-elérés diagramja](images/Windows-PowerShell-Web-Access-diagram.jpg)

## <a name="requirements-for-running-windows-powershell-web-access"></a>Windows PowerShell-elérés futtatásának követelményei

Windows PowerShell-elérés szükséges a webkiszolgáló (IIS), a .NET-keretrendszer 4.5, és a Windows PowerShell 3.0 vagy a Windows PowerShell 4.0-s verzióját a kiszolgálón, amelyen az átjáró futtatása szeretné futtatni. A Windows Server 2012 R2 rendszert futtató kiszolgáló vagy a Windows Server 2012 Windows PowerShell-elérés telepítheti a szerepkörök hozzáadása és a szolgáltatások varázsló a Kiszolgálókezelő vagy a Windows PowerShell telepítési parancsmagok a Kiszolgálókezelő használatával. Windows PowerShell-elérés telepítése a Kiszolgálókezelő vagy a központi telepítési parancsmagok használatával, amikor szükséges szerepkörök és szolgáltatások automatikusan hozzáadódnak a telepítési folyamat részeként.

Windows PowerShell-elérés lehetővé teszi, hogy a távoli felhasználók férhetnek hozzá a szervezetben lévő számítógépeken a Windows PowerShell használatával egy webböngészőben. Habár a Windows PowerShell-elérés egy kényelmes és hatékony kezelőeszköz, a webalapú hozzáférés biztonsági kockázatot is jelent, és így a lehető kell konfigurálni. Azt javasoljuk, hogy a Windows PowerShell-elérés átjárót konfiguráló rendszergazdák számára elérhető biztonsági rétegek használatával, a Parancsmagalapú hitelesítési szabályokat is tartalmazza a Windows PowerShell-elérés és a biztonsági rétegek, a Web Server) Az IIS) és harmadik féltől származó alkalmazások. Ez a dokumentáció tartalmaz mindkét nem biztonságos példa csak tesztkörnyezetekhez ajánlott konfigurációkra, valamint biztonságos telepítéshez ajánlott.

## <a name="browser-and-client-device-support"></a>Böngésző- és eszköz támogatása

Windows PowerShell-elérés a következő webböngészőket támogatja. Bár a mobilböngészők hivatalosan nem támogatottak, számos lehet képes a webalapú Windows PowerShell-konzol futtatásához.
Más böngészők, amely elfogadja a cookie-kat, JavaScriptet és HTTPS-webhelyeket futtató várható, de hivatalosan nem teszteltük.

### <a name="supported-desktop-computer-browsers"></a>Támogatott asztali számítógépes böngészők

- Windows Internet Explorer alkalmazás Microsoft Windows 8.0, 9.0, 10.0 és 11.0
- Mozilla Firefox 10.0.2
- Google Chrome-17.0.963.56m Windows esetében
- Apple Safari® 5.1.2 Windows
- Apple Safari® 5.1.2 Mac OS

### <a name="minimally-tested-mobile-devices-or-browsers"></a>Minimális tesztelésen átesett mobileszközök és böngészők

- Windows Phone 7 és 7.5
- Google Android WebKit 3.1 böngésző Android 2.2.1-en (Kernel 2.6)
- Apple Safari 5.0.1-es iPhone operációs rendszerhez
- Apple Safari 5.0.1-es iPad 2 operációs rendszerhez

### <a name="browser-requirements"></a>Webböngészőkre vonatkozó követelmények

A Windows PowerShell-elérés webalapú konzol használatához böngészők a következőket kell tennie.

- Cookie-k a Windows PowerShell-elérés átjáró webhelyéről.
- Tudni megnyitása és olvasása a HTTPS-lapok.
- Nyissa meg, és futtassa a JavaScriptet használó webhelyek.

## <a name="recommended-quick-deployment"></a>Gyors üzembe helyezés javasolt

Telepíthető a Windows PowerShell-elérés átjáró egy kiszolgálót, amelyen fut a Windows Server 2012 R2 vagy Windows Server 2012 vagy Windows PowerShell-parancsmagok használatával, illetve a szerepkörök hozzáadása és megnyitott a Kiszolgálókezelőben a szolgáltatások varázsló használatával. A gyors telepítéshez és konfigurációs Windows PowerShell-parancsmag használatával ebben a szakaszban leírtak szerint.

1. [Windows PowerShell-elérés telepítése](#install-windows-powershell-web-access-using-powershell-cmdlets)
1. [Az átjáró konfigurálása](#configure-the-gateway)
1. [Korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule)

### <a name="install-windows-powershell-web-access-using-powershell-cmdlets"></a>Windows PowerShell-parancsmagok használatával PowerShell-elérés telepítése

#### <a name="to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets"></a>Windows PowerShell-elérés telepítése a Windows PowerShell-parancsmagok használatával

1. Hajtsa végre az alábbi lépéseket egy Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultsággal nyissa meg.

   - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán, és kattintson a **Futtatás rendszergazdaként**.
   - A Windows a **Start** kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

   > [!NOTE]
   > A Windows PowerShell 3.0 és 4.0-s verzióját van, nem szükséges importálni a Kiszolgálókezelő-parancsmagokat a Windows PowerShell-munkamenetbe, amely a modul részét képező parancsmagok futtatása előtt. A modul a rendszer automatikusan importál a modul részét képező parancsmag első futtatásakor.
   > Emellett Windows PowerShell-parancsmagok nem különböznek.

1. Írja be a következőt, majd nyomja le **Enter**, ahol *számítógép_neve* jelöli egy távoli számítógépen, amelyen szeretné telepíteni a Windows PowerShell-elérés, ha van ilyen. A `-Restart` paraméter automatikusan újraindítja a célkiszolgálót, ha szükséges.

   `Install-WindowsFeature -Name WindowsPowerShellWebAccess -ComputerName <computer_name> -IncludeManagementTools -Restart`

   > [!NOTE]
   > Windows PowerShell-elérés telepítése a Windows PowerShell-parancsmagok használatával nem ad hozzá webkiszolgáló (IIS) felügyeleti eszközök alapértelmezés szerint. Ha szeretné telepíteni a kezelőeszközöket ugyanarra a kiszolgálóra, mint a Windows PowerShell-elérés átjáró, vegye fel a `-IncludeManagementTools` paramétert a telepítési parancshoz (ebben a lépésben ismertetett). Ha a Windows PowerShell-elérés webhely egy távoli számítógépről kezeli, telepítse az IIS-kezelő beépülő modul telepítésével [távoli kiszolgáló felügyeleti eszközei a Windows 8.1](https://www.microsoft.com/en-us/download/details.aspx?id=39296) vagy [távoli kiszolgáló felügyelete A Windows 8 rendszerű eszközök](https://www.microsoft.com/en-us/download/details.aspx?id=28972) azon a számítógépen, amelyről szeretné az átjáró felügyeletére.

   Telepítése a szerepkörök és szolgáltatások offline virtuális merevlemezen, hozzá kell adnia mind a `-ComputerName` paraméter és a `-VHD` paraméter. A `-ComputerName` paraméter, amelyhez csatlakoztatni kívánja a VHD-t, a kiszolgáló nevét tartalmazza, és a `-VHD` paraméter tartalmazza a megadott kiszolgálón a VHD-fájl elérési útját.

   `Install-WindowsFeature -Name WindowsPowerShellWebAccess -VHD <path> -ComputerName <computer_name> -IncludeManagementTools -Restart`

1. Ha a telepítés befejeződött, ellenőrizze, amelyen Windows PowerShell-elérés telepítve lett a célkiszolgálókon futtatásával a `Get-WindowsFeature` parancsmagot a célkiszolgálón, amely a megnyitott Windows PowerShell-konzolban, emelt szintű felhasználói jogosultságokkal. Azt is ellenőrizheti, hogy Windows PowerShell-elérés telepítése a Server Manager konzolon válassza a célkiszolgálóra a a **minden kiszolgáló** lapot, és tekintse a **szerepkörök és szolgáltatások** a kiválasztott kiszolgálóhoz tartozó csempe. A Windows PowerShell-elérés az információs fájl is megtekintheti.

1. Windows PowerShell-elérés telepítése után a rendszer kéri, tekintse át az információs fájl, amely az átjáró alapvető és szükséges beállítási utasításait tartalmazza. A telepítő az utasítások is megtalálhatók a következő szakaszban [az átjáró konfigurálásához](#configure-the-gateway). Az információs fájl elérési útja `C:\Windows\Web\PowerShellWebAccess\wwwroot\README.txt`.

### <a name="configure-the-gateway"></a>Az átjáró konfigurálása

A **Install-PswaWebApplication** parancsmag egy gyors módja Windows PowerShell webes elérés konfigurálva. Bár hozzáadhatja a `UseTestCertificate` paramétert a `Install-PswaWebApplication` parancsmagot, hogy a teszt önaláírt SSL-tanúsítvány telepítése célra használja, ez a nem biztonságos, a biztonságos éles környezethez mindig használja, amely által aláírt érvényes SSL-tanúsítványt egy hitelesítésszolgáltató (CA). A rendszergazdák az IIS-kezelő konzol használatával a tesztcélú tanúsítványt lecserélheti egy tetszőleges aláírt tanúsítványra.

Webalkalmazás konfigurációjának Windows PowerShell-elérés futtatásával befejezheti a `Install-PswaWebApplication` parancsmag vagy az IIS-kezelőben GUI-alapú konfigurációs lépések végrehajtásával.
Alapértelmezés szerint a parancsmag telepíti a webalkalmazás **pswa** (és a egy alkalmazáskészlet, **pswa_pool**), a a **Default Web Site** tárolót, az IIS-kezelőben látható módon ha szükség esetén utasíthatja a parancsmagot a webalkalmazás alapértelmezett helytárolójának módosítására. IIS-kezelőben elérhető webes alkalmazásokhoz, például a portszám vagy a Secure Sockets Layer (SSL) tanúsítványt módosítását konfigurációs beállításokat kínál.

> **![Biztonsági megjegyzés](images/securitynote.jpeg) biztonsági megjegyzés** erősen ajánlott beállítani, hogy a rendszergazdák az átjárót egy érvényes, hitelesítésszolgáltató által aláírt tanúsítványt használjon.

#### <a name="to-configure-the-windows-powershell-web-access-gateway-with-a-test-certificate-by-using-install-pswawebapplication"></a>A Windows PowerShell-elérés átjáró konfigurálása egy tesztcélú tanúsítvánnyal az Install-PswaWebApplication használatával

1. Hajtsa végre az alábbi lépéseket egy Windows PowerShell-munkamenetet.

   - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán.
   - A Windows a **Start** kattintson **Windows PowerShell**.

2. Írja be a következőt, majd nyomja le **Enter**.

   `Install-PswaWebApplication -UseTestCertificate`

   > **![Biztonsági megjegyzés](images/securitynote.jpeg) biztonsági megjegyzés** a `UseTestCertificate` paramétert csak privát tesztkörnyezetben használható. A biztonságos éles környezethez használatát javasoljuk egy érvényes, hitelesítésszolgáltató által aláírt tanúsítványt.

   A parancsmag futtatása telepíti a Windows PowerShell-elérés webalkalmazást az IIS alapértelmezett webhely tárolóján belül. A parancsmag létrehoz egy Windows PowerShell-elérés az alapértelmezett webhelyen való futtatásához szükséges infrastruktúrát `https://<server_name>/pswa`. A webalkalmazás egy másik webhelyre történő telepítéséhez adja meg a webhely neve hozzáadásával a `WebSiteName` paraméter. A webalkalmazás nevének módosításához (az alapértelmezett érték `pswa`), adja hozzá a `WebApplicationName` paraméter.

   A következő beállításokat a parancsmag futtatásával konfigurálhatók. Ha megfelelő ezeket manuálisan az IIS-kezelő konzolon módosíthatja.

   - Path: /pswa
   - ApplicationPool: pswa_pool
   - EnabledProtocols: http
   - PhysicalPath: %windir%/Web/PowerShellWebAccess/wwwroot

   **Példa**: `Install-PswaWebApplication -webApplicationName myWebApp -useTestCertificate`

   Ebben a példában az eredményül kapott webhelye a Windows PowerShell-elérés van `https://<server_name>/myWebApp`.

   > [!NOTE]
   > Nem tud bejelentkezni, amíg a felhasználók hozzáférést nyertek a webhelyen az engedélyezési szabályok hozzáadásával. További információkért lásd: [korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule) és [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell-elérés](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="to-configure-the-windows-powershell-web-access-gateway-with-a-genuine-certificate-by-using-install-pswawebapplication-and-iis-manager"></a>A Windows PowerShell-elérés átjáró konfigurálása egy eredeti tanúsítvánnyal Install-PswaWebApplication és IIS-kezelő használatával

1. Hajtsa végre az alábbi lépéseket egy Windows PowerShell-munkamenetet.

   - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán.
   - A Windows a **Start** kattintson **Windows PowerShell**.

2. Írja be a következőt, majd nyomja le **Enter**.

   `Install-PswaWebApplication`

   A következő átjáróbeállítások a parancsmag futtatásával konfigurálhatók. Ha megfelelő ezeket manuálisan az IIS-kezelő konzolon módosíthatja. Az értékeket is megadhat a `WebsiteName` és `WebApplicationName` paramétereit a `Install-PswaWebApplication` parancsmag.

   - Path: /pswa
   - ApplicationPool: pswa_pool
   - EnabledProtocols: http
   - PhysicalPath: %windir%/Web/PowerShellWebAccess/wwwroot

3. Nyissa meg az IIS-kezelő konzol a következő módszerek valamelyikével.

   - A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán. Az a **eszközök** menüjében a Kiszolgálókezelőben kattintson **Internet Information Services (IIS) kezelője**.
   - A Windows a **Start** kattintson **Kiszolgálókezelő**.

4. Az IIS-kezelő fát megjelenítő ablaktábláján, bontsa ki a kiszolgáló, amelyen Windows PowerShell-elérés telepítve van, amíg a csomópont a **helyek** mappa megjelent-e. Bontsa ki a **helyek** mappát.

5. Válassza ki a webhelyet, ahol telepítette a Windows PowerShell-elérés webalkalmazás.
   Az a **műveletek** ablaktáblán kattintson a **kötések**.

6. Az a **hely kötésének** párbeszédpanelen kattintson a **Hozzáadás**.

7. Az a **hely kötésének hozzáadása** párbeszédpanel a **típus** mezőben válassza **https**.

8. Az a **SSL-tanúsítvány** mezőben válassza ki a megfelelő aláírt tanúsítványt a legördülő menüből.
   Kattintson az **OK** gombra. Lásd: [SSL-tanúsítvány konfigurálása az IIS-kezelőben](#to-configure-an-ssl-certificate-in-iis-manager) tanúsítvány beszerzéséről további információt ebben a témakörben.

   A Windows PowerShell-elérés webes alkalmazás most már az aláírt SSL-tanúsítvány használatára van konfigurálva.

   Windows PowerShell-elérés történő megnyitásával is elérheti `https://<server_name>/pswa` egy böngészőablakban.

   > [!NOTE]
   > Nem tud bejelentkezni, amíg a felhasználók hozzáférést nyertek a webhelyen az engedélyezési szabályok hozzáadásával. További információkért lásd: [korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule), ez a témakör és [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell-elérés](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

### <a name="configure-a-restrictive-authorization-rule"></a>Korlátozó engedélyezési szabály konfigurálása

Után a Windows PowerShell-elérés telepítése és az átjáró van konfigurálva, a felhasználó meg tudja nyitni a böngészőben a bejelentkezési oldal, de nem tudnak bejelentkezni mindaddig, amíg a Windows PowerShell-elérés rendszergazdai hozzáférést biztosít a felhasználónak explicit módon. Windows PowerShell-elérés hozzáférés-vezérlés kezeli az alábbi táblázatban ismertetett Windows PowerShell-parancsmagok használatával. Nincs nincs hasonló grafikus felhasználói felület hozzáadásához és kezeléséhez az engedélyezési szabályok. További részletes információ a Windows PowerShell-elérés parancsmagjai, lásd a parancsmagokkal kapcsolatos témaköröket [Windows PowerShell webes elérés parancsmagjai](/powershell/module/powershellwebaccess/?view=winserver2012r2-ps).

Windows PowerShell-elérés engedélyezési szabályai és biztonsági kapcsolatos további részletekért lásd: [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell-elérés](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="to-add-a-restrictive-authorization-rule"></a>Korlátozó engedélyezési szabály hozzáadása

1. Hajtsa végre az alábbi lépéseket egy Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultsággal nyissa meg.

   - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán, és kattintson a **Futtatás rendszergazdaként**.
   - A Windows a **Start** kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

2. Nem kötelező lépés a felhasználói hozzáférés korlátozására munkamenet-konfigurációk használatával: Győződjön meg arról, hogy a munkamenet-konfigurációk, amelyeket szeretne használni a szabályokban már létezik. Ha azok még nem lett hozott, alkalmaznia munkamenet-konfigurációk létrehozására vonatkozó [about_Session_Configuration_Files](/powershell/module/microsoft.powershell.core/about/about_session_configurations).

3. Írja be a következőt, majd nyomja le **Enter**.

   `Add-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>`

   Ez az engedélyezési szabály lehetővé teszi, hogy egy adott felhasználó hozzáférését egy számítógépre a hálózaton, amelyhez általában hozzáférhetnek, hozzáférést egy adott munkamenet-konfiguráció, amely a felhasználó szokásos parancsfájl-kezelési hatókörét, és parancsmag-igényeihez.

   A következő példában egy felhasználó nevű `JSmith` a a `Contoso` tartományi hozzáférést kap a számítógép felügyeletéhez `Contoso_214`, és a egy munkamenet-konfiguráció használata `NewAdminsOnly`.

   `Add-PswaAuthorizationRule -UserName Contoso\JSmith -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly`

4. Győződjön meg arról, hogy az a szabály futtatásával hozták-e a `Get-PswaAuthorizationRule` parancsmagot, vagy `Test-PswaAuthorizationRule -UserName <domain\user> -ComputerName <computer-name>`

   Például: `Test-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214`.

Miután konfigurálta az engedélyezési szabály, készen áll a jogosult felhasználók számára, hogy jelentkezzen be a webalapú konzol, és megkezdheti a használatát a Windows PowerShell-elérés.

## <a name="custom-deployment"></a>Egyéni központi telepítés

Telepítheti a Windows PowerShell-elérés átjáró Windows Server 2012 R2 rendszert futtató kiszolgáló vagy a Windows Server 2012 használatával a adja hozzá szerepkörök és szolgáltatások varázsló a Kiszolgálókezelőben.
Windows PowerShell-elérés telepítése után testreszabhatja az átjáró az IIS-kezelő konfigurációját.

### <a name="install-windows-powershell-web-access-using-the-add-roles-and-features-wizard"></a>Windows adja hozzá szerepkörök és szolgáltatások varázsló PowerShell-elérés telepítése

1. Ha a Kiszolgálókezelő már meg nyitva, folytassa a következő lépéssel. Ha a Kiszolgálókezelő még nem nyitott, nyissa meg a következő módszerek valamelyikével.

   - A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán.
   - A Windows a **Start** kattintson **Kiszolgálókezelő**.

2. Az a **kezelés** menüben kattintson a **szerepkörök és szolgáltatások hozzáadása**.

3. A **Telepítés típusának kiválasztása** lapon kattintson a **Szerepköralapú vagy szolgáltatásalapú telepítés** elemre.
   Kattintson a **Tovább** gombra.

4. Az a **célkiszolgáló kijelölése** oldalon válassza ki a kiszolgálót a kiszolgálókészletből, vagy offline VHD kiválasztásához. Offline VHD célkiszolgálóként kiválasztásához először válassza ki a kiszolgálót, amelyhez csatlakoztatni kívánja a VHD-t, és válassza ki a VHD-fájlt. Kiszolgálók a kiszolgálókészlethez adásával kapcsolatos információkért tekintse meg a Kiszolgálókezelő segítségével. Miután kiválasztotta a célkiszolgálón, kattintson a **tovább**.

5. A a **jellemzőket** lapon bontsa ki a varázsló **Windows PowerShell**, majd válassza ki **Windows PowerShell-elérés**.

6. Vegye figyelembe, hogy szükséges szolgáltatások, például a .NET-keretrendszer 4.5 és a webkiszolgáló (IIS) szerepkör-szolgáltatások hozzáadását kéri. Szükséges szolgáltatások hozzáadását, és továbbra is.

   > [!NOTE]
   > Windows PowerShell-elérés telepítése a szerepkörök hozzáadása és a szolgáltatások varázsló használatával is telepíti a webkiszolgáló (IIS), beleértve az IIS-kezelő beépülő modulban. A beépülő modul és egyéb IIS felügyeleti eszközöket települnek alapértelmezés szerint adja hozzá szerepkörök és szolgáltatások varázsló használatakor. Ha a Windows PowerShell-elérés telepítése a Windows PowerShell-parancsmagok használatával, az alábbi eljárásban leírtak szerint, felügyeleti eszközöket nem adódnak alapértelmezés szerint.

7. Az a **telepítendő összetevők megerősítése** lapon, ha a szolgáltatásfájlok Windows PowerShell-elérés nem tárolódnak a 4. lépésben kiválasztott célkiszolgálón kattintson **adjon meg egy alternatív forrásútvonal**, és adja meg a szolgáltatásfájlok elérési útját. Ellenkező esetben kattintson a **telepítése**.

8. Miután rákattintott **telepítése**, a **telepítési folyamat** lap megjeleníti a telepítés folyamatát, eredményeit és üzeneteket a figyelmeztetésekkel, vagy a telepítés utáni konfigurációs lépésekkel, amelyek például Windows PowerShell-elérés számára szükséges. Windows PowerShell-elérés telepítése után a rendszer kéri, tekintse át az információs fájl, amely az átjáró alapvető és szükséges beállítási utasításait tartalmazza. Ezek az utasítások is megtalálhatók ebben a témakörben. Az információs fájl elérési útja `C:\Windows\Web\PowerShellWebAccess\wwwroot\README.txt`.

### <a name="configure-the-gateway"></a>Az átjáró konfigurálása

Jelen szakaszban található útmutatásokat is telepíthető a Windows PowerShell-elérés webalkalmazás alkönyvtárban és nem az a webhely gyökérkönyvtárában. Ez az eljárás akkor által végrehajtott műveletek GUI-alapú megfelelője a `Install-PswaWebApplication` parancsmagot. Ez a szakasz az IIS-kezelő segítségével konfigurálhatja a Windows PowerShell-elérés átjáró gyökérwebhelyként vonatkozó utasításokat is tartalmaz.

#### <a name="to-use-iis-manager-to-configure-the-gateway-in-an-existing-website"></a>Az IIS-kezelő használata az átjáró konfigurálása egy meglévő webhelyen

1. Nyissa meg az IIS-kezelő konzol a következő módszerek valamelyikével.

   - A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán. Az a **eszközök** menüjében a Kiszolgálókezelőben kattintson **Internet Information Services (IIS) kezelője**.
   - A Windows a **Start** írja be a nevének bármelyik részét **Internet Information Services (IIS) kezelője**. Kattintson a parancsikonra, amikor az megjelenik a **alkalmazások** eredményeket.

2. Hozzon létre egy új alkalmazáskészletet a Windows PowerShell-elérés. Bontsa ki az IIS-kezelő fát megjelenítő ablaktábláján, válassza az átjárókiszolgáló csomópontját **alkalmazáskészletek**, és kattintson a **alkalmazáskészlet hozzáadása** a a **műveletek** ablaktáblán.

3. Adjon hozzá egy új alkalmazáskészlet nevű **pswa_pool**, vagy adjon meg egy másik nevet. Kattintson az **OK** gombra.

4. Az IIS-kezelő fát megjelenítő ablaktábláján, bontsa ki a kiszolgáló, amelyen Windows PowerShell-elérés telepítve van, amíg a csomópont a **helyek** mappa megjelent-e. Válassza ki a **helyek** mappát.

5. Kattintson a jobb gombbal a webhelyet (például **Default Web Site**), szeretné a Windows PowerShell-elérés webhely hozzáadása, és kattintson a **alkalmazás hozzáadása**.

6. Az a **Alias** mezőbe írja be a pswa, vagy adjon meg egy másik aliast. Az alias lesz a virtuális könyvtár neve. Ha például **pswa** a következő URL-címet az ebben a lépésben aliast jelenti: `https://<server-name>/pswa`.

7. Az a **alkalmazáskészlet** mezőben válassza ki a 3. lépésben létrehozott alkalmazáskészletet.

8. Az a **fizikai elérési út** mezőben tallózással keresse meg az alkalmazás helyét. Használhatja az alapértelmezett hely `$env:windir/Web/PowerShellWebAccess/wwwroot`. Kattintson az **OK** gombra.

9. Az eljárás lépéseit kövesse [SSL-tanúsítvány konfigurálása az IIS-kezelőben](#to-configure-an-ssl-certificate-in-iis-manager) ebben a témakörben.

10. ![](images/SecurityNote.jpeg) Nem kötelező biztonsági lépés:

    A fát megjelenítő ablaktáblán ki a webhelyet, majd kattintson duplán **SSL-beállítások** a tartalompanelen.
    Válassza ki **SSL megkövetelése**, majd a **műveletek** ablaktáblán kattintson a **alkalmaz**. Ha szükséges, az a **SSL-beállítások** ablaktáblán megkövetelheti, hogy a Windows PowerShell-elérés webhely csatlakozó felhasználók rendelkezzenek ügyféltanúsítványokkal. Az ügyféltanúsítványok segítségével ellenőrizheti az ügyféleszközök felhasználóinak identitását. Hogyan Ügyféltanúsítványok megkövetelése növelni a Windows PowerShell-elérés biztonságának kapcsolatos további információkért lásd: [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell-elérés](authorization-rules-and-security-features-of-windows-powershell-web-access.md) ebben az útmutatóban.

11. Nyissa meg a böngésző-munkamenetet egy ügyféleszközön. Támogatott böngészőkkel és eszközökkel kapcsolatos további információkért lásd: [böngészőt, és támogatja az ügyféleszközön](#browser-and-client-device-support) ebben a témakörben.

12. Nyissa meg az új Windows PowerShell-elérés webhely **https://\<*átjáró kiszolgálónév*\>/pswa**.

    A böngészőben a Windows PowerShell-elérés konzol bejelentkezési oldal megjelenjen.

    > [!NOTE]
    > Nem tud bejelentkezni, amíg a felhasználók hozzáférést nyertek a webhelyen az engedélyezési szabályok hozzáadásával. További információkért lásd: [korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule), ez a témakör és [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell-elérés](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

13. Egy emelt szintű felhasználói jogosultságokkal (Futtatás rendszergazdaként) megnyitott Windows PowerShell-munkamenetben futtassa a következő parancsfájlt, amelyben *application_pool_name* a 3. lépésben létrehozott alkalmazáskészlet nevét jelöli hogy az alkalmazáskészlet hozzáférési jogokat a hitelesítési fájlhoz.

    ```powershell
    $applicationPoolName = "<application_pool_name>"
    $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
    c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null
    ```

    Meglévő hozzáférési jogosultságok megtekintéséhez az engedélyezési fájlon, futtassa a következő parancsot:

    ```powershell
    c:\windows\system32\icacls.exe $authorizationFile
    ```

#### <a name="to-use-iis-manager-to-configure-the-gateway-as-a-root-website-with-a-test-certificate"></a>Az IIS-kezelő használata az átjáró konfigurálásához teszttanúsítvány gyökérwebhelyként

1. Nyissa meg az IIS-kezelő konzol a következő módszerek valamelyikével.

   - A Windows asztalon indítsa el a Kiszolgálókezelőt kattintva **Kiszolgálókezelő** a Windows tálcán. Az a **eszközök** menüjében a Kiszolgálókezelőben kattintson **Internet Information Services (IIS) kezelője**.
   - A Windows a **Start** írja be a nevének bármelyik részét **Internet Information Services (IIS) kezelője**. Kattintson a parancsikonra, amikor az megjelenik a **alkalmazások** eredményeket.

1. Az IIS-kezelő fát megjelenítő ablaktábláján, bontsa ki a kiszolgáló, amelyen Windows PowerShell-elérés telepítve van, amíg a csomópont a **helyek** mappa megjelent-e. Válassza ki a **helyek** mappát.

1. Az a **műveletek** ablaktáblán kattintson a **webhely hozzáadása**.

1. Írja be például a webhely nevét **Windows PowerShell-elérés**.

1. Egy alkalmazáskészlet automatikusan létrejön az új webhelyhez. Másik alkalmazáskészlet használatához kattintson **kiválasztása** az új webhelyhez társítandó alkalmazáskészlet kiválasztásához. Válassza ki a másik alkalmazáskészletet az a **alkalmazáskészlet kiválasztása** párbeszédpanel, és kattintson **OK**.

1. Az a **fizikai elérési út** szöveg gombra, lépjen a % windir%/Web/PowerShellWebAccess/wwwroot.

1. Az a **típus** mezőjében a **kötés** területen válassza **https**.

1. Egy portszám hozzárendelése a webhelyet, amely még nincs egy másik webhely vagy alkalmazás használja.
   Megnyitott portok megkereséséhez futtathatja a **netstat** parancsot egy parancssori ablakot. Az alapértelmezett portszám 443-as porton.

   Ha egy másik webhely már használja a 443-as, vagy ha egyéb biztonsági okokból módosítani szeretné a portnak a számát, módosítsa az alapértelmezett portot. Ha az átjárókiszolgálón egy másik webhely használja a kiválasztott portot, figyelmeztetés jelenik meg kattintva **OK** a a **webhely hozzáadása** párbeszédpanel bezárásához. Windows PowerShell-elérés futtatásához egy nem használt portot kell használnia.

1. Ha a szervezet számára szükséges, megadhat egy állomásnevet, amely logikus a szervezet és a felhasználó számára, mint például **`www.contoso.com`**. Kattintson az **OK** gombra.

1. A biztonságosabb éles környezetben javasoljuk, hogy egy érvényes, hitelesítésszolgáltató által aláírt tanúsítványt biztosít. SSL-tanúsítványt kell megadnia, mivel a felhasználók csak a Windows PowerShell-elérés keresztül kapcsolódhatnak egy HTTPS-webhelyen. Lásd: [SSL-tanúsítvány konfigurálása az IIS-kezelőben](#to-configure-an-ssl-certificate-in-iis-manager) tanúsítvány beszerzéséről további információt ebben a témakörben.

1. Kattintson a **OK** gombra kattintva zárja be a **webhely hozzáadása** párbeszédpanel bezárásához.

1. Egy emelt szintű felhasználói jogosultságokkal (Futtatás rendszergazdaként) megnyitott Windows PowerShell-munkamenetben futtassa a következő parancsfájlt, amelyben _application_pool_name_ a 4. lépésben létrehozott alkalmazáskészlet nevét jelöli hogy az alkalmazáskészlet hozzáférési jogokat a hitelesítési fájlhoz.

   ```powershell
   $applicationPoolName = "<application_pool_name>"
   $authorizationFile = "C:\windows\web\powershellwebaccess\data\AuthorizationRules.xml"
   c:\windows\system32\icacls.exe $authorizationFile /grant ('"' + "IIS AppPool\$applicationPoolName" + '":R') > $null
   ```

   Meglévő hozzáférési jogosultságok megtekintéséhez az engedélyezési fájlon, futtassa a következő parancsot:

   ```powershell
   c:\windows\system32\icacls.exe $authorizationFile
   ```

1. Az új webhelyet az IIS-kezelő fát megjelenítő ablaktábláján kiválasztva, kattintson a **Start** a a **műveletek** ablaktáblán a webhely elindításához.

1. Nyissa meg a böngésző-munkamenetet egy ügyféleszközön. Támogatott böngészőkkel és eszközökkel kapcsolatos további információkért lásd: [böngészőt, és támogatja az ügyféleszközön](#browser-and-client-device-support) ebben a dokumentumban.

1. Nyissa meg az új Windows PowerShell-elérés webhely.

   Mivel a webhely a Windows PowerShell-elérés mappára mutat, a böngésző kell megjelenítenie a bejelentkezési oldal Windows PowerShell-elérés megnyitásakor `https://<gateway_server_name>`. Nem kell hozzáadni **/pswa** az URL-címre.

   > [!NOTE]
   > Nem tud bejelentkezni, amíg a felhasználók hozzáférést nyertek a webhelyen az engedélyezési szabályok hozzáadásával. További információkért lásd: [korlátozó engedélyezési szabály konfigurálása](#configure-a-restrictive-authorization-rule), ez a témakör és [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell-elérés](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

### <a name="configuring-a-restrictive-authorization-rule"></a>Korlátozó engedélyezési szabály konfigurálása

Után a Windows PowerShell-elérés telepítése és az átjáró van konfigurálva, a felhasználó meg tudja nyitni a böngészőben a bejelentkezési oldal, de nem tudnak bejelentkezni mindaddig, amíg a Windows PowerShell-elérés rendszergazdai hozzáférést biztosít a felhasználónak explicit módon. Windows PowerShell-elérés hozzáférés-vezérlés kezeli az alábbi táblázatban ismertetett Windows PowerShell-parancsmagok használatával. Nincs nincs hasonló grafikus felhasználói felület hozzáadásához és kezeléséhez az engedélyezési szabályok. További részletes információ a Windows PowerShell-elérés parancsmagjai, lásd a parancsmagokkal kapcsolatos témaköröket [Windows PowerShell webes elérés parancsmagjai](/powershell/module/powershellwebaccess/?view=winserver2012r2-ps).

Windows PowerShell-elérés engedélyezési szabályai és biztonsági kapcsolatos további részletekért lásd: [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell-elérés](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

#### <a name="adding-a-restrictive-authorization-rule"></a>Korlátozó engedélyezési szabály hozzáadása

1. Hajtsa végre az alábbi lépéseket egy Windows PowerShell-munkamenetet emelt szintű felhasználói jogosultsággal nyissa meg.

   - A Windows asztalon kattintson a jobb gombbal **Windows PowerShell** a tálcán, és kattintson a **Futtatás rendszergazdaként**.
   - A Windows a **Start** kattintson a jobb gombbal **Windows PowerShell**, és kattintson a **Futtatás rendszergazdaként**.

1. ![Biztonsági Megjegyzés](images/SecurityNote.jpeg) Nem kötelező lépés a felhasználói hozzáférés korlátozására munkamenet-konfigurációk használatával:

   Győződjön meg arról, hogy a munkamenet-konfigurációk, amelyeket szeretne használni a szabályokban már létezik. Ha azok még nem lett hozott, alkalmaznia munkamenet-konfigurációk létrehozására vonatkozó [about_Session_Configuration_Files](/powershell/module/microsoft.powershell.core/about/about_session_configurations).

1. Írja be a következőt, majd nyomja le **Enter**.

   `Add-PswaAuthorizationRule -UserName <domain\user | computer\user> -ComputerName <computer_name> -ConfigurationName <session_configuration_name>`

   Ez az engedélyezési szabály lehetővé teszi egy adott felhasználó hozzáférését egy adott számítógépre a hálózaton, amelyhez általában van hozzáférése egy adott munkamenet-konfiguráció, ami a felhasználói hozzáférést a(z)™ s tipikus parancsfájl-kezelési és parancsmag-igényeihez.

   A következő példában egy felhasználó nevű `JSmith` a a `Contoso` tartományi hozzáférést kap a számítógép felügyeletéhez `Contoso_214`, és a egy munkamenet-konfiguráció használata `NewAdminsOnly`.

   `Add-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214 -ConfigurationName NewAdminsOnly`

1. Győződjön meg arról, hogy az a szabály futtatásával hozták-e a `Get-PswaAuthorizationRule` parancsmagot, vagy `Test-PswaAuthorizationRule -UserName '<domain\user>' -ComputerName <computer-name>`.

   Például: `Test-PswaAuthorizationRule -UserName 'Contoso\JSmith' -ComputerName Contoso_214`.

   Miután konfigurálta az engedélyezési szabály, készen áll a jogosult felhasználók számára, hogy jelentkezzen be a webalapú konzol, és megkezdheti a használatát a Windows PowerShell-elérés.

## <a name="configure-a-genuine-certificate"></a>Eredeti tanúsítvány konfigurálása

A biztonságos éles környezethez mindig használja, a hitelesítésszolgáltató (CA) által aláírt érvényes SSL-tanúsítványt. Ebben a szakaszban az eljárás ismerteti, hogyan lehet beszerzése és a alkalmazni egy érvényes SSL-tanúsítványt a Hitelesítésszolgáltatótól.

### <a name="to-configure-an-ssl-certificate-in-iis-manager"></a>SSL-tanúsítvány konfigurálása az IIS-kezelőben

1. Az IIS-kezelő fát megjelenítő ablaktáblán válassza ki a kiszolgálót, amelyen telepítve van a Windows PowerShell-elérés.

1. A tartalom ablaktáblában kattintson duplán a **kiszolgálói tanúsítványok**.

1. Az a **műveletek** ablaktáblán, tegye a következők egyikét. Kiszolgálótanúsítványok konfigurálása az IIS-ben kapcsolatos további információkért lásd: [Kiszolgálótanúsítványok konfigurálása az IIS 7](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732230(v=ws.10)).

   - Kattintson a **importálása** egy meglévő, érvényes tanúsítvány importálásához a hálózat egy helyéről.
   - Kattintson a **tanúsítványkérelem létrehozása** tanúsítvány kérése hitelesítésszolgáltatótól például [VeriSign](https://www.verisign.com/), [Thawte](https://www.thawte.com/), vagy [GeoTrust](https://www.geotrust.com/). A tanúsítvány köznapi nevének egyeznie kell a kérelemben szereplő állomás fejlécével.

     Például, ha az ügyfél böngészője kérelmek `http://www.contoso.com/`, akkor a köznapi név is meg kell `http://www.contoso.com/`. Ez a lehetőség a legbiztonságosabb és ajánlott a Windows PowerShell-elérés átjáró-tanúsítvánnyal, amelyek biztosítják.

   - Kattintson a **önaláírt tanúsítvány létrehozása** , hozzon létre egy tanúsítványt, hogy azonnal használható, és később aláírhat egy hitelesítésszolgáltató Ha szükséges. Adjon meg egy rövid nevet az önaláírt tanúsítvány, például **Windows PowerShell-elérés**. Ez a beállítás nem tekinthető biztonságosnak, és csak privát tesztkörnyezetben ajánlott.

1. Miután létrehozott vagy beszerzett egy tanúsítványt, válassza ki a webhelyet, amelyhez a tanúsítványt alkalmazni kívánja (például **Default Web Site**) az IIS-kezelő fát ablaktáblán, és kattintson a **kötések** a a**Műveletek** ablaktáblán.

1. Az a **hely kötésének hozzáadása** párbeszédpanelen adjon hozzá egy **https** kötést a helyhez, ha egy már nem jelenik meg. Ha nem önaláírt tanúsítványt használ, adja meg az eljárás 3. lépésében megadott állomás nevét. Ha önaláírt tanúsítványt használ, ezt a lépést, nem szükséges.

1. Válassza ki a kapott, vagy ez az eljárás 3. lépésében létrehozott tanúsítványt, és kattintson **OK**.

## <a name="using-the-web-based-windows-powershell-console"></a>A webes Windows PowerShell-konzol használatával

Miután a Windows PowerShell-elérés telepítése és az átjáró konfigurációja befejeződött ebben a témakörben ismertetett módon, a webes Windows PowerShell konzol használatra készen áll. További információ az első lépések a webalapú konzolon, lásd: [a webes Windows PowerShell-konzol használata](use-the-web-based-windows-powershell-console.md).

## <a name="see-also"></a>Lásd még:

[Az Internet Information Services (IIS) 7.0 dokumentációja](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753433(v=ws.10))

[Az IIS-kezelő 7.0 súgó](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732664(v=ws.11))

[Webkiszolgáló (IIS 7) biztonságának konfigurálása](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731278(v=ws.10))

[Az IPsec telepítési erőforrásai](/previous-versions/windows/it-pro/windows-server-2003/cc776369(v=ws.10))
