---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: A Windows Management Framework (WMF)
ms.openlocfilehash: ae50e8d1495d7075163714ed873940d2d1d19b8e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="windows-management-framework"></a>Windows Management Framework

A Windows Management Framework (WMF) a kézbesítési mechanizmus, amely egységes felügyeleti felületet biztosít a különböző változatban is elkészíti a Windows és Windows Server között.
A WMF telepítése az ügyfelek közötti operációs rendszer a környezetükben keverékei együttműködését zavartalanul beolvasása.
WMF elérhetővé teszi a frissítések az felügyeleti funkciót, a Windows és Windows Server, az adott kiadás a Windows és Windows Server korábbi verzióin (általában 2 alacsonyabb verzió) telepítéséhez.

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

| Operációs rendszer verziója | [WMF 5.1](https://aka.ms/wmf51download) | [WMF 5.0](https://aka.ms/wmf5download) | [WMF 4.0](https://aka.ms/wmf4download) |  [A WMF 3.0](https://aka.ms/wmf3download) | [WMF 2.0](https://aka.ms/wmf2download) |
| ------------------------ | ----------- | ----------- | ----------- | ------------ |  ------------- |
| Windows Server 2016 | Beépített hajók |  |  |  |  |
| Windows-10 | Beépített hajók | Beépített hajók  | | | |
| Windows Server 2012 R2| Igen | Igen | Beépített hajók |  |  |
| A Windows 8.1 | Igen | Igen |  Beépített hajók |  |  |
| Windows Server 2012 | Igen | Igen | Igen |  Beépített hajók | |
| Windows 8 |  |  |  | Beépített hajók | |
| Windows Server 2008 R2 SP1 | Igen | Igen | Igen |  Igen| Beépített hajók |
| Windows 7 SP1  | Igen | Igen | Igen | Igen | Beépített hajók |
| Windows Server 2008 SP2 | | | | Igen | Igen |
| Windows Vista | | | | | Igen |
| Windows Server 2003| | | |  | Igen |
| Windows XP | | | |  | Igen |

**"Érhető el a beépített"**: az funkcióit a `specified WMF` Windows és Windows Server jelzett verziójában szállítási.
Emiatt a `specified WMF` nem kell telepíteni a jelzett, telepített operációs rendszereken.
