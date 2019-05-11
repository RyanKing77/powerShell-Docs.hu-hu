---
title: A parancsmag bemeneti feldolgozási módszerek |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- virtual methods (PowerShell SDK]
ms.assetid: b0bb8172-c9fa-454b-9f1b-57c3fe60671b
caps.latest.revision: 12
ms.openlocfilehash: a28c8d3df19bc72bf338d6abc4e02768c5097209
ms.sourcegitcommit: 00cf9a99972ce40db7c25b9a3fc6152dec6bddb6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/28/2019
ms.locfileid: "64670303"
---
# <a name="cmdlet-input-processing-methods"></a>Parancsmag bemeneti feldolgozási módszerei

Parancsmagok felül kell írnia a bemeneti adatok feldolgozása a munkájuk elvégzéséhez ebben a témakörben ismertetett módszerek valamelyikét.
Ezek a metódusok lehetővé teszik a parancsmag előfeldolgozásához, bemeneti feldolgozási és utáni feldolgozási műveletek végrehajtásához.
Ezek a módszerek is lehetővé teszik a parancsmag feldolgozás megállítása.
Ezek a módszerek használatát bemutató részletes példa: [SelectStr oktatóanyag](selectstr-tutorial.md).

## <a name="pre-processing-operations"></a>Előfeldolgozási műveletek

Parancsmagok felül kell írni a [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) adható hozzá, amelyek érvényesek a parancsmag által később feldolgozandó összes rekordjára vonatkozóan előfeldolgozási műveleteket.
Amikor az PowerShell paranccsal folyamat, PowerShell meghívja ezt a metódust egyszer a parancsmag a folyamat minden példánya esetében.
Hogyan PowerShell hívja meg a parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](/previous-versions/ms714429(v=vs.85)).

A következő kódot a BeginProcessing metódus megvalósítását mutatja be.

```csharp
protected override void BeginProcessing()
{
  // Replace the WriteObject method with the logic required by your cmdlet.
  WriteObject("This is a test of the BeginProcessing template.");
}
```

## <a name="input-processing-operations"></a>Adjon meg feldolgozási műveletek

Parancsmagok felül lehet bírálni a [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) feldolgozni a parancsmaghoz küldött bemeneti metódus.
Amikor az PowerShell paranccsal folyamat, PowerShell meghívja ezt a metódust a parancsmag által feldolgozott bemeneti rekordonként.
Hogyan PowerShell hívja meg a parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](/previous-versions/ms714429(v=vs.85)).

A következő kódot a ProcessRecord metódus megvalósítását mutatja be.

```csharp
protected override void ProcessRecord()
{
  // Replace the WriteObject method with the logic required by your cmdlet.
  WriteObject("This is a test of the ProcessRecord template.");
}
```

## <a name="post-processing-operations"></a>Utólagos feldolgozási műveletek

Parancsmagok felül kell írni a [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) adható hozzá, amelyek érvényesek a parancsmag által feldolgozott összes rekordjára vonatkozóan utólagos feldolgozási műveleteket.
Például a parancsmag karbantartása objektum változók a befejezése után lehet feldolgozása.

Amikor az PowerShell paranccsal folyamat, PowerShell meghívja ezt a metódust egyszer a parancsmag a folyamat minden példánya esetében.
Azonban fontos megjegyezni, hogy a PowerShell-modul nem hívja a EndProcessing módszert, ha a parancsmag midway megszakad a bemeneti feldolgozást keresztül, vagy ha a megszakító hiba akkor fordul elő, a parancsmag bármely részén.
Ebből kifolyólag objektum karbantartási igénylő parancsmag meg kell valósítania a teljes [System.IDisposable](/dotnet/api/System.IDisposable) minta, beleértve a egy befejezővel, hogy a futtatókörnyezet segítségével meghívhatja a mindkét EndProcessing és [ System.IDisposable.Dispose](/dotnet/api/System.IDisposable.Dispose) módszerek feldolgozás végén.
Hogyan PowerShell hívja meg a parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](/previous-versions/ms714429(v=vs.85)).

A következő kódot a EndProcessing metódus megvalósítását mutatja be.

```csharp
protected override void EndProcessing()
{
  // Replace the WriteObject method with the logic required by your cmdlet.
  WriteObject("This is a test of the EndProcessing template.");
}
```

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing)

[System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

[System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)

[SelectStr oktatóanyag](selectstr-tutorial.md)

[System.IDisposable](/dotnet/api/System.IDisposable)

[Windows PowerShell Shell SDK](../windows-powershell-reference.md)
