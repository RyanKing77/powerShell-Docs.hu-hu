---
ms.date: 06/12/2018
keywords: WMF, powershell, beállítás
title: A Windows Management Framework (WMF)
ms.openlocfilehash: 17011f88c364cb56a0c87f092873ccd99db450bc
ms.sourcegitcommit: 68093cc12a7a22c53d11ce7d33c18622921a0dd1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/26/2018
ms.locfileid: "36940391"
---
# <a name="windows-management-framework"></a>Windows Management Framework

A Windows Management Framework (WMF) egységes felületet biztosít a Windows. WMF zökkenőmentes megoldást egy Windows ügyfél és a Windows Server-verziók kezelése. WMF csomagok felügyeleti funkció frissítéseket tartalmaznak, és a Windows korábbi verziói érhetők el.

A WMF telepítése hozzáadja és/vagy az alábbi szolgáltatások frissítéseket:

- Windows PowerShell
- Windows PowerShell célállapot konfiguráló szolgáltatása (DSC)
- A Windows PowerShell integrált parancsfájl-környezet (ISE)
- Rendszerfelügyeleti webszolgáltatások (WinRM)
- Windows Management Instrumentation (WMI)
- A Windows PowerShell webszolgáltatások (felügyeleti OData IIS kiterjesztés)
- Szoftverleltár-naplózás (SIL)
- A Kiszolgálókezelő CIM-szolgáltatót

## <a name="wmf-release-notes"></a>WMF kibocsátási megjegyzései

A PowerShell és egyéb egy adott WMF összetevői különböző fejlesztések kapcsolatos információkért olvassa el az alábbi hivatkozásokat követve tekintse át a kibocsátási megjegyzések:

- [WMF 5.1](5.1/release-notes.md)
- [WMF 5.0](5.0/releasenotes.md)
- [WMF 4.0](https://download.microsoft.com/download/3/D/6/3D61D262-8549-4769-A660-230B67E15B25/Windows%20Management%20Framework%204%200%20Release%20Notes.docx)
- [A WMF 3.0](https://download.microsoft.com/download/E/7/6/E76850B8-DA6E-4FF5-8CCE-A24FC513FD16/WMF%203%20Release%20Notes.docx)

## <a name="wmf-availability-across-windows-operating-systems"></a>WMF elérhetőségét a Windows operációs rendszerek

|Operációs rendszer verziója  |[WMF 5.1][] |[WMF 5.0][] |[WMF 4.0][] |[A WMF 3.0][]  |[WMF 2.0][] |
|--------------------------|------------|------------|------------|-------------|------------|
|Windows Server 2016       |Beépített hajók|            |            |             |            |
|Windows-10                |Beépített hajók|Beépített hajók|            |             |            |
|Windows Server 2012 R2    |Igen         |Igen         |Beépített hajók|             |            |
|A Windows 8.1               |Igen         |Igen         |Beépített hajók|             |            |
|Windows Server 2012       |Igen         |Igen         |Igen         |Beépített hajók |            |
|Windows 8                 |            |            |            |Beépített hajók |            |
|Windows Server 2008 R2 SP1|Igen         |Igen         |Igen         |Igen          |Beépített hajók|
|Windows 7 SP1             |Igen         |Igen         |Igen         |Igen          |Beépített hajók|
|Windows Server 2008 SP2   |            |            |            |Igen          |Igen         |
|Windows Vista             |            |            |            |             |Igen         |
|Windows Server 2003       |            |            |            |             |Igen         |
|Windows XP                |            |            |            |Igen          |            |

**A beépített azonban**: WMF megadott verzióját, a szolgáltatások a Windows ügyfél vagy a Windows Server jelzett verziójában szállítási.

[WMF 5.1]: https://aka.ms/wmf51download
[WMF 5.0]: https://aka.ms/wmf5download
[WMF 4.0]: https://aka.ms/wmf4download
[A WMF 3.0]: https://aka.ms/wmf3download
[WMF 2.0]: https://aka.ms/wmf2download
