---
description: 
ms.topic: article
ms.prod: powershell
keywords: PowerShell parancsmag
ms.date: 2016-12-12
title: test-pswaauthorizationrule
ms.technology: powershell
ms.openlocfilehash: fb2937397616160c70b056e412e42fb8ff4c2f27
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="test-pswaauthorizationrule"></a>Test-PswaAuthorizationRule

## <a name="synopsis"></a>SYNOPSIS

Ellenőrzi, hogy létezik-e szabály egy adott felhasználó, számítógép vagy végpont.

## <a name="syntax"></a>SZINTAXIS

### <a name="computername"></a>ComputerName
```
Test-PswaAuthorizationRule [-UserName] <String> [-ComputerName] <String> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

### <a name="connectionuri"></a>ConnectionUri
```
Test-PswaAuthorizationRule [-UserName] <String> [-ConnectionUri] <Uri> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

## <a name="description"></a>LEÍRÁS

A **Test-PswaAuthorizationRule** parancsmag ellenőrzi, hogy létezik-e szabály egy adott felhasználó, számítógép vagy végpont.
Ez a parancsmag is használható engedélyezési szabályokat, ellenőrizze, hogy engedélyezve van-e egy adott felhasználó, számítógép vagy a végpont a hozzáférési kérelem teszteléséhez.
Alapértelmezés szerint ez a parancsmag a hitelesítési fájlhoz az összes szabályt kiértékeli.
A vizsgálandó szabályok részhalmazát is megadhat.

Ez a parancsmag segítségével hitelesítési hibák elhárítása.

Ez a parancsmag paramétereit felel meg a Windows PowerShell® Web Access bejelentkezési oldalra mezőket.

## <a name="parameters"></a>PARAMÉTEREK

### <a name="-computername-ltstringgt"></a>-ComputerName &lt;karakterlánc&gt;

Adja meg a vizsgálandó számítógép nevét.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | 2                                    |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-configurationname-ltstringgt"></a>-ConfigurationName &lt;karakterlánc&gt;

Megadja a nevét, a Windows PowerShell munkamenet-konfiguráció, más néven a végpont vagy a futási térből, teszteléséhez.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | 3                                    |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-connectionuri-lturigt"></a>-ConnectionUri &lt;Uri&gt;

Megadja a kapcsolat tesztelése URI.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | 2                                    |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-credential-ltpscredentialgt"></a>-Credential &lt;PSCredential&gt;

Megadja a **PSCredential** egy felhasználói fiókot, amely a Windows PowerShell Web Access engedélyezési szabályok teszteléséhez használni kívánt objektumot. Ha nem adja hozzá ezt a paramétert, a parancsmag használja az aktuálisan bejelentkezett felhasználói fiók. A beolvasandó egy **PSCredential** objektum, amely pedig szükséges engedélyezési szabályok távolról tesztelése, futtassa a [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936) parancsmag.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a>-Szabály &lt;PswaAuthorizationRule\[\]&gt;

Megadja a teszteléséhez szabályok részhalmazát. Ha ez a paraméter nincs megadva, majd a teszteli, szemben az összes engedélyezési szabályt.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByValue)                       |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-username-ltstringgt"></a>-UserName &lt;karakterlánc&gt;

Megadja a tesztelni kívánt felhasználó nevét.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | 1                                    |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="ltcommonparametersgt"></a>&lt;Általánosparaméterek&gt;

Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.
További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>BEMENETEK

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]

Ez a parancsmag PswaAuthorizationRule objektumokból álló tömb fogad el bemenetként.

## <a name="outputs"></a>KIMENETEK

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]

Ez a parancsmag kimeneteként hoz létre PswaAuthorizationRule objektumokból álló tömb.

## <a name="examples"></a>EXAMPLES

### <a name="example-1"></a>1. PÉLDA

Ebben a példában minden engedélyezési szabályok teszteli a szabályok, amelyek lehetővé teszik a felhasználó megjelenítéséhez *contoso\\mhanson* kapcsolódni a számítógéphez *KISZ2* és a Windows PowerShell-munkamenetet használjon nevű *tesztelése*.

```
Test-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserName contoso\mhanson -ConfigurationName test
```

### <a name="example-2"></a>2. PÉLDA

A példa tesztek összes engedélyezési szabályokat, hogy ellenőrizze, melyik engedélyezési szabályok vonatkoznak a felhasználói *contoso\\mhanson*.

```
Test-PswaAuthorizationRule -UserName contoso\mhanson -ComputerName *
```

## <a name="related-topics"></a>Kapcsolódó témakörök

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Install-PswaWebApplication](install-pswawebapplication.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
