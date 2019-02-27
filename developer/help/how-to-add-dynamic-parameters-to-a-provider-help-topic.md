---
title: Dinamikus paraméterek hozzáadása a szolgáltató súgótémakör |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e20e5ad6-a6e6-4a63-9d42-1ac54214f748
caps.latest.revision: 5
ms.openlocfilehash: cc4877242a16a9caa99564aeaae985f85e38791e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849524"
---
# <a name="how-to-add-dynamic-parameters-to-a-provider-help-topic"></a><span data-ttu-id="3ed76-102">Dinamikus paraméterek hozzáadása egy szolgáltatói súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="3ed76-102">How to Add Dynamic Parameters to a Provider Help Topic</span></span>

<span data-ttu-id="3ed76-103">Ez a szakasz azt ismerteti, hogyan töltse fel a **dinamikus paraméterek** szolgáltató súgótémakör szakaszában.</span><span class="sxs-lookup"><span data-stu-id="3ed76-103">This section explains how to populate the **DYNAMIC PARAMETERS** section of a provider help topic.</span></span>

<span data-ttu-id="3ed76-104">*Dinamikus paraméterek* egy parancsmag-paraméterek vagy a megadott feltétel-függvény, amely csak az érhető el.</span><span class="sxs-lookup"><span data-stu-id="3ed76-104">*Dynamic parameters* are parameters of a cmdlet or function that are available only under specified conditions.</span></span>

<span data-ttu-id="3ed76-105">A szolgáltató súgótémakör ismertetett dinamikus paraméterek a dinamikus paraméterek, amelyek a szolgáltató ad hozzá a parancsmag vagy a funkció használatakor a parancsmagot vagy a funkció a szolgáltató meghajtón.</span><span class="sxs-lookup"><span data-stu-id="3ed76-105">The dynamic parameters that are documented in a provider help topic are the dynamic parameters that the provider adds to the cmdlet or function when the cmdlet or function is used in the provider drive.</span></span>

<span data-ttu-id="3ed76-106">Dinamikus paraméterek egyéni parancsmag súgójában talál egy szolgáltatót kell dokumentálni.</span><span class="sxs-lookup"><span data-stu-id="3ed76-106">Dynamic parameters can also be documented in custom cmdlet help for a provider.</span></span> <span data-ttu-id="3ed76-107">Szolgáltató Súgó és az egyéni parancsmag súgóját írásakor szolgáltató, vegye fel a dinamikus paraméterek dokumentáció mindkét dokumentum.</span><span class="sxs-lookup"><span data-stu-id="3ed76-107">When writing both provider help and custom cmdlet help for a provider, include the dynamic parameter documentation in both documents.</span></span> <span data-ttu-id="3ed76-108">Egyéni parancsmag súgóját kapcsolatos további információkért lásd: [írása Windows PowerShell egyéni parancsmag segítségével a szolgáltatók](./writing-custom-cmdlet-help-for-windows-powershell-providers.md).</span><span class="sxs-lookup"><span data-stu-id="3ed76-108">For more information about custom cmdlet help, see [Writing Windows PowerShell Custom Cmdlet Help for Providers](./writing-custom-cmdlet-help-for-windows-powershell-providers.md).</span></span>

<span data-ttu-id="3ed76-109">Ha a szolgáltató nem valósítja meg a dinamikus paraméterek, a szolgáltató Súgó-témakör tartalmaz egy üres `DynamicParameters` elemet.</span><span class="sxs-lookup"><span data-stu-id="3ed76-109">If a provider does not implement any dynamic parameters, the provider help topic contains an empty `DynamicParameters` element.</span></span>

### <a name="to-add-dynamic-parameters"></a><span data-ttu-id="3ed76-110">Dinamikus paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="3ed76-110">To Add Dynamic Parameters</span></span>

