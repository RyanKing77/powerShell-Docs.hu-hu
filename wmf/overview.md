---
ms.date: 06/12/2018
keywords: WMF, powershell, beállítás
title: Windows Management Framework (WMF)
ms.openlocfilehash: f279f975527dc198dd9b47ca1dc4258f54fafef5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684436"
---
# <a name="windows-management-framework"></a>Windows Management Framework

Windows Management Framework (WMF) konzisztens felügyeleti felületet biztosít a Windows. A WMF Windows ügyfél és a Windows Server-verziók kezelése egy zökkenőmentes megoldást kínál. WMF-telepítési csomagok kezelőfunkciók frissítéseket tartalmaznak, és a Windows korábbi verziói érhetők el.

A WMF telepítése hozzáadja és/vagy frissíti a következő funkciókat:

- Windows PowerShell
- Windows PowerShell célállapot konfiguráló szolgáltatása (DSC)
- Windows PowerShell integrált parancsfájl-környezet (ISE)
- Rendszerfelügyeleti webszolgáltatások (WinRM)
- Windows Management Instrumentation (WMI)
- Windows PowerShell webszolgáltatások (felügyeleti OData IIS kiterjesztés)
- Szoftverleltár-naplózás (SIL)
- A Kiszolgálókezelő CIM-szolgáltatót

## <a name="wmf-release-notes"></a>A WMF kibocsátási megjegyzései

Számos bővítést tartalmaz, a PowerShell és más összetevőket egy adott WMF kapcsolatos további információkért tekintse meg az alábbi forrásokban, tekintse át a kibocsátási megjegyzések:

- [WMF 5.1](5.1/release-notes.md)
- [WMF 5.0](5.0/releasenotes.md)
- [WMF 4.0](https://download.microsoft.com/download/3/D/6/3D61D262-8549-4769-A660-230B67E15B25/Windows%20Management%20Framework%204%200%20Release%20Notes.docx)
- [WMF 3.0](https://download.microsoft.com/download/E/7/6/E76850B8-DA6E-4FF5-8CCE-A24FC513FD16/WMF%203%20Release%20Notes.docx)

## <a name="wmf-availability-across-windows-operating-systems"></a>A WMF rendelkezésre állása a Windows operációs rendszerek

|Operációs rendszer verziója  |[WMF 5.1][] |[WMF 5.0][] |[WMF 4.0][] |[WMF 3.0][]  |[A WMF 2.0][] |
|--------------------------|------------|------------|------------|-------------|------------|
|Windows Server 2019       |Beépített részeként szerezhető be|            |            |             |            |
|Windows Server 2016       |Beépített részeként szerezhető be|            |            |             |            |
|Windows 10                |Beépített részeként szerezhető be|Beépített részeként szerezhető be|            |             |            |
|Windows Server 2012 R2    |Igen         |Igen         |Beépített részeként szerezhető be|             |            |
|Windows 8.1               |Igen         |Igen         |Beépített részeként szerezhető be|             |            |
|Windows Server 2012       |Igen         |Igen         |Igen         |Beépített részeként szerezhető be |            |
|Windows 8                 |            |            |            |Beépített részeként szerezhető be |            |
|Windows Server 2008 R2 SP1|Igen         |Igen         |Igen         |Igen          |Beépített részeként szerezhető be|
|Windows 7 SP1             |Igen         |Igen         |Igen         |Igen          |Beépített részeként szerezhető be|
|Windows Server 2008 SP2   |            |            |            |Igen          |Igen         |
|Windows Vista             |            |            |            |             |Igen         |
|Windows Server 2003       |            |            |            |             |Igen         |
|Windows XP                |            |            |            |Igen          |            |

**A beépített mobilplatform**: A megadott verzióját, a WMF funkcióját Windows ügyfél- vagy Windows Server jelzett verziójában voltak Önnek.

[WMF 5.1]: https://aka.ms/wmf51download
[WMF 5.0]: https://aka.ms/wmf5download
[WMF 4.0]: https://aka.ms/wmf4download
[WMF 3.0]: https://aka.ms/wmf3download
[A WMF 2.0]: https://aka.ms/wmf2download
