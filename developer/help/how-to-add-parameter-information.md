---
title: Paraméter-információk hozzáadása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cf6c1442-60aa-477a-8f30-ab02b1b11039
caps.latest.revision: 7
ms.openlocfilehash: d4a5fc934a41b00f89862674e44e4540680674f7
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083365"
---
# <a name="how-to-add-parameter-information"></a><span data-ttu-id="850da-102">Paraméteradatok hozzáadása</span><span class="sxs-lookup"><span data-stu-id="850da-102">How to Add Parameter Information</span></span>

<span data-ttu-id="850da-103">Ez a szakasz ismerteti, hogyan adhat hozzá a Paraméterek szakaszban, a parancsmag súgó-témakörének megjelenő tartalmat.</span><span class="sxs-lookup"><span data-stu-id="850da-103">This section describes how to add content that is displayed in the PARAMETERS section of the cmdlet Help topic.</span></span> <span data-ttu-id="850da-104">A témakör a Paraméterek szakaszban megtalálja az összes, a parancsmag paramétereit, és minden paraméter részletes leírását.</span><span class="sxs-lookup"><span data-stu-id="850da-104">The PARAMETERS section of the Help topic lists each of the parameters of the cmdlet and provides a detailed description of each parameter.</span></span>

<span data-ttu-id="850da-105">A paraméterek szakasz tartalmát a Súgó-témakör szakaszának SZINTAXISA a tartalom összhangban kell lennie.</span><span class="sxs-lookup"><span data-stu-id="850da-105">The content of the PARAMETERS section should be consistent with the content of the SYNTAX section of the Help topic.</span></span> <span data-ttu-id="850da-106">A feladata a Súgó Szerző, győződjön meg arról, hogy a csomópont a szintaxist és a paraméterek hasonló XML-elemeket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="850da-106">It is the responsibility of the Help author to make sure that both the Syntax and Parameters node contain similar XML elements.</span></span>

> [!NOTE]
> <span data-ttu-id="850da-107">A súgófájl, nyissa meg a dll-Help.xml fájlok a Windows PowerShell telepítési könyvtárában található teljes megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="850da-107">For a complete view of a Help file, open one of the dll-Help.xml files located in the Windows PowerShell installation directory.</span></span> <span data-ttu-id="850da-108">Például a Microsoft.PowerShell.Commands.Management.dll-Help.xml fájl tartalma számos, a Windows PowerShell-parancsmagok számára.</span><span class="sxs-lookup"><span data-stu-id="850da-108">For example, the Microsoft.PowerShell.Commands.Management.dll-Help.xml file contains content for several of the Windows PowerShell cmdlets.</span></span>

### <a name="to-add-parameters"></a><span data-ttu-id="850da-109">Paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="850da-109">To Add Parameters</span></span>

1. <span data-ttu-id="850da-110">Nyissa meg a parancsmag Súgó-fájlt, és keresse meg a parancs csomópont vannak dokumentálja a parancsmaghoz.</span><span class="sxs-lookup"><span data-stu-id="850da-110">Open the cmdlet Help file and locate the Command node for the cmdlet you are documenting.</span></span> <span data-ttu-id="850da-111">Hozzon létre egy új parancs csomópont kell új parancsmag hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="850da-111">If you are adding a new cmdlet you will need to create a new Command node.</span></span> <span data-ttu-id="850da-112">A súgófájl tartalmazza az egyes parancsmagok súgóját meg van adva, a parancs csomópont.</span><span class="sxs-lookup"><span data-stu-id="850da-112">Your Help file will contain a Command node for each cmdlet that you are providing Help content for.</span></span> <span data-ttu-id="850da-113">Íme egy példa egy üres parancs csomópont.</span><span class="sxs-lookup"><span data-stu-id="850da-113">Here is an example of a blank Command node.</span></span>

    ```xml
    <command:command>
    </command:command>
    ```

2. <span data-ttu-id="850da-114">A parancs csomóponton belül keresse meg a leírás csomópont, és paraméterek csomópont hozzáadása az alább látható módon.</span><span class="sxs-lookup"><span data-stu-id="850da-114">Within the Command node, locate the Description node and add a Parameters node as shown below.</span></span> <span data-ttu-id="850da-115">Paraméterek csak egy csomópont használata engedélyezett, és a szintaxis csomópont azonnal követnie kell.</span><span class="sxs-lookup"><span data-stu-id="850da-115">Only one Parameters node is allowed, and it should immediately follow the Syntax node.</span></span>

    ```xml
    <command:command>
      <command:details></command:details>
      <maml:description></maml:description>
      <command:syntax></command:syntax>
      <command:parameters>
      </command:Parameters>
    </command:command>
    ```

