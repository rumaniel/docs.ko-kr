---
title: CacheMetadata를 사용하여 데이터 노출
ms.date: 03/30/2017
ms.assetid: 34832f23-e93b-40e6-a80b-606a855a00d9
ms.openlocfilehash: a044c896e56541ee954fc33853376eb8293c6ede
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945706"
---
# <a name="exposing-data-with-cachemetadata"></a>CacheMetadata를 사용하여 데이터 노출

작업을 실행하기 전에 워크플로 런타임은 실행을 유지하는 데 필요한 모든 작업 정보를 얻습니다. 워크플로 런타임은 <xref:System.Activities.Activity.CacheMetadata%2A> 메서드를 실행하는 동안 이 정보를 가져옵니다. 이 메서드의 기본 구현에서는 실행 시 작업에서 노출하는 모든 공용 인수, 변수 및 자식 작업을 런타임에 제공합니다. 작업에서 보다 많은 정보를 런타임에 제공해야 하는 경우(예: 전용 멤버 또는 작업에서 예약될 작업) 이 메서드를 재정의하여 제공할 수 있습니다.

## <a name="default-cachemetadata-behavior"></a>기본 CacheMetadata 동작

<xref:System.Activities.NativeActivity.CacheMetadata%2A>에서 파생되는 작업에 대한 <xref:System.Activities.NativeActivity>의 기본 구현에서는 다음 메서드 형식을 다음과 같은 방식으로 처리합니다.

- <xref:System.Activities.InArgument%601>하십시오 <xref:System.Activities.OutArgument%601>, 또는 <xref:System.Activities.InOutArgument%601> (제네릭 인수): 이러한 인수 이름으로 인수로 런타임에 노출 됩니다 하 고 노출된 된 속성 이름 및 형식, 적절 한 인수 방향 및 일부 유효성 검사 데이터가 같은 입력 합니다.

- <xref:System.Activities.Variable> 또는 해당 서브: 이러한 멤버는 런타임에 공용 변수로 노출 됩니다.

- <xref:System.Activities.Activity> 또는 해당 서브: 이러한 멤버는 런타임에 공용 자식 작업으로 노출 됩니다. 호출 하 여 기본 동작을 명시적으로 구현할 수 있습니다 <xref:System.Activities.ActivityMetadata.AddImportedChild%2A>자식 활동에 전달 합니다.

- <xref:System.Activities.ActivityDelegate> 또는 해당 서브: 이러한 멤버는 런타임에 공용 대리자로 노출 됩니다.

- <xref:System.Collections.ICollection> 형식의 <xref:System.Activities.Variable>: 컬렉션의 모든 요소가 런타임에 공용 변수로 노출 됩니다.

- <xref:System.Collections.ICollection> 형식의 <xref:System.Activities.Activity>: 컬렉션의 모든 요소는 런타임에 공용 자식으로 노출 됩니다.

- <xref:System.Collections.ICollection> 형식의 <xref:System.Activities.ActivityDelegate>: 컬렉션의 모든 요소가 런타임에 공용 대리자로 노출 됩니다.

<xref:System.Activities.Activity.CacheMetadata%2A>, <xref:System.Activities.Activity> 및 <xref:System.Workflow.Activities.CodeActivity>에서 파생되는 작업에 대한 <xref:System.Activities.AsyncCodeActivity>도 다음과 같은 차이점을 제외하고 위와 동일하게 작동합니다.

- <xref:System.Activities.Activity>에서 파생되는 클래스는 자식 작업이나 대리자를 예약할 수 없으므로 이러한 멤버는 가져온 자식 및 대리자로 노출됩니다.

- <xref:System.Activities.CodeActivity> 및 <xref:System.Activities.AsyncCodeActivity>에서 파생되는 클래스는 변수, 자식 또는 대리자를 지원하지 않으므로 인수만 노출됩니다.

## <a name="overriding-cachemetadata-to-provide-information-to-the-runtime"></a>CacheMetadata를 재정의하여 런타임에 정보 제공

다음 코드 조각에서는 <xref:System.Activities.Activity.CacheMetadata%2A> 메서드를 실행하는 동안 작업의 메타데이터에 멤버 정보를 추가하는 방법을 보여 줍니다. 작업에 대한 공용 데이터를 모두 캐시하기 위해 메서드의 기준이 호출됩니다.

```csharp
protected override void CacheMetadata(NativeActivityMetadata metadata)
{
    base.CacheMetadata(metadata);
    metadata.AddImplementationChild(this._writeLine);
    metadata.AddVariable(this._myVariable);
    metadata.AddImplementationVariable(this._myImplementationVariable);

    RuntimeArgument argument = new RuntimeArgument("MyArgument", ArgumentDirection.In, typeof(SomeType));
    metadata.Bind(argument, this.SomeName);
    metadata.AddArgument(argument);
}
```

## <a name="using-cachemetadata-to-expose-implementation-children"></a>CacheMetadata를 사용하여 구현 자식 노출

변수를 사용하여 작업에서 예약될 자식 작업에 데이터를 전달하려면 변수를 구현 변수로 추가해야 합니다. 공용 변수의 값은 이런 방식으로 설정할 수 없습니다. 이것은 작업이 속성을 가진 캡슐화된 클래스가 아니라 매개 변수를 가진 함수의 구현으로 실행되기 때문입니다. 하지만 예약된 작업은 자식 작업과 동일한 방식으로 부모 작업의 인수에 액세스할 수 없기 때문에 <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A>를 사용하는 경우와 같이 인수를 명시적으로 설정해야 하는 경우도 있습니다.

다음 코드 조각에서는 <xref:System.Activities.Activity.CacheMetadata%2A>를 사용하여 기본 작업의 인수를 예약된 작업에 전달하는 방법을 보여 줍니다.

```csharp
public sealed class ChildActivity : NativeActivity
{
    public WriteLine _writeLine;
    public InArgument<string> Message { get; set; }
    private Variable<string> MessageVariable { get; set; }
    public ChildActivity()
    {
        MessageVariable = new Variable<string>();
        _writeLine = new WriteLine
        {
            Text = new InArgument<string>(MessageVariable),
        };
    }
    protected override void CacheMetadata(NativeActivityMetadata metadata)
    {
        base.CacheMetadata(metadata);
        metadata.AddImplementationVariable(this.MessageVariable);
        metadata.AddImplementationChild(this._writeLine);
    }
    protected override void Execute(NativeActivityContext context)
    {
        string configuredMessage = context.GetValue(Message);
        context.SetValue(MessageVariable, configuredMessage);
        context.ScheduleActivity(this._writeLine);
    }
}
```
