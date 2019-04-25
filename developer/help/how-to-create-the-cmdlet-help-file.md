---
title: A parancsmag súgóját fájl létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4a88dd89-6beb-494f-9e2a-6b10baed1a8d
caps.latest.revision: 17
ms.openlocfilehash: 08e05939f8aee42f2cd502a3da7a528d8460dec1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083246"
---
# <a name="how-to-create-the-cmdlet-help-file"></a><span data-ttu-id="da4dc-102">Parancsmag súgófájljának létrehozása</span><span class="sxs-lookup"><span data-stu-id="da4dc-102">How to Create the Cmdlet Help File</span></span>

<span data-ttu-id="da4dc-103">Ez a szakasz azt ismerteti, hogyan hozhat létre, amely tartalmazza a Windows PowerShell parancsmagjaival kapcsolatos súgótémaköröket tartalmának érvényes XML-fájl.</span><span class="sxs-lookup"><span data-stu-id="da4dc-103">This section describes how to create a valid XML file that contains content for Windows PowerShell cmdlet Help topics.</span></span> <span data-ttu-id="da4dc-104">Ez a szakasz ismerteti a elnevezése a súgófájlban, a megfelelő XML-fejlécek felvétele és hogyan adhat hozzá csomópontokat, mely tartalmazni fogja a különböző szakaszokat, a parancsmag súgó tartalma.</span><span class="sxs-lookup"><span data-stu-id="da4dc-104">This section discusses how to name the Help file, how to add the appropriate XML headers, and how to add nodes that will contain the different sections of the cmdlet Help content.</span></span>

> [!NOTE]
> <span data-ttu-id="da4dc-105">A súgófájl, nyissa meg a dll-Help.xml fájlok a Windows PowerShell telepítési könyvtárában található teljes megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="da4dc-105">For a complete view of a Help file, open one of the dll-Help.xml files located in the Windows PowerShell installation directory.</span></span> <span data-ttu-id="da4dc-106">Például a Microsoft.PowerShell.Commands.Management.dll-Help.xml fájl tartalma számos, a Windows PowerShell-parancsmagok számára.</span><span class="sxs-lookup"><span data-stu-id="da4dc-106">For example, the Microsoft.PowerShell.Commands.Management.dll-Help.xml file contains content for several of the Windows PowerShell cmdlets.</span></span>

### <a name="how-to-create-a-cmdlet-help-file"></a><span data-ttu-id="da4dc-107">A parancsmag súgóját fájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="da4dc-107">How to Create a Cmdlet Help File</span></span>

1. <span data-ttu-id="da4dc-108">Hozzon létre egy szövegfájlt, és mentse a UTF8 kódolást.</span><span class="sxs-lookup"><span data-stu-id="da4dc-108">Create a text file and save it using UTF8 encoding.</span></span> <span data-ttu-id="da4dc-109">A fájlnév formátuma a következő rendelkeznie kell, hogy a Windows PowerShell észlelheti a parancsmag súgó-fájlként.</span><span class="sxs-lookup"><span data-stu-id="da4dc-109">The file name must have the following format so that Windows PowerShell can detect it as a cmdlet Help file.</span></span>

   `<PSSnapInAssemblyName>.dll-Help.xml`

2. <span data-ttu-id="da4dc-110">Adja hozzá a következő XML-fejlécek a szövegfájlba.</span><span class="sxs-lookup"><span data-stu-id="da4dc-110">Add the following XML headers to the text file.</span></span> <span data-ttu-id="da4dc-111">Vegye figyelembe, hogy a fájl érvényesíti a több ügynök Modeling Language (MAML) sémának.</span><span class="sxs-lookup"><span data-stu-id="da4dc-111">Be aware that the file will be validated against the Multi-Agent Modeling Language (MAML) schema.</span></span> <span data-ttu-id="da4dc-112">Windows PowerShell jelenleg nem biztosít olyan eszközöket, a fájl ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="da4dc-112">Currently, Windows PowerShell does not provide any tools to validate the file.</span></span>

   `<?xml version="1.0" encoding="utf-8" ?> <helpItems xmlns="http://msh" schema="maml">`

