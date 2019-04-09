---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Új objektum .NET- és COM-objektumok létrehozása
ms.assetid: 2057b113-efeb-465e-8b44-da2f20dbf603
ms.openlocfilehash: ef8215303aacd90536d3c2ae57bc3629e202f318
ms.sourcegitcommit: 806cf87488b80800b9f50a8af286e8379519a034
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2019
ms.locfileid: "59293367"
---
# <a name="creating-net-and-com-objects-new-object"></a><span data-ttu-id="88244-103">.NET- és COM-objektumok (új objektum) létrehozása</span><span class="sxs-lookup"><span data-stu-id="88244-103">Creating .NET and COM Objects (New-Object)</span></span>

<span data-ttu-id="88244-104">Nincsenek a .NET-keretrendszer és a COM-felületek, amelyek lehetővé teszik, hogy hány rendszer felügyeleti feladatainak végrehajtására szoftverösszetevőket.</span><span class="sxs-lookup"><span data-stu-id="88244-104">There are software components with .NET Framework and COM interfaces that enable you to perform many system administration tasks.</span></span> <span data-ttu-id="88244-105">Windows PowerShell lehetővé teszi, hogy ezek az összetevők használatát, így Ön nem korlátozódik a parancsmagokkal végrehajtható feladatokat.</span><span class="sxs-lookup"><span data-stu-id="88244-105">Windows PowerShell lets you use these components, so you are not limited to the tasks that can be performed by using cmdlets.</span></span> <span data-ttu-id="88244-106">Távoli számítógépek számos, az eredeti kiadásban a Windows PowerShell parancsmagjai nem működnek.</span><span class="sxs-lookup"><span data-stu-id="88244-106">Many of the cmdlets in the initial release of Windows PowerShell do not work against remote computers.</span></span> <span data-ttu-id="88244-107">Bemutatjuk, hogyan kaphat ezt a korlátozást úgy, ha az Eseménynapló kezelése a .NET-keretrendszer használatával **System.Diagnostics.EventLog** osztályban közvetlenül a Windows Powershellből.</span><span class="sxs-lookup"><span data-stu-id="88244-107">We will demonstrate how to get around this limitation when managing event logs by using the .NET Framework **System.Diagnostics.EventLog** class directly from Windows PowerShell.</span></span>

## <a name="using-new-object-for-event-log-access"></a><span data-ttu-id="88244-108">Új objektum használatával a Eseménynapló hozzáférés érdekében</span><span class="sxs-lookup"><span data-stu-id="88244-108">Using New-Object for Event Log Access</span></span>

<span data-ttu-id="88244-109">A .NET-keretrendszer osztálytár tartalmaz egy osztályt **System.Diagnostics.EventLog** , amely az eseménynaplókat kezelésére használható.</span><span class="sxs-lookup"><span data-stu-id="88244-109">The .NET Framework Class Library includes a class named **System.Diagnostics.EventLog** that can be used to manage event logs.</span></span> <span data-ttu-id="88244-110">Létrehozhat egy új példányát egy .NET-keretrendszer osztály használatával a **New-Object** parancsmagot a **TypeName** paraméter.</span><span class="sxs-lookup"><span data-stu-id="88244-110">You can create a new instance of a .NET Framework class by using the **New-Object** cmdlet with the **TypeName** parameter.</span></span> <span data-ttu-id="88244-111">Például a következő parancs létrehoz egy eseménynapló-hivatkozást:</span><span class="sxs-lookup"><span data-stu-id="88244-111">For example, the following command creates an event log reference:</span></span>

```
PS> New-Object -TypeName System.Diagnostics.EventLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
```

<span data-ttu-id="88244-112">Bár a paranccsal létrehozta az EventLog osztály egy példányát, a példány nem tartalmaz adatokat.</span><span class="sxs-lookup"><span data-stu-id="88244-112">Although the command has created an instance of the EventLog class, the instance does not include any data.</span></span> <span data-ttu-id="88244-113">Ennek oka az, hogy nem adott meg egy adott eseménynaplónál.</span><span class="sxs-lookup"><span data-stu-id="88244-113">That is because we did not specify a particular event log.</span></span> <span data-ttu-id="88244-114">Hogyan kap egy valódi Eseménynapló?</span><span class="sxs-lookup"><span data-stu-id="88244-114">How do you get a real event log?</span></span>

### <a name="using-constructors-with-new-object"></a><span data-ttu-id="88244-115">Új objektum konstruktorok használata</span><span class="sxs-lookup"><span data-stu-id="88244-115">Using Constructors with New-Object</span></span>

