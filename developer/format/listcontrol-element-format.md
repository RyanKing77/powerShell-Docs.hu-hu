---
title: ListControl elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 37beeb0b-7a81-4747-becb-e309e17278fb
caps.latest.revision: 12
ms.openlocfilehash: 7a117c25b0d117dc846ba8e060e31e838b5edd52
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065257"
---
# <a name="listcontrol-element-format"></a>ListControl elem (Formátum)

Határozza meg a nézet lista formájában.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ListControl>
  <ListEntries>...</ListEntries>
</ListControl>

```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ListControl` elemet. Ez az elem csak egyetlen gyermekelemet kell tartalmaznia.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[ListEntries elem (formátum)](./listentries-element-for-listcontrol-format.md)|Szükséges eleme.<br /><br /> A lista nézet a definíciókat tartalmazza.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[Nézet elem (formátum)](./view-element-format.md)|Meghatározza egy nézetet, amely egy vagy több objektum tagjait megjelenítésére szolgál.|

## <a name="remarks"></a>Megjegyzés

Lista nézet létrehozásával kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).

## <a name="example"></a>Példa

Ez a példa bemutatja a megjelenítheti a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum.

```
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>
    <ListEntries>
      <ListEntry>...</ListEntry>
    </ListEntries>
  </ListControl>
</View>
```

## <a name="see-also"></a>Lásd még:

[Nézet elem (formátum)](./view-element-format.md)

[ListEntries elem (formátum)](./listentries-element-for-listcontrol-format.md)

[Lista nézet létrehozása](./creating-a-list-view.md)

[Egy Windows PowerShell formázás és a fájl típusai](./writing-a-powershell-formatting-file.md)
