---
title: A formázási fájl létrehozása (. format.ps1xml) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eb568878-f63e-4561-98e2-16ee2ac7559d
caps.latest.revision: 8
ms.openlocfilehash: e97e9ddb1bf81ba66e5f3cedddd22e3a861ce228
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065501"
---
# <a name="how-to-create-a-formatting-file-formatps1xml"></a>Formázási fájl létrehozása (.format.ps1xml)

Ez a témakör ismerteti, hogyan hozhat létre egy formázási fájlt (. format.ps1xml).

> [!NOTE]
> Azáltal, hogy a Windows PowerShell által biztosított fájlok egy másolatát is létrehozhat egy formázási fájlt. Ha egy meglévő fájl egy példányát, törölje a meglévő digitális aláírás, és az új fájl hozzáadása a saját aláírását.

### <a name="to-create-a-formatps1xml-file"></a>Hozhat létre egy. format.ps1xml fájlt.

1. Hozzon létre egy szövegfájlt (.txt) használatával a szöveges szerkesztő, például a Jegyzettömbben.

2. Másolja a következő sorokat a formázási fájlba.

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <Configuration>
   <ViewDefinitions>
   </ViewDefinitions>
   </Configuration>
   ```

   - A \<Configuration >\</Configuration > címkék megadása a legfelső szintű `Configuration` csomópont. Ezen a csomóponton belüli minden további XML-címkék lesz zárva.

   - A <ViewDefinitions> </ViewDefinitions> címkék megadása a `ViewDefinitions` csomópont. Minden nézet ezen a csomóponton belül vannak meghatározva.

3. Mentse a fájlt, a Windows PowerShell telepítési mappájában, a modul mappáját, vagy a modul mappa egyik almappájára. Használja a következő név formátumban, ha a fájl mentése: `MyFile.format.ps1xml`. Formázási fájlokat kell használnia a `.format.ps1xml` bővítmény.

   Most már készen áll a formázási fájl nézetek hozzáadása. Formázási-fájlban definiált nézetek száma nincs korlátozva van. Hozzáadhat egyetlen nézetben minden objektum, több nézetet ugyanahhoz az objektumhoz vagy több objektum által használt egyetlen nézetben.

## <a name="see-also"></a>Lásd még:

[Egy Windows PowerShell formázás és a fájl típusai](./writing-a-powershell-formatting-file.md)
