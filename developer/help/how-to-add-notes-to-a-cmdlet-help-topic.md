---
title: Megjegyzések hozzáadása egy parancsmag súgó-témakörének |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2bea35e5-b680-4f86-b928-176890aac99d
caps.latest.revision: 5
ms.openlocfilehash: 4e9ca9a3bbcbc900d079b9275bc47d21de9e2996
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083416"
---
# <a name="how-to-add-notes-to-a-cmdlet-help-topic"></a><span data-ttu-id="50729-102">Jegyzetek hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="50729-102">How to Add Notes to a Cmdlet Help Topic</span></span>

<span data-ttu-id="50729-103">Ez a szakasz ismerteti a megjegyzések szakasza Windows PowerShell® parancsmag Súgó-témakör hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="50729-103">This section describes how to add a Notes section to a Windows PowerShell® cmdlet Help topic.</span></span> <span data-ttu-id="50729-104">A megjegyzések szakasza azt ismertetik, amelyek nem férnek el egyszerűen a többi strukturált szakaszokra, például egy paraméter részletesebb magyarázatáért részletek szolgál.</span><span class="sxs-lookup"><span data-stu-id="50729-104">The Notes section is used to explain details that do not fit easily into the other structured sections, such as a more detailed explanation of a parameter.</span></span> <span data-ttu-id="50729-105">Ez a tartalom magában foglalhatja a parancsmag működését egy adott szolgáltató, néhány egyedi, de fontos, használja a parancsmag vagy a lehetséges hibaállapotok elkerülésének fűzött megjegyzések.</span><span class="sxs-lookup"><span data-stu-id="50729-105">This content could include comments on how the cmdlet works with a specific provider, some unique, yet important, uses of the cmdlet, or ways to avoid possible error conditions.</span></span>

<span data-ttu-id="50729-106">Tudomásul veszi, hogy is hozzáadhat a megjegyzések szakasza száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="50729-106">There are no limits to the number of notes that you can add to a Notes section.</span></span> <span data-ttu-id="50729-107">Minden egyes Megjegyzés hozzáadása egy \<maml:alert > címkét rendel a \<maml:alertset > csomópont.</span><span class="sxs-lookup"><span data-stu-id="50729-107">For each note, add a pair of \<maml:alert> tags to the \<maml:alertset> node.</span></span> <span data-ttu-id="50729-108">Az egyes Megjegyzés tartalmakról halmazába \<maml:para > címkéket.</span><span class="sxs-lookup"><span data-stu-id="50729-108">The content of each note is added within a set of \<maml:para> tags.</span></span> <span data-ttu-id="50729-109">Használat üres \<maml:para > térköze címke.</span><span class="sxs-lookup"><span data-stu-id="50729-109">Use blank \<maml:para> tags for spacing.</span></span>

<span data-ttu-id="50729-110">A következő XML-mutatja egy \<maml:alertset > csomópont két megjegyzések.</span><span class="sxs-lookup"><span data-stu-id="50729-110">The following XML shows an \<maml:alertset> node with two notes.</span></span> <span data-ttu-id="50729-111">Figyelje meg, hogy minden egyes Megjegyzés rendelkezik egy nem kötelező \<maml:title > címke (címek segítségével minden olyan csoport \<maml:alert > címkék), és, hogy minden egyes Megjegyzés rendelkezik egy üres sort térköz tartalmát a következő.</span><span class="sxs-lookup"><span data-stu-id="50729-111">Notice that each note has an optional \<maml:title> tag (titles can be used to group any set of \<maml:alert> tags), and that each note has a blank line following the content for spacing.</span></span>

```xml
<maml:alertSet>
  <maml:title>title for Note 1</maml:title>
  <maml:alert>
    <maml:para> Note 1</maml:para>
    <maml:para></maml:para>
  </maml:alert>
  <maml:title>title for Note 2</maml:title>
  <maml:alert>
    <maml:para> Note 1</maml:para>
    <maml:para></maml:para>
  </maml:alert>
</maml:alertSet>
```



