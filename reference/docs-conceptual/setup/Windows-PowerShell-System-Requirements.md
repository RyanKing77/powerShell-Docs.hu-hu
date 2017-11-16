---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Windows PowerShell rendszerkövetelményei"
ms.assetid: 6d1d3c75-3be4-4fc9-8805-ca9b2c454d42
ms.openlocfilehash: 33824eac4de28de97990ffa1ea2500e61e03e847
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2017
---
# <a name="windows-powershell-system-requirements"></a>Windows PowerShell rendszerkövetelményei
Ez a témakör a Windows PowerShell 3.0, a Windows PowerShell 4.0-s verzióját és a Windows PowerShell 5.0, valamint a speciális funkciók, például a Windows PowerShell integrált parancsfájlkezelési környezet (ISE), a CIM-parancsok és a munkafolyamatok rendszerkövetelményeit ismerteti.

Windows® 8.1 és Windows Server® 2012 R2 tartalmazzák az összes szükséges programokat. Ez a témakör célja a felhasználók számára a Windows korábbi verzióiban.

## <a name="operating-system-requirements"></a>Operációs rendszerre vonatkozó követelmények
A Windows PowerShell 5.0 futtatja a következő Windows-verziókban.

- Windows Server 2016-os, alapértelmezés szerint telepítve

- Telepítse a Windows Server 2012 R2-ben [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) futtatásához a Windows PowerShell 5.0

- Telepítse a Windows Server 2012-ben [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) futtatásához a Windows PowerShell 5.0

- Windows Server 2008 R2 Service Pack 1 telepítése [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) futtatásához a Windows PowerShell 5.0

- A Windows 8.1

- Windows 7 Service Pack 1 telepítése [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) futtatásához a Windows PowerShell 5.0

Windows PowerShell 4.0-s verzióját futtatja, a következő Windows-verziókban.

- Windows 8.1, alapértelmezés szerint telepítve

- Windows Server 2012 R2 rendszerben alapértelmezés szerint telepítve

- Windows® 7 Service Pack 1 telepítése [Windows Management Framework 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) futtatásához a Windows PowerShell 4.0

- A Windows Server® 2008 R2 Service Pack 1 telepítése [Windows Management Framework 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) futtatásához a Windows PowerShell 4.0

A Windows PowerShell 3.0 fut, a következő Windows-verziókban.

- Windows 8, alapértelmezés szerint telepítve

- Windows Server 2012 rendszerben alapértelmezés szerint telepítve

- Windows® 7 Service Pack 1 telepítése [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) futtatásához a Windows PowerShell 3.0

- A Windows Server® 2008 R2 Service Pack 1 telepítése [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) futtatásához a Windows PowerShell 3.0

- Telepítse a Windows Server 2008 Service Pack 2 [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) futtatásához a Windows PowerShell 3.0

## <a name="microsoft-net-framework-requirements"></a>A Microsoft .NET-keretrendszer követelményei
A Windows PowerShell 5.0 a Microsoft .NET-keretrendszer 4.5 teljes telepítése szükséges. Windows 8.1 és Windows Server 2012 R2 tartalmazza a Microsoft .NET-keretrendszer 4.5 alapértelmezés szerint.

A Windows PowerShell 4.0-s verzióját a Microsoft .NET-keretrendszer 4.5 teljes telepítése szükséges. Windows 8.1 és Windows Server 2012 R2 tartalmazza a Microsoft .NET-keretrendszer 4.5 alapértelmezés szerint.

A Windows PowerShell 3.0 a Microsoft .NET-keretrendszer 4 teljes telepítése szükséges. Windows 8 és Windows Server 2012 tartalmazza a Microsoft .NET-keretrendszer 4.5 alapértelmezés szerint ennek a követelménynek megfelel.

