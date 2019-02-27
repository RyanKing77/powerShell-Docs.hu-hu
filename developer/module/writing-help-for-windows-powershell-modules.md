---
title: Windows PowerShell-modulok súgó írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f2b58fa5-01bc-426c-a043-5c700d6578e9
caps.latest.revision: 16
ms.openlocfilehash: 443bf5f693d2ab161668de25a1097347826cb5c2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845457"
---
# <a name="writing-help-for-windows-powershell-modules"></a><span data-ttu-id="4d31a-102">Windows PowerShell-modulok írása – súgó</span><span class="sxs-lookup"><span data-stu-id="4d31a-102">Writing Help for Windows PowerShell Modules</span></span>

<span data-ttu-id="4d31a-103">Windows PowerShell-modulok Súgó-témaköröket a modult, valamint arról a modul tagjainak, például a parancsmagok, a szolgáltatók, a függvények és parancsfájlok tartalmazhatnak.</span><span class="sxs-lookup"><span data-stu-id="4d31a-103">Windows PowerShell modules can include Help topics about the module and about the module members, such as cmdlets, providers, functions and scripts.</span></span> <span data-ttu-id="4d31a-104">A `Get-Help` parancsmag megjeleníti a modul súgótémakörök ugyanebben a formátumban, más Windows PowerShell-cikkek segítséget jeleníti meg, és a felhasználók használhatják a standard `Get-Help` parancsok beolvasni a Súgó-témaköröket.</span><span class="sxs-lookup"><span data-stu-id="4d31a-104">The `Get-Help` cmdlet displays the module Help topics in the same format as it displays Help for other Windows PowerShell items, and users use standard `Get-Help` commands to get the Help topics.</span></span>

<span data-ttu-id="4d31a-105">Ez a dokumentum ismerteti a formátum és a megfelelő elhelyezési modul súgótémakörök, és azt sugallja, hogy a modul súgó tartalma irányelvek.</span><span class="sxs-lookup"><span data-stu-id="4d31a-105">This document explains the format and correct placement of module Help topics, and it suggests guidelines for module Help content.</span></span>

## <a name="types-of-module-help"></a><span data-ttu-id="4d31a-106">A modul Súgó</span><span class="sxs-lookup"><span data-stu-id="4d31a-106">Types of Module Help</span></span>

<span data-ttu-id="4d31a-107">Egy modul súgó a következő típusú tartalmazhatnak.</span><span class="sxs-lookup"><span data-stu-id="4d31a-107">A module can include the following types of Help.</span></span>

- <span data-ttu-id="4d31a-108">**A parancsmag súgójában**.</span><span class="sxs-lookup"><span data-stu-id="4d31a-108">**Cmdlet Help**.</span></span> <span data-ttu-id="4d31a-109">A Súgó-témaköröket, amelyek ismertetik a modul parancsmagjai is XML-fájlok, amelyek a parancs segítségével séma</span><span class="sxs-lookup"><span data-stu-id="4d31a-109">The Help topics that describe cmdlets in a module are XML files that use the command help schema</span></span>

- <span data-ttu-id="4d31a-110">**Szolgáltató súgó**.</span><span class="sxs-lookup"><span data-stu-id="4d31a-110">**Provider Help**.</span></span> <span data-ttu-id="4d31a-111">A Súgó-témaköröket, amelyek ismertetik egy modulban levő szolgáltatók olyan XML-fájlok, amelyek a szolgáltató segítségével séma.</span><span class="sxs-lookup"><span data-stu-id="4d31a-111">The Help topics that describe providers in a module are XML files that use the provider help schema.</span></span>

- <span data-ttu-id="4d31a-112">**Súgó függvény**.</span><span class="sxs-lookup"><span data-stu-id="4d31a-112">**Function Help**.</span></span> <span data-ttu-id="4d31a-113">A Súgó-témaköröket, amelyek ismertetik a funkciók egy modulban levő lehet XML-fájlok, amelyek a parancs segítségével a séma vagy a Megjegyzés-alapú súgó-témaköröket a függvény vagy a parancsfájl vagy a modul skriptu</span><span class="sxs-lookup"><span data-stu-id="4d31a-113">The Help topics that describe functions in a module can be XML files that use the command help schema or comment-based Help topics within the function, or the script or script module</span></span>

