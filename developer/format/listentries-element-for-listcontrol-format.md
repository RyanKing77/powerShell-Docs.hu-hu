---
title: ListControl (formátum) ListEntries eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b62e81cc-4175-40fa-829f-634245b09f86
caps.latest.revision: 12
ms.openlocfilehash: aaf16702e485135b5299ccb43a2b62db2d9f5762
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065393"
---
# <a name="listentries-element-for-listcontrol-format"></a>A ListControl elemhez tartozó ListEntries elem (Formátum)

A lista nézet a definíciókat tartalmazza. A listanézet meg kell adnia egy vagy több definíciót.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<ListEntries>
  <ListEntry>...</ListEntry>
</ListEntries>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ListEntries` elemet. Meg kell adni legalább egy gyermekelemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

|Elem|Leírás|
|-------------|-----------------|
|[ListEntry elem (formátum)](./listentry-element-for-listcontrol-format.md)|A lista nézet definíciójának biztosít.|

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[ListControl elem (formátum)](./listcontrol-element-format.md)|Határozza meg a nézet lista formájában.|

## <a name="remarks"></a>Megjegyzés

Listanézetek kapcsolatos további információkért lásd: [listanézet](./creating-a-list-view.md).

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

[ListControl elem (formátum)](./listcontrol-element-format.md)

[ListEntry elem (formátum)](./listentry-element-for-listcontrol-format.md)

[Listanézet](./creating-a-list-view.md)

[Egy Windows PowerShell formázás és a fájl típusai](./writing-a-powershell-formatting-file.md)