A Microsoft .NET-keretrendszer 4.5 (dotNetFx45_Full_setup.exe) telepítéséhez tekintse át [Microsoft .NET-keretrendszer 4.5](http://go.microsoft.com/fwlink/?LinkID=242919) a Microsoft Download Center.

A Microsoft .NET-keretrendszer 4 (dotNetFx40_Full_setup.exe) teljes verziójának telepítéséhez tekintse át [Microsoft .NET-keretrendszer 4 (webes telepítő)](http://go.microsoft.com/fwlink/?LinkID=212931) a Microsoft Download Center.

## <a name="windows-management-framework-40"></a>A Windows Management Framework 4.0
A Windows PowerShell 5.0 Windows Management Framework 4.0 a Windows Server 2008 R2 SP1 és Windows 7 SP1 előtelepítve igényel.

## <a name="ws-management-30"></a>WS-Management 3.0
A Windows PowerShell 3.0 és a Windows PowerShell 4.0 szükséges a WS-Management 3.0, amely támogatja a WinRM szolgáltatás és a WSMan-protokollt. A program a Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0 és a Windows Management Framework 3.0 része.

## <a name="windows-management-instrumentation-30"></a>A Windows Management Instrumentation 3.0
A Windows PowerShell 3.0 és a Windows PowerShell 4.0 szükséges Windows Management Instrumentation (3.0 WMI). A program a Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0 és a Windows Management Framework 3.0 része. Ha a program nincs telepítve a számítógépen, a CIM-parancsok, például WMI, igénylő szolgáltatások nem működnek.

## <a name="common-language-runtime-40"></a>Közös nyelvi futtatókörnyezet 4.0
A Windows PowerShell 3.0, a Windows PowerShell 4.0-s verzióját és a Windows PowerShell 5.0 összeállítása elleni közös nyelvi futtatókörnyezetet (CLR) 4.0-s verzióját.

## <a name="graphical-user-interface-requirements"></a>Grafikus felhasználói felület követelmények
A Windows PowerShell egy konzol alapú alkalmazás, amely a grafikus felhasználói felületen nincs szükség. Ilyen van azt alkalmas arra, hogy képernyőkön vagy figyelők, vagy egy felhasználói felülethez, például a Windows Server 2012 R2 vagy Windows Server 2012 Server Core telepítési lehetőségekkel nem rendelkező számítógépek.

Azonban egyes elemek, például a következő kötelező, grafikus felhasználói felületen. További információkért lásd: az egyes elemekhez tartozó súgó-témakör.

- Windows PowerShell integrált parancsfájlkezelési környezet (ISE)

- Parancsmagok

    1.  [A GridView nézet out](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-gridview)

    2.  [A parancs megjelenítése](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Utility/Show-Command)

    3.  [Megjelenítése-ControlPanelItem](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Management/Show-ControlPanelItem)

    4.  [Az eseménynaplóban megjelenítése](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Management/Show-EventLog)

- Paraméterek

    1.  **ShowWindow** paramétere a [Get-Help](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Get-Help) parancsmag.

    2.  **ShowSecurityDescriptorUI** paramétere a [Register-PSSessionConfiguration](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Register-PSSessionConfiguration) és [Set-PSSessionConfiguration](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Set-PSSessionConfiguration) parancsmagok.

## <a name="windows-powershell-engine-requirements"></a>A Windows PowerShell-motor kapcsolatos követelmények
A Windows PowerShell 4.0 a visszamenőleges kompatibilitás érdekében a Windows PowerShell 3.0 és a Windows PowerShell 2.0 célja. Parancsmagok, a szolgáltatók, a beépülő modulok, a modulok és a parancsfájlokat a Windows PowerShell 2.0-s és a Windows PowerShell 3.0 futtassa a Windows PowerShell 4.0 változatlan.

Azonban módosulásának eredményeképpen a futásidejű aktiválási házirend a Microsoft .NET-keretrendszer 4-es, Windows PowerShell gazdagépre programok az Windows PowerShell 2.0-s verziójához és a közös nyelvi futtatókörnyezet (CLR) 2.0 fordítása nem futtatható a Windows rendszerben módosítás nélkül A CLR-beli 4.0-s fordítását, akkor a PowerShell 3.0.

A Windows PowerShell 2.0 motor 2.0.50727 Microsoft .NET-keretrendszer minimális szükséges. Ez a követelmény teljesül, a Microsoft .NET Framework 3.5 Service Pack 1 által. Ez a követelmény nem teljesül, a Microsoft .NET-keretrendszer 4-es és újabb verziókban a Microsoft .NET-keretrendszer.

Hozzáadása a Windows PowerShell 2.0 motor telepítése és felvétele vagy a Microsoft .NET-keretrendszer szükséges verzióinak telepítésével kapcsolatos információkért lásd: [telepítése a Windows PowerShell 2.0 motor](Installing-the-Windows-PowerShell-2.0-Engine.md). További információ a Windows PowerShell 2.0 motor: [indítása a Windows PowerShell 2.0 motor](Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="windows-preinstallation-environment"></a>Windows előtelepítési környezet
A Windows PowerShell 2.0, a Windows PowerShell 3.0 és a Windows PowerShell 4.0 futtassa a Windows előtelepítési környezetben (Windows PE). A következő parancsmagok azonban nem támogatott.

- [Háttérben futó intelligens átviteli szolgáltatás (BITS) parancsmagok](http://go.microsoft.com/fwlink/?LinkId=257514)

- [Get-Eseménynapló](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Management/Get-EventLog)

- [Get-WinEvent parancsmaggal](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent)

- [Save-Help](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Save-Help)

- [Update-Help](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Update-Help)

Emellett a **WinRM** szolgáltatás nincs jelen a Windows PE környezetben.

## <a name="see-also"></a>Lásd még:
- [Bevezetés a Windows PowerShell használatával](../getting-started/Getting-Started-with-Windows-PowerShell.md)
- [Windows PowerShell telepítése](Installing-Windows-PowerShell.md)
- [A Windows PowerShell indítása](Starting-Windows-PowerShell.md)

