---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A Windows PowerShell 2.0 motor telepítése
ms.assetid: 82928f2b-f96a-4ae6-a0d0-6e7b181da308
ms.openlocfilehash: b625b61b4e191402074f57ea2e942f800dbbcd53
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404312"
---
# <a name="installing-the-windows-powershell-20-engine"></a>A Windows PowerShell 2.0 motor telepítése
Ez a témakör ismerteti a Windows PowerShell 2.0 motor telepítése.

Windows PowerShell 3.0 visszamenőleg kompatibilis a Windows PowerShell 2.0 tervezték. Parancsmagok, szolgáltatók, beépülő modulok, modulok és a Windows PowerShell 2.0 írt szkriptekkel futtassa változatlan marad, a Windows PowerShell 3.0 és a Windows PowerShell 4.0-s verzióját. Azonban a Microsoft .NET-keretrendszer 4 futásidejű aktiválási házirendben módosulásának eredményeképpen Windows PowerShell gazdagép programok készült Windows PowerShell 2.0-s és a közös nyelvi futtatókörnyezet (CLR) 2.0 lefordított nem futnak a módosítás nélkül később Windows PowerShell-lel, amely CLR-beli 4.0-s lefordított kiadásaiban.

Parancsok és a változtatások által érintett gazdagépen programok előző verziókkal való kompatibilitás megőrzése érdekében, hogy a Windows PowerShell 2.0, a Windows PowerShell 3.0 és a Windows PowerShell 4.0 motorok futtatására lettek kialakítva egymás mellett. Ezenkívül a Windows PowerShell 2.0 motor a Windows Server 2012 R2, Windows 8.1, Windows 8, Windows Server 2012 és Windows Management Framework 3.0 tartalmazza. A Windows PowerShell 2.0 motor kívánják használni, ha egy meglévő parancsfájl vagy a gazdagép program nem futtatható, mert az nem kompatibilis a Windows PowerShell 3.0, a Windows PowerShell 4.0-s vagy a Microsoft .NET-keretrendszer 4. Ezekben az esetekben várhatóan ritkán fordul elő.

A Windows PowerShell 2.0 motor a Windows Server 2012 R2, Windows 8.1, Windows® 8 és Windows Server® 2012 egy opcionális szolgáltatása. A Windows korábbi verzióin Windows Management Framework 3.0 telepítésekor a Windows PowerShell 3.0 telepítés teljesen lecseréli a Windows PowerShell 2.0 telepítése a Windows PowerShell telepítési könyvtárában. Azonban a Windows PowerShell 2.0 motor megfelelően.

