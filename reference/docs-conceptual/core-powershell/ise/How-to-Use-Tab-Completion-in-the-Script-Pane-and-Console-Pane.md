---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Parancssori kiegészítés használata a Parancsfájl panelen és a Konzol panelen
ms.assetid: 3b752c3c-0bd0-4eca-a2d3-2d5a37fd9d84
ms.openlocfilehash: e1f8146b6113a82fd3d857c98550ec2e459715a4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a>Parancssori kiegészítés használata a Parancsfájl panelen és a Konzol panelen

Kiegészítést automatikus segítséget nyújt, ha a parancsfájl ablaktáblán vagy a parancssori ablaktáblában írja be. Ez a funkció előnyeit tegye a következőket:

## <a name="to-automatically-complete-a-command-entry"></a>A parancs bejegyzés automatikusan befejezéséhez

A parancs vagy parancsfájl ablaktáblán írja be a parancsot néhány karakterét, és nyomja le az FÜLRE kattintva válassza ki a kívánt befejezési szöveget. Ha több elemet a szöveg, amelyet eredetileg megadott kezdődik, akkor olvassa tovább Tab billentyűkombinációval, amíg meg nem jelenik meg a kívánt elemet. Kiegészítést is segítséget nyújt egy parancsmag neve, a paraméter neve, a változó neve, a objektum tulajdonság neve vagy a egy fájl elérési útját írja be.

> [!NOTE]
> A parancsfájl ablaktáblán TAB billentyűkombinációval automatikusan befejezi a parancs csak akkor, ha szerkeszti, .ps1, .psd1 vagy .psm1 fájlok. Kiegészítést bármikor, ha a parancs ablaktábla ír működik.

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a>A parancsmag paraméter bejegyzés automatikusan befejezéséhez

A parancs vagy a parancsfájl ablaktáblán írja be a parancsmag kötőjellel, és nyomja le az lapon.

Írja be például `Get-Process -` majd nyomja le az lapon többször a paraméterek, a parancsmag pedig megjelenítéséhez.

## <a name="see-also"></a>Lásd még:

- [A Windows PowerShell ISE bemutatása](Introducing-the-Windows-PowerShell-ISE.md)
- [A PowerShell lap létrehozása](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)