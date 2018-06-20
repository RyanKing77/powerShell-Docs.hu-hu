---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Új objektum .NET és a COM-objektumok létrehozása
ms.assetid: 2057b113-efeb-465e-8b44-da2f20dbf603
ms.openlocfilehash: 1ffd8d4afa419ec0c24321e44aa4a2f41a9bee44
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953388"
---
# <a name="creating-net-and-com-objects-new-object"></a><span data-ttu-id="2673e-103">.NET és a COM-objektumok (új objektum) létrehozása</span><span class="sxs-lookup"><span data-stu-id="2673e-103">Creating .NET and COM Objects (New-Object)</span></span>

<span data-ttu-id="2673e-104">Nincsenek szoftverösszetevőket. a .NET-keretrendszer és a COM-felületek, amelyek lehetővé teszik több rendszer felügyeleti feladatok elvégzéséhez.</span><span class="sxs-lookup"><span data-stu-id="2673e-104">There are software components with .NET Framework and COM interfaces that enable you to perform many system administration tasks.</span></span> <span data-ttu-id="2673e-105">A Windows PowerShell lehetővé teszi ezeket az összetevőket, így a felhasználó a parancsmagokkal végrehajtható feladatok korlátozott.</span><span class="sxs-lookup"><span data-stu-id="2673e-105">Windows PowerShell lets you use these components, so you are not limited to the tasks that can be performed by using cmdlets.</span></span> <span data-ttu-id="2673e-106">A parancsmagok a Windows PowerShell eredeti kiadását számos nem működik, távoli számítógépekről.</span><span class="sxs-lookup"><span data-stu-id="2673e-106">Many of the cmdlets in the initial release of Windows PowerShell do not work against remote computers.</span></span> <span data-ttu-id="2673e-107">Ismerteti az elkerülése érdekében ez a korlátozás eseménynaplók kezeléséhez, a .NET-keretrendszer használatával **System.Diagnostics.EventLog** közvetlenül a Windows PowerShell osztály.</span><span class="sxs-lookup"><span data-stu-id="2673e-107">We will demonstrate how to get around this limitation when managing event logs by using the .NET Framework **System.Diagnostics.EventLog** class directly from Windows PowerShell.</span></span>

### <a name="using-new-object-for-event-log-access"></a><span data-ttu-id="2673e-108">Új objektum használatát az Eseménynapló hozzáférésének</span><span class="sxs-lookup"><span data-stu-id="2673e-108">Using New-Object for Event Log Access</span></span>

<span data-ttu-id="2673e-109">A .NET-keretrendszer Class Library tartalmaz egy osztályt **System.Diagnostics.EventLog** , amely eseménynaplók kezelésére használható.</span><span class="sxs-lookup"><span data-stu-id="2673e-109">The .NET Framework Class Library includes a class named **System.Diagnostics.EventLog** that can be used to manage event logs.</span></span> <span data-ttu-id="2673e-110">A .NET-keretrendszer osztály új példánya segítségével létrehozható a **New-Object** parancsmagot a **TypeName** paraméter.</span><span class="sxs-lookup"><span data-stu-id="2673e-110">You can create a new instance of a .NET Framework class by using the **New-Object** cmdlet with the **TypeName** parameter.</span></span> <span data-ttu-id="2673e-111">Például a következő parancs létrehoz egy eseménynapló-hivatkozást:</span><span class="sxs-lookup"><span data-stu-id="2673e-111">For example, the following command creates an event log reference:</span></span>

```
PS> New-Object -TypeName System.Diagnostics.EventLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
```

<span data-ttu-id="2673e-112">Bár a parancs hozott létre az EventLog osztály egy példányát, a példány nem tartalmaz adatokat.</span><span class="sxs-lookup"><span data-stu-id="2673e-112">Although the command has created an instance of the EventLog class, the instance does not include any data.</span></span> <span data-ttu-id="2673e-113">Ennek oka az, hogy nem adott meg adott eseménynaplónál.</span><span class="sxs-lookup"><span data-stu-id="2673e-113">That is because we did not specify a particular event log.</span></span> <span data-ttu-id="2673e-114">Hogyan be egy valós eseménynaplóba?</span><span class="sxs-lookup"><span data-stu-id="2673e-114">How do you get a real event log?</span></span>

#### <a name="using-constructors-with-new-object"></a><span data-ttu-id="2673e-115">Új objektum konstruktorok használata</span><span class="sxs-lookup"><span data-stu-id="2673e-115">Using Constructors with New-Object</span></span>

