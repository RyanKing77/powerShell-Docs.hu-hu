---
title: Frissíthető súgó tesztelése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3e064048-2b94-4365-bdb7-f1ee7c0a7fd7
caps.latest.revision: 6
ms.openlocfilehash: f2f319a3cab4b4bd91e9b634dda57d58a6476b62
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845926"
---
# <a name="how-to-test-updatable-help"></a>Frissíthető súgó tesztelése

Ez a témakör ismerteti a frissíthető súgó tesztelését egy modul megközelítést.

## <a name="using-verbose-to-detect-errors"></a>Hibák észlelése részletes használatával

A HelpInfo XML-fájlt, és a CAB-fájlok a modul feltöltés után tesztelheti a fájlok futtatásával egy [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsot a **részletes** paraméter. A **részletes** paraméter arra utasítja a `Update-Help` jelenteni a kritikus lépések a műveletek, az olvasó a **HelpInfoUri** kulcsfontosságú a moduljegyzékben, hogy a fájltípus esetében a kicsomagolt CAB-fájl és a nyelvspecifikus modulkönyvtárat helyezi el a fájlokat.
A HelpInfo XML-fájlt, és a CAB-fájlok a modul feltöltés után tesztelheti a fájlok futtatásával egy [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsot a **részletes** paraméter. A **részletes** paraméter arra utasítja a `Update-Help` jelenteni a kritikus lépések a műveletek, az olvasó a **HelpInfoUri** kulcsfontosságú a moduljegyzékben, hogy a fájltípus esetében a kicsomagolt CAB-fájl és a nyelvspecifikus modulkönyvtárat helyezi el a fájlokat.

Ha az összes részletes üzenetek oldva, futtassa egy `Update-Help` parancsot a **Debug** paraméter. Ezt a paramétert kell talált a frissíthető Súgó fájlok fennmaradó hibát.