<span data-ttu-id="88244-116">Tekintse meg az adott eseménynaplóból, adja meg a napló nevét kell.</span><span class="sxs-lookup"><span data-stu-id="88244-116">To refer to a specific event log, you need to specify the name of the log.</span></span> <span data-ttu-id="88244-117">**Új objektum** rendelkezik egy **ArgumentList** paraméter.</span><span class="sxs-lookup"><span data-stu-id="88244-117">**New-Object** has an **ArgumentList** parameter.</span></span> <span data-ttu-id="88244-118">Ez a paraméter értékeként átadhatja az argumentumok használja az objektumot egy speciális indítási módját.</span><span class="sxs-lookup"><span data-stu-id="88244-118">The arguments you pass as values to this parameter are used by a special startup method of the object.</span></span> <span data-ttu-id="88244-119">A metódus lehívásra kerül egy *konstruktor* , mert az objektum létrehozásához használatos.</span><span class="sxs-lookup"><span data-stu-id="88244-119">The method is called a *constructor* because it is used to construct the object.</span></span> <span data-ttu-id="88244-120">Ha például egy hivatkozást a napló lekéréséhez karakterláncot adja meg "Alkalmazás" argumentumaként:</span><span class="sxs-lookup"><span data-stu-id="88244-120">For example, to get a reference to the Application log, you specify the string 'Application' as an argument:</span></span>

```
PS> New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application

Max(K) Retain OverflowAction        Entries Name
------ ------ --------------        ------- ----
16,384      7 OverwriteOlder          2,160 Application
```

> [!NOTE]
> <span data-ttu-id="88244-121">Mivel a rendszer névtér a .NET Framework core osztályok többsége található, Windows PowerShell automatikusan megpróbálja a rendszer névtér Ha nem találja a megadott typename egyezik megadott osztályok kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="88244-121">Since most of the .NET Framework core classes are contained in the System namespace, Windows PowerShell will automatically attempt to find classes you specify in the System namespace if it cannot find a match for the typename you specify.</span></span> <span data-ttu-id="88244-122">Ez azt jelenti, hogy Diagnostics.EventLog System.Diagnostics.EventLog helyett megadhat.</span><span class="sxs-lookup"><span data-stu-id="88244-122">This means that you can specify Diagnostics.EventLog instead of System.Diagnostics.EventLog.</span></span>

### <a name="storing-objects-in-variables"></a><span data-ttu-id="88244-123">Objektumok tárolása változókban</span><span class="sxs-lookup"><span data-stu-id="88244-123">Storing Objects in Variables</span></span>

<span data-ttu-id="88244-124">Előfordulhat, hogy szeretné tárolni a objektumot, egy hivatkozást, így használhatja az aktuális felületen.</span><span class="sxs-lookup"><span data-stu-id="88244-124">You might want to store a reference to an object, so you can use it in the current shell.</span></span> <span data-ttu-id="88244-125">Bár a Windows PowerShell lehetővé teszi folyamatok, a számos tennivalónk szükség változók csökkentését, néha tárolása változókban objektumokra mutató hivatkozásokat megkönnyíti a ezek az objektumok módosítására.</span><span class="sxs-lookup"><span data-stu-id="88244-125">Although Windows PowerShell lets you do a lot of work with pipelines, lessening the need for variables, sometimes storing references to objects in variables makes it more convenient to manipulate those objects.</span></span>

<span data-ttu-id="88244-126">Windows PowerShell segítségével hozhat létre változókat, amelyek lényegében elnevezett objektumokat.</span><span class="sxs-lookup"><span data-stu-id="88244-126">Windows PowerShell lets you create variables that are essentially named objects.</span></span> <span data-ttu-id="88244-127">Bármely érvényes Windows PowerShell-parancs kimenetében tárolható egy változóban.</span><span class="sxs-lookup"><span data-stu-id="88244-127">The output from any valid Windows PowerShell command can be stored in a variable.</span></span> <span data-ttu-id="88244-128">Változó neve mindig a $ kezdődik.</span><span class="sxs-lookup"><span data-stu-id="88244-128">Variable names always begin with $.</span></span> <span data-ttu-id="88244-129">Ha szeretné tárolni az alkalmazás-naplóinak referenciája $AppLog nevű változóba, adja meg a változó, egy egyenlőségjelet követ, és írja be a parancsot az alkalmazás log objektum létrehozásához használt:</span><span class="sxs-lookup"><span data-stu-id="88244-129">If you want to store the Application log reference in a variable named $AppLog, type the name of the variable, followed by an equal sign and then type the command used to create the Application log object:</span></span>

```
PS> $AppLog = New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
```

