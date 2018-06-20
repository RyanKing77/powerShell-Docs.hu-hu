---
ms.topic: reference
keywords: PowerShell parancsmag
ms.date: 12/12/2016
title: Remove-PswaAuthorizationRule
ms.openlocfilehash: 6a3720bb9b8df3e1c6bb9f4a6196c9868b85b67d
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189033"
---
# <a name="remove-pswaauthorizationrule"></a>Remove-PswaAuthorizationRule

## <a name="synopsis"></a>SYNOPSIS

A megadott engedélyezési szabály eltávolítása a Windows PowerShell® Web Access.

## <a name="syntax"></a>SZINTAXIS

### <a name="id"></a>Id
```
Remove-PswaAuthorizationRule [-Id] <Int32[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

### <a name="rule"></a>A szabály
```
Remove-PswaAuthorizationRule [-Rule] <PswaAuthorizationRule[]> [-Force] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a>LEÍRÁS

A megadott engedélyezési szabály eltávolítása a Windows PowerShell Web Access.

## <a name="parameters"></a>PARAMÉTEREK

### <a name="-force"></a>-Force

A parancsmagot futtatja a jóváhagyás kérése nélkül. Alapértelmezés szerint a parancsmag a folytatás előtt megerősítést kér.

|||
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | nevű                                |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | hamis                                |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-id-ltint32gt"></a>-Id &lt;Int32\[\]&gt;

Megadja a azonosítói (azonosítók) egy vagy több szabály eltávolításához.

|||
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | 2                                    |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByValue, ByPropertyName)       |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a>-Szabály &lt;PswaAuthorizationRule\[\]&gt;

Megadja a szabály eltávolítása.

|||
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | 2                                    |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByValue)                       |
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

Bemutatja, mi történne a parancsmag futtatásakor. A parancsmag nem fut.

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

### <a name="int"></a>int\[\]

Ez a parancsmag fogad el, vagy egy számokból álló tömb, vagy PswaAuthorizationRule objektumokból álló tömb.

### <a name="pswaauthorizationrule"></a>PswaAuthorizationRule\[\]

Ez a parancsmag fogad el, vagy egy számokból álló tömb, vagy PswaAuthorizationRule objektumokból álló tömb.

## <a name="outputs"></a>KIMENETEK

Ez a parancsmag nem kimenetet hoz létre.

## <a name="examples"></a>PÉLDÁK

### <a name="example-1"></a>1. PÉLDA

Ez a példa eltávolítja az engedélyezési szabály azonosítójú *2*.

```
Remove-PswaAuthorizationRule –Id 2
```

### <a name="example-2-example-2-subheading"></a>{#Example-2 .subHeading} 2. példa

Ez a példa eltávolítja az összes engedélyezési szabályt, és is az a felhasználó jóváhagyást igényel.

```
Get-PswaAuthorizationRule | Remove-PswaAuthorizationRule -Confirm
```

## <a name="related-topics"></a>Kapcsolódó témakörök

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Install-PswaWebApplication](install-pswawebapplication.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)