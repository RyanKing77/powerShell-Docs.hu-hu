---
title: Egy egyéni Windows PowerShell beépülő modul írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- snap-ins [PowerShell SDK], custom PSSnapin example
- cmdlets [PowerShell SDK], specified in snap-ins
ms.assetid: 55c8b5cb-8ee2-4080-afc4-3f09c9f20128
caps.latest.revision: 6
ms.openlocfilehash: 4d50ef4dcd75d5c0ba802fbcfe2d7d1d7c954707
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62067025"
---
# <a name="writing-a-custom-windows-powershell-snap-in"></a>Egyéni Windows PowerShelles beépülő modul írása

Ez a példa bemutatja, hogyan írhat egy Windows PowerShell beépülő modul, amely regisztrálja az adott parancsmagok.

Az ilyen típusú beépülő modul megadhatja a mely parancsmagok, szolgáltatók, típus vagy formátumok regisztrálni. Beépülő modul a parancsmagok és szolgáltatók regisztrálása egy szerelvény írásával kapcsolatban további információkért lásd: [egy Windows PowerShell beépülő modul írása](./writing-a-windows-powershell-snap-in.md).

## <a name="to-write-a-windows-powershell-snap-in-that-registers-specific-cmdlets"></a>Egy Windows PowerShell beépülő modult írhat, amelyek adott parancsmagok regisztrálja.

1. Adja hozzá a RunInstallerAttribute attribútumot.

2. Hozzon létre egy nyilvános osztályt származó a [System.Management.Automation.Custompssnapin](/dotnet/api/System.Management.Automation.CustomPSSnapIn) osztály.

   Ebben a példában az osztály neve "CustomPSSnapinTest".

3. Adja hozzá a nyilvános tulajdonság neve: a modul (kötelező). Beépülő modulok elnevezésekor ne használja a következő karaktereket: #. , ( ) { } [ ] & - /\ $ ; : " ' \< > &#124; ? @ ` *

   Ebben a példában a beépülő modul neve "CustomPSSnapInTest".

4. Adja hozzá a nyilvános tulajdonságot a szállító, a modul (kötelező).

   Ebben a példában a szállító pedig a "Microsoft".

5. Adja hozzá a nyilvános tulajdonságot a szállító erőforrás a beépülő modul (nem kötelező).

   Ebben a példában a "CustomPSSnapInTest, a Microsoft" a szállító erőforrás.

6. Adja hozzá a nyilvános tulajdonságot (kötelező) a beépülő modul a leírását.

   Ebben a példában a leírás megadása nem: "Ez az egy egyéni Windows PowerShell beépülő modul, amely tartalmazza a Test-HelloWorld és a Test-CustomSnapinTest parancsmagok".

7. Adja hozzá a nyilvános tulajdonságot a leírás erőforrás a beépülő modul (nem kötelező).

   Ebben a példában szállítói az erőforrás "CustomPSSnapInTest, ez is egy egyéni Windows PowerShell beépülő modul, amely a Test-HelloWorld és Test-CustomSnapinTest parancsokat tartalmaz".

8. Adja meg, amely az egyéni beépülő modult (nem kötelező) használatával tartozik a parancsmagok a [System.Management.Automation.Runspaces.Cmdletconfigurationentry](/dotnet/api/System.Management.Automation.Runspaces.CmdletConfigurationEntry) osztály. Az itt hozzáadott információkat tartalmazza a parancsmag, a .NET-típusát és a parancsmag súgófájl neve (a parancsmag súgójában fájlnév formátuma legyen name.dll-help.xml) nevét.

   Ez a példa hozzáadja a Test-HelloWorld és TestCustomSnapinTest parancsmagok.

9. Adja meg a szolgáltató, amely az egyéni beépülő modul (nem kötelező) tartozik.

   Ebben a példában adjon meg olyan szolgáltatót.

10. Adja meg a fájltípusok, az egyéni beépülő modul (nem kötelező) tartozik.

    Ebben a példában adjon meg olyan típusokat.

11. Adja meg a formátum, amely az egyéni beépülő modul (nem kötelező) tartozik.

    Ebben a példában nem ad meg semmilyen formátumokat.

## <a name="example"></a>Példa

