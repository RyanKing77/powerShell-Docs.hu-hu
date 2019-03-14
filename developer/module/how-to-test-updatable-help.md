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
ms.openlocfilehash: cecc6c26ccaece06462ddd74b53534137fcf3037
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794263"
---
# <a name="how-to-test-updatable-help"></a>Frissíthető súgó tesztelése

Ez a témakör ismerteti a frissíthető súgó tesztelését egy modul megközelítést.

## <a name="using-verbose-to-detect-errors"></a>Hibák észlelése részletes használatával

A HelpInfo XML-fájlt, és a CAB-fájlok a modul feltöltés után tesztelheti a fájlok futtatásával egy [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsot a **részletes** paraméter. A **részletes** paraméter arra utasítja a `Update-Help` jelenteni a kritikus lépések a műveletek, az olvasó a **HelpInfoUri** kulcsfontosságú a moduljegyzékben, hogy a fájltípus esetében a kicsomagolt CAB-fájl és a nyelvspecifikus modulkönyvtárat helyezi el a fájlokat.

Ha az összes részletes üzenetek oldva, futtassa egy `Update-Help` parancsot a **Debug** paraméter. Ezt a paramétert kell talált a frissíthető Súgó fájlok fennmaradó hibát.