---
title: 제네릭이 아닌 ParallelForEach
ms.date: 03/30/2017
ms.assetid: de17e7a2-257b-48b3-91a1-860e2e9bf6e6
ms.openlocfilehash: 52b851686ea2fdc8c573a0622fe91ca5e205edeb
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65637757"
---
# <a name="non-generic-parallelforeach"></a>제네릭이 아닌 ParallelForEach

[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]의 도구 상자에는 <xref:System.Activities.Statements.ParallelForEach%601> 컬렉션을 반복할 수 있도록 하는 <xref:System.Collections.Generic.IEnumerable%601>을 비롯한 흐름 제어 활동이 제공됩니다.

<xref:System.Activities.Statements.ParallelForEach%601> 필요한 해당 <xref:System.Activities.Statements.ParallelForEach%601.Values%2A> 형식으로 속성 <xref:System.Collections.Generic.IEnumerable%601>합니다. 그러면 사용자가 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스를 구현하는 데이터 구조(예: <xref:System.Collections.ArrayList>)를 반복하지 못합니다. <xref:System.Activities.Statements.ParallelForEach%601>의 비제네릭 버전은 컬렉션 값의 형식에 대한 호환성을 유지하기 위해 런타임 복잡성이 더 높아지지만 이러한 요구 사항의 제약을 받지 않습니다.

이 샘플에서는 비제네릭 <xref:System.Activities.Statements.ParallelForEach%601> 활동과 디자이너를 구현하는 방법을 보여 줍니다. 이 활동을 사용하여 <xref:System.Collections.ArrayList>를 반복할 수 있습니다.

## <a name="parallelforeach-activity"></a>ParallelForEach 활동

C#/VB `foreach` 문은 컬렉션의 각 요소에 대해 포함 문을 실행하여 컬렉션의 요소를 열거합니다. 그에 상응하는 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 활동은 <xref:System.Activities.Statements.ForEach%601> 및 <xref:System.Activities.Statements.ParallelForEach%601>입니다. <xref:System.Activities.Statements.ForEach%601> 활동은 값 목록과 본문을 포함합니다. 런타임에 목록이 반복되고 목록의 각 값에 대해 본문이 실행됩니다.

<xref:System.Activities.Statements.ParallelForEach%601>에는 <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A>이 있습니다. <xref:System.Activities.Statements.ParallelForEach%601>의 반환 결과가 <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A>이면 `true` 활동이 일찍 완료될 수 있습니다. <xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A>은 각 반복을 완료한 후에 확인됩니다.

대부분의 경우 제네릭 버전의 활동이 기본 솔루션이어야 합니다. 제네릭 버전은 이를 사용하는 대부분의 시나리오에 적용되고 컴파일 시 형식 검사 기능을 제공하기 때문입니다. 비제네릭 <xref:System.Collections.IEnumerable> 인터페이스를 구현하는 형식을 반복하는 데는 비제네릭 버전을 사용할 수 있습니다.

## <a name="class-definition"></a>클래스 정의

다음 코드 예제에서는 비제네릭 `ParallelForEach` 활동의 정의를 보여 줍니다.

```csharp
[ContentProperty("Body")]
public class ParallelForEach : NativeActivity
{
    [RequiredArgument]
    [DefaultValue(null)]
    InArgument<IEnumerable> Values { get; set; }

    [DefaultValue(null)]
    [DependsOn("Values")]
    public Activity<bool> CompletionCondition
    [DefaultValue(null)]
    [DependsOn("CompletionCondition")]
    ActivityAction<object> Body { get; set; }
}
```

Body (옵션) \
컬렉션의 각 요소에 대해 실행되는 <xref:System.Activities.ActivityAction> 형식의 <xref:System.Object>입니다. 각 개별 요소는 Argument 속성을 통해 본문에 전달됩니다.

값 (선택 사항) \
반복되는 요소의 컬렉션입니다. 컬렉션의 모든 요소가 호환 가능한 형식인지 확인하는 작업은 런타임에 수행됩니다.

CompletionCondition (옵션) \
<xref:System.Activities.Statements.ParallelForEach%601.CompletionCondition%2A> 속성은 반복을 완료한 후에 매번 확인됩니다. 그 결과가 `true`이면 예약하여 대기 중인 반복이 취소됩니다. 이 속성을 설정하지 않으면 분기 컬렉션의 모든 활동이 완료될 때까지 실행됩니다.

## <a name="example-of-using-parallelforeach"></a>ParallelForEach 사용 예제

다음 코드에서는 애플리케이션에서 ParallelForEach 활동을 사용하는 방법을 보여 줍니다.

```csharp
string[] names = { "bill", "steve", "ray" };

DelegateInArgument<object> iterationVariable = new DelegateInArgument<object>() { Name = "iterationVariable" };

Activity sampleUsage =
    new ParallelForEach
    {
       Values = new InArgument<IEnumerable>(c=> names),
       Body = new ActivityAction<object>
       {
           Argument = iterationVariable,
           Handler = new WriteLine
           {
               Text = new InArgument<string>(env => string.Format("Hello {0}",                                                               iterationVariable.Get(env)))
           }
       }
   };
```

## <a name="parallelforeach-designer"></a>ParallelForEach 디자이너

샘플의 활동 디자이너는 기본 제공 <xref:System.Activities.Statements.ParallelForEach%601> 활동에 제공되는 디자이너와 모양이 비슷합니다. 디자이너의 도구 상자에 표시 합니다 **샘플**, **비 제네릭 활동** 범주입니다. 디자이너 **ParallelForEachWithBodyFactory** 도구 상자에서 작업을 노출 하기 때문에 <xref:System.Activities.Presentation.IActivityTemplateFactory> 적절히 구성 된 된 작업을 만드는 도구 상자에서 <xref:System.Activities.ActivityAction>합니다.

```csharp
public sealed class ParallelForEachWithBodyFactory : IActivityTemplateFactory
{
    public Activity Create(DependencyObject target)
    {
        return new Microsoft.Samples.Activities.Statements.ParallelForEach()
        {
            Body = new ActivityAction<object>()
            {
                Argument = new DelegateInArgument<object>()
                {
                    Name = "item"
                }
            }
        };
    }
}
```

## <a name="to-run-the-sample"></a>이 샘플을 실행하려면

1. 선택한 프로젝트를 솔루션의 시작 프로젝트로 설정합니다.

    1. **CodeTestClient** 코드를 사용 하 여 작업을 사용 하는 방법을 보여 줍니다.

    2. **DesignerTestClient** 디자이너 내에서 작업을 사용 하는 방법을 보여 줍니다.

2. 프로젝트를 빌드하고 실행합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\NonGenericParallelForEach`
