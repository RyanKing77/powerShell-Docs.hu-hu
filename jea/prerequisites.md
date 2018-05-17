---
ms.date: 06/12/2017
keywords: jea, a powershell, a biztonsági
title: JEA Előfeltételek
ms.openlocfilehash: a5cf5519b30b24d44c12bdeedcf4cd763e2edbde
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="prerequisites"></a>Előfeltételek

> A következőkre vonatkozik: a Windows PowerShell 5.0

Csak elég felügyeleti lehetővé teszi a Windows PowerShell 5.0-s és újabb rendszer.
Ez a témakör ismerteti az előfeltételeket, amelyeket meg kell felelniük ahhoz, hogy a JEA használatának megkezdéséhez.

## <a name="install-jea"></a>JEA telepítése

JEA elérhető Windows PowerShell 5.0-s és újabb, de az összes funkció javasoljuk, hogy telepítse a PowerShell elérhető legújabb verzióját a rendszer.
Az alábbi táblázat a Windows Server JEA tartozó rendelkezésre állási ismerteti:

Kiszolgálói operációs rendszer   | JEA rendelkezésre állása
--------------------------|--------------------------------
Windows Server 2016       | Előre telepítve
Windows Server 2012 R2    | A WMF 5.1 összes funkcióját
Windows Server 2012       | A WMF 5.1 összes funkcióját
Windows Server 2008 R2    | Csökkentett funkció<sup>1</sup> a WMF 5.1

Otthoni vagy munkahelyi számítógépen JEA használhatja:

Ügyfél típusú operációs rendszer   | JEA rendelkezésre állása
--------------------------|-----------------------------------------------------
Windows 10 1607+          | Előre telepítve
Windows 10 1603, 1511     | Előtelepített, csökken funkció<sup>2</sup>
Windows 10 1507           | Nem elérhető el
Windows 8, 8.1            | A WMF 5.1 összes funkcióját
Windows 7                 | Csökkentett funkció<sup>1</sup> a WMF 5.1

<sup>1</sup> JEA csoportosan felügyelt szolgáltatásfiókok használatához Windows Server 2008 R2 vagy Windows 7 nem konfigurálható.
Virtuális fiókok és egyéb JEA szolgáltatások *vannak* támogatott.

<sup>2</sup> 1511-es és a 1603-as Windows 10-verziók nem támogatják a következő JEA: egy olyan csoport által felügyelt szolgáltatásfiókot, a munkamenet-konfigurációk feltételes hozzáférési szabályai, a felhasználó és helyi felhasználói fiókokhoz történő hozzáférés futtatnia.
Segítségre van szüksége a következő szolgáltatások, a Windows frissítése verzióra 1607 (évforduló frissítése) vagy újabb verzióját.

### <a name="check-which-version-of-powershell-is-installed"></a>Ellenőrizze, hogy mely PowerShell verziója telepítve van

Annak ellenőrzése, PowerShell verziójának telepítve van a rendszeren, ellenőrizze, hogy a `$PSVersionTable` változó a Windows PowerShell-parancssorban.

```powershell
PS C:\> $PSVersionTable.PSVersion

Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

A JEA használatára, ha készen áll a *fő* verziószáma kisebb mint **5**.
A legjobb élményt, és a legújabb szolgáltatásokhoz való hozzáférést, javasoljuk, hogy PowerShell verzióra frissít **5.1** amikor lehetséges.

### <a name="install-windows-management-framework"></a>A Windows Management Framework telepítése

Ha PowerShell régebbi verzióját futtatja, akkor frissítse rendszerét a Windows Management Framework (WMF) legfrissebb.
Frissítési csomagok és egy hivatkozást a WMF legújabb kibocsátási megjegyzésekben érhetők el a [letöltőközpontból](https://aka.ms/WMF5).

A számítási kompatibilitást WMF tesztelni az összes kiszolgáló frissítése előtt erősen ajánlott.

Windows 10 kell telepíteni a legújabb szolgáltatás-frissítéseket a Windows PowerShell aktuális verzióját.

## <a name="enable-powershell-remoting"></a>PowerShell-távelérés engedélyezése

PowerShell-távelérést az alapokat amelyen JEA épül.
Ezért elengedhetetlen, hogy engedélyezve van a PowerShell távelérése és [megfelelően védett](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity) JEA használata előtt a rendszeren.

A Windows Server 2012, 2012 R2 és 2016 alapértelmezés szerint engedélyezve van a PowerShell távvezérlését.
PowerShell távoli eljáráshívás engedélyezéséhez futtassa a következő parancsot egy emelt szintű PowerShell-ablakban.

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a>Engedélyezze a PowerShell-modul és a parancsfájl blokk naplózása (nem kötelező)

Az alábbi lépéseket az összes PowerShell műveleteket a rendszer a naplózás engedélyezése.
PowerShell modul naplózás nincs szükség JEA, azonban erősen ajánlott bekapcsolni, annak érdekében, hogy a parancsok felhasználók futtatni egy központi helyen vannak bejelentkezve.

A PowerShell modul naplózási házirend csoportházirend használatával konfigurálható.

1. Nyissa meg a Helyicsoportházirend-szerkesztő munkaállomáson vagy csoportházirend-objektumra a Csoportházirend kezelése konzol egy Active Directory tartományvezérlőn
2. Navigáljon a **számítógép konfigurációja\\felügyeleti sablonok\\Windows-összetevők\\Windows PowerShell**
3. Kattintson duplán a **kapcsolja be a modul naplózás**
4. Kattintson a **engedélyezve**
5. A beállítások területen kattintson a **megjelenítése** modul neve mellett
6. Típusa "**\***" az előugró ablakban. Ez arra utasítja a PowerShell-parancsok naplózásra kerül minden modul.
7. Kattintson a **OK** házirend beállítása
8. Kattintson duplán a **PowerShell parancsfájl-blokk naplózás bekapcsolása**
9. Kattintson a **engedélyezve**
10. Kattintson a **OK** házirend beállítása
11. (A tartományhoz csatlakoztatott számítógépeken csak) Futtatás **gpupdate** vagy várja meg, a frissített házirendet, és alkalmazza a beállításokat a csoportházirend

Rendszerszintű PowerShell írjanak elő csoportházirenden keresztül is engedélyezheti.

## <a name="next-steps"></a>További lépések

- [Egy szerepkör funkció fájl létrehozása](role-capabilities.md)
- [Egy munkamenet-konfigurációs fájl létrehozása](session-configurations.md)

## <a name="see-also"></a>Lásd még:

- [PowerShell távvezérlése és a Rendszerfelügyeleti webszolgáltatások biztonsággal kapcsolatos további információk](https://msdn.microsoft.com/powershell/scripting/setup/winrmsecurity)
- [*PowerShell ♥ a kék Team* a biztonsági által írt blogbejegyzés](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)