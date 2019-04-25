---
title: Kapcsolódó hivatkozások hozzáadása egy parancsmag súgó-témakörének |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5aadb730-4eb7-4936-b8df-3b0c0ca04fd5
caps.latest.revision: 5
ms.openlocfilehash: aa46cbc5bfcfdfec9fcf9d2581ff641baa532860
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083345"
---
# <a name="how-to-add-related-links-to-a-cmdlet-help-topic"></a><span data-ttu-id="145ad-102">Kapcsolódó hivatkozások hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="145ad-102">How to Add Related Links to a Cmdlet Help Topic</span></span>

<span data-ttu-id="145ad-103">Ez a szakasz ismerteti, hogyan adhat hozzá egy Windows PowerShell® parancsmag súgó-témakörének kapcsolódó más tartalomra mutató hivatkozások.</span><span class="sxs-lookup"><span data-stu-id="145ad-103">This section describes how to add references to other content that is related to a Windows PowerShell® cmdlet Help topic.</span></span> <span data-ttu-id="145ad-104">Ezeket a hivatkozásokat jelenik meg egy parancsablakot, mivel azok nem mutató közvetlen hivatkozás a hivatkozott tartalmat.</span><span class="sxs-lookup"><span data-stu-id="145ad-104">Because these references appear in a command window, they do not link directly to the referenced content.</span></span>

<span data-ttu-id="145ad-105">A parancsmag Súgó-témaköröket Windows PowerShell® részét képező, az ezeket a hivatkozásokat hivatkozhat, más parancsmagok, fogalmi tartalomra ("about_"), és egyéb dokumentumok és súgófájlokat, amelyek nem kapcsolódnak Windows PowerShell®.</span><span class="sxs-lookup"><span data-stu-id="145ad-105">In the cmdlet Help topics that are included in Windows PowerShell®, these links reference other cmdlets, conceptual content ("about_"), and other documents and Help files that are not related to Windows PowerShell®.</span></span>

<span data-ttu-id="145ad-106">A következő XML formátumú bemutatja, hogyan adhat hozzá, amely két kapcsolódó témakörök hivatkozásra hivatkozik RelatedLinks csomópontot.</span><span class="sxs-lookup"><span data-stu-id="145ad-106">The following XML shows how to add a RelatedLinks node that contains two references to related topics.</span></span>

```xml
<maml:relatedLinks>
  <maml:navigationLink>
    <maml:linkText>Topic-name</maml:linkText>
  </maml:navigationLink>
  <maml:navigationLink>
    <maml:linkText>Topic-name</maml:linkText>
  </maml:navigationLink>
</ maml:relatedLinks >
```



