---
description: 
ms.topic: article
ms.prod: powershell
keywords: PowerShell parancsmag
ms.date: 2016-12-12
title: "pswawebapplication telepítése"
ms.technology: powershell
ms.openlocfilehash: ce4d01fbe8a83924e7023d792c68c903a32e07d4
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="install-pswawebapplication"></a>Install-PswaWebApplication

## <a name="synopsis"></a>SYNOPSIS

A Windows PowerShell® Web Access webalkalmazás konfigurálja az IIS-ben.

## <a name="syntax"></a>SZINTAXIS

### <a name="default"></a>Alapértelmezett
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>LEÍRÁS

A **Install-PswaWebApplication** parancsmag konfigurálja a Windows PowerShell Web Access webes alkalmazást. Ez a parancsmag telepíti a webalkalmazás, társítja azt egy webhely, és választhatóan egy teszt SSL tanúsítvány használata a **useTestCertificate** paraméter. Biztonsági okokból webes rendszergazdák ne használjon egy teszttanúsítványt éles környezetekben.

## <a name="parameters"></a>PARAMÉTEREK

### <a name="-usetestcertificate"></a>-UseTestCertificate

Meghatározza, hogy létrejött-e egy teszttanúsítványt. Ha a paraméter értéke igaz, akkor ez a parancsmag létrehoz egy tesztelési tanúsítványt, és konfigurálja a Windows PowerShell Web Access webalkalmazás használhassa a tanúsítványt a HTTPS-kéréseket. Ha ez a paraméter false értékre van beállítva, akkor nincs tanúsítvány vagy a kötés jön létre. Állítsa be ezt az értéket az hamis, ha a Windows PowerShell Web Access egy másik tanúsítvánnyal.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | Igaz                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-webapplicationnameltstringgt"></a>-WebApplicationName&lt;String&gt;

Megadja a webalkalmazás nevét. Ez a Windows PowerShell Web Access URL-cím utolsó részeként jelenik meg.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | 1                                    |
| Alapértelmezett érték                        | pswa                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-websitenameltstringgt"></a>-WebSiteName&lt;String&gt;

Adja meg a webkiszolgáló (IIS) webhely telepítéséhez a Windows PowerShell Web Access webes alkalmazás neve.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | Alapértelmezett webhely                     |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-confirm"></a>-Confirm

Jóváhagyást kér a parancsmag futtatása előtt.

|||  
|-|-|
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | hamis                                |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-whatif"></a>-WhatIf

Bemutatja, mi történne a parancsmag futtatásakor.
A parancsmag nem fut.

|||  
|-|-|
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | hamis                                |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="ltcommonparametersgt"></a>&lt;Általánosparaméterek&gt;

Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.
További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>BEMENETEK

Ez a parancsmag nem bemenetből fogad adatokat.

## <a name="outputs"></a>KIMENETEK

Ez a parancsmag nem kimenetet hoz létre.

## <a name="examples"></a>EXAMPLES

### <a name="example-1"></a>1. PÉLDA

Ebben a példában a PSWA webes alkalmazás alapértelmezett értékeinek használatával telepíti a **WebApplicationName** (*pswa*) és **WebSiteName** (*alapértelmezett webhelyen* ) paraméterek.

```
Install-PswaWebApplication
```

### <a name="example-2"></a>2. PÉLDA

Ebben a példában a PSWA webalkalmazás telepíti egy teszttanúsítványt, és az alapértelmezett értékeit használatával a **WebApplicationName** és **WebSiteName** paraméterek.

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a>Kapcsolódó témakörök

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)