3. <span data-ttu-id="850da-116">A paraméterek csomóponton belül minden paraméter, a parancsmag paraméter csomópont hozzáadása alább látható módon.</span><span class="sxs-lookup"><span data-stu-id="850da-116">Within the Parameters node, add a Parameter node for each parameter of the cmdlet as shown below.</span></span>

   <span data-ttu-id="850da-117">Ebben a példában egy paraméter csomópontot hozzáadják a három paramétert.</span><span class="sxs-lookup"><span data-stu-id="850da-117">In this example, a Parameter node is added for three parameters.</span></span>

    ```xml
    <command:parameters>
      <command:parameter></command:parameter>
      <command:parameter></command:parameter>
      <command:parameter></command:parameter>
    </command:Parameters>
    ```

   <span data-ttu-id="850da-118">Az azonos XML-címkéket, amelyek a szintaxis csomópont használja, és mivel az itt megadott paraméterek meg kell egyeznie a szintaxis csomópont által megadott paraméterek tartoznak, mert a paraméter csomópontok átmásolhatja a szintaxis csomópont, és illessze be őket a paraméterek csomópont.</span><span class="sxs-lookup"><span data-stu-id="850da-118">Because these are the same XML tags that are used in the Syntax node, and because the parameters specified here must match the parameters specified by the Syntax node, you can copy the Parameter nodes from the Syntax node and paste them into the Parameters node.</span></span> <span data-ttu-id="850da-119">Azonban ügyeljen arra, hogy másolása paramétert csomópont csak egy példánya, még akkor is, ha a paraméter van megadva, a több paraméter állítja be a szintaxist.</span><span class="sxs-lookup"><span data-stu-id="850da-119">However, be sure to copy only one instance of a Parameter node, even if the parameter is specified in multiple parameter sets in the syntax.</span></span>

4. <span data-ttu-id="850da-120">Az egyes paraméterekhez tartozó csomópont, állítsa be az attribútumértékek, amelyek meghatározzák az egyes paraméterek jellemzőit.</span><span class="sxs-lookup"><span data-stu-id="850da-120">For each Parameter node, set the attribute values that define the characteristics of each parameter.</span></span> <span data-ttu-id="850da-121">Ezek az attribútumok a következők: helyettesítés pipelineinput és pozíciójának megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="850da-121">These attributes include the following: required, globbing, pipelineinput, and position.</span></span>

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
      </command:parameter>
      <command:parameter required="false" globbing="false"
               pipelineInput="false" position="named">
      </command:parameter>
      <command:parameter required="false" globbing="false"
               pipelineInput="false" position="named" ></command:parameter>
    </command:Parameters>
    ```

5. <span data-ttu-id="850da-122">Az egyes paraméter csomópontok hozzáadása a paraméter neve.</span><span class="sxs-lookup"><span data-stu-id="850da-122">For each Parameter node, add the name of the parameter.</span></span> <span data-ttu-id="850da-123">Íme egy példa a paraméter nevével, a paraméter csomópontot hozzáadni.</span><span class="sxs-lookup"><span data-stu-id="850da-123">Here is an example of the parameter name added to the Parameter node.</span></span>

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
      </command:parameter>
    </command:Parameters>
    ```

6. <span data-ttu-id="850da-124">Az egyes paraméter csomópontok hozzáadása a paraméter leírása.</span><span class="sxs-lookup"><span data-stu-id="850da-124">For each Parameter node, add the description of the parameter.</span></span> <span data-ttu-id="850da-125">Íme egy példa a paraméter csomópont hozzáadott paraméter leírása.</span><span class="sxs-lookup"><span data-stu-id="850da-125">Here is an example of the parameter description added to the Parameter node.</span></span>

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
        <maml:description>
          <maml:para> Add parameter description... </maml:para>
        </maml:description>
      </command:parameter>
    </command:parameters>
    ```

7. <span data-ttu-id="850da-126">Minden paraméter csomópont esetében adja hozzá a .NET-keretrendszer typ parametru.</span><span class="sxs-lookup"><span data-stu-id="850da-126">For each Parameter node, add the .NET Framework type of the parameter.</span></span> <span data-ttu-id="850da-127">A paraméter típusa a paraméter neve mellett jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="850da-127">The parameter type is displayed along with the parameter name.</span></span>

   <span data-ttu-id="850da-128">Íme egy példa a .NET-keretrendszer paramétertípus hozzáadva a paraméter csomópontra.</span><span class="sxs-lookup"><span data-stu-id="850da-128">Here is an example of the parameter .NET Framework type added to the Parameter node.</span></span>

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
        <maml:description>
          <maml:para> Add parameter description... </maml:para>
        </maml:description>
        <dev:type> Add .NET Framework type... </dev:type>
      </command:parameter>
    </command:parameters>
    ```