- <span data-ttu-id="4d31a-114">**Parancsfájl-súgó**.</span><span class="sxs-lookup"><span data-stu-id="4d31a-114">**Script Help**.</span></span> <span data-ttu-id="4d31a-115">A Súgó-témaköröket parancsfájlokat egy modulban levő leíró XML-fájlok, amelyek a parancs segítségével a séma vagy a Megjegyzés-alapú súgó-témaköröket a parancsfájl vagy a modul skriptu is lehet.</span><span class="sxs-lookup"><span data-stu-id="4d31a-115">The Help topics that describe scripts in a module can be XML files that use the command help schema or comment-based Help topics in the script or script module.</span></span>

- <span data-ttu-id="4d31a-116">**Fogalmi ("tudnivalók") Súgó**.</span><span class="sxs-lookup"><span data-stu-id="4d31a-116">**Conceptual ("About") Help**.</span></span> <span data-ttu-id="4d31a-117">Használhatja a fogalmi ("tudnivalók") Súgó-témakör írja le a modult és annak tagjait, és hogyan tagok együttes feladatait ismertetik.</span><span class="sxs-lookup"><span data-stu-id="4d31a-117">You can use a conceptual ("about") Help topic to describe the module and its members and to explain how the members can be used together to perform tasks.</span></span> <span data-ttu-id="4d31a-118">Fogalmi témakörök olyan szöveges fájlok, amelyek Unicode (UTF-8) kódolást.</span><span class="sxs-lookup"><span data-stu-id="4d31a-118">Conceptual Help topics are text files with Unicode (UTF-8) encoding.</span></span> <span data-ttu-id="4d31a-119">A fájl nevét kell használnia a `about_<name>.help.txt` formátumban, például a about_MyModule.help.txt.</span><span class="sxs-lookup"><span data-stu-id="4d31a-119">The file name must use the `about_<name>.help.txt` format, such as about_MyModule.help.txt.</span></span> <span data-ttu-id="4d31a-120">Alapértelmezés szerint a Windows PowerShell tartalmaz az alábbi információk segítségével fogalmi témakörök több mint 100, és az alábbi példához hasonlóan formázási.</span><span class="sxs-lookup"><span data-stu-id="4d31a-120">By default, Windows PowerShell includes over 100 of these conceptual About Help topics, and they are formatted like the following example.</span></span>

  ```
  TOPIC
      about_<subject or module name>

  SHORT DESCRIPTION
      A short, one-line description of the topic contents.

  LONG DESCRIPTION
      A detailed, full description of the subject or purpose of the module.

  EXAMPLES
      Examples of how to use the module or how the subject feature works in practice.

  KEYWORDS
      Terms or titles on which you might expect your users to search for the information in this topic.

  SEE ALSO
      Text-only references for further reading. Hyperlinks cannot work in the Windows PowerShell console.

  ```

## <a name="placement-of-module-help"></a><span data-ttu-id="4d31a-121">Elhelyezési modul Súgó</span><span class="sxs-lookup"><span data-stu-id="4d31a-121">Placement of Module Help</span></span>

<span data-ttu-id="4d31a-122">A `Get-Help` parancsmag nyelvspecifikus alkönyvtárát modul modul Súgó-témakör fájlokat keres.</span><span class="sxs-lookup"><span data-stu-id="4d31a-122">The `Get-Help` cmdlet looks for module Help topic files in language-specific subdirectories of the module directory.</span></span>

<span data-ttu-id="4d31a-123">Például a következő könyvtár struktúra ábrán a súgótémakörök SampleModule modul helyét.</span><span class="sxs-lookup"><span data-stu-id="4d31a-123">For example, the following directory structure diagram shows the location of the Help topics for the SampleModule module.</span></span>

```
<ModulePath>
         \SampleModule
               \<en-US>
                     \about_SampleModule.help.txt
                     \SampleModule.dll-help.xml
                     \SampleNestedModule.dll-help.xml
               \<fr-FR>
                     \about_SampleModule.help.txt
                     \SampleModule.dll-help.xml
                     \SampleNestedModule.dll-help.xml

```

