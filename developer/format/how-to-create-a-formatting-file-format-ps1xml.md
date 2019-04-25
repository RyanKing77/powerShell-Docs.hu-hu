---
title: A formázási fájl létrehozása (. format.ps1xml) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eb568878-f63e-4561-98e2-16ee2ac7559d
caps.latest.revision: 8
ms.openlocfilehash: e97e9ddb1bf81ba66e5f3cedddd22e3a861ce228
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065501"
---
# <a name="how-to-create-a-formatting-file-formatps1xml"></a><span data-ttu-id="01b38-102">Formázási fájl létrehozása (.format.ps1xml)</span><span class="sxs-lookup"><span data-stu-id="01b38-102">How to Create a Formatting File (.format.ps1xml)</span></span>

<span data-ttu-id="01b38-103">Ez a témakör ismerteti, hogyan hozhat létre egy formázási fájlt (. format.ps1xml).</span><span class="sxs-lookup"><span data-stu-id="01b38-103">This topic describes how to create a formatting file (.format.ps1xml).</span></span>

> [!NOTE]
> <span data-ttu-id="01b38-104">Azáltal, hogy a Windows PowerShell által biztosított fájlok egy másolatát is létrehozhat egy formázási fájlt.</span><span class="sxs-lookup"><span data-stu-id="01b38-104">You can also create a formatting file by making a copy of one of the files provided by Windows PowerShell.</span></span> <span data-ttu-id="01b38-105">Ha egy meglévő fájl egy példányát, törölje a meglévő digitális aláírás, és az új fájl hozzáadása a saját aláírását.</span><span class="sxs-lookup"><span data-stu-id="01b38-105">If you make a copy of an existing file, delete the existing digital signature, and add your own signature to the new file.</span></span>

### <a name="to-create-a-formatps1xml-file"></a><span data-ttu-id="01b38-106">Hozhat létre egy. format.ps1xml fájlt.</span><span class="sxs-lookup"><span data-stu-id="01b38-106">To create a .format.ps1xml file.</span></span>

1. <span data-ttu-id="01b38-107">Hozzon létre egy szövegfájlt (.txt) használatával a szöveges szerkesztő, például a Jegyzettömbben.</span><span class="sxs-lookup"><span data-stu-id="01b38-107">Create a text file (.txt) using a text editor such as Notepad.</span></span>

2. <span data-ttu-id="01b38-108">Másolja a következő sorokat a formázási fájlba.</span><span class="sxs-lookup"><span data-stu-id="01b38-108">Copy the following lines into the formatting file.</span></span>

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <Configuration>
   <ViewDefinitions>
   </ViewDefinitions>
   </Configuration>
   ```

   - <span data-ttu-id="01b38-109">A \<Configuration >\</Configuration > címkék megadása a legfelső szintű `Configuration` csomópont.</span><span class="sxs-lookup"><span data-stu-id="01b38-109">The \<Configuration>\</Configuration> tags define the root `Configuration` node.</span></span> <span data-ttu-id="01b38-110">Ezen a csomóponton belüli minden további XML-címkék lesz zárva.</span><span class="sxs-lookup"><span data-stu-id="01b38-110">All additional XML tags will be enclosed within this node.</span></span>

   - <span data-ttu-id="01b38-111">A <ViewDefinitions> </ViewDefinitions> címkék megadása a `ViewDefinitions` csomópont.</span><span class="sxs-lookup"><span data-stu-id="01b38-111">The <ViewDefinitions></ViewDefinitions> tags define the `ViewDefinitions` node.</span></span> <span data-ttu-id="01b38-112">Minden nézet ezen a csomóponton belül vannak meghatározva.</span><span class="sxs-lookup"><span data-stu-id="01b38-112">All views are defined within this node.</span></span>

3. <span data-ttu-id="01b38-113">Mentse a fájlt, a Windows PowerShell telepítési mappájában, a modul mappáját, vagy a modul mappa egyik almappájára.</span><span class="sxs-lookup"><span data-stu-id="01b38-113">Save the file to the Windows PowerShell installation folder, to your module folder, or to a subfolder of the module folder.</span></span> <span data-ttu-id="01b38-114">Használja a következő név formátumban, ha a fájl mentése: `MyFile.format.ps1xml`.</span><span class="sxs-lookup"><span data-stu-id="01b38-114">Use the following name format when you save the file:  `MyFile.format.ps1xml`.</span></span> <span data-ttu-id="01b38-115">Formázási fájlokat kell használnia a `.format.ps1xml` bővítmény.</span><span class="sxs-lookup"><span data-stu-id="01b38-115">Formatting files must use the `.format.ps1xml` extension.</span></span>

   <span data-ttu-id="01b38-116">Most már készen áll a formázási fájl nézetek hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="01b38-116">You are now ready to add views to the formatting file.</span></span> <span data-ttu-id="01b38-117">Formázási-fájlban definiált nézetek száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="01b38-117">There is no limit to the number of views that can be defined in a formatting file.</span></span> <span data-ttu-id="01b38-118">Hozzáadhat egyetlen nézetben minden objektum, több nézetet ugyanahhoz az objektumhoz vagy több objektum által használt egyetlen nézetben.</span><span class="sxs-lookup"><span data-stu-id="01b38-118">You can add a single view for each object, multiple views for the same object, or a single view that is used by multiple objects.</span></span>

## <a name="see-also"></a><span data-ttu-id="01b38-119">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="01b38-119">See Also</span></span>

[<span data-ttu-id="01b38-120">Egy Windows PowerShell formázás és a fájl típusai</span><span class="sxs-lookup"><span data-stu-id="01b38-120">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
