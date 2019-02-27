---
title: Listanézet (GroupBy) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a2e66c86-83a7-4148-8575-c28d6d429d4f
caps.latest.revision: 6
ms.openlocfilehash: ad7ea457fe0f67bfa41f6bf81f36d4b2e4a76cb3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849713"
---
# <a name="list-view-groupby"></a>Listanézet (GroupBy)

Ez a példa bemutatja, hogyan valósíthat meg, amely elválasztja a lista a sorok csoportokba megjelenítheti. Ez a lista nézet tulajdonságait jeleníti meg a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektumok a [Get-Service](/powershell/module/microsoft.powershell.management/get-service) parancsmagot. Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).
Ez a példa bemutatja, hogyan valósíthat meg, amely elválasztja a lista a sorok csoportokba megjelenítheti. Ez a lista nézet tulajdonságait jeleníti meg a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektumok a [Get-Service](/powershell/module/Microsoft.PowerShell.Management/Get-Service) parancsmagot. Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).

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

- A [GroupBy](./viewselectedby-element-format.md) elem, amely meghatározza, hogyan jelenjen meg az objektumok egy új csoportot.

- A [ListControl](./listcontrol-element-format.md) elem, amely meghatározza, milyen tulajdonság szerint a nézet jelenik meg.

- A [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) elem, amely meghatározza, hogy a listanézet sorban jelenik meg.

- A [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elem, amely meghatározza, mely tulajdonsága jelenik meg.

## <a name="example"></a>Példa

A következő XML formátumú határozza meg, amely elindítja egy új megjelenítheti, ha a csoport értékét a [System.Serviceprocess.Servicecontroller.Status](/dotnet/api/System.ServiceProcess.ServiceController.Status) tulajdonságukat módosítják. Minden csoport elindult, egy egyéni felirat jelenik meg, amely tartalmazza az új értéket a tulajdonság.

```xml
<Configuration>
  <ViewDefinitions>
    <View>
      <Name>System.ServiceProcess.ServiceController</Name>
      <ViewSelectedBy>
        <TypeName>System.ServiceProcess.ServiceController</TypeName>
      </ViewSelectedBy>
      <GroupBy>
        <PropertyName>Status</PropertyName>
        <Label>New Service Status</Label>
      </GroupBy>
      <ListControl>
        <ListEntries>
          <ListEntry>
            <ListItems>
              <ListItem>
                <PropertyName>Name</PropertyName>
              </ListItem>
              <ListItem>
                <PropertyName>DisplayName</PropertyName>
              </ListItem>
              <ListItem>
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

Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) után betöltődik a formátumfájlban objektumokat. Az üres sorok hozzáadása előtt és után a csoport címkét a rendszer automatikusan hozzáadja a Windows PowerShell.

```powershell
Get-Service f*
```

```output
   New Service Status: Stopped

Name        : Fax
DisplayName : Fax
ServiceType : Win32OwnProcess

   New Service Status: Running

Name        : FCSAM
DisplayName : Microsoft Antimalware Service
ServiceType : Win32OwnProcess

   New Service Status: Stopped

Name        : fdPHost
DisplayName : Function Discovery Provider Host
ServiceType : Win32ShareProcess

   New Service Status: Running

Name        : FDResPub
DisplayName : Function Discovery Resource Publication
ServiceType : Win32ShareProcess

Name        : FontCache
DisplayName : Windows Font Cache Service
ServiceType : Win32ShareProcess

   New Service Status: Stopped

Name        : FontCache3.0.0.0
DisplayName : Windows Presentation Foundation Font Cache 3.0.0.0
ServiceType : Win32OwnProcess

   New Service Status: Running

Name        : FSysAgent
DisplayName : Microsoft Forefront System Agent
ServiceType : Win32OwnProcess

Name        : FwcAgent
DisplayName : Firewall Client Agent
ServiceType : Win32OwnProcess
```

## <a name="see-also"></a>Lásd még:

[Példák a formázási fájlok](./examples-of-formatting-files.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