> [!NOTE]
> <span data-ttu-id="4d31a-124">A példában a  *\<ModulePath >* helyőrző egyik szereplő elérési utakat a `PSModulePath` környezeti változót, például $home\Documents\Modules, $pshome\Modules vagy a felhasználó adja meg egyéni elérési utat.</span><span class="sxs-lookup"><span data-stu-id="4d31a-124">In the example, the *\<ModulePath>* placeholder represents one of the paths in the `PSModulePath` environment variable, such as $home\Documents\Modules, $pshome\Modules, or a custom path that the user specifies.</span></span>

## <a name="getting-module-help"></a><span data-ttu-id="4d31a-125">A modul Súgó</span><span class="sxs-lookup"><span data-stu-id="4d31a-125">Getting Module Help</span></span>

<span data-ttu-id="4d31a-126">Amikor egy felhasználó egy munkamenetbe importálja a modult, a Súgó-témaköröket, hogy a modul importálásának a modullal együtt a munkamenetbe.</span><span class="sxs-lookup"><span data-stu-id="4d31a-126">When a user imports a module into a session, the Help topics for that module are imported into the session along with the module.</span></span> <span data-ttu-id="4d31a-127">Listázza a moduljegyzékben a fájllista kulcs értékét a Súgó-témakör fájlokat is, de nem érinti a Súgó-témaköröket a `Export-ModuleMember` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="4d31a-127">You can list the Help topic files in the value of the FileList key in the module manifest, but Help topics are not affected by the `Export-ModuleMember` cmdlet.</span></span>

<span data-ttu-id="4d31a-128">Különböző nyelveken modul Súgó-témaköröket biztosíthat.</span><span class="sxs-lookup"><span data-stu-id="4d31a-128">You can provide module Help topics in different languages.</span></span> <span data-ttu-id="4d31a-129">A `Get-Help` parancsmag automatikusan megjeleníti a modul Súgó-témaköröket a nyelv, amely az aktuális felhasználó Vezérlőpult a területi és nyelvi beállítások elemben meg van adva.</span><span class="sxs-lookup"><span data-stu-id="4d31a-129">The `Get-Help` cmdlet automatically displays module Help topics in the language that is specified for the current user in the Regional and Language Options item in Control Panel.</span></span> <span data-ttu-id="4d31a-130">A Windows Vista és újabb verziók, Windows `Get-Help` nyelvspecifikus alkönyvtárát modul a Windows számára hoztak létre nyelvi tartalék szabványoknak megfelelően a súgótémakörök keres.</span><span class="sxs-lookup"><span data-stu-id="4d31a-130">In Windows Vista and later versions of Windows, `Get-Help` searches for the Help topics in language-specific subdirectories of the module directory in accordance with the language fallback standards established for Windows.</span></span>

<span data-ttu-id="4d31a-131">Windows PowerShell 3.0-s verziójával futó kezdve egy `Get-Help` parancs egy parancsmag vagy a függvény aktiválása automatikus importálja a modult.</span><span class="sxs-lookup"><span data-stu-id="4d31a-131">Beginning in Windows PowerShell 3.0, running a `Get-Help` command for a cmdlet or function triggers automatic importing of the module.</span></span> <span data-ttu-id="4d31a-132">A `Get-Help` parancsmag azonnal megjeleníti a Súgó-témaköröket tartalmát a modulban.</span><span class="sxs-lookup"><span data-stu-id="4d31a-132">The `Get-Help` cmdlet immediately displays the contents of the help topics in the module.</span></span>

