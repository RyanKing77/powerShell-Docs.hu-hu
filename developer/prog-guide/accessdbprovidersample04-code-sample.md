---
title: Kódminta AccessDbProviderSample04 |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f9374c4a-e499-4516-9eb6-107c59df98d9
caps.latest.revision: 7
ms.openlocfilehash: 43f01b9cd6af3ab6c26f88ee0c1e9269499b2bc3
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62081954"
---
# <a name="accessdbprovidersample04-code-sample"></a>AccessDbProviderSample04 – kódminta

A következő kód bemutatja a Windows PowerShell-szolgáltatóban ismertetett végrehajtásának [létrehozása a Windows PowerShell-tároló szolgáltató](./creating-a-windows-powershell-container-provider.md). Ez a szolgáltató a többrétegű adattárak működik. Az ilyen típusú adattárat a legfelső szintre a tároló a legfelső szintű elemeket tartalmaz, és minden további szint gyermekelemek csomópont neve. Azáltal, hogy a felhasználót, hogy ezek gyermekcsomópontokat működjön, a felhasználók beavatkozhatnak hierarchikusan keresztül az adattárban.

## <a name="code-sample"></a>Kódminta

[!code-csharp[AccessDBProviderSample04.cs](../../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample04/AccessDBProviderSample04.cs#L11-L1635 "AccessDBProviderSample04.cs")]

## <a name="see-also"></a>Lásd még:

[Windows PowerShell SDK](../windows-powershell-reference.md)