---
ms.topic: reference
keywords: PowerShell, a parancsmag
ms.date: 12/12/2016
title: Install-PswaWebApplication
ms.openlocfilehash: 29e074b75eeb387640831229c63142e6dd5e991a
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268299"
---
# <a name="install-pswawebapplication"></a>Install-PswaWebApplication

## <a name="synopsis"></a>SYNOPSIS

Konfigurálja a Windows PowerShell-elérés webes alkalmazást az IIS-ben.

## <a name="syntax"></a>SZINTAXIS

### <a name="default"></a>Alapértelmezett
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>LEÍRÁS

A **Install-PswaWebApplication** parancsmag konfigurálja a Windows PowerShell-elérés webes alkalmazást.
Ez a parancsmag telepíti a webalkalmazás, hozzárendeli egy webhely, és igény szerint létrehoz egy tesztelési SSL tanúsítvány használatával a **useTestCertificate** paraméter. Biztonsági okokból a webes rendszergazdák ne használjon egy tesztcélú tanúsítvánnyal az éles környezetekhez.

## <a name="parameters"></a>PARAMÉTEREK

### <a name="-usetestcertificate"></a>-UseTestCertificate

Megadja, hogy létrejött-e egy tesztcélú tanúsítvánnyal. Ha ez a paraméter értéke true, akkor ez a parancsmag létrehoz egy tesztcélú tanúsítvánnyal, és konfigurálja a tanúsítványt használja a HTTPS-kéréseket a Windows PowerShell-elérés webes alkalmazást. Ha ez a paraméter false értékre van állítva, akkor nincs tanúsítvány vagy kötési jön létre. Ha egy másik tanúsítványt használ a Windows PowerShell-elérés "false" értékűre ezt az értéket.

|||
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | Igaz                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-webapplicationname"></a>-WebApplicationName

Megadja a webalkalmazás nevét. Ez a Windows PowerShell Web Access URL-cím utolsó része jelenik meg.

|||
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | 1                                    |
| Alapértelmezett érték                        | pswa                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-websitename"></a>-Webhelynév helyére írja be

Megadja a nevét a webkiszolgáló (IIS) webhely, amelyen a Windows PowerShell-elérés webes alkalmazás telepítéséhez.

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

### <a name="ltcommonparametersgt"></a>&lt;CommonParameters&gt;

Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable. További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>BEMENETEK

Ennél a parancsmagnál nincs bemenet.

## <a name="outputs"></a>KIMENETEK

Ez a parancsmag nem hoz létre kimenetet.

## <a name="examples"></a>PÉLDÁK

### <a name="example-1"></a>1. PÉLDA

Ebben a példában a PSWA webes alkalmazás alapértelmezett értékeinek használatával telepíti a **WebApplicationName** (*pswa*) és **Webhelynév helyére írja be** (*Default Web Site* ) paramétereket.

```
Install-PswaWebApplication
```

### <a name="example-2"></a>2. PÉLDA

Ebben a példában a PSWA webalkalmazás telepítése egy tesztcélú tanúsítvánnyal, és a tartozó alapértelmezett értékeket használ a **WebApplicationName** és **Webhelynév helyére írja be** paramétereket.

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a>Kapcsolódó témakörök

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)