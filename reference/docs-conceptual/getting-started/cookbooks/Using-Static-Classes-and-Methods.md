---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Statikus osztályok és módszerek használata
ms.assetid: 418ad766-afa6-4b8c-9a44-471889af7fd9
ms.openlocfilehash: 0f2b02c3a40365ad0335118b057a4e548c9f6535
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="using-static-classes-and-methods"></a><span data-ttu-id="addaf-103">Statikus osztályok és módszerek használata</span><span class="sxs-lookup"><span data-stu-id="addaf-103">Using Static Classes and Methods</span></span>
<span data-ttu-id="addaf-104">Nem minden .NET-keretrendszer osztály használatával hozhatók létre **New-Object**.</span><span class="sxs-lookup"><span data-stu-id="addaf-104">Not all .NET Framework classes can be created by using **New-Object**.</span></span> <span data-ttu-id="addaf-105">Például, ha megpróbál létrehozni egy **System.Environment** vagy egy **System.Math** rendelkező objektum **New-Object**, elérhetővé válik a következő hibaüzeneteket:</span><span class="sxs-lookup"><span data-stu-id="addaf-105">For example, if you try to create a **System.Environment** or a **System.Math** object with **New-Object**, you will get the following error messages:</span></span>

```
PS> New-Object System.Environment
New-Object : Constructor not found. Cannot find an appropriate constructor for
type System.Environment.
At line:1 char:11
+ New-Object  <<<< System.Environment

PS> New-Object System.Math
New-Object : Constructor not found. Cannot find an appropriate constructor for
type System.Math.
At line:1 char:11
+ New-Object  <<<< System.Math
```

<span data-ttu-id="addaf-106">Ezek a hibák akkor áll elő semmilyen módon nem lehet létrehozni új objektumot ezeket az osztályokat.</span><span class="sxs-lookup"><span data-stu-id="addaf-106">These errors occur because there is no way to create a new object from these classes.</span></span> <span data-ttu-id="addaf-107">Ezeket az osztályokat olyan referencia könyvtárak módszerek és a tulajdonságokhoz, ne módosítsa az állapotot.</span><span class="sxs-lookup"><span data-stu-id="addaf-107">These classes are reference libraries of methods and properties that do not change state.</span></span> <span data-ttu-id="addaf-108">Nem kell hozza létre a címzetteket, egyszerűen használja.</span><span class="sxs-lookup"><span data-stu-id="addaf-108">You don't need to create them, you simply use them.</span></span> <span data-ttu-id="addaf-109">Osztályok és a fenti módszerek nevezzük *statikus osztályok* azok nem jönnek létre, mert megsemmisítették, vagy megváltozott.</span><span class="sxs-lookup"><span data-stu-id="addaf-109">Classes and methods such as these are called *static classes* because they are not created, destroyed, or changed.</span></span> <span data-ttu-id="addaf-110">Ez egyértelművé példák statikus osztályokat használó lesz elérhető.</span><span class="sxs-lookup"><span data-stu-id="addaf-110">To make this clear we will provide examples that use static classes.</span></span>

### <a name="getting-environment-data-with-systemenvironment"></a><span data-ttu-id="addaf-111">A System.Environment környezeti adatok beolvasása</span><span class="sxs-lookup"><span data-stu-id="addaf-111">Getting Environment Data with System.Environment</span></span>
<span data-ttu-id="addaf-112">Általában az első lépés egy objektum a Windows PowerShell használata Get-tag segítségével megtudhatja, milyen tartalmaz tagokat.</span><span class="sxs-lookup"><span data-stu-id="addaf-112">Usually, the first step in working with an object in Windows PowerShell is to use Get-Member to find out what members it contains.</span></span> <span data-ttu-id="addaf-113">A statikus osztályok a folyamat kissé eltérő, mert a tényleges osztály, amely nem objektum.</span><span class="sxs-lookup"><span data-stu-id="addaf-113">With static classes, the process is a little different because the actual class is not an object.</span></span>

#### <a name="referring-to-the-static-systemenvironment-class"></a><span data-ttu-id="addaf-114">A statikus System.Environment osztály hivatkozik</span><span class="sxs-lookup"><span data-stu-id="addaf-114">Referring to the Static System.Environment Class</span></span>
<span data-ttu-id="addaf-115">Egy statikus osztály hivatkoznak körülvevő az osztály nevét a szögletes zárójelek között.</span><span class="sxs-lookup"><span data-stu-id="addaf-115">You can refer to a static class by surrounding the class name with square brackets.</span></span> <span data-ttu-id="addaf-116">Például hivatkozhat **System.Environment** szögletes zárójelben a név beírásával.</span><span class="sxs-lookup"><span data-stu-id="addaf-116">For example, you can refer to **System.Environment** by typing the name within brackets.</span></span> <span data-ttu-id="addaf-117">Ekkor megjelenik néhány általános típussal kapcsolatos információk:</span><span class="sxs-lookup"><span data-stu-id="addaf-117">Doing so displays some generic type information:</span></span>

```
PS> [System.Environment]

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     False    Environment                              System.Object
```

