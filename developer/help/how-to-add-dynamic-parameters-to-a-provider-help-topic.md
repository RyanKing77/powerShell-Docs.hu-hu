---
title: Dinamikus paraméterek hozzáadása szolgáltatói súgótémakörre | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e20e5ad6-a6e6-4a63-9d42-1ac54214f748
caps.latest.revision: 5
ms.openlocfilehash: cc4877242a16a9caa99564aeaae985f85e38791e
ms.sourcegitcommit: ffcc1c55f5b3adc063353cb75f2a2183acc2234a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/06/2019
ms.locfileid: "70737602"
---
# <a name="how-to-add-dynamic-parameters-to-a-provider-help-topic"></a><span data-ttu-id="736b9-102">Dinamikus paraméterek hozzáadása egy szolgáltatói súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="736b9-102">How to Add Dynamic Parameters to a Provider Help Topic</span></span>

<span data-ttu-id="736b9-103">Ez a szakasz azt ismerteti, hogyan tölthetők fel a szolgáltatói súgótémakör **dinamikus paraméterek** szakasza.</span><span class="sxs-lookup"><span data-stu-id="736b9-103">This section explains how to populate the **DYNAMIC PARAMETERS** section of a provider help topic.</span></span>

<span data-ttu-id="736b9-104">A *dinamikus paraméterek* olyan parancsmagok vagy függvények paramétereinek, amelyek csak meghatározott feltételek esetén érhetők el.</span><span class="sxs-lookup"><span data-stu-id="736b9-104">*Dynamic parameters* are parameters of a cmdlet or function that are available only under specified conditions.</span></span>

<span data-ttu-id="736b9-105">A szolgáltatói súgótémakör által dokumentált dinamikus paraméterek a szolgáltató által a parancsmaghoz vagy függvényhez hozzáadott dinamikus paraméterek, ha a szolgáltató meghajtóján a parancsmagot vagy a függvényt használja a rendszer.</span><span class="sxs-lookup"><span data-stu-id="736b9-105">The dynamic parameters that are documented in a provider help topic are the dynamic parameters that the provider adds to the cmdlet or function when the cmdlet or function is used in the provider drive.</span></span>

<span data-ttu-id="736b9-106">A dinamikus paraméterek a szolgáltatók egyéni parancsmag súgójában is dokumentálva lehetnek.</span><span class="sxs-lookup"><span data-stu-id="736b9-106">Dynamic parameters can also be documented in custom cmdlet help for a provider.</span></span> <span data-ttu-id="736b9-107">Ha a szolgáltató súgóját és az egyéni parancsmag súgóját is megírta a szolgáltatók számára, a dinamikus paraméterek dokumentációját is adja meg mindkét dokumentumban.</span><span class="sxs-lookup"><span data-stu-id="736b9-107">When writing both provider help and custom cmdlet help for a provider, include the dynamic parameter documentation in both documents.</span></span> <span data-ttu-id="736b9-108">További információ az egyéni parancsmag súgójában: [a Windows PowerShell egyéni parancsmag súgójának írása a szolgáltatók számára](./writing-custom-cmdlet-help-for-windows-powershell-providers.md).</span><span class="sxs-lookup"><span data-stu-id="736b9-108">For more information about custom cmdlet help, see [Writing Windows PowerShell Custom Cmdlet Help for Providers](./writing-custom-cmdlet-help-for-windows-powershell-providers.md).</span></span>

<span data-ttu-id="736b9-109">Ha a szolgáltató nem valósít meg dinamikus paramétereket, a szolgáltatói súgótémakör üres `DynamicParameters` elemet tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="736b9-109">If a provider does not implement any dynamic parameters, the provider help topic contains an empty `DynamicParameters` element.</span></span>

### <a name="to-add-dynamic-parameters"></a><span data-ttu-id="736b9-110">Dinamikus paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="736b9-110">To Add Dynamic Parameters</span></span>

