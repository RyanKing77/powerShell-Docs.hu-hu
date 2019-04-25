---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: PowerShell-lap létrehozása a Windows PowerShell ISE-ben
ms.assetid: c10c18c7-9ece-4fd0-83dc-a19c53d4fd83
ms.openlocfilehash: 080fe89bf1443f51460589b445431913fa20b4b8
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057740"
---
# <a name="how-to-create-a-powershell-tab-in-windows-powershell-ise"></a>PowerShell-lap létrehozása a Windows PowerShell ISE-ben

Lapok a a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) lehetővé teszi, hogy egyszerre hozzon létre, és használja ugyanazt az alkalmazást belül több végrehajtási környezet.
Egyes PowerShell-lap egy különálló környezetben vagy a munkamenet felel meg.

> [!NOTE]
> Változók, a functions és a aliasról, amelyek egy lapot hoz létre a másikra nem kerülnek át. Azok a különböző Windows PowerShell-munkameneteket.

A következő lépések segítségével megnyitása vagy bezárása egy lapon, a Windows PowerShellben.
Nevezze át a lapon, állítsa be a [DisplayName](object-model/The-PowerShellTab-Object.md#displayname) a Windows PowerShell-lap scripting objektum tulajdonságának.

## <a name="to-create-and-use-a-new-powershell-tab"></a>Hozhat létre és használhat egy új PowerShell-lap

Az a **fájl** menüben kattintson a **új PowerShell-lap**. Az új PowerShell-lap mindig az aktív ablak nyílik meg.
PowerShell-lapok növekményes számozása ahhoz, hogy meg vannak nyitva.
Minden lap társítva a saját Windows PowerShell-konzolablakot.
Legfeljebb 32 PowerShell lapokat, egyszerre (Ez a korlátozott, a Windows PowerShell ISE 2.0 8-ra.) nyissa meg a saját munkamenettel is rendelkezhet

Vegye figyelembe, hogy kattint a **új** vagy **nyílt** az eszköztár ikonjainak hozzon létre egy új lap egy külön munkamenetben.
Ehelyett ezekre a gombokra nyisson meg egy új vagy meglévő parancsfájl a jelenleg aktív lapon egy munkamenetet.
Fájlok meg minden egyes lapon és a munkamenet több szkript is rendelkezhet.
A munkamenet a parancsfájl lapok csak alatt jelennek meg a munkamenet-lapok Ha a társított munkamenet aktív.

Ahhoz, hogy aktív PowerShell-lap, kattintson a lap. Jelölje be minden megnyitott, a PowerShell-lap a **nézet** menüben kattintson a használni kívánt PowerShell fülre.

## <a name="to-create-and-use-a-new-remote-powershell-tab"></a>Hozhat létre és használhat egy új távoli PowerShell-lap

Az a **fájl** menüben kattintson a **új távoli PowerShell-lap** hozzon létre egy munkamenetet egy távoli számítógépen.
Egy párbeszédpanel jelenik meg, és megkéri, hogy adja meg a távoli kapcsolat létrehozásához szükséges adatokat.
A Távoli használat lapról funkciók ugyanúgy mint egy helyi PowerShell-lap, de a parancsokat és szkripteket a távoli számítógépen futnak.

## <a name="to-close-a-powershell-tab"></a>PowerShell-lap bezárása

A lap bezárásához, az alábbi módszerek bármelyikét használhatja:

- Kattintson a gombra kattintva zárja be a kívánt lapra.

- Az a **fájl** menüben kattintson a **PowerShell-lap bezárásához**, vagy kattintson a Bezárás gombra (**X**) egy aktív lapon a lap bezárásához.

Ha mentette a fájlokat nyissa meg a PowerShell-lap, hogy bezárásakor, mentse vagy vesse el azokat kéri.
Mentse a parancsfájlt kapcsolatos további információkért lásd: [egy parancsfájl mentése hogyan](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE bemutatása](Introducing-the-Windows-PowerShell-ISE.md)
- [A konzol panel használata a Windows PowerShell ISE-ben](How-to-Use-the-Console-Pane-in-the-Windows-PowerShell-ISE.md)