---
title: Listanézet (címkék) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 53442bb1-74a3-49f9-9150-3bc3081a7565
caps.latest.revision: 6
ms.openlocfilehash: 2bb62ab3e4fa1db9b3af8c82eb9035aa4f3e31c0
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849699"
---
# <a name="list-view-labels"></a>Listanézet (Címkék)

Ez a példa bemutatja, hogyan valósíthat meg, amely megjeleníti az egyéni címkével nem rendelkező a lista minden egyes sorára megjelenítheti. Ez a lista nézet tulajdonságait jeleníti meg a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektum a [Get-Service](/powershell/module/microsoft.powershell.management/get-service) parancsmagot. Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).
Ez a példa bemutatja, hogyan valósíthat meg, amely megjeleníti az egyéni címkével nem rendelkező a lista minden egyes sorára megjelenítheti. Ez a lista nézet tulajdonságait jeleníti meg a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektum a [Get-Service](/powershell/module/Microsoft.PowerShell.Management/Get-Service) parancsmagot. Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).

### <a name="to-load-this-formatting-file"></a>Ez a formázási fájl betöltése

1. Az XML-fájl másolása a példa című fejezetet a témakör egy szövegfájlba.

2. Mentse a fájlt. Adja hozzá a `format.ps1xml` kiterjesztést a fájl formázási fájlként az azonosításához.

3. Nyissa meg a Windows Powershellt, és futtassa a következő parancsot betölteni a formázási fájlt az aktuális munkamenetbe: `Update-formatdata -prependpath PathToFormattingFile`.

   > [!WARNING]
   > A formázási fájl olyan objektum, amely már definiálva van egy Windows PowerShell formázási fájl megjelenítését határozza meg. Kell használnia a `prependPath` paramétert, ha futtatja a parancsmagot, és nem tölthető be, a formázást modulként fájlt.

## <a name="demonstrates"></a>Bemutatók

Ez a fájl formázási mutat be a következő XML-elemeket:

- A [neve](./name-element-for-view-format.md) elem a nézet.

- A [ViewSelectedBy](./viewselectedby-element-format.md) elem, amely meghatározza, milyen objektumok jelennek meg a nézet által.

- A [ListControl](./listcontrol-element-format.md) elem, amely meghatározza, milyen tulajdonság szerint a nézet jelenik meg.

- A [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) elem, amely meghatározza, hogy a listanézet sorban jelenik meg.

- A [címke](./label-element-for-listitem-for-listcontrol-format.md) elem, amely meghatározza, hogy a listanézet sorban jelenik meg.

- A [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elem, amely meghatározza, mely tulajdonsága jelenik meg.

## <a name="example"></a>Példa

A következő XML formátumú egyéni címkével nem rendelkező megjelenítő az egyes sorokban szereplő lista nézet határozza meg. Ebben az esetben a címke tartalmazza a tulajdonságnév minden kezdőbetűnek betű- és a "property" szó. Minden egyes sorban a tulajdonság neve megjelenik a tulajdonság értéke követ.

```xml
<Configuration>
  <ViewDefinitions>
    <View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>
    <ListEntries>
      <ListEntry>
        <ListItems>
          <ListItem>
            <Label>NAME property</Label>
            <PropertyName>Name</PropertyName>
          </ListItem>
          <ListItem>
            <Label>DISPLAYNAME property</Label>
            <PropertyName>DisplayName</PropertyName>
          </ListItem>
          <ListItem>
            <Label>STATUS property</Label>
            <PropertyName>Status</PropertyName>
          </ListItem>
          <ListItem>
            <Label>SERVICETYPE property</Label>
            <PropertyName>ServiceType</PropertyName>
          </ListItem>
        </ListItems>
      </ListEntry>
    </ListEntries>
  </ListControl>
</View>

  </ViewDefinitions>
</Configuration>
```

Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) után betöltődik a formátumfájlban objektumokat.

```powershell
Get-Service f*
```

```output
NAME property        : Fax
DISPLAYNAME property : Fax
STATUS property      : Stopped
SERVICETYPE property : Win32OwnProcess

NAME property        : FCSAM
DISPLAYNAME property : Microsoft Antimalware Service
STATUS property      : Running
SERVICETYPE property : Win32OwnProcess

NAME property        : fdPHost
DISPLAYNAME property : Function Discovery Provider Host
STATUS property      : Stopped
SERVICETYPE property : Win32ShareProcess

NAME property        : FDResPub
DISPLAYNAME property : Function Discovery Resource Publication
STATUS property      : Running
SERVICETYPE property : Win32ShareProcess

NAME property        : FontCache
DISPLAYNAME property : Windows Font Cache Service
STATUS property      : Running
SERVICETYPE property : Win32ShareProcess

NAME property        : FontCache3.0.0.0
DISPLAYNAME property : Windows Presentation Foundation Font Cache 3.0.0.0
STATUS property      : Stopped
SERVICETYPE property : Win32OwnProcess

NAME property        : FSysAgent
DISPLAYNAME property : Microsoft Forefront System Agent
STATUS property      : Running
SERVICETYPE property : Win32OwnProcess

NAME property        : FwcAgent
DISPLAYNAME property : Firewall Client Agent
STATUS property      : Running
SERVICETYPE property : Win32OwnProcess
```

## <a name="see-also"></a>Lásd még:

[Példák a formázási fájlok](./examples-of-formatting-files.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