<span data-ttu-id="2673e-116">Egy adott eseménynaplóból hivatkozunk, meg kell adnia a napló nevét.</span><span class="sxs-lookup"><span data-stu-id="2673e-116">To refer to a specific event log, you need to specify the name of the log.</span></span> <span data-ttu-id="2673e-117">**Új objektum** rendelkezik egy **ArgumentList** paraméter.</span><span class="sxs-lookup"><span data-stu-id="2673e-117">**New-Object** has an **ArgumentList** parameter.</span></span> <span data-ttu-id="2673e-118">Az argumentumok át értékként ennek a paraméternek egy különleges indítási metódus az objektum által használt.</span><span class="sxs-lookup"><span data-stu-id="2673e-118">The arguments you pass as values to this parameter are used by a special startup method of the object.</span></span> <span data-ttu-id="2673e-119">A metódus lehívásra kerül egy *konstruktor* mert létrehozni az objektumot használja.</span><span class="sxs-lookup"><span data-stu-id="2673e-119">The method is called a *constructor* because it is used to construct the object.</span></span> <span data-ttu-id="2673e-120">Ahhoz, hogy az alkalmazásnaplóba hivatkozást, akkor adja meg például az "Alkalmazás" karakterlánc argumentumként:</span><span class="sxs-lookup"><span data-stu-id="2673e-120">For example, to get a reference to the Application log, you specify the string 'Application' as an argument:</span></span>

```
PS> New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application

Max(K) Retain OverflowAction        Entries Name
------ ------ --------------        ------- ----
16,384      7 OverwriteOlder          2,160 Application
```

> [!NOTE]
> <span data-ttu-id="2673e-121">A .NET Framework core osztályok többsége tartalmazza a rendszer egyik névtere, mivel Windows PowerShell automatikusan kísérli meg meghatározni a rendszer egyik névtere, ha nem találja a megadott typename megfelelő osztályok kereséséhez.</span><span class="sxs-lookup"><span data-stu-id="2673e-121">Since most of the .NET Framework core classes are contained in the System namespace, Windows PowerShell will automatically attempt to find classes you specify in the System namespace if it cannot find a match for the typename you specify.</span></span> <span data-ttu-id="2673e-122">Ez azt jelenti, hogy Diagnostics.EventLog helyett System.Diagnostics.EventLog is megadhat.</span><span class="sxs-lookup"><span data-stu-id="2673e-122">This means that you can specify Diagnostics.EventLog instead of System.Diagnostics.EventLog.</span></span>

#### <a name="storing-objects-in-variables"></a><span data-ttu-id="2673e-123">Objektumok tárolása változók</span><span class="sxs-lookup"><span data-stu-id="2673e-123">Storing Objects in Variables</span></span>

<span data-ttu-id="2673e-124">Előfordulhat, hogy szeretne tárolni egy objektumra mutató hivatkozás, hogy használhassa az aktuális rendszerhéjban.</span><span class="sxs-lookup"><span data-stu-id="2673e-124">You might want to store a reference to an object, so you can use it in the current shell.</span></span> <span data-ttu-id="2673e-125">Bár a Windows PowerShell lehetővé teszi nagy mennyiségű munkahelyi kimenetátirányítási mechanizmusát használó műveletekről, a változók szükségességét csökkentését, változók néha tárolni objektumokra való hivatkozások megkönnyíti a kezelheti azokat az objektumokat.</span><span class="sxs-lookup"><span data-stu-id="2673e-125">Although Windows PowerShell lets you do a lot of work with pipelines, lessening the need for variables, sometimes storing references to objects in variables makes it more convenient to manipulate those objects.</span></span>

<span data-ttu-id="2673e-126">A Windows PowerShell lehetővé teszi objektumok lényegében nevű változókat létrehozni.</span><span class="sxs-lookup"><span data-stu-id="2673e-126">Windows PowerShell lets you create variables that are essentially named objects.</span></span> <span data-ttu-id="2673e-127">Bármilyen érvényes Windows PowerShell-parancs kimenetében tárolható egy változóban.</span><span class="sxs-lookup"><span data-stu-id="2673e-127">The output from any valid Windows PowerShell command can be stored in a variable.</span></span> <span data-ttu-id="2673e-128">Változónevek kezdő $ mindig.</span><span class="sxs-lookup"><span data-stu-id="2673e-128">Variable names always begin with $.</span></span> <span data-ttu-id="2673e-129">Ha azt szeretné, hogy az alkalmazás naplózása tárolható egy változóban nevű $AppLog, írja be a változó egy egyenlőségjellel követni, és írja be a parancsot az alkalmazási napló objektum létrehozásához használt:</span><span class="sxs-lookup"><span data-stu-id="2673e-129">If you want to store the Application log reference in a variable named $AppLog, type the name of the variable, followed by an equal sign and then type the command used to create the Application log object:</span></span>

