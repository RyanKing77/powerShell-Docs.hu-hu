---
title: Szintaxis egy parancsmag Súgó-témakör hozzáadása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d0c6d03f-1c1a-43d8-928e-e3290e90e0bc
caps.latest.revision: 5
ms.openlocfilehash: 0210b5ed3104777541692a0e78e7d3b16f9c8256
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65855135"
---
# <a name="how-to-add-syntax-to-a-cmdlet-help-topic"></a><span data-ttu-id="1ad77-102">Szintaxis hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="1ad77-102">How to Add Syntax to a Cmdlet Help Topic</span></span>

<span data-ttu-id="1ad77-103">Olvassa el ezt a szakaszt, hogy milyen típusú adatok törlése képet kapjon a parancsmag súgójában szintaxisdiagramja XML-kód megkezdése előtt meg kell adnia, például a paraméter-attribútumok és hogyan jelenjen meg az adatokat a szintaxisdiagramja...</span><span class="sxs-lookup"><span data-stu-id="1ad77-103">Before you start to code the XML for the syntax diagram in the cmdlet Help file, read this section to get a clear picture of the kind of data you need to provide, such as the parameter attributes, and how that data is displayed in the syntax diagram..</span></span>

### <a name="parameter-attributes"></a><span data-ttu-id="1ad77-104">A paraméter-attribútumok</span><span class="sxs-lookup"><span data-stu-id="1ad77-104">Parameter Attributes</span></span>

- <span data-ttu-id="1ad77-105">Szükséges</span><span class="sxs-lookup"><span data-stu-id="1ad77-105">Required</span></span>

  - <span data-ttu-id="1ad77-106">Igaz értéke esetén a paraméter szerepelnie kell minden parancs, amely a paraméterkészletet használja.</span><span class="sxs-lookup"><span data-stu-id="1ad77-106">If true, the parameter must appear in all commands that use the parameter set.</span></span>

  - <span data-ttu-id="1ad77-107">Ha FALSE (hamis), a paraméter nem kötelező minden parancs, amely a paraméterkészletet használja.</span><span class="sxs-lookup"><span data-stu-id="1ad77-107">If false, the parameter is optional in all commands that use the parameter set.</span></span>

- <span data-ttu-id="1ad77-108">Beosztás</span><span class="sxs-lookup"><span data-stu-id="1ad77-108">Position</span></span>

  - <span data-ttu-id="1ad77-109">Ha a neve, a paraméter nevének megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="1ad77-109">If named, the parameter name is required.</span></span>

  - <span data-ttu-id="1ad77-110">A Helyzetbeállító, ha a paraméter neve nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="1ad77-110">If positional, the parameter name is optional.</span></span> <span data-ttu-id="1ad77-111">Ha ki van hagyva, a paraméter értéke a parancsban megadott helyen kell lennie.</span><span class="sxs-lookup"><span data-stu-id="1ad77-111">When it is omitted, the parameter value must be in the specified position in the command.</span></span> <span data-ttu-id="1ad77-112">Például ha az érték pozíció = "1", a paraméter értékét kell lennie az első vagy csak névtelen paraméter értéke a parancsban.</span><span class="sxs-lookup"><span data-stu-id="1ad77-112">For example, if the value is position="1", the parameter value must be the first or only unnamed parameter value in the command.</span></span>

