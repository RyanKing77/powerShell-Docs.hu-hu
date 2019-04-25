---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Statikus osztályok és módszerek használata
ms.assetid: 418ad766-afa6-4b8c-9a44-471889af7fd9
ms.openlocfilehash: e4caff63a1ec7295b6fe450c2915baf0cc7e31af
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086014"
---
# <a name="using-static-classes-and-methods"></a>Statikus osztályok és módszerek használata

Nem minden .NET-keretrendszer osztály használatával hozható létre **New-Object**. Például, ha megpróbál létrehozni egy **System.Environment** vagy egy **System.Math** rendelkező objektum **New-Object**, a következő hibaüzeneteket kap:

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

Ezek a hibák akkor fordul elő, mert nem lehet új objektum létrehozása a ezeket az osztályokat. Ezeket az osztályokat olyan referencia könyvtárak metódusok és tulajdonságok, amelyek nem változtatja az állapotát. Nem kell létrehoznia őket, akkor egyszerűen használja. Osztályok és módszerek, például a következő nevű *statikus osztályok* azok nem jönnek létre, mert megsemmisül, vagy módosítani. Ez egyértelművé teszi példák statikus osztályokat használó biztosít.

## <a name="getting-environment-data-with-systemenvironment"></a>A System.Environment környezet adatainak lekérése

Általában az első lépés a Windows PowerShell-objektum használata, hogy a Get-Member segítségével megtudhatja, milyen tagokat tartalmaz. A statikus osztályok esetében való kissé eltérő, mert a tényleges osztály, amely nem objektum.

### <a name="referring-to-the-static-systemenvironment-class"></a>A statikus System.Environment osztály hivatkozó

Az osztály nevét a szögletes zárójelek közé téve egy statikus osztályt is hivatkozunk. Például, olvassa el **System.Environment** zárójelben a név beírásával. Ezzel néhány általános típusú információkat jeleníti meg:

```
PS> [System.Environment]

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     False    Environment                              System.Object
```

> [!NOTE]
> Ahogy korábban említettük korábban a Windows PowerShell automatikusan lefoglalja "**System.**" Írja be a neveket, ha használja a **New-Object**. Ugyanezt történik, ha egy zárójeles típusú név használatával adhatja meg  **\[System.Environment]** ,  **\[környezet]**.

A **System.Environment** osztály tartalmazza az aktuális folyamat, amely powershell.exe Windows PowerShell használatakor a munkakörnyezet kapcsolatos általános információkat.

Ha megpróbál Ez az osztály a részletek megtekintéséhez írja be a  **\[System.Environment] |} Get-Member**, az objektumtípus, hogy jelentett **System.RuntimeType** , nem **System.Environment**:

```
PS> [System.Environment] | Get-Member

   TypeName: System.RuntimeType
```

A Get-Member statikus tagok megtekintéséhez adja meg a **statikus** paramétert:

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

Tulajdonságok megtekintése a System.Environment most kiválaszthatja.

### <a name="displaying-static-properties-of-systemenvironment"></a>System.Environment statikus tulajdonságainak megjelenítése

System.Environment tulajdonságait is statikus, és meg kell adni, mint a normál tulajdonságok eltérő módon. Használjuk a **::** jelzi, amelyet meg szeretnénk dolgozni egy statická metoda nebo vlastnost Windows powershellt. Tekintse meg a parancsot, amellyel indítsa el a Windows Powershellt, hogy ellenőrizze a **CommandLine** tulajdonság beírásával:

```
PS> [System.Environment]::Commandline
"C:\Program Files\Windows PowerShell\v1.0\powershell.exe"
```

Az operációs rendszer verziójának ellenőrzéséhez OSVersion tulajdonság megjelenítéséhez írja be:

```
PS> [System.Environment]::OSVersion

           Platform ServicePack         Version             VersionString
           -------- -----------         -------             -------------
            Win32NT Service Pack 2      5.1.2600.131072     Microsoft Windows...
```

Azt is ellenőrizze, hogy a számítógép megjelenítésével leáll a **HasShutdownStarted** tulajdonság:

```
PS> [System.Environment]::HasShutdownStarted
False
```

## <a name="doing-math-with-systemmath"></a>Ennek során a System.Math matematikai

A statikus System.Math osztály hasznos néhány matematikai műveletek végrehajtása. A fontos tagjai **System.Math** leginkább, módszerek használatával is meg vannak **Get-Member**.

> [!NOTE]
> System.Math rendelkezik ugyanazzal a névvel több módszert, de azok különbözteti meg a paraméter típusát.

A módszerek listája a következő parancsot írja be a **System.Math** osztály.

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

Ez megjeleníti a matematikai több módszert is. A következő parancsokat, amelyek bemutatják, hogyan működnek a gyakran használt módszerek némelyike listáját:

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