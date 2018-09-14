---
ms.topic: reference
keywords: PowerShell, a parancsmag
ms.date: 12/12/2016
title: Add-PswaAuthorizationRule
schema: 2.0.0
ms.openlocfilehash: fe2b71dcfa870ba3f92484ae3fd3c45b3107a1bc
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523079"
---
# <a name="add-pswaauthorizationrule"></a>Add-PswaAuthorizationRule

## <a name="synopsis"></a>SYNOPSIS

Új engedélyezési szabályt ad hozzá a Windows PowerShell-elérés engedélyezési szabályok készletéhez.

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

A **Add-PswaAuthorizationRule** parancsmag új engedélyezési szabályt ad a Windows PowerShell(r) webes elérés engedélyezési szabályok készletéhez.

Adjon meg a felhasználók, számítógépek és Windows PowerShell-végpontok ehhez a szabályhoz. Megadhatja a felhasználók és a számítógépek vagy egyéni felhasználói fiókokhoz és a számítógépek nevét, vagy csoport megadásával.

Az Active Directory-tartományhoz csatlakozó számítógépen a parancsmag használatával a számítógép biztonsági azonosítója (SID) hozza létre a szabályt. Ez lehetővé teszi, hogy egy rövid nevet, egy teljesen minősített tartománynevét (FQDN) vagy IP-címet a **számítógépnév** mezőt a bejelentkezési oldalon.

Az Active Directory-tartományhoz nem csatlakozó számítógépek esetében a parancsmag a szabály a számítógép nevét, a rendszergazda által biztosított használatával hoz létre. A sikeres csatlakozás a számítógéphez, a végfelhasználónak kell megadni a számítógép nevét, pontosan megegyezzen a szabályban.

Ha több számítógépet, ezzel a névvel, a hálózaton, majd rövid, nevet képes legyen feloldani egynél több számítógép. Ez vezethet félreérthetőség-kapcsolat létrehozásakor. Például, ha egy szabály létezik a munkacsoport-számítógép neve "*kiszolgáló1*" és a egy új számítógép nevű *server1.contoso.com* csatlakozik a hálózathoz, az engedélyezési szabályok használatával érvényesítés sikeres, és Windows PowerShell-elérés próbál egy kapcsolatot a számítógép neve "*kiszolgáló1*". Nem garantált, hogy a kapcsolatot létesíteni a megadott munkacsoporthoz tartozó számítógépet; a kísérlet sikerült elvégezni a workgroup vagy a tartományi számítógép neve "*kiszolgáló1*". A többértelműség csökkentése érdekében, javasoljuk, hogy a célként megadott számítógéphez, amikor csak lehetséges, egy olyan engedélyezési szabály létrehozása a teljes Tartománynevet használja.

Az engedélyezési szabályok kiértékelése elsődleges bejelentkezési hitelesítő adatait a Windows PowerShell-elérés felhasználók, nem a másodlagos hitelesítő adatokat (a második hitelesítő adatok található a **választható csatlakozási beállítások** szakaszában a bejelentkezési oldalon). Példa erre tekintse meg a példában 6.

## <a name="parameters"></a>Paraméterek

### <a name="-computergroupname-string"></a>-ComputerGroupName \<karakterlánc\>

Egy számítógépcsoport nevét adja meg az Active Directory Domain Services (AD DS) vagy a helyi csoport, amelyhez ez a szabály engedélyezi a hozzáférést.

|||
|-|-|
| Aliasok                     | nincs                  |
| Kötelező?                   | Igaz                  |
| Pozíció?                   | nevű                 |
| Alapértelmezett érték               | nincs                  |
| Láncbemenet fogadása?      | Igaz (ByPropertyName) |
| Helyettesítő karakterek elfogadása? | hamis                 |

### <a name="-computername-string"></a>-ComputerName \<karakterlánc\>

A számítógép neve, amelyhez ez a szabály engedélyezi a hozzáférést.

