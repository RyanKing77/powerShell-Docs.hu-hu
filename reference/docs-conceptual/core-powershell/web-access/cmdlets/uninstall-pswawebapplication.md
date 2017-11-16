---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: PowerShell parancsmag
ms.date: 2016-12-12
title: "Távolítsa el a pswawebapplication"
ms.technology: powershell
ms.openlocfilehash: 5fe608b3bfbb90f842f16c1f5a8c51879589cf6d
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="uninstall-pswawebapplication"></a>Távolítsa el PswaWebApplication

## <a name="synopsis"></a>ÖSSZEGZÉST

Eltávolítja a Windows PowerShell® webalkalmazás.

## <a name="syntax"></a>SZINTAXIS

### <a name="default"></a>Alapértelmezett
```
Uninstall-PswaWebApplication [[-WebApplicationName] <String> ] [-DeleteTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>LEÍRÁS

A **Uninstall-PswaWebApplication** parancsmag eltávolítja a Windows PowerShell-webalkalmazáshoz, és eltávolítja a webhely az IIS. A parancsmag nem távolítja el az IIS vagy bármely más, mert nem voltak Windows PowerShell futtatásához szükséges telepített szolgáltatások.

## <a name="parameters"></a>PARAMÉTEREK

### <a name="-deletetestcertificate"></a>-DeleteTestCertificate

Azt jelzi, hogy a teszt tanúsítványok által a **telepítése\_PswaWebApplication** parancsmag (az a **UseTestCertificate** paraméter) törlődik.
Csak a tanúsítvány azonos nevű megegyezik a hozta létre a **Install-PswaWebApplication** parancsmag törlődik.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | Igaz                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-webapplicationname-ltstringgt"></a>-WebApplicationName &lt;karakterlánc&gt;

A webes alkalmazás eltávolítása a nevét adja meg.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | 1                                    |
| Alapértelmezett érték                        | pswa                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-websitename-ltstringgt"></a>-WebSiteName &lt;karakterlánc&gt;

Megadja a nevét, a webhely, ahol a webes alkalmazás telepítve van.

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

Ez a parancsmag nem-kimenet visszaadása.

## <a name="examples"></a>PÉLDÁK

### <a name="example-1"></a>1. PÉLDA

Ez a parancs eltávolítja a Windows PowerShell webalkalmazás.
Ez a parancsmag segítségével távolítsa el a Windows PowerShell webalkalmazás, ha telepítette az alapértelmezett értékekkel.

```PowerShell
Uninstall-PswaWebApplication
```

### <a name="example-2"></a>2. PÉLDA

A parancs eltávolítja a Windows PowerShell webalkalmazás, és törli az alkalmazáshoz kapcsolódó teszttanúsítványt.
Ez a parancsmag segítségével távolítsa el a Windows PowerShell webalkalmazás, ha telepítették őket az alapértelmezett értékekkel, és létrehozott egy teszttanúsítványt.

```PowerShell
Uninstall-PswaWebApplication -DeleteTestCertificate
```

### <a name="example-3-example-3-subheading"></a>{#Example-3 .subHeading} 3. példa

Ez a parancs eltávolítja a Windows PowerShell webalkalmazás, ha egy egyéni webhelyet és alkalmazást a telepítés során megadott.
A parancs eltávolítja a webhely nevű *saját webhely* és a nevű alkalmazást *Tesztalkalmazás kategóriában* és megadja, hogy a teszt tanúsítványokat, az alkalmazással társított is törlődnek.

```
Uninstall-PswaWebApplication -WebApplicationName TestApplication -WebsiteName MySite -DeleteTestCertificate
```

## <a name="related-topics"></a>Kapcsolódó témakörök

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Install-PswaWebApplication](install-pswawebapplication.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)
