---
title: Hogyan állíthatja be a verziószámok HelpInfo XML |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 93a00463-af58-41c8-b088-450909fa1d05
caps.latest.revision: 6
ms.openlocfilehash: 4929a5b1c9f73bb12b6df975e03fc529db3565ef
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851932"
---
# <a name="how-to-set-helpinfo-xml-version-numbers"></a><span data-ttu-id="83d23-102">HelpInfo XML-verziószámok beállítása</span><span class="sxs-lookup"><span data-stu-id="83d23-102">How to Set HelpInfo XML Version Numbers</span></span>

<span data-ttu-id="83d23-103">Ez a témakör azt ismerteti, hogyan állítsa be, és a egy frissíthető súgó információs fájlban, a "HelpInfo XML-fájl." néven a verziószámok növelése</span><span class="sxs-lookup"><span data-stu-id="83d23-103">This topic explains how to set and increase the version numbers in an Updatable Help Information file, commonly known as a "HelpInfo XML file."</span></span>

## <a name="how-to-set-helpinfo-xml-version-numbers"></a><span data-ttu-id="83d23-104">HelpInfo XML-verziószámok beállítása</span><span class="sxs-lookup"><span data-stu-id="83d23-104">How to Set HelpInfo XML Version Numbers</span></span>

<span data-ttu-id="83d23-105">Egy HelpInfo XML-fájlban a verziószámok létfontosságúak frissíthető súgó működését.</span><span class="sxs-lookup"><span data-stu-id="83d23-105">The version numbers in a HelpInfo XML file are critical to the operation of Updatable Help.</span></span> <span data-ttu-id="83d23-106">A [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) és [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsmagok új súgófájlok letöltéséhez, csak akkor, ha egy felhasználói felületi kulturális környezet a távoli HelpInfo XML-fájlban a verziószám nagyobb, mint a verziószáma az adott felhasználói felület kultúrafüggő részletei a helyi HelpInfo XML, vagy nincs helyi HelpInfo XML-fájl.</span><span class="sxs-lookup"><span data-stu-id="83d23-106">The [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) and [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) cmdlets download new help files only when the version number for a UI culture in the remote HelpInfo XML file is greater than the version number for that UI culture in the local HelpInfo XML, or there is no local HelpInfo XML file.</span></span>
<span data-ttu-id="83d23-107">Egy HelpInfo XML-fájlban a verziószámok létfontosságúak frissíthető súgó működését.</span><span class="sxs-lookup"><span data-stu-id="83d23-107">The version numbers in a HelpInfo XML file are critical to the operation of Updatable Help.</span></span> <span data-ttu-id="83d23-108">A [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) és [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) parancsmagok új súgófájlok letöltéséhez, csak akkor, ha egy felhasználói felületi kulturális környezet a távoli HelpInfo XML-fájlban a verziószám nagyobb, mint a verziószáma az adott felhasználói felület kultúrafüggő részletei a helyi HelpInfo XML, vagy nincs helyi HelpInfo XML-fájl.</span><span class="sxs-lookup"><span data-stu-id="83d23-108">The [Update-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) and [Save-Help](/powershell/module/Microsoft.PowerShell.Core/Update-Help) cmdlets download new help files only when the version number for a UI culture in the remote HelpInfo XML file is greater than the version number for that UI culture in the local HelpInfo XML, or there is no local HelpInfo XML file.</span></span>

<span data-ttu-id="83d23-109">A HelpInfo XML-fájlt használ a 4 részből verziószámot, amely van definiálva a **System.Version** a Microsoft .NET-keretrendszer osztályát.</span><span class="sxs-lookup"><span data-stu-id="83d23-109">The HelpInfo XML file uses the 4-part version number that is defined in the **System.Version** class of the Microsoft .NET Framework.</span></span> <span data-ttu-id="83d23-110">A formátum `N1.N2.N3.N4`.</span><span class="sxs-lookup"><span data-stu-id="83d23-110">The format is `N1.N2.N3.N4`.</span></span> <span data-ttu-id="83d23-111">Modul szerzők bármely verzióját, amely lehetővé teszi számozási használhatják a **System.Version** osztály.</span><span class="sxs-lookup"><span data-stu-id="83d23-111">Module authors can use any version numbering scheme that is permitted by the **System.Version** class.</span></span> <span data-ttu-id="83d23-112">Frissíthető súgó csak ehhez meg kell adni a verziószám felhasználói felületi kulturális környezet növeléséhez a CAB-fájl, a felhasználói felület kulturális környezethez tartozó új verziója, a hely által meghatározott feltöltésekor a **HelpContentURI** elem a HelpInfo XML-fájlban.</span><span class="sxs-lookup"><span data-stu-id="83d23-112">Updatable Help requires only that the version number for a UI culture increase when a new version of the CAB file for that UI culture is uploaded to the location that is specified by the **HelpContentURI** element in the HelpInfo XML file.</span></span>

<span data-ttu-id="83d23-113">Az alábbi példa a német (de-DE) felhasználói felület culture, ha a verzió 2.15.0.10 HelpInfo XML-fájl elemeinek megjeleníti.</span><span class="sxs-lookup"><span data-stu-id="83d23-113">The following example shows the elements of the HelpInfo XML file for the German (de-DE) UI culture when the version is 2.15.0.10.</span></span>

```xml

<UICulture>
  <UICultureName>de-DE</UICultureName>
  <UICultureVersion>2.15.0.10</UICultureVersion>
</UICulture>
```

<span data-ttu-id="83d23-114">A verziószám egy felhasználói felületi kulturális környezet tükrözi az adott felhasználói felület kultúrafüggő részletei a CAB-fájl verzióját.</span><span class="sxs-lookup"><span data-stu-id="83d23-114">The version number for a UI culture reflects the version of the CAB file for that UI culture.</span></span> <span data-ttu-id="83d23-115">A verziószámot a teljes CAB-fájl vonatkozik.</span><span class="sxs-lookup"><span data-stu-id="83d23-115">The version number applies to the entire CAB file.</span></span> <span data-ttu-id="83d23-116">A CAB-fájl nem beállíthat különböző verziószámokat a különböző fájlok.</span><span class="sxs-lookup"><span data-stu-id="83d23-116">You cannot set different version numbers for different files in the CAB file.</span></span> <span data-ttu-id="83d23-117">A verziószám az egyes felhasználói felület kultúrafüggő részletei egymástól függetlenül ki lesz értékelve, és nem kell kapcsolódnak a verziószámokat a többi felhasználói felületi kulturális környezetek, a modul által támogatott.</span><span class="sxs-lookup"><span data-stu-id="83d23-117">The version number for each UI culture is evaluated independently and need not be related to the version numbers for other UI cultures that the module supports.</span></span>