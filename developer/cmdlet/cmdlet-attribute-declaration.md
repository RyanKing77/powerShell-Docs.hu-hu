---
title: A parancsmag típusattribútum-deklaráció |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Cmdlet attribute, described
- attributes, Cmdlet
- Cmdlet attribute
ms.assetid: 1d323332-f773-4c0e-8a69-2aada765afb2
caps.latest.revision: 12
ms.openlocfilehash: 6887467ad5ccafe6edf8f03f531b4750133aa9e9
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068623"
---
# <a name="cmdlet-attribute-declaration"></a>Parancsmagok attribútumdeklarációja

A parancsmag attribútum egy Microsoft .NET-keretrendszer osztályt, a parancsmag azonosítja, és adja meg a ige és főnév, a parancsmag indítja.

## <a name="syntax"></a>Szintaxis

```csharp
[Cmdlet("verbName", "nounName")]
[Cmdlet("verbName", "nounName", Named Parameters...)]
```

#### <a name="parameters"></a>Paraméterek

`VerbName` ([System.String](/dotnet/api/System.String)) szükséges. Adja meg a parancsmag-műveletet. Ez a művelet meghatározza a parancsmag által végrehajtott műveletet. A parancsmag jóváhagyott igék kapcsolatos további információkért lásd: [művelet neve](./approved-verbs-for-windows-powershell-commands.md) és [szükséges fejlesztési irányelvek](./required-development-guidelines.md).

`NounName` ([System.String](/dotnet/api/System.String)) szükséges. Adja meg a parancsmag főnév. Ez főnév adja meg az erőforrást, amely a parancsmag közvetítőtől. A parancsmag főneveket kapcsolatos további információkért lásd: [parancsmag Deklarace](./cmdlet-class-declaration.md) és [fejlesztési irányelvek erősen javasolt,](./strongly-encouraged-development-guidelines.md).

`SupportsShouldProcess` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező. `True` jelzi, hogy a parancsmag támogatja a hívásokat a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódussal, amely biztosítja a parancsmag kéri a felhasználótól, amely módosítja a rendszer művelet végrehajtása előtt meg tudja. `False`, az alapértelmezett érték azt jelzi, hogy a parancsmag nem támogatja a hívásokat a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódust. Megerősítési kérések kapcsolatos további információkért lásd: [megerősítést kérő](./requesting-confirmation-from-cmdlets.md).

`ConfirmImpact` ([System.Management.Automation.Confirmimpact](/dotnet/api/System.Management.Automation.ConfirmImpact)) nevű paraméter nem kötelező. Itt adhatja meg, ha a művelet a parancsmag hívást kell megerősíteni a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) metódust. [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) fog lze volat pouze (alapértelmezés szerint, közepes méretű) a parancsmag ConfirmImpact érték esetén egyenlő vagy nagyobb, mint az értékét a `$ConfirmPreference` változó. Ezt a paramétert kell megadni. csak akkor, ha a `SupportsShouldProcess` paraméter meg van adva.

`DefaultParameterSetName` ([System.String](/dotnet/api/System.String)) nevű paraméter nem kötelező. Itt adhatja meg az alapértelmezett paraméter beállítása, hogy a Windows PowerShell-modult használja, ha nem tudja meghatározni, melyik paraméterkészlet használandó próbál. Figyelje meg, hogy ez a helyzet azáltal, hogy az egyedi paramétereket minden paraméter egy kötelező paraméter beállítása kell számolni.

Nincs egyetlen esetet, amelyben Windows PowerShell a még akkor is, ha egy alapértelmezett paraméternév-készlet van megadva alapértelmezett paraméter nem használható. A Windows PowerShell-modul nem tudja megkülönböztetni paraméterkészlettel kizárólag objektumtípus alapján. Például ha rendelkezik egy karakterláncot vesz fel a fájl elérési útját, és a egy másik készlet, amely egy paraméterkészlettel tart egy **FileInfo** objektumot közvetlenül, Windows PowerShell nem tudja meghatározni, melyik paraméter használata átadott értékek alapján a parancsmagot, és nem az alapértelmezett paraméterkészletet használja. Ebben az esetben akkor is, ha megad egy alapértelmezett paraméterkészlet neve, Windows PowerShell nem egyértelmű paraméter beállítása hibaüzenetet jelez.

`SupportsTransactions` ([System.Boolean](/dotnet/api/System.Boolean)) nevű paraméter nem kötelező. `True` azt jelzi, hogy a parancsmag is használható a tranzakción belül. Amikor `True` van megadva, a Windows PowerShell-modul hozzáadása a `UseTransaction` a parancsmag a paraméterlistában paramétert. `False`, az alapértelmezett érték azt jelzi, hogy a parancsmag nem használható tranzakción belül.

## <a name="remarks"></a>Megjegyzés

- Együtt a ige és főnév használt azonosítani a regisztrált parancsmag és a egy parancsfájlban a parancsmag meghívása.

- A parancsmag meghívása a Windows PowerShell-konzolon, ha a parancs hasonló a következő parancsot:

**VerbName-NounName**

- Windows PowerShell-en kívül erőforrások módosító összes parancsmaghoz tartalmaznia kell a `SupportsShouldProcess` kulcsszóval a parancsmag attribútum deklarálva van, amikor, amely lehetővé teszi, hogy a parancsmag meghívása a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) módszert ahhoz a parancsmag végrehajtja a műveletet. Ha a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) értéket ad vissza hívás `false`, a művelet nem kell venni. A megerősítési kérések által létrehozott további információt a [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) hívja, lásd: [megerősítést kérő](./requesting-confirmation-from-cmdlets.md).

A `Confirm` és `WhatIf` parancsmag-paraméterek csak támogató parancsmagok érhetők [System.Management.Automation.Cmdlet.ShouldProcess](/dotnet/api/System.Management.Automation.Cmdlet.ShouldProcess) hívások.

## <a name="example"></a>Példa

Az alábbi osztálydefiníciót a parancsmag attribútum segítségével azonosítja a a .NET-keretrendszer osztály egy **Get-Proc** parancsmagot, amely a helyi számítógépen futó folyamatok adatait kérdezi le.

```csharp
[Cmdlet(VerbsCommon.Get, "Proc")]
public class GetProcCommand : Cmdlet
```

További információ a **Get-Proc** parancsmagot, tekintse meg [GetProc oktatóanyag](./getproc-tutorial.md).

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
