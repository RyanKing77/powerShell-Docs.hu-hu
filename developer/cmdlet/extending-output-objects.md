---
title: Kimeneti objektumok kiterjesztése |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a252e0ec-d456-42d7-bd49-d6b8bc57f388
caps.latest.revision: 11
ms.openlocfilehash: 9c9d50c880f843e21621e5735c800e3afb48b2ad
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62068164"
---
# <a name="extending-output-objects"></a>Kimeneti objektumok kiterjesztése

A .NET keretrendszer objektumait típusok fájlokkal (.ps1xml) parancsmagok, függvények és parancsfájlok által visszaadott bővítheti. Típusok fájlok, amelyek lehetővé teszik a adhat hozzá a meglévő objektumok tulajdonságait és metódusait XML alapú fájlok. Például a Windows PowerShell nyújt a Types.ps1xml fájlt, amely elemeket ad hozzá több meglévő .NET keretrendszer objektumait. A Types.ps1xml fájlt a Windows PowerShell telepítési könyvtárában található (`$pshome`). Létrehozhat saját típusok fájlt további kiterjesztését azokat az objektumokat, vagy az egyéb objektumok ki. Az objektum típusú fájl használatával bővítésekor az objektum bármelyik példányát kiegészül az új elemek.

## <a name="extending-the-systemarray-object"></a>A System.Array objektum kiterjesztése

Az alábbi példa bemutatja, hogyan kiterjeszti a Windows PowerShell a [System.Array](/dotnet/api/System.Array) objektum a Types.ps1xml fájlban. Alapértelmezés szerint [System.Array](/dotnet/api/System.Array) objektumok rendelkeznek egy `Length` tulajdonságot, amely a tömb objektumainak számát sorolja fel. Azonban az "hossza" nem egyértelműen ismerteti a tulajdonságot, mert Windows PowerShell ad hozzá a `Count` alias tulajdonságot használja, amely megjeleníti a értéke megegyezik a `Length` tulajdonság. A következő XML formátumú hozzáadja a `Count` tulajdonságot a [System.Array](/dotnet/api/System.Array) típusa.

```xml
<Type>
  <Name>System.Array</Name>
  <Members>
    <AliasProperty>
      <Name>Count</Name>
      <ReferencedMemberName>Length</ReferencedMemberName>
    </AliasProperty>
  </Members>
</Type>

```

Az új alias tulajdonságot használja a [Get-Member](/powershell/module/Microsoft.PowerShell.Utility/Get-Member) parancsot minden olyan tömbből, az alábbi példában látható módon.

```powershell
Get-Member -InputObject (1,2,3,4)
```

A parancs az alábbi eredményeket adja vissza.
```output
Name           MemberType    Definition
----           ----------    ----------
Count          AliasProperty Count = Length
Address        Method        System.Object& Address(Int32 )
Clone          Method        System.Object Clone()
CopyTo         Method        System.Void CopyTo(Array array, Int32 index):
Equals         Method        System.Boolean Equals(Object obj)
Get            Method        System.Object Get(Int32 )
...
Length         Property      System.Int32 Length {get;}
```
Használhatja a `Count` tulajdonság, vagy a `Length` tulajdonság annak meghatározására, hogy hány objektumot a tömbben. Például:

```powershell
PS> (1, 2, 3, 4).Count
```

```output
4
```

```powershell
PS> (1, 2, 3, 4).Length
```

```output
4
```

## <a name="custom-types-files"></a>Egyéni típusok fájlok

Hozzon létre egy egyéni típusok fájlt, indítsa el egy meglévő típusú fájl másolásával. Az új fájlt minden olyan csoportnévvel rendelkezhet, de .ps1xml fájlnévkiterjesztéssel kell rendelkeznie. Másolja a fájlt, az új fájl elhelyezheti bármilyen könyvtárat, amely hozzáférhető annak a Windows PowerShell, de hasznos lehet helyezni, a fájlok a Windows PowerShell telepítési könyvtár (`$pshome`) vagy egy alkönyvtárában található cikkre hivatkozik a telepítési könyvtár.

A saját kiterjesztett típusok hozzáadása a fájlhoz, adjon hozzá egy típusok elemet minden egyes kiterjeszteni kívánt objektumhoz. Az alábbi témakörök nyújtanak példát.

- Tulajdonságok és tulajdonság csoportok hozzáadásával kapcsolatos további információkért lásd: [kiterjesztett tulajdonságok](./extending-properties-for-objects.md)

- Metódusok hozzáadásával kapcsolatos további információkért lásd: [kiterjesztett módszerek](./defining-default-methods-for-objects.md).

- Tag csoportok hozzáadásával kapcsolatos további információkért lásd: [tag beállítja kiterjesztett](./defining-default-member-sets-for-objects.md).

Miután a saját kiterjesztett típust határoznak meg, a következő módszerek egyikét használatával elérhetővé teheti a kiterjesztett objektumok:

- Elérhetővé teszi a kiterjesztett típusok fájlt az aktuális munkamenethez, használja a [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) parancsmag használatával adja hozzá az új fájlt. Ha azt szeretné, hogy a típusok elsőbbséget élveznek a alkalmazásban definiált típusok egyéb típusú fájlokat (többek között a Types.ps1xml fájlt), használja a `PrependData` paraméterében a [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) parancsmagot.
- Elérhetővé teszi a kiterjesztett típusok fájlt minden további munkamenetekhez, adja hozzá a típusú modulra, exportálhatja a jelenlegi munkamenet, vagy adja hozzá a [Update-TypeData](/powershell/module/Microsoft.PowerShell.Utility/Update-TypeData) parancsot a Windows PowerShell-profilra.

## <a name="signing-types-files"></a>Típusok fájlok aláírása

Típusok fájlok illetéktelen, mert az XML-fájl is tartalmazza a parancsfájl-blokkokban digitálisan alá kell. Digitális aláírások hozzáadásával kapcsolatos további információkért lásd: [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing)

## <a name="see-also"></a>Lásd még:

[Az objektumok alapértelmezett tulajdonságainak meghatározása](./extending-properties-for-objects.md)

[Az objektumok alapértelmezett módszerek meghatározása](./defining-default-methods-for-objects.md)

[Az objektumok alapértelmezett tag csoportok meghatározása](./defining-default-member-sets-for-objects.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