<span data-ttu-id="88244-130">Ha majd $AppLog, láthatja, hogy a napló tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="88244-130">If you then type $AppLog, you can see that it contains the Application log:</span></span>

```
PS> $AppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
  16,384      7 OverwriteOlder          2,160 Application
```

### <a name="accessing-a-remote-event-log-with-new-object"></a><span data-ttu-id="88244-131">Az új objektum egy távoli Eseménynapló elérése</span><span class="sxs-lookup"><span data-stu-id="88244-131">Accessing a Remote Event Log with New-Object</span></span>

<span data-ttu-id="88244-132">Az előző szakaszban szereplő parancsokkal a helyi számítógépen; cél a **Get-Eseménynapló** parancsmaggal teheti meg.</span><span class="sxs-lookup"><span data-stu-id="88244-132">The commands used in the preceding section target the local computer; the **Get-EventLog** cmdlet can do that.</span></span> <span data-ttu-id="88244-133">Egy távoli számítógépen a napló eléréséhez kell adnia mind a napló nevét és a számítógép nevét (vagy IP-cím) argumentumként.</span><span class="sxs-lookup"><span data-stu-id="88244-133">To access the Application log on a remote computer, you must supply both the log name and a computer name (or IP address) as arguments.</span></span>

```
PS> $RemoteAppLog = New-Object -TypeName System.Diagnostics.EventLog Application,192.168.1.81
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder            262 Application
```

<span data-ttu-id="88244-134">Most, hogy egy hivatkozást egy eseménynaplót a $RemoteAppLog változó tárolja, milyen feladatokat lehet elvégzése rá?</span><span class="sxs-lookup"><span data-stu-id="88244-134">Now that we have a reference to an event log stored in the $RemoteAppLog variable, what tasks can we perform on it?</span></span>

### <a name="clearing-an-event-log-with-object-methods"></a><span data-ttu-id="88244-135">Az objektum módszerekkel az Eseménynapló tartalmának törlése</span><span class="sxs-lookup"><span data-stu-id="88244-135">Clearing an Event Log with Object Methods</span></span>

<span data-ttu-id="88244-136">Objektumok gyakran rendelkeznek, amely a feladatok elvégzéséhez nem hívható módszerek.</span><span class="sxs-lookup"><span data-stu-id="88244-136">Objects often have methods that can be called to perform tasks.</span></span> <span data-ttu-id="88244-137">Használhat **Get-Member** az objektumhoz társított módszerek megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="88244-137">You can use **Get-Member** to display the methods associated with an object.</span></span> <span data-ttu-id="88244-138">A következő parancsot, és a megadott kimeneti mutatják a módszerek az EventLog osztály:</span><span class="sxs-lookup"><span data-stu-id="88244-138">The following command and selected output show some the methods of the EventLog class:</span></span>

```
PS> $RemoteAppLog | Get-Member -MemberType Method

   TypeName: System.Diagnostics.EventLog

Name                      MemberType Definition
----                      ---------- ----------
...
Clear                     Method     System.Void Clear()
Close                     Method     System.Void Close()
...
GetType                   Method     System.Type GetType()
...
ModifyOverflowPolicy      Method     System.Void ModifyOverflowPolicy(Overfl...
RegisterDisplayName       Method     System.Void RegisterDisplayName(String ...
...
ToString                  Method     System.String ToString()
WriteEntry                Method     System.Void WriteEntry(String message),...
WriteEvent                Method     System.Void WriteEvent(EventInstance in...
```

<span data-ttu-id="88244-139">A **Clear()** metódus segítségével törölje az eseménynaplóban.</span><span class="sxs-lookup"><span data-stu-id="88244-139">The **Clear()** method can be used to clear the event log.</span></span> <span data-ttu-id="88244-140">Metódus hívásakor mindig kell követni a metódus nevét zárójelek közé kell tenni, akkor is, ha a metódus nem szükséges argumentumot.</span><span class="sxs-lookup"><span data-stu-id="88244-140">When calling a method, you must always follow the method name by parentheses, even if the method does not require arguments.</span></span> <span data-ttu-id="88244-141">Ez lehetővé teszi, hogy a Windows PowerShell különböztetni egymástól a metódust, és a egy lehetséges tulajdonság ezzel a névvel.</span><span class="sxs-lookup"><span data-stu-id="88244-141">This lets Windows PowerShell distinguish between the method and a potential property with the same name.</span></span> <span data-ttu-id="88244-142">Írja be a következőt hívja a **egyértelmű** módszer:</span><span class="sxs-lookup"><span data-stu-id="88244-142">Type the following to call the **Clear** method:</span></span>

