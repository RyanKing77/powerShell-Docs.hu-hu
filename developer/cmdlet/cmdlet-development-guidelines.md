---
title: A parancsmag fejlesztői útmutató |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- development guidelines [PowerShell Programmer's Guide]
- cmdlets [PowerShell Programmer's Guide], development guidelines
ms.assetid: c30cc3c0-e958-4a8f-b81f-1e38de772f13
caps.latest.revision: 14
ms.openlocfilehash: 89c7682e87fa6f389349fc44275be0d2ffc83957
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068572"
---
# <a name="cmdlet-development-guidelines"></a><span data-ttu-id="1a6fa-102">Parancsmagfejlesztői útmutató</span><span class="sxs-lookup"><span data-stu-id="1a6fa-102">Cmdlet Development Guidelines</span></span>

<span data-ttu-id="1a6fa-103">Az ebben a szakaszban lévő témakörök nyújtanak a fejlesztési, amellyel megfelelően formázott parancsmagok előállításához.</span><span class="sxs-lookup"><span data-stu-id="1a6fa-103">The topics in this section provide development guidelines that you can use to produce well-formed cmdlets.</span></span> <span data-ttu-id="1a6fa-104">Ezen irányelvek betartása és a Windows PowerShell-modul által biztosított általános szolgáltatásokat kihasználva minimális erőfeszítéssel robusztus parancsmagok fejlesztéséhez és egységes felhasználói élményt biztosíthat a felhasználónak.</span><span class="sxs-lookup"><span data-stu-id="1a6fa-104">By leveraging the common functionality provided by the Windows PowerShell runtime and by following these guidelines, you can develop robust cmdlets with minimal effort and provide the user with a consistent experience.</span></span> <span data-ttu-id="1a6fa-105">Emellett a tesztelési terheket fog csökkenti, mert a közös funkciók nem szükséges időt.</span><span class="sxs-lookup"><span data-stu-id="1a6fa-105">Additionally, you will reduce the test burden because common functionality does not require retesting.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="1a6fa-106">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="1a6fa-106">In This Section</span></span>

- [<span data-ttu-id="1a6fa-107">Szükséges fejlesztési irányelvek</span><span class="sxs-lookup"><span data-stu-id="1a6fa-107">Required Development Guidelines</span></span>](./required-development-guidelines.md)

- [<span data-ttu-id="1a6fa-108">Erősen javasolt fejlesztői útmutató</span><span class="sxs-lookup"><span data-stu-id="1a6fa-108">Strongly Encouraged Development Guidelines</span></span>](./strongly-encouraged-development-guidelines.md)

- [<span data-ttu-id="1a6fa-109">Tanácsadói fejlesztői útmutató</span><span class="sxs-lookup"><span data-stu-id="1a6fa-109">Advisory Development Guidelines</span></span>](./advisory-development-guidelines.md)

## <a name="see-also"></a><span data-ttu-id="1a6fa-110">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1a6fa-110">See Also</span></span>

[<span data-ttu-id="1a6fa-111">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="1a6fa-111">Writing a Windows PowerShell Cmdlet</span></span>](./writing-a-windows-powershell-cmdlet.md)

[<span data-ttu-id="1a6fa-112">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="1a6fa-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)
