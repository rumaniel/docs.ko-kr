---
title: 활동 대리자 사용
ms.date: 03/30/2017
ms.assetid: e33cf876-8979-440b-9b23-4a12d1139960
ms.openlocfilehash: 63f550549456404b237067c98afdb18a8758dd7a
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989091"
---
# <a name="using-activity-delegates"></a>활동 대리자 사용
작업 대리자를 사용하면 활동 작성자는 활동 사용자가 활동 기반 처리기를 제공할 수 있는 특정 시그니처가 있는 콜백을 노출할 수 있습니다. 두 가지 형식의 작업 대리자를 사용할 수 있습니다. <xref:System.Activities.ActivityAction%601>은 반환 값이 없는 작업 대리자를 정의하는 데 사용되고 <xref:System.Activities.ActivityFunc%601>은 반환 값이 있는 작업 대리자를 정의하는 데 사용됩니다.

작업 대리자는 자식 작업이 특정 시그니처를 가지도록 제약되어야 하는 시나리오에서 유용합니다. 예를 들어 <xref:System.Activities.Statements.While> 활동은 제약 조건 없이 모든 형식의 자식 활동을 포함할 수 있지만 <xref:System.Activities.Statements.ForEach%601> 활동의 본문은 <xref:System.Activities.ActivityAction%601>이며 최종적으로 <xref:System.Activities.Statements.ForEach%601>에서 실행되는 자식 활동에는 <xref:System.Activities.InArgument%601>이 열거하는 컬렉션 멤버와 동일한 형식의 <xref:System.Activities.Statements.ForEach%601>이 있어야 합니다.

## <a name="using-activityaction"></a>ActivityAction 사용

