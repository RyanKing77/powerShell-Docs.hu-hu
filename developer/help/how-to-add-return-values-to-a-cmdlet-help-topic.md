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
# <a name="how-to-add-return-values-to-a-cmdlet-help-topic"></a><span data-ttu-id="e0e65-102">Visszatérési értékek hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="e0e65-102">How to Add Return Values to a Cmdlet Help Topic</span></span>

<span data-ttu-id="e0e65-103">Ez a szakasz ismerteti a kimeneti szakasz Windows PowerShell® parancsmag Súgó-témakör hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="e0e65-103">This section describes how to add an OUTPUTS section to a Windows PowerShell® cmdlet Help topic.</span></span> <span data-ttu-id="e0e65-104">A kimeneti szakasz olyan objektum, a parancsmag adja vissza, vagy le a folyamat továbbítja a .NET-osztályok sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="e0e65-104">The OUTPUTS section lists the .NET classes of objects that the cmdlet returns or passes down the pipeline.</span></span>

<span data-ttu-id="e0e65-105">Az osztályok, amely a kimeneti szakasz is hozzáadhat száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="e0e65-105">There is no limit to the number of classes that you can add to the OUTPUTS section.</span></span> <span data-ttu-id="e0e65-106">Egy parancsmag návratové typy parancsfájlblokkjában találhatók egy \<parancs: returnValues > csomóponthoz, és minden egyes osztály idézőjelek között egy \<parancs: returnValue > elemet.</span><span class="sxs-lookup"><span data-stu-id="e0e65-106">The return types of a cmdlet are enclosed in a \<command:returnValues> node, with each class enclosed in a \<command:returnValue> element.</span></span>

<span data-ttu-id="e0e65-107">A parancsmag nem ad kimenetet, ha ez a szakasz segítségével jelzi, hogy semmilyen kimenet.</span><span class="sxs-lookup"><span data-stu-id="e0e65-107">If a cmdlet does not generate any output, use this section to indicate that there is no output.</span></span> <span data-ttu-id="e0e65-108">Helyett az osztály nevét, például írhat "None", és a egy rövid magyarázatot.</span><span class="sxs-lookup"><span data-stu-id="e0e65-108">For example, in place of the class name, write "None" and provide a brief explanation.</span></span> <span data-ttu-id="e0e65-109">A parancsmag kimenete feltételesen állít elő, ha a csomópontot használva ismertetik a feltételeket, és ismertetik a feltételes kimenet.</span><span class="sxs-lookup"><span data-stu-id="e0e65-109">If the cmdlet generates output conditionally, use this node to explain the conditions and describe the conditional output.</span></span>

<span data-ttu-id="e0e65-110">A séma tartalmaz két \<maml:description > az egyes elemek \<parancs: returnValue > elemet.</span><span class="sxs-lookup"><span data-stu-id="e0e65-110">The schema includes two \<maml:description> elements in each \<command:returnValue> element.</span></span> <span data-ttu-id="e0e65-111">Azonban a `Get-Help` parancsmag megjeleníti a tartalma csak a \<parancs: returnValue > /\<maml:description > elemet.</span><span class="sxs-lookup"><span data-stu-id="e0e65-111">However, the `Get-Help` cmdlet displays only the content of the \<command:returnValue>/\<maml:description> element.</span></span>

<span data-ttu-id="e0e65-112">Windows PowerShell 3.0-s verziójával kezdődően a `Get-Help` parancsmag megjeleníti a tartalmát a \<maml:uri > elemet.</span><span class="sxs-lookup"><span data-stu-id="e0e65-112">Beginning in Windows PowerShell 3.0, the `Get-Help` cmdlet displays the content of the \<maml:uri> element.</span></span> <span data-ttu-id="e0e65-113">Ez az elem lehetővé teszi a .NET-osztály leíró témakörök felhasználókat.</span><span class="sxs-lookup"><span data-stu-id="e0e65-113">This element lets you direct users to topics that describe the .NET class.</span></span>

<span data-ttu-id="e0e65-114">A következő XML-mutatja a \<maml:returnValues > csomópont.</span><span class="sxs-lookup"><span data-stu-id="e0e65-114">The following XML shows the \<maml:returnValues> node.</span></span>

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

<span data-ttu-id="e0e65-115">A következő XML formátumú használatának példája bemutatja a \<maml:returnValues > a dokumentum egy kimeneti típus a csomópontot.</span><span class="sxs-lookup"><span data-stu-id="e0e65-115">The following XML shows an example of using the \<maml:returnValues> node to document an output type.</span></span>

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