További információ a Windows PowerShell 2.0 motor indítása: [a Windows PowerShell 2.0 motor indítása](../getting-started/Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="on-windows-81-and-windows-8"></a>A Windows 8.1 és Windows 8-ban
A Windows 8.1 és Windows 8 a Windows PowerShell 2.0 motor funkció alapértelmezés szerint van kapcsolva. Azonban a használatához szüksége bekapcsolása a Microsoft .NET-keretrendszer 3.5, a lehetőséget, amely van szükség. Ez a szakasz emellett ismerteti a Windows PowerShell 2.0 motor szolgáltatás be- és kikapcsolása.

#### <a name="to-turn-on-net-framework-35"></a>.NET-keretrendszer 3.5 bekapcsolása

1. Az a **Start** írja be **Windows szolgáltatások**.

2. Az a **alkalmazások** sávban kattintson **beállítások**, és kattintson a **kapcsolja be Windows-szolgáltatások be- és kikapcsolása**.

3. Az a **Windows szolgáltatások** kattintson **.NET-keretrendszer 3.5 (tartalmazza a .NET 2.0 és 3.0 verziót** a kiválasztásához.

    Ha bejelöli **.NET-keretrendszer 3.5 (tartalmazza a .NET 2.0 és 3.0 verziót**, a box beírja annak jelzésére, hogy a funkció csak egy része van kiválasztva. Ez azonban a Windows PowerShell 2.0 motor elegendő.

#### <a name="to-turn-the-windows-powershell-20-engine-on-and-off"></a>Az a Windows PowerShell 2.0 motor be- és kikapcsolása

1. Az a **Start** írja be **Windows szolgáltatások**.

2. Az a **alkalmazások** sávban kattintson **beállítások**, és kattintson a **kapcsolja be Windows-szolgáltatások be- és kikapcsolása**.

3. Az a **Windows szolgáltatások** bontsa ki a **Windows PowerShell 2.0** csomópontot, majd kattintson a **Windows PowerShell 2.0 motor** mezőben válassza ki, vagy törölje a jelölést.

## <a name="on-windows-server-2012-r2-and-windows-server-2012"></a>A Windows Server 2012 R2 és Windows Server 2012-ben
A következő eljárásokat követve adja hozzá a Windows PowerShell 2.0 motor és a Microsoft .NET-keretrendszer 3.5 szolgáltatásai. A Windows PowerShell 2.0 motor 2.0.50727 Microsoft .NET-keretrendszer minimális szükséges. Ez a követelmény teljesül, a Microsoft .NET-keretrendszer 3.5-ös verzióját.

#### <a name="to-add-the-net-framework-35-feature"></a>A .NET-keretrendszer 3.5-funkció hozzáadása

1. A **Kiszolgálókezelő**, az a **kezelés** menüjében válassza **szerepkörök és szolgáltatások hozzáadása**.

    Vagy a **Kiszolgálókezelő**, kattintson a **minden kiszolgáló**, és kattintson a jobb gombbal a kiszolgáló nevét, majd válassza ki **szerepkörök és szolgáltatások hozzáadása**.

2. Az a **telepítési típus** lapon jelölje be **szerepköralapú vagy szolgáltatásalapú telepítés**.

3. Az a **funkciók** lapon, bontsa ki a **.NET-keretrendszer 3.5 szolgáltatásai** csomópontra, és válassza **.NET-keretrendszer 3.5 (tartalmazza a .NET 2.0 és 3.0 verziót)**.

    A Windows PowerShell 2.0 motor nem szükségesek, hogy a csomópont alatt a többi beállítást.

#### <a name="to-add-the-windows-powershell-20-engine-feature"></a>A Windows PowerShell 2.0 motor funkció hozzáadása

- A **Kiszolgálókezelő**, az a **kezelés** menüjében válassza **szerepkörök és szolgáltatások hozzáadása**.

    Vagy **Kiszolgálókezelő**, kattintson a **minden kiszolgáló**, és kattintson a jobb gombbal a kiszolgáló nevét, majd válassza ki **szerepkörök és szolgáltatások hozzáadása**.

- Az a **telepítési típus** lapon jelölje be **szerepköralapú vagy szolgáltatásalapú telepítés**.

- Az a **funkciók** lapon, bontsa ki a **Windows PowerShell (telepítve)** csomópontra, és válassza **Windows PowerShell 2.0 motor**.

További információ a Windows PowerShell 2.0 motor indítása: [a Windows PowerShell 2.0 motor indítása](../getting-started/Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="on-earlier-systems"></a>A korábbi rendszerek
A [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkID=293881) csomagot, amely telepíti a Windows 7, Windows Server 2008 R2 és Windows Server 2012, Windows PowerShell 4.0 a Windows PowerShell 2.0 motor tartalmazza. A Windows PowerShell 2.0 motor engedélyezett és készen áll a használatra, akkor, ha szükséges, további telepítési, telepítés és konfiguráció nélkül.

A Windows Management Framework 3.0-csomag, amely telepíti a Windows 7, Windows Server 2008 R2 és Windows Server 2008, Windows PowerShell 3.0 a Windows PowerShell 2.0 motor tartalmazza. A Windows PowerShell 2.0 motor engedélyezett és készen áll a használatra, akkor, ha szükséges, további telepítési, telepítés és konfiguráció nélkül.

## <a name="see-also"></a>Lásd még:
- [Windows PowerShell rendszerkövetelményei](Windows-PowerShell-System-Requirements.md)
- [Windows PowerShell telepítése](Installing-Windows-PowerShell.md)
- [Windows PowerShell indítása](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)
- [A Windows PowerShell 2.0 motor indítása](../getting-started/Starting-the-Windows-PowerShell-2.0-Engine.md)