---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: PowerShell-galériában fiók létrehozása
ms.openlocfilehash: 3ec9ad8f979fc0b88fbee72fc28ad1e3394eb01d
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
## <a name="creating-a-powershell-gallery-account"></a><span data-ttu-id="a7551-103">PowerShell-galériában fiók létrehozása</span><span class="sxs-lookup"><span data-stu-id="a7551-103">Creating a PowerShell Gallery account</span></span>

<span data-ttu-id="a7551-104">A PowerShell-galériában fiók semmit a PowerShell-galériában való közzététele előtt kell létrehozni.</span><span class="sxs-lookup"><span data-stu-id="a7551-104">A PowerShell Gallery account must be established before publishing anything to the PowerShell Gallery.</span></span>
<span data-ttu-id="a7551-105">A PowerShell-galériában fiókok össze kell kapcsolni egy Azure Active Directory levelezési fiók vagy egy Microsoft-fiók (tartománnyal rendelkező Outlook.com-os, hotmail.com, stb.)</span><span class="sxs-lookup"><span data-stu-id="a7551-105">The PowerShell Gallery accounts must be linked to an Azure Active Directory email-enabled account, or a Microsoft email account (with a domain of outlook.com, hotmail.com, etc.)</span></span>

<span data-ttu-id="a7551-106">PowerShell-galériában-fiók létrehozásához látogassa https://PowerShellGallery.com , majd kattintson a "Regisztráció" (lásd az alábbi képen).</span><span class="sxs-lookup"><span data-stu-id="a7551-106">To create a PowerShell Gallery account, go to https://PowerShellGallery.com and click on "Register" (see the image below).</span></span>

![Új fiók regisztrálása](../../Images/CreatingAccount-Register.png)

<span data-ttu-id="a7551-108">A következő oldalon egy Azure Active Directory-fiókot használ, jelölje ki "Munkahelyi vagy iskolai fiók", és jelentkezzen be a fiókjával.</span><span class="sxs-lookup"><span data-stu-id="a7551-108">In the next page, to use an Azure Active Directory account, select "Work or School Account", and log in with your account.</span></span>
<span data-ttu-id="a7551-109">Használja a Microsoft-fiók – például Hotmail.com vagy Outlook.com-os tartomány - válassza a "Személyes fiók", és jelentkezzen be.</span><span class="sxs-lookup"><span data-stu-id="a7551-109">To use a Microsoft account - such as one in a Hotmail.com or Outlook.com domain - choose "Personal Account", and log in.</span></span>

<span data-ttu-id="a7551-110">Ha már bejelentkezett, kérni fogja a PowerShell-galériában felhasználónevét létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="a7551-110">Once you have logged in, you will be prompted to create a username for the PowerShell Gallery.</span></span>
<span data-ttu-id="a7551-111">Tekintse át a használati feltételeket és adatvédelmi szabályzat a csatolt, adjon meg egy felhasználónevet, majd regisztrálja.</span><span class="sxs-lookup"><span data-stu-id="a7551-111">Review the Terms of Use and Privacy Policy that are linked in, enter a username, and then click Register.</span></span>

<span data-ttu-id="a7551-112">Megjegyzés: A fiók neve nem lehet módosítani, a már létrehozott.</span><span class="sxs-lookup"><span data-stu-id="a7551-112">Note: This account name cannot be changed once it is created.</span></span>
<span data-ttu-id="a7551-113">Lásd: [elem tulajdonosainak kezelése](https://msdn.microsoft.com/powershell/gallery/psgallery/managing-item-owners) az ezzel kapcsolatos további részletekért.</span><span class="sxs-lookup"><span data-stu-id="a7551-113">See [Managing Item Owners](https://msdn.microsoft.com/powershell/gallery/psgallery/managing-item-owners) for additional details related to this.</span></span>

## <a name="recommended-practices-for-powershell-gallery-accounts"></a><span data-ttu-id="a7551-114">Ajánlott eljárások a PowerShell-galériában fiókok</span><span class="sxs-lookup"><span data-stu-id="a7551-114">Recommended Practices for PowerShell Gallery Accounts</span></span>

<span data-ttu-id="a7551-115">Fontos, hogy a PowerShell-galériában fiókjához használt e-mail fiókot felügyelhető aktívan.</span><span class="sxs-lookup"><span data-stu-id="a7551-115">It is important that the email account used with your PowerShell Gallery account be actively monitored.</span></span>
<span data-ttu-id="a7551-116">A PowerShell gyűjteményelemek tulajdonosainak összes communiction az e-mailt a PowerShell-galériában fiókjához társított címen keresztül történik.</span><span class="sxs-lookup"><span data-stu-id="a7551-116">All communiction with owners of PowerShell Gallery items is through the email using the address associated with your PowerShell Gallery account.</span></span>
<span data-ttu-id="a7551-117">Ha azt nem lehet csatlakozni a tulajdonosa, a műveleti csapata előfordulhat, hogy kell bizonyos körülmények elem törlése.</span><span class="sxs-lookup"><span data-stu-id="a7551-117">If we are unable to contact an item owner, the Operations team may be required to delete an item under some circumstances.</span></span>

<span data-ttu-id="a7551-118">A szervezeteknek, amelyek gyakran közzétételére a PowerShell-galériában egyedi fiók létrehozása az Outlook.com-os, vagy egy másik Microsoft-fiók tartománya erre a célra.</span><span class="sxs-lookup"><span data-stu-id="a7551-118">Organizations that publish to the PowerShell Gallery often create a unique account for that purpose in Outlook.com, or another Microsoft account domain.</span></span>
<span data-ttu-id="a7551-119">Sok esetben fiók nem rendszeresen figyeli a rendszer.</span><span class="sxs-lookup"><span data-stu-id="a7551-119">In many cases that account is not regularly monitored.</span></span>
<span data-ttu-id="a7551-120">Ebben az esetben ajánlott Outlook továbbítás használatára egy másik fiókot, a szervezeten belül, a cikk tulajdonos(ok) által figyelendő általában egy e-mail küldéséhez.</span><span class="sxs-lookup"><span data-stu-id="a7551-120">A best practice in that case is to use Outlook Forwarding to send email to another account, typically one within the organization, that will be monitored by the item owner(s).</span></span>

<span data-ttu-id="a7551-121">Ha egy elemhez tartozó több tulajdonosai, az összes kommunikáció a PowerShell-galériában érkező kerül minden tulajdonosai számára.</span><span class="sxs-lookup"><span data-stu-id="a7551-121">If there are multiple owners associated with an item, all communications that come from the PowerShell Gallery will go to all owners.</span></span>
<span data-ttu-id="a7551-122">Lásd: [elem tulajdonosainak kezelése](https://msdn.microsoft.com/powershell/gallery/psgallery/managing-item-owners) további részleteket a tulajdonosok ad hozzá egy elemet.</span><span class="sxs-lookup"><span data-stu-id="a7551-122">See [Managing Item Owners](https://msdn.microsoft.com/powershell/gallery/psgallery/managing-item-owners) for additional details on adding owners to an item.</span></span>