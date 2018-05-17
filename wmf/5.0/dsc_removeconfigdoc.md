---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: af16ce7c5d97731581aa3393a70aba672244c9d8
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="remove-dsc-documents"></a>A DSC-dokumentumok törlése

Amikor egy konfigurációs dokumentum DSC érkeznek, a dokumentum végighalad különböző szakaszaiban (függőben lévő, aktuális, előző). A DSC-ből a Windows PowerShell 4.0, azt hozzá egy új parancsmagot `Remove-DscConfigurationDocument`, részeként [2014. novemberben kiadott kumulatív frissítés a Windows RT 8.1, Windows 8.1 és Windows Server 2012 R2](https://support.microsoft.com/kb/3000850).