8. <span data-ttu-id="850da-129">Az egyes paraméter csomópontok hozzáadása a paraméter alapértelmezett értékét.</span><span class="sxs-lookup"><span data-stu-id="850da-129">For each Parameter node, add the default value of the parameter.</span></span> <span data-ttu-id="850da-130">A tartalom megjelenik a következő mondat hozzáadódik a paraméter leírása: Az alapértelmezett érték a "DefaultValue".</span><span class="sxs-lookup"><span data-stu-id="850da-130">The following sentence is added to the parameter description when the content is displayed: "DefaultValue" is the default.</span></span>

   <span data-ttu-id="850da-131">Íme egy példa a paraméter alapértelmezett értéke a paraméter csomópontra kerül.</span><span class="sxs-lookup"><span data-stu-id="850da-131">Here is an example of the parameter default value is added to the Parameter node.</span></span>

    ```xml
    <command:parameters>
      <command:parameter required="true" globbing="true"
               pipelineInput="false" position="named">
        <maml:name> Add parameter name...  </maml:name>
        <maml:description>
          <maml:para> Add parameter description... </maml:para>
        </maml:description>
        <dev:type> Add .NET Framework type... </dev:type>
        <dev:defaultvalue> Add default value...</dev:defaultvalue>
      </command:parameter>
    </command:parameters>
    ```

9. <span data-ttu-id="850da-132">Minden paraméter, amely több érték tartozik a lehetséges értékek csomópontot.</span><span class="sxs-lookup"><span data-stu-id="850da-132">For each Parameter that has multiple values, add a possible values node.</span></span>

   <span data-ttu-id="850da-133">Íme egy példa a a lehetséges értékek csomópont, amely meghatározza a két lehetséges értéket a paraméterhez</span><span class="sxs-lookup"><span data-stu-id="850da-133">Here is an example of the of a possible values node that defines two possible values for the parameter</span></span>

    ```xml
    <dev:possiblevalues>
      <dev:possiblevalue>
        <dev:value>Unknown</dev:value>
        <maml:description>
          <maml:para></maml:para>
        </maml:description>
      /dev:possiblevalue>
      <dev:possiblevalue>
        <dev:value>String</dev:value>
        <maml:description>
          <maml:para></maml:para>
        </maml:description>
      </dev:possibleValue>
    </dev:possiblevalues>
    ```

<span data-ttu-id="850da-134">Az alábbiakban néhány dolog láthat, amikor a-paramétereket adunk hozzá.</span><span class="sxs-lookup"><span data-stu-id="850da-134">Here are some things to remember when adding parameters.</span></span>

- <span data-ttu-id="850da-135">A paraméter az attribútumok nem jelennek meg az összes nézetben megtekinthetők, a parancsmag Súgó-témakör.</span><span class="sxs-lookup"><span data-stu-id="850da-135">The attributes of the parameter are not displayed in all views of the cmdlet Help topic.</span></span> <span data-ttu-id="850da-136">Azonban ezek jelennek meg a következő paraméter leírása, amikor a felhasználó kéri a teljes tábla (Get-Help \<cmdletname > – teljes) vagy paramétert (Get-Help \<cmdletname >-paraméter) nézetben, a következő témakörben.</span><span class="sxs-lookup"><span data-stu-id="850da-136">However, they are displayed in a table following the parameter description when the user asks for the Full (Get-Help \<cmdletname> -full) or Parameter (Get-Help \<cmdletname> -parameter) view of the topic.</span></span>

- <span data-ttu-id="850da-137">A paraméter leírása az egyik legfontosabb részeit egy parancsmag Súgó-témakör.</span><span class="sxs-lookup"><span data-stu-id="850da-137">The parameter description is one of the most important parts of a cmdlet Help topic.</span></span> <span data-ttu-id="850da-138">A leírás rövid, valamint alapos kell lennie.</span><span class="sxs-lookup"><span data-stu-id="850da-138">The description should be brief, as well as thorough.</span></span> <span data-ttu-id="850da-139">Azt se feledje, hogy ha a paraméter leírása túl hosszú, például ha a két paramétert léphetnek kapcsolatba egymással, adhat hozzá további tartalmak, a parancsmag Súgó-témakör a megjegyzések szakasza.</span><span class="sxs-lookup"><span data-stu-id="850da-139">Also, remember that if the parameter description becomes too long, such as when two parameters interact with each other, you can add more content in the NOTES section of the cmdlet Help topic.</span></span>

  <span data-ttu-id="850da-140">A paraméter leírása kétféle típusú információt biztosít.</span><span class="sxs-lookup"><span data-stu-id="850da-140">The parameter description provides two types of information.</span></span>

