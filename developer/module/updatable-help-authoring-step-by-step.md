---
title: 'Frissíthető súgó írása: Részletes |} A Microsoft Docs'
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 10098160-c6b4-4339-b8ff-2c4f8cc0699b
caps.latest.revision: 13
ms.openlocfilehash: fbc77cc0fafce93d239da1c459d4b761b21ef3cb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849832"
---
# <a name="updatable-help-authoring-step-by-step"></a><span data-ttu-id="a3d40-102">Frissíthető súgó írása: Részletes útmutató</span><span class="sxs-lookup"><span data-stu-id="a3d40-102">Updatable Help Authoring: Step-by-Step</span></span>

<span data-ttu-id="a3d40-103">A dokumentumok frissíthető súgó szerzői lépéseit sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="a3d40-103">This documents lists the steps in the process of authoring Updatable Help.</span></span>

## <a name="authoring-updatable-help-step-by-step"></a><span data-ttu-id="a3d40-104">Frissíthető súgó szerzői: Részletes útmutató</span><span class="sxs-lookup"><span data-stu-id="a3d40-104">Authoring Updatable Help: Step-by-Step</span></span>

<span data-ttu-id="a3d40-105">Frissíthető súgó célja a végfelhasználók számára, de jelentős előnyöket is kínál, a modul szerzőknek súgó írók, lehetővé teszi, hogy tartalmat, beleértve javítsa a hibákat, alatt több felhasználói felületi kulturális környezetek, valamint választ után mennyi ideig felhasználói megjegyzések és a kérelmek, a a modul postáztuk.</span><span class="sxs-lookup"><span data-stu-id="a3d40-105">Updatable Help is designed for end-users, but it also provides significant benefits to module authors and help writers, including the ability to add content, fix errors, deliver in multiple UI cultures, and respond to user comments and requests, long after the module has shipped.</span></span> <span data-ttu-id="a3d40-106">Ez a témakör azt ismerteti, hogyan csomag és a feltöltés súgó, hogy a felhasználók letöltheti és telepítheti azokat a fájlokat a [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) és [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="a3d40-106">This topic explains how you package and upload help files so that users can download and install them by using the [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) and [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Save-Help) cmdlets.</span></span>

<span data-ttu-id="a3d40-107">Az alábbi lépéseket nyújt áttekintést a folyamat a frissíthető súgó támogatása.</span><span class="sxs-lookup"><span data-stu-id="a3d40-107">The following steps provide an overview of the process of supporting Updatable Help.</span></span>

### <a name="step-1-find-an-internet-site-for-your-help-files"></a><span data-ttu-id="a3d40-108">1. lépés: A súgófájlok internetes hely keresése</span><span class="sxs-lookup"><span data-stu-id="a3d40-108">Step 1: Find an Internet site for your help files</span></span>

<span data-ttu-id="a3d40-109">Frissíthető súgó létrehozásának első lépése, hogy az interneten található, a modul Súgó fájlok megtalálja.</span><span class="sxs-lookup"><span data-stu-id="a3d40-109">The first step in creating updatable help is to find an Internet location for your module's help files.</span></span> <span data-ttu-id="a3d40-110">Valójában két különböző helyen is használhatja.</span><span class="sxs-lookup"><span data-stu-id="a3d40-110">Actually, you can use two different locations.</span></span> <span data-ttu-id="a3d40-111">A modul súgó információs fájl (HelpInfo XML - alább ismertetett) is megőrizheti az Internet egyetlen helyen, és a súgó tartalom CAB-fájlok internetes egy másik helyen.</span><span class="sxs-lookup"><span data-stu-id="a3d40-111">You can keep your module's help information file (HelpInfo XML - described below) at one Internet location and the help content CAB files at another Internet location.</span></span> <span data-ttu-id="a3d40-112">Súgó CAB tartozó összes tartalomfájlt modul ugyanazon a helyen kell lennie.</span><span class="sxs-lookup"><span data-stu-id="a3d40-112">All help content CAB files for a module must be in the same location.</span></span> <span data-ttu-id="a3d40-113">Súgó tartalma CAB-fájlok eltérő modulok helyezheti ugyanazon a helyen.</span><span class="sxs-lookup"><span data-stu-id="a3d40-113">You can place help content CAB files for different modules in the same location.</span></span>

### <a name="step-2-add-a-helpinfouri-key-to-your-module-manifest"></a><span data-ttu-id="a3d40-114">2. lépés: A moduljegyzék HelpInfoURI kulcs hozzáadása</span><span class="sxs-lookup"><span data-stu-id="a3d40-114">Step 2: Add a HelpInfoURI key to your module manifest</span></span>

<span data-ttu-id="a3d40-115">Adjon hozzá egy **HelpInfoURI** a moduljegyzék kulcs.</span><span class="sxs-lookup"><span data-stu-id="a3d40-115">Add a **HelpInfoURI** key to your module manifest.</span></span> <span data-ttu-id="a3d40-116">A kulcs értéke az egységes erőforrás-azonosító (URI) annak a helynek a modul HelpInfo XML-információs fájl.</span><span class="sxs-lookup"><span data-stu-id="a3d40-116">The value of the key is the Uniform Resource Identifier (URI) of the location of the HelpInfo XML information file for your module.</span></span> <span data-ttu-id="a3d40-117">A biztonság érdekében a címet kell kezdődniük "http" vagy "https".</span><span class="sxs-lookup"><span data-stu-id="a3d40-117">For security, the address must begin with "http" or "https".</span></span> <span data-ttu-id="a3d40-118">Az URI-t kell megadnia az interneten található, de a HelpInfo XML-fájl neve nem tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="a3d40-118">The URI should specify an Internet location, but must not include the HelpInfo XML file name.</span></span>

<span data-ttu-id="a3d40-119">Például:</span><span class="sxs-lookup"><span data-stu-id="a3d40-119">For example:</span></span>

```powershell

@{
RootModule = TestModule.psm1
ModuleVersion = '2.0'
HelpInfoURI = 'http://go.microsoft.com/fwlink/?LinkID=0123'
}
```

### <a name="step-3-create-a-helpinfo-xml-file"></a><span data-ttu-id="a3d40-120">3. lépés: Egy HelpInfo XML-fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="a3d40-120">Step 3: Create a HelpInfo XML file</span></span>

<span data-ttu-id="a3d40-121">A HelpInfo XML fájl tartalmaz URI-ját a súgófájlok és a legújabb súgófájlokat, az egyes támogatott felhasználói felület kultúrafüggő részletei a modul verziószámát az Internet helyét.</span><span class="sxs-lookup"><span data-stu-id="a3d40-121">The HelpInfo XML information file contains the URI of the Internet location of your help files and the version numbers of the newest help files for your module in each supported UI culture.</span></span> <span data-ttu-id="a3d40-122">Minden Windows PowerShell-modul egy HelpInfo XML-fájlt tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="a3d40-122">Every Windows PowerShell module has one HelpInfo XML file.</span></span> <span data-ttu-id="a3d40-123">Amikor frissíti a súgófájlokat, szerkesztheti, vagy cserélje le a HelpInfo XML-fájl; nem adhat meg egy másikat.</span><span class="sxs-lookup"><span data-stu-id="a3d40-123">When you update your help files, you edit or replace the HelpInfo XML file; you do not add another one.</span></span> <span data-ttu-id="a3d40-124">További információkért lásd: [HelpInfo XML-fájl létrehozása](./how-to-create-a-helpinfo-xml-file.md).</span><span class="sxs-lookup"><span data-stu-id="a3d40-124">For more information, see [How to Create a HelpInfo XML File](./how-to-create-a-helpinfo-xml-file.md).</span></span>

### <a name="step-4-sign-your-help-files"></a><span data-ttu-id="a3d40-125">4. lépés: A súgófájlok aláírása</span><span class="sxs-lookup"><span data-stu-id="a3d40-125">Step 4: Sign your help files</span></span>

<span data-ttu-id="a3d40-126">Digitális aláírások nem szükségesek, de azok egy ajánlott eljárásokat javaslatot, amikor osztanak meg fájlokat.</span><span class="sxs-lookup"><span data-stu-id="a3d40-126">Digital signatures are not required, but they are a best-practice recommendation whenever you are sharing files.</span></span>

### <a name="step-5-create-cab-files"></a><span data-ttu-id="a3d40-127">5. lépés: CAB-fájlok létrehozása</span><span class="sxs-lookup"><span data-stu-id="a3d40-127">Step 5: Create CAB files</span></span>

<span data-ttu-id="a3d40-128">Megfelelő eszköz, amely létrehozza a kabinetfájlban (.cab) fájlok, például MakeCab.exe hozhat létre egy. CAB-fájl, amely a modul súgó fájljait tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="a3d40-128">Use a tool that creates cabinet (.cab) files, such as MakeCab.exe, to create a .CAB file that contains the help files for your module.</span></span> <span data-ttu-id="a3d40-129">Hozzon létre egy külön CAB fájljának a súgófájlok minden támogatott felhasználói felület kultúrafüggő részletei.</span><span class="sxs-lookup"><span data-stu-id="a3d40-129">Create a separate CAB file for the help files in each supported UI culture.</span></span> <span data-ttu-id="a3d40-130">További információkért lásd: [előkészítése frissíthető súgó CAB-fájlok hogyan](./how-to-prepare-updatable-help-cab-files.md).</span><span class="sxs-lookup"><span data-stu-id="a3d40-130">For more information, see [How to Prepare Updatable Help CAB Files](./how-to-prepare-updatable-help-cab-files.md).</span></span>

### <a name="step-6-upload-your-files"></a><span data-ttu-id="a3d40-131">6. lépés: A fájlok feltöltése</span><span class="sxs-lookup"><span data-stu-id="a3d40-131">Step 6: Upload your files</span></span>

<span data-ttu-id="a3d40-132">Új vagy frissített Súgó-fájlok közzétételét, az Internet által megadott helyen a CAB-fájlok feltöltése a **HelpContentUri** elem a HelpInfo XML-fájlban.</span><span class="sxs-lookup"><span data-stu-id="a3d40-132">To publish new or updated help files, upload the CAB files to the Internet location that is specified by the **HelpContentUri** element in the HelpInfo XML file.</span></span> <span data-ttu-id="a3d40-133">Ezután töltse fel a HelpInfo XML-fájlt a értéke által meghatározott internetes helyre a **HelpInfoUri** kulcsfontosságú a moduljegyzékben.</span><span class="sxs-lookup"><span data-stu-id="a3d40-133">Then, upload the HelpInfo XML file to the Internet location that is specified by the value of the **HelpInfoUri** key in the module manifest.</span></span>
