---
title: 속성 및 인수
ms.date: 03/30/2017
ms.assetid: 14651389-4a49-4cbb-9ddf-c83fdc155df1
ms.openlocfilehash: a6ea4755599f18e8bbaa8187941623578d2168ac
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61962632"
---
# <a name="properties-vs-arguments"></a>속성 및 인수
데이터를 작업으로 전달하는 데 사용할 수 있는 여러 가지 옵션이 있습니다. <xref:System.Activities.InArgument>를 사용하는 것 외에 표준 CLR 속성이나 공용 <xref:System.Activities.ActivityAction> 속성을 사용하여 데이터를 받는 작업을 개발할 수도 있습니다. 이 항목에서는 적절한 메서드 형식을 선택하는 방법에 대해 설명합니다.  
  
## <a name="using-clr-properties"></a>CLR 속성 사용  
 데이터를 작업에 전달할 때 CLR 속성(즉, Get 및 Set 루틴을 사용하여 데이터를 노출하는 공용 메서드)은 가장 제한적인 옵션입니다. 솔루션을 컴파일할 때 CLR 속성에 전달되는 매개 변수 값을 알고 있어야 합니다. 이 값은 모든 워크플로 인스턴스에서 동일합니다. 이 방식에서 CLR 속성에 전달되는 값은 코드로 정의되는 상수와 유사합니다. 이 값은 작업 수명 동안 변경될 수 없으며 작업의 다른 인스턴스에 대해 변경할 수도 없습니다. <xref:System.Activities.Expressions.InvokeMethod%601.MethodName%2A>은 작업에서 노출되는 CLR 속성의 한 예입니다. 작업에서 호출하는 메서드 이름은 런타임 조건에 따라 변경될 수 없으며 작업의 모든 인스턴스에서 동일합니다.  
  
## <a name="using-arguments"></a>인수 사용  
 작업의 수명 동안 한 번만 데이터가 평가되는 경우 인수를 사용해야 합니다. 즉, 인수 값은 작업 수명 동안 변경되지 않지만 작업 인스턴스마다 다를 수 있습니다. <xref:System.Activities.Statements.If.Condition%2A>은 실행되는 동안 한 번만 평가되기 때문에 인수로 정의되어야 하는 값의 또 다른 예입니다. <xref:System.Activities.Statements.WriteLine.Text%2A>는 작업이 실행되는 동안 한 번만 평가되기 때문에 인수로 정의되어야 하는 메서드의 또 다른 예이지만 작업 인스턴스마다 다를 수 있습니다.  
  
## <a name="using-activityaction"></a>ActivityAction 사용  
 작업이 실행되는 동안 데이터를 여러 번 평가해야 하는 경우 <xref:System.Activities.ActivityAction>을 사용해야 합니다. 예를 들어, <xref:System.Activities.Statements.While.Condition%2A> 속성은 <xref:System.Activities.Statements.While> 루프를 반복할 때마다 평가됩니다. <xref:System.Activities.InArgument>를 이런 용도로 사용한 경우 각 반복에 대해 인수가 다시 평가되지 않고 항상 동일한 결과를 반환하기 때문에 루프가 종료되지 않습니다.