```
PS> $RemoteAppLog.Clear()
```

<span data-ttu-id="88244-143">Írja be a következő, a napló megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="88244-143">Type the following to display the log.</span></span> <span data-ttu-id="88244-144">Látni fogja, hogy az Eseménynapló törölve lett, és most már a 0 bejegyzés 262 helyett:</span><span class="sxs-lookup"><span data-stu-id="88244-144">You will see that the event log was cleared, and now has 0 entries instead of 262:</span></span>

```
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder              0 Application
```

## <a name="creating-com-objects-with-new-object"></a><span data-ttu-id="88244-145">COM-objektumok létrehozása New-Object</span><span class="sxs-lookup"><span data-stu-id="88244-145">Creating COM Objects with New-Object</span></span>
<span data-ttu-id="88244-146">Használhat **New-Object** Component Object Model (COM) összetevővel működnek.</span><span class="sxs-lookup"><span data-stu-id="88244-146">You can use **New-Object** to work with Component Object Model (COM) components.</span></span> <span data-ttu-id="88244-147">Összetevők tartomány különböző függvénytárak ActiveX például az Internet Explorer telepített alkalmazások a legtöbb esetben a Windows Script Host (WSH) tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="88244-147">Components range from the various libraries included with Windows Script Host (WSH) to ActiveX applications such as Internet Explorer that are installed on most systems.</span></span>

<span data-ttu-id="88244-148">**Új objektum** használja a .NET-keretrendszer modul használata hívható burkolókat COM-objektumok létrehozásához, így ugyanazokkal a korlátozásokkal, amely .NET-keretrendszer COM-objektumok hívásakor.</span><span class="sxs-lookup"><span data-stu-id="88244-148">**New-Object** uses .NET Framework Runtime-Callable Wrappers to create COM objects, so it has the same limitations that .NET Framework does when calling COM objects.</span></span> <span data-ttu-id="88244-149">A COM-objektum létrehozásához adjon meg kell a **ComObject** paraméter a programozott azonosítóval vagy *ProgId* is használni szeretné a COM-osztály.</span><span class="sxs-lookup"><span data-stu-id="88244-149">To create a COM object, you need to specify the **ComObject** parameter with the Programmatic Identifier or *ProgId* of the COM class you want to use.</span></span> <span data-ttu-id="88244-150">A korlátozások COM feltételeit, és amely meghatározza, hogy mi ProgID érhetők el a rendszer a teljes hatásának a megbeszélését a felhasználói útmutató hatókörén kívül esik, de jól ismert objektumok, például WSH környezetben a Windows PowerShell is használható.</span><span class="sxs-lookup"><span data-stu-id="88244-150">A complete discussion of the limitations of COM use and determining what ProgIds are available on a system is beyond the scope of this user's guide, but most well-known objects from environments such as WSH can be used within Windows PowerShell.</span></span>

<span data-ttu-id="88244-151">Ezek ProgID megadásával hozhat létre a WSH objektumok: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, és **Scripting.FileSystemObject**.</span><span class="sxs-lookup"><span data-stu-id="88244-151">You can create the WSH objects by specifying these progids: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, and **Scripting.FileSystemObject**.</span></span> <span data-ttu-id="88244-152">A következő parancsok ezen objektumok létrehozása:</span><span class="sxs-lookup"><span data-stu-id="88244-152">The following commands create these objects:</span></span>

```powershell
New-Object -ComObject WScript.Shell
New-Object -ComObject WScript.Network
New-Object -ComObject Scripting.Dictionary
New-Object -ComObject Scripting.FileSystemObject
```

<span data-ttu-id="88244-153">Bár a legtöbb funkciója az osztályok a Windows PowerShellben érhető el, egyéb módon történik, néhány feladatot, például a parancsikon létrehozása továbbra is leegyszerűsítheti a WHS-osztályokkal is.</span><span class="sxs-lookup"><span data-stu-id="88244-153">Although most of the functionality of these classes is made available in other ways in Windows PowerShell, a few tasks such as shortcut creation are still easier to do using the WSH classes.</span></span>

## <a name="creating-a-desktop-shortcut-with-wscriptshell"></a><span data-ttu-id="88244-154">Asztali parancsikon létrehozása WScript.Shell</span><span class="sxs-lookup"><span data-stu-id="88244-154">Creating a Desktop Shortcut with WScript.Shell</span></span>

