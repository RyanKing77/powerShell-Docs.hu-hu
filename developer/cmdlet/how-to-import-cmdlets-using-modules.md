---
title: Parancsmagok importálása modulok használatával | Microsoft Docs
ms.custom: ''
ms.date: 08/28/2019
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a41d9e5f-de6f-47b7-9601-c108609320d0
caps.latest.revision: 8
ms.openlocfilehash: 2f145795a57c988da0cb4ed294142aa141c53cae
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215273"
---
# <a name="how-to-import-cmdlets-using-modules"></a>Parancsmagok importálása modulokkal

Ez a cikk azt ismerteti, hogyan lehet parancsmagokat importálni egy PowerShell-munkamenetbe egy bináris modul használatával.

> [!NOTE]
> A modulok tagjai lehetnek parancsmagok, szolgáltatók, függvények, változók, aliasok és sok más. A beépülő modulok csak parancsmagokat és szolgáltatókat tartalmazhatnak.

## <a name="how-to-load-cmdlets-using-a-module"></a>Parancsmagok betöltése modul használatával

1. Hozzon létre egy modul-mappát, amelynek a neve megegyezik azzal a szerelvény-fájllal, amelyben a parancsmagok implementálva vannak. Ebben az eljárásban a modul mappáját a Windows mappában hozza `system32` létre a rendszer.

   `%SystemRoot%\system32\WindowsPowerShell\v1.0\Modules\mymodule`

1. Győződjön meg arról, `PSModulePath` hogy a környezeti változó tartalmazza az új modul mappájának elérési útját. Alapértelmezés szerint a rendszer mappa már hozzá van adva a `PSModulePath` környezeti változóhoz. A (z `PSModulePath`) megtekintéséhez írja `$env:PSModulePath`be a következőt:.

1. Másolja a parancsmag szerelvényt a modul mappájába.

1. Adjon hozzá egy modul manifest-`.psd1`fájlt () a modul gyökérkönyvtárában. A PowerShell a modul jegyzékfájlját használja a modul importálásához. További információ: [a PowerShell-modul írása](../module/how-to-write-a-powershell-module-manifest.md).

1. Futtassa a következő parancsot a parancsmagok a munkamenethez való hozzáadásához:

   `Import-Module [Module_Name]`

   Ez az eljárás használható a parancsmagok tesztelésére. Hozzáadja a szerelvényben található összes parancsmagot a munkamenethez. A modulokkal kapcsolatos további információkért lásd: [Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md).

## <a name="see-also"></a>Lásd még:

[PowerShell-modul jegyzékének írása](../module/how-to-write-a-powershell-module-manifest.md)

[PowerShell-modul importálása](../module/importing-a-powershell-module.md)

[Importálás – modul](/powershell/module/Microsoft.PowerShell.Core/Import-Module)

[Modulok telepítése](../module/installing-a-powershell-module.md)

[A PSModulePath telepítési útvonalának módosítása](../module/modifying-the-psmodulepath-installation-path.md)

[Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
