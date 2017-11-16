---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: PowerShell parancsmag
ms.date: 2016-12-12
title: "pswaauthorizationrule hozzáadása"
ms.technology: powershell
schema: 2.0.0
ms.openlocfilehash: 18422f71b2a5f9af07af94e4324d3c7774f1d5ea
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="add-pswaauthorizationrule"></a>Add-PswaAuthorizationRule

## <a name="synopsis"></a>ÖSSZEGZÉST

Új engedélyezési szabály hozzáadása a Windows PowerShell® Web Access engedélyezési szabályok készletéhez.

## <a name="syntax"></a>Szintaxis

### <a name="usergroupnamecomputergroupname"></a>UserGroupNameComputerGroupName
```
Add-PswaAuthorizationRule -ComputerGroupName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usergroupnamecomputername"></a>UserGroupNameComputerName
```
Add-PswaAuthorizationRule -ComputerName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputergroupname"></a>UserNameComputerGroupName
```
Add-PswaAuthorizationRule [-UserName] <String[]> -ComputerGroupName <String> -ConfigurationName <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputername"></a>UserNameComputerName
```
Add-PswaAuthorizationRule [-UserName] <String[]> [-ComputerName] <String> [-ConfigurationName] <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

## <a name="description"></a>LEÍRÁS

A **Add-PswaAuthorizationRule** parancsmag új felhatalmazási szabály hozzáadása a Windows PowerShell® Web Access engedélyezési szabályok készletéhez.

A felhasználók, számítógépek és a szabály a Windows PowerShell végpontokat kell megadnia. Megadhatja a felhasználók és számítógépek egyes felhasználói fiókok és a számítógép nevét, vagy csoportok megadása.

Egy számítógép, amely egy Active Directory-tartományhoz csatlakozik a parancsmag a szabály létrehozásához használ a számítógép biztonsági azonosítóját (SID).
Ez lehetővé teszi, hogy egy rövid nevet, egy teljesen minősített tartománynevét (FQDN) vagy IP-címet a **számítógépnév** mezőjét a bejelentkezési oldalon.

Egy számítógép, amely nem csatlakozik egy Active Directory-tartomány a parancsmag a szabály a számítógép nevét, a rendszergazda által biztosított segítségével hoz létre. Sikeres csatlakozás a számítógéphez, hogy a végfelhasználó biztosítania kell a számítógép neve pontosan, ahogyan az a szabály megjelenik.

Ha több számítógépet, ezzel a névvel, a hálózaton, rövid neve egynél több számítógép tudja oldani. Ez vezethet kétértelműség egy kapcsolat. Például, ha a szabály létezik a munkacsoportban működő számítógép nevű "*kiszolgáló1*" és nevű új számítógép *server1.contoso.com* csatlakozik a hálózathoz, az engedélyezési szabályok segítségével érvényesítés sikeres, és A Windows PowerShell Web Access megkísérli a kapcsolatot a következő nevű számítógépet "*kiszolgáló1*". Nem garantált, hogy a kapcsolatot létesíteni a megadott munkacsoportban működő számítógép; a kísérlet sikerült meg a workgroup vagy a nevű számítógépet "*kiszolgáló1*". Kétértelműség csökkentése érdekében javasoljuk, hogy a célszámítógép, amikor csak lehetséges az engedélyezési szabály létrehozásához használja a teljes Tartománynevet.

Az engedélyezési szabályok kiértékelése elsődleges bejelentkezési hitelesítő adatait a Windows PowerShell Web Access a felhasználók nem a másodlagos hitelesítő (hitelesítő adatok a második készlet megtalálható a **választható csatlakozási beállítások** szakasza a bejelentkezési oldal). Példa erre lásd: Példa 6.

## <a name="parameters"></a>Paraméterek

### <a name="-computergroupnameltstringgt"></a>-ComputerGroupName&lt;karakterlánc&gt;

Adja meg egy számítógépcsoport nevét, amelyhez ez a szabály engedélyezi a hozzáférést az Active Directory tartományi szolgáltatások (AD DS) vagy helyi csoportot.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByPropertyName)                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-computernameltstringgt"></a>-ComputerName&lt;karakterlánc&gt;

A számítógép neve, amelyhez ez a szabály engedélyezi a hozzáférést.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByPropertyName)                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-configurationnameltstringgt"></a>-ConfigurationName&lt;karakterlánc&gt;

Megadja a nevét, a Windows PowerShell munkamenet-konfiguráció, más néven futási térből, amelyhez ez a szabály engedélyezi a hozzáférést.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByPropertyName)                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-credentialltpscredentialgt"></a>-Credential&lt;PSCredential&gt;

Megadja a **PSCredential** objektum, amely a Windows PowerShell Web Access engedélyezési szabályok módosítása használni kívánt felhasználói fiók. Ha nem adja hozzá ezt a paramétert, a parancsmag használja az aktuálisan bejelentkezett felhasználói fiók. A beolvasandó egy **PSCredential** objektum, amely pedig szükséges, adja hozzá az engedélyezési szabályok távolról, futtassa a [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) parancsmag.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-force"></a>-Force

A felhasználó jóváhagyásának kérése nélkül futtatja a parancsot. \
Ezenkívül rendszer is kérni fogja a megerősítő egy egyszerű vagy rövid számítógép nevét (például a nevet, amely nem egy tartománynevet vagy nincs teljesen minősített) beírásakor. Jóváhagyás biztonsági okokból van szükség, hogy az egyszerű név segítségével adja hozzá a számítógépet, csak ha a számítógép egy munkacsoport.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-rulenameltstringgt"></a>-RuleName&lt;karakterlánc&gt;