<span data-ttu-id="88244-155">Egy COM-objektummal gyorsan elvégezhető feladat parancsikon létrehozása.</span><span class="sxs-lookup"><span data-stu-id="88244-155">One task that can be performed quickly with a COM object is creating a shortcut.</span></span> <span data-ttu-id="88244-156">Tegyük fel, hogy hozzon létre egy parancsikont az asztalon a kezdőmappa mutat a Windows PowerShell környezethez.</span><span class="sxs-lookup"><span data-stu-id="88244-156">Suppose you want to create a shortcut on your desktop that links to the home folder for Windows PowerShell.</span></span> <span data-ttu-id="88244-157">Először hozzon létre egy hivatkozást **WScript.Shell**, amely lesz a nevű változóban tároljuk **$WshShell**:</span><span class="sxs-lookup"><span data-stu-id="88244-157">You first need to create a reference to **WScript.Shell**, which we will store in a variable named **$WshShell**:</span></span>

```powershell
$WshShell = New-Object -ComObject WScript.Shell
```

<span data-ttu-id="88244-158">Get-Member együttműködik a COM-objektumok, így megismerheti az objektum tagjait beírásával:</span><span class="sxs-lookup"><span data-stu-id="88244-158">Get-Member works with COM objects, so you can explore the members of the object by typing:</span></span>

```
PS> $WshShell | Get-Member

   TypeName: System.__ComObject#{41904400-be18-11d3-a28b-00104bd35090}

Name                     MemberType            Definition
----                     ----------            ----------
AppActivate              Method                bool AppActivate (Variant, Va...
CreateShortcut           Method                IDispatch CreateShortcut (str...
...
```

<span data-ttu-id="88244-159">**Get-Member** rendelkezik egy nem kötelező **InputObject** átirányítás helyett segítségével adja meg a bemeneti paraméter **Get-Member**.</span><span class="sxs-lookup"><span data-stu-id="88244-159">**Get-Member** has an optional **InputObject** parameter you can use instead of piping to provide input to **Get-Member**.</span></span> <span data-ttu-id="88244-160">Ugyanaz, ahogy fent látható, ha ehelyett használt a parancs kimenete számíthat **Get-Member - InputObject $WshShell**.</span><span class="sxs-lookup"><span data-stu-id="88244-160">You would get the same output as shown above if you instead used the command **Get-Member -InputObject $WshShell**.</span></span> <span data-ttu-id="88244-161">Ha **InputObject**, azonos módon kezeli az argumentuma egyetlen elemként.</span><span class="sxs-lookup"><span data-stu-id="88244-161">If you use **InputObject**, it treats its argument as a single item.</span></span> <span data-ttu-id="88244-162">Ez azt jelenti, hogy ha több objektumot egy változóban **Get-Member** objektumok tömbjeként kezeli őket.</span><span class="sxs-lookup"><span data-stu-id="88244-162">This means that if you have several objects in a variable, **Get-Member** treats them as an array of objects.</span></span> <span data-ttu-id="88244-163">Például:</span><span class="sxs-lookup"><span data-stu-id="88244-163">For example:</span></span>

```
PS> $a = 1,2,"three"
PS> Get-Member -InputObject $a
TypeName: System.Object[]
Name               MemberType    Definition
----               ----------    ----------
Count              AliasProperty Count = Length
...
```

<span data-ttu-id="88244-164">A **WScript.Shell CreateShortcut** metódus egyetlen argumentumot, hozhat létre a helyi fájl elérési útját fogadja.</span><span class="sxs-lookup"><span data-stu-id="88244-164">The **WScript.Shell CreateShortcut** method accepts a single argument, the path to the shortcut file to create.</span></span> <span data-ttu-id="88244-165">Azt írja be a teljes elérési útját az asztalon, de egy egyszerűbb.</span><span class="sxs-lookup"><span data-stu-id="88244-165">We could type in the full path to the desktop, but there is an easier way.</span></span> <span data-ttu-id="88244-166">Az asztal általában képviseli egy otthoni a mappába, az aktuális felhasználó asztali nevű mappát.</span><span class="sxs-lookup"><span data-stu-id="88244-166">The desktop is normally represented by a folder named Desktop inside the home folder of the current user.</span></span> <span data-ttu-id="88244-167">Windows PowerShell rendelkezik egy változó **$Home** , amely tartalmazza a mappa elérési útját.</span><span class="sxs-lookup"><span data-stu-id="88244-167">Windows PowerShell has a variable **$Home** that contains the path to this folder.</span></span> <span data-ttu-id="88244-168">Azt adja meg a mappa elérési útját az otthoni változó használatával, és adja az asztali mappa nevét és a parancsikon létrehozása beírásával nevét:</span><span class="sxs-lookup"><span data-stu-id="88244-168">We can specify the path to the home folder by using this variable, and then add the name of the Desktop folder and the name for the shortcut to create by typing:</span></span>