> [!NOTE]
> <span data-ttu-id="addaf-118">Ahogy azt korábban említettük, a Windows PowerShell automatikusan lefoglalja "**System.**"</span><span class="sxs-lookup"><span data-stu-id="addaf-118">As we mentioned previously, Windows PowerShell automatically prepends '**System.**'</span></span> <span data-ttu-id="addaf-119">Írja be a neveket, ha használja a **New-Object**.</span><span class="sxs-lookup"><span data-stu-id="addaf-119">to type names when you use **New-Object**.</span></span> <span data-ttu-id="addaf-120">Az ugyanaz történik, ha használatával zárójeles típusnév kell adnia  **\[System.Environment]** ,  **\[környezet]**.</span><span class="sxs-lookup"><span data-stu-id="addaf-120">The same thing happens when using a bracketed type name, so you can specify **\[System.Environment]** as **\[Environment]**.</span></span>

<span data-ttu-id="addaf-121">A **System.Environment** osztály az aktuális folyamat, amely powershell.exe Windows PowerShell használatakor a munkakörnyezet általános információkat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="addaf-121">The **System.Environment** class contains general information about the working environment for the current process, which is powershell.exe when working within Windows PowerShell.</span></span>

<span data-ttu-id="addaf-122">Ha ez az osztály részleteinek megtekintéséhez írja be a próbál  **\[System.Environment] |} Get-tag**, az objektum típusának jelenti, hogy **System.RuntimeType** , nem **System.Environment**:</span><span class="sxs-lookup"><span data-stu-id="addaf-122">If you try to view details of this class by typing **\[System.Environment] | Get-Member**, the object type is reported as being **System.RuntimeType** , not **System.Environment**:</span></span>

```
PS> [System.Environment] | Get-Member

   TypeName: System.RuntimeType
```

<span data-ttu-id="addaf-123">A Get-tag statikus tagok megtekintéséhez, adja meg a **statikus** paraméter:</span><span class="sxs-lookup"><span data-stu-id="addaf-123">To view static members with Get-Member, specify the **Static** parameter:</span></span>

```
PS> [System.Environment] | Get-Member -Static

   TypeName: System.Environment

Name                       MemberType Definition
----                       ---------- ----------
Equals                     Method     static System.Boolean Equals(Object ob...
Exit                       Method     static System.Void Exit(Int32 exitCode)
...
CommandLine                Property   static System.String CommandLine {get;}
CurrentDirectory           Property   static System.String CurrentDirectory ...
ExitCode                   Property   static System.Int32 ExitCode {get;set;}
HasShutdownStarted         Property   static System.Boolean HasShutdownStart...
MachineName                Property   static System.String MachineName {get;}
NewLine                    Property   static System.String NewLine {get;}
OSVersion                  Property   static System.OperatingSystem OSVersio...
ProcessorCount             Property   static System.Int32 ProcessorCount {get;}
StackTrace                 Property   static System.String StackTrace {get;}
SystemDirectory            Property   static System.String SystemDirectory {...
TickCount                  Property   static System.Int32 TickCount {get;}
UserDomainName             Property   static System.String UserDomainName {g...
UserInteractive            Property   static System.Boolean UserInteractive ...
UserName                   Property   static System.String UserName {get;}
Version                    Property   static System.Version Version {get;}
WorkingSet                 Property   static System.Int64 WorkingSet {get;}
TickCount                               ExitCode
```

<span data-ttu-id="addaf-124">A Microsoft immár tulajdonságok System.Environment a megtekintéséhez.</span><span class="sxs-lookup"><span data-stu-id="addaf-124">We can now select properties to view from System.Environment.</span></span>

#### <a name="displaying-static-properties-of-systemenvironment"></a><span data-ttu-id="addaf-125">System.Environment statikus tulajdonságainak megjelenítése</span><span class="sxs-lookup"><span data-stu-id="addaf-125">Displaying Static Properties of System.Environment</span></span>

<span data-ttu-id="addaf-126">System.Environment tulajdonságainak is statikusak, és meg kell adni, mint a normál tulajdonságok eltérő módon.</span><span class="sxs-lookup"><span data-stu-id="addaf-126">The properties of System.Environment are also static, and must be specified in a different way than normal properties.</span></span> <span data-ttu-id="addaf-127">Használjuk **::** jelzi a Windows Powershellhez, amely azt szeretnénk, hogy egy statikus metódus vagy tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="addaf-127">We use **::** to indicate to Windows PowerShell that we want to work with a static method or property.</span></span> <span data-ttu-id="addaf-128">A parancs, indítsa el a Windows Powershellt használt megtekintéséhez ellenőrizzük a **CommandLine** tulajdonság beírásával:</span><span class="sxs-lookup"><span data-stu-id="addaf-128">To see the command that was used to launch Windows PowerShell, we check the **CommandLine** property by typing:</span></span>

```
PS> [System.Environment]::Commandline
"C:\Program Files\Windows PowerShell\v1.0\powershell.exe"
```

<span data-ttu-id="addaf-129">Ellenőrizze az operációs rendszer verziója, OSVersion tulajdonság megjelenítéséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="addaf-129">To check the operating system version, display the OSVersion property by typing:</span></span>

