---
title: Jóváhagyás kérése a parancsmagok |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ConfirmImpact [PowerShell Programmer's Guide], described
- ShouldContinue [PowerShell Programmer's Guide], described
- user feedback [PowerShell Programmer's Guide], requesting
- ShouldProcess [PowerShell Programmer's Guide], described
- ConfirmPreference [PowerShell Programmer's Guide], described
ms.assetid: 37d6e87f-57b7-40bd-b645-392cf0b6e88e
caps.latest.revision: 13
ms.openlocfilehash: 0c0517ef7fbd5ae6434773a2dfe276f3a8c35f39
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067484"
---
# <a name="requesting-confirmation-from-cmdlets"></a>Megerősítés kérése parancsmagoktól

Parancsmagok igényeljen megerősítő, amelyek készül, hogy hajtson végre módosítást a rendszer a Windows PowerShell környezetben kívül esik. Például a parancsmag arra készül, hogy adjon hozzá egy felhasználót vagy a folyamat leállítása, ha a parancsmag elvégzéséhez szükséges felhasználói megerősítés előtt halad. Ezzel szemben ha a parancsmag egy Windows PowerShell-változóban megváltozása, a parancsmag nem kell megerősítést.

Annak érdekében, hogy egy megerősítési kérést, a parancsmag jeleznie kell, hogy eseménymegerősítési kéréseknek támogatja, és azt meg kell hívnia a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [ System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) (nem kötelező) módszer a megerősítést kérő üzenet megjelenítéséhez.

## <a name="supporting-confirmation-requests"></a>Megerősítési kérések támogatása

Megerősítési kérések támogatja, a parancsmag be kell állítania a `SupportsShouldProcess` paraméter, a parancsmag attribútum `true`. Ez lehetővé teszi a `Confirm` és `WhatIf` biztosított Windows PowerShell parancsmag-paraméterek. A `Confirm` paraméter lehetővé teszi, hogy a felhasználó szabályozza-e a megerősítési kérés jelenik meg. A `WhatIf` paraméter lehetővé teszi, hogy a felhasználó határozza meg, hogy a parancsmag megjelenít egy üzenetet vagy a művelet végrehajtására. Manuálisan nem adja hozzá a `Confirm` és `WhatIf` a parancsmag paramétereit.

Az alábbi példa bemutatja a parancsmag attribútum határozza meg, amely támogatja az eseménymegerősítési kéréseknek.

```csharp
[Cmdlet(VerbsDiagnostic.Test, "RequestConfirmationTemplate1",
        SupportsShouldProcess = true)]
```

## <a name="calling-the-confirmation-request-methods"></a>A megerősítési kérés metódusok meghívása

A parancsmag kód hívása a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) módszer, amely módosítja a rendszer a művelet végrehajtása előtt. A parancsmag Tervező, úgy, hogy ha a hívás értéket ad `false`, nem történik meg a műveletet, és a parancsmag végrehajtja a következő műveletet.

## <a name="calling-the-shouldcontinue-method"></a>A ShouldContinue metódus hívása

A legtöbb parancsmagok kérelem megerősítő használatával csak a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódust. Bizonyos esetekben azonban szükség lehet további megerősítést. Ezekben az esetekben kiegészítik a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) hívásával hívja a [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódust. Ez lehetővé teszi a parancsmag vagy a szolgáltatót, hogy több hatókörét szabályozza a **Igen, az összeset** válasz a megerősítési kérést.

Ha a parancsmag a [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) metódus, a parancsmag is meg kell egy `Force` paraméter váltani. Ha a felhasználó adja meg `Force` a felhasználó a parancsmag hív meg, továbbra is meghívja a parancsmag [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess), de azt kell kerülni a hívást [ System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).

[System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue) kivételt ad hívott nem interaktív környezetből, nem kéri a felhasználót. Hozzáadás egy `Force` paraméter gondoskodik arról, hogy a parancs továbbra is elvégezhető a nem interaktív környezetben meghívásakor.

A következő példa bemutatja, hogyan hívhat meg [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) és [System.Management.Automation.Cmdlet.ShouldContinue](/dotnet/api/System.Management.Automation.Cmdlet.ShouldContinue).

```csharp
if (ShouldProcess (...) )
{
  if (Force || ShouldContinue(...))
  {
     // Add code that performs the operation.
  }
}
```

Viselkedését egy [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) hívás, amelyben a parancsmag meghívása a környezettől függően változhat. Használja az előző irányelvek segítségével győződjön meg arról, hogy a parancsmag a többi parancsmag esetében a gazdagép környezet függetlenül konzisztens módon viselkedik.

Hívása egy példát a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódus, lásd: [kérelem megerősítések hogyan](./how-to-request-confirmations.md).

## <a name="specify-the-impact-level"></a>Adja meg a hatás szintje

A parancsmag létrehozásakor adja meg a változtatás a hatás szintje (a súlyosság). Ehhez állítsa az értékét a `ConfirmImpact` paraméter a parancsmag attribútum magas, közepes vagy alacsony. Egy értéket is megadhat `ConfirmImpact` csak is megadása a `SupportsShouldProcess` paramétert a parancsmaghoz.

A legtöbb parancsmag esetében nem kell explicit módon kell megadni `ConfirmImpact`.  Ehelyett használjon az alapértelmezett beállítás a paraméter, amely közepes. Ha `ConfirmImpact` magas, a művelet fogja erősíteni alapértelmezés szerint. Ezt a beállítást a magas azokat a káros műveleteket, például a merevlemez-kötet újraformázást lefoglalni.

## <a name="calling-non-confirmation-methods"></a>Nem megerősítő metódusok meghívása

Ha a parancsmag vagy a szolgáltató üzenetet küldeni, de nem a megerősítést kérő, meghívhatja az alábbi három módszerrel. Kerülje a [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) metódus az ilyen jellegű üzenetek küldéséhez, mert [System.Management.Automation.Cmdlet.WriteObject](/dotnet/api/System.Management.Automation.Cmdlet.WriteObject) kimeneti vezérlőelemen van és a szokásos kimenete a parancsmag vagy a szolgáltató, amely megnehezíti parancsprogram írása.

- Figyelmeztetés a felhasználó, és folytatja a műveletet, a parancsmag vagy a szolgáltató meghívhatja a [System.Management.Automation.Cmdlet.WriteWarning](/dotnet/api/System.Management.Automation.Cmdlet.WriteWarning) metódust.

- Kiegészítő információkat, amelyek a felhasználó használja a `Verbose` paraméter, a parancsmag vagy a szolgáltató segítségével meghívhatja a [System.Management.Automation.Cmdlet.WriteVerbose](/dotnet/api/System.Management.Automation.Cmdlet.WriteVerbose) metódust.

- Hibakeresés szintű részletes-fejlesztőknek szántam vagy terméktámogatási megadásához a parancsmag vagy a szolgáltató meghívhatja a [System.Management.Automation.Cmdlet.WriteDebug](/dotnet/api/System.Management.Automation.Cmdlet.WriteDebug) metódust. A felhasználó ezen információk használatával lehet lekérdezni a `Debug` paraméter.

Parancsmagok és szolgáltatók első hívás megerősítés kérése, mielőtt újabb végrehajtania egy műveletet, amely módosítja a Windows PowerShell-en kívül a rendszer a következő módszerekkel:

- [System.Management.Automation.Cmdlet.Shouldprocess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess)

- [System.Management.Automation.Provider.Cmdletprovider.Shouldprocess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess)

Ehhez a meghívásával a [System.Management.Automation.Cmdlet.Shouldprocess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódussal, amely felszólítja a felhasználót, hogy erősítse meg a műveletet, hogy a felhasználó hív-e a parancs alapján.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
