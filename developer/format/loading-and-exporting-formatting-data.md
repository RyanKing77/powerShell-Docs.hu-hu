---
title: Be- és az adatok formázási exportálása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2a48de31-7961-4b0e-b58b-93466e38370b
caps.latest.revision: 6
ms.openlocfilehash: 86a0e8b7e8967280daa57faf5c323efcd3b1368b
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57794195"
---
# <a name="loading-and-exporting-formatting-data"></a>Formázási adatok betöltése és exportálása

Miután létrehozta a formázási fájlt, a fájlok betöltése az aktuális munkamenetbe által az adatok formázása a munkamenet frissíteni szeretné. (A Windows PowerShell által biztosított formázási fájlokat a rendszer betölti az aktuális munkamenet megnyitásakor regisztrált beépülő modulok által.) Az adatok formázása az aktuális munkamenet frissül, ha Windows PowerShell az adatok használatával a .NET-objektumokat a meghatározott formázási betöltött fájlok nézetek társított jeleníti meg. Nincs a jelenlegi munkamenet betölthetnek formázási fájlok száma nincs korlátozva. Vissza a formázási fájlt a jelenlegi munkamenet mellett a formázási adatok frissítése, exportálhatja az adatok formázása.

## <a name="loading-format-data"></a>Formátum az adatok betöltésekor

Formázási fájlok tölthetők be az aktuális munkamenet a következő módszerekkel:

- A formázási fájl importálhatja az aktuális munkamenet a parancssorból. Használja a [Update-FormatData](/powershell/module/Microsoft.PowerShell.Utility/Update-FormatData) parancsmag az alábbi eljárásban leírtak szerint.

- Egy moduljegyzék a formázási fájlra hivatkozó hozhat létre. Modulok lehetővé teszik, hogy a csomag, terjesztési fájlok formázása. Használja a [New-ModuleManifest](/powershell/module/Microsoft.PowerShell.Core/New-ModuleManifest) parancsmagot a jegyzék létrehozásához és a [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) parancsmagot, hogy a modul betöltse az aktuális munkamenet. Modulok kapcsolatos további információkért lásd: [Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md).

- Létrehozhat egy beépülő modult a formázási fájlra hivatkozik. Használja a [System.Management.Automation.Pssnapin.Formats](/dotnet/api/System.Management.Automation.PSSnapIn.Formats) való hivatkozáshoz a formázási fájlokat. Erősen javasolt modulok csomag parancsmagok, és minden kapcsolódó formázás és típusú fájlok terjesztés. Modulok kapcsolatos további információkért lásd: [Windows PowerShell-modul írása](../module/writing-a-windows-powershell-module.md).

- Ha programozott módon meghívott parancsok, ahol a parancsok futtatása a futási térben kezdeti munkamenet állapota is hozzáadhat egy formázási fájlbejegyzés. Adja hozzá a formázási használt .NET típusára vonatkozó további információkért lásd: a [System.Management.Automation.Runspaces.Sessionstateformatentry? Displayproperty = Fullname](/dotnet/api/System.Management.Automation.Runspaces.SessionStateFormatEntry) osztály.

Amikor egy formázási fájl betöltődik, megjelenik egy belső listához, hogy akkor Windows PowerShell segítségével határozza meg, amely megjelenítése során használatos évformátum meghatározása az objektumok a parancssorból. Ön is a formázási fájlt a lista elejére jogosultságokat, vagy hozzáfűzheti a lista végére. Ahol a formázási fájl kerül a listában, hogy akkor fontos, ha formázási fájlt, amely meghatározza egy olyan objektum, amely rendelkezik definiált, például ha szeretne módosítani, hogyan történik a Windows PowerShell core a parancsmag által visszaadott objektum egy meglévő nézethez megtekintése betöltés  jelenik meg. Ha egy formázási fájlt, amely meghatározza az objektum nézetben tölt be, a korábban ismertetett módszerek bármelyikét használhatja.  Ha tölt be egy formázási fájlt, amely meghatározza az objektum egy másik nézetre, kell használnia a [Update-FormatData](/powershell/module/Microsoft.PowerShell.Utility/Update-FormatData) parancsmag és jogosultságokat a fájlt, hogy a lista elejére.

## <a name="storing-your-formatting-file"></a>A formázási fájl tárolásához

Esetében nem követelmény a lemezen a formázási fájlok tárolására. Azonban erősen ajánlott, hogy tárolja ezeket a következő mappában: `user\documents\windowspowershell\`

#### <a name="loading-a-format-file-using-import-formatdata"></a>Importálás – FormatData használatával formátumfájlt betöltése

1. A formázási fájl lemezre Store.

2. Futtassa a [Update-FormatData](/powershell/module/Microsoft.PowerShell.Utility/Update-FormatData) parancsmag használatával a következő parancsok egyikét.

   Ez a parancs használatával adja hozzá a formázás fájlt a lista elejére. Hogyan jelenik meg az objektum módosítani, használja ezt a parancsot.

   ```powershell
   Update-FormatData -PrependPath PathToFormattingFile
   ```

   Ez a parancs használatával adja hozzá a formázás fájlt a lista végére.

   ```powershell
   Update-FormatData -AppendPath PathToFormattingFile
   ```

   Miután hozzáadta a fájlok a [Update-FormatData](/powershell/module/Microsoft.PowerShell.Utility/Update-FormatData) parancsmag nem távolítható el a fájlt a listából a munkamenet meg van nyitva. Zárja be a munkamenet a formázási fájl eltávolítása a listából.

## <a name="exporting-format-data"></a>Formátum az adatok exportálása

A szakasz szövegtörzsét itt.
