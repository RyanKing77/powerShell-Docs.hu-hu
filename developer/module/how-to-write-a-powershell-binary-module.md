---
title: Egy bináris PowerShell-modul írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eb4e72e6-24c4-42b6-b7b9-a62585c17f26
caps.latest.revision: 15
ms.openlocfilehash: 9ddb3bc172c66314603d2be4df5192a76c92e05d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62082226"
---
# <a name="how-to-write-a-powershell-binary-module"></a><span data-ttu-id="481c1-102">Bináris PowerShell-modul írása</span><span class="sxs-lookup"><span data-stu-id="481c1-102">How to Write a PowerShell Binary Module</span></span>

<span data-ttu-id="481c1-103">Egy bináris modul bármely szerelvény (.dll), amely tartalmazza a parancsmag osztályokat is lehet.</span><span class="sxs-lookup"><span data-stu-id="481c1-103">A binary module can be any assembly (.dll) that contains cmdlet classes.</span></span> <span data-ttu-id="481c1-104">Alapértelmezés szerint a szerelvényben lévő összes parancsmag importálása a bináris modul importálása.</span><span class="sxs-lookup"><span data-stu-id="481c1-104">By default, all the cmdlets in the assembly are imported when the binary module is imported.</span></span> <span data-ttu-id="481c1-105">A parancsmagok, hozzon létre egy moduljegyzék, amelynek gyökérmodult a szerelvényben importált azonban korlátozhatja.</span><span class="sxs-lookup"><span data-stu-id="481c1-105">However, you can restrict the cmdlets that are imported by creating a module manifest whose root module is the assembly.</span></span> <span data-ttu-id="481c1-106">(Például a jegyzékfájl CmdletsToExport kulcsa segítségével csak a szükséges parancsmagok exportálása.) Egy bináris modul emellett további fájlokat könyvtárszerkezete és más, hogy egyetlen a parancsmag nem hasznos felügyeleti információt is tartalmazhat.</span><span class="sxs-lookup"><span data-stu-id="481c1-106">(For example, the CmdletsToExport key of the manifest can be used to export only those cmdlets that are needed.) In addition, a binary module can contain additional files, a directory structure, and other pieces of useful management information that a single cmdlet cannot.</span></span>

<span data-ttu-id="481c1-107">Az alábbi eljárás ismerteti, hogyan hozhat létre, és a egy bináris PowerShell-modul telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="481c1-107">The following procedure describes how to create and install a PowerShell binary module.</span></span>

#### <a name="how-to-create-and-install-a-powershell-binary-module"></a><span data-ttu-id="481c1-108">Hogyan hozhat létre, és a egy bináris PowerShell-modul telepítése</span><span class="sxs-lookup"><span data-stu-id="481c1-108">How to create and install a PowerShell binary module</span></span>