1. <span data-ttu-id="3ed76-111">Az a *AssemblyName*belül a .dll-help.xml fájlt a `providerHelp` elem, adjon hozzá egy `DynamicParameters` elem.</span><span class="sxs-lookup"><span data-stu-id="3ed76-111">In the *AssemblyName*.dll-help.xml file, within the `providerHelp` element, add a `DynamicParameters` element.</span></span> <span data-ttu-id="3ed76-112">A `DynamicParameters` elem után meg kell jelennie a `Tasks` elem előtt a `RelatedLinks` elemet.</span><span class="sxs-lookup"><span data-stu-id="3ed76-112">The `DynamicParameters` element should appear after the `Tasks` element and before the `RelatedLinks` element.</span></span>

   <span data-ttu-id="3ed76-113">Például:</span><span class="sxs-lookup"><span data-stu-id="3ed76-113">For example:</span></span>

    ```xml
    <providerHelp>
        <Tasks>
        </Tasks>
        <DynamicParameters>
        </DynamicParameters>
        <RelatedLinks>
        </RelatedLinks>
    </providerHelp>
    ```

   <span data-ttu-id="3ed76-114">Ha a szolgáltató nem valósítja meg a dinamikus paraméterek a `DynamicParameters` elem lehet üres.</span><span class="sxs-lookup"><span data-stu-id="3ed76-114">If the provider does not implement any dynamic parameters, the `DynamicParameters` element can be empty.</span></span>

2. <span data-ttu-id="3ed76-115">Belül a `DynamicParameters` elem, minden egyes dinamikus paraméterre, adjon hozzá egy `DynamicParameter` elemet.</span><span class="sxs-lookup"><span data-stu-id="3ed76-115">Within the `DynamicParameters` element, for each dynamic parameter, add a `DynamicParameter` element.</span></span>

   <span data-ttu-id="3ed76-116">Például:</span><span class="sxs-lookup"><span data-stu-id="3ed76-116">For example:</span></span>

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
        </DynamicParameter>
    </DynamicParameters>
    ```

3. <span data-ttu-id="3ed76-117">Az egyes `DynamicParameter` elem, adjon hozzá egy `Name` és `CmdletSupported` elemet.</span><span class="sxs-lookup"><span data-stu-id="3ed76-117">In each `DynamicParameter` element, add a `Name` and `CmdletSupported` element.</span></span>

   |<span data-ttu-id="3ed76-118">Elem neve</span><span class="sxs-lookup"><span data-stu-id="3ed76-118">Element Name</span></span>|<span data-ttu-id="3ed76-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="3ed76-119">Description</span></span>|
   |------------------|-----------------|
   |<span data-ttu-id="3ed76-120">Név</span><span class="sxs-lookup"><span data-stu-id="3ed76-120">Name</span></span>|<span data-ttu-id="3ed76-121">A paraméter neve.</span><span class="sxs-lookup"><span data-stu-id="3ed76-121">Specifies the parameter name.</span></span>|
   |<span data-ttu-id="3ed76-122">CmdletSupported</span><span class="sxs-lookup"><span data-stu-id="3ed76-122">CmdletSupported</span></span>|<span data-ttu-id="3ed76-123">Adja meg a parancsmagok, amelyben a paraméter nem érvényes.</span><span class="sxs-lookup"><span data-stu-id="3ed76-123">Specifies the cmdlets in which the parameter is valid.</span></span> <span data-ttu-id="3ed76-124">Írja be a parancsmag nevek vesszővel tagolt listája.</span><span class="sxs-lookup"><span data-stu-id="3ed76-124">Type a comma-separated list of cmdlet names.</span></span>|

   <span data-ttu-id="3ed76-125">Ha például a következő XML-dokumentumok a `Encoding` dinamikus paraméter, amely hozzáadja a Windows PowerShell fájlrendszer-szolgáltatót a `Add-Content`, `Get-Content`, `Set-Content` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="3ed76-125">For example, the following XML documents the `Encoding` dynamic parameter that the Windows PowerShell FileSystem provider adds to the `Add-Content`, `Get-Content`, `Set-Content` cmdlets.</span></span>

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
            <Name> Encoding </Name>
            <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
    </DynamicParameters>

    ```

