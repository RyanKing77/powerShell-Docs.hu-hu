---
title: A parancsmag súgóját fájl létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4a88dd89-6beb-494f-9e2a-6b10baed1a8d
caps.latest.revision: 17
ms.openlocfilehash: 08e05939f8aee42f2cd502a3da7a528d8460dec1
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848894"
---
# <a name="how-to-create-the-cmdlet-help-file"></a>Parancsmag súgófájljának létrehozása

Ez a szakasz azt ismerteti, hogyan hozhat létre, amely tartalmazza a Windows PowerShell parancsmagjaival kapcsolatos súgótémaköröket tartalmának érvényes XML-fájl. Ez a szakasz ismerteti a elnevezése a súgófájlban, a megfelelő XML-fejlécek felvétele és hogyan adhat hozzá csomópontokat, mely tartalmazni fogja a különböző szakaszokat, a parancsmag súgó tartalma.

> [!NOTE]
> A súgófájl, nyissa meg a dll-Help.xml fájlok a Windows PowerShell telepítési könyvtárában található teljes megjelenítéséhez. Például a Microsoft.PowerShell.Commands.Management.dll-Help.xml fájl tartalma számos, a Windows PowerShell-parancsmagok számára.

### <a name="how-to-create-a-cmdlet-help-file"></a>A parancsmag súgóját fájl létrehozása

1. Hozzon létre egy szövegfájlt, és mentse a UTF8 kódolást. A fájlnév formátuma a következő rendelkeznie kell, hogy a Windows PowerShell észlelheti a parancsmag súgó-fájlként.

   `<PSSnapInAssemblyName>.dll-Help.xml`

2. Adja hozzá a következő XML-fejlécek a szövegfájlba. Vegye figyelembe, hogy a fájl érvényesíti a több ügynök Modeling Language (MAML) sémának. Windows PowerShell jelenleg nem biztosít olyan eszközöket, a fájl ellenőrzéséhez.

   `<?xml version="1.0" encoding="utf-8" ?> <helpItems xmlns="http://msh" schema="maml">`

3. A parancs csomópont hozzáadása a parancsmag Súgó-fájlt az egyes parancsmagok a szerelvényben. A parancs csomóponton lévő összes csomópont vonatkozik, a parancsmag Súgó-témakör a különböző szakaszaiban.

   A következő táblázat felsorolja az XML-elem az egyes csomópontok, a leírások az egyes csomópontok követ.

   |Csomópont|Leírás|
   |----------|-----------------|
   |`<details>`|Hozzáadja a parancsmag súgó-témakörének nevét és a SZINOPSZIST szakaszait tartalmát. További információkért lásd: [hozzáadása a parancsmag neve és a Szinopszist](./how-to-add-the-cmdlet-name-and-synopsis-to-a-cmdlet-help-topic.md).|
   |`<maml:description>`|Adds content for the DESCRIPTION section of the cmdlet Help topic. További információkért lásd: [hozzáadása a részletes leírás egy parancsmag súgó-témakörének](./how-to-add-a-cmdlet-description.md).|
   |`<command:syntax>`|Hozzáadja a parancsmag súgó-témakörének szintaxis szakaszában tartalmát. További információkért lásd: [hozzáadása szintaxis egy parancsmag súgó-témakörének hogyan](./how-to-add-syntax-to-a-cmdlet-help-topic.md).|
   |`<command:parameters>`|Hozzáadja a tartalmat a parancsmag Súgó-témakör a paraméterek szakaszához. További információkért lásd: [paraméterek hozzáadása egy parancsmag súgó-témakörének hogyan](./how-to-add-parameter-information.md).|
   |`<command:inputTypes>`|Hozzáadja a parancsmag súgó-témakörének BEMENETEK szakaszában tartalmát. További információkért lásd: [bemeneti típusok hozzáadása egy parancsmag súgó-témakörének hogyan](./how-to-add-input-types-to-a-cmdlet-help-topic.md).|
   |`<command:returnValues>`|Hozzáadja a parancsmag súgó-témakörének, a kimeneti szakasz tartalmát. További információkért lásd: [hozzáadása vissza értékeket a parancsmag súgó-témakörének hogyan](./how-to-add-return-values-to-a-cmdlet-help-topic.md).|
   |`<maml:alertset>`|Tartalom hozzáadása a parancsmag Súgó-témakör a megjegyzések szakasza. További információkért lásd: [hozzáadása egy parancsmag súgó-témakörének megjegyzések](./how-to-add-notes-to-a-cmdlet-help-topic.md).|
   |`<command:examples>`|Hozzáadja a parancsmag súgó-témakörének példák szakaszában tartalmát. További információkért lásd: [példák hozzáadása egy parancsmag súgó-témakörének hogyan](./how-to-add-examples-to-a-cmdlet-help-topic.md).|
   |`<maml:relatedLinks>`|Hozzáadja a parancsmag súgó-témakörének kapcsolódó hivatkozások szakaszában tartalmát. További információkért lásd: [kapcsolódó hivatkozások hozzáadása egy parancsmag súgó-témakörének hogyan](./how-to-add-related-links-to-a-cmdlet-help-topic.md).|

