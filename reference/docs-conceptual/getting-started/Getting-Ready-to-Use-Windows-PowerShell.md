---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Felkészülés a Windows PowerShell használatával"
ms.assetid: 6dc7052d-cc5a-4220-950f-98f963a2b587
ms.openlocfilehash: de09c74e938f11a130864b1620d6c169006a27be
ms.sourcegitcommit: 4807ab554d55fdee499980835bcc279368b1df68
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 11/07/2017
---
# <a name="getting-ready-to-use-windows-powershell"></a>Felkészülés a Windows PowerShell használatával
A Windows PowerShell telepítése és elindítása, vegye figyelembe a következő telepítési lehetőségekkel. Ezek a feladatok tetszőleges időpontban végezheti el.

- **Fájlok telepítése.** A parancsmagok a Windows PowerShell 3.0 szereplő Súgó fájlok nem rendelkeznek. Azonban használhatja a [Update-Help](/powershell/module/microsoft.powershell.core/update-help) parancsmaggal töltse le és telepítse a legújabb súgófájlokat a számítógépen. Ha a fájlok vannak telepítve, használhatja a [Get-Help](/powershell/module/microsoft.powershell.core/get-help) parancsmagot is a megjelenítésükhöz jobbra a parancssorban. További információkért lásd: [about_Updatable_Help](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

    Ha úgy dönt, hogy nem telepíti a súgófájlokat, továbbra is olvashatják súgótémakörök online. Bármely parancsmag Súgó-témakör online verziója található, írja be a következőt: `Get-Help <CmdletName> -Online`. A Windows PowerShell-Súgó-témaköröket lásd tallózással a [PowerShell dokumentációs](/powershell/scripting).

- **Parancsfájlok futtatása.** A Windows PowerShell a biztonságos, az alapértelmezett végrehajtási házirend a Windows PowerShell van **korlátozott**. Ez a házirend lehetővé teszi a parancsmagok, de nem a parancsfájlok futtatásához. Parancsfájlok futtatásához használja a [Set-ExecutionPolicy](/powershell/module/microsoft.powershell.security/set-executionpolicy) parancsmag futtatásával módosítsa a végrehajtási házirendet **AllSigned** vagy **RemoteSigned**. Csak a számítógépen a Rendszergazdák csoport tagjai futtathatják a ezt a parancsmagot. További információkért lásd: [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

- **Távelérés engedélyezése.** A rendszer már konfigurálva van ahhoz, hogy a más számítógépeken található parancsok távoli futtatása. A Windows Server 2012 R2 és Windows Server 2012, a rendszer van is konfigurálva kapcsolódva fogadják távoli, ez azt jelenti, hogy más számítógépek a parancsok távoli futtatása a helyi számítógépen. A Windows távoli parancsok fogadására más verzióit futtató számítógépek engedélyezéséhez futtassa a [Enable-PSRemoting](/powershell/module/microsoft.powershell.core/enable-psremoting) parancsmagot a távolról felügyelni kívánt számítógépen. Csak a számítógépen a Rendszergazdák csoport tagjai futtathatják a ezt a parancsmagot. További információkért lásd: [about_Remote](/powershell/module/microsoft.powershell.core/about/about_remote).

    Megjegyzés: A Windows PowerShell 2.0-t futtató számítógépen engedélyezve van a távelérése, ha engedélyezve van a távelérése továbbra is a Windows Management Framework 3.0 telepítése után. Azonban a Windows Server 2008 (nem Windows Server 2008 R2), újra engedélyeznie kell a távelérés Windows Management Framework 3.0 telepítése után.

## <a name="see-also"></a>Lásd még:
- [Windows PowerShell telepítése](../setup/Installing-Windows-PowerShell.md)
- [A Windows PowerShell indítása](/powershell/scripting/setup/starting-windows-powershell)

