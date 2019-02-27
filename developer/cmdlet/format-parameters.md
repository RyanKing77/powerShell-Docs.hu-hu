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
ms.openlocfilehash: 4f24af9b32f785695d156bfb4784aa03c97e8987
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849419"
---
# <a name="format-parameters"></a><span data-ttu-id="04257-102">Formátumparaméterek</span><span class="sxs-lookup"><span data-stu-id="04257-102">Format Parameters</span></span>

<span data-ttu-id="04257-103">Az alábbi táblázat felsorolja a javasolt nevek és funkciók a paramétereket, formázását vagy az adatok létrehozása érdekében.</span><span class="sxs-lookup"><span data-stu-id="04257-103">The following table lists recommended names and functionality for parameters that are used to format or to generate data.</span></span>

<span data-ttu-id="04257-104">Adatok típusa: Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="04257-104">As Data type: Keyword</span></span>

<span data-ttu-id="04257-105">Ezzel a paraméterrel adja meg a parancsmag kimeneti formátum megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="04257-105">Implement this parameter to specify the cmdlet output format.</span></span> <span data-ttu-id="04257-106">A lehetséges értékek lehet például szöveg vagy parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="04257-106">For example, possible values could be Text or Script.</span></span>

<span data-ttu-id="04257-107">Bináris adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="04257-107">Binary Data type: SwitchParameter</span></span>

<span data-ttu-id="04257-108">Ez a paraméter jelzi, hogy a parancsmag kezeli-e a bináris értékek megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="04257-108">Implement this parameter to indicate that the cmdlet handles binary values.</span></span>

<span data-ttu-id="04257-109">Kódolási adattípus: Kulcsszó</span><span class="sxs-lookup"><span data-stu-id="04257-109">Encoding Data type: Keyword</span></span>

<span data-ttu-id="04257-110">Ez a paraméter határozza meg a típusát, amely támogatott a kódolási megvalósításához.</span><span class="sxs-lookup"><span data-stu-id="04257-110">Implement this parameter to specify the type of encoding that is supported.</span></span> <span data-ttu-id="04257-111">Ha például a lehetséges értékek lehet ASCII, UTF8, Unicode, UTF7, Toto, bájt, és karakterlánc.</span><span class="sxs-lookup"><span data-stu-id="04257-111">For example, possible values could be ASCII, UTF8, Unicode, UTF7, BigEndianUnicode, Byte, and String.</span></span>

<span data-ttu-id="04257-112">Új sor adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="04257-112">NewLine Data type: SwitchParameter</span></span>

<span data-ttu-id="04257-113">Ez a paraméter valósítja meg, hogy a sortörés karakterek támogatottak, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="04257-113">Implement this parameter so that the newline characters are supported when the parameter is specified.</span></span>

<span data-ttu-id="04257-114">A ShortName adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="04257-114">ShortName Data type: SwitchParameter</span></span>

<span data-ttu-id="04257-115">Ez a paraméter valósítja meg, hogy rövid nevek használata támogatott, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="04257-115">Implement this parameter so that short names are supported when the parameter is specified.</span></span>

<span data-ttu-id="04257-116">Szélesség adattípus: Int32</span><span class="sxs-lookup"><span data-stu-id="04257-116">Width Data type: Int32</span></span>

<span data-ttu-id="04257-117">Ez a paraméter valósítja meg, hogy a felhasználó megadhatja a kimeneti eszköz szélességét.</span><span class="sxs-lookup"><span data-stu-id="04257-117">Implement this parameter so that the user can specify the width of the output device.</span></span>

<span data-ttu-id="04257-118">Wrap adattípus: SwitchParameter</span><span class="sxs-lookup"><span data-stu-id="04257-118">Wrap Data type: SwitchParameter</span></span>

<span data-ttu-id="04257-119">Ez a paraméter valósítja meg, hogy körbefuttatási használata támogatott, ha a paraméter meg van adva.</span><span class="sxs-lookup"><span data-stu-id="04257-119">Implement this parameter so that text wrapping is supported when the parameter is specified.</span></span>

## <a name="see-also"></a><span data-ttu-id="04257-120">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="04257-120">See Also</span></span>

[<span data-ttu-id="04257-121">Parancsmag-paraméterek</span><span class="sxs-lookup"><span data-stu-id="04257-121">Cmdlet Parameters</span></span>](./cmdlet-parameters.md)

[<span data-ttu-id="04257-122">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="04257-122">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="04257-123">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="04257-123">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
