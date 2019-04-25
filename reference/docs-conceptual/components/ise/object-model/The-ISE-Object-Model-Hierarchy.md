---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISE objektummodell-hierarchiája
ms.openlocfilehash: 0159707b1050c412a74da3d3ca02a46cea982556
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057723"
---
# <a name="the-ise-object-model-hierarchy"></a>Az ISE objektummodell-hierarchiája

Ez a témakör bemutatja a Windows PowerShell integrált parancsfájlkezelési környezet (ISE) részét képező objektumok hierarchiáját.
Windows PowerShell ISE-ben megtalálható a Windows PowerShell 3.0 és a Windows PowerShell 4.0-s verzióját.
Kattintson egy objektum, amelyben az osztály, amely meghatározza az objektum a hivatkozási dokumentációját.

## <a name="psise-object"></a>$psISE Object

A **$psISE** objektum a [gyökérobjektum](The-ObjectModelRoot-Object.md) a Windows PowerShell ISE-objektum hierarchia.
A legfelső szintű helyen található, azt elérhetővé teszi a következő objektumok scripting:

## <a name="psisecurrentfilethe-isefile-objectmd"></a>[$psISE.CurrentFile](The-ISEFile-Object.md)

A **$psISE.CurrentFile** objektum egy példányát a [ISEFile](The-ISEFile-Object.md) osztály.

## <a name="psisecurrentpowershelltabthe-powershelltab-objectmd"></a>[$psISE.CurrentPowerShellTab](The-PowerShellTab-Object.md)

The **$psISE.CurrentPowerShellTab** object is an instance of the [PowerShellTab](The-PowerShellTab-Object.md) class.

## <a name="psisecurrentvisiblehorizontaltool"></a>$psISE.CurrentVisibleHorizontalTool

A **$psISE.CurrentVisibleHorizontalTool** objektum egy példányát a [ISEAddOnTool](The-ISEAddOnTool-Object.md) osztály.
A telepített kiegészítő eszköz, amely jelenleg rögzítve van a Windows PowerShell ISE-ben ablak felső széle képviseli.

## <a name="psisecurrentvisibleverticaltool"></a>$psISE.CurrentVisibleVerticalTool

A **$psISE.CurrentVisibleHorizontalTool** objektum egy példányát a [ISEAddOnTool](The-ISEAddOnTool-Object.md) osztály.
A telepített kiegészítő eszköz, amely jelenleg rögzítve van a Windows PowerShell ISE-ablak jobb oldali széle képviseli.

## <a name="psiseoptionsthe-iseoptions-objectmd"></a>[$psISE.Options](The-ISEOptions-Object.md)

A **$psISE.Options** objektum egy példányát a [ISEOptions](The-ISEOptions-Object.md) osztály.
Az ISEOptions objektum Windows PowerShell ISE-ben különböző beállításait jelöli.
Fontos a Microsoft.PowerShell.Host.ISE.ISEOptions osztály egy példányát.

## <a name="psisepowershelltabsthe-powershelltabcollection-objectmd"></a>[$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md)

A **$psISE.PowerShellTabs** objektum egy példányát a [PowerShellTabCollection](The-PowerShellTabCollection-Object.md) osztály.
Az összes a jelenleg megnyitott PowerShell lapok, amelyek az elérhető Windows PowerShell környezetben futtatni, a helyi számítógépen vagy a csatlakoztatott távoli számítógépeken lévő gyűjteménye.
A gyűjtemény minden tagja egy példányát a [PowerShellTab](The-PowerShellTab-Object.md) osztály.

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)