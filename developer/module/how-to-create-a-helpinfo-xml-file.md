---
title: Egy HelpInfo XML-fájl létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3971ce1f-271c-4938-a9d3-47ff3aaf7219
caps.latest.revision: 9
ms.openlocfilehash: 7df9764fd573b75f285fec592448a550e481bea3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56844897"
---
# <a name="how-to-create-a-helpinfo-xml-file"></a><span data-ttu-id="61725-102">HelpInfo XML-fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="61725-102">How to Create a HelpInfo XML File</span></span>

<span data-ttu-id="61725-103">Ez a szakasz témakörei azt ismerteti, hogyan hozhat létre és tölthet fel egy Súgó információs fájl, egy "HelpInfo XML-fájl," a Windows PowerShell frissíthető súgójának szolgáltatás gyakran nevezik.</span><span class="sxs-lookup"><span data-stu-id="61725-103">This topics in this section explains how to create and populate a help information file, commonly known as a "HelpInfo XML file," for the Windows PowerShell Updatable Help feature.</span></span>

## <a name="helpinfo-xml-file-overview"></a><span data-ttu-id="61725-104">HelpInfo XML-fájl áttekintése</span><span class="sxs-lookup"><span data-stu-id="61725-104">HelpInfo XML File Overview</span></span>

<span data-ttu-id="61725-105">A HelpInfo XML-fájlt az kapcsolatos frissíthető súgó információit az sp_refresh_parameter_encryption elsődleges forrása.</span><span class="sxs-lookup"><span data-stu-id="61725-105">The HelpInfo XML file is the primary source of information about Updatable Help for the module.</span></span> <span data-ttu-id="61725-106">Ez magában foglalja a modulok, a felhasználói felület a támogatott kulturális környezetek és a verziószámokat, amely frissíthető súgó segítségével határozza meg, hogy a felhasználó rendelkezik-e a legújabb súgófájlokat a Súgó-fájlok helyét.</span><span class="sxs-lookup"><span data-stu-id="61725-106">It includes the location of the help files for the modules, the supported UI cultures, and the version numbers that Updatable Help uses to determine whether the user has the newest help files.</span></span>

<span data-ttu-id="61725-107">Minden egyes a modulnak csak egy HelpInfo XML-fájl, akkor is, ha a modul tartalmazza a felhasználói felület több országban több súgófájlok.</span><span class="sxs-lookup"><span data-stu-id="61725-107">Each module has just one HelpInfo XML file, even if the module includes multiple help files for multiple UI cultures.</span></span> <span data-ttu-id="61725-108">A modul szerzőjének hoz létre a HelpInfo XML-fájlt, és elhelyezi által meghatározott internetes a helyen a **HelpInfoUri** kulcsfontosságú a moduljegyzékben.</span><span class="sxs-lookup"><span data-stu-id="61725-108">The module author creates the HelpInfo XML file and places it in the Internet location that is specified by the **HelpInfoUri** key in the module manifest.</span></span> <span data-ttu-id="61725-109">A modul súgófájlok frissítve, és a feltöltött, amikor a modul szerzőjének frissíti a HelpInfo XML-fájl, és felülírja az eredeti HelpInfo XML-fájlt az új verzióval.</span><span class="sxs-lookup"><span data-stu-id="61725-109">When the module help files are updated and uploaded, the module author updates the HelpInfo XML file and replaces the original HelpInfo XML file with the new version.</span></span>

<span data-ttu-id="61725-110">Rendkívül fontos, hogy alaposan változatlan marad a HelpInfo XML-fájlt.</span><span class="sxs-lookup"><span data-stu-id="61725-110">It is critical that the HelpInfo XML file is carefully maintained.</span></span> <span data-ttu-id="61725-111">Ha új fájlokat feltölteni, de a verziószámok növekedjenek felejtse el, frissíthető súgó nem letölti az új fájlok felhasználók számítógépein.</span><span class="sxs-lookup"><span data-stu-id="61725-111">If you upload new files, but forget to increment the version numbers, Updatable Help will not download the new files to users' computers.</span></span> <span data-ttu-id="61725-112">Ha egy új felhasználói felület kulturális környezethez tartozó Súgó-fájlok hozzáadása, de nem frissítse a HelpInfo XML-fájlt vagy a megfelelő helyre, frissíthető súgó nem letölti az új fájlokat.</span><span class="sxs-lookup"><span data-stu-id="61725-112">if you add help files for a new UI culture, but don't update the HelpInfo XML file or place it in the correct location, Updatable Help will not download the new files.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="61725-113">A szakasz tartalma</span><span class="sxs-lookup"><span data-stu-id="61725-113">In this section</span></span>

<span data-ttu-id="61725-114">Ez a szakasz a következő témakörökből áll.</span><span class="sxs-lookup"><span data-stu-id="61725-114">This section includes the following topics.</span></span>

- [<span data-ttu-id="61725-115">HelpInfo XML-séma</span><span class="sxs-lookup"><span data-stu-id="61725-115">HelpInfo XML Schema</span></span>](./helpinfo-xml-schema.md)

- [<span data-ttu-id="61725-116">Mintafájl HelpInfo XML</span><span class="sxs-lookup"><span data-stu-id="61725-116">HelpInfo XML Sample File</span></span>](./helpinfo-xml-sample-file.md)

- [<span data-ttu-id="61725-117">Hogyan lehet egy HelpInfo XML-fájl neve</span><span class="sxs-lookup"><span data-stu-id="61725-117">How to Name a HelpInfo XML File</span></span>](./how-to-name-a-helpinfo-xml-file.md)

- [<span data-ttu-id="61725-118">HelpInfo XML-verziószámok beállítása</span><span class="sxs-lookup"><span data-stu-id="61725-118">How to Set HelpInfo XML Version Numbers</span></span>](./how-to-set-helpinfo-xml-version-numbers.md)

## <a name="see-also"></a><span data-ttu-id="61725-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="61725-119">See Also</span></span>

[<span data-ttu-id="61725-120">Frissíthető súgó támogatása</span><span class="sxs-lookup"><span data-stu-id="61725-120">Supporting Updatable Help</span></span>](./supporting-updatable-help.md)