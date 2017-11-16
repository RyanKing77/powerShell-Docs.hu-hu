---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A PowerShell lap létrehozása a Windows PowerShell ISE"
ms.assetid: c10c18c7-9ece-4fd0-83dc-a19c53d4fd83
ms.openlocfilehash: 3cfeb18babe6b63f0e02da8cf0fd460950f1afce
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="how-to-create-a-powershell-tab-in-windows-powershell-ise"></a>A PowerShell lap létrehozása a Windows PowerShell ISE
Lapok a a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) lehetővé teszi, hogy egyszerre hozzon létre, és ugyanahhoz az alkalmazáshoz belül több végrehajtási környezetet használja.
PowerShell lapokon megfelel egy külön végrehajtási környezet vagy a munkamenet.

> **MEGJEGYZÉS:**:
>
> Változók, funkcióit és az egyik lapon létrehozott aliasok nem jelenik meg egy másik. Azok a különböző Windows PowerShell-munkamenetekben.

Az alábbi lépések segítségével megnyitása és bezárása egy Windows PowerShell lapján.
Nevezze át a lapon, állítsa be a [DisplayName](The-PowerShellTab-Object.md#displayname) a Windows PowerShell lapon scripting objektum tulajdonságát.

## <a name="to-create-and-use-a-new-powershell-tab"></a>Hozzon létre, és egy új PowerShell lapon

Az a **fájl** menüben kattintson a **új PowerShell lapon**. Az új PowerShell lapon mindig weblapként jelennek meg az aktív ablak.
PowerShell lapok Növekményesen számozása a ahhoz, azok megnyitása.
Minden lap társítva a saját Windows PowerShell-konzolablakot.
A saját munkamenet megnyitása (Ez a korlátozott Windows PowerShell ISE 2.0 8.) egyszerre legfeljebb 32 PowerShell lapokon lehet

Vegye figyelembe, hogy gombra kattintva a **új** vagy **nyitott** az eszköztáron látható ikonok hozzon létre egy új lapon külön munkamenetben.
Ehelyett a gombok egy munkamenet-nyisson meg egy új vagy meglévő parancsfájl a jelenleg aktív lapon.
Fájlok nyissa meg az egyes lapon és a munkamenet több parancsfájlt is.
A parancsprogram lapfülek munkamenet csak alatt jelennek meg a munkamenet lapok aktív a társított munkamenet esetén.

A PowerShell lapon aktívvá tételéhez kattintson a lap. Jelölje be minden nyitott, a PowerShell-lapról a **nézet** menüben kattintson a használni kívánt PowerShell fülre.

## <a name="to-create-and-use-a-new-remote-powershell-tab"></a>Hozzon létre, és egy új távoli PowerShell lapon

Az a **fájl** menüben kattintson a **új távoli PowerShell lapon** hozzon létre egy munkamenetet egy távoli számítógépen.
Egy párbeszédpanel jelenik meg, és megkéri, hogy adja meg a távoli kapcsolat létrehozásához szükséges adatokat.
A távoli lapon funkciók ugyanúgy, mint az egy helyi PowerShell lap, de a parancsok és parancsfájlok futnak a távoli számítógépen.

## <a name="to-close-a-powershell-tab"></a>A PowerShell lap bezárásához

Zárja be a lapon, az alábbi módszerek bármelyikét használhatja:

- Kattintson a bezárni kívánt fülre.

- Az a **fájl** menüben kattintson a **PowerShell lap bezárása**, vagy kattintson a Bezárás gombra (**X**) egy aktív lapon a lap bezárásához.

Ha mentette a fájlok megnyitása a PowerShell lapon, hogy bezárja, mentse vagy vesse el őket kéri.
A parancsfájl mentése kapcsolatos további információkért lásd: [a parancsfájl mentése hogyan](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE használatával](Using-the-Windows-PowerShell-ISE.md)
- [A konzol ablaktáblában a Windows PowerShell ISE használata](How-to-Use-the-Console-Pane-in-the-Windows-PowerShell-ISE.md)

