---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, powershell, a parancsmag, psgallery, psget"
title: "A PowerShell-galériában"
ms.openlocfilehash: 9fe341e4b297764321f3b3f07caca8ef4b8b40e0
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/13/2017
---
# <a name="the-powershell-gallery"></a>A PowerShell-galériában

A PowerShell-galériában PowerShell tartalom központi tárháza. Új PowerShell-parancsok vagy a kívánt állapot konfigurációs szolgáltatása (DSC) erőforrások a gyűjteményben található.

## <a name="powershellget-overview"></a>PowerShellGet áttekintése

A PowerShellGet modul tartalmaz parancsmagokat a felderítése, telepítése, frissítése és PowerShell összetevők, például a modulok, a DSC-erőforrások, a szerepkör képességek és a parancsfájlokat a közzététel a [PowerShell-galériában](https://www.PowerShellGallery.com) és egyéb magánhálózatokon tárházak találhatók.

## <a name="getting-started-with-the-gallery"></a>A gyűjtemény első lépések

Elemet a gyűjteményből telepítéséhez a PowerShellGet modul, amely megtalálható a Windows 10, Windows Management Framework (WMF) 5.0 vagy az MSI-alapú telepítő (a PowerShell 3. és 4) a legújabb verzióra.

- [**Windows 10 beolvasása**](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409),
- [**WMF 5.0 beolvasása**](http://go.microsoft.com/fwlink/?LinkId=398175), vagy
- [**Az MSI telepítő beolvasása**](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

A legújabb [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) modulban is:

-   A gyűjtemény elemeinek keresztül keresési [keresés-modul](https://go.microsoft.com/fwlink/?LinkId=821658) és [keresés-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822322)
-   A rendszer a gyűjteményből elemek mentése [mentés-modul](https://go.microsoft.com/fwlink/?LinkId=821669) és [mentés-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822334)
-   A gyűjtemény elemeinek telepítéséhez [Install-modul](https://go.microsoft.com/fwlink/?LinkId=821663) és [telepítési-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822327)
-   Elemek feltöltése a gyűjteményébe [Publish-modul](https://go.microsoft.com/fwlink/?LinkId=821666) és [Publish-parancsfájl](https://go.microsoft.com/fwlink/?LinkId=822331)
-   Adja hozzá a saját egyéni tárház [Register-PSRepository](https://go.microsoft.com/fwlink/?LinkId=821668)

Tekintse meg a [bevezetés](psgallery/psgallery_gettingstarted.md) oldalon olvashat PowerShellGet parancsok használata a gyűjteményben. Is futtathatja *Update-Help-modul PowerShellGet* parancsok helyi súgó telepítése.

## <a name="supported-operating-systems"></a>Támogatott operációs rendszerek

A **PowerShellGet** module használatához **PowerShell 3.0-s vagy újabb**.

Ezért **PowerShellGet** a következő operációs rendszerek egyike szükséges:

- Windows-10
- Windows 8.1 Pro
- Windows 8.1 Enterprise
- Windows 7 SP1
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2008 R2 SP1

**PowerShellGet** is szükséges a .NET-keretrendszer 4.5 vagy újabb. Telepítheti a .NET-keretrendszer 4.5 vagy újabb a [Itt](https://msdn.microsoft.com/en-us/library/5a4x27ek.aspx).


## <a name="got-a-question-have-feedback"></a>A kapott a következő kérdést? Van?

További információ a PowerShell-galériában és PowerShellGet megtalálhatók a [bevezetés](psgallery/psgallery_gettingstarted.md) lap. Adja meg a visszajelzések és a jelentés kapcsolatos problémákat [UserVoice](http://windowsserver.uservoice.com/forums/301869-powershell).

