---
title: Egy alapszintű Windows PowerShell-szolgáltató létrehozása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- base provider [PowerShell Programmer's Guide]
- providers [PowerShell Programmer's Guide], base provider
ms.assetid: 11eeea41-15c8-47ad-9016-0f4b72573305
caps.latest.revision: 7
ms.openlocfilehash: 19cc3817016d96e1412a5f3506e9d694ba55b48d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850847"
---
# <a name="creating-a-basic-windows-powershell-provider"></a>Alapszintű Windows PowerShell-szolgáltató létrehozása

Ez a témakör a kiindulási pontként megtudhatja, hogyan hozhat létre egy Windows PowerShell-szolgáltató. Az itt leírt alapszintű szolgáltató és a szolgáltató leállítási módszert biztosít, és bár ez a szolgáltató nem ad meg egy azt jelenti, hogy egy adattár eléréséhez, vagy a, vagy állítsa be az adatokat az adattárban, azt adja meg az alapvető funkciói által igényelt Minden szolgáltató.

A leírt alapszintű szolgáltató korábban említettek szerint itt valósítja meg a metódusok és a szolgáltató leállításáért. A Windows PowerShell-modul inicializálása, és a szolgáltató meghívná a módszerek meghívja.

> [!NOTE]
> A szolgáltató egy minta a Windows PowerShell által biztosított AccessDBSampleProvider01.cs fájlban találja.

A jelen témakör szakaszai a következők:

- [A Windows PowerShell-szolgáltatóban osztály meghatározása](#Defining-the-Windows-PowerShell-Provider-Class)

- [Szolgáltatóspecifikus állapotinformációkat meghatározása](#Defining-Provider-Specific-State-Information)

- [A szolgáltató inicializálása](#Initializing-the-Provider)

- [Indítsa el a dinamikus paraméterek](#Start-Dynamic-Parameters)

- [A szolgáltató uninitializing](#Uninitializing-the-Provider)

- [Kódminta](#Code-Sample)

- [A Windows PowerShell-szolgáltatóban tesztelése](#Testing-the-Windows-PowerShell-Provider)

## <a name="defining-the-windows-powershell-provider-class"></a>A Windows PowerShell-szolgáltatóban osztály meghatározása

Az első lépés egy Windows PowerShell-szolgáltató létrehozása, hogy a .NET-osztály meghatározása. Ez a alapvető szolgáltató határozza meg a nevű osztály `AccessDBProvider` származik, amely a [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) alaposztály.

Javasoljuk, hogy a szolgáltató osztályait helyez egy `Providers` névtér az API-t névtér, például: xxx. PowerShell.Providers. Ez a szolgáltató használ a `Microsoft.Samples.PowerShell.Provider` névteret, amelyben Windows PowerShell-szolgáltató az összes minta futtatása.

> [!NOTE]
> Az osztály egy Windows PowerShell-szolgáltató explicit módon jelöléssel kell nyilvánosként. Nem nyilvános megjelölt osztályok belső alapértelmezés szerint, és nem található a Windows PowerShell-modul által.

Ez a alapvető szolgáltató osztály definícióját a következő:

[!code-csharp[AccessDBProviderSample01.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample01/AccessDBProviderSample01.cs#L23-L24 "AccessDBProviderSample01.cs")]

Az osztálykiterjesztések definíciója közvetlenül előtt be kell állítania a [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribútum, a következő szintaxissal: [CmdletProvider()].

Attribútum az osztály tovább deklarálja, szükség esetén kulcsszavakkal állíthatja be. Figyelje meg, hogy a [System.Management.Automation.Provider.Cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) attribútumot deklarálni Itt két paramétert tartalmaz. Az első attribútum paraméter megadja a szolgáltató, amely a felhasználó később módosíthatja az alapértelmezett mobilbarát nevét. A második paraméter adja meg a Windows PowerShell által meghatározott képességeket, amelyek a szolgáltató tesz elérhetővé a Windows PowerShell-modul a parancs feldolgozása közben. A lehetséges értékek a szolgáltató képességei határozzák meg a [System.Management.Automation.Provider.Providercapabilities](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) enumerálása. Mivel ez egy alapszintű szolgáltatót, az alkalmazás nem funkcióját támogatja.

> [!NOTE]
> A Windows PowerShell-szolgáltató teljesen minősített neve tartalmazza a szerelvény neve és egyéb attribútumok Windows PowerShell határozza meg a szolgáltató regisztrálásakor.

## <a name="defining-provider-specific-state-information"></a>Szolgáltatóspecifikus állapotinformációkat meghatározása

A [System.Management.Automation.Provider.Cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) alaposztály és az összes származtatott osztály tekintendők állapot nélküli, mert a Windows PowerShell-modul provider-példányok csak szükség szerint hoz létre. Ezért, ha a szolgáltató a szolgáltatóhoz tartozó adatok teljes körű vezérlés és karbantartási állapot van szüksége, kell származniuk egy osztály az [System.Management.Automation.Providerinfo](/dotnet/api/System.Management.Automation.ProviderInfo) osztály. A származtatott osztály meg kell határoznia a szükséges a-állapot karbantartásához, hogy amikor a Windows PowerShell-modult meghívja a szolgáltatóhoz tartozó adatok is el tagokat a [System.Management.Automation.Provider.Cmdletprovider.Start*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Start) metódusnak a felülbírásával inicializálhatja a szolgáltató.

Egy Windows PowerShell-szolgáltató állapota kapcsolat alapján is fenntartására. Kapcsolat állapota fenntartásának kapcsolatos további információkért lásd: [létrehozása a PowerShell Meghajtószolgáltató](./creating-a-windows-powershell-drive-provider.md).

## <a name="initializing-the-provider"></a>A szolgáltató inicializálása

A Windows PowerShell-modul meghívja a szolgáltató inicializálása a [System.Management.Automation.Provider.Cmdletprovider.Start*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Start) metódust, amikor a Windows PowerShell elindul. Az esetek többségében, a szolgáltató használható ez a módszer, amely egyszerűen visszaad alapértelmezett megvalósítása a [System.Management.Automation.Providerinfo](/dotnet/api/System.Management.Automation.ProviderInfo) objektum, amely ismerteti a szolgáltatónál. Azonban abban az esetben, ahol szeretné adja meg a további inicializálási adatait, akkor meg kell valósítania a saját [System.Management.Automation.Provider.Cmdletprovider.Start*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Start) metódushoz, amely a módosítottváltozatátadjavissza[ System.Management.Automation.Providerinfo](/dotnet/api/System.Management.Automation.ProviderInfo) a szolgáltató átadott objektumot. Általában ez a módszer térjen vissza a megadott [System.Management.Automation.Providerinfo](/dotnet/api/System.Management.Automation.ProviderInfo) , vagy egy módosított objektum átadott [System.Management.Automation.Providerinfo](/dotnet/api/System.Management.Automation.ProviderInfo) , amely az objektum más inicializálási információkat tartalmaz.

Ez a alapvető szolgáltató nem bírálja felül ezt a módszert. Az alábbi kód azonban ez a módszer alapértelmezett megvalósítását mutatja be:

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesaccessdbprov01#accessdbprov01ProviderStart](Msh_samplesaccessdbprov01#accessdbprov01ProviderStart)]  -->

A szolgáltató fenntarthatja a szolgáltatóhoz tartozó információk állapotát a leírtak szerint [definiáló szolgáltatóhoz tartozó adatok állapot](#Defining-Provider-Specific-State-Information). Ebben az esetben a megvalósítás felül kell írnia a [System.Management.Automation.Provider.Cmdletprovider.Start*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Start) metódust a származtatott osztály egy példányát adja vissza.

## <a name="start-dynamic-parameters"></a>Indítsa el a dinamikus paraméterek

A szolgáltató megvalósítását a [System.Management.Automation.Provider.Cmdletprovider.Start*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Start) metódus szükség lehet további paramétereket. Ebben az esetben a szolgáltató felül kell írni a [System.Management.Automation.Provider.Cmdletprovider.Startdynamicparameters*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.StartDynamicParameters) metódus és egy objektum, amely rendelkezik a tulajdonságokat és mezőket az elemzés attribútumok hasonló vissza egy a parancsmag osztály vagy egy [System.Management.Automation.Runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) objektum.

Ez a alapvető szolgáltató nem bírálja felül ezt a módszert. Az alábbi kód azonban ez a módszer alapértelmezett megvalósítását mutatja be:

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesaccessdbprov01#accessdbprov01ProviderDynamicParameters](Msh_samplesaccessdbprov01#accessdbprov01ProviderDynamicParameters)]  -->

## <a name="uninitializing-the-provider"></a>A szolgáltató uninitializing

Az ingyenes erőforrásokat, amelyek a Windows PowerShell-szolgáltató használ, a szolgáltatóhoz meg kell valósítania a saját [System.Management.Automation.Provider.Cmdletprovider.Stop*](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Stop) metódust. Ezt a módszert hívja meg a Windows PowerShell futtatási meghívná a szolgáltató egy munkamenet lezárásakor.

Ez a alapvető szolgáltató nem bírálja felül ezt a módszert. Az alábbi kód azonban ez a módszer alapértelmezett megvalósítását mutatja be:

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplesaccessdbprov01#accessdbprov01ProviderStop](Msh_samplesaccessdbprov01#accessdbprov01ProviderStop)]  -->

## <a name="code-sample"></a>Kódminta

Teljes minta kódja, lásd: [AccessDbProviderSample01 kódminta](./accessdbprovidersample01-code-sample.md).

## <a name="testing-the-windows-powershell-provider"></a>A Windows PowerShell-szolgáltatóban tesztelése

Ha a Windows PowerShell-szolgáltató regisztrálva van a Windows PowerShell-lel, tesztelheti a támogatott parancsmagok futtatásával a parancssorban. Ez a alapvető szolgáltató, indítsa el az új and use a `Get-PSProvider` parancsmaggal szolgáltatók listájának beolvasása, és győződjön meg arról, hogy megtalálható-e a AccessDb szolgáltató.

```powershell
Get-PSProvider
```

A következő eredmény jelenik meg:

```output
Name                 Capabilities                  Drives
----                 ------------                  ------
AccessDb             None                          {}
Alias                ShouldProcess                 {Alias}
Environment          ShouldProcess                 {Env}
FileSystem           Filter, ShouldProcess         {C, Z}
Function             ShouldProcess                 {function}
Registry             ShouldProcess                 {HKLM, HKCU}
```

## <a name="see-also"></a>Lásd még:

[Windows PowerShell-szolgáltató létrehozása](./how-to-create-a-windows-powershell-provider.md)

[A Windows PowerShell-szolgáltató tervezése](./designing-your-windows-powershell-provider.md)