```
PS> $AppLog = New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
```

<span data-ttu-id="2673e-130">Ha majd $AppLog, láthatja, hogy az tartalmazza-e az alkalmazásnaplóba:</span><span class="sxs-lookup"><span data-stu-id="2673e-130">If you then type $AppLog, you can see that it contains the Application log:</span></span>

```
PS> $AppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
  16,384      7 OverwriteOlder          2,160 Application
```

#### <a name="accessing-a-remote-event-log-with-new-object"></a><span data-ttu-id="2673e-131">Új objektum a Távoli Eseménynapló elérése</span><span class="sxs-lookup"><span data-stu-id="2673e-131">Accessing a Remote Event Log with New-Object</span></span>

<span data-ttu-id="2673e-132">Az előző szakaszban leírt használt parancsok megcélozni a helyi számítógépen; a **Get-eseménynaplóban** parancsmaggal teheti meg.</span><span class="sxs-lookup"><span data-stu-id="2673e-132">The commands used in the preceding section target the local computer; the **Get-EventLog** cmdlet can do that.</span></span> <span data-ttu-id="2673e-133">Az alkalmazásnaplóba egy távoli számítógépen szeretne használni, adjon meg mind a napló nevét és a számítógép nevét (vagy IP-cím) argumentumként.</span><span class="sxs-lookup"><span data-stu-id="2673e-133">To access the Application log on a remote computer, you must supply both the log name and a computer name (or IP address) as arguments.</span></span>

```
PS> $RemoteAppLog = New-Object -TypeName System.Diagnostics.EventLog Application,192.168.1.81
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder            262 Application
```

<span data-ttu-id="2673e-134">Most, hogy egy eseménynapló a $RemoteAppLog változó tárolja egy hivatkozást, milyen feladatokat lehet végezzük rajta?</span><span class="sxs-lookup"><span data-stu-id="2673e-134">Now that we have a reference to an event log stored in the $RemoteAppLog variable, what tasks can we perform on it?</span></span>

#### <a name="clearing-an-event-log-with-object-methods"></a><span data-ttu-id="2673e-135">Egy objektum metódusával Eseménynapló tartalmának törlése</span><span class="sxs-lookup"><span data-stu-id="2673e-135">Clearing an Event Log with Object Methods</span></span>

<span data-ttu-id="2673e-136">Az objektumok gyakran lehet módszereket, amelyek a feladatok elvégzéséhez hívható.</span><span class="sxs-lookup"><span data-stu-id="2673e-136">Objects often have methods that can be called to perform tasks.</span></span> <span data-ttu-id="2673e-137">Használhat **Get-tag** társított módszerek megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="2673e-137">You can use **Get-Member** to display the methods associated with an object.</span></span> <span data-ttu-id="2673e-138">A következő parancsot, és a megadott kimeneti megjelenítése néhány EventLog osztály módszerek:</span><span class="sxs-lookup"><span data-stu-id="2673e-138">The following command and selected output show some the methods of the EventLog class:</span></span>

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

<span data-ttu-id="2673e-139">A **Clear()** módszer segítségével törölje az eseménynaplóban talál.</span><span class="sxs-lookup"><span data-stu-id="2673e-139">The **Clear()** method can be used to clear the event log.</span></span> <span data-ttu-id="2673e-140">A metódus hívásakor mindig kövesse a metódus nevét zárójelek, akkor is, ha a metódus nem igényel argumentumot.</span><span class="sxs-lookup"><span data-stu-id="2673e-140">When calling a method, you must always follow the method name by parentheses, even if the method does not require arguments.</span></span> <span data-ttu-id="2673e-141">Ez lehetővé teszi, hogy a Windows PowerShell megkülönböztetni a metódus és a potenciális tulajdonság ugyanazzal a névvel.</span><span class="sxs-lookup"><span data-stu-id="2673e-141">This lets Windows PowerShell distinguish between the method and a potential property with the same name.</span></span> <span data-ttu-id="2673e-142">Írja be a következőt hívja a **egyértelmű** módszert:</span><span class="sxs-lookup"><span data-stu-id="2673e-142">Type the following to call the **Clear** method:</span></span>

