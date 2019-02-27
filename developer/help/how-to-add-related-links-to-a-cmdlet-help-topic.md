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
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846388"
---
# <a name="how-to-add-related-links-to-a-cmdlet-help-topic"></a>Kapcsolódó hivatkozások hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz

Ez a szakasz ismerteti, hogyan adhat hozzá egy Windows PowerShell® parancsmag súgó-témakörének kapcsolódó más tartalomra mutató hivatkozások. Ezeket a hivatkozásokat jelenik meg egy parancsablakot, mivel azok nem mutató közvetlen hivatkozás a hivatkozott tartalmat.

A parancsmag Súgó-témaköröket Windows PowerShell® részét képező, az ezeket a hivatkozásokat hivatkozhat, más parancsmagok, fogalmi tartalomra ("about_"), és egyéb dokumentumok és súgófájlokat, amelyek nem kapcsolódnak Windows PowerShell®.

A következő XML formátumú bemutatja, hogyan adhat hozzá, amely két kapcsolódó témakörök hivatkozásra hivatkozik RelatedLinks csomópontot.

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



