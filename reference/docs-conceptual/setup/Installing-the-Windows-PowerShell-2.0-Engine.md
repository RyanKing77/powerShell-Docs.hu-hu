---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A Windows PowerShell 2.0 motor telepítése
ms.assetid: 82928f2b-f96a-4ae6-a0d0-6e7b181da308
ms.openlocfilehash: 0b3282a1a67886509e749af0f499c47fe7a99411
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952341"
---
# <a name="installing-the-windows-powershell-20-engine"></a>A Windows PowerShell 2.0 motor telepítése
Ez a témakör ismerteti, hogyan telepítheti a Windows PowerShell 2.0 motor.

Visszafelé kompatibilis a Windows PowerShell 2.0 a Windows PowerShell 3.0 célja. Parancsmagok, szolgáltatók, beépülő modulok, modulok és a Windows PowerShell 2.0 parancsfájlokat futtassa a Windows PowerShell 3.0 és a Windows PowerShell 4.0 változatlan. Azonban a Microsoft .NET-keretrendszer 4 futásidejű aktiválási házirend módosítása miatt Windows PowerShell gazdagépre programok az Windows PowerShell 2.0-s verziójához és a közös nyelvi futtatókörnyezet (CLR) 2.0 fordítása nem futtatható a módosítás nélkül később a Windows PowerShell, amelyek a közös nyelvi futtató környezet 4.0-s lefordított kiadásaiban.

Az előző verziókkal való kompatibilitás a parancsok és ezek a változások által érintett gazdagépre programok, a Windows PowerShell 2.0, a Windows PowerShell 3.0 és a Windows PowerShell 4.0 motorok való egymás melletti futtatásra tervezték. Emellett a Windows PowerShell 2.0 motor a Windows Server 2012 R2, Windows 8.1, Windows 8, Windows Server 2012 és Windows Management Framework 3.0 tartalmazza. A Windows PowerShell 2.0 motor kívánják használni, ha egy meglévő parancsfájl vagy a gazdagép program nem futtatható, mert nem kompatibilis a Windows PowerShell 3.0, a Windows PowerShell 4.0 vagy a Microsoft .NET-keretrendszer 4. Ilyen esetekben várhatóan ritkán fordul elő.

A Windows PowerShell 2.0 motor a Windows Server 2012 R2, Windows 8.1, Windows® 8 és Windows Server® 2012 választható lehetőség. A Windows korábbi verzióiban a Windows Management Framework 3.0 telepítésekor a Windows PowerShell 3.0 telepítés teljesen lecseréli a Windows PowerShell 2.0 telepítése a Windows PowerShell telepítési könyvtárában. Azonban a Windows PowerShell 2.0 motor megőrzi.