## <a name="example"></a>Példa

 Íme egy példa, amely tartalmazza a csomópontok a különböző részeit, a parancsmag súgó-témakörének parancs csomópont.

```xml
<command:command
  xmlns:maml="http://schemas.microsoft.com/maml/2004/10"
  xmlns:command="http://schemas.microsoft.com/maml/dev/command/2004/10"
  xmlns:dev="http://schemas.microsoft.com/maml/dev/2004/10">
  <command:details>
    <!--Add name an synopsis here-->
  </command:details>
  <maml:description>
    <!--Add detailed description here-->
  </maml:description>
  <command:syntax>
    <!--Add syntax information here-->
  </command:syntax>
  <command:parameters>
    <!--Add parameter information here-->
  </command:parameters>
  <command:inputTypes>
    <!--Add input type information here-->
  </command:inputTypes>
  <command:returnValues>
    <!--Add return value information here-->
  </command:returnValues>
  <maml:alertSet>
    <!--Add Note information here-->
  </maml:alertSet>
  <command:examples>
    <!--Add cmdlet examples here-->
  </command:examples>
  <maml:relatedLinks>
    <!--Add links to related content here-->
  </maml:relatedLinks>
</command:command>
```

## <a name="see-also"></a>Lásd még:

 [A parancsmag neve és a Szinopszist hozzáadása](./how-to-add-the-cmdlet-name-and-synopsis-to-a-cmdlet-help-topic.md)

 [A részletes leírás egy parancsmag Súgó-témakör hozzáadása](./how-to-add-a-cmdlet-description.md)

 [Szintaxis egy parancsmag Súgó-témakör hozzáadása](./how-to-add-syntax-to-a-cmdlet-help-topic.md)

 [Egy parancsmag súgó-témakörének paraméterek hozzáadása](./how-to-add-parameter-information.md)

 [A bemeneti típusok egy parancsmag Súgó-témakör hozzáadása](./how-to-add-input-types-to-a-cmdlet-help-topic.md)

 [Visszaadott értékeket a parancsmag Súgó-témakör hozzáadása](./how-to-add-return-values-to-a-cmdlet-help-topic.md)

 [Hogyan adhat hozzá egy parancsmag súgó-témakörének megjegyzések](./how-to-add-notes-to-a-cmdlet-help-topic.md)

 [Példák, a parancsmag Súgó-témakör hozzáadása](./how-to-add-examples-to-a-cmdlet-help-topic.md)

 [Kapcsolódó hivatkozások hozzáadása egy parancsmag Súgó-témakör](./how-to-add-related-links-to-a-cmdlet-help-topic.md)

 [Windows PowerShell SDK](../windows-powershell-reference.md)