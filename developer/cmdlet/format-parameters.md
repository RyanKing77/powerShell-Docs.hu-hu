---
title: Paraméterek formázása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 10e025c5-9aa6-45a5-b851-23d14db1f4cc
caps.latest.revision: 7
ms.openlocfilehash: 0bd3888d81aa6d1dde26c0066f7bca9dac8a8bca
ms.sourcegitcommit: ce46e5098786e19d521b4bf948ff62d2b90bc53e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/02/2019
ms.locfileid: "57251183"
---
# <a name="format-parameters"></a><span data-ttu-id="51d12-102">Formátumparaméterek</span><span class="sxs-lookup"><span data-stu-id="51d12-102">Format Parameters</span></span>

<span data-ttu-id="51d12-103">Az alábbi táblázat felsorolja a javasolt nevek és funkciók a paramétereket, formázását vagy az adatok létrehozása érdekében.</span><span class="sxs-lookup"><span data-stu-id="51d12-103">The following table lists recommended names and functionality for parameters that are used to format or to generate data.</span></span>

|<span data-ttu-id="51d12-104">Paraméter</span><span class="sxs-lookup"><span data-stu-id="51d12-104">Parameter</span></span>|<span data-ttu-id="51d12-105">Funkció</span><span class="sxs-lookup"><span data-stu-id="51d12-105">Functionality</span></span>|
|---|---|
|<span data-ttu-id="51d12-106">**Mint**</span><span class="sxs-lookup"><span data-stu-id="51d12-106">**As**</span></span><br><span data-ttu-id="51d12-107">Adattípus: Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="51d12-107">Data type: Keyword</span></span>|<span data-ttu-id="51d12-108">Ezzel a paraméterrel adja meg a parancsmag kimeneti formátum megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="51d12-108">Implement this parameter to specify the cmdlet output format.</span></span> <span data-ttu-id="51d12-109">A lehetséges értékek lehet például szöveg vagy parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="51d12-109">For example, possible values could be Text or Script.</span></span>|
|<span data-ttu-id="51d12-110">**Bináris**</span><span class="sxs-lookup"><span data-stu-id="51d12-110">**Binary**</span></span><br><span data-ttu-id="51d12-111">Adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="51d12-111">Data type: SwitchParameter</span></span>|<span data-ttu-id="51d12-112">Ez a paraméter jelzi, hogy a parancsmag kezeli-e a bináris értékek megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="51d12-112">Implement this parameter to indicate that the cmdlet handles binary values.</span></span>|
|<span data-ttu-id="51d12-113">**Kódolás**</span><span class="sxs-lookup"><span data-stu-id="51d12-113">**Encoding**</span></span><br><span data-ttu-id="51d12-114">Adattípus: Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="51d12-114">Data type: Keyword</span></span>|<span data-ttu-id="51d12-115">Ez a paraméter határozza meg a típusát, amely támogatott a kódolási megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="51d12-115">Implement this parameter to specify the type of encoding that is supported.</span></span> <span data-ttu-id="51d12-116">Ha például a lehetséges értékek lehet ASCII, UTF8, Unicode, UTF7, Toto, bájt, és karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="51d12-116">For example, possible values could be ASCII, UTF8, Unicode, UTF7, BigEndianUnicode, Byte, and String.</span></span>|
|<span data-ttu-id="51d12-117">**Új sor**</span><span class="sxs-lookup"><span data-stu-id="51d12-117">**NewLine**</span></span><br><span data-ttu-id="51d12-118">Adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="51d12-118">Data type: SwitchParameter</span></span>|<span data-ttu-id="51d12-119">Ez a paraméter valósítja meg, hogy a sortörés karakterek támogatottak, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="51d12-119">Implement this parameter so that the newline characters are supported when the parameter is specified.</span></span>|
|<span data-ttu-id="51d12-120">**A ShortName**</span><span class="sxs-lookup"><span data-stu-id="51d12-120">**ShortName**</span></span><br><span data-ttu-id="51d12-121">Adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="51d12-121">Data type: SwitchParameter</span></span>|<span data-ttu-id="51d12-122">Ez a paraméter valósítja meg, hogy rövid nevek használata támogatott, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="51d12-122">Implement this parameter so that short names are supported when the parameter is specified.</span></span>|
|<span data-ttu-id="51d12-123">**Szélesség**</span><span class="sxs-lookup"><span data-stu-id="51d12-123">**Width**</span></span><br><span data-ttu-id="51d12-124">Adattípus: Int32</span><span class="sxs-lookup"><span data-stu-id="51d12-124">Data type: Int32</span></span>|<span data-ttu-id="51d12-125">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kimeneti eszköz szélességét.</span><span class="sxs-lookup"><span data-stu-id="51d12-125">Implement this parameter so that the user can specify the width of the output device.</span></span>|
|<span data-ttu-id="51d12-126">**Wrap**</span><span class="sxs-lookup"><span data-stu-id="51d12-126">**Wrap**</span></span><br><span data-ttu-id="51d12-127">Adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="51d12-127">Data type: SwitchParameter</span></span>|<span data-ttu-id="51d12-128">Ez a paraméter valósítja meg, hogy körbefuttatási használata támogatott, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="51d12-128">Implement this parameter so that text wrapping is supported when the parameter is specified.</span></span>|
## <a name="see-also"></a><span data-ttu-id="51d12-129">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="51d12-129">See Also</span></span>

[<span data-ttu-id="51d12-130">Parancsmag-paraméterek</span><span class="sxs-lookup"><span data-stu-id="51d12-130">Cmdlet Parameters</span></span>](./cmdlet-parameters.md)

[<span data-ttu-id="51d12-131">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="51d12-131">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="51d12-132">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="51d12-132">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