```
PS> [System.Environment]::OSVersion

           Platform ServicePack         Version             VersionString
           -------- -----------         -------             -------------
            Win32NT Service Pack 2      5.1.2600.131072     Microsoft Windows...
```

<span data-ttu-id="addaf-130">Azt is ellenőrizze, hogy a számítógép megjelenítésével leállítási folyamatban van a **HasShutdownStarted** tulajdonság:</span><span class="sxs-lookup"><span data-stu-id="addaf-130">We can check whether the computer is in the process of shutting down by displaying the **HasShutdownStarted** property:</span></span>

```
PS> [System.Environment]::HasShutdownStarted
False
```

### <a name="doing-math-with-systemmath"></a><span data-ttu-id="addaf-131">Ennek során a System.Math matematikai</span><span class="sxs-lookup"><span data-stu-id="addaf-131">Doing Math with System.Math</span></span>

<span data-ttu-id="addaf-132">A System.Math statikus osztály néhány matematikai műveletet hajt végre.</span><span class="sxs-lookup"><span data-stu-id="addaf-132">The System.Math static class is useful for performing some mathematical operations.</span></span> <span data-ttu-id="addaf-133">A fontos tagjai **System.Math** többnyire módszer, amelyek használatával is meg **Get-tag**.</span><span class="sxs-lookup"><span data-stu-id="addaf-133">The important members of **System.Math** are mostly methods, which we can display by using **Get-Member**.</span></span>

> [!NOTE]
> <span data-ttu-id="addaf-134">System.Math többféle módszer ugyanazzal a névvel rendelkezik, de ezek a paraméterek típusával alapján megkülönböztetett.</span><span class="sxs-lookup"><span data-stu-id="addaf-134">System.Math has several methods with the same name, but they are distinguished by the type of their parameters.</span></span>

<span data-ttu-id="addaf-135">Írja be a következő paranccsal listát készíthet a módszerek a **System.Math** osztály.</span><span class="sxs-lookup"><span data-stu-id="addaf-135">Type the following command to list the methods of the **System.Math** class.</span></span>

```
PS> [System.Math] | Get-Member -Static -MemberType Methods

   TypeName: System.Math

Name            MemberType Definition
----            ---------- ----------
Abs             Method     static System.Single Abs(Single value), static Sy...
Acos            Method     static System.Double Acos(Double d)
Asin            Method     static System.Double Asin(Double d)
Atan            Method     static System.Double Atan(Double d)
Atan2           Method     static System.Double Atan2(Double y, Double x)
BigMul          Method     static System.Int64 BigMul(Int32 a, Int32 b)
Ceiling         Method     static System.Double Ceiling(Double a), static Sy...
Cos             Method     static System.Double Cos(Double d)
Cosh            Method     static System.Double Cosh(Double value)
DivRem          Method     static System.Int32 DivRem(Int32 a, Int32 b, Int3...
Equals          Method     static System.Boolean Equals(Object objA, Object ...
Exp             Method     static System.Double Exp(Double d)
Floor           Method     static System.Double Floor(Double d), static Syst...
IEEERemainder   Method     static System.Double IEEERemainder(Double x, Doub...
Log             Method     static System.Double Log(Double d), static System...
Log10           Method     static System.Double Log10(Double d)
Max             Method     static System.SByte Max(SByte val1, SByte val2), ...
Min             Method     static System.SByte Min(SByte val1, SByte val2), ...
Pow             Method     static System.Double Pow(Double x, Double y)
ReferenceEquals Method     static System.Boolean ReferenceEquals(Object objA...
Round           Method     static System.Double Round(Double a), static Syst...
Sign            Method     static System.Int32 Sign(SByte value), static Sys...
Sin             Method     static System.Double Sin(Double a)
Sinh            Method     static System.Double Sinh(Double value)
Sqrt            Method     static System.Double Sqrt(Double d)
Tan             Method     static System.Double Tan(Double a)
Tanh            Method     static System.Double Tanh(Double value)
Truncate        Method     static System.Decimal Truncate(Decimal d), static...
```

<span data-ttu-id="addaf-136">Ez megjeleníti a több matematikai módszert.</span><span class="sxs-lookup"><span data-stu-id="addaf-136">This displays several mathematical methods.</span></span> <span data-ttu-id="addaf-137">Parancsok, amelyek bemutatják, hogyan működnek az egyes módszerek listája itt található:</span><span class="sxs-lookup"><span data-stu-id="addaf-137">Here is a list of commands that demonstrate how some of the common methods work:</span></span>

```
PS> [System.Math]::Sqrt(9)
3
PS> [System.Math]::Pow(2,3)
8
PS> [System.Math]::Floor(3.3)
3
PS> [System.Math]::Floor(-3.3)
-4
PS> [System.Math]::Ceiling(3.3)
4
PS> [System.Math]::Ceiling(-3.3)
-3
PS> [System.Math]::Max(2,7)
7
PS> [System.Math]::Min(2,7)
2
PS> [System.Math]::Truncate(9.3)
9
PS> [System.Math]::Truncate(-9.3)
-9
```