|||
|-|-|
| Aliasok                     | nincs                  |
| Kötelező?                   | Igaz                  |
| Pozíció?                   | nevű                 |
| Alapértelmezett érték               | nincs                  |
| Láncbemenet fogadása?      | Igaz (ByPropertyName) |
| Helyettesítő karakterek elfogadása? | hamis                 |

### <a name="-configurationname-string"></a>-ConfigurationName \<karakterlánc\>

A neve, a Windows PowerShell munkamenet-konfiguráció, más néven futási térből, amelyhez ez a szabály engedélyezi a hozzáférést.

|||
|-|-|
| Aliasok                     | nincs                  |
| Kötelező?                   | Igaz                  |
| Pozíció?                   | nevű                 |
| Alapértelmezett érték               | nincs                  |
| Láncbemenet fogadása?      | Igaz (ByPropertyName) |
| Helyettesítő karakterek elfogadása? | hamis                 |

### <a name="-credential--pscredential"></a>-Credential \<PSCredential\>

Megadja egy **PSCredential** egy felhasználói fiók segítségével módosíthatja a Windows PowerShell-elérés engedélyezési szabályai kívánt objektumot. Ha nem adja hozzá ezt a paramétert, a parancsmag jelenleg bejelentkezett felhasználói fiókot használja. Az első egy **PSCredential** objektum, amely a szükséges, adja hozzá az engedélyezési szabályok távolról, futtassa a [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) parancsmag.

|||
|-|-|
| Aliasok                     | nincs  |
| Kötelező?                   | hamis |
| Pozíció?                   | nevű |
| Alapértelmezett érték               | nincs  |
| Láncbemenet fogadása?      | hamis |
| Helyettesítő karakterek elfogadása? | hamis |

### <a name="-force"></a>-Force

Kikényszeríti a parancs futtatását a felhasználó jóváhagyásának kérése nélkül. Emellett azt is kérni fogja megerősítő (például olyan nevet, amely nem egy tartomány nevét, vagy nem teljesen minősített) egyszerű vagy rövid számítógép nevének megadásakor. Megerősítő biztonsági okokból kérik, hogy a számítógép hozzáadása, csak ha a számítógép egy munkacsoporthoz tartozik, az egyszerű nevet használhat.

|||
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-rulename-string"></a>-RuleName \<karakterlánc\>

Megadja a szabály rövid nevét.

|||
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByPropertyName)                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-usergroupname-string"></a>-UserGroupName \<karakterlánc\[\]\>

Adja meg egy vagy több felhasználói csoport neve az Active Directory tartományi szolgáltatások vagy helyi csoport, amelyhez ez a szabály engedélyezi a hozzáférést.

|||
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByPropertyName)                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-username-string"></a>-UserName \<karakterlánc\[\]\>

Itt adhatja meg, amelyhez ez a szabály engedélyezi a hozzáférést egy vagy több felhasználó. A felhasználónév az átjáró-számítógép vagy az AD DS-ben a felhasználó helyi felhasználói fiók is lehet. A formátum `domain\user` vagy `computer\user`.

|||
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | 1                                    |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByValue, ByPropertyName)       |
| Helyettesítő karakterek elfogadása?          | hamis                                |

###  <a name="commonparameters"></a>\<CommonParameters\>

Ez a parancsmag a következő általános paramétereket támogatja:

-Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer és -OutVariable.
További információkért lásd: [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).

## <a name="inputs"></a>BEMENETEK

### <a name="string"></a>Sztring

Ez a parancsmag egy karakterláncot vagy karakterláncok tömbje fogad el bemenetként.

### <a name="string"></a>Karakterlánc\[\]

Ez a parancsmag egy karakterláncot vagy karakterláncok tömbje fogad el bemenetként.

## <a name="outputs"></a>Kimenetek

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule

Ez a parancsmag adja vissza az engedélyezési szabály objektum.

## <a name="examples"></a>PÉLDÁK

### <a name="example-1"></a>1. PÉLDA

