---
title: A bemeneti típusok hozzáadása egy parancsmag súgó-témakörének |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 432798e4-5d69-46b1-9517-ff09bffaa4be
caps.latest.revision: 7
ms.openlocfilehash: f213605dda0132051d983f8608515325e815c455
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850175"
---
# <a name="how-to-add-input-types-to-a-cmdlet-help-topic"></a>Bemeneti típusok hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz

Ez a szakasz egy bemeneti szakasz hozzáadása egy Windows PowerShell® parancsmag Súgó-témakör ismerteti. A BEMENETEK a szakasz a .NET-osztályok olyan objektum, a parancsmag elfogadja az adatcsatornából bemenetként az érték vagy tulajdonságnév.

Az osztályok, adhat hozzá egy bemeneti szakasz száma nincs korlátozva van. A bemeneti típusok parancsfájlblokkjában találhatók egy \<parancs: inputTypes > csomóponthoz, és minden egyes osztály idézőjelek között egy \<parancs: inputType > elemet.

A séma tartalmaz két \<maml:description > az egyes elemek \<parancs: inputType > elemet. Azonban a `Get-Help` parancsmag megjeleníti a tartalma csak a \<parancs: inputType > /\<maml:description >) elemet.

Windows PowerShell 3.0-s verziójával kezdődően a `Get-Help` parancsmag megjeleníti a tartalmát a \<maml:uri > elemet. Ez az elem lehetővé teszi a .NET-osztály leíró témakörök felhasználókat.

A következő XML-mutatja a \<maml:inputTypes > csomópont.

```xml
<command:inputTypes>
  <command:inputType>
    <dev:type>
      <maml:name> Class name </maml:name>
      <maml:uri>  URI of a topic that describes the class </maml:uri>
      <maml:description/>
    </dev:type>
    <maml:description>
      <maml:para> Brief description </maml:para>
    </maml:description>
  </command:inputType>
</command:inputTypes>
```

A következő XML formátumú használatának példája bemutatja a \<maml:inputTypes > a csomópontot a dokumentum egy bemeneti típusa.

```xml
<command:inputTypes>
  <command:inputType>
    <dev:type>
      <maml:name> System.DateTime </maml:name>
      <maml:uri>  http://msdn.microsoft.com/library/system.datetime.aspx </maml:uri>
      <maml:description/>
    </dev:type>
    <maml:description>
      <maml:para> You can pipe a date to the Set-Date cmdlet. <maml:para>
    <maml:description>
  </command:inputType>
</command:inputTypes>
```