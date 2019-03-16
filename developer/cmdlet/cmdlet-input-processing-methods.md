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
ms.openlocfilehash: 065214647dfa6d376b727930fe75140911095faf
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059371"
---
# <a name="cmdlet-input-processing-methods"></a>Parancsmag bemeneti feldolgozási módszerei

Parancsmagok felül kell írnia a bemeneti adatok feldolgozása a munkájuk elvégzéséhez ebben a témakörben ismertetett módszerek valamelyikét. Ezek a metódusok lehetővé teszik a parancsmag előfeldolgozási művelet, bemeneti feldolgozási műveletekhez és utáni feldolgozási műveletek végrehajtásához. Ezek a módszerek is lehetővé teszik a parancsmag feldolgozás megállítása.

## <a name="pre-processing-tasks"></a>Előfeldolgozási feladatok

Parancsmagok felül kell írni a [System.Management.Automation.Cmdlet.Beginprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) adható hozzá, amelyek érvényesek a parancsmag által később feldolgozandó összes rekordjára vonatkozóan előfeldolgozási műveleteket. Ha a Windows PowerShell parancs folyamat feldolgozza, Windows PowerShell meghívja ezt a módszert egyszer a parancsmag a folyamat minden példánya esetében. Hogyan hívja meg a Windows PowerShell parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](https://msdn.microsoft.com/en-us/3202f55c-314d-4ac3-ad78-4c7ca72253c5).

A következő kódot egy megvalósítását mutatja be a [System.Management.Automation.Cmdlet.Beginprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) metódust.

```csharp
protected override void BeginProcessing()
{
  // Replace the WriteObject method with the logic required
  // by your cmdlet. It is used here to generate the following
  // output:
  // "This is a test of the BeginProcessing template."
  WriteObject("This is a test of the BeginProcessing template.");
}
```

Részletesebb példát, hogyan használható a [System.Management.Automation.Cmdlet.Beginprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) metódus, lásd: [SelectStr oktatóanyag](./selectstr-tutorial.md). Ebben az oktatóanyagban a **Select-Str** parancsmagot használja a [System.Management.Automation.Cmdlet.Beginprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0) létrehozni a reguláris kifejezés, amely a bemeneti rekordjának segítségével módszert.

## <a name="input-processing-tasks"></a>Adjon meg feldolgozási feladatok

Parancsmagok felül lehet bírálni a [System.Management.Automation.Cmdlet.Processrecord%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) feldolgozni a parancsmaghoz küldött bemeneti metódus. Windows PowerShell parancs folyamat dolgozza fel, ha a Windows PowerShell meghívja ezt a metódust a parancsmag által feldolgozott bemeneti rekordonként. Hogyan hívja meg a Windows PowerShell parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](https://msdn.microsoft.com/en-us/3202f55c-314d-4ac3-ad78-4c7ca72253c5).

A következő kódot egy megvalósítását mutatja be a [System.Management.Automation.Cmdlet.Processrecord%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) metódust.

```csharp
protected override void ProcessRecord()
{
  // Replace the WriteObject method with the logic required
  // by your cmdlet. It is used here to generate the following
  // output:
  // "This is a test of the ProcessRecord template."
  WriteObject("This is a test of the ProcessRecord template.");
}
```

Részletesebb példát, hogyan használható a [System.Management.Automation.Cmdlet.Processrecord%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) metódus, lásd: [SelectStr oktatóanyag](./selectstr-tutorial.md).

## <a name="post-processing-tasks"></a>Utólagos feldolgozási feladatokat

Parancsmagok felül kell írni a [System.Management.Automation.Cmdlet.Endprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.endprocessing?view=powershellsdk-1.1.0) adható hozzá, amelyek érvényesek a parancsmag által feldolgozott összes rekordjára vonatkozóan utólagos feldolgozási műveleteket. Például a parancsmag karbantartása objektum változók a befejezése után lehet feldolgozása.

Ha a Windows PowerShell parancs folyamat feldolgozza, Windows PowerShell meghívja ezt a módszert egyszer a parancsmag a folyamat minden példánya esetében. Azonban fontos megjegyezni, hogy a Windows PowerShell-modul nem meghívja a [System.Management.Automation.Cmdlet.Endprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.endprocessing?view=powershellsdk-1.1.0) módszert, ha a parancsmagot a bemeneti feldolgozást keresztül midway megszakadt, vagy ha egy megszakítást okozó hiba jelenik meg a parancsmag bármely részén. Ebből kifolyólag objektum karbantartási igénylő parancsmag meg kell valósítania a teljes [System.IDisposable](/dotnet/api/System.IDisposable) minta, beleértve a egy befejezővel, hogy a futtatókörnyezet is meghívhatja a [ System.Management.Automation.Cmdlet.Endprocessing%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.endprocessing?view=powershellsdk-1.1.0) és [System.IDisposable.Dispose*](/dotnet/api/System.IDisposable.Dispose) módszerek feldolgozás végén. Hogyan hívja meg a Windows PowerShell parancs folyamat kapcsolatos további információkért lásd: [parancsmag feldolgozása életciklus](https://msdn.microsoft.com/en-us/3202f55c-314d-4ac3-ad78-4c7ca72253c5).

A következő kódot egy megvalósítását mutatja be a [System.Management.Automation.Cmdlet.Processrecord%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) metódust.

```csharp
protected override void EndProcessing()
{
  // Replace the WriteObject method with the logic required
  // by your cmdlet. It is used here to generate the following
  // output:
  // "This is a test of the EndProcessing template."
  WriteObject("This is a test of the EndProcessing template.");
}
```

Részletesebb példát, hogyan használható a [System.Management.Automation.Cmdlet.Processrecord%2A? Displayproperty = Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0) metódus, lásd: [SelectStr oktatóanyag](./selectstr-tutorial.md).

## <a name="see-also"></a>Lásd még:

[System.Management.Automation.Cmdlet.Beginprocessing%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.beginprocessing?view=powershellsdk-1.1.0)

[System.Management.Automation.Cmdlet.Processrecord%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.processrecord?view=powershellsdk-1.1.0)

[System.Management.Automation.Cmdlet.Endprocessing%2A?Displayproperty=Fullname](/dotnet/api/system.management.automation.cmdlet.endprocessing?view=powershellsdk-1.1.0)

[System.IDisposable](/dotnet/api/System.IDisposable)

[Windows PowerShell Shell SDK](../windows-powershell-reference.md)