- <span data-ttu-id="1ad77-113">Adatcsatorna bemenetének</span><span class="sxs-lookup"><span data-stu-id="1ad77-113">Pipeline Input</span></span>

  - <span data-ttu-id="1ad77-114">Ha az értéke igaz (ByValue), akkor is lehet adatcsatornán bemenetet átadni a paramétert.</span><span class="sxs-lookup"><span data-stu-id="1ad77-114">If true (ByValue), you can pipe input to the parameter.</span></span> <span data-ttu-id="1ad77-115">A bemeneti társítva ("köthető az") az a paraméter, akkor is, ha a tulajdonság nevét és az objektum típusa nem egyezik a várt típus.</span><span class="sxs-lookup"><span data-stu-id="1ad77-115">The input is associated with ("bound to") the parameter even if the property name and the object type do not match the expected type.</span></span> <span data-ttu-id="1ad77-116">A Windows PowerShell? a paraméter kötelező összetevők próbálja meg a megfelelő típusú a bemenet átalakítása és a parancs csak akkor, amikor a típus nem konvertálható.</span><span class="sxs-lookup"><span data-stu-id="1ad77-116">The Windows PowerShell? parameter binding components try to convert the input to the correct type and fail the command only when the type cannot be converted.</span></span> <span data-ttu-id="1ad77-117">A paraméterkészlet csak egy paraméter értéke hozzá lehet rendelni.</span><span class="sxs-lookup"><span data-stu-id="1ad77-117">Only one parameter in a parameter set can be associated by value.</span></span>

  - <span data-ttu-id="1ad77-118">Ha az értéke igaz (ByPropertyName), akkor is lehet adatcsatornán bemenetet átadni a paramétert.</span><span class="sxs-lookup"><span data-stu-id="1ad77-118">If true (ByPropertyName), you can pipe input to the parameter.</span></span> <span data-ttu-id="1ad77-119">Azonban a bemeneti társítva a paraméter csak akkor, ha a paraméter neve megegyezik-e a bemeneti objektum olyan osztályát.</span><span class="sxs-lookup"><span data-stu-id="1ad77-119">However, the input is associated with the parameter only when the parameter name matches the name of a property of the input object.</span></span> <span data-ttu-id="1ad77-120">Például, ha a paraméter neve `Path`, irányíthatja át a parancsmag objektum arra a paraméterre társítva, csak akkor, amikor az objektum elérési útja nevű tulajdonsággal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="1ad77-120">For example, if the parameter name is `Path`, objects piped to the cmdlet are associated with that parameter only when the object has a property named path.</span></span>

  - <span data-ttu-id="1ad77-121">Ha a bemeneti paraméteréhez adatcsatornán keresztül tulajdonság neve vagy értéke igaz (ByValue, ByPropertyName).</span><span class="sxs-lookup"><span data-stu-id="1ad77-121">If true (ByValue, ByPropertyName), you can pipe input to the parameter either by property name or by value.</span></span> <span data-ttu-id="1ad77-122">A paraméterkészlet csak egy paraméter értéke hozzá lehet rendelni.</span><span class="sxs-lookup"><span data-stu-id="1ad77-122">Only one parameter in a parameter set can be associated by value.</span></span>

  - <span data-ttu-id="1ad77-123">Ha hamis, akkor a paraméter bemenete nem kanálu.</span><span class="sxs-lookup"><span data-stu-id="1ad77-123">If false, you cannot pipe input to this parameter.</span></span>

- <span data-ttu-id="1ad77-124">Helyettesítés</span><span class="sxs-lookup"><span data-stu-id="1ad77-124">Globbing</span></span>

  - <span data-ttu-id="1ad77-125">Ha az értéke igaz, a felhasználó beír a paraméter értékeként a szöveg tartalmazhat helyettesítő karaktereket is.</span><span class="sxs-lookup"><span data-stu-id="1ad77-125">If true, the text that the user types for the parameter value can include wildcard characters.</span></span>

  - <span data-ttu-id="1ad77-126">Ha nem, a felhasználó beír a paraméter értékeként a szöveg nem tartalmazhat helyettesítő karaktereket.</span><span class="sxs-lookup"><span data-stu-id="1ad77-126">If false, the text that the user types for the parameter value cannot include wildcard characters.</span></span>

### <a name="parameter-value-attributes"></a><span data-ttu-id="1ad77-127">A paraméter értéke attribútumok</span><span class="sxs-lookup"><span data-stu-id="1ad77-127">Parameter Value Attributes</span></span>

- <span data-ttu-id="1ad77-128">Szükséges</span><span class="sxs-lookup"><span data-stu-id="1ad77-128">Required</span></span>

  - <span data-ttu-id="1ad77-129">Amennyiben az értéke igaz, a megadott értéket kell használni, amikor egy paraméter használatával.</span><span class="sxs-lookup"><span data-stu-id="1ad77-129">If true, the specified value must be used whenever using the parameter in a command.</span></span>

  - <span data-ttu-id="1ad77-130">Ha nem, a paraméter értéke nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="1ad77-130">If false, the parameter value is optional.</span></span> <span data-ttu-id="1ad77-131">Általában egy értéket nem kötelező, csak akkor, ha egyike több érvényes értékei a paramétert, mint például a sorszámozott típus.</span><span class="sxs-lookup"><span data-stu-id="1ad77-131">Typically, a value is optional only when it is one of several valid values for a parameter, such as in an enumerated type.</span></span>

