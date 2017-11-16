---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Statikus osztályok és módszerek használatával"
ms.assetid: 418ad766-afa6-4b8c-9a44-471889af7fd9
ms.openlocfilehash: fe41c7d6b45564e7b5bc2b922a18587c9745e26d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="using-static-classes-and-methods"></a>Statikus osztályok és módszerek használatával
Nem minden .NET-keretrendszer osztály használatával hozhatók létre **New-Object**. Például, ha megpróbál létrehozni egy **System.Environment** vagy egy **System.Math** rendelkező objektum **New-Object**, elérhetővé válik a következő hibaüzeneteket:

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

Ezek a hibák akkor áll elő semmilyen módon nem lehet létrehozni új objektumot ezeket az osztályokat. Ezeket az osztályokat olyan referencia könyvtárak módszerek és a tulajdonságokhoz, ne módosítsa az állapotot. Nem kell hozza létre a címzetteket, egyszerűen használja. Osztályok és a fenti módszerek nevezzük *statikus osztályok* azok nem jönnek létre, mert megsemmisítették, vagy megváltozott. Ez egyértelművé példák statikus osztályokat használó lesz elérhető.

### <a name="getting-environment-data-with-systemenvironment"></a>A System.Environment környezeti adatok beolvasása
Általában az első lépés egy objektum a Windows PowerShell használata Get-tag segítségével megtudhatja, milyen tartalmaz tagokat. A statikus osztályok a folyamat kissé eltérő, mert a tényleges osztály, amely nem objektum.

#### <a name="referring-to-the-static-systemenvironment-class"></a>A statikus System.Environment osztály hivatkozik
Egy statikus osztály hivatkoznak körülvevő az osztály nevét a szögletes zárójelek között. Például hivatkozhat **System.Environment** szögletes zárójelben a név beírásával. Ekkor megjelenik néhány általános típussal kapcsolatos információk:

```
PS> [System.Environment]

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     False    Environment                              System.Object
```

> [!NOTE]
> Ahogy azt korábban említettük, a Windows PowerShell automatikusan lefoglalja "**System.**" Írja be a neveket, ha használja a **New-Object**. Az ugyanaz történik, ha használatával zárójeles típusnév kell adnia  **\[System.Environment]** ,  **\[környezet]**.

A **System.Environment** osztály az aktuális folyamat, amely powershell.exe Windows PowerShell használatakor a munkakörnyezet általános információkat tartalmaz.

Ha ez az osztály részleteinek megtekintéséhez írja be a próbál  **\[System.Environment] |} Get-tag**, az objektum típusának jelenti, hogy **System.RuntimeType** , nem **System.Environment**:

```
PS> [System.Environment] | Get-Member

   TypeName: System.RuntimeType
```

A Get-tag statikus tagok megtekintéséhez, adja meg a **statikus** paraméter:

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

A Microsoft immár tulajdonságok System.Environment a megtekintéséhez.

#### <a name="displaying-static-properties-of-systemenvironment"></a>System.Environment statikus tulajdonságainak megjelenítése
System.Environment tulajdonságainak is statikusak, és meg kell adni, mint a normál tulajdonságok eltérő módon. Használjuk **::** jelzi a Windows Powershellhez, amely azt szeretnénk, hogy egy statikus metódus vagy tulajdonság. A parancs, indítsa el a Windows Powershellt használt megtekintéséhez ellenőrizzük a **CommandLine** tulajdonság beírásával:

```
PS> [System.Environment]::Commandline
"C:\Program Files\Windows PowerShell\v1.0\powershell.exe"
```

Ellenőrizze az operációs rendszer verziója, OSVersion tulajdonság megjelenítéséhez írja be:

```
PS> [System.Environment]::OSVersion

           Platform ServicePack         Version             VersionString
           -------- -----------         -------             -------------
            Win32NT Service Pack 2      5.1.2600.131072     Microsoft Windows...
```

Azt is ellenőrizze, hogy a számítógép megjelenítésével leállítási folyamatban van a **HasShutdownStarted** tulajdonság:

```
PS> [System.Environment]::HasShutdownStarted
False
```

### <a name="doing-math-with-systemmath"></a>Ennek során a System.Math matematikai
A System.Math statikus osztály néhány matematikai műveletet hajt végre. A fontos tagjai **System.Math** többnyire módszer, amelyek használatával is meg **Get-tag**.

> [!NOTE]
> System.Math többféle módszer ugyanazzal a névvel rendelkezik, de ezek a paraméterek típusával alapján megkülönböztetett.

Írja be a következő paranccsal listát készíthet a módszerek a **System.Math** osztály.

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

Ez megjeleníti a több matematikai módszert. Parancsok, amelyek bemutatják, hogyan működnek az egyes módszerek listája itt található:

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