Ebben a példában hozzáférést biztosít a munkamenet-konfiguráció _PSWAEndpoint_, amely egy korlátozott futási térrel, _srv2_ lévő felhasználók számára a _SMAdmins_ csoport.

> [!NOTE]
> A számítógép nevét egy teljesen minősített tartománynevét (FQDN) kell lennie. A rendszergazdák egy korlátozott munkamenet-konfiguráció vagy a futási térből, amely a parancsmagok és a végfelhasználók futtatható feladatok korlátozott tartománya határozza meg. Korlátozott futási térrel definiálása megakadályozhatja a felhasználók más számítógépekhez, amelyek nem engedélyezett Windows PowerShell(r) a futási térben található, így több biztonságos kapcsolatot. A munkamenet-konfigurációk további információkért lásd: [about_Session_Configurations](/powershell/module/microsoft.powershell.core/about/about_session_configurations) vagy [telepítése és használata Windows PowerShell-elérés](../install-and-use-windows-powershell-web-access.md).

```powershell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a>2. PÉLDA

Ebben a példában hozzáférést biztosít az alapértelmezett Windows PowerShell-munkamenet konfigurációk, `Microsoft.PowerShell`, a *srv2* a felhasználók számára az nevű felhasználók `contoso\user1`, `contoso\user2`, és `contoso\user3`. Ez a parancsmag három szabályokat (1 / személy) hoz létre.

```powershell
Add-PswaAuthorizationRule -UserName contoso\user1, contoso\user2, contoso\user3 -ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a>3. PÉLDA

Ez a példa szemlélteti, hogyan bemeneti felhasználói név értékek keresztül a folyamat.

```powershell
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule -ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a>4. PÉLDA

Ez a példa bemutatja, hogy minden paraméter értékeit folyamat igénybe tulajdonság neve.

````powershell
$o = New-Object -TypeName PSObject |
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru |
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru |
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" -PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a>5. PÉLDA

Ez a példa hozzáad egy szabályt, amely engedélyezi a helyi felhasználó nevű `PswaServer\ChrisLocal` nevű kiszolgálóra való hozzáférés **srv1.contoso.com**.

Ebben a példában egy forgatókönyvet, ahol az átjáró egy munkacsoporthoz tartozik, és a célszámítógép egy tartományhoz tartozik mutatja be. Az átjáró a helyi felhasználók az engedélyezési szabály vonatkozik. A bejelentkezési lapon Windows PowerShell-elérés e sikeres hitelesítést végezni, a felhasználónak meg kell adnia a hitelesítő adatokat egy második együttesét a **választható csatlakozási beállítások** területen. Az átjáró-kiszolgálót a további hitelesítő adatokat használja a célszámítógépen, a kiszolgáló neve a felhasználó hitelesítésére *srv1.contoso.com*.

````powershell
Add-PswaAuthorizationRule -UserName PswaServer\ChrisLocal -ComputerName srv1.contoso.com -ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a>6. PÉLDA

Ebben a példában engedélyezi az összes felhasználó összes végponthoz való hozzáférést az összes számítógépen. Ez lényegében kikapcsolja az engedélyezési szabályok.

> [!NOTE]
> Használja a `*` helyettesítő karakter biztonsági szempontból kényes központi telepítések esetében nem javasolt, és csak tesztkörnyezetekhez tekinthető, vagy el kell telepítések esetén használják, ahol csökkenthető a biztonsági.

````powershell
Add-PswaAuthorizationRule -UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a>Lásd még:

[Get-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592891(v=wps.630).aspx)

[Remove-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592893(v=wps.630).aspx)

[Test-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592892(v=wps.630).aspx)

[Install-PswaWebApplication](https://technet.microsoft.com/library/jj592894(v=wps.630).aspx)

[Tag hozzáadása](http://go.microsoft.com/fwlink/p/?LinkId=113280)

[New-Object](http://go.microsoft.com/fwlink/p/?LinkId=113355)

[Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936)
