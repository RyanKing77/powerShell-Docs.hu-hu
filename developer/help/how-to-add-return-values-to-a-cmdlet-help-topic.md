---
title: Egy parancsmag Súgó-témakör hozzáadása a visszaadandó értékek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a52ab737-753c-4d04-8af7-758d5c805e18
caps.latest.revision: 7
ms.openlocfilehash: b21811e5a5a819c3d5c4a55fcbe685a84819b71d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849216"
---
# <a name="how-to-add-return-values-to-a-cmdlet-help-topic"></a>Visszatérési értékek hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz

Ez a szakasz ismerteti a kimeneti szakasz Windows PowerShell® parancsmag Súgó-témakör hozzáadása. A kimeneti szakasz olyan objektum, a parancsmag adja vissza, vagy le a folyamat továbbítja a .NET-osztályok sorolja fel.

Az osztályok, amely a kimeneti szakasz is hozzáadhat száma nincs korlátozva van. Egy parancsmag návratové typy parancsfájlblokkjában találhatók egy \<parancs: returnValues > csomóponthoz, és minden egyes osztály idézőjelek között egy \<parancs: returnValue > elemet.

A parancsmag nem ad kimenetet, ha ez a szakasz segítségével jelzi, hogy semmilyen kimenet. Helyett az osztály nevét, például írhat "None", és a egy rövid magyarázatot. A parancsmag kimenete feltételesen állít elő, ha a csomópontot használva ismertetik a feltételeket, és ismertetik a feltételes kimenet.

A séma tartalmaz két \<maml:description > az egyes elemek \<parancs: returnValue > elemet. Azonban a `Get-Help` parancsmag megjeleníti a tartalma csak a \<parancs: returnValue > /\<maml:description > elemet.

Windows PowerShell 3.0-s verziójával kezdődően a `Get-Help` parancsmag megjeleníti a tartalmát a \<maml:uri > elemet. Ez az elem lehetővé teszi a .NET-osztály leíró témakörök felhasználókat.

A következő XML-mutatja a \<maml:returnValues > csomópont.

```xml
<command:returnValues>
  <command:returnValue>
    <dev:type>
      <maml:name> Class Name </maml:name>
      <maml:uri>  URI of a topic that describes the class </maml:uri>
      <maml:description/>
    </dev:type>
    <maml:description>
       <maml:para> Brief description <maml:para>

</maml:description>
  </command: returnValue>
</command: returnValues>
```

A következő XML formátumú használatának példája bemutatja a \<maml:returnValues > a dokumentum egy kimeneti típus a csomópontot.

```xml
<command:returnValues>
  <command:returnValue>
    <dev:type>
      <maml:name> System.DateTime </maml:name>
      <maml:uri>  http://msdn.microsoft.com/library/system.datetime.aspx </maml:uri>
      <maml:description/>
    </dev:type>
    <maml:description>
      <maml:para> Get-Date returns a DateTime object. <maml:para>
    </maml:description>
  </command: returnValue>
</command: returnValues>
```



