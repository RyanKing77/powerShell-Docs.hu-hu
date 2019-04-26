---
title: A Windows PowerShell-tulajdonság szolgáltató létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- property providers [PowerShell Programmer's Guide]
- providers [PowerShell Programmer's Guide], property provider
ms.assetid: a6adca44-b94b-4103-9970-a9b414355e60
caps.latest.revision: 5
ms.openlocfilehash: 6ec0752a9ae06c5c2cdd1a1851caeeff52d8eb74
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081835"
---
# <a name="creating-a-windows-powershell-property-provider"></a>Windows PowerShelles tulajdonságszolgáltató létrehozása

Ez a témakör ismerteti, hogyan hozhat létre olyan szolgáltatót, amely lehetővé teszi a felhasználó a adattárban lévő elemek tulajdonságainak módosítására. Ennek következtében az ilyen típusú szolgáltató nevezzük egy Windows PowerShell-tulajdonság szolgáltató. Például a beállításjegyzék-szolgáltatója biztosítja a Windows PowerShell végzi beállításkulcs-értékeket, a beállításjegyzék-kulcs elem tulajdonságai. Az ilyen típusú szolgáltató hozzá kell adnia a [System.Management.Automation.Provider.Ipropertycmdletprovider](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider) végrehajtása a .NET-osztály felületet.

> [!NOTE]
> Windows PowerShell biztosít egy sablon fájlt, amely egy Windows PowerShell-szolgáltatóban fejlesztéséhez használhatja. A Microsoft Windows szoftverek fejlesztési Kit for Windows Vista és a .NET Framework 3.0 futtatási összetevői a TemplateProvider.cs fájl érhető el. Letöltési útmutatás: [Windows PowerShell telepítése és a Windows PowerShell SDK letöltési](/powershell/developer/installing-the-windows-powershell-sdk).
>
> A letöltött sablon megtalálható a  **\<PowerShell-minták >** könyvtár. Ez a fájl másolatának kell, és használatával a másolat egy új Windows PowerShell-szolgáltatóban, olyan funkciót, amelynek nincs szüksége eltávolítása.
>
> Más Windows PowerShell-szolgáltató esetében kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).

> [!CAUTION]
> A módszerek-tulajdonság szolgáltató használatával objektumokat kell írnia a [System.Management.Automation.Provider.Cmdletprovider.Writepropertyobject*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WritePropertyObject) metódust.

Az alábbi lista tartalmazza az ebben a témakörben szakaszokban. Ha nem ismeri a Windows PowerShell-tulajdonság szolgáltató írása, olvassa el ezt az információt a sorrendben, amely akkor jelenik meg. Azonban ha ismeri a Windows PowerShell-tulajdonság szolgáltató írása, nyissa meg közvetlenül a keresett információt.

- [A Windows PowerShell-szolgáltatóban meghatározása](#Defining-the-Windows-PowerShell-provider)

- [Alapfunkciók meghatározása](#Defining-Base-Functionality)

- [Tulajdonságainak beolvasása](#Retrieving-Properties)

- [Dinamikus paraméterek csatolása a `Get-ItemProperty` parancsmag](#Attaching-Dynamic-Parameters-to-the-Get-ItemProperty-Cmdlet)

- [Tulajdonságok beállítása](#Setting-Properties)

- [Dinamikus paraméterek csatolása a `Set-ItemProperty` parancsmag](#Attaching-Dynamic-Parameters-for-the-Set-ItemProperty-Cmdlet)

- [Vymazání Vlastnosti egy](#Clearing-Properties)

- [Dinamikus paraméterek csatolása a `Clear-ItemProperty` parancsmag](#Attaching-Dynamic-Parameters-to-the-Clear-ItemProperty-Cmdlet)

- [A Windows PowerShell-szolgáltató létrehozása](#Building-the-Windows-PowerShell-provider)

## <a name="defining-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltatóban meghatározása

Egy tulajdonság szolgáltató létre kell hoznia egy .NET-osztály, amely támogatja a [System.Management.Automation.Provider.Ipropertycmdletprovider](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider) felületet. Ez az alapértelmezett osztálydeklaráció Windows PowerShell által biztosított TemplateProvider.cs-fájlból.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testcmdletspropertyproviderclassdeclaration](Msh_samplestestcmdlets#testcmdletspropertyproviderclassdeclaration)]  -->

## <a name="defining-base-functionality"></a>Alapfunkciók meghatározása

A [System.Management.Automation.Provider.Ipropertycmdletprovider](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider) felület bármely, a szolgáltató alaposztályok, kivéve a csatolható a [ System.Management.Automation.Provider.Drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) osztály. Adja hozzá az alaposztály alaposztályát használ által igényelt alapvető funkciót biztosítja. Alaposztályok kapcsolatos további információkért lásd: [tervezése a Windows PowerShell-szolgáltatóban](./designing-your-windows-powershell-provider.md).

## <a name="retrieving-properties"></a>Tulajdonságainak beolvasása

Beolvasni a tulajdonságokat, a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Ipropertycmdletprovider.Getproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetProperty) metódus támogatja a hívást a `Get-ItemProperty` parancsmagot. Ez a módszer az elem található a megadott útvonalon provider – belső (teljes) tulajdonságait olvassa be.

A `providerSpecificPickList` paraméter azt jelzi, hogy mely tulajdonságok lekéréséhez. Ha ez a paraméter `null` vagy üres, a metódus érdemes lekérni az összes tulajdonság. Emellett [System.Management.Automation.Provider.Ipropertycmdletprovider.Getproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetProperty) ír egy példányát egy [System.Management.Automation.PSObject](/dotnet/api/System.Management.Automation.PSObject) képviselő objektumot egy a lekérdezett tulajdonságainak tulajdonságcsomagot. A metódus semmit nem kell visszaadnia.

Javasoljuk, hogy végrehajtásának [System.Management.Automation.Provider.Ipropertycmdletprovider.Getproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetProperty) a kivételezési listában az egyes elemek nevei altartományokra is kibővített változata támogatja. Ehhez használja a [System.Management.Automation.Wildcardpattern](/dotnet/api/System.Management.Automation.WildcardPattern) osztály végrehajtásához a helyettesítő karakterek is megadhatók.

Itt van az alapértelmezett megvalósítása [System.Management.Automation.Provider.Ipropertycmdletprovider.Getproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetProperty) a Windows PowerShell által biztosított TemplateProvider.cs fájlból.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testcmdletspropertyprovidergetproperty](Msh_samplestestcmdlets#testcmdletspropertyprovidergetproperty)]  -->

#### <a name="things-to-remember-about-implementing-getproperty"></a>Megjegyzendő GetProperty megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Ipropertycmdletprovider.Getproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetProperty):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-tulajdonság szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Ipropertycmdletprovider.Getproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetProperty) metódus meg kell győződnie arról, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott követelményeinek képességek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását nem kell lekérni, kivéve, ha a felhasználó elől rejtett objektumok egy olvasót a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Hiba történt kell írni, ha az elérési utat jelöl egy elemet a felhasználó elől elrejtett és [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) értékre van állítva `false`.

## <a name="attaching-dynamic-parameters-to-the-get-itemproperty-cmdlet"></a>A Get-ItemProperty parancsmag dinamikus paraméterek csatolása

A `Get-ItemProperty` parancsmag szükség lehet további paramétereket, amelyeket dinamikusan futásidőben. Ahhoz, hogy ezek a dinamikus paraméterek, a Windows PowerShell tulajdonság a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Ipropertycmdletprovider.Getpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetPropertyDynamicParameters) metódust. A `path` paraméter azt jelzi, hogy a teljes provider – belső elérési útját, míg a `providerSpecificPickList` paraméter adja meg a szolgáltatóhoz tartozó tulajdonságok adta meg a parancssort. Ez a paraméter lehet `null` vagy üres, ha a tulajdonságok vannak a parancsmag eredményez. Ebben az esetben ez a módszer, amely rendelkezik a tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés objektumot adja vissza vagy egy [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A Windows PowerShell-modul a visszaadott objektum segítségével adja hozzá a paramétereket a parancsmaghoz.

Itt van az alapértelmezett megvalósítása [System.Management.Automation.Provider.Ipropertycmdletprovider.Getpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetPropertyDynamicParameters) a Windows PowerShell által biztosított TemplateProvider.cs fájlból.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testcmdletspropertyprovidergetpropertydynamicparameters](Msh_samplestestcmdlets#testcmdletspropertyprovidergetpropertydynamicparameters)]  -->

## <a name="setting-properties"></a>Tulajdonságok beállítása

Állítsa be a tulajdonságokat, hogy a Windows PowerShell tulajdonság a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Ipropertycmdletprovider.Setproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetProperty) metódus támogatja a hívást a `Set-ItemProperty` parancsmagot. Ez a módszer egy vagy több tulajdonságának elem beállítja a megadott elérési úton, és szükség szerint a megadott tulajdonságok felülírja. [System.Management.Automation.Provider.Ipropertycmdletprovider.Setproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetProperty) egy példányát is ír egy [System.Management.Automation.PSObject](/dotnet/api/System.Management.Automation.PSObject) egy tulajdonságcsomagot, a frissített képviselő objektumot tulajdonságok.

Itt van az alapértelmezett megvalósítása [System.Management.Automation.Provider.Ipropertycmdletprovider.Setproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetProperty) a Windows PowerShell által biztosított TemplateProvider.cs fájlból.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testcmdletspropertyprovidersetproperty](Msh_samplestestcmdlets#testcmdletspropertyprovidersetproperty)]  -->

#### <a name="things-to-remember-about-implementing-set-itemproperty"></a>Megjegyzendő Set-ItemProperty megvalósításával kapcsolatos tudnivalók

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Ipropertycmdletprovider.Setproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetProperty):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-tulajdonság szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Ipropertycmdletprovider.Setproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetProperty) metódus biztosítania kell, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott követelményeinek képességek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását nem kell lekérni, kivéve, ha a felhasználó elől rejtett objektumok egy olvasót a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Hiba történt kell írni, ha az elérési utat jelöl egy elemet a felhasználó elől elrejtett és [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) értékre van állítva `false`.

- A megvalósítását az [System.Management.Automation.Provider.Ipropertycmdletprovider.Setproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetProperty) metódus meg kell hívnia [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) , és ellenőrizze a visszaadott érték az adattár változtatások előtt. Ez a módszer segítségével amikor módosításakor a rendszer állapotáról, például fájlok átnevezésével, győződjön meg arról, hogy egy művelet végrehajtását. [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) küld a felhasználónak, a Windows PowerShell-modul és kezelése parancssori beállítást vagy meghatározásakor preferenciaváltozók módosítani az erőforrás neve milyen üzenetnek kell megjelennie.

  Hívása után [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) adja vissza `true`, ha a rendszer potenciálisan veszélyes fürthálózathoz, a [ System.Management.Automation.Provider.Ipropertycmdletprovider.Setproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetProperty) metódus meg kell hívnia a [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) metódust. Ez a módszer egy megerősítő üzenetet küld a felhasználó számára lehetővé teszi további visszajelzés jelzi, hogy a művelet fenn kell tartani.

## <a name="attaching-dynamic-parameters-for-the-set-itemproperty-cmdlet"></a>Dinamikus paraméterek csatolása a Set-ItemProperty parancsmaghoz

A `Set-ItemProperty` parancsmag szükség lehet további paramétereket, amelyeket dinamikusan futásidőben. Ahhoz, hogy ezek a dinamikus paraméterek, a Windows PowerShell tulajdonság a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Ipropertycmdletprovider.Setpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.SetPropertyDynamicParameters) metódust. Ez a módszer, amely rendelkezik a tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés objektumot adja vissza vagy egy [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A `null` értéket is ad vissza, ha a dinamikus paraméterek nélkül fel kell venni.

Itt van az alapértelmezett megvalósítása [System.Management.Automation.Provider.Ipropertycmdletprovider.Getpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.GetPropertyDynamicParameters) a Windows PowerShell által biztosított TemplateProvider.cs fájlból.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testcmdletspropertyprovidersetpropertydynamicparameters](Msh_samplestestcmdlets#testcmdletspropertyprovidersetpropertydynamicparameters)]  -->

## <a name="clearing-properties"></a>Tulajdonságok törlése

Törölje a tulajdonságai, a Windows PowerShell tulajdonság a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Ipropertycmdletprovider.Clearproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearProperty) metódus támogatja a hívást a `Clear-ItemProperty` parancsmagot. Ez a módszer az elemet a megadott elérési úton található egy vagy több tulajdonságait állítja be.

Itt van az alapértelmezett megvalósítása [System.Management.Automation.Provider.Ipropertycmdletprovider.Clearproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearProperty) a Windows PowerShell által biztosított TemplateProvider.cs fájlból.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testcmdletspropertyproviderclearproperty](Msh_samplestestcmdlets#testcmdletspropertyproviderclearproperty)]  -->

#### <a name="thing-to-remember-about-implementing-clearproperty"></a>Fontos megjegyezni ClearProperty megvalósításáról

A következő feltételek érvényesek az megvalósítását [System.Management.Automation.Provider.Ipropertycmdletprovider.Clearproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearProperty):

- A szolgáltató osztálya meghatározásakor egy Windows PowerShell-tulajdonság szolgáltató a szolgáltató képességei ExpandWildcards, szűrő, belefoglalása vagy kizárása, előfordulhat, hogy deklarálja a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. Ezekben az esetekben a megvalósítását az [System.Management.Automation.Provider.Ipropertycmdletprovider.Clearproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearProperty) metódus meg kell győződnie arról, hogy az elérési utat, a metódusnak átadott megfelel-e a megadott követelményeinek képességek. Ehhez a metódus hozzá kell férnie a megfelelő tulajdonságot használja, például a [System.Management.Automation.Provider.Cmdletprovider.Exclude*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Exclude) és [ System.Management.Automation.Provider.Cmdletprovider.Include*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Include) tulajdonságait.

- Alapértelmezés szerint ez a metódus felülbírálását nem kell lekérni, kivéve, ha a felhasználó elől rejtett objektumok egy olvasót a [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) tulajdonsága `true`. Hiba történt kell írni, ha az elérési utat jelöl egy elemet a felhasználó elől elrejtett és [System.Management.Automation.Provider.Cmdletprovider.Force*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Force) értékre van állítva `false`.

- A megvalósítását az [System.Management.Automation.Provider.Ipropertycmdletprovider.Clearproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearProperty) metódus meg kell hívnia [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess ](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) , és ellenőrizze a visszaadott érték az adattár változtatások előtt. Ez a módszer módosításakor a rendszer állapotáról, például a tartalom kiürítése előtt, győződjön meg arról, hogy egy művelet végrehajtására szolgál. [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) küld a felhasználó a Windows PowerShell-futtatókörnyezetben, figyelembe véve parancssori beállítást vagy a preferenciaváltozók módosítani az erőforrás neve annak meghatározása, mi megjelenjenek.

  Hívása után [System.Management.Automation.Provider.Cmdletprovider.ShouldProcess](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldProcess) adja vissza `true`, ha a rendszer potenciálisan veszélyes fürthálózathoz, a [ System.Management.Automation.Provider.Ipropertycmdletprovider.Clearproperty*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearProperty) metódus meg kell hívnia a [System.Management.Automation.Provider.Cmdletprovider.ShouldContinue](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.ShouldContinue) metódust. Ez a módszer egy megerősítő üzenetet küld a felhasználó számára lehetővé teszi annak jelzésére, hogy fenn kell tartani a potenciálisan veszélyes művelet további visszajelzés.

## <a name="attaching-dynamic-parameters-to-the-clear-itemproperty-cmdlet"></a>Dinamikus paraméterek csatolása a Clear-ItemProperty parancsmaghoz

A `Clear-ItemProperty` parancsmag szükség lehet további paramétereket, amelyeket dinamikusan futásidőben. Ahhoz, hogy ezek a dinamikus paraméterek, a Windows PowerShell tulajdonság a szolgáltatónak tartalmaznia kell a [System.Management.Automation.Provider.Ipropertycmdletprovider.Clearpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearPropertyDynamicParameters) metódust. Ez a módszer, amely rendelkezik a tulajdonságokat és mezőket az attribútumok hasonlít egy parancsmag osztály elemzés objektumot adja vissza vagy egy [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum. A `null` értéket is ad vissza, ha a dinamikus paraméterek nélkül fel kell venni.

Itt van az alapértelmezett megvalósítása [System.Management.Automation.Provider.Ipropertycmdletprovider.Clearpropertydynamicparameters*](/dotnet/api/System.Management.Automation.Provider.IPropertyCmdletProvider.ClearPropertyDynamicParameters) a Windows PowerShell által biztosított TemplateProvider.cs fájlból.

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testcmdletspropertyproviderclearpropertydynamicparameters](Msh_samplestestcmdlets#testcmdletspropertyproviderclearpropertydynamicparameters)]  -->

## <a name="building-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltató létrehozása

Lásd: [parancsmagok,-szolgáltatók regisztrálása és alkalmazások üzemeltetése](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-szolgáltató](./designing-your-windows-powershell-provider.md)

[Terv a Windows PowerShell-szolgáltató](./designing-your-windows-powershell-provider.md)

[Objektumtípusok kiterjesztése és formázása](http://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](http://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)