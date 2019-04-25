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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083433"
---
# <a name="how-to-add-input-types-to-a-cmdlet-help-topic"></a><span data-ttu-id="c7b27-102">Bemeneti típusok hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="c7b27-102">How to Add Input Types to a Cmdlet Help Topic</span></span>

<span data-ttu-id="c7b27-103">Ez a szakasz egy bemeneti szakasz hozzáadása egy Windows PowerShell® parancsmag Súgó-témakör ismerteti.</span><span class="sxs-lookup"><span data-stu-id="c7b27-103">This section describes how to add an INPUTS section to a Windows PowerShell® cmdlet Help topic.</span></span> <span data-ttu-id="c7b27-104">A BEMENETEK a szakasz a .NET-osztályok olyan objektum, a parancsmag elfogadja az adatcsatornából bemenetként az érték vagy tulajdonságnév.</span><span class="sxs-lookup"><span data-stu-id="c7b27-104">The INPUTS section lists the .NET classes of objects that the cmdlet accepts as input from the pipeline, either by value or by property name.</span></span>

<span data-ttu-id="c7b27-105">Az osztályok, adhat hozzá egy bemeneti szakasz száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="c7b27-105">There is no limit to the number of classes that you can add to an INPUTS section.</span></span> <span data-ttu-id="c7b27-106">A bemeneti típusok parancsfájlblokkjában találhatók egy \<parancs: inputTypes > csomóponthoz, és minden egyes osztály idézőjelek között egy \<parancs: inputType > elemet.</span><span class="sxs-lookup"><span data-stu-id="c7b27-106">The input types are enclosed in a \<command:inputTypes> node, with each class enclosed in a  \<command:inputType> element.</span></span>

<span data-ttu-id="c7b27-107">A séma tartalmaz két \<maml:description > az egyes elemek \<parancs: inputType > elemet.</span><span class="sxs-lookup"><span data-stu-id="c7b27-107">The schema includes two \<maml:description> elements in each \<command:inputType> element.</span></span> <span data-ttu-id="c7b27-108">Azonban a `Get-Help` parancsmag megjeleníti a tartalma csak a \<parancs: inputType > /\<maml:description >) elemet.</span><span class="sxs-lookup"><span data-stu-id="c7b27-108">However, the `Get-Help` cmdlet displays only the content of the \<command:inputType>/\<maml:description>) element.</span></span>

<span data-ttu-id="c7b27-109">Windows PowerShell 3.0-s verziójával kezdődően a `Get-Help` parancsmag megjeleníti a tartalmát a \<maml:uri > elemet.</span><span class="sxs-lookup"><span data-stu-id="c7b27-109">Beginning in Windows PowerShell 3.0, the `Get-Help` cmdlet displays the content of the \<maml:uri> element.</span></span> <span data-ttu-id="c7b27-110">Ez az elem lehetővé teszi a .NET-osztály leíró témakörök felhasználókat.</span><span class="sxs-lookup"><span data-stu-id="c7b27-110">This element lets you direct users to topics that describe the .NET class.</span></span>

<span data-ttu-id="c7b27-111">A következő XML-mutatja a \<maml:inputTypes > csomópont.</span><span class="sxs-lookup"><span data-stu-id="c7b27-111">The following XML shows the \<maml:inputTypes> node.</span></span>

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

<span data-ttu-id="c7b27-112">A következő XML formátumú használatának példája bemutatja a \<maml:inputTypes > a csomópontot a dokumentum egy bemeneti típusa.</span><span class="sxs-lookup"><span data-stu-id="c7b27-112">The following XML shows an example of using the \<maml:inputTypes> node to document an input type.</span></span>

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