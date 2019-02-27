---
title: Széles nézet (GroupBy) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 39388197-4ff9-4889-aa32-526011afa1f6
caps.latest.revision: 6
ms.openlocfilehash: e95ec550a7815a76a8bd7f9526dfa405a9644360
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850749"
---
# <a name="wide-view-groupby"></a>Széles nézet (GroupBy)

Ez a példa bemutatja, hogyan valósíthat meg a csoportjait megjelenítő széles nézet [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektumok a `Get-Service` parancsmagot. Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).

### <a name="to-load-this-formatting-file"></a>Ez a formázási fájl betöltése

1. Az XML-fájl másolása a példa című fejezetet a témakör egy szövegfájlba.

2. Mentse a fájlt. Adja hozzá a `format.ps1xml` kiterjesztést a fájl formázási fájlként az azonosításához.

3. Nyissa meg a Windows Powershellt, és futtassa a következő parancsot betölteni a formázási fájlt az aktuális munkamenetbe: `Update-formatdata -prependpath PathToFormattingFile`.

   > [!WARNING]
   > Ez a formázási fájl olyan objektum, amely már definiálva van egy Windows PowerShell formázás fájlok megjelenítését határozza meg. Kell használnia a `prependPath` paramétert, ha futtatja a parancsmagot, és nem tölthető be, a formázást modulként fájlt.

## <a name="demonstrates"></a>Bemutatók

Ez a fájl formázási mutat be a következő XML-elemeket:

- A [neve](./name-element-for-view-format.md) elem a nézet.

- A [ViewSelectedBy](./viewselectedby-element-format.md) elem, amely meghatározza, milyen objektumok jelennek meg a nézet által.

- A [GroupBy](./groupby-element-for-view-format.md) elem, amely meghatározza, hogy ha egy új csoport megjelenik.

- A [WideItem](./wideitem-element-for-widecontrol-format.md) elem, amely meghatározza, milyen tulajdonság szerint a nézet jelenik meg.

## <a name="example"></a>Példa

A következő XML-kódot, amely megjeleníti az objektumok csoportjaihoz széles nézet határozza meg. Minden egyes új csoport indítása során értékét a [System.Serviceprocess.Servicecontroller.Servicetype](/dotnet/api/System.ServiceProcess.ServiceController.ServiceType) tulajdonságukat módosítják.

```xml
<?xml version="1.0" encoding="utf-8" ?>

<Configuration>
  <ViewDefinitions>
    <View>
      <Name>ServiceWideView</Name>
      <ViewSelectedBy>
        <TypeName>System.ServiceProcess.ServiceController</TypeName>
      </ViewSelectedBy>
      <GroupBy>
        <Label>Service Type</Label>
        <PropertyName>ServiceType</PropertyName>
      </GroupBy>
      <WideControl>
        <WideEntries>
          <WideEntry>
            <WideItem>
              <PropertyName>ServiceName</PropertyName>
            </WideItem>
          </WideEntry>
        </WideEntries>
      </WideControl>
    </View>
  </ViewDefinitions>
</Configuration>
```

Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) után betöltődik a formátumfájlban objektumokat.

```powershell
Get-Service f*
```

```output
   Service Type: Win32OwnProcess

Fax                             FCSAM

   Service Type: Win32ShareProcess

fdPHost                         FDResPub
FontCache

   Service Type: Win32OwnProcess

FontCache3.0.0.0                FSysAgent
FwcAgent
```

## <a name="see-also"></a>Lásd még:

[Példák a formázási fájlok](./examples-of-formatting-files.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
