---
ms.date: 07/10/2019
keywords: jea, PowerShell, biztonság
title: A JEA előfeltételei
ms.openlocfilehash: 8fca5c068412e86acfdb8bed400699f721b76191
ms.sourcegitcommit: e894ed833cef57967cdaf002f8c883f66864e836
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/25/2019
ms.locfileid: "70017936"
---
# <a name="prerequisites"></a>Előfeltételek

Elég adminisztráció a PowerShell 5,0-es és újabb verziója. Ez a cikk azokat az előfeltételeket ismerteti, amelyeknek teljesülniük kell a JEA használatának megkezdéséhez.


## <a name="check-which-version-of-powershell-is-installed"></a>A PowerShell telepített verziójának megkeresése

Ha szeretné megnézni, hogy a PowerShell melyik verziója van telepítve a rendszeren `$PSVersionTable` , akkor a változót egy Windows PowerShell-parancssorban jelenítheti meg.

```powershell
$PSVersionTable.PSVersion
```

```Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

A JEA a PowerShell 5,0-es vagy újabb verziójával érhető el. A teljes funkcionalitás érdekében javasoljuk, hogy telepítse a PowerShell legújabb verzióját a rendszer számára. A következő táblázat ismerteti a JEA rendelkezésre állását a Windows Serveren:

| Kiszolgálói operációs rendszer |                JEA rendelkezésre állása                |
| ----------------------- | ---------------------------------------------- |
| Windows Server 2016 +    | Előtelepített                                   |
| Windows Server 2012 R2  | Teljes funkcionalitás a WMF 5,1-vel                |
| Windows Server 2012     | Teljes funkcionalitás a WMF 5,1-vel                |
| Windows Server 2008 R2  | Kevesebb funkció<sup>1</sup> a WMF 5,1-vel |

Használhatja a JEA a saját otthoni vagy munkahelyi számítógépén is:

| Ügyféloldali operációs rendszer |                   JEA rendelkezésre állása                   |
| ----------------------- | ---------------------------------------------------- |
| Windows 10 1607+        | Előtelepített                                         |
| Windows 10 1603, 1511   | Előre telepítve, a csökkentett funkciókkal<sup>2</sup> |
| Windows 10 1507         | Nem elérhető el                                        |
| Windows 8, 8,1          | Teljes funkcionalitás a WMF 5,1-vel                      |
| Windows 7               | Kevesebb funkció<sup>1</sup> a WMF 5,1-vel       |

- <sup>1</sup> a JEA nem konfigurálhatók csoportosan felügyelt szolgáltatásfiókok használatára windows Server 2008 R2 vagy Windows 7 rendszeren. *A* virtuális fiókok és egyéb JEA-funkciók támogatottak.

- <sup>2</sup> a következő JEA funkciók nem támogatottak a Windows 10 1511-es és 1603-es verziójában:

  - Futtatás csoportosan felügyelt szolgáltatásfiókként
  - Feltételes hozzáférési szabályok a munkamenet-konfigurációkban
  - A felhasználói meghajtó
  - Hozzáférés biztosítása a helyi felhasználói fiókokhoz

  Ezeknek a funkcióknak a támogatásához frissítse a Windowst az 1607-es (évfordulós frissítés) vagy újabb verzióra.

### <a name="install-windows-management-framework"></a>A Windows Management Framework telepítése

Ha a PowerShell egy régebbi verzióját futtatja, előfordulhat, hogy frissítenie kell a rendszert a legújabb Windows Management Framework (WMF) frissítéssel. További információt a [WMF dokumentációjában](/powershell/wmf/overview)talál.

Javasoljuk, hogy az összes kiszolgáló frissítése előtt tesztelje a munkaterhelést a WMF-kompatibilitással.

A Windows 10 rendszerű felhasználóknak telepíteniük kell a legújabb szolgáltatás-frissítéseket a Windows PowerShell aktuális verziójának beszerzéséhez.

## <a name="enable-powershell-remoting"></a>A PowerShell távelérésének engedélyezése

A PowerShell-távelérés biztosítja azt az alapot, amely a JEA épül. A JEA használata előtt meg kell győződnie arról, hogy a PowerShell távelérése engedélyezve van és megfelelően védett. További információ: [WinRM Security](/powershell/scripting/learn/remoting/winrmsecurity).

A PowerShell-távelérés alapértelmezés szerint engedélyezve van a Windows Server 2012, 2012 R2 és 2016 rendszeren. A PowerShell távelérési szolgáltatásának engedélyezéséhez futtassa a következő parancsot egy emelt szintű PowerShell-ablakban.

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a>PowerShell-modul és parancsfájl-blokkoló naplózásának engedélyezése (nem kötelező)

A következő lépésekkel engedélyezheti a naplózást a rendszeren lévő összes PowerShell-művelethez. A PowerShell-modul naplózása nem szükséges a JEA, azonban javasoljuk, hogy kapcsolja be a naplózást, hogy a felhasználók által futtatott parancsok központi helyen legyenek naplózva.

A PowerShell-modul naplózási házirendjét Csoportházirend használatával konfigurálhatja.

1. A Helyicsoportházirend-szerkesztő megnyitása egy munkaállomáson vagy egy Csoportházirend objektumon a Csoportházirend-kezelő konzol egy Active Directory-tartomány vezérlőn
2. Navigáljon a **számítógép\\konfigurációja\\felügyeleti sablonok Windows\\-összetevők Windows PowerShell**
3. Kattintson duplán a **modul naplózásának** bekapcsolása elemre.
4. Kattintson az **engedélyezve** lehetőségre
5. A beállítások szakaszban kattintson a **Megjelenítés** elemre a modulok neve mellett.
6. Írja `*` be az előugró ablakot a parancsok minden modulból való naplózásához.
7. A házirend beállításához kattintson **az OK** gombra.
8. Kattintson duplán a **PowerShell parancsfájl** -blokkoló naplózásának bekapcsolása elemre.
9. Kattintson az **engedélyezve** lehetőségre
10. A házirend beállításához kattintson **az OK** gombra.
11. (Csak tartományhoz csatlakoztatott gépeken) Futtassa `gpupdate` vagy várjon csoportházirend a frissített szabályzat feldolgozásához és a beállítások alkalmazásához

A Csoportházirend használatával is engedélyezheti a rendszerszintű PowerShell-átírást.

## <a name="next-steps"></a>További lépések

[Szerepkör-képesség fájl létrehozása](role-capabilities.md)

[Munkamenet-konfigurációs fájl létrehozása](session-configurations.md)

## <a name="see-also"></a>Lásd még:

[WinRM-biztonság](/powershell/scripting/learn/remoting/winrmsecurity)

[A PowerShell ♥ a kék csapatot](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)