1. <span data-ttu-id="481c1-109">Hozzon létre egy bináris PowerShell megoldást (például az írt parancsmag C#), az a funkciók kell, és győződjön meg arról, hogy megfelelően fut-e.</span><span class="sxs-lookup"><span data-stu-id="481c1-109">Create a binary PowerShell solution (such as a cmdlet written in C#), with the capabilities you need, and ensure that it runs properly.</span></span>

   <span data-ttu-id="481c1-110">A kód szempontjából a bináris modulok középpontjában egyszerűen egy parancsmag sestavení.</span><span class="sxs-lookup"><span data-stu-id="481c1-110">From a code perspective, the core of a binary module is simply a cmdlet assembly.</span></span> <span data-ttu-id="481c1-111">PowerShell valójában kezeli a egy egyetlen parancsmag szerelvény betöltése és a memóriából való eltávolítása nélkül további védhetik a fejlesztő hitelesítendő modulként.</span><span class="sxs-lookup"><span data-stu-id="481c1-111">In fact, PowerShell will treat a single cmdlet assembly as a module, in terms of loading and unloading, with no additional effort on the part of the developer.</span></span> <span data-ttu-id="481c1-112">A parancsmag írt kapcsolatos további információkért lásd: [írása egy Windows PowerShell-parancsmag](../cmdlet/writing-a-windows-powershell-cmdlet.md).</span><span class="sxs-lookup"><span data-stu-id="481c1-112">For more information about writing a cmdlet, see [Writing a Windows PowerShell Cmdlet](../cmdlet/writing-a-windows-powershell-cmdlet.md).</span></span>

2. <span data-ttu-id="481c1-113">Ha szükséges, hozzon létre, hogy a megoldás többi: (további parancsmag XML-fájlok és így tovább) és a egy moduljegyzék ismertetik azokat.</span><span class="sxs-lookup"><span data-stu-id="481c1-113">If necessary, create the rest of your solution: (additional cmdlets, XML files, and so on) and describe them with a module manifest.</span></span>

   <span data-ttu-id="481c1-114">Kívül a megoldásban a parancsmag szerelvényeket leíró, egy moduljegyzék is bemutatják, hogyan exportálja és importálja a modult szeretné, milyen parancsmagok lesz közzétéve és milyen további fájlok lépnek a modul.</span><span class="sxs-lookup"><span data-stu-id="481c1-114">In addition to describing the cmdlet assemblies in your solution, a module manifest can describe how you want your module exported and imported, what cmdlets will be exposed, and what additional files will go into the module.</span></span> <span data-ttu-id="481c1-115">Ahogy korábban is hangsúlyoztuk azonban, a PowerShell egy bináris parancsmag például egy modult a következővel nincsenek további erőfeszítésekre is kezelheti.</span><span class="sxs-lookup"><span data-stu-id="481c1-115">As stated previously however, PowerShell can treat a binary cmdlet like a module with no additional effort.</span></span> <span data-ttu-id="481c1-116">Egy moduljegyzék mint ilyen, az elsősorban több fájlok ötvözéséhez egyetlen csomagban, vagy explicit módon való közzététel – egy adott szerelvény.</span><span class="sxs-lookup"><span data-stu-id="481c1-116">As such, a module manifest is useful mainly for combining multiple files into a single package, or for explicitly controlling publication for a given assembly.</span></span> <span data-ttu-id="481c1-117">További információkért lásd: [írásával, egy PowerShell modul Manifest](http://msdn.microsoft.com/en-us/abe4c24b-e64e-4a61-81d5-18c4fceba0b6).</span><span class="sxs-lookup"><span data-stu-id="481c1-117">For more information, see [How to Write a PowerShell Module Manifest](http://msdn.microsoft.com/en-us/abe4c24b-e64e-4a61-81d5-18c4fceba0b6).</span></span>

   <span data-ttu-id="481c1-118">A következő kódot egy rendkívül egyszerű C# kódblokk, amely ugyanebben a fájlban modulként használható három parancsmagokat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="481c1-118">The following code is an extremely simple C# code block that contains three cmdlets in the same file that can be used as a module.</span></span>

   ```csharp
   using System.Management.Automation;           // Windows PowerShell namespace.

   namespace ModuleCmdlets
   {
     [Cmdlet(VerbsDiagnostic.Test,"BinaryModuleCmdlet1")]
     public class TestBinaryModuleCmdlet1Command : Cmdlet
     {
       protected override void BeginProcessing()
       {
         WriteObject("BinaryModuleCmdlet1 exported by the ModuleCmdlets module.");
       }
     }

     [Cmdlet(VerbsDiagnostic.Test, "BinaryModuleCmdlet2")]
     public class TestBinaryModuleCmdlet2Command : Cmdlet
     {
         protected override void BeginProcessing()
         {
             WriteObject("BinaryModuleCmdlet2 exported by the ModuleCmdlets module.");
         }
     }

     [Cmdlet(VerbsDiagnostic.Test, "BinaryModuleCmdlet3")]
     public class TestBinaryModuleCmdlet3Command : Cmdlet
     {
         protected override void BeginProcessing()
         {
             WriteObject("BinaryModuleCmdlet3 exported by the ModuleCmdlets module.");
         }
     }

   }
   ```

3. <span data-ttu-id="481c1-119">A megoldás csomagot, és mentse a csomag valahol a PowerShell-modul elérési úton.</span><span class="sxs-lookup"><span data-stu-id="481c1-119">Package your solution, and save the package to somewhere in the PowerShell module path.</span></span>

   <span data-ttu-id="481c1-120">A `PSModulePath` globális környezeti változó ismerteti a PowerShell használatával keresse meg a modul alapértelmezett elérési utakat.</span><span class="sxs-lookup"><span data-stu-id="481c1-120">The `PSModulePath` global environment variable describes the default paths that PowerShell will use to locate your module.</span></span> <span data-ttu-id="481c1-121">Például egy gyakori útvonalat, ahová a modul a rendszer lenne `%SystemRoot%\users\<user>\Documents\WindowsPowerShell\Modules\<moduleName>`.</span><span class="sxs-lookup"><span data-stu-id="481c1-121">For example, a common path to save a module on a system would be `%SystemRoot%\users\<user>\Documents\WindowsPowerShell\Modules\<moduleName>`.</span></span> <span data-ttu-id="481c1-122">Ha nem használja az alapértelmezett elérési utak, szüksége lesz, de explicit módon a modul a hely telepítése során.</span><span class="sxs-lookup"><span data-stu-id="481c1-122">If you do not use the default paths, you will need to explicitly state the location of your module during installation.</span></span> <span data-ttu-id="481c1-123">Győződjön meg arról, mentéséhez, a modul egy olyan mappa létrehozásához, mivel előfordulhat, hogy a mappa több szerelvényeket és a megoldás a fájlok tárolására van szüksége.</span><span class="sxs-lookup"><span data-stu-id="481c1-123">Be sure to create a folder to save your module in, as you may need the folder to store multiple assemblies and files for your solution.</span></span>

   <span data-ttu-id="481c1-124">Vegye figyelembe, hogy technikailag nem kell a modul telepítése bárhol a `PSModulePath` – most már egyszerűen, amely PowerShell modul az alapértelmezett helyére.</span><span class="sxs-lookup"><span data-stu-id="481c1-124">Note that technically you do not need to install your module anywhere on the `PSModulePath` - those are simply the default locations that PowerShell will look for your module.</span></span> <span data-ttu-id="481c1-125">Azonban akkor számít célszerű megtenni, kivéve, ha a modul valahol máshol tárolására szolgáló csak jó okkal.</span><span class="sxs-lookup"><span data-stu-id="481c1-125">However, it is considered best practice to do so, unless you have a good reason for storing your module somewhere else.</span></span> <span data-ttu-id="481c1-126">További információkért lásd: [egy PowerShell-modul telepítése](./installing-a-powershell-module.md) és [módosítása a PowerShell modul telepítési elérési út](./modifying-the-psmodulepath-installation-path.md).</span><span class="sxs-lookup"><span data-stu-id="481c1-126">For more information, see [Installing a PowerShell Module](./installing-a-powershell-module.md) and [Modifying the PowerShell Module Installation Path](./modifying-the-psmodulepath-installation-path.md).</span></span>

4. <span data-ttu-id="481c1-127">Importálja a modult PowerShell hívásával [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module).</span><span class="sxs-lookup"><span data-stu-id="481c1-127">Import your module into PowerShell with a call to [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module).</span></span>

   <span data-ttu-id="481c1-128">A hívó [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) a modul betölti a memóriába aktív.</span><span class="sxs-lookup"><span data-stu-id="481c1-128">Calling to [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) will load your module into active memory.</span></span> <span data-ttu-id="481c1-129">Ha a PowerShell 3.0 használja, és később, egyszerűen történt a modul neve a kódot is importálni fogja azt. További információkért lásd: [egy PowerShell-modul importálása](./importing-a-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="481c1-129">If you are using PowerShell 3.0 and later, simply calling the name of your module in code will also import it; for more information, see [Importing a PowerShell Module](./importing-a-powershell-module.md).</span></span>

## <a name="importing-snap-in-assemblies-as-modules"></a><span data-ttu-id="481c1-130">Importálás szerelvények beépülő modulként</span><span class="sxs-lookup"><span data-stu-id="481c1-130">Importing Snap-in Assemblies as Modules</span></span>

<span data-ttu-id="481c1-131">Parancsmagok és szolgáltatók, a beépülő modul szerelvényeket tölthetők bináris modulként.</span><span class="sxs-lookup"><span data-stu-id="481c1-131">Cmdlets and providers that exist in snap-in assemblies can be loaded as binary modules.</span></span> <span data-ttu-id="481c1-132">A beépülő modul betöltődjenek, a bináris modulok, amikor szolgáltatók a beépülő modul és a parancsmagok érhetők el a felhasználóhoz, de a szerelvény beépülő modul osztályt a rendszer figyelmen kívül hagyja, és a beépülő modul nincs regisztrálva.</span><span class="sxs-lookup"><span data-stu-id="481c1-132">When the snap-in assemblies are loaded as binary modules, the cmdlets and providers in the snap-in are available to the user, but the snap-in class in the assembly is ignored, and the snap-in is not registered.</span></span> <span data-ttu-id="481c1-133">Ennek eredményeképpen a Windows PowerShell által biztosított beépülő modul parancsmagjai nem észleli a beépülő modult annak ellenére, hogy a parancsmagok és szolgáltatók érhetők el a munkamenethez.</span><span class="sxs-lookup"><span data-stu-id="481c1-133">As a result, the snap-in cmdlets provided by Windows PowerShell cannot detect the snap-in even though the cmdlets and providers are available to the session.</span></span>

<span data-ttu-id="481c1-134">Ezenkívül formázását vagy típusú fájlokat, a beépülő modul által hivatkozott bináris modul részeként nem lehet importálni.</span><span class="sxs-lookup"><span data-stu-id="481c1-134">In addition, any formatting or types files that are referenced by the snap-in cannot be imported as part of a binary module.</span></span> <span data-ttu-id="481c1-135">A fájlok importálása a formázás és típusok létre kell hoznia egy moduljegyzék.</span><span class="sxs-lookup"><span data-stu-id="481c1-135">To import the formatting and types files you must create a module manifest.</span></span> <span data-ttu-id="481c1-136">Látható, [PowerShell-modul jegyzék írása](http://msdn.microsoft.com/en-us/abe4c24b-e64e-4a61-81d5-18c4fceba0b6).</span><span class="sxs-lookup"><span data-stu-id="481c1-136">See, [How to Write a PowerShell Module Manifest](http://msdn.microsoft.com/en-us/abe4c24b-e64e-4a61-81d5-18c4fceba0b6).</span></span>

## <a name="see-also"></a><span data-ttu-id="481c1-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="481c1-137">See Also</span></span>

[<span data-ttu-id="481c1-138">Windows PowerShell-modul írása</span><span class="sxs-lookup"><span data-stu-id="481c1-138">Writing a Windows PowerShell Module</span></span>](./writing-a-windows-powershell-module.md)
