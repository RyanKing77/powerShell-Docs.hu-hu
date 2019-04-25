---
ms.date: 08/09/2017
keywords: PowerShell, parancsmag, letöltése, telepítése, a telepítő, windows 10, windows 8.1, windows 8.0-s, windows 7
title: A Windows PowerShell telepítése
ms.openlocfilehash: 345cde8012bece730e7217ed16be6175ad26bb28
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086476"
---
# <a name="installing-windows-powershell"></a>A Windows PowerShell telepítése

Windows PowerShell előre telepített alapértelmezés szerint a minden Windows, Windows 7 SP1 és a Windows Server 2008 R2 SP1-től.

Ha érdekli a PowerShell 6-os vagy újabb, a PowerShell Core helyett a Windows PowerShell telepíteni szeretné. Ehhez lásd [Windows-alapú PowerShell Core telepítése](Installing-PowerShell-Core-on-Windows.md).

## <a name="finding-powershell-in-windows-10-81-80-and-7"></a>A Windows 10-es, 8.1, 8.0-s és 7 PowerShell keresése

Néha keresése a PowerShell konzolt vagy az ISE-ben (integrált parancsfájl-kezelési környezet) a Windows nehézkes lehet, mint a Windows egyik verziójának a helyét helyez át a következő.

Az alábbi táblázatok segítséget PowerShell található Windows-verzióhoz.
Az itt felsorolt összes verzió az eredeti verzió, mert a kiadott, sem a frissítés.

### <a name="for-console"></a>-Konzol

Verzió | Hely
-- | --
Windows 10 | Kattintson a bal alsó sarokban Windows ikonjára, és kezdje el begépelni a PowerShell
Windows 8.1, 8.0 | A kezdőképernyőn írja be a PowerShell indítása.<br/>Ha a számítógépen, kattintson a bal alsó sarokban Windows ikonjára, kezdje el begépelni a PowerShell
Windows 7 SP1 | Kattintson a bal alsó sarokban található Windows ikont, a Keresés mezőbe írja be a PowerShell start

### <a name="for-ise"></a>Az ISE-ben

Verzió | Hely
-- | --
Windows 10 | Kattintson a bal alsó sarokban Windows ikonjára, és kezdje el begépelni az ISE-ben
Windows 8.1, 8.0 | A kezdőképernyőn írja be a **PowerShell ISE-ben**.<br/>Ha az asztalon kattintson bal alsó sarokban található Windows ikonra, írja be a **PowerShell ISE-ben**
Windows 7 SP1 | Kattintson a bal alsó sarokban található Windows ikont, a Keresés mezőbe írja be a PowerShell start

## <a name="finding-powershell-in-windows-server-versions"></a>Keresés a PowerShell a Windows Server-verziók

A Windows Server 2008 R2 verziótól kezdődően Windows operációs rendszer nélkül is telepíthetők a grafikus felhasználói felületen (GUI).
Windows Server a grafikus felhasználói felület nélkül kiadásai nevesített **Core** és kiadása a grafikus felhasználói Felülettel rendelkező nevű **asztali**.

### <a name="windows-server-core-editions"></a>A Windows Server Core kiadásokban

A Core kiadásokban az összes a kiszolgálón való bejelentkezéskor kap egy Windows parancssori ablakban.

Típus `powershell` nyomja le az ENTER **ENTER** PowerShell elindítása belül a parancssori munkamenetben.
Típus `exit` leállítása a PowerShell-munkamenetet, és visszatérhet a parancssor használatával.

### <a name="windows-server-desktop-editions"></a>A Windows Server asztali verziója esetén

Az összes asztali verzió kattintson a bal alsó sarokban található Windows ikonra, kezdje el begépelni a PowerShell.
Konzol és az ISE-beállítások is kap.

Az egyetlen kivétel a fenti szabály, a Windows Server 2008 R2 SP1; az ISE-ben Ebben az esetben kattintson a bal alsó sarokban található Windows ikonra, írja be a PowerShell ISE-ben.

## <a name="how-to-check-the-version-of-powershell"></a>A PowerShell-verzió ellenőrzése

Keresse meg a PowerShell-verzió van telepítve, indítsa el a PowerShell-konzolt (vagy az ISE-ben), és írja be `$PSVersionTable` nyomja le az ENTER **ENTER**. Keresse meg a `PSVersion` értéket.

## <a name="upgrading-existing-windows-powershell"></a>Meglévő Windows PowerShell frissítése

A telepítőcsomag PowerShell belül a WMF-telepítési származnak.
A WMF telepítő verzióegyezéseket PowerShell; verziója Nincs nincs önálló telepítő a Windows PowerShell környezethez.

Ha a meglévő PowerShell-lel, frissítenie kell a Windows, segítségével az alábbi táblázatban keresse meg a frissíteni kívánt PowerShell verziójának telepítőjét.

Windows | PS 3.0 | PS 4.0 | PS 5.0 | PS 5.1 |
--|--|--|--|--|
A Windows 10-es (lásd a Note1)<br/>Windows Server 2016 | - | - | - | Telepítve van
Windows 8.1<br/>Windows Server 2012 R2 | - | Telepítve van | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
Windows 8<br/>Windows Server 2012 | Telepítve van | [WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
Windows 7 SP1<br/>Windows Server 2008 R2 SP1 | [WMF 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) | [WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)

> [!NOTE]
>
> Az automatikus frissítések szolgáltatás engedélyezve van, a Windows 10, az eredeti kiadásban a PowerShell 5.0, 5.1-es verziójából származó frissül.
>
> Ha az eredeti verzió Windows 10-es nem frissül a Windows-frissítések, a PowerShell verziója 5.0-s.

## <a name="need-azure-powershell"></a>Az Azure PowerShell szükséges.

Ha a keresett **Azure PowerShell-lel**, kezdheti [áttekintése az Azure PowerShell](/powershell/azure/overview).

Ellenkező esetben van, mit érdemes [telepítése és konfigurálása az Azure PowerShell-lel](/powershell/azure/install-az-ps)

## <a name="see-also"></a>Lásd még:

[Windows PowerShell rendszerkövetelményei](Windows-PowerShell-System-Requirements.md)

[Windows PowerShell indítása](../getting-started/Starting-Windows-PowerShell.md)