Megadja a szabály rövid nevét.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByPropertyName)                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-usergroupnameltstringgt"></a>-UserGroupName&lt;karakterlánc\[\]&gt;

Megadja egy vagy több felhasználói csoport nevét az AD DS vagy helyi csoportot, amelyhez ez a szabály engedélyezi a hozzáférést.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByPropertyName)                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-usernameltstringgt"></a>-UserName&lt;karakterlánc\[\]&gt;

Itt adhatja meg, amelyhez ez a szabály engedélyezi a hozzáférést egy vagy több felhasználó. A felhasználónév lehet egy helyi felhasználói fiók az átjáró számítógépre vagy egy felhasználót az Active Directory tartományi Szolgáltatásokban.
A formátum `domain\user` vagy `computer\user`.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | 1                                    |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByValue, ByPropertyName)       |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="ltcommonparametersgt"></a>&lt;Általánosparaméterek&gt;

Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.
További információkért lásd: [about_CommonParameters](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).

## <a name="inputs"></a>BEMENETEK

### <a name="string"></a>Karakterlánc

Ez a parancsmag egy karakterláncot vagy karakterláncok fogad el bemenetként.

### <a name="string"></a>Karakterlánc\[\]

Ez a parancsmag egy karakterláncot vagy karakterláncok fogad el bemenetként.

## <a name="outputs"></a>Kimenetek

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule

Ez a parancsmag adja vissza az engedélyezési szabály objektum.

## <a name="examples"></a>PÉLDÁK

### <a name="example-1"></a>1. PÉLDA

Ez a példa engedélyezi a hozzáférést a munkamenet-konfigurációjához *PSWAEndpoint*, egy korlátozott futási térrel, *KISZ2* lévő felhasználók számára a *SMAdmins* csoport. \
**Megjegyzés:**: A számítógép nevét egy teljesen minősített tartománynevét (FQDN) kell lennie. A rendszergazdák egy korlátozott munkamenet-konfiguráció vagy a parancsmagok és a végfelhasználók futtatott feladatok korlátozott tartománya futási térben határozza meg. Egy korlátozott futási térrel definiálása megakadályozhatja a felhasználók hozzáférhessenek más számítógépekhez, amely nem áll az engedélyezett Windows PowerShell® térben, így rendelkezésre több biztonságos kapcsolatot. A munkamenet-konfigurációk további információkért lásd: [about_session_configuration_files](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) vagy a [telepítése és használata a Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).

```PowerShell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a>2. PÉLDA

Ebben a példában az alapértelmezett Windows PowerShell munkamenet-konfiguráció, hozzáférést biztosít a `Microsoft.PowerShell`a *KISZ2* a felhasználók számára a felhasználókhoz, contoso nevű\\felhasználó1, contoso\\felhasználó2, és a contoso\\Felhasználó3. Ez a parancsmag három szabályokat (1 / személy) hoz létre.

```PowerShell
Add-PswaAuthorizationRule –UserName contoso\user1, contoso\user2, contoso\user3 –ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a>3. PÉLDA

Ez a példa bemutatja, hogyan a felhasználótól, felhasználói név értékek keresztül a feldolgozási sor.

```
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule –ComputerName srv2.contoso.com –ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a>4. PÉLDA

Ez a példa bemutatja, hogyan minden paraméter láncból értékek tegye meg a tulajdonság nevét.

````PowerShell
$o = New-Object -TypeName PSObject | 
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru | 
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru | 
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" –PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a>5. PÉLDA

Ebben a példában a szabály nevű a helyi felhasználó hozzáadása *PswaServer\\ChrisLocal* nevű kiszolgálóra való hozzáférés *srv1.contoso.com*.

Ez a példa bemutatja, egy olyan forgatókönyvet, amelyben az átjáró a munkacsoport és a célszámítógép tartományban van. Az engedélyezési szabály vonatkozik a helyi felhasználók az átjárón. A Windows PowerShell Web Access bejelentkezési oldal, a sikeres hitelesítést végezni, a felhasználónak meg kell adnia egy második együttesét a hitelesítő adatokat a **választható csatlakozási beállítások** területen. Az átjárókiszolgáló használ a további hitelesítő adatok hitelesíteni a felhasználót a célszámítógépen, a kiszolgáló nevű *srv1.contoso.com*.

````
Add-PswaAuthorizationRule –UserName PswaServer\ChrisLocal –ComputerName srv1.contoso.com –ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a>6. PÉLDA

Ebben a példában minden végpontok hozzáférést biztosít minden felhasználó az összes olyan számítógépen.
Ez lényegében kikapcsolja az engedélyezési szabályok. \
**Megjegyzés:**: használja a `*` helyettesítő karakter használata nem ajánlott a biztonsági szempontból kényes központi telepítések és csak kell figyelembe venni a tesztkörnyezetek vagy központi telepítések szerepel, ahol a biztonsági mérsékelhető.

````PowerShell
Add-PswaAuthorizationRule –UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a>Lásd még:

- [Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)
- [Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)
- [Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)
- [Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)
- [Tag hozzáadása](http://go.microsoft.com/fwlink/p/?LinkId=113280)
- [Új objektum](http://go.microsoft.com/fwlink/p/?LinkId=113355)
- [A GET-Credential parancsmag](http://go.microsoft.com/fwlink/?LinkID=293936)