[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 활동이나 <xref:System.Activities.Statements.Catch> 활동 같은 여러 가지 <xref:System.Activities.Statements.ForEach%601> 활동에 활동 동작이 사용됩니다. 각 경우에 활동 동작은 해당 활동 중 하나를 사용하여 워크플로를 작성할 때 필요한 동작을 제공하기 위해 워크플로 작성자가 활동을 지정하는 위치를 나타냅니다. 다음 예제에서는 <xref:System.Activities.Statements.ForEach%601> 활동을 사용하여 콘솔 창에 텍스트를 표시합니다. <xref:System.Activities.Statements.ForEach%601>의 본문은 문자열인 <xref:System.Activities.ActivityAction%601>의 형식에 일치하는 <xref:System.Activities.Statements.ForEach%601>을 사용하여 지정됩니다. <xref:System.Activities.Statements.WriteLine>에 지정된 <xref:System.Activities.ActivityDelegate.Handler%2A> 활동의 <xref:System.Activities.Statements.WriteLine.Text%2A> 인수는 <xref:System.Activities.Statements.ForEach%601> 활동의 반복 대상인 컬렉션의 문자열 값에 바인딩됩니다.

[!code-csharp[CFX_ActivityExample#6](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#6)]

actionArgument는 컬렉션의 개별 항목을 WriteLine으로 이동하는 데 사용됩니다. 워크플로가 호출되면 다음 출력이 콘솔에 표시됩니다.

```console
HelloWorld.
```

이 항목의 예에서는 개체 초기화 구문을 사용합니다. 개체 초기화 구문은 워크플로에 있는 활동의 계층적 뷰를 제공하고 활동 간의 관계를 표시하기 때문에 코드에서 워크플로 정의를 만드는 유용한 방법일 수 있습니다. 프로그래밍 방식으로 워크플로를 만들 때 개체 초기화 구문을 사용하기 위한 요구 사항은 없습니다. 다음 예는 이전 예와 기능적으로 동일합니다.

[!code-csharp[CFX_ActivityExample#7](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#7)]

개체 이니셜라이저 [에 대 한 자세한 내용은 방법: 생성자를 호출 하지 않고 개체 초기화C# (프로그래밍 가이드](https://go.microsoft.com/fwlink/?LinkId=161015) ) [및 방법: 개체 이니셜라이저](https://go.microsoft.com/fwlink/?LinkId=161016)를 사용 하 여 개체를 선언 합니다.

다음 예제에서는 <xref:System.Activities.Statements.TryCatch> 활동이 워크플로에 사용됩니다. <xref:System.ApplicationException>이 워크플로를 통해 throw되고 <xref:System.Activities.Statements.Catch%601> 활동을 통해 처리됩니다. 활동의 작업 동작 <xref:System.Activities.Statements.Catch%601> <xref:System.Activities.Statements.WriteLine> 에 대 한 처리기는 활동 이며 예외 세부 정보는를 사용 하 여 `ex` <xref:System.Activities.DelegateInArgument%601>전달 됩니다.

[!code-csharp[CFX_WorkflowApplicationExample#33](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#33)]

<xref:System.Activities.ActivityAction%601>을 정의하는 사용자 지정 활동을 만들 때는 <xref:System.Activities.Statements.InvokeAction%601>을 사용하여 해당 <xref:System.Activities.ActivityAction%601>의 호출을 모델링합니다. 이 예제에서는 사용자 지정 `WriteLineWithNotification` 활동을 정의합니다. 이 활동은 <xref:System.Activities.Statements.Sequence> 활동과, 문자열 인수 하나를 사용하는 <xref:System.Activities.Statements.WriteLine>을 호출하는 <xref:System.Activities.Statements.InvokeAction%601>을 차례로 포함하는 <xref:System.Activities.ActivityAction%601>로 구성됩니다.

[!code-csharp[CFX_ActivityExample#1](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#1)]

`WriteLineWithNotification` 활동을 사용하여 워크플로를 만드는 경우 워크플로 작성자는 필요한 사용자 지정 논리를 활동 동작의 <xref:System.Activities.ActivityDelegate.Handler%2A>에 지정합니다. 이 예제에서는 `WriteLineWithNotification` 활동을 사용하는 워크플로를 만들고 <xref:System.Activities.Statements.WriteLine> 활동을 <xref:System.Activities.ActivityDelegate.Handler%2A>로 사용합니다.

[!code-csharp[CFX_ActivityExample#2](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#2)]

하나 이상의 인수를 전달하기 위해 제공된 일반 버전의 여러 <xref:System.Activities.Statements.InvokeAction%601> 및 <xref:System.Activities.ActivityAction%601>이 있습니다.

## <a name="using-activityfunc"></a>ActivityFunc 사용

<xref:System.Activities.ActivityAction%601>은 활동의 결과 값이 없는 경우에 유용하고, 결과 값이 반환되는 경우에는 <xref:System.Activities.ActivityFunc%601>이 사용됩니다. <xref:System.Activities.ActivityFunc%601>을 정의하는 사용자 지정 활동을 만들 때는 <xref:System.Activities.Expressions.InvokeFunc%601>을 사용하여 해당 <xref:System.Activities.ActivityFunc%601>의 호출을 모델링합니다. 다음 예제에서는 `WriteFillerText` 활동을 정의합니다. 필터 텍스트를 제공하기 위해 정수 인수를 사용하고 문자열 결과를 반환하는 <xref:System.Activities.Expressions.InvokeFunc%601>을 지정합니다. 필터 텍스트가 검색되면 <xref:System.Activities.Statements.WriteLine> 활동을 사용하여 해당 텍스트가 콘솔에 표시됩니다.

[!code-csharp[CFX_ActivityExample#3](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#3)]

텍스트를 제공하기 위해 `int` 인수 하나를 사용하고 문자열 결과가 있는 활동을 사용해야 합니다. 이 예제에서는 이 요구 사항과 일치하는 `TextGenerator` 활동을 보여 줍니다.

[!code-csharp[CFX_ActivityExample#4](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#4)]

`TextGenerator` 활동을 `WriteFillerText` 활동과 함께 사용하려면 이 활동을 <xref:System.Activities.ActivityDelegate.Handler%2A>로 지정합니다.

[!code-csharp[CFX_ActivityExample#5](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#5)]