```
PS> $RemoteAppLog.Clear()
```

<span data-ttu-id="2673e-143">Írja be a következőt a napló megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="2673e-143">Type the following to display the log.</span></span> <span data-ttu-id="2673e-144">Látni fogja, hogy az Eseménynapló lett törölve, és 0 bejegyzések 262 helyett most már rendelkezik:</span><span class="sxs-lookup"><span data-stu-id="2673e-144">You will see that the event log was cleared, and now has 0 entries instead of 262:</span></span>

```
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder              0 Application
```

### <a name="creating-com-objects-with-new-object"></a><span data-ttu-id="2673e-145">Új objektum COM-objektumok létrehozása</span><span class="sxs-lookup"><span data-stu-id="2673e-145">Creating COM Objects with New-Object</span></span>
<span data-ttu-id="2673e-146">Használhat **New-Object** Component Object Model (COM) összetevők együttműködni.</span><span class="sxs-lookup"><span data-stu-id="2673e-146">You can use **New-Object** to work with Component Object Model (COM) components.</span></span> <span data-ttu-id="2673e-147">A különböző könyvtárak része a Windows Script Host (WSH) ActiveX alkalmazások például az Internet Explorer, a legtöbb rendszerre telepített összetevők közé.</span><span class="sxs-lookup"><span data-stu-id="2673e-147">Components range from the various libraries included with Windows Script Host (WSH) to ActiveX applications such as Internet Explorer that are installed on most systems.</span></span>

<span data-ttu-id="2673e-148">**Új objektum** COM-objektumok létrehozása, a .NET-keretrendszer hajtja COM-objektumok meghívásakor ugyanazokkal a korlátozásokkal rendelkezik a .NET-keretrendszer futásidejű hívható burkolók használatával.</span><span class="sxs-lookup"><span data-stu-id="2673e-148">**New-Object** uses .NET Framework Runtime-Callable Wrappers to create COM objects, so it has the same limitations that .NET Framework does when calling COM objects.</span></span> <span data-ttu-id="2673e-149">A COM-objektum létrehozásához meg kell adnia a **ComObject** programozott azonosítóval paraméter vagy *ProgId* a használni kívánt COM-osztály.</span><span class="sxs-lookup"><span data-stu-id="2673e-149">To create a COM object, you need to specify the **ComObject** parameter with the Programmatic Identifier or *ProgId* of the COM class you want to use.</span></span> <span data-ttu-id="2673e-150">A COM használatának és a meghatározása, hogy mi ProgID érhetők el a rendszer korlátainak teljes leírása a felhasználói útmutató túlmutat, de környezetekben WSH például jól ismert objektumok használhatja a Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2673e-150">A complete discussion of the limitations of COM use and determining what ProgIds are available on a system is beyond the scope of this user's guide, but most well-known objects from environments such as WSH can be used within Windows PowerShell.</span></span>

<span data-ttu-id="2673e-151">A WSH objektumok ezek ProgID megadásával hozhat létre: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, és  **Scripting.FileSystemObject**.</span><span class="sxs-lookup"><span data-stu-id="2673e-151">You can create the WSH objects by specifying these progids: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, and **Scripting.FileSystemObject**.</span></span> <span data-ttu-id="2673e-152">A következő parancsok ezen objektumok létrehozása:</span><span class="sxs-lookup"><span data-stu-id="2673e-152">The following commands create these objects:</span></span>

```powershell
New-Object -ComObject WScript.Shell
New-Object -ComObject WScript.Network
New-Object -ComObject Scripting.Dictionary
New-Object -ComObject Scripting.FileSystemObject
```

<span data-ttu-id="2673e-153">Bár a legtöbb ezeket az osztályokat funkciója a Windows PowerShell érhető el, egyéb módon történik, néhány feladatokat, mint a parancsikon létrehozása még könnyebben tegye a WSH osztályokat is.</span><span class="sxs-lookup"><span data-stu-id="2673e-153">Although most of the functionality of these classes is made available in other ways in Windows PowerShell, a few tasks such as shortcut creation are still easier to do using the WSH classes.</span></span>

### <a name="creating-a-desktop-shortcut-with-wscriptshell"></a><span data-ttu-id="2673e-154">A parancsikon létrehozása WScript.Shell</span><span class="sxs-lookup"><span data-stu-id="2673e-154">Creating a Desktop Shortcut with WScript.Shell</span></span>

