---
title: A parancsmag neve és a Szinopszist hozzáadása egy parancsmag súgó-témakörének |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1d0e1eb1-a962-4406-9625-175cfa3364ad
caps.latest.revision: 10
ms.openlocfilehash: f142548be473da15e702f4fa01835609d75b9d51
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850889"
---
# <a name="how-to-add-the-cmdlet-name-and-synopsis-to-a-cmdlet-help-topic"></a><span data-ttu-id="8fa5d-102">Parancsmag nevének és összefoglalójának hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="8fa5d-102">How to Add the Cmdlet Name and Synopsis to a Cmdlet Help Topic</span></span>

<span data-ttu-id="8fa5d-103">Ez a szakasz ismerteti, hogyan adhat hozzá a parancsmag súgóját nevét és a SZINOPSZIST szakaszait megjelenő tartalmat.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-103">This section describes how to add content that is displayed in the NAME and SYNOPSIS sections of the cmdlet help.</span></span> <span data-ttu-id="8fa5d-104">Ez a tartalom a súgófájlban a parancs csomópont az egyes parancsmagok kerül.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-104">In the Help file, this content is added to the Command node for each cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="8fa5d-105">A súgófájl, nyissa meg a dll-Help.xml fájlok a Windows PowerShell telepítési könyvtárában található teljes megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-105">For a complete view of a Help file, open one of the dll-Help.xml files located in the Windows PowerShell installation directory.</span></span> <span data-ttu-id="8fa5d-106">Például a Microsoft.PowerShell.Commands.Management.dll-Help.xml fájl tartalma számos, a Windows PowerShell-parancsmagok számára.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-106">For example, the Microsoft.PowerShell.Commands.Management.dll-Help.xml file contains content for several of the Windows PowerShell cmdlets.</span></span>

### <a name="to-add-the-cmdlet-name-and-a-synopsis"></a><span data-ttu-id="8fa5d-107">A parancsmag neve és a egy Szinopszist hozzáadása</span><span class="sxs-lookup"><span data-stu-id="8fa5d-107">To Add the Cmdlet Name and a Synopsis</span></span>

- <span data-ttu-id="8fa5d-108">A parancsmag súgójában megjelenítheti a parancsmag két leírását.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-108">The cmdlet Help can display two descriptions for the cmdlet.</span></span> <span data-ttu-id="8fa5d-109">Az első leírása egy rövid leírást a szinopszist hivatkozunk.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-109">The first description is a short description that is referred to as the synopsis.</span></span> <span data-ttu-id="8fa5d-110">A második leírás megadása nem ismertetett részletesebb leírását [hozzáadása a részletes leírás egy parancsmag súgó-témakörének](./how-to-add-a-cmdlet-description.md).</span><span class="sxs-lookup"><span data-stu-id="8fa5d-110">The second description is a more detailed description that is discussed in [Adding the Detailed Description to a Cmdlet Help Topic](./how-to-add-a-cmdlet-description.md).</span></span> <span data-ttu-id="8fa5d-111">Mindkét leírások egyetlen bekezdésként kell írni.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-111">Both these descriptions should be written as a single paragraph.</span></span>

- <span data-ttu-id="8fa5d-112">Az a szinopszist nem ismételje meg a parancsmag neve.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-112">In the synopsis do not repeat the cmdlet name.</span></span> <span data-ttu-id="8fa5d-113">Amely tájékoztatja a felhasználót, hogy a Get-kiszolgáló parancsmag lekérdezi a kiszolgáló nem a rövid, de nem informatív.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-113">Informing the user that the Get-Server cmdlet gets a server is brief, but not informative.</span></span> <span data-ttu-id="8fa5d-114">Ehelyett a szinonimák használata, és adja hozzá részletes leírása.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-114">Instead, use synonyms and add details to the description.</span></span>

  <span data-ttu-id="8fa5d-115">Példa: "Lekérdezi egy helyi vagy távoli számítógépen képviselő objektum."</span><span class="sxs-lookup"><span data-stu-id="8fa5d-115">Example: "Gets an object that represents a local or remote computer."</span></span>

- <span data-ttu-id="8fa5d-116">Egyszerű műveleteket, például a "get", "create" és "módosítása" az a szinopszist használja.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-116">Use simple verbs like "get", "create", and "change" in the synopsis.</span></span> <span data-ttu-id="8fa5d-117">Kerülje a "set", mert országról, és amikor szavak például "módosítása"</span><span class="sxs-lookup"><span data-stu-id="8fa5d-117">Avoid using "set" because it is vague, and fancy words such as "modify."</span></span>

  <span data-ttu-id="8fa5d-118">Példa: "Adatainak beolvasása, az Authenticode aláírás-fájlban."</span><span class="sxs-lookup"><span data-stu-id="8fa5d-118">Example: "Gets information about the Authenticode signature in a file."</span></span>

- <span data-ttu-id="8fa5d-119">Aktív hang írhat.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-119">Write in active voice.</span></span> <span data-ttu-id="8fa5d-120">Például "használata a TimeSpan objektum..." sokkal tisztább, mint "az időtartam objektum segítségével..."</span><span class="sxs-lookup"><span data-stu-id="8fa5d-120">For example, "Use the TimeSpan object..." is much clearer than "the TimeSpan object can be used to..."</span></span>

- <span data-ttu-id="8fa5d-121">A művelet "megjelenített" elkerülése érdekében a leíró parancsmagok, amelyek az objektumokat.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-121">Avoid the verb "display" when describing cmdlets that get objects.</span></span> <span data-ttu-id="8fa5d-122">Windows PowerShell parancsmag adatokat jeleníti meg, de fontos be a felhasználók a fogalmat, amely a parancsmag visszaadja a .NET keretrendszer objektumait, amelynek adatai nem lesznek megjelenítve.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-122">Although Windows PowerShell displays cmdlet data, it is important to introduce users to the concept that the cmdlet returns .NET Framework objects whose data may not be displayed.</span></span> <span data-ttu-id="8fa5d-123">Ha meg szeretné kiemelni a megjelenítendő, a felhasználó előfordulhat, hogy nem valósíthat meg, hogy a parancsmag rendelkezik vissza, számos más hasznos tulajdonságokat és metódusokat, amelyek nem jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="8fa5d-123">If you emphasize the display, the user might not realize that the cmdlet may have returned many other useful properties and methods that are not displayed.</span></span>

## <a name="see-also"></a><span data-ttu-id="8fa5d-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8fa5d-124">See Also</span></span>

 [<span data-ttu-id="8fa5d-125">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="8fa5d-125">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)