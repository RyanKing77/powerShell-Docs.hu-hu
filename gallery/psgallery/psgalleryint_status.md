---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "gyűjtemény, a powershell, a parancsmag, a psgallery"
title: psgalleryint_status
ms.openlocfilehash: 0b2f1ebcb365fcd24438a028a9c8181449266a8b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
<a name="powershell-gallery-status"></a><span data-ttu-id="57ee0-103">PowerShell-galériában állapota</span><span class="sxs-lookup"><span data-stu-id="57ee0-103">PowerShell Gallery Status</span></span>
=========================

## <a name="03272017---resolved-unable-to-see-individual-module-and-script-pages"></a><span data-ttu-id="57ee0-104">03/27/2017 - FELOLDVA: nem egyedi modul és a parancsfájl lap látható</span><span class="sxs-lookup"><span data-stu-id="57ee0-104">03/27/2017 - RESOLVED: Unable to see individual module and script pages</span></span>

<span data-ttu-id="57ee0-105">__Összegző gyakorolt hatás__: közvetlen hivatkozások https://www.powershellgallery.com egyedi modul és a parancsfájl lapján hibás volt.</span><span class="sxs-lookup"><span data-stu-id="57ee0-105">__Summary of Impact__: Direct links to individual module and script pages on https://www.powershellgallery.com were broken.</span></span> <span data-ttu-id="57ee0-106">Ez a régiók közötti történt alatt.</span><span class="sxs-lookup"><span data-stu-id="57ee0-106">This was being reported across all the regions.</span></span> <span data-ttu-id="57ee0-107">Ez volt nincs hatással az PowerShellGet parancsmagokat ie., Install-modul, a telepítési parancsfájl, a frissítés-modul, frissítés-parancsfájl, Publish-modul, Publish-parancsfájl továbbra is működik.</span><span class="sxs-lookup"><span data-stu-id="57ee0-107">This did not impact any of the PowerShellGet cmdlets ie., Install-Module, Install-Script, Update-Module, Update-Script, Publish-Module, Publish-Script continued to work.</span></span>

<span data-ttu-id="57ee0-108">__Alapvető oka__: mérnökök okát azonosítottak hibát Tulajdonságkészítő közösségi gombok Facebook hasonlóan a lapra.</span><span class="sxs-lookup"><span data-stu-id="57ee0-108">__Root Cause__: Engineers identified the cause as an issue bringing up social media buttons like Facebook onto the page.</span></span>  

<span data-ttu-id="57ee0-109">__Megoldási__: mérnökök megoldotta a problémát a Facebook számlálóadatok letiltásával.</span><span class="sxs-lookup"><span data-stu-id="57ee0-109">__Resolution__: Engineers fixed the problem by disabling the Facebook count information.</span></span>

<span data-ttu-id="57ee0-110">__További lépések__: belső követési hibát javítsa ki a használati Facebook API megnyitni azt.</span><span class="sxs-lookup"><span data-stu-id="57ee0-110">__Next Steps__: We opened an internal tracking issue to fix our usage of Facebook API.</span></span>

## <a name="12152016---unable-to-send-emails-via-powershellgallery-website"></a><span data-ttu-id="57ee0-111">12/15/2016 – nem lehet elküldeni az e-mailek PowerShellGallery webhelyen keresztül</span><span class="sxs-lookup"><span data-stu-id="57ee0-111">12/15/2016 - Unable to send emails via PowerShellGallery website</span></span>

<span data-ttu-id="57ee0-112">__Összegző gyakorolt hatás__: 12/13/2016 és a 12/15/2016 közötti bármely ügyfél tulajdonosok, -tulajdonosok kezelése, forduljon a támogatási szolgálathoz vagy a jelentés visszaélés küldött üzenetek nem érkezett a PowerShell-Galériabeli rendszergazdái.</span><span class="sxs-lookup"><span data-stu-id="57ee0-112">__Summary of Impact__: Between 12/13/2016 and 12/15/2016, any messages sent via Contact Owners, Manage Owners, Contact Support, or Report Abuse were not received by the PowerShell Gallery Administrators.</span></span>  
<span data-ttu-id="57ee0-113">__Alapvető oka__: mérnökök azonosítottak okát hitelesítési problémát az SMTP-kiszolgálóhoz.</span><span class="sxs-lookup"><span data-stu-id="57ee0-113">__Root Cause__: Engineers identified the cause as an authentication issue with the SMTP server.</span></span>  
<span data-ttu-id="57ee0-114">__Megoldási__: mérnökök sikerült megoldani a hitelesítési problémát, és állítsa vissza a kapcsolatot az SMTP-kiszolgálóhoz.</span><span class="sxs-lookup"><span data-stu-id="57ee0-114">__Resolution__: Engineers were able to resolve the authentication issue and restore connection to the SMTP server.</span></span>  
<span data-ttu-id="57ee0-115">__További lépések__: Ha az ügyfél-tulajdonosok, -tulajdonosok kezelése, forduljon a támogatási szolgálathoz vagy jelentés visszaélés hivatkozások használatával az e-mailek küldését cgadmin@microsoft.com során ez idő, és azt a még nem válaszolt, próbálja meg újból.</span><span class="sxs-lookup"><span data-stu-id="57ee0-115">__Next Steps__: If you used the Contact Owners, Manage Owners, Contact Support, or Report Abuse links to send mail to cgadmin@microsoft.com during this time and we have not responded, please try again.</span></span> <span data-ttu-id="57ee0-116">Elnézést kérünk a kellemetlenségért.</span><span class="sxs-lookup"><span data-stu-id="57ee0-116">We apologize for the inconvenience.</span></span>   


## <a name="8102016---resolved-unable-to-send-emails-to-cgadminmicrosoftcom"></a><span data-ttu-id="57ee0-117">8/10/2016 - feloldva: nem sikerült elküldeni az e-maileketcgadmin@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="57ee0-117">8/10/2016 - Resolved: Unable to send emails to cgadmin@microsoft.com</span></span>
<span data-ttu-id="57ee0-118">__Összegző gyakorolt hatás__: 8/5/2016 és 8/10/2016, az ügyfelek tudtuk elküldeni az e-maileket cgadmin@microsoft.com, vagy használja a kapcsolatfelvétel a szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="57ee0-118">__Summary of Impact__: Between 8/5/2016 and 8/10/2016, customers were unable to send emails to cgadmin@microsoft.com, or use the Contact Us feature.</span></span>  
<span data-ttu-id="57ee0-119">__Alapvető oka__: mérnökök okát azonosítottak az e-mail fiók módosításait.</span><span class="sxs-lookup"><span data-stu-id="57ee0-119">__Root Cause__: Engineers identified the cause as a configuration change of the email account.</span></span>  
<span data-ttu-id="57ee0-120">__Megoldási__: mérnökök működött a konfigurációs probléma megoldása érdekében.</span><span class="sxs-lookup"><span data-stu-id="57ee0-120">__Resolution__: Engineers worked to resolve the configuration issue.</span></span>  
<span data-ttu-id="57ee0-121">__További lépések__: Ha a kapcsolatfelvétel hivatkozás használt, vagy el, hogy cgadmin@microsoft.com során ez idő, és azt a még nem válaszolt, próbálja meg újból.</span><span class="sxs-lookup"><span data-stu-id="57ee0-121">__Next Steps__: If you used the Contact Us link or sent mail to cgadmin@microsoft.com during this time and we have not responded, please try again.</span></span> <span data-ttu-id="57ee0-122">Köszönjük türelmét.</span><span class="sxs-lookup"><span data-stu-id="57ee0-122">Thank you for your patience.</span></span>