<span data-ttu-id="2673e-155">Egy COM-objektum gyorsan elvégezhető feladat hoz létre egy parancsikont.</span><span class="sxs-lookup"><span data-stu-id="2673e-155">One task that can be performed quickly with a COM object is creating a shortcut.</span></span> <span data-ttu-id="2673e-156">Tegyük fel, hozzon létre egy parancsikont az asztalon a kezdőmappa mutató Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2673e-156">Suppose you want to create a shortcut on your desktop that links to the home folder for Windows PowerShell.</span></span> <span data-ttu-id="2673e-157">Először hozzon létre egy hivatkozást **WScript.Shell**, amely nevű változóban tároljuk fog **$WshShell**:</span><span class="sxs-lookup"><span data-stu-id="2673e-157">You first need to create a reference to **WScript.Shell**, which we will store in a variable named **$WshShell**:</span></span>

```powershell
$WshShell = New-Object -ComObject WScript.Shell
```

<span data-ttu-id="2673e-158">Get-tag együttműködik a COM-objektumok, így megismerheti az objektum tagjait, írja be:</span><span class="sxs-lookup"><span data-stu-id="2673e-158">Get-Member works with COM objects, so you can explore the members of the object by typing:</span></span>

```
PS> $WshShell | Get-Member

   TypeName: System.__ComObject#{41904400-be18-11d3-a28b-00104bd35090}

Name                     MemberType            Definition
----                     ----------            ----------
AppActivate              Method                bool AppActivate (Variant, Va...
CreateShortcut           Method                IDispatch CreateShortcut (str...
...
```

<span data-ttu-id="2673e-159">**Get-tag** van egy nem kötelező **InputObject** helyett kimenetátirányításával segítségével adja meg a bemeneti paraméter **Get-tag**.</span><span class="sxs-lookup"><span data-stu-id="2673e-159">**Get-Member** has an optional **InputObject** parameter you can use instead of piping to provide input to **Get-Member**.</span></span> <span data-ttu-id="2673e-160">Ahogy fent látható, ha inkább használt a parancs kimenetét azonos számíthat **Get-tag - InputObject $WshShell**.</span><span class="sxs-lookup"><span data-stu-id="2673e-160">You would get the same output as shown above if you instead used the command **Get-Member -InputObject $WshShell**.</span></span> <span data-ttu-id="2673e-161">Ha **InputObject**, azt csak egy elemet az argumentumát kezeli.</span><span class="sxs-lookup"><span data-stu-id="2673e-161">If you use **InputObject**, it treats its argument as a single item.</span></span> <span data-ttu-id="2673e-162">Ez azt jelenti, hogy ha több objektumot egy változóban **Get-tag** kezeli őket, egy objektumokból álló tömb.</span><span class="sxs-lookup"><span data-stu-id="2673e-162">This means that if you have several objects in a variable, **Get-Member** treats them as an array of objects.</span></span> <span data-ttu-id="2673e-163">Például:</span><span class="sxs-lookup"><span data-stu-id="2673e-163">For example:</span></span>

```
PS> $a = 1,2,"three"
PS> Get-Member -InputObject $a
TypeName: System.Object[]
Name               MemberType    Definition
----               ----------    ----------
Count              AliasProperty Count = Length
...
```

<span data-ttu-id="2673e-164">A **WScript.Shell CreateShortcut** metódus egyetlen argumentuma, a fájl elérési útját a helyi létrehozásához fogad el.</span><span class="sxs-lookup"><span data-stu-id="2673e-164">The **WScript.Shell CreateShortcut** method accepts a single argument, the path to the shortcut file to create.</span></span> <span data-ttu-id="2673e-165">Azt írja be a teljes elérési útját az asztalon, de egy egyszerűbb.</span><span class="sxs-lookup"><span data-stu-id="2673e-165">We could type in the full path to the desktop, but there is an easier way.</span></span> <span data-ttu-id="2673e-166">Az asztal általában az aktuális felhasználó otthoni mappában mappájában asztali jelképezi.</span><span class="sxs-lookup"><span data-stu-id="2673e-166">The desktop is normally represented by a folder named Desktop inside the home folder of the current user.</span></span> <span data-ttu-id="2673e-167">A Windows PowerShell rendelkezik egy változó **$Home** , amely tartalmazza a mappa elérési útját.</span><span class="sxs-lookup"><span data-stu-id="2673e-167">Windows PowerShell has a variable **$Home** that contains the path to this folder.</span></span> <span data-ttu-id="2673e-168">Azt adja meg a mappa elérési útját az otthoni változó használatával, és adja meg a mappa nevét, mely az asztali és a helyi létrehozásához írja be a nevet:</span><span class="sxs-lookup"><span data-stu-id="2673e-168">We can specify the path to the home folder by using this variable, and then add the name of the Desktop folder and the name for the shortcut to create by typing:</span></span>

