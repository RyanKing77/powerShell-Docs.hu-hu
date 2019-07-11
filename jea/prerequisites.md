---
ms.date: 07/10/2019
keywords: a jea, powershell, biztonsági
title: A JEA-Előfeltételek
ms.openlocfilehash: 8fca5c068412e86acfdb8bed400699f721b76191
ms.sourcegitcommit: 46bebe692689ebedfe65ff2c828fe666b443198d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/10/2019
ms.locfileid: "67734291"
---
# <a name="prerequisites"></a>Előfeltételek

Just Enough Administration lehetővé teszi a PowerShell 5.0-s vagy újabb. Ez a cikk ismerteti az előfeltételeket kell biztosítani a JEA használatának megkezdéséhez.


## <a name="check-which-version-of-powershell-is-installed"></a>Ellenőrizze, hogy telepítve van a PowerShell-verzió

Ellenőrizze a PowerShell-verzió van telepítve a rendszeren, ellenőrizze a `$PSVersionTable` változót egy Windows PowerShell-parancssort.

```powershell
$PSVersionTable.PSVersion
```

```Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      14393  1000
```

A JEA, a PowerShell 5.0-s vagy újabb. Az összes funkció ajánlott elérhető PowerShell legújabb verzióját telepíti a rendszer. A következő táblázat ismerteti a JEA a rendelkezésre állás Windows-kiszolgálón:

| Kiszolgálóoldali operációs rendszer |                A JEA rendelkezésre állása                |
| ----------------------- | ---------------------------------------------- |
| Windows Server 2016+    | Előtelepített                                   |
| Windows Server 2012 R2  | A WMF 5.1 összes funkciójának                |
| Windows Server 2012     | A WMF 5.1 összes funkciójának                |
| Windows Server 2008 R2  | Csökkentett funkciók<sup>1</sup> a WMF 5.1 |

A JEA a otthoni vagy munkahelyi számítógépen is használhatja:

| Ügyfél típusú operációs rendszer |                   A JEA rendelkezésre állása                   |
| ----------------------- | ---------------------------------------------------- |
| Windows 10 1607+        | Előtelepített                                         |
| Windows 10 1603, 1511   | Előre telepítve, a csökkentett funkciók<sup>2</sup> |
| Windows 10 1507         | Nem elérhető el                                        |
| A Windows 8, 8.1          | A WMF 5.1 összes funkciójának                      |
| Windows 7               | Csökkentett funkciók<sup>1</sup> a WMF 5.1       |

- <sup>1</sup> JEA csoportosan felügyelt szolgáltatásfiókok használatához a Windows Server 2008 R2 vagy Windows 7-es nem konfigurálható. A virtuális fiókok és egyéb JEA funkciók *vannak* támogatott.

- <sup>2</sup> a következő JEA-funkciók nem támogatottak a Windows 10-verziók 1511-es és a 1603-as:

  - A csoportosan felügyelt szolgáltatásfiókként fut
  - Feltételes hozzáférési szabályok a munkamenet-konfigurációk
  - A felhasználó meghajtó
  - Helyi felhasználói fiókokhoz való hozzáférést

  Segítségre van szüksége a következő szolgáltatások, 1607-es (Évfordulós frissítés) verzió Windows update vagy újabb verziója.

### <a name="install-windows-management-framework"></a>Telepítse a Windows Management Framework

Ha a PowerShell egy régebbi verzióját futtatja, szükség lehet a rendszer frissítése a legújabb Windows Management Framework (WMF) frissítéssel. További információkért lásd: a [WMF dokumentáció](/powershell/wmf/overview).

Javasoljuk, a WMF kompatibilitást a számítási feladat összes kiszolgáló frissítése előtt tesztelje.

Windows 10-es Windows PowerShell aktuális verzióját a legújabb funkciófrissítések kell telepítenie.

## <a name="enable-powershell-remoting"></a>PowerShell-távelérés engedélyezése

PowerShell-táveléréssel az alapokat, amelyen a JEA épül. Fontos biztosítani kell a PowerShell-táveléréssel engedélyezve van, és megfelelően titkosított a JEA használata előtt. További információkért lásd: [WinRM biztonsági](/powershell/scripting/learn/remoting/winrmsecurity).

A Windows Server 2012, 2012 R2 és 2016 alapértelmezés szerint engedélyezve van a PowerShell távoli eljáráshívás. PowerShell távoli eljáráshívás engedélyezéséhez futtassa a következő parancsot egy emelt szintű PowerShell-ablakban.

```powershell
Enable-PSRemoting
```

## <a name="enable-powershell-module-and-script-block-logging-optional"></a>Engedélyezze a PowerShell-modul és a parancsfájl blokk naplózása (nem kötelező)

Az alábbi lépésekkel engedélyezheti a rendszer minden PowerShell-műveletek naplózása. PowerShell-modul naplózás nem szükséges a jea-t, azonban ajánlott bekapcsolja a naplózást, és győződjön meg arról, a parancsok felhasználók futtatnak egy központi helyen van bejelentkezve.

A PowerShell-modul naplózási házirend csoportházirend használatával konfigurálható.

1. Nyissa meg a Helyicsoportházirend-szerkesztő a munkaállomásokon vagy csoportházirend-objektum az Active Directory-tartományvezérlő a Csoportházirend kezelése konzolt
2. Navigáljon a **számítógép konfigurációja\\felügyeleti sablonok\\Windows-összetevők\\Windows PowerShell**
3. Kattintson duplán a **modul naplózás bekapcsolása**
4. Kattintson a **engedélyezve**
5. Ebben a szakaszban, kattintson a **megjelenítése** Modulneveket mellett
6. Típus `*` a felugró ablakban parancsokat az összes modulok bejelentkezni.
7. Kattintson a **OK** házirend beállítása
8. Kattintson duplán a **PowerShell parancsprogram-blokkot naplózás bekapcsolása**
9. Kattintson a **engedélyezve**
10. Kattintson a **OK** házirend beállítása
11. (A tartományhoz csatlakoztatott gépeket csak) Futtatás `gpupdate` vagy várjon, amíg a csoportházirend segítségével dolgozza fel a frissített szabályzatot, és a alkalmazni a beállításokat

Rendszerszintű PowerShell beszédátírási csoportházirenden keresztül is engedélyezheti.

## <a name="next-steps"></a>További lépések

[Hozzon létre egy szerepkört képesség fájlt](role-capabilities.md)

[Egy munkamenet-konfigurációs fájl létrehozása](session-configurations.md)

## <a name="see-also"></a>Lásd még:

[A WinRM-biztonság](/powershell/scripting/learn/remoting/winrmsecurity)

[PowerShell ♥ a kék csapat](https://devblogs.microsoft.com/powershell/powershell-the-blue-team/)