3. <span data-ttu-id="da4dc-113">A parancs csomópont hozzáadása a parancsmag Súgó-fájlt az egyes parancsmagok a szerelvényben.</span><span class="sxs-lookup"><span data-stu-id="da4dc-113">Add a Command node to the cmdlet Help file for each cmdlet in the assembly.</span></span> <span data-ttu-id="da4dc-114">A parancs csomóponton lévő összes csomópont vonatkozik, a parancsmag Súgó-témakör a különböző szakaszaiban.</span><span class="sxs-lookup"><span data-stu-id="da4dc-114">Each node within the Command node relates to the different sections of the cmdlet Help topic.</span></span>

   <span data-ttu-id="da4dc-115">A következő táblázat felsorolja az XML-elem az egyes csomópontok, a leírások az egyes csomópontok követ.</span><span class="sxs-lookup"><span data-stu-id="da4dc-115">The following table lists the XML element for each node, followed by a descriptions of each node.</span></span>

   |<span data-ttu-id="da4dc-116">Csomópont</span><span class="sxs-lookup"><span data-stu-id="da4dc-116">Node</span></span>|<span data-ttu-id="da4dc-117">Leírás</span><span class="sxs-lookup"><span data-stu-id="da4dc-117">Description</span></span>|
   |----------|-----------------|
   |`<details>`|<span data-ttu-id="da4dc-118">Hozzáadja a parancsmag súgó-témakörének nevét és a SZINOPSZIST szakaszait tartalmát.</span><span class="sxs-lookup"><span data-stu-id="da4dc-118">Adds content for the NAME and SYNOPSIS sections of the cmdlet Help topic.</span></span> <span data-ttu-id="da4dc-119">További információkért lásd: [hozzáadása a parancsmag neve és a Szinopszist](./how-to-add-the-cmdlet-name-and-synopsis-to-a-cmdlet-help-topic.md).</span><span class="sxs-lookup"><span data-stu-id="da4dc-119">For more information, see [How to Add the Cmdlet Name and Synopsis](./how-to-add-the-cmdlet-name-and-synopsis-to-a-cmdlet-help-topic.md).</span></span>|
   |`<maml:description>`|<span data-ttu-id="da4dc-120">Adds content for the DESCRIPTION section of the cmdlet Help topic.</span><span class="sxs-lookup"><span data-stu-id="da4dc-120">Adds content for the DESCRIPTION section of the cmdlet Help topic.</span></span> <span data-ttu-id="da4dc-121">További információkért lásd: [hozzáadása a részletes leírás egy parancsmag súgó-témakörének](./how-to-add-a-cmdlet-description.md).</span><span class="sxs-lookup"><span data-stu-id="da4dc-121">For more information, see [How to Add the Detailed Description to a Cmdlet Help Topic](./how-to-add-a-cmdlet-description.md).</span></span>|
   |`<command:syntax>`|<span data-ttu-id="da4dc-122">Hozzáadja a parancsmag súgó-témakörének szintaxis szakaszában tartalmát.</span><span class="sxs-lookup"><span data-stu-id="da4dc-122">Adds content for the SYNTAX section of the cmdlet Help topic.</span></span> <span data-ttu-id="da4dc-123">További információkért lásd: [hozzáadása szintaxis egy parancsmag súgó-témakörének hogyan](./how-to-add-syntax-to-a-cmdlet-help-topic.md).</span><span class="sxs-lookup"><span data-stu-id="da4dc-123">For more information, see [How to Add Syntax to a Cmdlet Help Topic](./how-to-add-syntax-to-a-cmdlet-help-topic.md).</span></span>|
   |`<command:parameters>`|<span data-ttu-id="da4dc-124">Hozzáadja a tartalmat a parancsmag Súgó-témakör a paraméterek szakaszához.</span><span class="sxs-lookup"><span data-stu-id="da4dc-124">Adds content for the PARAMETERS section of the cmdlet Help topic.</span></span> <span data-ttu-id="da4dc-125">További információkért lásd: [paraméterek hozzáadása egy parancsmag súgó-témakörének hogyan](./how-to-add-parameter-information.md).</span><span class="sxs-lookup"><span data-stu-id="da4dc-125">For more information, see [How to Add Parameters to a Cmdlet Help Topic](./how-to-add-parameter-information.md).</span></span>|
   |`<command:inputTypes>`|<span data-ttu-id="da4dc-126">Hozzáadja a parancsmag súgó-témakörének BEMENETEK szakaszában tartalmát.</span><span class="sxs-lookup"><span data-stu-id="da4dc-126">Adds content for the INPUTS section of the cmdlet Help topic.</span></span> <span data-ttu-id="da4dc-127">További információkért lásd: [bemeneti típusok hozzáadása egy parancsmag súgó-témakörének hogyan](./how-to-add-input-types-to-a-cmdlet-help-topic.md).</span><span class="sxs-lookup"><span data-stu-id="da4dc-127">For more information, see [How to Add Input Types to a Cmdlet Help Topic](./how-to-add-input-types-to-a-cmdlet-help-topic.md).</span></span>|
   |`<command:returnValues>`|<span data-ttu-id="da4dc-128">Hozzáadja a parancsmag súgó-témakörének, a kimeneti szakasz tartalmát.</span><span class="sxs-lookup"><span data-stu-id="da4dc-128">Adds content for the OUTPUTS section of the cmdlet Help topic.</span></span> <span data-ttu-id="da4dc-129">További információkért lásd: [hozzáadása vissza értékeket a parancsmag súgó-témakörének hogyan](./how-to-add-return-values-to-a-cmdlet-help-topic.md).</span><span class="sxs-lookup"><span data-stu-id="da4dc-129">For more information, see [How to Add Return Values to a Cmdlet Help Topic](./how-to-add-return-values-to-a-cmdlet-help-topic.md).</span></span>|
   |`<maml:alertset>`|<span data-ttu-id="da4dc-130">Tartalom hozzáadása a parancsmag Súgó-témakör a megjegyzések szakasza.</span><span class="sxs-lookup"><span data-stu-id="da4dc-130">Adds content to the NOTES section of the cmdlet Help topic.</span></span> <span data-ttu-id="da4dc-131">További információkért lásd: [hozzáadása egy parancsmag súgó-témakörének megjegyzések](./how-to-add-notes-to-a-cmdlet-help-topic.md).</span><span class="sxs-lookup"><span data-stu-id="da4dc-131">For more information, see [How to add Notes to a Cmdlet Help Topic](./how-to-add-notes-to-a-cmdlet-help-topic.md).</span></span>|
   |`<command:examples>`|<span data-ttu-id="da4dc-132">Hozzáadja a parancsmag súgó-témakörének példák szakaszában tartalmát.</span><span class="sxs-lookup"><span data-stu-id="da4dc-132">Adds content for the EXAMPLES section of the cmdlet Help topic.</span></span> <span data-ttu-id="da4dc-133">További információkért lásd: [példák hozzáadása egy parancsmag súgó-témakörének hogyan](./how-to-add-examples-to-a-cmdlet-help-topic.md).</span><span class="sxs-lookup"><span data-stu-id="da4dc-133">For more information, see [How to Add Examples to a Cmdlet Help Topic](./how-to-add-examples-to-a-cmdlet-help-topic.md).</span></span>|
   |`<maml:relatedLinks>`|<span data-ttu-id="da4dc-134">Hozzáadja a parancsmag súgó-témakörének kapcsolódó hivatkozások szakaszában tartalmát.</span><span class="sxs-lookup"><span data-stu-id="da4dc-134">Adds content for the RELATED LINKS section of the cmdlet Help topic.</span></span> <span data-ttu-id="da4dc-135">További információkért lásd: [kapcsolódó hivatkozások hozzáadása egy parancsmag súgó-témakörének hogyan](./how-to-add-related-links-to-a-cmdlet-help-topic.md).</span><span class="sxs-lookup"><span data-stu-id="da4dc-135">For more information, see [How to Add Related Links to a Cmdlet Help Topic](./how-to-add-related-links-to-a-cmdlet-help-topic.md).</span></span>|