```powershell
$lnk = $WshShell.CreateShortcut("$Home\Desktop\PSHome.lnk")
```

<span data-ttu-id="88244-169">Hogy néz ki egy változónevet belül idézőjelek használata esetén a Windows PowerShell próbál helyettesítse be a megfelelő érték.</span><span class="sxs-lookup"><span data-stu-id="88244-169">When you use something that looks like a variable name inside double-quotes, Windows PowerShell tries to substitute a matching value.</span></span> <span data-ttu-id="88244-170">Egyszeres idézőjelet használja, ha Windows PowerShell próbáljon helyettesítse be a változó értékét.</span><span class="sxs-lookup"><span data-stu-id="88244-170">If you use single-quotes, Windows PowerShell does not try to substitute the variable value.</span></span> <span data-ttu-id="88244-171">Próbáljon meg például írja be a következő parancsokat:</span><span class="sxs-lookup"><span data-stu-id="88244-171">For example, try typing the following commands:</span></span>

```
PS> "$Home\Desktop\PSHome.lnk"
C:\Documents and Settings\aka\Desktop\PSHome.lnk
PS> '$Home\Desktop\PSHome.lnk'
$Home\Desktop\PSHome.lnk
```

<span data-ttu-id="88244-172">Most megvalósult nevű változó **$lnk** , amely egy új helyi hivatkozást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="88244-172">We now have a variable named **$lnk** that contains a new shortcut reference.</span></span> <span data-ttu-id="88244-173">Ha meg szeretné tekinteni a tagjai, adatcsatornán keresztül is, hogy **Get-Member**.</span><span class="sxs-lookup"><span data-stu-id="88244-173">If you want to see its members, you can pipe it to **Get-Member**.</span></span> <span data-ttu-id="88244-174">Az alábbi kimenetben látható kell használnia a parancsikon létrehozása befejeződik a tagok:</span><span class="sxs-lookup"><span data-stu-id="88244-174">The output below shows the members we need to use to finish creating our shortcut:</span></span>

```
PS> $lnk | Get-Member
TypeName: System.__ComObject#{f935dc23-1cf0-11d0-adb9-00c04fd58a0b}
Name             MemberType   Definition
----             ----------   ----------
...
Save             Method       void Save ()
...
TargetPath       Property     string TargetPath () {get} {set}
```

<span data-ttu-id="88244-175">Adja meg kell a **TargetPath**, vagyis az alkalmazás mappájában, a Windows PowerShell környezethez, majd mentse a helyi **$lnk** meghívásával a **mentése** metódust.</span><span class="sxs-lookup"><span data-stu-id="88244-175">We need to specify the **TargetPath**, which is the application folder for Windows PowerShell, and then save the shortcut **$lnk** by calling the **Save** method.</span></span> <span data-ttu-id="88244-176">A változó tárolja a Windows PowerShell alkalmazást mappa elérési útjának **$PSHome**, így azt ehhez írja be:</span><span class="sxs-lookup"><span data-stu-id="88244-176">The Windows PowerShell application folder path is stored in the variable **$PSHome**, so we can do this by typing:</span></span>

```powershell
$lnk.TargetPath = $PSHome
$lnk.Save()
```

## <a name="using-internet-explorer-from-windows-powershell"></a><span data-ttu-id="88244-177">Az Internet Explorer a Windows PowerShell használatával</span><span class="sxs-lookup"><span data-stu-id="88244-177">Using Internet Explorer from Windows PowerShell</span></span>

<span data-ttu-id="88244-178">Számos alkalmazás (beleértve a Microsoft Office-alkalmazások és az Internet Explorer család) automatizálható a modulu COM.</span><span class="sxs-lookup"><span data-stu-id="88244-178">Many applications (including the Microsoft Office family of applications and Internet Explorer) can be automated by using COM.</span></span> <span data-ttu-id="88244-179">Az Internet Explorer mutatja be néhány tipikus technikák és COM-alapú alkalmazások használata során felmerülő kérdésekkel.</span><span class="sxs-lookup"><span data-stu-id="88244-179">Internet Explorer illustrates some of the typical techniques and issues involved in working with COM-based applications.</span></span>

<span data-ttu-id="88244-180">Az Internet Explorer példányt hoz létre az Internet Explorer programazonosítója megadásával **InternetExplorer.Application**:</span><span class="sxs-lookup"><span data-stu-id="88244-180">You create an Internet Explorer instance by specifying the Internet Explorer ProgId, **InternetExplorer.Application**:</span></span>