<span data-ttu-id="4d31a-133">Ha a modul nem tartalmaz Súgó-témaköröket, és nem a felhasználó számítógépén, a modulban lévő parancsokhoz tartozó Súgó-témaköröket vannak `Get-Help` automatikusan létrehozott Súgó megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="4d31a-133">If the module does not contain help topics and there are no help topics for the commands in the module on the user's computer, `Get-Help` displays auto-generated help.</span></span> <span data-ttu-id="4d31a-134">Az automatikusan létrehozott súgó a parancs szintaxisát, paramétereit és bemeneti és kimeneti típusokat tartalmazza, de nem tartalmaz semmilyen leírása.</span><span class="sxs-lookup"><span data-stu-id="4d31a-134">The auto-generated help includes the command syntax, parameters, and input and output types, but does not include any descriptions.</span></span> <span data-ttu-id="4d31a-135">Az automatikusan létrehozott súgó tartalmaz szöveg, amely átirányítja a felhasználót, hogy próbálja meg használni a `Update-Help` parancsmaggal letöltheti a parancs az internetről vagy egy fájlmegosztás.</span><span class="sxs-lookup"><span data-stu-id="4d31a-135">The auto-generated help includes text that directs the user to try to use the `Update-Help` cmdlet to download help for the command from the Internet or a file share.</span></span> <span data-ttu-id="4d31a-136">Azt is használatát javasolja a **Online** paraméterében a `Get-Help` -parancsmaggal beolvasható a Súgó-témakör online verzióját.</span><span class="sxs-lookup"><span data-stu-id="4d31a-136">It also recommends using the **Online** parameter of the `Get-Help` cmdlet to get the online version of the help topic.</span></span>

## <a name="supporting-updatable-help"></a><span data-ttu-id="4d31a-137">Frissíthető súgó támogatása</span><span class="sxs-lookup"><span data-stu-id="4d31a-137">Supporting Updatable Help</span></span>

<span data-ttu-id="4d31a-138">A Windows PowerShell 3.0-felhasználók és a Windows PowerShell későbbi verziói is fájljainak letöltése és telepítése a frissített súgó egy modul az internetről vagy a helyi fájlmegosztásként.</span><span class="sxs-lookup"><span data-stu-id="4d31a-138">Users of Windows PowerShell 3.0 and later versions of Windows PowerShell can download and install updated help files for a module from the Internet or from a local file share.</span></span> <span data-ttu-id="4d31a-139">A `Update-Help` és `Save-Help` parancsmagok elrejtése a felhasználói felügyeleti adatait.</span><span class="sxs-lookup"><span data-stu-id="4d31a-139">The `Update-Help` and `Save-Help` cmdlets hide the management details from the user.</span></span> <span data-ttu-id="4d31a-140">Felhasználók futtassa a `Update-Help` parancsmagot, majd a `Get-Help` parancsmag használatával, olvassa el a legújabb súgófájlokat a modul a Windows PowerShell parancssorába.</span><span class="sxs-lookup"><span data-stu-id="4d31a-140">Users run the `Update-Help` cmdlet and then use the `Get-Help` cmdlet to read the newest help files for the module at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="4d31a-141">Felhasználóknak nem kell indítania Windows vagy a Windows PowerShell használatával.</span><span class="sxs-lookup"><span data-stu-id="4d31a-141">Users do not need to restart Windows or Windows PowerShell.</span></span>

<span data-ttu-id="4d31a-142">Felhasználók tűzfalak és az Internet-hozzáférés nélküli mögött a frissíthető érdekében is.</span><span class="sxs-lookup"><span data-stu-id="4d31a-142">Users behind firewalls and those without Internet access can use Updatable Help, as well.</span></span> <span data-ttu-id="4d31a-143">A rendszergazdák az Internet eléréséhez használja a `Save-Help` parancsmag használatával töltse le és telepítse a legújabb súgófájlokat azt a fájlmegosztást.</span><span class="sxs-lookup"><span data-stu-id="4d31a-143">Administrators with Internet access use the `Save-Help` cmdlet to download and install the newest help files to a file share.</span></span> <span data-ttu-id="4d31a-144">Ezt követően a felhasználók használhatják a **elérési** paraméterében a `Update-Help` -parancsmaggal beolvasható a legújabb súgófájlokat a fájlmegosztásból.</span><span class="sxs-lookup"><span data-stu-id="4d31a-144">Then, users use the **Path** parameter of the `Update-Help` cmdlet to get the newest help files from the file share.</span></span>

