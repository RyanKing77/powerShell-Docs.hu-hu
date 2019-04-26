---
title: Parancsmag-paraméterek típusú |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6602730d-3892-4656-80c7-7bca2d14337f
caps.latest.revision: 14
ms.openlocfilehash: f5781c0c03aca41d01a44598a9a8c00d6d21d2fd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067195"
---
# <a name="types-of-cmdlet-parameters"></a>Parancsmag-paraméterek típusai

Ez a témakör ismerteti a különböző típusú paramétereket, a parancsmagok eszközhöz adhat. Parancsmag-paraméterek a Helyzetbeállító, nevesített, szükséges, választható kell, vagy a kapcsolóparaméterek.

## <a name="positional-and-named-parameters"></a>A Helyzetbeállító és elnevezett paraméterek

Az összes parancsmag-paraméterek olyan elnevezett vagy helyfüggő paraméterek. Egy elnevezett paraméterhez meg kell adnia a paraméter nevének és argumentum a parancsmag hívásakor. A Helyzetbeállító paraméter csak követel meg, hogy az argumentumok relatív sorrendben írja be. A rendszer az első névtelen argumentum majd hozzárendeli az első Helyzetbeállító paraméter. A rendszer névtelen második argumentumként hozzárendeli a második névtelen paramétert, és így tovább. Alapértelmezés szerint az összes parancsmag-paraméterek paraméter neve.

Egy elnevezett paraméter határozza meg, hagyja ki ezt a `Position` kulcsszó a **paraméter** attribútum nyilatkozat, ahogyan az az alábbi deklarace parametru.

```csharp
[Parameter(ValueFromPipeline=true)]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

Adjon meg a Helyzetbeállító paramétert, adja hozzá a `Position` kulcsszó, paraméterben deklarace attribútumot, és adja meg az olyan helyzetben. Az alábbi minta a `UserName` paraméter 0 pozíciója a Helyzetbeállító paraméterként van deklarálva. Ez azt jelenti, hogy az első argumentum a hívás automatikusan társítani ehhez a paraméterhez.

```csharp
[Parameter(Position = 0)]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

> [!NOTE]
> Jó parancsmag tervezési javasolja, hogy a leggyakrabban használt paraméterek deklarálható pozicionális paramétereknél, hogy a felhasználó nem rendelkezik, adja meg a paraméter nevével, a parancsmag futtatásakor.

A Helyzetbeállító és elnevezett paraméterek fogadja el a egyetlen argumentumok vagy vesszővel elválasztva több argumentumot. Több argumentumot engedélyezett csak akkor, ha a paraméter karakterláncok például egy tömb gyűjteménye fogad el. Ugyanezzel a parancsmaggal a Helyzetbeállító és elnevezett paraméterek is kombinálhatók. Ebben az esetben a rendszer beolvassa a pojmenované argumenty először, és majd kísérletek való leképezéséhez a hátralévő el a névtelen a pozicionális paramétereknél argumentumokat.

Az alábbi parancsokat az egyetlen és a paraméterek, több argumentumot is megadhat, amelyben különböző módszereket mutatnak a `Get-Command` parancsmagot. Figyelje meg, hogy az utolsó két minta **-név** nem kell megadni, mert a `Name` paraméter csak pozíciórekord paraméterként van definiálva.

```powershell
Get-Command -Name get-service
Get-Command -Name get-service,set-service
Get-Command get-service
Get-Command get-service,set-service
```

## <a name="mandatory-and-optional-parameters"></a>Kötelező és választható paramétereket

Parancsmag-paraméterek, kötelező vagy választható paramétereket is definiálhat. (Paraméter megadása kötelező a Windows PowerShell-modul a parancsmag meghívása előtt kell megadni.)  Alapértelmezés szerint a paraméterek vannak meghatározva, nem kötelező.

Egy kötelező paraméter határozza meg, adja hozzá a `Mandatory` kulcsszó, paraméterben deklarace attribútumot, és állítsa be `true`, ahogyan az az alábbi deklarace parametru.

```csharp
[Parameter(Position = 0, Mandatory = true)]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

Adja meg egy nem kötelező paraméter, hagyja ki ezt a `Mandatory` kulcsszót a a **paraméter** attribútum nyilatkozat, ahogyan az az alábbi deklarace parametru.

```csharp
[Parameter(Position = 0)]
public string UserName
{
  get { return userName; }
  set { userName = value; }
}
private string userName;
```

## <a name="switch-parameters"></a>Kapcsolóparaméterek

Windows PowerShell biztosít egy [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter) típus, amely lehetővé teszi egy paraméter értékének értéke automatikusan `false` Ha a paraméter nincs megadva a parancsmag esetén nevezik. Amikor csak lehetséges, használja a kapcsolóparaméterek logikai típusú paraméterek helyett.

Vegye figyelembe a következő mintát. Alapértelmezés szerint számos Windows PowerShell-parancsmagok nem ad meg a folyamat egy kimeneti objektumot. Van azonban, hogy ezek a parancsmagok egy `PassThru` váltson paraméter, amely felülírja az alapértelmezett viselkedést. Ha a `PassThru` paraméter meg van adva, ha ezeket a parancsmagokat a rendszer meghív, a parancsmag kimeneti objektumot adja vissza a folyamathoz.

Ha szüksége van-e a paraméter alapértelmezett értéke `true` a paraméter nincs megadva a hívást, vegye figyelembe az értelemben paraméter megfordítása. A minta egy logikai érték, amely a paraméter-attribútumhoz beállítás helyett `true`, deklarálja a tulajdonság a [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter) írja be, és állítsa az alapértelmezett érték a paraméter`false`.

Egy új kapcsolóparaméter definiálásához deklarálja a tulajdonság a [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter) írja be az alábbi mintában látható módon.

```csharp
[Parameter(Position = 1)]
public SwitchParameter GoodBye
{
  get { return goodbye; }
  set { goodbye = value; }
}
private bool goodbye;
```

Ahhoz, hogy a parancsmag reagálhat rájuk a paramétert, ha a célgyűjtemény meg van adva, használja az alábbi struktúrával módszerek feldolgozása a bemeneti egyikében.

```csharp
protected override void ProcessRecord()
{
  WriteObject("Switch parameter test: " + userName + ".");
  if(goodbye)
  {
    WriteObject(" Goodbye!");
  }
} // End ProcessRecord
```

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