```powershell
$lnk = $WshShell.CreateShortcut("$Home\Desktop\PSHome.lnk")
```

<span data-ttu-id="2673e-169">Valami hasonló a változó nevének belül idézőjelek használata esetén a Windows PowerShell megpróbálja helyettesítse be a megfelelő érték.</span><span class="sxs-lookup"><span data-stu-id="2673e-169">When you use something that looks like a variable name inside double-quotes, Windows PowerShell tries to substitute a matching value.</span></span> <span data-ttu-id="2673e-170">Single-ajánlatok használatakor a Windows PowerShell nem próbálkozik meg helyettesíti a változó értékét.</span><span class="sxs-lookup"><span data-stu-id="2673e-170">If you use single-quotes, Windows PowerShell does not try to substitute the variable value.</span></span> <span data-ttu-id="2673e-171">Például adjon meg a következő parancsokat:</span><span class="sxs-lookup"><span data-stu-id="2673e-171">For example, try typing the following commands:</span></span>

```
PS> "$Home\Desktop\PSHome.lnk"
C:\Documents and Settings\aka\Desktop\PSHome.lnk
PS> '$Home\Desktop\PSHome.lnk'
$Home\Desktop\PSHome.lnk
```

<span data-ttu-id="2673e-172">Most már tudunk nevű változó **$lnk** , amely egy új helyi hivatkozást tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="2673e-172">We now have a variable named **$lnk** that contains a new shortcut reference.</span></span> <span data-ttu-id="2673e-173">Ha meg szeretné tekinteni a tagok, átadható úgy, hogy **Get-tag**.</span><span class="sxs-lookup"><span data-stu-id="2673e-173">If you want to see its members, you can pipe it to **Get-Member**.</span></span> <span data-ttu-id="2673e-174">Az alábbi kimenetben jeleníti meg a tagok a helyi létrehozásának befejezéséhez használja:</span><span class="sxs-lookup"><span data-stu-id="2673e-174">The output below shows the members we need to use to finish creating our shortcut:</span></span>

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

<span data-ttu-id="2673e-175">Adja meg kell a **Cél_elérési_útja**, vagyis az alkalmazás mappájában, a Windows PowerShell környezethez, majd mentse a helyi **$lnk** meghívásával a **mentése** metódus.</span><span class="sxs-lookup"><span data-stu-id="2673e-175">We need to specify the **TargetPath**, which is the application folder for Windows PowerShell, and then save the shortcut **$lnk** by calling the **Save** method.</span></span> <span data-ttu-id="2673e-176">A változó tárolja a Windows PowerShell alkalmazást mappa elérési útja **$PSHome**, így azt ehhez írja be:</span><span class="sxs-lookup"><span data-stu-id="2673e-176">The Windows PowerShell application folder path is stored in the variable **$PSHome**, so we can do this by typing:</span></span>

```powershell
$lnk.TargetPath = $PSHome
$lnk.Save()
```

### <a name="using-internet-explorer-from-windows-powershell"></a><span data-ttu-id="2673e-177">Internet Explorer, a Windows PowerShell használatával</span><span class="sxs-lookup"><span data-stu-id="2673e-177">Using Internet Explorer from Windows PowerShell</span></span>

<span data-ttu-id="2673e-178">Számos alkalmazás (beleértve a Microsoft Office-alkalmazások és az Internet Explorer család) automatizálható a COM-környezetbe.</span><span class="sxs-lookup"><span data-stu-id="2673e-178">Many applications (including the Microsoft Office family of applications and Internet Explorer) can be automated by using COM.</span></span> <span data-ttu-id="2673e-179">Az Internet Explorer néhány tipikus technikák és COM-alapú alkalmazások használata során felmerülő kérdésekkel mutatja be.</span><span class="sxs-lookup"><span data-stu-id="2673e-179">Internet Explorer illustrates some of the typical techniques and issues involved in working with COM-based applications.</span></span>

