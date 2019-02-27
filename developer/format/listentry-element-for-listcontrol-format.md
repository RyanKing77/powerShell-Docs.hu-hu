---
title: ListControl (formátum) ListEntry eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6d16bca8-d025-432d-aa84-8b607b8af3ae
caps.latest.revision: 12
ms.openlocfilehash: 1a3bafd4ca94aee70e869c699f7a4ef8befc5511
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851183"
---
# <a name="listentry-element-for-listcontrol-format"></a>A ListControl elemhez tartozó ListEntry elem (Formátum)

A lista nézet definíciójának biztosít.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ListEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <ListItems>...</ListItems>
</ListEntry>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ListEntry` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[EntrySelectedBy eleme ListEntry (formátum)](./entryselectedby-element-for-listentry-for-listcontrol-format.md)|Nem kötelező eleme.<br /><br /> A .NET-objektumok, amelyek a lista nézetdefinícióban, illetve a feltétellel, hogy léteznie kell a definíció használandó határozza meg.|
|[ListItems elemek elem (formátum)](./listitems-element-for-listentry-for-listcontrol-format.md)|Szükséges eleme.<br /><br /> Meghatározza a tulajdonságok és a parancsfájlok, melynek értékei szerint a listanézetet jelennek meg.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[ListEntries elem (formátum)](./listentries-element-for-listcontrol-format.md)|A lista nézet a definíciókat tartalmazza.|

## <a name="remarks"></a>Megjegyzés

Lista nézetben, amely megjeleníti a tulajdonság vagy parancsfájl értékei az egyes objektumok lista formájában. Listanézetek kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja az XML-elemeket, amelyek meghatározzák a listanézet a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum.

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>
    <ListEntries>
      <ListEntry>
        <ListItems>...</ListItems>
      </ListEntry>
    </ListEntries>
  </ListControl>
</View>
```

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[EntrySelectedBy eleme ListEntry (formátum)](./entryselectedby-element-for-listentry-for-listcontrol-format.md)

[ListEntries elem (formátum)](./listentries-element-for-listcontrol-format.md)

[ListItems elemek elem (formátum)](./listitems-element-for-listentry-for-listcontrol-format.md)

[Egy Windows PowerShell formázás és a fájl típusai](./writing-a-powershell-formatting-file.md)