<span data-ttu-id="1ad77-132">Hodnota parametru szükséges attribútuma eltér a paraméter kötelező attribútum.</span><span class="sxs-lookup"><span data-stu-id="1ad77-132">The Required attribute of a parameter value is different from the Required attribute of a parameter.</span></span>

<span data-ttu-id="1ad77-133">A paraméter kötelező attribútum jelzi-e a paraméter (és annak értékét) kell foglalni a parancsmag meghívásakor.</span><span class="sxs-lookup"><span data-stu-id="1ad77-133">The required attribute of a parameter indicates whether the parameter (and its value) must be included when invoking the cmdlet.</span></span> <span data-ttu-id="1ad77-134">Ezzel szemben a paraméter értéke a kötelező attribútum csak akkor, ha a paraméter tartalmazza a parancs szolgál.</span><span class="sxs-lookup"><span data-stu-id="1ad77-134">In contrast, the required attribute of a parameter value is used only when the parameter is included in the command.</span></span> <span data-ttu-id="1ad77-135">Azt jelzi, hogy adott értékkel a paraméterrel együtt kell használni.</span><span class="sxs-lookup"><span data-stu-id="1ad77-135">It indicates whether that particular value must be used with the parameter.</span></span>

<span data-ttu-id="1ad77-136">Általában, hogy a rendszer a helyőrzők paraméterértékek szükségesek, és szövegkonstans paraméterértékeket nem szükségesek, mivel azok, amelyeket lehet, hogy a paraméter együtt több érték egyikét.</span><span class="sxs-lookup"><span data-stu-id="1ad77-136">Typically, parameter values that are placeholders are required and parameter values that are literal are not required, because they are one of several values that might be used with the parameter.</span></span>

### <a name="gathering-syntax-information"></a><span data-ttu-id="1ad77-137">Szintaxis-információk gyűjtése</span><span class="sxs-lookup"><span data-stu-id="1ad77-137">Gathering Syntax Information</span></span>

1. <span data-ttu-id="1ad77-138">Indítsa el a parancsmag neve.</span><span class="sxs-lookup"><span data-stu-id="1ad77-138">Start with the cmdlet name.</span></span>

   ```
   SYNTAX
       Get-Tech
   ```