## <a name="example"></a><span data-ttu-id="da4dc-136">Példa</span><span class="sxs-lookup"><span data-stu-id="da4dc-136">Example</span></span>

 <span data-ttu-id="da4dc-137">Íme egy példa, amely tartalmazza a csomópontok a különböző részeit, a parancsmag súgó-témakörének parancs csomópont.</span><span class="sxs-lookup"><span data-stu-id="da4dc-137">Here is an example of a Command node that includes the nodes for the various sections of the cmdlet Help topic.</span></span>

```xml
<command:command
  xmlns:maml="http://schemas.microsoft.com/maml/2004/10"
  xmlns:command="http://schemas.microsoft.com/maml/dev/command/2004/10"
  xmlns:dev="http://schemas.microsoft.com/maml/dev/2004/10">
  <command:details>
    <!--Add name an synopsis here-->
  </command:details>
  <maml:description>
    <!--Add detailed description here-->
  </maml:description>
  <command:syntax>
    <!--Add syntax information here-->
  </command:syntax>
  <command:parameters>
    <!--Add parameter information here-->
  </command:parameters>
  <command:inputTypes>
    <!--Add input type information here-->
  </command:inputTypes>
  <command:returnValues>
    <!--Add return value information here-->
  </command:returnValues>
  <maml:alertSet>
    <!--Add Note information here-->
  </maml:alertSet>
  <command:examples>
    <!--Add cmdlet examples here-->
  </command:examples>
  <maml:relatedLinks>
    <!--Add links to related content here-->
  </maml:relatedLinks>
</command:command>
```

