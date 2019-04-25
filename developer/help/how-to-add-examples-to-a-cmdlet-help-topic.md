---
title: Példák, a parancsmag Súgó-témakör hozzáadása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8f723b21-8f95-4981-8b6e-4f07c22d601a
caps.latest.revision: 5
ms.openlocfilehash: 5e8d1df6b423bfd2cd6b0a64a8875dea9c3fb4ef
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083467"
---
# <a name="how-to-add-examples-to-a-cmdlet-help-topic"></a>Példák hozzáadása egy parancsmagokkal kapcsolatos súgótémakörhöz

- [Tudnivaló a parancsmag súgóját példái kapcsolatban](#Things-to-Know-about-Examples-in-Cmdlet-Help)

- [Példák megjelenítő nézetek segítségével](#Help-Views-that-Display-Examples)

- [Egy példa csomópont hozzáadása](#Adding-an-Examples-Node)

- [Karakterek megelőző hozzáadása](#Adding-Preceding-Characters)

- [A parancs felvétele](#Adding-the-Command)

- [Leírás hozzáadása](#Adding-a-Description)

- [Példa kimenet hozzáadása](#Adding-Example-Output)

## <a name="things-to-know-about-examples-in-cmdlet-help"></a>Tudnivaló a parancsmag súgóját példái kapcsolatban

- Listán minden, a parancsban a paraméter neve, akkor is, ha a paraméter nevének megadása nem kötelező. Ez segít a felhasználó könnyen értelmezni a parancsot.

- Kerülje a aliasok és a részleges paraméterneveket, annak ellenére, hogy a Windows PowerShell® működnek.

- Példa leírásában adja meg a parancs építésére ésszerű ismertetik. Azt ismerteti, miért döntött az adott paramétereket és értékeket, és a változók használatának módjáról.

- Ha a parancs kifejezéseket használ, ezeket részletesen elmagyarázza.

- Ha a parancs tulajdonságai és metódusai objektumok használ, különösen olyan tulajdonságok, amelyek nem jelennek meg az alapértelmezett megjelenítést a példát követve, mert lehetőséget a felhasználó értesítése az objektumra vonatkozó.

## <a name="help-views-that-display-examples"></a>Példák megjelenítő nézetek segítségével

Példák csak a Súgó parancsmag részletes és a teljes nézetek jelennek meg.

## <a name="adding-an-examples-node"></a>Egy példa csomópont hozzáadása

A következő XML-példákat csomópont, amely tartalmazza a példában egyetlen csomópont hozzáadása mutatja be. Minden egyes példák fel szeretne venni a témakör a további példa csomópontok hozzáadása.

```xml
<command:examples>
  <command:example>
  </command:example>
</command:examples>
```

## <a name="adding-an-example-title"></a>Egy példa cím hozzáadása

A következő XML formátumú bemutatja, hogyan például cím megadásához. A cím beállítása mellett további példák a példa szolgál. Windows PowerShell® használ egy standard fejlécet, amely több egymást követő példában.

```xml
<command:examples>
  <command:example>
    <maml:title>----------  EXAMPLE 1  ----------</maml:title>
  </command:example>
</command:examples>
```

## <a name="adding-preceding-characters"></a>Karakterek megelőző hozzáadása

A következő XML formátumú karaktereket, például a Windows PowerShell-parancssort, amely jelennek meg azonnal a példaparancs (bármely beavatkozó szóközök nélkül) előtt adjon hozzá mutatja be. Windows PowerShell® használja a Windows PowerShell-parancssorba: C:\PS>.

```xml
<command:examples>
  <command:example>
    <maml:title>----------  EXAMPLE 1  ----------</maml:title>
    <maml:Introduction>
      <maml:paragraph>C:\PS></maml:paragraph>
    </maml:Introduction>
</command:example>
</command:examples>
```

## <a name="adding-the-command"></a>A parancs felvétele

A következő XML formátumú adja hozzá a tényleges parancsot a példa szemlélteti. A parancs való hozzáadásakor, írja be a teljes nevét (ne használja a alias) parancsmagok és paraméterek. Továbbá a használnak kisbetűs karaktert, amikor csak lehetséges.

```xml
<command:examples>
  <command:example>
    <maml:title>----------  EXAMPLE 1  ----------</maml:title>
    <maml:Introduction>
      <maml:paragraph>C:\PS></maml:paragraph>
    </maml:Introduction>
    <dev:code> command </dev:code>
</command:example>
</command:examples>
```

## <a name="adding-a-description"></a>Leírás hozzáadása

A következő XML-kódot adjon meg egy leírást a példa szemlélteti. Windows PowerShell® használja egyetlen \<maml:para > címkék leírására, akkor is, ha több \<maml:para > címkék használhatók.

```xml
<command:examples>
  <command:example>
    <maml:title>----------  EXAMPLE 1  ----------</maml:title>
    <maml:Introduction>
      <maml:paragraph>C:\PS></maml:paragraph>
    </maml:Introduction>
    <dev:code> command </dev:code>
    <dev:remarks>
      <maml:para> command description </maml:para>
    </dev:remarks>
</command:example>
</command:examples>
```

## <a name="adding-example-output"></a>Példa kimenet hozzáadása

A következő XML formátumú adja hozzá a parancs kimenetét mutatja be. A parancs eredménye információ megadása nem kötelező, de bizonyos esetekben hasznos lehet a megadott paraméterekkel hatásának bemutatása. Windows PowerShell® használ üres két készletnyi \<maml:para > címkéket, hogy a parancs kimenete elkülönítése a parancsot.

```xml
<command:examples>
  <command:example>
    <maml:title>----------  EXAMPLE 1  ----------</maml:title>
    <maml:Introduction>
      <maml:paragraph>C:\PS></maml:paragraph>
    </maml:Introduction>
    <dev:code> command </dev:code>
    <dev:remarks>
      <maml:para> command description </maml:para>
      <maml:para></maml:para>
      <maml:para></maml:para>
      <maml:para> command output </maml:para>
</dev:remarks>
</command:example>
</command:examples>
```