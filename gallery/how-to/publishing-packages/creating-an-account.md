---
ms.date: 09/11/2018
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: PowerShell-Galériabeli fiók létrehozása
ms.openlocfilehash: e4cf73edb03267cff6bbcc0cf3b754225e45be9f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685269"
---
# <a name="creating-a-powershell-gallery-account"></a><span data-ttu-id="b271b-103">PowerShell-Galériabeli fiók létrehozása</span><span class="sxs-lookup"><span data-stu-id="b271b-103">Creating a PowerShell Gallery account</span></span>

<span data-ttu-id="b271b-104">Semmit a PowerShell-galériából történő közzététele előtt létre kell hoznia egy PowerShell-Galériabeli fiók.</span><span class="sxs-lookup"><span data-stu-id="b271b-104">You must create a PowerShell Gallery account before publishing anything to the PowerShell Gallery.</span></span>
<span data-ttu-id="b271b-105">PowerShell-galériából fiókokhoz kell társítani egy levelezési bejelentkezési fiókot.</span><span class="sxs-lookup"><span data-stu-id="b271b-105">PowerShell Gallery accounts must be linked to an email-enabled login account.</span></span> <span data-ttu-id="b271b-106">Ez a fiók lehet egy Azure Active Directory-fiókot, vagy a Microsoft ID, például az Outlook.com-os vagy hotmail.com-os e-mail-fiók.</span><span class="sxs-lookup"><span data-stu-id="b271b-106">This account can be an Azure Active Directory account or a Microsoft ID, like an email account from outlook.com or hotmail.com.</span></span>

<span data-ttu-id="b271b-107">PowerShell-Galériabeli fiók létrehozásához lépjen a [ https://PowerShellGallery.com ](https://PowerShellGallery.com) , majd kattintson a **jelentkezzen be a** az alábbi képen látható módon.</span><span class="sxs-lookup"><span data-stu-id="b271b-107">To create a PowerShell Gallery account, go to [https://PowerShellGallery.com](https://PowerShellGallery.com) and click on **Sign in** as shown in the following image.</span></span>

![Új fiók regisztrálása](../../Images/CreateAccount-Register.png)

<span data-ttu-id="b271b-109">Az Azure Active Directory-fiók használatához válassza **munkahelyi vagy iskolai fiókkal**, és jelentkezzen be a fiókjával.</span><span class="sxs-lookup"><span data-stu-id="b271b-109">To use an Azure Active Directory account, select **Work or School Account**, and sign in with your account.</span></span> <span data-ttu-id="b271b-110">A Microsoft ID használatához válasszon **személyes fiók** , és jelentkezzen be.</span><span class="sxs-lookup"><span data-stu-id="b271b-110">To use a Microsoft ID, choose **Personal Account** and sign in.</span></span>

<span data-ttu-id="b271b-111">Ezután kéri felhasználónevét, a PowerShell-galériából létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="b271b-111">Next, you are prompted to create a username for the PowerShell Gallery.</span></span> <span data-ttu-id="b271b-112">Tekintse át a használati feltételeket és adatvédelmi szabályzatát, írjon be egy felhasználónevet, és kattintson **regisztrálása**.</span><span class="sxs-lookup"><span data-stu-id="b271b-112">Review the Terms of Use and Privacy Policy, enter a username, and then click **Register**.</span></span>

> [!NOTE]
> <span data-ttu-id="b271b-113">A fiók neve a létrehozásuk után nem módosítható.</span><span class="sxs-lookup"><span data-stu-id="b271b-113">The account name cannot be changed once it is created.</span></span> <span data-ttu-id="b271b-114">További információkért lásd: [csomag tulajdonosainak kezelése](managing-package-owners.md).</span><span class="sxs-lookup"><span data-stu-id="b271b-114">For more information, see [Managing Package Owners](managing-package-owners.md).</span></span>

## <a name="recommended-practices-for-powershell-gallery-accounts"></a><span data-ttu-id="b271b-115">PowerShell-galériából fiókok ajánlott eljárásai</span><span class="sxs-lookup"><span data-stu-id="b271b-115">Recommended practices for PowerShell Gallery accounts</span></span>

<span data-ttu-id="b271b-116">Fontos aktívan figyeljük a PowerShell-galériából fiókjához használt e-mail-fiók.</span><span class="sxs-lookup"><span data-stu-id="b271b-116">It's important to actively monitor the email account used with your PowerShell Gallery account.</span></span> <span data-ttu-id="b271b-117">A PowerShell-galériából csomagok tulajdonosok folytatott minden kommunikáció az e-mail-cím keresztül történik.</span><span class="sxs-lookup"><span data-stu-id="b271b-117">All communication with owners of PowerShell Gallery packages is through this email address.</span></span> <span data-ttu-id="b271b-118">Ha a PowerShell-galéria üzemeltetési csapat tud kapcsolatba lépni a csomag tulajdonosát, hogy fiókdíjat csomag törlése.</span><span class="sxs-lookup"><span data-stu-id="b271b-118">If the PowerShell Gallery Operations team is unable to contact a package owner, we may be required to delete a package.</span></span>

<span data-ttu-id="b271b-119">Szervezetek számára, amelyek gyakran közzététele a PowerShell-galériában erre a célra hozzon létre egy egyedi külső fiókot.</span><span class="sxs-lookup"><span data-stu-id="b271b-119">Organizations that publish to the PowerShell Gallery often create a unique external account for that purpose.</span></span> <span data-ttu-id="b271b-120">Azt javasoljuk, hogy e-mail továbbítás használatával értesítések címre továbbítsa a szervezeten belül.</span><span class="sxs-lookup"><span data-stu-id="b271b-120">We recommend you use email forwarding to forward notifications to an address within your organization.</span></span>

<span data-ttu-id="b271b-121">Ha több tulajdonosok társítva a csomaghoz, minden PowerShell-galériából értesítést kapnak összes tulajdonos.</span><span class="sxs-lookup"><span data-stu-id="b271b-121">When multiple owners are associated with a package, all PowerShell Gallery notifications are sent to all owners.</span></span> <span data-ttu-id="b271b-122">További információkért lásd: [csomag tulajdonosainak kezelése](managing-package-owners.md).</span><span class="sxs-lookup"><span data-stu-id="b271b-122">For more information, see [Managing Package Owners](managing-package-owners.md).</span></span>