## <a name="see-also"></a><span data-ttu-id="da4dc-138">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="da4dc-138">See Also</span></span>

 [<span data-ttu-id="da4dc-139">A parancsmag neve és a Szinopszist hozzáadása</span><span class="sxs-lookup"><span data-stu-id="da4dc-139">How to Add the Cmdlet Name and Synopsis</span></span>](./how-to-add-the-cmdlet-name-and-synopsis-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="da4dc-140">A részletes leírás egy parancsmag Súgó-témakör hozzáadása</span><span class="sxs-lookup"><span data-stu-id="da4dc-140">How to Add the Detailed Description to a Cmdlet Help Topic</span></span>](./how-to-add-a-cmdlet-description.md)

 [<span data-ttu-id="da4dc-141">Szintaxis egy parancsmag Súgó-témakör hozzáadása</span><span class="sxs-lookup"><span data-stu-id="da4dc-141">How to Add Syntax to a Cmdlet Help Topic</span></span>](./how-to-add-syntax-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="da4dc-142">Egy parancsmag súgó-témakörének paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="da4dc-142">How to Add Parameters to a Cmdlet Help Topic</span></span>](./how-to-add-parameter-information.md)

 [<span data-ttu-id="da4dc-143">A bemeneti típusok egy parancsmag Súgó-témakör hozzáadása</span><span class="sxs-lookup"><span data-stu-id="da4dc-143">How to Add Input Types to a Cmdlet Help Topic</span></span>](./how-to-add-input-types-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="da4dc-144">Visszaadott értékeket a parancsmag Súgó-témakör hozzáadása</span><span class="sxs-lookup"><span data-stu-id="da4dc-144">How to Add Return Values to a Cmdlet Help Topic</span></span>](./how-to-add-return-values-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="da4dc-145">Hogyan adhat hozzá egy parancsmag súgó-témakörének megjegyzések</span><span class="sxs-lookup"><span data-stu-id="da4dc-145">How to add Notes to a Cmdlet Help Topic</span></span>](./how-to-add-notes-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="da4dc-146">Példák, a parancsmag Súgó-témakör hozzáadása</span><span class="sxs-lookup"><span data-stu-id="da4dc-146">How to Add Examples to a Cmdlet Help Topic</span></span>](./how-to-add-examples-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="da4dc-147">Kapcsolódó hivatkozások hozzáadása egy parancsmag Súgó-témakör</span><span class="sxs-lookup"><span data-stu-id="da4dc-147">How to Add Related Links to a Cmdlet Help Topic</span></span>](./how-to-add-related-links-to-a-cmdlet-help-topic.md)

 [<span data-ttu-id="da4dc-148">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="da4dc-148">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)