<span data-ttu-id="4d31a-145">A modul szerzők megadhatja súgófájlokat a modul és frissíthető súgójának használata a súgófájlokat, vagy hagyja ki a modulból súgófájlok és használja a frissíthető súgó telepítéséhez, és frissítse azokat.</span><span class="sxs-lookup"><span data-stu-id="4d31a-145">Module authors can include help files in the module and use Updatable Help to update the help files, or omit help files from the module and use Updatable Help both to install and to update them.</span></span>

<span data-ttu-id="4d31a-146">Frissíthető súgó kapcsolatos további információkért lásd: [frissíthető súgó támogatása](./supporting-updatable-help.md).</span><span class="sxs-lookup"><span data-stu-id="4d31a-146">For more information about Updatable Help, see [Supporting Updatable Help](./supporting-updatable-help.md).</span></span>

## <a name="supporting-online-help"></a><span data-ttu-id="4d31a-147">Online súgó támogatása</span><span class="sxs-lookup"><span data-stu-id="4d31a-147">Supporting Online Help</span></span>

<span data-ttu-id="4d31a-148">Felhasználók, akik nem, vagy ne telepítse a frissített Súgó fájlokat a számítógépükön gyakran támaszkodnak az online változata annak modul Súgó-témaköröket.</span><span class="sxs-lookup"><span data-stu-id="4d31a-148">Users who cannot or do not install updated help files on their computers often rely on the online version of module help topics.</span></span> <span data-ttu-id="4d31a-149">A **Online** paraméterében a `Get-Help` parancsmag egy parancsmag vagy a felhasználó speciális funkcióhoz Súgó-témakör online verzióját az alapértelmezett böngészőben nyílik meg.</span><span class="sxs-lookup"><span data-stu-id="4d31a-149">The **Online** parameter of the `Get-Help` cmdlet opens the online version of a cmdlet or advanced function help topic for the user in their default Internet browser.</span></span>

<span data-ttu-id="4d31a-150">A `Get-Help` parancsmag értékét használja a **HelpUri** tulajdonsága, a parancsmag vagy a függvényt, hogy a Súgó-témakör online verzióját.</span><span class="sxs-lookup"><span data-stu-id="4d31a-150">The `Get-Help` cmdlet uses the value of the **HelpUri** property of the cmdlet or function to find the online version of the help topic.</span></span>

<span data-ttu-id="4d31a-151">A Windows PowerShell 3.0-es verziótól kezdve segíthet a HelpUri attribútumot a parancsmag osztályról definiálásával parancsmag és funkció Súgó-témaköröket online verziója található felhasználók vagy a **HelpUri** tulajdonságát a **CmdletBinding** attribútum.</span><span class="sxs-lookup"><span data-stu-id="4d31a-151">Beginning in Windows PowerShell 3.0, you can help users find the online version of cmdlet and function help topics by defining the HelpUri attribute on the cmdlet class or the **HelpUri** property of the **CmdletBinding** attribute.</span></span> <span data-ttu-id="4d31a-152">Az attribútum értéke értékét a **HelpUri** tulajdonság a parancsmag vagy függvény.</span><span class="sxs-lookup"><span data-stu-id="4d31a-152">The value of the attribute is the value of the **HelpUri** property of the cmdlet or function.</span></span>

<span data-ttu-id="4d31a-153">További információkért lásd: [Online súgó támogatása](./supporting-online-help.md).</span><span class="sxs-lookup"><span data-stu-id="4d31a-153">For more information, see [Supporting Online Help](./supporting-online-help.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4d31a-154">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4d31a-154">See Also</span></span>

[<span data-ttu-id="4d31a-155">Windows PowerShell-modul írása</span><span class="sxs-lookup"><span data-stu-id="4d31a-155">Writing a Windows PowerShell Module</span></span>](./writing-a-windows-powershell-module.md)

[<span data-ttu-id="4d31a-156">Frissíthető súgó támogatása</span><span class="sxs-lookup"><span data-stu-id="4d31a-156">Supporting Updatable Help</span></span>](./supporting-updatable-help.md)

[<span data-ttu-id="4d31a-157">Online súgó támogatása</span><span class="sxs-lookup"><span data-stu-id="4d31a-157">Supporting Online Help</span></span>](./supporting-online-help.md)