```powershell
$ie = New-Object -ComObject InternetExplorer.Application
```

<span data-ttu-id="88244-181">Ez a parancs elindítja az Internet Explorer, de nem teszi azt láthatóvá.</span><span class="sxs-lookup"><span data-stu-id="88244-181">This command starts Internet Explorer, but does not make it visible.</span></span> <span data-ttu-id="88244-182">Írja be a Get-Process, láthatja, hogy fut-e egy iexplore nevű folyamatot.</span><span class="sxs-lookup"><span data-stu-id="88244-182">If you type Get-Process, you can see that a process named iexplore is running.</span></span> <span data-ttu-id="88244-183">Sőt Ha kilép a Windows PowerShell, a folyamat továbbra is futtassa.</span><span class="sxs-lookup"><span data-stu-id="88244-183">In fact, if you exit Windows PowerShell, the process will continue to run.</span></span> <span data-ttu-id="88244-184">Indítsa újra a számítógépet vagy egy eszköz, például a Feladatkezelő segítségével az iexplore folyamatot kell.</span><span class="sxs-lookup"><span data-stu-id="88244-184">You must reboot the computer or use a tool like Task Manager to end the iexplore process.</span></span>

> [!NOTE]
> <span data-ttu-id="88244-185">COM-objektumok, amely külön folyamatként start gyakori nevén *ActiveX végrehajtható fájlok*, előfordulhat, hogy, vagy előfordulhat, hogy nem jelennek meg a felhasználói felület ablak indításkor.</span><span class="sxs-lookup"><span data-stu-id="88244-185">COM objects that start as separate processes, commonly called *ActiveX executables*, may or may not display a user interface window when they start up.</span></span> <span data-ttu-id="88244-186">Ha azok időszak létrehozása, de nem teszi azt láthatóvá, például az Internet Explorer, a Windows asztali általában áthelyezi a fókuszt, és meg kell győződnie, az ablakban látható kommunikálhat.</span><span class="sxs-lookup"><span data-stu-id="88244-186">If they create a window but do not make it visible, like Internet Explorer, the focus will generally move to the Windows desktop and you must make the window visible to interact with it.</span></span>

<span data-ttu-id="88244-187">Beírásával **$ie |} Get-Member**, tekintse meg a tulajdonságokat és metódusokat az Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="88244-187">By typing **$ie | Get-Member**, you can view properties and methods for Internet Explorer.</span></span> <span data-ttu-id="88244-188">Az Internet Explorer ablak jelenik meg, állítsa be a látható tulajdonság $true beírásával:</span><span class="sxs-lookup"><span data-stu-id="88244-188">To see the Internet Explorer window, set the Visible property to $true by typing:</span></span>

```powershell
$ie.Visible = $true
```

<span data-ttu-id="88244-189">Ezután válthat egy adott webes címre a Navigate módszer használatával:</span><span class="sxs-lookup"><span data-stu-id="88244-189">You can then navigate to a specific Web address by using the Navigate method:</span></span>

```powershell
$ie.Navigate("http://www.microsoft.com/technet/scriptcenter/default.mspx")
```

<span data-ttu-id="88244-190">Más tagjai az Internet Explorer hálózatiobjektum-modellt használja, lehetőség szöveg tartalmat lekérjen a weblapot.</span><span class="sxs-lookup"><span data-stu-id="88244-190">Using other members of the Internet Explorer object model, it is possible to retrieve text content from the Web page.</span></span> <span data-ttu-id="88244-191">A következő parancsot a HTML-szöveg jelenik meg az aktuális weblap törzse:</span><span class="sxs-lookup"><span data-stu-id="88244-191">The following command will display the HTML text in the body of the current Web page:</span></span>

```powershell
$ie.Document.Body.InnerText
```

<span data-ttu-id="88244-192">Zárja be az Internet Explorer hozzáférését a Powershellen belülről, hívja meg a Quit() módszert:</span><span class="sxs-lookup"><span data-stu-id="88244-192">To close Internet Explorer from within PowerShell, call its Quit() method:</span></span>

```powershell
$ie.Quit()
```

<span data-ttu-id="88244-193">Ezzel kikényszeríti azt a gombra kattintva zárja be.</span><span class="sxs-lookup"><span data-stu-id="88244-193">This will force it to close.</span></span> <span data-ttu-id="88244-194">Az ie változó $ már nem tartalmaz érvényes hivatkozást, annak ellenére, hogy továbbra is megjelenik egy COM-objektummal kell.</span><span class="sxs-lookup"><span data-stu-id="88244-194">The $ie variable no longer contains a valid reference even though it still appears to be a COM object.</span></span> <span data-ttu-id="88244-195">Ha megpróbálja használni, kap egy automation-hiba:</span><span class="sxs-lookup"><span data-stu-id="88244-195">If you attempt to use it, you will get an automation error:</span></span>