2. <span data-ttu-id="1ad77-139">A parancsmag a paraméterek listája.</span><span class="sxs-lookup"><span data-stu-id="1ad77-139">List all the parameters of the cmdlet.</span></span> <span data-ttu-id="1ad77-140">Írja be a kötőjel (más néven "kötőjel" vagy "mínusz" (ASCII 45) előtt minden paraméter neve.</span><span class="sxs-lookup"><span data-stu-id="1ad77-140">Type a dash (also known as a "dash" or "minus sign" (ASCII 45) before each parameter name.</span></span> <span data-ttu-id="1ad77-141">A paraméterek szét paraméterkészlettel (egyes parancsmagok beállítása csak egyetlen paraméterrel rendelkezhet).</span><span class="sxs-lookup"><span data-stu-id="1ad77-141">Separate the parameters into parameter sets (some cmdlets may have only one parameter set).</span></span> <span data-ttu-id="1ad77-142">A Get, csúcskategóriás műszaki példánkban ez a parancsmag két paraméterkészlettel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="1ad77-142">In this example the Get-Tech cmdlet has two parameter sets.</span></span>

   ```
   SYNTAX
       Get-Tech -name -type
       Get-Tech -ID -list -type
   ```

   <span data-ttu-id="1ad77-143">Indítsa el az egyes parancsmag nevű paramétert.</span><span class="sxs-lookup"><span data-stu-id="1ad77-143">Start each parameter set with the cmdlet name.</span></span>

   <span data-ttu-id="1ad77-144">Az alapértelmezett paraméter első listája.</span><span class="sxs-lookup"><span data-stu-id="1ad77-144">List the default parameter set first.</span></span> <span data-ttu-id="1ad77-145">Az alapértelmezett paraméter nincs megadva, a parancsmag osztály alapján.</span><span class="sxs-lookup"><span data-stu-id="1ad77-145">The default parameter is specified by the cmdlet class.</span></span>

   <span data-ttu-id="1ad77-146">Minden egyes paraméterkészletet listázza egyedi paramétereként először, kivéve ha pozícióparaméterek kell elsőként jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="1ad77-146">For each parameter set, list its unique parameter first, unless there are positional parameters that must appear first.</span></span> <span data-ttu-id="1ad77-147">Az előző példában a neve és azonosítója paraméterei a két paraméterkészlettel egyedi paramétereket (a minden egyes paraméterkészletet musí mít jeden parametr, amely egyedi az adott paraméter).</span><span class="sxs-lookup"><span data-stu-id="1ad77-147">In the previous example, the Name and ID parameters are unique parameters for the two parameter sets (each parameter set must have one parameter that is unique to that parameter set).</span></span> <span data-ttu-id="1ad77-148">Így megkönnyítheti a felhasználók azonosítására, hogy milyen paramétert, akkor meg kell adnia a paraméter beállítása.</span><span class="sxs-lookup"><span data-stu-id="1ad77-148">This makes it easier for users to identify what parameter they need to supply for the parameter set.</span></span>

   <span data-ttu-id="1ad77-149">A megadott sorrendben szerepelniük kell a parancs a paraméterek listája.</span><span class="sxs-lookup"><span data-stu-id="1ad77-149">List the parameters in the order that they should appear in the command.</span></span> <span data-ttu-id="1ad77-150">Sorrendje nem számít, ha a kapcsolódó paraméterekkel együtt listában, vagy először lista a leggyakrabban használt paraméterek.</span><span class="sxs-lookup"><span data-stu-id="1ad77-150">If the order does not matter, list related parameters together, or list the most frequently used parameters first.</span></span>

   <span data-ttu-id="1ad77-151">Győződjön meg arról, a WhatIf és Confirm paraméter listázásához, ha a parancsmag támogatja a ShouldProcess.</span><span class="sxs-lookup"><span data-stu-id="1ad77-151">Be sure to list the WhatIf and Confirm parameters if the cmdlet supports ShouldProcess.</span></span>

   <span data-ttu-id="1ad77-152">A következő általános paramétereket (például a Verbose, a hibakeresési és ErrorAction) a szintaxis diagramon nem szerepelhet.</span><span class="sxs-lookup"><span data-stu-id="1ad77-152">Do not list the common parameters (such as Verbose, Debug, and ErrorAction) in your syntax diagram.</span></span> <span data-ttu-id="1ad77-153">A `Get-Help` parancsmag hozzáadja ezt az információt, amikor megjeleníti a Súgó-témakör.</span><span class="sxs-lookup"><span data-stu-id="1ad77-153">The `Get-Help` cmdlet adds that information for you when it displays the Help topic.</span></span>

3. <span data-ttu-id="1ad77-154">Adja hozzá a paraméterértékeket.</span><span class="sxs-lookup"><span data-stu-id="1ad77-154">Add the parameter values.</span></span> <span data-ttu-id="1ad77-155">A Windows PowerShell?, a .NET-típus paraméter értékét képviseli.</span><span class="sxs-lookup"><span data-stu-id="1ad77-155">In Windows PowerShell?, parameter values are represented by their .NET type.</span></span> <span data-ttu-id="1ad77-156">Azonban a típusnév rövidíthető, például a "string" System.String.</span><span class="sxs-lookup"><span data-stu-id="1ad77-156">However, the type name can be abbreviated, such as "string" for System.String.</span></span>

   ```
   SYNTAX
       Get-Tech -name string -type basic advanced
       Get-Tech -ID int -list -type basic advanced
   ```

   <span data-ttu-id="1ad77-157">Mindaddig, amíg azok jelentését nincs bejelölve, például "string" System.String és "int" System.Int32, rövidítése típusokat.</span><span class="sxs-lookup"><span data-stu-id="1ad77-157">Abbreviate types as long as their meaning is clear, such as "string" for System.String and "int" for System.Int32.</span></span>

   <span data-ttu-id="1ad77-158">A listában szereplő összes enumerálások, például az "alapszintű" vagy "speciális" való beállítása az előző példában a - típusú paramétert.</span><span class="sxs-lookup"><span data-stu-id="1ad77-158">List all values of enumerations, such as the -type parameter in the previous example, which can be set to "basic" or "advanced".</span></span>

   <span data-ttu-id="1ad77-159">Váltson a paraméterek, például - lista az előző példában szereplő, nem rendelkezik az értékekkel.</span><span class="sxs-lookup"><span data-stu-id="1ad77-159">Switch parameters, such as -list in the previous example, do not have values.</span></span>

4. <span data-ttu-id="1ad77-160">Adja hozzá a csúcsos zárójeleket helyőrző, mint a korábban megszokott literálok paraméterértékeket paraméterek értékeket.</span><span class="sxs-lookup"><span data-stu-id="1ad77-160">Add angle brackets to parameters values that are placeholder, as compared to parameter values that are literals.</span></span>

   ```
   SYNTAX
       Get-Tech -name <string> -type basic advanced
       Get-Tech -ID <int> -list -type basic advanced
   ```

5. <span data-ttu-id="1ad77-161">Nem kötelező paraméterek és azok értékeket foglaljuk szögletes zárójelek közé.</span><span class="sxs-lookup"><span data-stu-id="1ad77-161">Enclose optional parameters and their vales in square brackets.</span></span>

   ```
   SYNTAX
       Get-Tech -name <string> [-type basic advanced]
       Get-Tech -ID <int> [-list] [-type basic advanced]
   ```

6. <span data-ttu-id="1ad77-162">Választható paraméterek nevei (a pozicionális paramétereknél) foglaljuk szögletes zárójelek közé.</span><span class="sxs-lookup"><span data-stu-id="1ad77-162">Enclose optional parameters names (for positional parameters) in square brackets.</span></span> <span data-ttu-id="1ad77-163">A name paraméterek csak pozíciórekord, például a következő példában a Name paraméter esetében nem kell a parancsban benne lennie.</span><span class="sxs-lookup"><span data-stu-id="1ad77-163">The name for parameters that are positional, such as the Name parameter in the following example, do not have to be included in the command.</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <string> [-type basic advanced]
       Get-Tech -ID <int> [-list] [-type basic advanced]
   ```

7. <span data-ttu-id="1ad77-164">Ha egy paraméterérték tartalmazhat több érték a Name paraméter, a nevek listája például szögletes zárójelek között, a paraméter értéke a következő két hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="1ad77-164">If a parameter value can contain multiple values, such as a list of names in the Name parameter, add a pair of square brackets directly following the parameter value.</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <string[]> [-type basic advanced]
       Get-Tech -ID <int[]> [-list] [-type basic advanced]
   ```

8. <span data-ttu-id="1ad77-165">Ha a felhasználó kiválaszthat a paraméterek vagy a paraméterértékeket, például a típus paraméternél tegye a választási lehetőségek kapcsos zárójelek közé, és válassza el őket a kizárólagos vagy symbol(;).</span><span class="sxs-lookup"><span data-stu-id="1ad77-165">If the user can choose from parameters or parameter values, such as the Type parameter, enclose the choices in curly brackets and separate them with the exclusive OR symbol(;).</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <string[]> [-type {basic | advanced}]
       Get-Tech -ID <int[]> [-list] [-type {basic | advanced}]
   ```

9. <span data-ttu-id="1ad77-166">Ha a paraméter értékét kell használnia adott formázás, idézőjelek vagy zárójelben, például a szintaxis megjelenítése formátumban.</span><span class="sxs-lookup"><span data-stu-id="1ad77-166">If the parameter value must use specific formatting, such as quotation marks or parentheses, show the format in the syntax.</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <"string[]"> [-type {basic | advanced}]
       Get-Tech -ID <int[]> [-list] [-type {basic | advanced}]
   ```

## <a name="coding-the-syntax-diagram-xml"></a><span data-ttu-id="1ad77-167">Kódolási Szintaxisdiagramja XML</span><span class="sxs-lookup"><span data-stu-id="1ad77-167">Coding the Syntax Diagram XML</span></span>

<span data-ttu-id="1ad77-168">A leírás csomópont vége után azonnal megkezdődik a szintaxis csomópont XML-kód a \</maml:description > címke.</span><span class="sxs-lookup"><span data-stu-id="1ad77-168">The syntax node of the XML begins immediately after the description node, which ends with the \</maml:description> tag.</span></span> <span data-ttu-id="1ad77-169">Szintaxisdiagramja használja az adatok összegyűjtésével kapcsolatban lásd: [szintaxis információk összegyűjtéséhez](#gathering-syntax-information).</span><span class="sxs-lookup"><span data-stu-id="1ad77-169">For information about gathering the data used in the syntax diagram, see [Gathering Syntax Information](#gathering-syntax-information).</span></span>

### <a name="adding-a-syntax-node"></a><span data-ttu-id="1ad77-170">Szintaxis csomópont hozzáadása</span><span class="sxs-lookup"><span data-stu-id="1ad77-170">Adding a Syntax Node</span></span>

<span data-ttu-id="1ad77-171">Az adatokból az XML-fájl szintaktikai csomópontjában jelenik meg a parancsmag súgó-témakörének szintaxisdiagramja jön létre.</span><span class="sxs-lookup"><span data-stu-id="1ad77-171">The syntax diagram displayed in the cmdlet Help topic is generated from the data in the syntax node of the XML.</span></span> <span data-ttu-id="1ad77-172">A szintaxis csomópont idézőjelek között egy pár, ha \<parancsszintaxist: > címkéket.</span><span class="sxs-lookup"><span data-stu-id="1ad77-172">The syntax node is enclosed in a pair if \<command:syntax> tags.</span></span> <span data-ttu-id="1ad77-173">Az egyes paraméterkészletet, a parancsmag egy idézőjelbe foglalt \<parancs: syntaxitem > címkéket.</span><span class="sxs-lookup"><span data-stu-id="1ad77-173">With each parameter set of the cmdlet enclosed in a pair of \<command:syntaxitem> tags.</span></span> <span data-ttu-id="1ad77-174">Nem korlátozott számú \<parancs: syntaxitem > címkéket adhat hozzá.</span><span class="sxs-lookup"><span data-stu-id="1ad77-174">There is no limit to the number of \<command:syntaxitem> tags that you can add.</span></span>

<span data-ttu-id="1ad77-175">Az alábbi példa bemutatja egy szintaxis csomópont, amely szintaxis elem csomópontok két paraméterkészlettel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="1ad77-175">The following example shows a syntax node that has syntax item nodes for two parameter sets.</span></span>

```xml
<command:syntax>
  <command:syntaxItem>
    ...
    <!--Parameter Set 1 (default parameter set) parameters go here-->
    ...
  </command:syntaxItem>
  <command:syntaxItem>
    ...
    <!--Parameter Set 2 parameters go here-->
    ...
  </command:syntaxItem>
</command:syntax>
```

### <a name="adding-the-cmdlet-name-to-the-parameter-set-data"></a><span data-ttu-id="1ad77-176">Adatok hozzáadása a parancsmag Name paraméteréhez beállítása</span><span class="sxs-lookup"><span data-stu-id="1ad77-176">Adding the Cmdlet Name to the Parameter Set Data</span></span>

<span data-ttu-id="1ad77-177">Minden egyes paraméterkészletet, a parancsmag szintaxisa elem csomópont van megadva.</span><span class="sxs-lookup"><span data-stu-id="1ad77-177">Each parameter set of the cmdlet is specified in a syntax item node.</span></span> <span data-ttu-id="1ad77-178">Minden egyes szintaxis elem csomópont párjai kezdődik \<maml:name > címkék, amely tartalmazza annak a parancsmagnak a nevét.</span><span class="sxs-lookup"><span data-stu-id="1ad77-178">Each syntax item node begins with a pair of \<maml:name> tags that include the name of the cmdlet.</span></span>

<span data-ttu-id="1ad77-179">Az alábbi példában megtalálhatja, amely rendelkezik a szintaxis-elem csomópont két paraméterkészlettel szintaxis csomópont.</span><span class="sxs-lookup"><span data-stu-id="1ad77-179">The following example includes a syntax node that has syntax item nodes for two parameter sets.</span></span>

```xml
<command:syntax>
  <command:syntaxItem>
    <maml:name>Cmdlet-Name</maml:name>
  </command:syntaxItem>
  <command:syntaxItem>
    <maml:name>Cmdlet-Name</maml:name>
  </command:syntaxItem>
</command:syntax>
```

### <a name="adding-parameters"></a><span data-ttu-id="1ad77-180">Paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="1ad77-180">Adding Parameters</span></span>

<span data-ttu-id="1ad77-181">Minden egyes paraméter, a szintaxis elem csomópont van megadva egy \<parancsparaméter: > címkéket.</span><span class="sxs-lookup"><span data-stu-id="1ad77-181">Each parameter added to the syntax item node is specified within a pair of \<command:parameter> tags.</span></span> <span data-ttu-id="1ad77-182">Egy kulcspárra van szüksége \<parancsparaméter: > címke szerepel a paraméterkészletet, a következő általános paramétereket, amelyek a Windows PowerShell által biztosított kivételével minden paraméter?.</span><span class="sxs-lookup"><span data-stu-id="1ad77-182">You need a pair of \<command:parameter> tags for each parameter included in the parameter set, with the exception of the common parameters that are provided by Windows PowerShell?.</span></span>

<span data-ttu-id="1ad77-183">A nyitó attribútumai \<parancsparaméter: > címke határozza meg, hogyan jelenjen meg a paraméter szintaxisdiagramja.</span><span class="sxs-lookup"><span data-stu-id="1ad77-183">The attributes of the opening \<command:parameter> tag determine how the parameter appears in the syntax diagram.</span></span> <span data-ttu-id="1ad77-184">A paraméter-attribútumok kapcsolatos információkért lásd: [paraméter-attribútumok](#parameter-attributes).</span><span class="sxs-lookup"><span data-stu-id="1ad77-184">For information on parameter attributes, see [Parameter Attributes](#parameter-attributes).</span></span>

> [!NOTE]
> <span data-ttu-id="1ad77-185">A \<parancsparaméter: > címke támogatja a gyermekelem \<maml:description > tartalmú soha nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1ad77-185">The \<command:parameter> tag supports a child element \<maml:description> whose content is never displayed.</span></span> <span data-ttu-id="1ad77-186">A paraméterek leírásait meg van adva a paraméter csomópont XML-kód.</span><span class="sxs-lookup"><span data-stu-id="1ad77-186">The parameter descriptions are specified in the parameter node of the XML.</span></span> <span data-ttu-id="1ad77-187">A szintaxis elem található információk közötti inkonzisztencia elkerülése érdekében bodes és a paraméter csomópont, hagyja ki a (\<maml:description >, vagy hagyja üresen.</span><span class="sxs-lookup"><span data-stu-id="1ad77-187">To avoid inconsistencies between the information in the syntax item bodes and the parameter node, omit the (\<maml:description> or leave it empty.</span></span>

<span data-ttu-id="1ad77-188">Az alábbi példa egy két paraméterrel rendelkező paraméter szintaxisa elem csomópont tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="1ad77-188">The following example includes a syntax item node for a parameter set with two parameters.</span></span>

```xml
<command:syntaxItem>
  <maml:name>Cmdlet-Name</maml:name>
  <command:parameter required="true" globbing="true"
    pipelineInput="true (ByValue)" position="1">
    <maml:name>ParameterName1</maml:name>
    <command:parameterValue required="true">
      string[]
    </command:parameterValue>
  </command:parameter>
  <command:parameter required="true" globbing="true"
    pipelineInput="true (ByPropertyName)">
    <maml:name>ParameterName2</maml:name>
    <command:parameterValue required="true">
      int32[]
    </command:parameterValue>
  </command:parameter>
</command:syntaxItem>
```
