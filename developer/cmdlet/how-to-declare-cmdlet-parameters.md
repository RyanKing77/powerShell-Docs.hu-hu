---
title: Hogyan parancsmag-paraméterek deklarálnia |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0c0509cc-5a50-49ad-a74f-5527023d0270
caps.latest.revision: 10
ms.openlocfilehash: 80e3e27bcf72b078c192525a843a3b3afb306529
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059167"
---
# <a name="how-to-declare-cmdlet-parameters"></a>Parancsmag-paraméterek deklarálása

Ezek a példák bemutatják, hogyan deklarálja nevű, csak pozíciórekord, szükséges, választható, és váltson a paramétereket. Ezek a példák is mutatják határozza meg a paraméter-alias.

## <a name="how-to-declare-a-named-parameter"></a>Hogyan Deklaráljon egy elnevezett paraméter

- Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon. Amikor hozzáadja a paraméter-attribútumhoz, hagyja ki a `Position` kulcsszó attribútum.

    ```csharp
    [Parameter()]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).

## <a name="how-to-declare-a-positional-parameter"></a>Hogyan Deklarovat Parametr Helyzetbeállító

- Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon. Amikor hozzáadja a paraméter-attribútumhoz, állítsa be a `Position` kulcsszó argumentum helyére. A 0 érték azt jelzi, hogy az első pozíciót.

    ```csharp
    [Parameter(Position = 0)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).

## <a name="how-to-declare-a-mandatory-parameter"></a>Hogyan Deklaráljon egy kötelező paraméter

- Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon. Amikor hozzáadja a paraméter-attribútumhoz, állítsa be a `Mandatory` kulcsszó használatával `true`.

    ```csharp
    [Parameter(Position = 0, Mandatory = true)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).

## <a name="how-to-declare-an-optional-parameter"></a>Hogyan Deklaráljon egy nem kötelező paraméter

- Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon. Amikor hozzáadja a paraméter-attribútumhoz, hagyja ki a `Mandatory` kulcsszót.

    ```csharp
    [Parameter(Position = 0)]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

## <a name="how-to-declare-a-switch-parameter"></a>Hogyan Deklarovat Parametr kapcsoló

- Típus nyilvános tulajdonságának kell definiálni [System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter), és majd deklarálja a paraméter-attribútumhoz.

    ```csharp
    [Parameter(Position = 1)]
    public SwitchParameter GoodBye
    {
      get { return goodbye; }
      set { goodbye = value; }
    }
    private bool goodbye;
    ```

A paraméter-attribútumhoz kapcsolatos további információkért lásd: [paraméter típusattribútum-deklaráció](./parameter-attribute-declaration.md).

## <a name="how-to-declare-a-parameter-with-aliases"></a>Hogyan Deklarovat Parametr-aliasok

- Adja meg a nyilvános tulajdonság, az alábbi kódban látható módon. Adjon hozzá egy aliast attribútum, amely a paraméter az aliasokat tartalmazza. Ebben a példában három aliasok vannak definiálva ugyanezt a paramétert. Az első alias nyújt hivatkozást. A második és harmadik aliasok is használhatja a különböző helyzetekhez nevét adja meg.

    ```csharp
    [Alias("UN","Writer","Editor")]
    [Parameter()]
    public string UserName
    {
      get { return userName; }
      set { userName = value; }
    }
    private string userName;
    ```

Az Alias attribútum kapcsolatos további információkért lásd: [Alias típusattribútum-deklaráció](./alias-attribute-declaration.md).

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.SwitchParameter](/dotnet/api/System.Management.Automation.SwitchParameter)

[Deklarace parametru attribútum](./parameter-attribute-declaration.md)

[Alias típusattribútum-deklaráció](./alias-attribute-declaration.md)

[Egy Windows PowerShell-parancsmag írása](./writing-a-windows-powershell-cmdlet.md)