```
PS> $ie | Get-Member
Get-Member : Exception retrieving the string representation for property "Appli
cation" : "The object invoked has disconnected from its clients. (Exception fro
m HRESULT: 0x80010108 (RPC_E_DISCONNECTED))"
At line:1 char:16
+ $ie | Get-Member <<<<
```

<span data-ttu-id="88244-196">Eltávolíthat a fennmaradó hivatkozni tudjon ie $ hasonló parancsot = $null vagy a teljes eltávolításához írja be a változót:</span><span class="sxs-lookup"><span data-stu-id="88244-196">You can either remove the remaining reference with a command like $ie = $null, or completely remove the variable by typing:</span></span>

```powershell
Remove-Variable ie
```

> [!NOTE]
> <span data-ttu-id="88244-197">Nincs nem általános szabvány e ActiveX végrehajtható fájlok lépjen ki, és továbbra is egy hivatkozást eltávolításakor futnak.</span><span class="sxs-lookup"><span data-stu-id="88244-197">There is no common standard for whether ActiveX executables exit or continue to run when you remove a reference to one.</span></span> <span data-ttu-id="88244-198">Attól függően, például hogy jelenik meg az alkalmazás, egy dokumentum szerkesztett fut-e, és még Windows PowerShell továbbra is fut-e körülmények között az alkalmazás is, vagy előfordulhat, hogy nincs Kilépés.</span><span class="sxs-lookup"><span data-stu-id="88244-198">Depending on circumstances such as whether the application is visible, whether an edited document is running in it, and even whether Windows PowerShell is still running, the application may or may not exit.</span></span> <span data-ttu-id="88244-199">Ebből kifolyólag a végrehajtható, a Windows PowerShellben használni kívánt minden egyes ActiveX lezárást viselkedés kell tesztelni.</span><span class="sxs-lookup"><span data-stu-id="88244-199">For this reason, you should test termination behavior for each ActiveX executable you want to use in Windows PowerShell.</span></span>

## <a name="getting-warnings-about-net-framework-wrapped-com-objects"></a><span data-ttu-id="88244-200">Bevezetés a .NET-keretrendszer csomagolt COM-objektumok kapcsolatos figyelmeztetések</span><span class="sxs-lookup"><span data-stu-id="88244-200">Getting Warnings About .NET Framework-Wrapped COM Objects</span></span>

<span data-ttu-id="88244-201">Bizonyos esetekben a COM-objektum lehet egy kapcsolódó .NET-keretrendszer *futásidejű meghívható* vagy RCW, és ezzel által használt **New-Object**.</span><span class="sxs-lookup"><span data-stu-id="88244-201">In some cases, a COM object might have an associated .NET Framework *Runtime-Callable Wrapper* or RCW, and this will be used by **New-Object**.</span></span> <span data-ttu-id="88244-202">Mivel a RCW viselkedését eltérhet a szokásos COM-objektum viselkedését **New-Object** rendelkezik egy **Strict** figyelmeztetni RCW hozzáférés paraméter.</span><span class="sxs-lookup"><span data-stu-id="88244-202">Since the behavior of the RCW may be different from the behavior of the normal COM object, **New-Object** has a **Strict** parameter to warn you about RCW access.</span></span> <span data-ttu-id="88244-203">Ha megad a **Strict** paraméter és majd hozzon létre egy COM-objektum, amely egy RCW használja, megjelenik egy figyelmeztető üzenet:</span><span class="sxs-lookup"><span data-stu-id="88244-203">If you specify the **Strict** parameter and then create a COM object that uses an RCW, you get a warning message:</span></span>

```
PS> $xl = New-Object -ComObject Excel.Application -Strict
New-Object : The object written to the pipeline is an instance of the type "Mic
rosoft.Office.Interop.Excel.ApplicationClass" from the component's primary inte
rop assembly. If this type exposes different members than the IDispatch members
, scripts written to work with this object might not work if the primary intero
p assembly is not installed.
At line:1 char:17
+ $xl = New-Object  <<<< -ComObject Excel.Application -Strict
```

<span data-ttu-id="88244-204">Bár az objektum még mindig létrejön, figyelmeztetést kap, hogy azt ne legyen egy standard COM-objektummal.</span><span class="sxs-lookup"><span data-stu-id="88244-204">Although the object is still created, you are warned that it is not a standard COM object.</span></span>