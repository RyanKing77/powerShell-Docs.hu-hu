---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Ismerkedés a PowerShell-Célállapotkonfiguráció
ms.openlocfilehash: b5aff5008db5a5e45b77d8094b0e48ad98dc63fa
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="getting-started-with-powershell-desired-state-configuration"></a>Ismerkedés a PowerShell-Célállapotkonfiguráció #

Ez az útmutató ismerteti, hogyan elindítja a PowerShell célállapot-konfiguráció dokumentumok létrehozása és alkalmazása a gépeken. Funkciók, a PowerShell parancsmagok és a modulok alapszintű ismeretét feltételezi.


## <a name="create-a-configuration"></a>Konfiguráció létrehozása ##

[**Konfigurációk** ](https://msdn.microsoft.com/powershell/dsc/configurations) környezet ismertető dokumentum. Környezetek áll "**csomópontok**", amelyeket gyakran virtuális vagy fizikai gépek.

Az űrlap különböző konfigurációkat kerülhet. Az új konfiguráció létrehozásához legkönnyebben .ps1 (PowerShell-parancsfájl) fájl létrehozásához. Ehhez nyissa meg a választott szerkesztővel. A PowerShell ISE érdemes használni, mert DSC natív módon támogatja. Mentse a PS1 a következőket:

```powershell
configuration MyFirstConfiguration
{
    Import-DscResource -Name WindowsFeature

    Node localhost
    {
        WindowsFeature IIS
        {
            Name = "IIS"

        }

    }

}
```
## <a name="parts-of-a-configuration"></a>A konfiguráció részei ##
**Konfigurációs** PowerShell 4.0-s hozzáadott kulcsszó. Azt jelzi, hogy olyan különleges célállapot-konfiguráció által használt PowerShell-függvény. Ebben a példában a függvény myFirstConfiguration neve.

A következő sorban egy importálási utasítást, a modul importálása hasonlít. Az tárgyalja később.

"Csomópont" Ebben a konfigurációban fog működni a számítógép nevét adja meg. Bár ez a konfiguráció helyi szerkeszt, konfigurációk elérhetők a távoli csomópontokat, és konfigurálja őket.

Csomópontok lehetnek a számítógép nevét vagy IP-címeket. Több csomópont lehet egy egyetlen konfigurációs dokumentumot. Használatával [konfigurációs adatok](https://msdn.microsoft.com/powershell/dsc/configdata), ugyanaz a konfiguráció alkalmazása több csomópont is lehet. Ebben az esetben a csomópont nem "localhost" – ami azt jelenti, hogy a helyi számítógépen.

A következő elem egy [ **erőforrás**](https://msdn.microsoft.com/powershell/dsc/resources). Erőforrások konfigurációk építőelemei. Minden erőforrás, amely meghatározza egy gép egyetlen aspektusa végrehajtási logikájának modul. Megtekintheti minden erőforrás a számítógépen futó **Get-DscResource** a PowerShellben. Erőforrások a helyi számítógépen jelen kell lennie, és konfigurációban való használat előtt importálni **Import-DscResource** Ez a konfiguráció a második sorban.

**A konfiguráció életbe**

A fenti parancsfájl menti, és futtassa, ha nincs kimenet gyűjtenek. Ez a, mert a konfiguráció csak a következő függvényt, és a fenti parancsfájl a függvény definiálva van, de még nem futtatható. Miután a függvény definiálva van, a kell meghívni:
```powershell
myFirstConfiguration
```

Végrehajtásakor konfigurációs funkciók a konfiguráció ellenőrzése érvényes. Nincsenek szintaktikai hibák rendelkeznie kell, és erőforrások rendelkeznie kell meghatározott összes kötelező paraméterek összes erőforrás végrehajtása előtt kell importálni.

A konfigurációs végrehajtása, amennyiben azt egy mappát hoz létre a konfigurációs tartalmazó nevű egy **. MOF-fájlt** a konfiguráció minden csomópontján. A. MOF-fájlt a hálózaton keresztül kommunikálnak a PowerShell DSC által használt szabványalapú felügyeleti formátumban.

A konfiguráció életbe léptetni:
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration
```
Ezzel létrehoz egy PowerShell feladat egészítse ki a konfigurációs csomópontjaihoz, és konfigurálja azokat. A feladat eredményének megtekintéséhez használja a-Wait.
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration -Wait
```