1. <span data-ttu-id="736b9-111">A *AssemblyName*. dll-help. xml fájlban a `providerHelp` elemen belül adjon hozzá egy `DynamicParameters` elemet.</span><span class="sxs-lookup"><span data-stu-id="736b9-111">In the *AssemblyName*.dll-help.xml file, within the `providerHelp` element, add a `DynamicParameters` element.</span></span> <span data-ttu-id="736b9-112">Az `DynamicParameters` elemnek az `Tasks` elem után és az `RelatedLinks` elem előtt kell megjelennie.</span><span class="sxs-lookup"><span data-stu-id="736b9-112">The `DynamicParameters` element should appear after the `Tasks` element and before the `RelatedLinks` element.</span></span>

   <span data-ttu-id="736b9-113">Például:</span><span class="sxs-lookup"><span data-stu-id="736b9-113">For example:</span></span>

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

   <span data-ttu-id="736b9-114">Ha a szolgáltató nem valósít meg dinamikus paramétereket, az `DynamicParameters` elem üres is lehet.</span><span class="sxs-lookup"><span data-stu-id="736b9-114">If the provider does not implement any dynamic parameters, the `DynamicParameters` element can be empty.</span></span>

2. <span data-ttu-id="736b9-115">A `DynamicParameters` elemen belül minden dinamikus paraméterhez adjon hozzá egy `DynamicParameter` elemet.</span><span class="sxs-lookup"><span data-stu-id="736b9-115">Within the `DynamicParameters` element, for each dynamic parameter, add a `DynamicParameter` element.</span></span>

   <span data-ttu-id="736b9-116">Például:</span><span class="sxs-lookup"><span data-stu-id="736b9-116">For example:</span></span>

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
        </DynamicParameter>
    </DynamicParameters>
    ```

3. <span data-ttu-id="736b9-117">Minden `DynamicParameter` elemnél adjon hozzá egy `Name` és `CmdletSupported` egy elemet.</span><span class="sxs-lookup"><span data-stu-id="736b9-117">In each `DynamicParameter` element, add a `Name` and `CmdletSupported` element.</span></span>

   |<span data-ttu-id="736b9-118">Elem neve</span><span class="sxs-lookup"><span data-stu-id="736b9-118">Element Name</span></span>|<span data-ttu-id="736b9-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="736b9-119">Description</span></span>|
   |------------------|-----------------|
   |<span data-ttu-id="736b9-120">Név</span><span class="sxs-lookup"><span data-stu-id="736b9-120">Name</span></span>|<span data-ttu-id="736b9-121">Megadja a paraméter nevét.</span><span class="sxs-lookup"><span data-stu-id="736b9-121">Specifies the parameter name.</span></span>|
   |<span data-ttu-id="736b9-122">CmdletSupported</span><span class="sxs-lookup"><span data-stu-id="736b9-122">CmdletSupported</span></span>|<span data-ttu-id="736b9-123">Meghatározza azokat a parancsmagokat, amelyekben a paraméter érvényes.</span><span class="sxs-lookup"><span data-stu-id="736b9-123">Specifies the cmdlets in which the parameter is valid.</span></span> <span data-ttu-id="736b9-124">Adja meg a parancsmagok neveinek vesszővel tagolt listáját.</span><span class="sxs-lookup"><span data-stu-id="736b9-124">Type a comma-separated list of cmdlet names.</span></span>|

   <span data-ttu-id="736b9-125">A következő XML- `Encoding` dokumentumok például a Windows PowerShell fájlrendszer-szolgáltató által a, `Add-Content` `Get-Content` `Set-Content` a parancsmagokhoz hozzáadott dinamikus paraméter.</span><span class="sxs-lookup"><span data-stu-id="736b9-125">For example, the following XML documents the `Encoding` dynamic parameter that the Windows PowerShell FileSystem provider adds to the `Add-Content`, `Get-Content`, `Set-Content` cmdlets.</span></span>

    ```xml
    <DynamicParameters/>
        <DynamicParameter>
            <Name> Encoding </Name>
            <CmdletSupported> Add-Content, Get-Content, Set-Content </CmdletSupported>
    </DynamicParameters>

    ```

4. <span data-ttu-id="736b9-126">Minden `DynamicParameter` elemnél adjon hozzá egy `Type` elemet.</span><span class="sxs-lookup"><span data-stu-id="736b9-126">In each `DynamicParameter` element, add a `Type` element.</span></span> <span data-ttu-id="736b9-127">Az `Type` elem a dinamikus paraméter értékének `Name` .net-típusát tartalmazó elem tárolója.</span><span class="sxs-lookup"><span data-stu-id="736b9-127">The `Type` element is a container for the `Name` element which contains the .NET type of the value of the dynamic parameter.</span></span>

   <span data-ttu-id="736b9-128">Például a következő XML azt mutatja, hogy a `Encoding` dinamikus paraméter .net-típusa a [Microsoft. PowerShell. commands. FileSystemCmdletProviderEncoding](/dotnet/api/microsoft.powershell.commands.filesystemcmdletproviderencoding) enumerálása.</span><span class="sxs-lookup"><span data-stu-id="736b9-128">For example, the following XML shows that the .NET type of the `Encoding` dynamic parameter is the [Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncoding](/dotnet/api/microsoft.powershell.commands.filesystemcmdletproviderencoding) enumeration.</span></span>

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

5. <span data-ttu-id="736b9-129">Adja hozzá `Description` a (z) elemet, amely a dinamikus paraméter rövid leírását tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="736b9-129">Add the `Description` element, which contains a brief description of the dynamic parameter.</span></span> <span data-ttu-id="736b9-130">A Leírás összeállítása során az összes parancsmag-paraméterhez megadott irányelvek [alapján adja](./how-to-add-parameter-information.md)meg a paraméter-információkat.</span><span class="sxs-lookup"><span data-stu-id="736b9-130">When composing the description, use the guidelines prescribed for all cmdlet parameters in [How to Add Parameter Information](./how-to-add-parameter-information.md).</span></span>

   <span data-ttu-id="736b9-131">A következő XML például tartalmazza a `Encoding` dinamikus paraméter leírását.</span><span class="sxs-lookup"><span data-stu-id="736b9-131">For example, the following XML includes the description of the `Encoding` dynamic parameter.</span></span>

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

6. <span data-ttu-id="736b9-132">Adja hozzá `PossibleValues` az elemet és annak alárendelt elemeit.</span><span class="sxs-lookup"><span data-stu-id="736b9-132">Add the `PossibleValues` element and its child elements.</span></span> <span data-ttu-id="736b9-133">Ezek az elemek együttesen írják le a dinamikus paraméter értékeit.</span><span class="sxs-lookup"><span data-stu-id="736b9-133">Together, these elements describe the values of the dynamic parameter.</span></span> <span data-ttu-id="736b9-134">Ez az elem enumerált értékekhez lett tervezve.</span><span class="sxs-lookup"><span data-stu-id="736b9-134">This element is designed for enumerated values.</span></span> <span data-ttu-id="736b9-135">Ha a dinamikus paraméter nem vesz fel értéket, például egy kapcsoló paraméterrel, vagy az értékek nem sorolhatók fel, adjon hozzá egy üres `PossibleValues` elemet.</span><span class="sxs-lookup"><span data-stu-id="736b9-135">If the dynamic parameter does not take a value, such as is the case with a switch parameter, or the values cannot be enumerated, add an empty `PossibleValues` element.</span></span>

   <span data-ttu-id="736b9-136">Az alábbi táblázat felsorolja és leírja az `PossibleValues` elemet és annak alárendelt elemeit.</span><span class="sxs-lookup"><span data-stu-id="736b9-136">The following table lists and describes the `PossibleValues` element and its child elements.</span></span>

   |<span data-ttu-id="736b9-137">Elem neve</span><span class="sxs-lookup"><span data-stu-id="736b9-137">Element Name</span></span>|<span data-ttu-id="736b9-138">Leírás</span><span class="sxs-lookup"><span data-stu-id="736b9-138">Description</span></span>|
   |------------------|-----------------|
   |<span data-ttu-id="736b9-139">PossibleValues</span><span class="sxs-lookup"><span data-stu-id="736b9-139">PossibleValues</span></span>|<span data-ttu-id="736b9-140">Ez az elem egy tároló.</span><span class="sxs-lookup"><span data-stu-id="736b9-140">This element is a container.</span></span> <span data-ttu-id="736b9-141">Az alárendelt elemek az alábbiakban olvashatók.</span><span class="sxs-lookup"><span data-stu-id="736b9-141">Its child elements are described below.</span></span> <span data-ttu-id="736b9-142">Adjon hozzá `PossibleValues` egy elemet az egyes szolgáltatói témakörökhöz.</span><span class="sxs-lookup"><span data-stu-id="736b9-142">Add one `PossibleValues` element to each provider help topic.</span></span> <span data-ttu-id="736b9-143">Az elem üres is lehet.</span><span class="sxs-lookup"><span data-stu-id="736b9-143">The element can be empty.</span></span>|
   |<span data-ttu-id="736b9-144">PossibleValue</span><span class="sxs-lookup"><span data-stu-id="736b9-144">PossibleValue</span></span>|<span data-ttu-id="736b9-145">Ez az elem egy tároló.</span><span class="sxs-lookup"><span data-stu-id="736b9-145">This element is a container.</span></span> <span data-ttu-id="736b9-146">Az alárendelt elemek az alábbiakban olvashatók.</span><span class="sxs-lookup"><span data-stu-id="736b9-146">Its child elements are described below.</span></span> <span data-ttu-id="736b9-147">Adjon hozzá `PossibleValue` egy elemet a dinamikus paraméter minden értékéhez.</span><span class="sxs-lookup"><span data-stu-id="736b9-147">Add one `PossibleValue` element for each value of the dynamic parameter.</span></span>|
   |<span data-ttu-id="736b9-148">Érték</span><span class="sxs-lookup"><span data-stu-id="736b9-148">Value</span></span>|<span data-ttu-id="736b9-149">Megadja az érték nevét.</span><span class="sxs-lookup"><span data-stu-id="736b9-149">Specifies the value name.</span></span>|
   |<span data-ttu-id="736b9-150">Leírás</span><span class="sxs-lookup"><span data-stu-id="736b9-150">Description</span></span>|<span data-ttu-id="736b9-151">Ez az elem egy `Para` elemet tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="736b9-151">This element contains a `Para` element.</span></span> <span data-ttu-id="736b9-152">Az `Para` elem szövege a `Value` elemben szereplő értéket írja le.</span><span class="sxs-lookup"><span data-stu-id="736b9-152">The text in the `Para` element describes the value that is named in the `Value` element.</span></span>|

   <span data-ttu-id="736b9-153">A következő XML például a `PossibleValue` `Encoding` dinamikus paraméter egy elemét jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="736b9-153">For example, the following XML shows one `PossibleValue` element of the `Encoding` dynamic parameter.</span></span>

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

## <a name="example"></a><span data-ttu-id="736b9-154">Példa</span><span class="sxs-lookup"><span data-stu-id="736b9-154">Example</span></span>

<span data-ttu-id="736b9-155">A következő példában a `DynamicParameters` `Encoding` dinamikus paraméter elemét láthatja.</span><span class="sxs-lookup"><span data-stu-id="736b9-155">The following example shows the `DynamicParameters` element of the `Encoding` dynamic parameter.</span></span>

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