- <span data-ttu-id="850da-141">A parancsmag funkciója a paraméter használata esetén.</span><span class="sxs-lookup"><span data-stu-id="850da-141">What the cmdlet does when the parameter is used.</span></span>

- <span data-ttu-id="850da-142">Milyen jogi érték a paraméterhez.</span><span class="sxs-lookup"><span data-stu-id="850da-142">What a legal value is for the parameter.</span></span>

- <span data-ttu-id="850da-143">A paraméterértékek ki, a .NET-keretrendszer objektumként, mert felhasználók több információra van szüksége ezekre az értékekre, mint a hagyományos parancssori súgó lennének.</span><span class="sxs-lookup"><span data-stu-id="850da-143">Because the parameter values are expressed as .NET Framework objects, users need more information about these values than they would in a traditional command-line Help.</span></span> <span data-ttu-id="850da-144">A felhasználó értesítése, milyen típusú adatot a paraméter az célja, hogy fogadja el, és példákat is tartalmaznak.</span><span class="sxs-lookup"><span data-stu-id="850da-144">Tell the user what type of data the parameter is designed to accept, and include examples.</span></span>

<span data-ttu-id="850da-145">A paraméter alapértelmezett értéke az érték, amely akkor használatos, ha a paraméter nincs megadva a parancssorban.</span><span class="sxs-lookup"><span data-stu-id="850da-145">The default value of the parameter is the value that is used if the parameter is not specified on the command line.</span></span> <span data-ttu-id="850da-146">Vegye figyelembe, hogy az alapértelmezett érték megadása nem kötelező, és nincs szükség van bizonyos paraméterek, például a szükséges paramétereket.</span><span class="sxs-lookup"><span data-stu-id="850da-146">Note that the default value is optional, and is not needed for some parameters, such as required parameters.</span></span> <span data-ttu-id="850da-147">A legtöbb nem kötelező paraméter alapértelmezett értékének kell adnia.</span><span class="sxs-lookup"><span data-stu-id="850da-147">However, you should specify a default value for most optional parameters.</span></span>

<span data-ttu-id="850da-148">Az alapértelmezett érték a felhasználó nem használja a paraméterrel hatásának megértéséhez segítséget nyújt.</span><span class="sxs-lookup"><span data-stu-id="850da-148">The default value helps the user to understand the effect of not using the parameter.</span></span> <span data-ttu-id="850da-149">Írja le az alapértelmezett érték nagyon kifejezetten, például az "aktuális könyvtár" vagy "Windows PowerShell telepítési könyvtárát ($pshome)" egy opcionális elérési útja.</span><span class="sxs-lookup"><span data-stu-id="850da-149">Describe the default value very specifically, such as the "Current directory" or the "Windows PowerShell installation directory ($pshome)" for an optional path.</span></span> <span data-ttu-id="850da-150">Az alapértelmezett beállítás, például a következő mondat használt leíró mondatok is kiírhatja a `PassThru` paramétert: "Ha PassThru nincs megadva, a parancsmag nem felel meg a folyamat objektumokat."</span><span class="sxs-lookup"><span data-stu-id="850da-150">You can also write a sentence that describes the default, such as the following sentence used for the `PassThru` parameter: "If PassThru is not specified, the cmdlet does not pass objects down the pipeline."</span></span>  <span data-ttu-id="850da-151">Emellett mert ellentétes a mező neve jelenik meg az értéket "**alapértelmezett érték**", "alapértelmezett érték" kifejezés szerepeljenek a bejegyzés nem kell.</span><span class="sxs-lookup"><span data-stu-id="850da-151">Also, because the value is displayed opposite the field name "**Default value**", you do not need to include the term "default value" in the entry.</span></span>