4. <span data-ttu-id="3ed76-126">Az egyes `DynamicParameter` elemben adjon hozzá egy `Type` elemet.</span><span class="sxs-lookup"><span data-stu-id="3ed76-126">In each `DynamicParameter` element, add a `Type` element.</span></span> <span data-ttu-id="3ed76-127">A `Type` elem tárolója a `Name` elem, amely tartalmazza a dinamikus paraméter értéke a .NET-típus.</span><span class="sxs-lookup"><span data-stu-id="3ed76-127">The `Type` element is a container for the `Name` element which contains the .NET type of the value of the dynamic parameter.</span></span>

   <span data-ttu-id="3ed76-128">Ha például a következő XML formátumú típusát jeleníti meg, amely .NET a `Encoding` dinamikus paraméter a [Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding](/dotnet/api/microsoft.powershell.commands.filesystemcmdletproviderencoding) enumerálása.</span><span class="sxs-lookup"><span data-stu-id="3ed76-128">For example, the following XML shows that the .NET type of the `Encoding` dynamic parameter is the [Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding](/dotnet/api/microsoft.powershell.commands.filesystemcmdletproviderencoding) enumeration.</span></span>

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
            <Name> Encoding </Name>
            <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
            <Type>
                <Name> Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding </Name>
            <Type>
    ...
    </DynamicParameters>
    ```

5. <span data-ttu-id="3ed76-129">Adja hozzá a `Description` elem, amely a dinamikus paraméterek rövid leírását tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="3ed76-129">Add the `Description` element, which contains a brief description of the dynamic parameter.</span></span> <span data-ttu-id="3ed76-130">A leírás szerkesztésekor kövesse az alábbi útmutatást az összes parancsmag-paraméterek a előírt [paraméter-adatok hozzáadása](./how-to-add-parameter-information.md).</span><span class="sxs-lookup"><span data-stu-id="3ed76-130">When composing the description, use the guidelines prescribed for all cmdlet parameters in [How to Add Parameter Information](./how-to-add-parameter-information.md).</span></span>

   <span data-ttu-id="3ed76-131">Például a következő XML-kódot tartalmaz a leírása a `Encoding` dinamikus paraméterét.</span><span class="sxs-lookup"><span data-stu-id="3ed76-131">For example, the following XML includes the description of the `Encoding` dynamic parameter.</span></span>

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
            <Name> Encoding </Name>
            <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
            <Type>
                <Name> Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding </Name>
            <Type>
            <Description> Specifies the encoding of the output file that contains the content. </Description>
    ...
    </DynamicParameters>
    ```