Ez a példa bemutatja, hogyan írhat olyan egyéni Windows PowerShell beépülő modul, amely a Test-HelloWorld és a Test-CustomSnapinTest parancsmagjainak regisztrálásához használható. Vegye figyelembe, hogy ebben a példában a teljes szerelvény tartalmazhatnak más parancsmagok és szolgáltatók szerint ez a beépülő modul nem lenne regisztrált.

```csharp
[RunInstaller(true)]
public class CustomPSSnapinTest : CustomPSSnapIn
{
  /// <summary>
  /// Creates an instance of CustomPSSnapInTest class.
  /// </summary>
  public CustomPSSnapinTest()
          : base()
  {
  }

  /// <summary>
  /// Specify the name of the custom PowerShell snap-in.
  /// </summary>
  public override string Name
  {
    get
    {
      return "CustomPSSnapInTest";
    }
  }

  /// <summary>
  /// Specify the vendor for the custom PowerShell snap-in.
  /// </summary>
  public override string Vendor
  {
    get
    {
      return "Microsoft";
    }
  }

  /// <summary>
  /// Specify the localization resource information for the vendor.
  /// Use the format: resourceBaseName,resourceName.
  /// </summary>
  public override string VendorResource
  {
    get
    {
        return "CustomPSSnapInTest,Microsoft";
    }
  }

  /// <summary>
  /// Specify a description of the custom PowerShell snap-in.
  /// </summary>
  public override string Description
  {
    get
    {
      return "This is a custom PowerShell snap-in that includes the Test-HelloWorld and Test-CustomSnapinTest cmdlets.";
    }
  }

  /// <summary>
  /// Specify the localization resource information for the description.
  /// Use the format: resourceBaseName,Description.
  /// </summary>
  public override string DescriptionResource
  {
    get
    {
        return "CustomPSSnapInTest,This is a custom PowerShell snap-in that includes the Test-HelloWorld and Test-CustomSnapinTest cmdlets.";
    }
  }

  /// <summary>
  /// Specify the cmdlets that belong to this custom PowerShell snap-in.
  /// </summary>
  private Collection<CmdletConfigurationEntry> _cmdlets;
  public override Collection<CmdletConfigurationEntry> Cmdlets
  {
    get
    {
      if (_cmdlets == null)
      {
        _cmdlets = new Collection<CmdletConfigurationEntry>();
        _cmdlets.Add(new CmdletConfigurationEntry("test-customsnapintest", typeof(TestCustomSnapinTest), "TestCmdletHelp.dll-help.xml"));
        _cmdlets.Add(new CmdletConfigurationEntry("test-helloworld", typeof(TestHelloWorld), "HelloWorldHelp.dll-help.xml"));
      }

      return _cmdlets;
    }
  }

  /// <summary>
  /// Specify the providers that belong to this custom PowerShell snap-in.
  /// </summary>
  private Collection<ProviderConfigurationEntry> _providers;
  public override Collection<ProviderConfigurationEntry> Providers
  {
    get
    {
      if (_providers == null)
      {
        _providers = new Collection<ProviderConfigurationEntry>();
      }

      return _providers;
    }
  }

  /// <summary>
  /// Specify the types that belong to this custom PowerShell snap-in.
  /// </summary>
  private Collection<TypeConfigurationEntry> _types;
  public override Collection<TypeConfigurationEntry> Types
  {
    get
    {
      if (_types == null)
      {
        _types = new Collection<TypeConfigurationEntry>();
      }

      return _types;
    }
  }

  /// <summary>
  /// Specify the formats that belong to this custom PowerShell snap-in.
  /// </summary>
  private Collection<FormatConfigurationEntry> _formats;
  public override Collection<FormatConfigurationEntry> Formats
  {
    get
    {
      if (_formats == null)
      {
        _formats = new Collection<FormatConfigurationEntry>();
      }

      return _formats;
    }
  }
}
```

Beépülő modulok regisztrálásával kapcsolatos további információkért lásd: [parancsmagjainak regisztrálásához, a szolgáltatók és az alkalmazások üzemeltetése hogyan](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c) a a [Windows PowerShell programozói útmutató](../prog-guide/windows-powershell-programmer-s-guide.md).

## <a name="see-also"></a>Lásd még:

[How to Register parancsmagok, a szolgáltatók és az alkalmazások üzemeltetéséhez](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[Windows PowerShell Shell SDK](../windows-powershell-reference.md)
