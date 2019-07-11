---
ms.date: 08/23/2017
keywords: PowerShell, a parancsmag
title: a windows powershell-elérés hozzáférési problémák hibaelhárítása
ms.openlocfilehash: 66e913504cf0c34f8d9ab18b088fb06173aca24c
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67733864"
---
# <a name="troubleshooting-access-problems-in-windows-powershell-web-access"></a>Hozzáférési problémák hibaelhárítása a Webes Windows PowerShell-elérésben

Frissítve: Június 24 2013 (2017. augusztus 23 módosított)

Érvényes: Windows Server 2012 R2, Windows Server 2012

Az alábbi szakaszok néhány gyakori problémák azonosítása a Windows PowerShell-elérés használatával távoli számítógéphez való csatlakozásra tett kísérlet közben, és a problémák megoldásához javaslatokat tartalmaz.

## <a name="sign-in-failure"></a>Bejelentkezési hiba

A hiba oka a következők bármelyike lehet.

- Hiányzik egy olyan engedélyezési szabály, amely lehetővé tenné a felhasználónak a számítógép hozzáférését vagy hiányzik egy adott munkamenet-konfiguráció a távoli számítógépen.

  Windows PowerShell-elérés biztonsági korlátozó; felhasználók engedélyezési szabályok segítségével a távoli számítógépek kifejezett hozzáférést kell adni.

  Az engedélyezési szabályok létrehozásával kapcsolatos további információkért lásd: [engedélyezési szabályai és biztonsági szolgáltatások a Windows PowerShell-elérés](authorization-rules-and-security-features-of-windows-powershell-web-access.md).

