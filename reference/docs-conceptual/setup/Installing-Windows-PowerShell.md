---
ms.date: 08/09/2017
keywords: PowerShell, a parancsmag, letöltése, telepítése, beállításához, windows 10, windows 8.1, windows 8.0-s, windows 7
title: A Windows PowerShell telepítése
ms.openlocfilehash: 89f0f689ebfcd34dd4c8ec3824ec8ab4bddc34d9
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/25/2018
---
# <a name="installing-windows-powershell"></a>A Windows PowerShell telepítése
A Windows PowerShell előre telepített alapértelmezés szerint a minden Windows, Windows 7 SP1 és Windows Server 2008 R2 SP1 kezdve.

Ha érdekli PowerShell 6 és újabb verziók, telepítendő PowerShell alapvető Windows PowerShell helyett. Az adott, lásd: [PowerShell központi telepítése Windows](Installing-PowerShell-Core-on-Windows.md).

## <a name="finding-powershell-in-windows-10-81-80-and-7"></a>A Windows 10, 8.1, 8.0 és 7 PowerShell keresése

Néha a PowerShell keresése konzol vagy a ISE (integrált parancsfájlkezelési környezet) a Windows nehézségekbe ütközhet, helyének áthelyezése egyik verzióról a Windows a következő módon.

Az alábbi táblázatok segítséget PowerShell található a Windows-verzió.
Az itt felsorolt összes verzió az eredeti verzió, amelyeket szabaddá, nincsenek frissítések.

### <a name="for-console"></a>A konzol

Verzió | Hely
-- | --
Windows-10 | Kattintson a bal alsó sarokban Windows ikon, kezdje el begépelni PowerShell
Windows 8.1, 8.0 | Indítsa el a kezdőképernyőn írja be a PowerShell.<br/>Ha a számítógépen, kattintson a bal alsó sarokban Windows ikon kezdje el beírni PowerShell
Windows 7 SP1 | Kattintson a bal alsó sarokban Windows ikonra, a keresési mezőbe írja be a PowerShell elindítása

### <a name="for-ise"></a>Az ISE

Verzió | Hely
-- | --
Windows-10 | Kattintson a bal alsó sarokban Windows ikon, kezdje el begépelni az ISE
Windows 8.1, 8.0 | A kezdőképernyőn írja be a **PowerShell ISE**.<br/>Ha az asztalon kattintson bal alsó sarokban Windows ikonra, írja be a **PowerShell ISE**
Windows 7 SP1 | Kattintson a bal alsó sarokban Windows ikonra, a keresési mezőbe írja be a PowerShell elindítása

## <a name="finding-powershell-in-windows-server-versions"></a>Windows Server-verziók PowerShell keresése

Windows Server 2008 R2 verziótól kezdődően a Windows operációs rendszer nélkül is telepíthetők a grafikus felhasználói felületen (GUI).
Windows Server a grafikus felhasználói felület nélkül kiadásai megnevezett **Core** és a grafikus felhasználói Felülettel rendelkező kiadásához nevű **asztali**.

### <a name="windows-server-core-editions"></a>Windows Server Core kiadásokban

Az összes mag kiadásai amikor bejelentkezik a kiszolgáló kap egy Windows parancssori ablakban.

Típus `powershell` nyomja le az ENTER **ENTER** PowerShell elindítása belül a parancssor-szakaszt.
Típus `exit` állítsa le a PowerShell-parancssorba, majd a parancssorba való visszatéréshez.

### <a name="windows-server-desktop-editions"></a>Windows Server asztali verziója esetén

Összes asztali kiadása kattintson a bal alsó sarokban Windows ikonra kezdje el beírni PowerShell.
Mind a konzolon, és az ISE-beállítások kapják meg.

Az egyetlen kivétel a fenti szabály, a Windows Server 2008 R2 SP1; ISE Ebben az esetben kattintson a bal alsó sarokban Windows ikonra, írja be a PowerShell ISE.

## <a name="how-to-check-the-version-of-powershell"></a>Hogyan PowerShell verziójának ellenőrzése

Található PowerShell verziójának telepítését, indítsa el a PowerShell-konzolban (vagy az ISE) és típus `$PSVersionTable` nyomja le az ENTER **ENTER**. Keresse meg a `PSVersion` érték.

## <a name="upgrading-existing-windows-powershell"></a>Meglévő Windows PowerShell frissítése

A telepítőcsomag PowerShell belül egy WMF telepítő származnak.
A WMF installer verziójának ugyanolyan verziójúak, mint a PowerShell; nem önálló telepítő Windows PowerShell van.

Ha frissítenie kell a meglévő PowerShell, a Windows rendszerben segítségével az alábbi táblázatban keresse meg a telepítő frissíti a PowerShell-verziójának.

Windows | POWERSHELL 3.0 | PS 4.0 | PS 5.0 | PS 5.1 |
--|--|--|--|--|
Windows 10 (lásd a Note1)<br/>Windows Server 2016 | - | - | - | telepítve
A Windows 8.1<br/>Windows Server 2012 R2 | - | telepítve | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
Windows 8<br/>Windows Server 2012 | telepítve | [WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
Windows 7 SP1<br/>Windows Server 2008 R2 SP1 | [A WMF 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) | [WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)

> **Megjegyzés: 1**:
  >>
  >> PowerShell engedélyezve van, az automatikus frissítések szolgáltatással a Windows 10, a kezdeti verzióját a 5.1 5.0-s verziójáról frissíti az lekérdezi.
  >>
  >> Ha a Windows 10 eredeti verzióját nem frissül a Windows-frissítések, a PowerShell verziója 5.0.

## <a name="need-azure-powershell"></a>Az Azure PowerShell kell

Ha a keresett **Azure PowerShell**, sikerült a kiindulási pont [áttekintés az Azure PowerShell](https://docs.microsoft.com/powershell/azure).

Ellenkező esetben előfordulhat, hogy teendők van [telepítése és konfigurálása az Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

## <a name="see-also"></a>Lásd még:

- [Windows PowerShell rendszerkövetelményei](Windows-PowerShell-System-Requirements.md)
- [A Windows PowerShell indítása](Starting-Windows-PowerShell.md)