<span data-ttu-id="2673e-180">Az Internet Explorer példányt hoz létre az Internet Explorer ProgId, megadásával **InternetExplorer.Application**:</span><span class="sxs-lookup"><span data-stu-id="2673e-180">You create an Internet Explorer instance by specifying the Internet Explorer ProgId, **InternetExplorer.Application**:</span></span>

```powershell
$ie = New-Object -ComObject InternetExplorer.Application
```

<span data-ttu-id="2673e-181">Ez a parancs az Internet Explorer elindul, de nem láthatóvá tegye azt.</span><span class="sxs-lookup"><span data-stu-id="2673e-181">This command starts Internet Explorer, but does not make it visible.</span></span> <span data-ttu-id="2673e-182">Írja be a Get-Process, láthatja, hogy fut-e egy iexplore nevű folyamatot.</span><span class="sxs-lookup"><span data-stu-id="2673e-182">If you type Get-Process, you can see that a process named iexplore is running.</span></span> <span data-ttu-id="2673e-183">Valójában Ha kilép a Windows PowerShell, a folyamat továbbra is futtatható.</span><span class="sxs-lookup"><span data-stu-id="2673e-183">In fact, if you exit Windows PowerShell, the process will continue to run.</span></span> <span data-ttu-id="2673e-184">Kell újraindítania a számítógépet vagy egy eszköz, például a Feladatkezelő segítségével a iexplore folyamat befejezéséhez.</span><span class="sxs-lookup"><span data-stu-id="2673e-184">You must reboot the computer or use a tool like Task Manager to end the iexplore process.</span></span>

> [!NOTE]
> <span data-ttu-id="2673e-185">Indítsa el a különálló folyamatként COM-objektumok általában nevezett *ActiveX végrehajtható fájlok*, lehet, vagy előfordulhat, hogy nem jelennek meg a felhasználói felület ablak indításkor.</span><span class="sxs-lookup"><span data-stu-id="2673e-185">COM objects that start as separate processes, commonly called *ActiveX executables*, may or may not display a user interface window when they start up.</span></span> <span data-ttu-id="2673e-186">Ha ablakának létrehozása, de nem láthatóvá tegye azt, például az Internet Explorer, a fókusz általában helyezi át a Windows asztalon, és meg kell győződnie az ablakban látható használhatja őket.</span><span class="sxs-lookup"><span data-stu-id="2673e-186">If they create a window but do not make it visible, like Internet Explorer, the focus will generally move to the Windows desktop and you must make the window visible to interact with it.</span></span>

<span data-ttu-id="2673e-187">Írja be a **$ie |} Get-tag**, tekintse meg a tulajdonságokat és metódusokat az Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="2673e-187">By typing **$ie | Get-Member**, you can view properties and methods for Internet Explorer.</span></span> <span data-ttu-id="2673e-188">Tekintse meg az Internet Explorer-ablakban, állítsa be a Visible tulajdonság $true beírásával:</span><span class="sxs-lookup"><span data-stu-id="2673e-188">To see the Internet Explorer window, set the Visible property to $true by typing:</span></span>

```powershell
$ie.Visible = $true
```

<span data-ttu-id="2673e-189">Ezután lépjen egy adott webcímet Navigálás módszer használatával:</span><span class="sxs-lookup"><span data-stu-id="2673e-189">You can then navigate to a specific Web address by using the Navigate method:</span></span>

```powershell
$ie.Navigate("http://www.microsoft.com/technet/scriptcenter/default.mspx")
```

<span data-ttu-id="2673e-190">Más tagjai az Internet Explorer hálózatiobjektum-modellt használ, akkor lehet szöveg tartalmat lekérjen a weblap.</span><span class="sxs-lookup"><span data-stu-id="2673e-190">Using other members of the Internet Explorer object model, it is possible to retrieve text content from the Web page.</span></span> <span data-ttu-id="2673e-191">A következő paranccsal jelenítse meg a HTML az aktuális weblap törzse:</span><span class="sxs-lookup"><span data-stu-id="2673e-191">The following command will display the HTML text in the body of the current Web page:</span></span>

```powershell
$ie.Document.Body.InnerText
```

<span data-ttu-id="2673e-192">Az Internet Explorer hozzáférését belül PowerShell bezárásához hívja meg az Quit() metódust:</span><span class="sxs-lookup"><span data-stu-id="2673e-192">To close Internet Explorer from within PowerShell, call its Quit() method:</span></span>

```powershell
$ie.Quit()
```

