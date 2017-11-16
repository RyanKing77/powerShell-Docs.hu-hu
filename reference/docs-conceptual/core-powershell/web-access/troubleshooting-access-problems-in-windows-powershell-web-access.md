---
ms.date: 2017-08-23
keywords: PowerShell parancsmag
title: "a windows powershell web access hozzáférési problémák elhárítása"
ms.openlocfilehash: 08a9fd286ed8a40e9423deb7d29dc0a8ecf8e5b1
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/31/2017
---
# <a name="troubleshooting-access-problems-in-windows-powershell-web-access"></a>Hozzáférési problémák hibaelhárítása a Webes Windows PowerShell-elérésben

Frissítés: Június 24, 2013 (módosított 2017. augusztus 23.)

Vonatkozik: Windows Server 2012 R2, Windows Server 2012-ben

A következő szakaszok olyan gyakori problémákat azonosítása, a Windows PowerShell Web Access használatával kapcsolódik egy távoli számítógépen, és javaslatokat is kínál a problémák.

## <a name="sign-in-failure"></a>Bejelentkezési hiba

A hiba oka a következők bármelyike lehet.

- Hiányzik egy olyan engedélyezési szabály, amely lehetővé tenné a felhasználónak a számítógép hozzáférését vagy hiányzik egy adott munkamenet-konfiguráció a távoli számítógépen.

  A Windows PowerShell Web Access biztonsági érték korlátozó; felhasználókhoz kifejezett hozzáférést távoli számítógépekhez engedélyezési szabályok segítségével kell kell rendelni.

  Az engedélyezési szabályok létrehozásával kapcsolatos további információkért lásd: [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell Web Access](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

- A felhasználó rendelkezik engedélyezett hozzáféréssel a célszámítógéphez. A hozzáférést a hozzáférés-vezérlési listák (access control list, ACL) határozzák meg.

  További információkért lásd: [bejelentkezés a Windows PowerShell Web Access](use-the-web-based-windows-powershell-console.md#signing-in-to-windows-powershell-web-access), vagy a Windows PowerShell csapatának blogját.

- Előfordulhat, hogy a célszámítógépen nincs engedélyezve távoli felügyelet a Windows PowerShell.

  Ellenőrizze a távoli felügyelet engedélyezve van a számítógépen, amelyre a felhasználó csatlakozni próbál.

  További információkért lásd: [hogyan konfigurálhatja a számítógép a távoli eljáráshívás](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_requirements#how-to-configure-your-computer-for-remoting).

## <a name="internal-server-error"></a>Belső kiszolgálóhiba.

Amikor a felhasználó próbál bejelentkezni a Windows PowerShell Web Access egy Internet Explorer-ablakban, megtekinthető egy **belső kiszolgálóhiba** lapon vagy *Internet Explorer* nem válaszol.

Ez a hiba csak az Internet Explorerben fordul elő.

### <a name="possible-cause"></a>Lehetséges ok

Olyan felhasználóknál jelentkezhet, akik kínai karaktereket használó tartománynévvel jelentkeztek be, vagy akiknél az átjárókiszolgáló neve kínai karaktereket tartalmaz.

#### <a name="workaround"></a>Megkerülő megoldás

1. [Telepítheti és futtathatja az Internet Explorer 10](http://ie.microsoft.com/testdrive/info/downloads/Default.html)
1. Módosítsa az Internet Explorer **dokumentum-üzemmód** beállítást *IE10* szabványoknak.
   1. Nyomja le az **F12** a fejlesztői eszközök konzol megnyitása
   1. Kattintson az Internet Explorer 10 **böngésző üzemmódja**, majd válassza ki *Internet Explorer 10*.
   1. Kattintson a **dokumentum-üzemmód**, és kattintson a *IE10* szabványoknak.
   1. Nyomja le az **F12** a fejlesztői eszközök konzol bezárásához.
1. Tiltsa le az Internet Explorer 10 automatikus proxybeállítást.
   1. Kattintson a **eszközök**, és kattintson a **Internetbeállítások**.
   1. Az a **Internetbeállítások** párbeszédpanel a **kapcsolatok** lapra, majd **LAN-beállítások**.
   1. Törölje a jelet a **beállítások automatikus észlelése** jelölőnégyzetet. Kattintson a **OK**, és kattintson a **OK** bezárásához a *Internetbeállítások* párbeszédpanel megnyitásához.

## <a name="cannot-connect-to-a-remote-workgroup-computer"></a>Nem lehet csatlakozni egy távoli munkacsoport-számítógéphez

Ha a célszámítógép egy munkacsoport tagja, használja a következő szintaxist a felhasználónév megadásához és a számítógépre történő bejelentkezéshez:`<workgroup_name>\<user_name>`

## <a name="cannot-find-web-server-iis-management-tools-even-though-the-role-was-installed"></a>A rendszer nem találja a webkiszolgáló (IIS) felügyeleti eszközöket, pedig a szerepkör telepítve van

Ha a Windows PowerShell Web Access segítségével telepítette a `Install-WindowsFeature` parancsmag, felügyeleti eszközei nincsenek telepítve, kivéve, ha a `-IncludeManagementTools` paraméter hozzáadódik a parancsmagot.

Egy vonatkozó példáért lásd: [Windows PowerShell Web Access telepítése a Windows PowerShell-parancsmagok használatával](install-and-use-windows-powershell-web-access.md#to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets).

Az IIS-kezelő konzolon is hozzáadhat, és egyéb IIS felügyeleti eszközöket, hogy van szüksége, ha kiválasztja a egy **hozzáadása szerepkörök és szolgáltatások varázsló** az átjárókiszolgálót célzó munkamenet.
A szerepkörök hozzáadása és szolgáltatások varázsló megnyitása a Kiszolgálókezelőben

## <a name="windows-powershell-web-access-website-is-not-accessible"></a>A Windows PowerShell Web Access webhely nem érhető el.

Ha fokozott biztonsági beállítások engedélyezve van az Internet Explorerben (IE ESC), a Windows PowerShell Web Access webhely is hozzáadhat a megbízható helyek listájához.

A kisebb ajánlott megközelítést, biztonsági kockázatok miatt is letilthatja az IE ESC-t.
Letilthatja az IE ESC-t a helyi kiszolgáló oldalán a Kiszolgálókezelőben a Tulajdonságok csempén.

## <a name="an-authorization-failure-occurred-verify-that-you-are-authorized-to-connect-to-the-destination-computer"></a>Engedélyezési hiba történt. Győződjön meg arról, hogy jogosult a célszámítógéphez kapcsolódni.

A fenti hibaüzenet jelenik meg, amikor az átjárókiszolgáló a célszámítógép, és egyben egy munkacsoporthoz csatlakozás közben.

Amikor az átjárókiszolgáló is a célkiszolgálón, és egy munkacsoporthoz, adja meg a felhasználónevet, a számítógépnév és a felhasználó csoportnevét.
A számítógép nevét képviselő ne használjon önmagában egy pontot (.) önmagában.

### <a name="scenarios-and-proper-values"></a>Forgatókönyvek és a megfelelő értékek

#### <a name="all-cases"></a>Minden esetben

Paraméter | Érték
-- | --
UserName | Kiszolgáló\_neve\\felhasználói\_neve<br/>Localhost\\felhasználói\_neve<br/>. \\felhasználói\_neve
Felhasználói csoport | Kiszolgáló\_neve\\felhasználói\_csoport<br/>Localhost\\felhasználói\_csoport<br/>. \\felhasználói\_csoport
ComputerGroup | Kiszolgáló\_neve\\számítógép\_csoport<br/>Localhost\\számítógép\_csoport<br/>. \\számítógép\_csoport

#### <a name="gateway-server-is-in-a-domain"></a>Az átjárókiszolgáló egy tartományhoz tartozik

Paraméter | Érték
-- | --
ComputerName | Az átjárókiszolgáló teljes neve vagy Localhost

#### <a name="gateway-server-is-in-a-workgroup"></a>Az átjárókiszolgáló egy munkacsoporthoz tartozik

Paraméter | Érték
-- | --
ComputerName | Kiszolgálónév

### <a name="gateway-credentials"></a>Átjáró hitelesítő adatok

Jelentkezzen be a célkiszolgálóként működő átjárókiszolgálóra a következők valamelyike szerint formázott hitelesítő adatokkal.

- Kiszolgáló\_neve\\felhasználói\_neve
- Localhost\\felhasználói\_neve
- . \\felhasználói\_neve

## <a name="a-security-identifier-sid-is-displayed-in-an-authorization-rule"></a>Egy biztonsági azonosítóval (SID) jelenik meg egy engedélyezési szabályban

Egy biztonsági azonosítóval (SID) jelenik meg egy engedélyezési szabályt, a szintaxis felhasználó helyett\_neve/számítógép\_nevét.

Ennek az lehet az oka, hogy a szabály már nem érvényes, vagy az Active Directory tartományi szolgáltatások lekérdezése meghiúsult.
Az engedélyezési szabály érvénytelen általában helyzetekben, amikor az átjárókiszolgáló korábban egy munkacsoporthoz tartozott, de aztán egy tartományhoz csatlakoztatták

## <a name="cannot-sign-in-with-rule-as-an-ipv6-address-with-a-domain"></a>Tartománnyal rendelkező IPv6-címként nem tud bejelentkezni a szabály

Nem lehet bejelentkezni egy olyan célszámítógépre, ami az engedélyezési szabályokban tartománnyal rendelkező IPv6-címként lett meghatározva.

Az engedélyezési szabályok nem támogatják az IPv6-címek használatát a tartománynevekben.

Ha IPv6-cím használatával szeretne megadni egy célszámítógépet, használja az eredeti (kettőspontokat tartalmazó) IPv6-címet az engedélyezési szabályban.
A tartomány és a numerikus (kettőspontokat tartalmazó) IPv6-címeket a célszámítógép nevének a Windows PowerShell Web Access bejelentkezési oldal, de az engedélyezési szabályok nem támogatottak. 

IPv6-címekre vonatkozó további információkért lásd: [IPv6 működése](https://technet.microsoft.com/en-us/library/cc781672(v=ws.10).aspx).

## <a name="see-also"></a>Lásd még:

- [Az engedélyezési szabályok és a Windows PowerShell Web Access biztonsági funkciói](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)
- [A webes Windows PowerShell konzol használata](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)
- [about_Remote_Requirements](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_remote_requirements)