6. <span data-ttu-id="3ed76-132">Adja hozzá a `PossibleValues` elem és az alárendelt elemei.</span><span class="sxs-lookup"><span data-stu-id="3ed76-132">Add the `PossibleValues` element and its child elements.</span></span> <span data-ttu-id="3ed76-133">Ezek az elemek együtt, a dinamikus paraméterek értékeit mutatják.</span><span class="sxs-lookup"><span data-stu-id="3ed76-133">Together, these elements describe the values of the dynamic parameter.</span></span> <span data-ttu-id="3ed76-134">Ez az elem a felsorolt értékek lett tervezve.</span><span class="sxs-lookup"><span data-stu-id="3ed76-134">This element is designed for enumerated values.</span></span> <span data-ttu-id="3ed76-135">A dinamikus paraméterek nem vesz egy értéket, ha például egy kapcsoló paraméter esetében, vagy az értékek számbavétele nem lehetséges, vagy adjon hozzá egy üres `PossibleValues` elemet.</span><span class="sxs-lookup"><span data-stu-id="3ed76-135">If the dynamic parameter does not take a value, such as is the case with a switch parameter, or the values cannot be enumerated, add an empty `PossibleValues` element.</span></span>

   <span data-ttu-id="3ed76-136">A következő táblázat felsorolja és ismerteti a `PossibleValues` elem és az alárendelt elemei.</span><span class="sxs-lookup"><span data-stu-id="3ed76-136">The following table lists and describes the `PossibleValues` element and its child elements.</span></span>

   |<span data-ttu-id="3ed76-137">Elem neve</span><span class="sxs-lookup"><span data-stu-id="3ed76-137">Element Name</span></span>|<span data-ttu-id="3ed76-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="3ed76-138">Description</span></span>|
   |------------------|-----------------|
   |<span data-ttu-id="3ed76-139">PossibleValues</span><span class="sxs-lookup"><span data-stu-id="3ed76-139">PossibleValues</span></span>|<span data-ttu-id="3ed76-140">Az elem a tárolóban.</span><span class="sxs-lookup"><span data-stu-id="3ed76-140">This element is a container.</span></span> <span data-ttu-id="3ed76-141">Az alárendelt elemei az alábbiakban tekintheti át.</span><span class="sxs-lookup"><span data-stu-id="3ed76-141">Its child elements are described below.</span></span> <span data-ttu-id="3ed76-142">Vegyen fel egy `PossibleValues` elem minden szolgáltató Súgó-témakör.</span><span class="sxs-lookup"><span data-stu-id="3ed76-142">Add one `PossibleValues` element to each provider help topic.</span></span> <span data-ttu-id="3ed76-143">Lehet, hogy az elem üres.</span><span class="sxs-lookup"><span data-stu-id="3ed76-143">The element can be empty.</span></span>|
   |<span data-ttu-id="3ed76-144">PossibleValue</span><span class="sxs-lookup"><span data-stu-id="3ed76-144">PossibleValue</span></span>|<span data-ttu-id="3ed76-145">Az elem a tárolóban.</span><span class="sxs-lookup"><span data-stu-id="3ed76-145">This element is a container.</span></span> <span data-ttu-id="3ed76-146">Az alárendelt elemei az alábbiakban tekintheti át.</span><span class="sxs-lookup"><span data-stu-id="3ed76-146">Its child elements are described below.</span></span> <span data-ttu-id="3ed76-147">Vegyen fel egy `PossibleValue` elem minden egyes érték a-dynamic paraméter.</span><span class="sxs-lookup"><span data-stu-id="3ed76-147">Add one `PossibleValue` element for each value of the dynamic parameter.</span></span>|
   |<span data-ttu-id="3ed76-148">Érték</span><span class="sxs-lookup"><span data-stu-id="3ed76-148">Value</span></span>|<span data-ttu-id="3ed76-149">Az érték nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="3ed76-149">Specifies the value name.</span></span>|
   |<span data-ttu-id="3ed76-150">Leírás</span><span class="sxs-lookup"><span data-stu-id="3ed76-150">Description</span></span>|<span data-ttu-id="3ed76-151">Tento element obsahuje egy `Para` elemet.</span><span class="sxs-lookup"><span data-stu-id="3ed76-151">This element contains a `Para` element.</span></span> <span data-ttu-id="3ed76-152">A szöveget a `Para` elem a nevű értékét mutatja be a `Value` elemet.</span><span class="sxs-lookup"><span data-stu-id="3ed76-152">The text in the `Para` element describes the value that is named in the `Value` element.</span></span>|

   <span data-ttu-id="3ed76-153">Például a következő XML formátumú látható egy `PossibleValue` eleme a `Encoding` dinamikus paraméterét.</span><span class="sxs-lookup"><span data-stu-id="3ed76-153">For example, the following XML shows one `PossibleValue` element of the `Encoding` dynamic parameter.</span></span>

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
    ...
            <Description> Specifies the encoding of the output file that contains the content. </Description>
            <PossibleValues>
                <PossibleValue>
                    <Value> ASCII </Value>
                    <Description>
                        <para> Uses the encoding for the ASCII (7-bit) character set. </para>
                    </Description>
                </PossibleValue>
    ...
            </PossibleValues>
    </DynamicParameters>
    ```

## <a name="example"></a><span data-ttu-id="3ed76-154">Példa</span><span class="sxs-lookup"><span data-stu-id="3ed76-154">Example</span></span>

<span data-ttu-id="3ed76-155">A következő példa bemutatja a `DynamicParameters` eleme a `Encoding` dinamikus paraméterét.</span><span class="sxs-lookup"><span data-stu-id="3ed76-155">The following example shows the `DynamicParameters` element of the `Encoding` dynamic parameter.</span></span>

```xml
<DynamicParameters/>
    <DynamicParameter>
        <Name> Encoding </Name>
        <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
        <Type>
            <Name> Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding </Name>
        <Type>
        <Description> Specifies the encoding of the output file that contains the content. </Description>
        <PossibleValues>
            <PossibleValue>
                <Value> ASCII </Value>
                <Description>
                    <para> Uses the encoding for the ASCII (7-bit) character set. </para>
                </Description>
            </PossibleValue>
            <PossibleValue>
                <Value> Unicode </Value>
                <Description>
                    <para> Encodes in UTF-16 format using the little-endian byte order. </para>
                </Description>
            </PossibleValue>
        </PossibleValues>
</DynamicParameters>
```