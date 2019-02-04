---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A Windows PowerShell használatának első lépései
ms.assetid: b0e2ad92-875f-421d-b612-f624e644aa69
ms.openlocfilehash: 8a158427d319e43ec011898fe4e1826d48d5b951
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685549"
---
# <a name="getting-started-with-windows-powershell"></a><span data-ttu-id="79976-103">A Windows PowerShell használatának első lépései</span><span class="sxs-lookup"><span data-stu-id="79976-103">Getting Started with Windows PowerShell</span></span>
<span data-ttu-id="79976-104">Windows PowerShell az egy Windows parancssori rendszerhéj, különösen a rendszergazdák számára terveztek.</span><span class="sxs-lookup"><span data-stu-id="79976-104">Windows PowerShell is a Windows command-line shell designed especially for system administrators.</span></span> <span data-ttu-id="79976-105">Windows PowerShell tartalmaz egy interaktív kérdés és a egy parancsfájl-kezelési környezet, amely önállóan vagy együtt is használhatók.</span><span class="sxs-lookup"><span data-stu-id="79976-105">Windows PowerShell includes an interactive prompt and a scripting environment that can be used independently or in combination.</span></span>

<span data-ttu-id="79976-106">Legtöbb rendszerhéjjal ellentétben, amelyek fogadja el, és a visszaadott szöveg, Windows PowerShell a .NET-keretrendszer közös nyelvi futtatókörnyezet (CLR) és a .NET-keretrendszer épül, és fogadja el, és adja vissza a .NET keretrendszer objektumait.</span><span class="sxs-lookup"><span data-stu-id="79976-106">Unlike most shells, which accept and return text, Windows PowerShell is built on top of the .NET Framework common language runtime (CLR) and the .NET Framework, and accepts and returns .NET Framework objects.</span></span> <span data-ttu-id="79976-107">Ez a alapvető változtatás a környezet kezelése és a Windows configuration teljesen új eszközöket és módszereket biztosít.</span><span class="sxs-lookup"><span data-stu-id="79976-107">This fundamental change in the environment brings entirely new tools and methods to the management and configuration of Windows.</span></span>

<span data-ttu-id="79976-108">Windows PowerShell bevezeti a parancsmag fogalmát (ejtsd "parancsmagot"), egy egyszerű, egyfunkciós parancssori eszköz, amely a rendszerhéjba van beépítve.</span><span class="sxs-lookup"><span data-stu-id="79976-108">Windows PowerShell introduces the concept of a cmdlet (pronounced "command-let"), a simple, single-function command-line tool built into the shell.</span></span> <span data-ttu-id="79976-109">Minden parancsmagot külön-külön használhatja, de azok power létrejött használatakor ezek az egyszerű eszközök együttes alkalmazásával összetett feladatok végrehajtásához.</span><span class="sxs-lookup"><span data-stu-id="79976-109">You can use each cmdlet separately, but their power is realized when you use these simple tools in combination to perform complex tasks.</span></span> <span data-ttu-id="79976-110">Windows PowerShell több mint száz alapszintű fő parancsmagot tartalmaz, és írhat saját parancsmagjai és más felhasználókkal való megosztására.</span><span class="sxs-lookup"><span data-stu-id="79976-110">Windows PowerShell includes more than one hundred basic core cmdlets, and you can write your own cmdlets and share them with other users.</span></span>

<span data-ttu-id="79976-111">Hány környezetválasztóval, például a Windows PowerShell hozzáférést biztosít a fájlrendszerben azon a számítógépen.</span><span class="sxs-lookup"><span data-stu-id="79976-111">Like many shells, Windows PowerShell gives you access to the file system on the computer.</span></span> <span data-ttu-id="79976-112">Ezenkívül a Windows PowerShell *szolgáltatók* más adattárakban, például a beállításjegyzék és a digitális aláírás tanúsítványtárolókban könnyedén hozzáférhet a fájlrendszer elérését teszik lehetővé.</span><span class="sxs-lookup"><span data-stu-id="79976-112">In addition, Windows PowerShell *providers* enable you to access other data stores, such as the registry and the digital signature certificate stores, as easily as you access the file system.</span></span>

<span data-ttu-id="79976-113">Az első lépések útmutató bevezetést nyújt a Windows PowerShell: a nyelv, a parancsmagok, a szolgáltatók és az objektumok használatát.</span><span class="sxs-lookup"><span data-stu-id="79976-113">This Getting Started guide provides an introduction to Windows PowerShell: the language, the cmdlets, the providers, and the use of objects.</span></span>

<span data-ttu-id="79976-114">Ebben a témakörben:</span><span class="sxs-lookup"><span data-stu-id="79976-114">In this topic:</span></span>

- [<span data-ttu-id="79976-115">Windows PowerShell rendszerkövetelményei</span><span class="sxs-lookup"><span data-stu-id="79976-115">Windows PowerShell System Requirements</span></span>](../setup/Windows-PowerShell-System-Requirements.md)

- [<span data-ttu-id="79976-116">Windows PowerShell telepítése</span><span class="sxs-lookup"><span data-stu-id="79976-116">Installing Windows PowerShell</span></span>](../setup/Installing-Windows-PowerShell.md)

- [<span data-ttu-id="79976-117">Windows PowerShell indítása</span><span class="sxs-lookup"><span data-stu-id="79976-117">Starting Windows PowerShell</span></span>](../setup/Starting-Windows-PowerShell.md)
