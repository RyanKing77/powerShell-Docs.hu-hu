---
description: 
ms.topic: article
ms.prod: powershell
keywords: PowerShell parancsmag
ms.date: 2016-12-12
title: Get-pswaauthorizationrule
ms.technology: powershell
ms.openlocfilehash: 003195457660a18b9bbed065181b6d8c23835348
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="get-pswaauthorizationrule"></a>Get-PswaAuthorizationRule

## <a name="synopsis"></a>SYNOPSIS

A Windows PowerShell® Web Access-engedélyezési szabályok készletét adja vissza.

## <a name="syntax"></a>Szintaxis

### <a name="id"></a>ID
```
Get-PswaAuthorizationRule [[-Id] <Int32[]> ] [ <CommonParameters>]
```

### <a name="name"></a>Név
```
Get-PswaAuthorizationRule [-RuleName] <String[]> [ <CommonParameters>]
```

## <a name="description"></a>LEÍRÁS

A **Get-PswaAuthorizationRule** parancsmag a Windows PowerShell® Web Access-engedélyezési szabályok készletét adja vissza.
Ha sem a **azonosító** paraméter, sem a **szabálynév** paraméter meg van adva, akkor ez a parancsmag az összes szabályokat sorolja fel. A **azonosító** paraméter használható eredmények szűrésére.

## <a name="parameters"></a>PARAMÉTEREK

### <a name="-idltint32gt"></a>-Id&lt;Int32\[\]&gt;

Adja meg a szabályokat, amelyek ennek a parancsmagnak kell kapnia a azonosítói (azonosítók). Ha nincs azonosítók meg van adva, ennek a parancsmagnak összes engedélyezési szabályt adja vissza.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | hamis                                |
| Pozíció?                            | 2                                    |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByValue, ByPropertyName)       |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="-rulenameltstringgt"></a>-RuleName&lt;String\[\]&gt;

Meghatározza az engedélyezési szabályok beolvasása nevét. Ez a paraméter a szabály a tömb karakterláncok szabály nevének pontosan egyeznie adja vissza.

|||  
|-|-|
| Aliasok                              | nincs                                 |
| Kötelező?                            | Igaz                                 |
| Pozíció?                            | 2                                    |
| Alapértelmezett érték                        | nincs                                 |
| Láncbemenet fogadása?               | Igaz (ByValue, ByPropertyName)       |
| Helyettesítő karakterek elfogadása?          | hamis                                |

### <a name="ltcommonparametersgt"></a>&lt;Általánosparaméterek&gt;

Ez a parancsmag a következő általános paramétereket támogatja:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer és - OutVariable.
További információkért lásd: [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>BEMENETEK

### <a name="int"></a>int\[\]

Ez a parancsmag egy számokból álló tömb vagy karakterlánc-értékek tömbje fogad el bemenetként.

### <a name="string"></a>Karakterlánc\[\]

Ez a parancsmag egy számokból álló tömb vagy karakterlánc-értékek tömbje fogad el bemenetként.

## <a name="outputs"></a>KIMENETEK

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]

Ez a parancsmag kimeneteként hoz létre egy PswaAuthorizationRule objektum.


## <a name="examples"></a>EXAMPLES

### <a name="example-1"></a>1. PÉLDA

Ebben a példában az összes szabály lekérdezi.

```PowerShell
    PS C:\> Get-PswaAuthorizationRule
```

### <a name="example-2"></a>2. PÉLDA

Ebben a példában az ID változója szabály lekérdezi *2*.

```PowerShell
    PS C:\> Get-PswaAuthorizationRule –Id 2
```

### <a name="example-3-example-3-subheading"></a>{#Example-3 .subHeading} 3. példa

Ez a példa bemutatja, hogyan a parancsmag elfogadja láncból értéket.
A szabály azonosítót és egy szabálynevet átadott ebben a parancsmagban.

```PowerShell
    PS C:\> "rule1",0 | Get-PswaAuthorizationRule
```

## <a name="related-topics"></a>Kapcsolódó témakörök

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)
- [Test-PswaAuthorizationRule](test-pswaauthorizationrule.md)
- [Install-PswaWebApplication](install-pswawebapplication.md)