<span data-ttu-id="850da-152">Az alapértelmezett érték a paraméter nem jelenik meg az összes nézetben megtekinthetők, a parancsmag Súgó-témakör.</span><span class="sxs-lookup"><span data-stu-id="850da-152">The default value of the parameter is not displayed in all views of the cmdlet Help topic.</span></span> <span data-ttu-id="850da-153">Azonban, amikor a teljes kéri a felhasználót a következő paraméter leírása (valamint a paraméter-attribútumok) tábla megjelenik (Get-Help \<cmdletname > – teljes) vagy paramétert (Get-Help \<cmdletname >-paraméter) megtekintése a témakör.</span><span class="sxs-lookup"><span data-stu-id="850da-153">However, it is displayed in a table (along with the parameter attributes) following the parameter description when the user asks for the Full (Get-Help \<cmdletname> -full) or Parameter (Get-Help \<cmdletname> -parameter) view of the topic.</span></span>

<span data-ttu-id="850da-154">A következő XML formátumú látható két `<dev:defaultValue>` hozzá címkéket a `<command:parameter>` csomópont.</span><span class="sxs-lookup"><span data-stu-id="850da-154">The following XML shows a pair of `<dev:defaultValue>` tags added to the `<command:parameter>` node.</span></span> <span data-ttu-id="850da-155">Figyelje meg, hogy az alapértelmezett érték a következő záró után azonnal `</command:parameterValue>` tag (Ha a paraméter értéke meg van adva) vagy a záró `</maml:description>` címke, a paraméter leírása.</span><span class="sxs-lookup"><span data-stu-id="850da-155">Notice that the default value follows immediately after the closing `</command:parameterValue>` tag (when the parameter value is specified) or the closing `</maml:description>` tag of the parameter description.</span></span> <span data-ttu-id="850da-156">név.</span><span class="sxs-lookup"><span data-stu-id="850da-156">name.</span></span>

```xml
<command:parameters>
  <command:parameter required="true" globbing="true"
           pipelineInput="false" position="named">
    <maml:name> Parameter name </maml:name>
    <maml:description>
      <maml:para> Parameter Description </maml:para>
    </maml:description>
    <command:parameterValue required="true">
      Value
    </command:parameterValue>
    <dev:defaultValue> Default parameter value </dev:defaultValue>
  </command:parameter>
</command:parameters>
```

<span data-ttu-id="850da-157">Értékek hozzáadásához, felsorolt típusok</span><span class="sxs-lookup"><span data-stu-id="850da-157">Add Values for Enumerated Types</span></span>

<span data-ttu-id="850da-158">Ha a paraméter több értéket vagy értékek sorszámozott típus, egy nem kötelező használható \<dev:possibleValues > csomópont.</span><span class="sxs-lookup"><span data-stu-id="850da-158">If the parameter has multiple values or values of an enumerated type, you can use an optional \<dev:possibleValues> node.</span></span> <span data-ttu-id="850da-159">Ez a csomópont lehetővé teszi, hogy adjon meg egy nevet és leírást a több érték.</span><span class="sxs-lookup"><span data-stu-id="850da-159">This node allows you to specify a name and description for multiple values.</span></span>

<span data-ttu-id="850da-160">Vegye figyelembe, hogy a felsorolt értékek leírását nem jelennek meg az alapértelmezett bármelyikét súgó nézetek által megjelenített a `Get-Help` parancsmag, de más Súgó megtekintők jelenhetnek meg ezt a tartalmat a nézeteket.</span><span class="sxs-lookup"><span data-stu-id="850da-160">Be aware that the descriptions of the enumerated values do not appear in any of the default Help views displayed by the `Get-Help` cmdlet, but other Help viewers may display this content in their views.</span></span>

<span data-ttu-id="850da-161">A következő XML-mutatja egy `<dev:possibleValues>` két értéket a megadott csomópont.</span><span class="sxs-lookup"><span data-stu-id="850da-161">The following XML shows a `<dev:possibleValues>` node with two values specified.</span></span>

```xml
<command:parameters>
  <command:parameter required="true" globbing="true"
           pipelineInput="false" position="named">
    <maml:name> Parameter name </maml:name>
    <maml:description>
      <maml:para> Parameter Description </maml:para>
    </maml:description>
    <command:parameterValue required="true">
      Value
    </command:parameterValue>
    <dev:defaultValue> Default parameter value </dev:defaultValue>
    <dev:possibleValues>
      <dev:possibleValue>
        <dev:value> Value 1 </dev:value>
        <maml:description>
          <maml:para> Description 1 </maml:para>
        </maml:description>
      <dev:possibleValue>
      <dev:possibleValue>
        <dev:value> Value 2 </dev:value>
        <maml:description>
          <maml:para> Description 2 </maml:para>
        </maml:description>
      <dev:possibleValue>
    </dev:possibleValues>
  </command:parameter>
</command:parameters>
```