- A felhasználó rendelkezik engedélyezett hozzáféréssel a célszámítógéphez. A hozzáférést a hozzáférés-vezérlési listák (access control list, ACL) határozzák meg.

  További információkért lásd: [bejelentkezés a Windows PowerShell-elérés](use-the-web-based-windows-powershell-console.md#signing-in-to-windows-powershell-web-access), vagy a Windows PowerShell csapatának blogját.

- Előfordulhat, hogy a célszámítógépen nincs engedélyezve távoli felügyelet a Windows PowerShell.

  Ellenőrizze a távoli felügyelet engedélyezve van a számítógépen, amelyre a felhasználó csatlakozni próbál.

  További információkért lásd: [hogyan konfigurálja a számítógépet a távelérése](/powershell/module/microsoft.powershell.core/about/about_remote_requirements#how-to-configure-your-computer-for-remoting).

## <a name="internal-server-error"></a>Belső kiszolgálóhiba

Amikor a felhasználók próbálnak bejelentkezni a Windows PowerShell-elérés-Internet Explorer-ablakban, láthatók- **belső kiszolgálóhiba** lapon vagy *az Internet Explorer* nem válaszol.

Ez a hiba csak az Internet Explorerben fordul elő.

### <a name="possible-cause"></a>Lehetséges ok

Olyan felhasználóknál jelentkezhet, akik kínai karaktereket használó tartománynévvel jelentkeztek be, vagy akiknél az átjárókiszolgáló neve kínai karaktereket tartalmaz.

#### <a name="workaround"></a>Áthidaló megoldás

1. [Telepítse és futtassa az Internet Explorer 10](https://ie.microsoft.com/testdrive/info/downloads/Default.html)
1. Módosítsa az Internet Explorer **dokumentum-üzemmód** beállítást *IE10* szabványoknak.
   1. Nyomja meg **F12** a fejlesztői eszközök konzol megnyitása
   1. Kattintson az Internet Explorer 10 **Böngészőmódot használ**, majd válassza ki *Internet Explorer 10*.
   1. Kattintson a **dokumentum-üzemmód**, és kattintson a *IE10* szabványoknak.
   1. Nyomja meg **F12** a fejlesztői eszközök konzol bezárásához.
1. Tiltsa le az Internet Explorer 10 automatikus proxybeállítást.
   1. Kattintson a **eszközök**, és kattintson a **Internetbeállítások**.
   1. Az a **Internetbeállítások** párbeszédpanel a **kapcsolatok** lapra, majd **LAN-beállítások**.
   1. Törölje a **beállítások automatikus észlelése** jelölőnégyzetet. Kattintson a **OK**, és kattintson a **OK** újra gombra kattintva zárja be a *Internetbeállítások* párbeszédpanel bezárásához.

## <a name="cannot-connect-to-a-remote-workgroup-computer"></a>Nem lehet csatlakozni egy távoli munkacsoport-számítógéphez

Ha a célszámítógép egy munkacsoport tagja, használja a következő szintaxist a felhasználónév megadásához és a számítógépre történő bejelentkezéshez: `<workgroup_name>\<user_name>`

## <a name="cannot-find-web-server-iis-management-tools-even-though-the-role-was-installed"></a>A rendszer nem találja a webkiszolgáló (IIS) felügyeleti eszközöket, pedig a szerepkör telepítve van

Ha a Windows PowerShell-elérés segítségével telepítve van a `Install-WindowsFeature` parancsmagot, a felügyeleti eszközök nincsenek telepítve, kivéve, ha a `-IncludeManagementTools` paramétert a parancsmaghoz kerül.

Egy vonatkozó példáért lásd: [Windows PowerShell-elérés telepítése a Windows PowerShell-parancsmagok használatával](install-and-use-windows-powershell-web-access.md#to-install-windows-powershell-web-access-by-using-windows-powershell-cmdlets).

Az IIS-kezelő konzolon is hozzáadhat, és egyéb IIS felügyeleti eszközöket, hogy van szüksége, az eszközök a kiválasztásával egy **adja hozzá szerepkörök és szolgáltatások varázsló** munkamenetet, amely az átjárókiszolgáló célja.
A szerepkörök hozzáadása és a szolgáltatások varázsló megnyílik a Kiszolgálókezelőben.

## <a name="windows-powershell-web-access-website-is-not-accessible"></a>Windows PowerShell-elérés webhely nem érhető el.

Ha fokozott biztonsági beállítások engedélyezve van az Internet Explorer (IE ESC), a Windows PowerShell-elérés webhely is hozzáadhat a megbízható helyek listájához.

A kisebb ajánlott megközelítés, biztonsági kockázatok miatt az IE ESC letiltása.
Letilthatja az IE ESC a helyi kiszolgáló oldalán a Kiszolgálókezelőben a Tulajdonságok csempén.

## <a name="an-authorization-failure-occurred-verify-that-you-are-authorized-to-connect-to-the-destination-computer"></a>Engedélyezési hiba történt. Győződjön meg arról, hogy jogosult a célszámítógéphez kapcsolódni.

A fenti hibaüzenet jelenik meg az átjárókiszolgáló a célszámítógép, és egyben egy munkacsoporthoz való kapcsolódás közben.

Ha az átjáró-kiszolgálót is a célkiszolgálón, és azt egy munkacsoporthoz tartozik, adja meg a felhasználónevet, a számítógép neve és a felhasználói csoport nevét.
Ne használjon egy pontot (.) önmagában számítógépnévként.

### <a name="scenarios-and-proper-values"></a>Forgatókönyvek és a megfelelő értékekre

#### <a name="all-cases"></a>Minden esetben

Paraméter | Érték
-- | --
UserName | Server\_name\\user\_name<br/>Localhost\\user\_name<br/>.\\user\_name
UserGroup | Kiszolgáló\_neve\\felhasználói\_csoport<br/>Localhost\\user\_group<br/>. \\felhasználói\_csoport
ComputerGroup | Kiszolgáló\_neve\\számítógép\_csoport<br/>Localhost\\computer\_group<br/>.\\computer\_group

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

- Server\_name\\user\_name
- Localhost\\user\_name
- .\\user\_name

## <a name="a-security-identifier-sid-is-displayed-in-an-authorization-rule"></a>Egy biztonsági azonosítóval (SID) jelenik meg egy olyan engedélyezési szabály

Egy biztonsági azonosítóval (SID) jelenik meg a szintaxis felhasználó helyett egy olyan engedélyezési szabály\_neve/számítógép\_nevét.

Ennek az lehet az oka, hogy a szabály már nem érvényes, vagy az Active Directory Domain Services lekérdezése meghiúsult.
Az engedélyezési szabály érvénytelen általában nem forgatókönyvekben, ahol az átjárókiszolgáló korábban egy munkacsoporthoz tartozik, de később csatlakozik egy tartományhoz

## <a name="cannot-sign-in-with-rule-as-an-ipv6-address-with-a-domain"></a>IPv6-címként egy tartomány nem tud bejelentkezni a szabály

Nem lehet bejelentkezni egy olyan célszámítógépre, ami az engedélyezési szabályokban tartománnyal rendelkező IPv6-címként lett meghatározva.

Az engedélyezési szabályok nem támogatják az IPv6-címek használatát a tartománynevekben.

Ha IPv6-cím használatával szeretne megadni egy célszámítógépet, használja az eredeti (kettőspontokat tartalmazó) IPv6-címet az engedélyezési szabályban.
A tartomány és a numerikus (kettőspontokat tartalmazó) IPv6-címeket is a célszámítógép nevének a Windows PowerShell-elérés bejelentkezési oldalon, de az engedélyezési szabályok nem támogatottak.

IPv6-címek kapcsolatos további információkért lásd: [IPv6 működése](https://technet.microsoft.com/library/cc781672(v=ws.10).aspx).

## <a name="see-also"></a>Lásd még:

- [Engedélyezési szabályai és biztonsági funkciói Windows PowerShell-Elérésbe](https://technet.microsoft.com/en-us/library/dn282394(v=ws.11).aspx)
- [A webes Windows PowerShell-konzol használata](https://technet.microsoft.com/en-us/library/hh831417(v=ws.11).aspx)
- [about_Remote_Requirements](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_requirements)
