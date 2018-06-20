---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: A Windows PowerShell használatának első lépései
ms.assetid: b0e2ad92-875f-421d-b612-f624e644aa69
ms.openlocfilehash: d8f1a416c1618040311ec0ea3b98b28aa432bcf1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30949485"
---
# <a name="getting-started-with-windows-powershell"></a><span data-ttu-id="14a96-103">A Windows PowerShell használatának első lépései</span><span class="sxs-lookup"><span data-stu-id="14a96-103">Getting Started with Windows PowerShell</span></span>
<span data-ttu-id="14a96-104">A Windows PowerShell egy Windows parancssori rendszerhéj, kifejezetten rendszergazdák számára tervezett.</span><span class="sxs-lookup"><span data-stu-id="14a96-104">Windows PowerShell is a Windows command-line shell designed especially for system administrators.</span></span> <span data-ttu-id="14a96-105">A Windows PowerShell tartalmaz egy interaktív kérdés és a parancsfájl-kezelési környezet, amely külön vagy együtt használható.</span><span class="sxs-lookup"><span data-stu-id="14a96-105">Windows PowerShell includes an interactive prompt and a scripting environment that can be used independently or in combination.</span></span>

<span data-ttu-id="14a96-106">Ellentétben a legtöbb ismertetése, amely fogadja el, és térjen vissza a szöveg, Windows PowerShell a .NET-keretrendszer közös nyelvi futtatókörnyezet (CLR) és a .NET-keretrendszer épül, és fogad, és adja vissza a .NET keretrendszer objektumait.</span><span class="sxs-lookup"><span data-stu-id="14a96-106">Unlike most shells, which accept and return text, Windows PowerShell is built on top of the .NET Framework common language runtime (CLR) and the .NET Framework, and accepts and returns .NET Framework objects.</span></span> <span data-ttu-id="14a96-107">A kezelési és a Windows konfigurációs biztosítható teljesen új eszközök és módszerek az ebben a környezetben alapvető módosítása.</span><span class="sxs-lookup"><span data-stu-id="14a96-107">This fundamental change in the environment brings entirely new tools and methods to the management and configuration of Windows.</span></span>

<span data-ttu-id="14a96-108">A Windows PowerShell parancsmag (hangsúlyozottan "parancs-let"), egy egyszerű, egy funkcióval parancssori eszköz a rendszerhéj épített bemutatja.</span><span class="sxs-lookup"><span data-stu-id="14a96-108">Windows PowerShell introduces the concept of a cmdlet (pronounced "command-let"), a simple, single-function command-line tool built into the shell.</span></span> <span data-ttu-id="14a96-109">Minden parancsmagot külön használhatja, de a power létrejött használatakor ezek egyszerű eszközökkel együtt összetett feladatok elvégzéséhez.</span><span class="sxs-lookup"><span data-stu-id="14a96-109">You can use each cmdlet separately, but their power is realized when you use these simple tools in combination to perform complex tasks.</span></span> <span data-ttu-id="14a96-110">Windows PowerShell több mint száz alapszintű parancsmagot foglal magában, és a saját parancsmagok írhat és más felhasználókkal való megosztására.</span><span class="sxs-lookup"><span data-stu-id="14a96-110">Windows PowerShell includes more than one hundred basic core cmdlets, and you can write your own cmdlets and share them with other users.</span></span>

<span data-ttu-id="14a96-111">Sok ismertetése, például a Windows PowerShell hozzáférést biztosít a fájlrendszer azon a számítógépen.</span><span class="sxs-lookup"><span data-stu-id="14a96-111">Like many shells, Windows PowerShell gives you access to the file system on the computer.</span></span> <span data-ttu-id="14a96-112">Emellett a Windows PowerShell *szolgáltatók* lehetővé teszik a hozzáférést, más, például a beállításjegyzék és a digitális aláírás tanúsítványtárolókat könnyen férhet hozzá a fájlrendszerhez.</span><span class="sxs-lookup"><span data-stu-id="14a96-112">In addition, Windows PowerShell *providers* enable you to access other data stores, such as the registry and the digital signature certificate stores, as easily as you access the file system.</span></span>

<span data-ttu-id="14a96-113">Az első lépések útmutató mutatja be Windows PowerShell: a nyelv, a parancsmagok, a szolgáltatók és az objektumok használatát.</span><span class="sxs-lookup"><span data-stu-id="14a96-113">This Getting Started guide provides an introduction to Windows PowerShell: the language, the cmdlets, the providers, and the use of objects.</span></span>

<span data-ttu-id="14a96-114">Ebben a témakörben:</span><span class="sxs-lookup"><span data-stu-id="14a96-114">In this topic:</span></span>

- [<span data-ttu-id="14a96-115">Windows PowerShell rendszerkövetelményei</span><span class="sxs-lookup"><span data-stu-id="14a96-115">Windows PowerShell System Requirements</span></span>](../setup/Windows-PowerShell-System-Requirements.md)

- [<span data-ttu-id="14a96-116">Windows PowerShell telepítése</span><span class="sxs-lookup"><span data-stu-id="14a96-116">Installing Windows PowerShell</span></span>](../setup/Installing-Windows-PowerShell.md)

- [<span data-ttu-id="14a96-117">A Windows PowerShell indítása</span><span class="sxs-lookup"><span data-stu-id="14a96-117">Starting Windows PowerShell</span></span>](../setup/Starting-Windows-PowerShell.md)

- [<span data-ttu-id="14a96-118">Felkészülés a Windows PowerShell használatával</span><span class="sxs-lookup"><span data-stu-id="14a96-118">Getting Ready to Use Windows PowerShell</span></span>](Getting-Ready-to-Use-Windows-PowerShell.md)