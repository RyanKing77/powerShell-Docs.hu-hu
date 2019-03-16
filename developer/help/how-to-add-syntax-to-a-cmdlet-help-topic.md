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
ms.openlocfilehash: 2e9dbc9ff8f9507f2008cd6e114ba6fec36b10bf
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054611"
---
# <a name="how-to-add-syntax-to-a-cmdlet-help-topic"></a><span data-ttu-id="e5dfe-102">Szintaxis hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz</span><span class="sxs-lookup"><span data-stu-id="e5dfe-102">How to Add Syntax to a Cmdlet Help Topic</span></span>

- [<span data-ttu-id="e5dfe-103">A paraméter-attribútumok</span><span class="sxs-lookup"><span data-stu-id="e5dfe-103">Parameter Attributes</span></span>](#Parameter-Attributes)

- [<span data-ttu-id="e5dfe-104">A paraméter értéke attribútumok</span><span class="sxs-lookup"><span data-stu-id="e5dfe-104">Parameter Value Attributes</span></span>](#Parameter-Value-Attributes)

- [<span data-ttu-id="e5dfe-105">Szintaxis-információk gyűjtése</span><span class="sxs-lookup"><span data-stu-id="e5dfe-105">Gathering Syntax Information</span></span>](#Gathering-Syntax-Information)

- [<span data-ttu-id="e5dfe-106">Kódolási Szintaxisdiagramja XML</span><span class="sxs-lookup"><span data-stu-id="e5dfe-106">Coding the Syntax Diagram XML</span></span>](#Coding-the-Syntax-Diagram-XML)

## <a name="things-to-know-about-the-syntax-diagram-in-cmdlet-help"></a><span data-ttu-id="e5dfe-107">Tudnivaló a parancsmag súgóját Szintaxisdiagramja kapcsolatban</span><span class="sxs-lookup"><span data-stu-id="e5dfe-107">Things to Know About the Syntax Diagram in Cmdlet Help</span></span>

<span data-ttu-id="e5dfe-108">Olvassa el ezt a szakaszt, hogy milyen típusú adatok törlése képet kapjon a parancsmag súgójában szintaxisdiagramja XML-kód megkezdése előtt meg kell adnia, például a paraméter-attribútumok és hogyan jelenjen meg az adatokat a szintaxisdiagramja...</span><span class="sxs-lookup"><span data-stu-id="e5dfe-108">Before you start to code the XML for the syntax diagram in the cmdlet Help file, read this section to get a clear picture of the kind of data you need to provide, such as the parameter attributes, and how that data is displayed in the syntax diagram..</span></span>

### <a name="parameter-attributes"></a><span data-ttu-id="e5dfe-109">A paraméter-attribútumok</span><span class="sxs-lookup"><span data-stu-id="e5dfe-109">Parameter Attributes</span></span>

- <span data-ttu-id="e5dfe-110">Szükséges</span><span class="sxs-lookup"><span data-stu-id="e5dfe-110">Required</span></span>

  - <span data-ttu-id="e5dfe-111">Igaz értéke esetén a paraméter szerepelnie kell minden parancs, amely a paraméterkészletet használja.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-111">If true, the parameter must appear in all commands that use the parameter set.</span></span>

  - <span data-ttu-id="e5dfe-112">Ha FALSE (hamis), a paraméter nem kötelező minden parancs, amely a paraméterkészletet használja.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-112">If false, the parameter is optional in all commands that use the parameter set.</span></span>

- <span data-ttu-id="e5dfe-113">Beosztás</span><span class="sxs-lookup"><span data-stu-id="e5dfe-113">Position</span></span>

  - <span data-ttu-id="e5dfe-114">Ha a neve, a paraméter nevének megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-114">If named, the parameter name is required.</span></span>

  - <span data-ttu-id="e5dfe-115">A Helyzetbeállító, ha a paraméter neve nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-115">If positional, the parameter name is optional.</span></span> <span data-ttu-id="e5dfe-116">Ha ki van hagyva, a paraméter értéke a parancsban megadott helyen kell lennie.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-116">When it is omitted, the parameter value must be in the specified position in the command.</span></span> <span data-ttu-id="e5dfe-117">Például ha az érték pozíció = "1", a paraméter értékét kell lennie az első vagy csak névtelen paraméter értéke a parancsban.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-117">For example, if the value is position="1", the parameter value must be the first or only unnamed parameter value in the command.</span></span>

- <span data-ttu-id="e5dfe-118">Adatcsatorna bemenetének</span><span class="sxs-lookup"><span data-stu-id="e5dfe-118">Pipeline Input</span></span>

  - <span data-ttu-id="e5dfe-119">Ha az értéke igaz (ByValue), akkor is lehet adatcsatornán bemenetet átadni a paramétert.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-119">If true (ByValue), you can pipe input to the parameter.</span></span> <span data-ttu-id="e5dfe-120">A bemeneti társítva ("köthető az") az a paraméter, akkor is, ha a tulajdonság nevét és az objektum típusa nem egyezik a várt típus.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-120">The input is associated with ("bound to") the parameter even if the property name and the object type do not match the expected type.</span></span> <span data-ttu-id="e5dfe-121">A Windows PowerShell? a paraméter kötelező összetevők próbálja meg a megfelelő típusú a bemenet átalakítása és a parancs csak akkor, amikor a típus nem konvertálható.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-121">The Windows PowerShell? parameter binding components try to convert the input to the correct type and fail the command only when the type cannot be converted.</span></span> <span data-ttu-id="e5dfe-122">A paraméterkészlet csak egy paraméter értéke hozzá lehet rendelni.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-122">Only one parameter in a parameter set can be associated by value.</span></span>

  - <span data-ttu-id="e5dfe-123">Ha az értéke igaz (ByPropertyName), akkor is lehet adatcsatornán bemenetet átadni a paramétert.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-123">If true (ByPropertyName), you can pipe input to the parameter.</span></span> <span data-ttu-id="e5dfe-124">Azonban a bemeneti társítva a paraméter csak akkor, ha a paraméter neve megegyezik-e a bemeneti objektum olyan osztályát.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-124">However, the input is associated with the parameter only when the parameter name matches the name of a property of the input object.</span></span> <span data-ttu-id="e5dfe-125">Például, ha a paraméter neve `Path`, irányíthatja át a parancsmag objektum arra a paraméterre társítva, csak akkor, amikor az objektum elérési útja nevű tulajdonsággal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-125">For example, if the parameter name is `Path`, objects piped to the cmdlet are associated with that parameter only when the object has a property named path.</span></span>

  - <span data-ttu-id="e5dfe-126">Ha a bemeneti paraméteréhez adatcsatornán keresztül tulajdonság neve vagy értéke igaz (ByValue, ByPropertyName).</span><span class="sxs-lookup"><span data-stu-id="e5dfe-126">If true (ByValue, ByPropertyName), you can pipe input to the parameter either by property name or by value.</span></span> <span data-ttu-id="e5dfe-127">A paraméterkészlet csak egy paraméter értéke hozzá lehet rendelni.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-127">Only one parameter in a parameter set can be associated by value.</span></span>

  - <span data-ttu-id="e5dfe-128">Ha hamis, akkor a paraméter bemenete nem kanálu.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-128">If false, you cannot pipe input to this parameter.</span></span>

- <span data-ttu-id="e5dfe-129">Helyettesítés</span><span class="sxs-lookup"><span data-stu-id="e5dfe-129">Globbing</span></span>

  - <span data-ttu-id="e5dfe-130">Ha az értéke igaz, a felhasználó beír a paraméter értékeként a szöveg tartalmazhat helyettesítő karaktereket is.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-130">If true, the text that the user types for the parameter value can include wildcard characters.</span></span>

  - <span data-ttu-id="e5dfe-131">Ha nem, a felhasználó beír a paraméter értékeként a szöveg nem tartalmazhat helyettesítő karaktereket.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-131">If false, the text that the user types for the parameter value cannot include wildcard characters.</span></span>

### <a name="parameter-value-attributes"></a><span data-ttu-id="e5dfe-132">A paraméter értéke attribútumok</span><span class="sxs-lookup"><span data-stu-id="e5dfe-132">Parameter Value Attributes</span></span>

- <span data-ttu-id="e5dfe-133">Szükséges</span><span class="sxs-lookup"><span data-stu-id="e5dfe-133">Required</span></span>

  - <span data-ttu-id="e5dfe-134">Amennyiben az értéke igaz, a megadott értéket kell használni, amikor egy paraméter használatával.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-134">If true, the specified value must be used whenever using the parameter in a command.</span></span>

  - <span data-ttu-id="e5dfe-135">Ha nem, a paraméter értéke nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-135">If false, the parameter value is optional.</span></span> <span data-ttu-id="e5dfe-136">Általában egy értéket nem kötelező, csak akkor, ha egyike több érvényes értékei a paramétert, mint például a sorszámozott típus.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-136">Typically, a value is optional only when it is one of several valid values for a parameter, such as in an enumerated type.</span></span>

<span data-ttu-id="e5dfe-137">Hodnota parametru szükséges attribútuma eltér a paraméter kötelező attribútum.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-137">The Required attribute of a parameter value is different from the Required attribute of a parameter.</span></span>

<span data-ttu-id="e5dfe-138">A paraméter kötelező attribútum jelzi-e a paraméter (és annak értékét) kell foglalni a parancsmag meghívásakor.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-138">The required attribute of a parameter indicates whether the parameter (and its value) must be included when invoking the cmdlet.</span></span> <span data-ttu-id="e5dfe-139">Ezzel szemben a paraméter értéke a kötelező attribútum csak akkor, ha a paraméter tartalmazza a parancs szolgál.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-139">In contrast, the required attribute of a parameter value is used only when the parameter is included in the command.</span></span> <span data-ttu-id="e5dfe-140">Azt jelzi, hogy adott értékkel a paraméterrel együtt kell használni.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-140">It indicates whether that particular value must be used with the parameter.</span></span>

<span data-ttu-id="e5dfe-141">Általában, hogy a rendszer a helyőrzők paraméterértékek szükségesek, és szövegkonstans paraméterértékeket nem szükségesek, mivel azok, amelyeket lehet, hogy a paraméter együtt több érték egyikét.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-141">Typically, parameter values that are placeholders are required and parameter values that are literal are not required, because they are one of several values that might be used with the parameter.</span></span>

### <a name="gathering-syntax-information"></a><span data-ttu-id="e5dfe-142">Szintaxis-információk gyűjtése</span><span class="sxs-lookup"><span data-stu-id="e5dfe-142">Gathering Syntax Information</span></span>

1. <span data-ttu-id="e5dfe-143">Indítsa el a parancsmag neve.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-143">Start with the cmdlet name.</span></span>

   ```
   SYNTAX
       Get-Tech
   ```

2. <span data-ttu-id="e5dfe-144">A parancsmag a paraméterek listája.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-144">List all the parameters of the cmdlet.</span></span> <span data-ttu-id="e5dfe-145">Írja be a kötőjel (más néven "kötőjel" vagy "mínusz" (ASCII 45) előtt minden paraméter neve.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-145">Type a dash (also known as a "dash" or "minus sign" (ASCII 45) before each parameter name.</span></span> <span data-ttu-id="e5dfe-146">A paraméterek szét paraméterkészlettel (egyes parancsmagok beállítása csak egyetlen paraméterrel rendelkezhet).</span><span class="sxs-lookup"><span data-stu-id="e5dfe-146">Separate the parameters into parameter sets (some cmdlets may have only one parameter set).</span></span> <span data-ttu-id="e5dfe-147">A Get, csúcskategóriás műszaki példánkban ez a parancsmag két paraméterkészlettel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-147">In this example the Get-Tech cmdlet has two parameter sets.</span></span>

   ```
   SYNTAX
       Get-Tech -name -type
       Get-Tech -ID -list -type
   ```

   <span data-ttu-id="e5dfe-148">Indítsa el az egyes parancsmag nevű paramétert.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-148">Start each parameter set with the cmdlet name.</span></span>

   <span data-ttu-id="e5dfe-149">Az alapértelmezett paraméter első listája.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-149">List the default parameter set first.</span></span> <span data-ttu-id="e5dfe-150">Az alapértelmezett paraméter nincs megadva, a parancsmag osztály alapján.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-150">The default parameter is specified by the cmdlet class.</span></span>

   <span data-ttu-id="e5dfe-151">Minden egyes paraméterkészletet listázza egyedi paramétereként először, kivéve ha pozícióparaméterek kell elsőként jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-151">For each parameter set, list its unique parameter first, unless there are positional parameters that must appear first.</span></span> <span data-ttu-id="e5dfe-152">Az előző példában a neve és azonosítója paraméterei a két paraméterkészlettel egyedi paramétereket (a minden egyes paraméterkészletet musí mít jeden parametr, amely egyedi az adott paraméter).</span><span class="sxs-lookup"><span data-stu-id="e5dfe-152">In the previous example, the Name and ID parameters are unique parameters for the two parameter sets (each parameter set must have one parameter that is unique to that parameter set).</span></span> <span data-ttu-id="e5dfe-153">Így megkönnyítheti a felhasználók azonosítására, hogy milyen paramétert, akkor meg kell adnia a paraméter beállítása.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-153">This makes it easier for users to identify what parameter they need to supply for the parameter set.</span></span>

   <span data-ttu-id="e5dfe-154">A megadott sorrendben szerepelniük kell a parancs a paraméterek listája.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-154">List the parameters in the order that they should appear in the command.</span></span> <span data-ttu-id="e5dfe-155">Sorrendje nem számít, ha a kapcsolódó paraméterekkel együtt listában, vagy először lista a leggyakrabban használt paraméterek.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-155">If the order does not matter, list related parameters together, or list the most frequently used parameters first.</span></span>

   <span data-ttu-id="e5dfe-156">Győződjön meg arról, a WhatIf és Confirm paraméter listázásához, ha a parancsmag támogatja a ShouldProcess.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-156">Be sure to list the WhatIf and Confirm parameters if the cmdlet supports ShouldProcess.</span></span>

   <span data-ttu-id="e5dfe-157">A következő általános paramétereket (például a Verbose, a hibakeresési és ErrorAction) a szintaxis diagramon nem szerepelhet.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-157">Do not list the common parameters (such as Verbose, Debug, and ErrorAction) in your syntax diagram.</span></span> <span data-ttu-id="e5dfe-158">A `Get-Help` parancsmag hozzáadja ezt az információt, amikor megjeleníti a Súgó-témakör.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-158">The `Get-Help` cmdlet adds that information for you when it displays the Help topic.</span></span>

3. <span data-ttu-id="e5dfe-159">Adja hozzá a paraméterértékeket.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-159">Add the parameter values.</span></span> <span data-ttu-id="e5dfe-160">A Windows PowerShell?, a .NET-típus paraméter értékét képviseli.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-160">In Windows PowerShell?, parameter values are represented by their .NET type.</span></span> <span data-ttu-id="e5dfe-161">Azonban a típusnév rövidíthető, például a "string" System.String.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-161">However, the type name can be abbreviated, such as "string" for System.String.</span></span>

   ```
   SYNTAX
       Get-Tech -name string -type basic advanced
       Get-Tech -ID int -list -type basic advanced
   ```

   <span data-ttu-id="e5dfe-162">Mindaddig, amíg azok jelentését nincs bejelölve, például "string" System.String és "int" System.Int32, rövidítése típusokat.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-162">Abbreviate types as long as their meaning is clear, such as "string" for System.String and "int" for System.Int32.</span></span>

   <span data-ttu-id="e5dfe-163">A listában szereplő összes enumerálások, például az "alapszintű" vagy "speciális" való beállítása az előző példában a - típusú paramétert.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-163">List all values of enumerations, such as the -type parameter in the previous example, which can be set to "basic" or "advanced".</span></span>

   <span data-ttu-id="e5dfe-164">Váltson a paraméterek, például - lista az előző példában szereplő, nem rendelkezik az értékekkel.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-164">Switch parameters, such as -list in the previous example, do not have values.</span></span>

4. <span data-ttu-id="e5dfe-165">Adja hozzá a csúcsos zárójeleket helyőrző, mint a korábban megszokott literálok paraméterértékeket paraméterek értékeket.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-165">Add angle brackets to parameters values that are placeholder, as compared to parameter values that are literals.</span></span>

   ```
   SYNTAX
       Get-Tech -name <string> -type basic advanced
       Get-Tech -ID <int> -list -type basic advanced
   ```

5. <span data-ttu-id="e5dfe-166">Nem kötelező paraméterek és azok értékeket foglaljuk szögletes zárójelek közé.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-166">Enclose optional parameters and their vales in square brackets.</span></span>

   ```
   SYNTAX
       Get-Tech -name <string> [-type basic advanced]
       Get-Tech -ID <int> [-list] [-type basic advanced]
   ```

6. <span data-ttu-id="e5dfe-167">Választható paraméterek nevei (a pozicionális paramétereknél) foglaljuk szögletes zárójelek közé.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-167">Enclose optional parameters names (for positional parameters) in square brackets.</span></span> <span data-ttu-id="e5dfe-168">A name paraméterek csak pozíciórekord, például a következő példában a Name paraméter esetében nem kell a parancsban benne lennie.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-168">The name for parameters that are positional, such as the Name parameter in the following example, do not have to be included in the command.</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <string> [-type basic advanced]
       Get-Tech -ID <int> [-list] [-type basic advanced]
   ```

7. <span data-ttu-id="e5dfe-169">Ha egy paraméterérték tartalmazhat több érték a Name paraméter, a nevek listája például szögletes zárójelek között, a paraméter értéke a következő két hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-169">If a parameter value can contain multiple values, such as a list of names in the Name parameter, add a pair of square brackets directly following the parameter value.</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <string[]> [-type basic advanced]
       Get-Tech -ID <int[]> [-list] [-type basic advanced]
   ```

8. <span data-ttu-id="e5dfe-170">Ha a felhasználó kiválaszthat a paraméterek vagy a paraméterértékeket, például a típus paraméternél tegye a választási lehetőségek kapcsos zárójelek közé, és válassza el őket a kizárólagos vagy symbol(;).</span><span class="sxs-lookup"><span data-stu-id="e5dfe-170">If the user can choose from parameters or parameter values, such as the Type parameter, enclose the choices in curly brackets and separate them with the exclusive OR symbol(;).</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <string[]> [-type {basic | advanced}]
       Get-Tech -ID <int[]> [-list] [-type {basic | advanced}]
   ```

9. <span data-ttu-id="e5dfe-171">Ha a paraméter értékét kell használnia adott formázás, idézőjelek vagy zárójelben, például a szintaxis megjelenítése formátumban.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-171">If the parameter value must use specific formatting, such as quotation marks or parentheses, show the format in the syntax.</span></span>

   ```
   SYNTAX
       Get-Tech [-name] <"string[]"> [-type {basic | advanced}]
       Get-Tech -ID <int[]> [-list] [-type {basic | advanced}]
   ```

## <a name="coding-the-syntax-diagram-xml"></a><span data-ttu-id="e5dfe-172">Kódolási Szintaxisdiagramja XML</span><span class="sxs-lookup"><span data-stu-id="e5dfe-172">Coding the Syntax Diagram XML</span></span>

<span data-ttu-id="e5dfe-173">A leírás csomópont vége után azonnal megkezdődik a szintaxis csomópont XML-kód a \</maml:description > címke.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-173">The syntax node of the XML begins immediately after the description node, which ends with the \</maml:description> tag.</span></span> <span data-ttu-id="e5dfe-174">Szintaxisdiagramja használja az adatok összegyűjtésével kapcsolatban lásd: [szintaxis információk összegyűjtéséhez](#Gathering-Syntax-Information).</span><span class="sxs-lookup"><span data-stu-id="e5dfe-174">For information about gathering the data used in the syntax diagram, see [Gathering Syntax Information](#Gathering-Syntax-Information).</span></span>

### <a name="adding-a-syntax-node"></a><span data-ttu-id="e5dfe-175">Szintaxis csomópont hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e5dfe-175">Adding a Syntax Node</span></span>

<span data-ttu-id="e5dfe-176">Az adatokból az XML-fájl szintaktikai csomópontjában jelenik meg a parancsmag súgó-témakörének szintaxisdiagramja jön létre.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-176">The syntax diagram displayed in the cmdlet Help topic is generated from the data in the syntax node of the XML.</span></span> <span data-ttu-id="e5dfe-177">A szintaxis csomópont idézőjelek között egy pár, ha \<parancsszintaxist: > címkéket.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-177">The syntax node is enclosed in a pair if \<command:syntax> tags.</span></span> <span data-ttu-id="e5dfe-178">Az egyes paraméterkészletet, a parancsmag egy idézőjelbe foglalt \<parancs: syntaxitem > címkéket.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-178">With each parameter set of the cmdlet enclosed in a pair of \<command:syntaxitem> tags.</span></span> <span data-ttu-id="e5dfe-179">Nem korlátozott számú \<parancs: syntaxitem > címkéket adhat hozzá.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-179">There is no limit to the number of \<command:syntaxitem> tags that you can add.</span></span>

<span data-ttu-id="e5dfe-180">Az alábbi példa bemutatja egy szintaxis csomópont, amely szintaxis elem csomópontok két paraméterkészlettel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-180">The following example shows a syntax node that has syntax item nodes for two parameter sets.</span></span>

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

### <a name="adding-the-cmdlet-name-to-the-parameter-set-data"></a><span data-ttu-id="e5dfe-181">Adatok hozzáadása a parancsmag Name paraméteréhez beállítása</span><span class="sxs-lookup"><span data-stu-id="e5dfe-181">Adding the Cmdlet Name to the Parameter Set Data</span></span>

<span data-ttu-id="e5dfe-182">Minden egyes paraméterkészletet, a parancsmag szintaxisa elem csomópont van megadva.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-182">Each parameter set of the cmdlet is specified in a syntax item node.</span></span> <span data-ttu-id="e5dfe-183">Minden egyes szintaxis elem csomópont párjai kezdődik \<maml:name > címkék, amely tartalmazza annak a parancsmagnak a nevét.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-183">Each syntax item node begins with a pair of \<maml:name> tags that include the name of the cmdlet.</span></span>

<span data-ttu-id="e5dfe-184">Az alábbi példában megtalálhatja, amely rendelkezik a szintaxis-elem csomópont két paraméterkészlettel szintaxis csomópont.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-184">The following example includes a syntax node that has syntax item nodes for two parameter sets.</span></span>

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

### <a name="adding-parameters"></a><span data-ttu-id="e5dfe-185">Paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="e5dfe-185">Adding Parameters</span></span>

<span data-ttu-id="e5dfe-186">Minden egyes paraméter, a szintaxis elem csomópont van megadva egy \<parancsparaméter: > címkéket.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-186">Each parameter added to the syntax item node is specified within a pair of \<command:parameter> tags.</span></span> <span data-ttu-id="e5dfe-187">Egy kulcspárra van szüksége \<parancsparaméter: > címke szerepel a paraméterkészletet, a következő általános paramétereket, amelyek a Windows PowerShell által biztosított kivételével minden paraméter?.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-187">You need a pair of \<command:parameter> tags for each parameter included in the parameter set, with the exception of the common parameters that are provided by Windows PowerShell?.</span></span>

<span data-ttu-id="e5dfe-188">A nyitó attribútumai \<parancsparaméter: > címke határozza meg, hogyan jelenjen meg a paraméter szintaxisdiagramja.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-188">The attributes of the opening \<command:parameter> tag determine how the parameter appears in the syntax diagram.</span></span> <span data-ttu-id="e5dfe-189">A paraméter-attribútumok kapcsolatos információkért lásd: [paraméter-attribútumok](#Parameter-Attributes).</span><span class="sxs-lookup"><span data-stu-id="e5dfe-189">For information on parameter attributes, see [Parameter Attributes](#Parameter-Attributes).</span></span>

> [!NOTE]
> <span data-ttu-id="e5dfe-190">A \<parancsparaméter: > címke támogatja a gyermekelem \<maml:description > tartalmú soha nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-190">The \<command:parameter> tag supports a child element \<maml:description> whose content is never displayed.</span></span> <span data-ttu-id="e5dfe-191">A paraméterek leírásait meg van adva a paraméter csomópont XML-kód.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-191">The parameter descriptions are specified in the parameter node of the XML.</span></span> <span data-ttu-id="e5dfe-192">A szintaxis elem található információk közötti inkonzisztencia elkerülése érdekében bodes és a paraméter csomópont, hagyja ki a (\<maml:description >, vagy hagyja üresen.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-192">To avoid inconsistencies between the information in the syntax item bodes and the parameter node, omit the (\<maml:description> or leave it empty.</span></span>

<span data-ttu-id="e5dfe-193">Az alábbi példa egy két paraméterrel rendelkező paraméter szintaxisa elem csomópont tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="e5dfe-193">The following example includes a syntax item node for a parameter set with two parameters.</span></span>

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