A Windows PowerShell 2.0 motor indításával kapcsolatos információkért lásd: [indítása a Windows PowerShell 2.0 motor](Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="on-windows-81-and-windows-8"></a>A Windows 8.1 és Windows 8
A Windows 8.1 és Windows 8 a Windows PowerShell 2.0 motor funkció alapértelmezés szerint van kapcsolva. Azonban a használatához meg kell kapcsolja be a Microsoft .NET-keretrendszer 3.5-ös verzióját, amely van szükség. Ez a szakasz azt is bemutatja, hogyan kapcsolja be a Windows PowerShell 2.0 motor szolgáltatás be- és kikapcsolható.

#### <a name="to-turn-on-net-framework-35"></a>.NET-keretrendszer 3.5 bekapcsolása

1. Az a **Start** írja be **Windows-szolgáltatások**.

2. Az a **alkalmazások** sávban kattintson **beállítások**, és kattintson a **Windows-szolgáltatások be- és kikapcsolása**.

3. Az a **Windows-szolgáltatások** kattintson **.NET-keretrendszer 3.5 (.NET 2.0 és 3.0** rá kattintva jelölje ki.

    Ha bejelöli **.NET-keretrendszer 3.5 (.NET 2.0 és 3.0**, a mezőben változó kitöltése jelzi, hogy a szolgáltatás csak egy része van kiválasztva. Ez azonban elegendő-e a Windows PowerShell 2.0 motor.

#### <a name="to-turn-the-windows-powershell-20-engine-on-and-off"></a>Be- és kikapcsolható, kapcsolja be a Windows PowerShell 2.0 motor

1. Az a **Start** írja be **Windows-szolgáltatások**.

2. Az a **alkalmazások** sávban kattintson **beállítások**, és kattintson a **Windows-szolgáltatások be- és kikapcsolása**.

3. Az a **Windows-szolgáltatások** bontsa ki a **Windows PowerShell 2.0** csomópontot, majd kattintson a **Windows PowerShell 2.0 motor** szövegmezőre, válassza ki, vagy törölje a jelölést.

## <a name="on-windows-server-2012-r2-and-windows-server-2012"></a>A Windows Server 2012 R2 és Windows Server 2012-ben
Az alábbi eljárások segítségével adja hozzá a Windows PowerShell 2.0 motor és a Microsoft .NET-keretrendszer 3.5 szolgáltatásai. A Windows PowerShell 2.0 motor 2.0.50727 Microsoft .NET-keretrendszer minimális szükséges. Ez a követelmény teljesül által a Microsoft .NET-keretrendszer 3.5-ös verzióját.

#### <a name="to-add-the-net-framework-35-feature"></a>A .NET-keretrendszer 3.5 funkció hozzáadása

1. A **Kiszolgálókezelő**, az a **kezelése** menü **szerepkörök és szolgáltatások hozzáadása**.

    Vagy a **Kiszolgálókezelő**, kattintson a **kiszolgálóinak**, kattintson a jobb gombbal a kiszolgáló nevét, majd válassza ki **szerepkörök és szolgáltatások hozzáadása**.

2. Az a **telepítési típus** lapon jelölje be **szerepköralapú vagy szolgáltatásalapú telepítés**.

3. Az a **szolgáltatások** ablaktáblában bontsa ki a **.NET-keretrendszer 3.5 szolgáltatásai** csomópont, és válassza **.NET-keretrendszer 3.5 (tartalmazza a .NET 2.0 és 3.0 verziót)**.

    A Windows PowerShell 2.0 motor nem szükségesek az adott csomópont alatt található egyéb beállításokat.

#### <a name="to-add-the-windows-powershell-20-engine-feature"></a>Adható hozzá a Windows PowerShell 2.0 motor

- A **Kiszolgálókezelő**, az a **kezelése** menü **szerepkörök és szolgáltatások hozzáadása**.

    Vagy **Kiszolgálókezelő**, kattintson a **kiszolgálóinak**, kattintson a jobb gombbal a kiszolgáló nevét, majd válassza ki **szerepkörök és szolgáltatások hozzáadása**.

- Az a **telepítési típus** lapon jelölje be **szerepköralapú vagy szolgáltatásalapú telepítés**.

- Az a **szolgáltatások** ablaktáblában bontsa ki a **Windows PowerShell (telepített)** csomópont, és válassza **Windows PowerShell 2.0 motor**.

A Windows PowerShell 2.0 motor indításával kapcsolatos információkért lásd: [indítása a Windows PowerShell 2.0 motor](Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="on-earlier-systems"></a>A korábbi rendszerek
A [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881) csomagot, amely a Windows 7, Windows Server 2008 R2 és Windows Server 2012, Windows PowerShell 4.0-s verzióját telepíti a Windows PowerShell 2.0 motor tartalmazza. A Windows PowerShell 2.0 motor az engedélyezett és készen áll a használatra, szükség esetén további telepítési, a telepítés vagy a konfiguráció nélkül.

A Windows Management Framework 3.0-csomagot, amely a Windows 7, Windows Server 2008 R2 és Windows Server 2008, Windows PowerShell 3.0 telepíti a Windows PowerShell 2.0 motor tartalmazza. A Windows PowerShell 2.0 motor az engedélyezett és készen áll a használatra, szükség esetén további telepítési, a telepítés vagy a konfiguráció nélkül.

## <a name="see-also"></a>Lásd még:
- [Windows PowerShell rendszerkövetelményei](Windows-PowerShell-System-Requirements.md)
- [Windows PowerShell telepítése](Installing-Windows-PowerShell.md)
- [A Windows PowerShell indítása](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)
- [A Windows PowerShell 2.0 motor indítása](Starting-the-Windows-PowerShell-2.0-Engine.md)