<span data-ttu-id="2673e-193">Ezzel kikényszeríti azt bezárásához.</span><span class="sxs-lookup"><span data-stu-id="2673e-193">This will force it to close.</span></span> <span data-ttu-id="2673e-194">Az ie változó $ már nem egy érvényes hivatkozást tartalmaz, annak ellenére, hogy továbbra is látható a COM objektum lehet.</span><span class="sxs-lookup"><span data-stu-id="2673e-194">The $ie variable no longer contains a valid reference even though it still appears to be a COM object.</span></span> <span data-ttu-id="2673e-195">Ha próbál használni, az automation-hiba jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="2673e-195">If you attempt to use it, you will get an automation error:</span></span>

```
PS> $ie | Get-Member
Get-Member : Exception retrieving the string representation for property "Appli
cation" : "The object invoked has disconnected from its clients. (Exception fro
m HRESULT: 0x80010108 (RPC_E_DISCONNECTED))"
At line:1 char:16
+ $ie | Get-Member <<<<
```

<span data-ttu-id="2673e-196">Eltávolíthat a fennmaradó hivatkozást egy parancs például $ie = $null, vagy a teljes eltávolításához írja be a változó:</span><span class="sxs-lookup"><span data-stu-id="2673e-196">You can either remove the remaining reference with a command like $ie = $null, or completely remove the variable by typing:</span></span>

```powershell
Remove-Variable ie
```

> [!NOTE]
> <span data-ttu-id="2673e-197">Nincs nem általános szabvány e ActiveX végrehajtható fájlok zárja be, és folytatja a futtatását, amikor egy mutató hivatkozás eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="2673e-197">There is no common standard for whether ActiveX executables exit or continue to run when you remove a reference to one.</span></span> <span data-ttu-id="2673e-198">Körülmények között például látható-e az alkalmazás, egy dokumentum szerkesztett fut-e azt, és akár a Windows PowerShell továbbra is fut-e, attól függően, hogy az alkalmazás esetleg, vagy nem kiléphet.</span><span class="sxs-lookup"><span data-stu-id="2673e-198">Depending on circumstances such as whether the application is visible, whether an edited document is running in it, and even whether Windows PowerShell is still running, the application may or may not exit.</span></span> <span data-ttu-id="2673e-199">Ezért tesztelje a végrehajtható, a Windows PowerShell használni kívánt egyes ActiveX miként viselkedjenek.</span><span class="sxs-lookup"><span data-stu-id="2673e-199">For this reason, you should test termination behavior for each ActiveX executable you want to use in Windows PowerShell.</span></span>

### <a name="getting-warnings-about-net-framework-wrapped-com-objects"></a><span data-ttu-id="2673e-200">.NET-keretrendszer becsomagolt COM-objektumok kapcsolatos figyelmeztetés</span><span class="sxs-lookup"><span data-stu-id="2673e-200">Getting Warnings About .NET Framework-Wrapped COM Objects</span></span>

<span data-ttu-id="2673e-201">Bizonyos esetekben egy COM-objektum lehet társított .NET-keretrendszer *futásidejű hívható burkoló* vagy RCW, és a rendszer által használt **New-Object**.</span><span class="sxs-lookup"><span data-stu-id="2673e-201">In some cases, a COM object might have an associated .NET Framework *Runtime-Callable Wrapper* or RCW, and this will be used by **New-Object**.</span></span> <span data-ttu-id="2673e-202">Mivel az RCW viselkedését eltérhet a normál COM-objektum viselkedését **New-Object** rendelkezik egy **Strict** figyelmeztetni RCW hozzáférés paraméter.</span><span class="sxs-lookup"><span data-stu-id="2673e-202">Since the behavior of the RCW may be different from the behavior of the normal COM object, **New-Object** has a **Strict** parameter to warn you about RCW access.</span></span> <span data-ttu-id="2673e-203">Ha megadja a **Strict** paraméter, és ezután hozzon létre egy COM-objektum használatban levő RCW használó, egy figyelmeztetés jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="2673e-203">If you specify the **Strict** parameter and then create a COM object that uses an RCW, you get a warning message:</span></span>

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

<span data-ttu-id="2673e-204">Bár továbbra is létrejön az objektum, figyelmeztetést kap, hogy nincs egy szabványos COM-objektum.</span><span class="sxs-lookup"><span data-stu-id="2673e-204">Although the object is still created, you are warned that it is not a standard COM object.</span></span>