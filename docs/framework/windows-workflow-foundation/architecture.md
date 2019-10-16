---
title: Windows Workflow 아키텍처
ms.date: 03/30/2017
ms.assetid: 1d4c6495-d64a-46d0-896a-3a01fac90aa9
ms.openlocfilehash: e2effc0f53153057b8a9034e4dc80cb19bbe7685
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834857"
---
# <a name="windows-workflow-architecture"></a>Windows Workflow 아키텍처
WF (Windows Workflow Foundation)는 대화형 장기 실행 응용 프로그램을 개발 하기 위한 추상화 수준을 높입니다. 작업 단위는 활동으로 캡슐화됩니다. 또한 활동은 흐름 제어, 예외 처리, 오류 전파, 상태 데이터 지속성, 메모리에서 진행 중인 워크플로 로드 및 언로드, 추적, 트랜잭션 흐름 등과 같은 기능을 제공하는 환경에서 실행됩니다.  
  
## <a name="activity-architecture"></a>활동 아키텍처  
 활동은 <xref:System.Activities.Activity>, <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity> 또는 <xref:System.Activities.NativeActivity>에서 파생되는 CLR 형식 또는 <xref:System.Activities.Activity%601>, <xref:System.Activities.CodeActivity%601>, <xref:System.Activities.AsyncCodeActivity%601> 또는 <xref:System.Activities.NativeActivity%601> 값을 반환하는 변형으로 개발됩니다. <xref:System.Activities.Activity>에서 파생되는 개발 활동을 사용하면 기존 활동을 어셈블하여 워크플로 환경에서 실행되는 작업 단위를 신속하게 만들 수 있습니다. 반면 <xref:System.Activities.CodeActivity>를 사용하면 주로 <xref:System.Activities.CodeActivityContext>를 통해 관리 코드에서 활동 인수에 액세스하는 데 필요한 실행 논리를 작성할 수 있습니다. <xref:System.Activities.AsyncCodeActivity>는 비동기 작업을 구현하는 데 사용할 수 있다는 점을 제외하고 <xref:System.Activities.CodeActivity>와 비슷합니다. <xref:System.Activities.NativeActivity>에서 파생되는 활동을 개발하면 자식 예약, 책갈피 만들기, 비동기 작업 호출, 트랜잭션 등록 등과 같은 기능에 <xref:System.Activities.NativeActivityContext>를 통해 런타임에 액세스할 수 있습니다.  
  
 <xref:System.Activities.Activity>에서 파생되는 작성 활동은 선언적이며 XAML로 작성될 수 있습니다. 다음 예제에서는 실행 본문에 다른 활동을 사용하여 `Prompt`라는 활동을 만듭니다.  
  
```xml  
<Activity x:Class='Prompt'  
  xmlns:x='http://schemas.microsoft.com/winfx/2006/xaml'  
    xmlns:z='http://schemas.microsoft.com/netfx/2008/xaml/schema'  
xmlns:my='clr-namespace:XAMLActivityDefinition;assembly=XAMLActivityDefinition'  
xmlns:s="clr-namespace:System;assembly=mscorlib"  
xmlns="http://schemas.microsoft.com/2009/workflow">  
<z:SchemaType.Members>  
    <z:SchemaType.SchemaProperty Name='Text' Type=' InArgument(s:String)' />  
  <z:SchemaType.SchemaProperty Name='Response' Type='OutArgument(s:String)' />  
</z:SchemaType.Members>  
  <Sequence>  
    <my:WriteLine Text='[Text]' />  
    <my:ReadLine BookmarkName='r1' Result='[Response]' />  
  </Sequence>  
</Activity>  
```  
  
## <a name="activity-context"></a>활동 컨텍스트  
 <xref:System.Activities.ActivityContext>는 워크플로 런타임에 대한 활동 작성자 인터페이스이며 풍부한 런타임 기능에 대한 액세스를 제공합니다. 다음 예제에서는 실행 컨텍스트를 사용하여 책갈피를 만드는 데 사용하는 활동을 정의합니다. 책갈피는 활동 실행 중에 호스트에서 데이터를 활동에 전달하기 위해 다시 시작할 수 있는 연속 지점을 등록할 수 있는 메커니즘입니다.  
  
 [!code-csharp[CFX_WorkflowApplicationExample#15](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#15)]  
  
## <a name="activity-life-cycle"></a>활동 수명 주기  
 활동 인스턴스는 <xref:System.Activities.ActivityInstanceState.Executing> 상태에서 시작합니다. 예외가 발생하지 않는 한 실행 중인 모든 자식 활동과 보류 중인 다른 작업(예: <xref:System.Activities.Bookmark> 개체)을 마칠 때까지는 활동 인스턴스가 이 상태로 유지됩니다. 이러한 활동이 완료되면 <xref:System.Activities.ActivityInstanceState.Closed> 상태로 전환됩니다. 활동 인스턴스의 부모가 자식을 취소하도록 요청할 수 있습니다. 자식을 취소할 수 있으면 <xref:System.Activities.ActivityInstanceState.Canceled> 상태로 완료됩니다. 실행 중에 예외가 throw되면 런타임에 활동이 <xref:System.Activities.ActivityInstanceState.Faulted> 상태로 전환되고 예외가 활동의 부모 체인으로 전파됩니다. 다음은 활동의 세 가지 완료 상태입니다.
  
- **닫히면** 작업을 완료 하 고 종료 했습니다.  
  
- **님** 작업이 정상적으로 중단 되 고 종료 되었습니다. 이 상태로 전환될 경우 작업이 명시적으로 롤백되지 않습니다.  
  
- **오류가** 활동에서 오류가 발생 하 여 작업을 완료 하지 않고 종료 되었습니다.  
  
 활동이 지속되거나 언로드되는 경우에는 <xref:System.Activities.ActivityInstanceState.Executing> 상태로 유지됩니다.
