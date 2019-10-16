---
title: 공간 함수
ms.date: 03/30/2017
ms.assetid: 90cb177d-88a0-45be-97e8-3b306283c6e0
ms.openlocfilehash: 09402633c5e7f591a534992fc92655e6a2d1d88d
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61797698"
---
# <a name="spatial-functions"></a>공간 함수
공간 형식의 경우 리터럴 형식이 없습니다. 그러나 WKT(Well Known Text) 형식의 문자열을 사용하여 호출하는 정식 Entity Framework 함수를 사용할 수 있습니다. 예를 들어 다음 함수 호출은 기하 도형 점을 만듭니다.  
  
```  
GeometryFromText('POINT (43 -73)')  
```  
  
 <xref:System.Data.Common.CommandTrees.ExpressionBuilder.Spatial.SpatialEdmFunctions> 메서드는 모든 공간 정식 Entity Framework 메서드가 있어야 합니다. 함수에 전달해야 하는 매개 변수를 보려면 해당 메서드를 클릭하세요.
