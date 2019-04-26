---
ms.date: 04/19/2019
keywords: WMF, powershell, beállítás
title: Windows Management Framework (WMF)
ms.openlocfilehash: 6d25b4025bbc86f6be0e5c74db9f1fbe6705d816
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62055445"
---
# <a name="windows-management-framework"></a>Windows Management Framework

Windows Management Framework (WMF) konzisztens felügyeleti felületet biztosít a Windows. A WMF Windows ügyfél és a Windows Server-verziók kezelése egy zökkenőmentes megoldást kínál. WMF-telepítési csomagok kezelőfunkciók frissítéseket tartalmaznak, és a Windows korábbi verziói érhetők el.

A WMF telepítése hozzáadja és/vagy frissíti a következő funkciókat:

- Windows PowerShell
- Windows PowerShell Desired State Configuration (DSC)
- Windows PowerShell integrált parancsfájl-környezet (ISE)
- Windows Rendszerfelügyeleti (webszolgáltatások WinRM)
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

|        Operációs rendszer verziója         | [WMF 5.1][]  | WMF 5.0<br>*Nem támogatott* | [WMF 4.0][]  | [WMF 3.0][]  | [A WMF 2.0][]  |
| --------------------------------------- | ------------ | --------------------------- | ------------ | ------------ | ------------ |
| A Windows Server 2019                     | Beépített részeként szerezhető be |                             |              |              |              |
| Windows Server 2016                     | Beépített részeként szerezhető be |                             |              |              |              |
| Windows 10                              | Beépített részeként szerezhető be | Beépített részeként szerezhető be                |              |              |              |
| Windows Server 2012 R2                  | Igen          | Igen                         | Beépített részeként szerezhető be |              |              |
| Windows 8.1                             | Igen          | Igen                         | Beépített részeként szerezhető be |              |              |
| Windows Server 2012                     | Igen          | Igen                         | Igen          | Beépített részeként szerezhető be |              |
| Windows 8<br>*Nem támogatott*           |              |                             |              | Beépített részeként szerezhető be |              |
| Windows Server 2008 R2 SP1              | Igen          | Igen                         | Igen          | Igen          | Beépített részeként szerezhető be |
| Windows 7 SP1                           | Igen          | Igen                         | Igen          | Igen          | Beépített részeként szerezhető be |
| Windows Server 2008 SP2                 |              |                             |              | Igen          | Igen          |
| Windows Vista<br>*Nem támogatott*       |              |                             |              |              | Igen          |
| Windows Server 2003<br>*Nem támogatott* |              |                             |              |              | Igen          |
| Windows XP<br>*Nem támogatott*          |              |                             |              | Igen          | Igen          |

- **A beépített mobilplatform**: A megadott verzióját, a WMF funkcióját Windows ügyfél- vagy Windows Server jelzett verziójában voltak Önnek.
- **Nem támogatott**: Ezeket a termékeket a Microsoft már nem támogatottak. Frissítenie kell egy új verzióra támogatott. További információkért lásd: a [A Microsoft életciklus-szabályzat][] lapot.

> [!NOTE]
> A telepítő a WMF 5.0, már nem érhető el vagy nem támogatott. A WMF 5.1 váltotta fel.

[A Microsoft életciklus-szabályzat]: https://support.microsoft.com/lifecycle
[WMF 5.1]: https://aka.ms/wmf51download
[WMF 4.0]: https://aka.ms/wmf4download
[WMF 3.0]: https://aka.ms/wmf3download
[A WMF 2.0]: https://aka.ms/wmf2download
