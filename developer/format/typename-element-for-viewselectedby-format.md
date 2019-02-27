---
title: ViewSelectedBy (formátum) TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0ad807a9-d7d8-4e96-b799-9c6a7677cc2d
caps.latest.revision: 12
ms.openlocfilehash: e2028c479103cc414295dc24a0f9bb69190bfc66
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848138"
---
# <a name="typename-element-for-viewselectedby-format"></a>A ViewSelectedBy elem TypeName eleme (Formátum)

Megadja a nézet által megjelenített .NET-objektumokat.

Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ViewSelectedBy elem (formátum) TypeName eleme ViewSelectedBy (formátum)

## <a name="syntax"></a>Szintaxis

```xml
<TypeName>FullyQualifiedTypeName</TypeName>
```

## <a name="attributes-and-elements"></a>Attribútumok és elemek

A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a szülő elemei a `TypeName` elemet.

### <a name="attributes"></a>Attribútumok

Nincs.

### <a name="child-elements"></a>Gyermekelemek

Nincs.

### <a name="parent-elements"></a>Szülőelemek

|Elem|Leírás|
|-------------|-----------------|
|[ViewSelectedBy elem (formátum)](./viewselectedby-element-format.md)|A .NET-objektumokat a nézet által megjelenített határozza meg.|

## <a name="text-value"></a>Szöveges érték

Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.

## <a name="remarks"></a>Megjegyzés

Ez az elem használatának módja a következőben különböző nézeteket kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md), [lista nézet létrehozásával](./creating-a-list-view.md), [széles nézet létrehozásával](./creating-a-wide-view.md), és [ Egyéni nézet összetevők](./creating-custom-controls.md).

## <a name="example"></a>Példa

Az alábbi példa bemutatja, hogyan adja meg a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) objektum az adott nézet. Tábla, széles és egyéni nézetekben használható ugyanazzal a sémával.

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

## <a name="see-also"></a>Lásd még:

[Lista nézet létrehozása](./creating-a-list-view.md)

[Tábla nézet létrehozása](./creating-a-table-view.md)

[Egy széles nézet létrehozása](./creating-a-wide-view.md)

[Egyéni vezérlők létrehozását](./creating-custom-controls.md)

[ViewSelectedBy elem (formátum)](./viewselectedby-element-format.md)

[A fájl formázása PowerShell írása](./writing-a-powershell-formatting-file.md)
