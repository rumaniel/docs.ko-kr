---
title: 변수 및 인수
ms.date: 03/30/2017
ms.assetid: d03dbe34-5b2e-4f21-8b57-693ee49611b8
ms.openlocfilehash: 251641c924bbf33c176f519f8fc4f9dec59e2eb8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962200"
---
# <a name="variables-and-arguments"></a>변수 및 인수
WF (Windows Workflow Foundation)에서 변수는 데이터의 저장소를 나타내고 인수는 활동에 대 한 데이터의 흐름을 나타냅니다. 활동에는 인수 집합이 있으며 인수는 활동의 시그니처를 구성합니다. 또한 활동은 개발자가 워크플로 디자인 중에 변수를 추가하거나 제거할 수 있는 변수 목록을 유지할 수 있습니다. 인수는 값을 반환하는 식을 사용하여 바인딩됩니다.  
  
## <a name="variables"></a>변수  
 변수는 데이터의 스토리지 위치입니다. 변수는 워크플로 정의의 일부로 선언됩니다. 변수는 런타임에 값을 가져오고 이 값은 워크플로 인스턴스 상태의 일부로 저장됩니다. 변수 정의는 변수의 형식과 선택적으로 이름을 지정합니다. 다음 코드에서는 변수를 선언하고 <xref:System.Activities.Statements.Assign%601> 활동을 사용하여 변수에 값을 할당한 다음 <xref:System.Activities.Statements.WriteLine> 활동을 사용하여 콘솔에 값을 표시하는 방법을 보여 줍니다.  
  
```csharp  
// Define a variable named "str" of type string.  
Variable<string> var = new Variable<string>  
{  
    Name = "str"  
};  
  
// Declare the variable within a Sequence, assign  
// a value to it, and then display it.  
Activity wf = new Sequence()  
{  
    Variables = { var },  
    Activities =  
    {  
        new Assign<string>  
        {  
            To = var,  
            Value = "Hello World."  
        },  
        new WriteLine  
        {  
            Text = var  
        }  
    }  
};  
  
WorkflowInvoker.Invoke(wf);  
```  
  
 변수 선언의 일부로 기본값 식을 선택적으로 지정할 수 있습니다. 변수도 한정자를 가질 수 있습니다. 예를 들어 변수가 읽기 전용이면 읽기 전용 <xref:System.Activities.VariableModifiers> 한정자를 적용할 수 있습니다. 다음 예제에서는 기본값이 할당되는 읽기 전용 변수를 만듭니다.  
  
```csharp  
// Define a read-only variable with a default value.  
Variable<string> var = new Variable<string>  
{  
    Default = "Hello World.",  
    Modifiers = VariableModifiers.ReadOnly  
};  
```  
  
## <a name="variable-scoping"></a>변수 범위 지정  
 런타임에 변수의 수명은 변수를 선언하는 활동의 수명과 같습니다. 활동이 완료되면 변수가 정리되고 변수를 더 이상 참조할 수 없습니다.  
  
## <a name="arguments"></a>인수  
 활동 작성자는 인수를 사용하여 데이터가 활동 내부 및 외부로 흐르는 방법을 정의합니다. 각 인수에는 <xref:System.Activities.ArgumentDirection.In>, <xref:System.Activities.ArgumentDirection.Out> 또는 <xref:System.Activities.ArgumentDirection.InOut>과 같은 지정된 방향이 있습니다.  
  
 워크플로 런타임은 활동 내부 및 외부로 데이터가 이동하는 타이밍에 대해 다음을 보장합니다.  
  
1. 활동이 실행되기 시작하면 모든 입력 및 입/출력 인수의 값이 계산됩니다. 예를 들어 <xref:System.Activities.Argument.Get%2A>이 호출되는 시간과 상관없이, 반환되는 값은 `Execute` 호출 전에 런타임에서 계산된 값입니다.  
  
2. <xref:System.Activities.InOutArgument%601.Set%2A>이 호출되면 런타임은 값을 즉시 설정합니다.  
  
3. 인수는 선택적으로 <xref:System.Activities.Argument.EvaluationOrder%2A>를 지정할 수 있습니다. <xref:System.Activities.Argument.EvaluationOrder%2A>는 인수를 평가하는 순서를 지정하는 0부터 시작하는 값입니다. 기본적으로 인수의 평가 순서는 지정되지 않으며 <xref:System.Activities.Argument.UnspecifiedEvaluationOrder> 값과 같습니다. <xref:System.Activities.Argument.EvaluationOrder%2A>를 0보다 크거나 같은 값으로 설정하여 이 인수의 평가 순서를 지정합니다. Windows Workflow Foundation에는 오름차순에서 지정한 평가 순서의 인수를 평가합니다. 평가 순서가 지정되지 않은 인수는 평가 순서가 지정된 인수 이전에 평가됩니다.  
  
 활동 작성자는 강력한 형식의 메커니즘을 사용하여 인수를 노출합니다. 이 작업은 <xref:System.Activities.InArgument%601>, <xref:System.Activities.OutArgument%601> 및 <xref:System.Activities.InOutArgument%601> 형식의 속성을 선언하여 수행됩니다. 이렇게 하면 활동 작성자가 활동 내부 및 외부로 이동하는 데이터에 대한 특정 계약을 설정할 수 있습니다.  
  
### <a name="defining-the-arguments-on-an-activity"></a>활동에서 인수 정의  
 <xref:System.Activities.InArgument%601>, <xref:System.Activities.OutArgument%601> 및 <xref:System.Activities.InOutArgument%601> 형식의 속성을 지정하여 활동에서 인수를 정의할 수 있습니다. 다음 코드에서는 사용자에게 표시할 문자열을 가져와서 사용자 응답을 포함하는 문자열을 반환하는 `Prompt` 활동에 대한 인수를 정의하는 방법을 보여 줍니다.  
  
```csharp  
public class Prompt : Activity  
{  
    public InArgument<string> Text { get; set; }  
    public OutArgument<string> Response { get; set; }  
    // Rest of activity definition omitted.  
}  
```  
  
> [!NOTE]
> 단일 값을 반환하는 활동은 <xref:System.Activities.Activity%601>, <xref:System.Activities.NativeActivity%601> 또는 <xref:System.Activities.CodeActivity%601>에서 파생될 수 있습니다. 이 활동에는 활동의 반환 값을 포함하는 <xref:System.Activities.OutArgument%601>라는 잘 정의된 <xref:System.Activities.Activity%601.Result%2A>이 있습니다.  
  
### <a name="using-variables-and-arguments-in-workflows"></a>워크플로에서 변수 및 인수 사용  
 다음 예제에서는 워크플로에서 변수와 인수를 사용하는 방법을 보여 줍니다. 워크플로는 `var1`, `var2` 및 `var3`이라는 세 가지 변수를 선언하는 시퀀스입니다. 워크플로의 첫 번째 활동은 `Assign` 변수에 `var1` 변수의 값을 할당하는 `var2` 활동입니다. 다음은 `WriteLine` 변수의 값을 인쇄하는 `var2` 활동입니다. 그 다음은 `Assign` 변수에 `var2` 변수의 값을 할당하는 다른 `var3` 활동입니다. 마지막으로 `WriteLine` 변수의 값을 인쇄하는 다른 `var3` 활동이 있습니다. 첫 번째 `Assign` 활동은 활동의 인수에 대한 바인딩을 명시적으로 나타내는 `InArgument<string>` 및 `OutArgument<string>` 개체를 사용합니다. `InArgument<string>`에서는 값은 <xref:System.Activities.Statements.Assign.Value%2A> 인수를 통해 <xref:System.Activities.Statements.Assign%601> 활동으로 전달되기 때문에 <xref:System.Activities.Statements.Assign.Value%2A>이 사용되고 `OutArgument<string>`에서는 값이 <xref:System.Activities.Statements.Assign.To%2A> 인수에서 변수로 전달되기 때문에 <xref:System.Activities.Statements.Assign.To%2A>이 사용됩니다. 두 번째 `Assign` 활동은 암시적 캐스트를 사용하는 더 간단하지만 동일한 구문을 사용하여 같은 작업을 수행합니다. `WriteLine` 활동도 간단한 구문을 사용합니다.  
  
```csharp  
// Declare three variables; the first one is given an initial value.  
Variable<string> var1 = new Variable<string>()  
{  
    Default = "one"  
};  
Variable<string> var2 = new Variable<string>();  
Variable<string> var3 = new Variable<string>();  
  
// Define the workflow  
Activity wf = new Sequence  
{  
    Variables = { var1, var2, var3 },  
    Activities =   
    {  
        new Assign<string>()  
        {  
            Value = new InArgument<string>(var1),  
            To = new OutArgument<string>(var2)  
        },  
        new WriteLine() { Text = var2 },  
        new Assign<string>()  
        {  
            Value = var2,  
            To = var3  
        },  
        new WriteLine() { Text = var3 }  
    }  
};  
  
WorkflowInvoker.Invoke(wf);  
```  
  
### <a name="using-variables-and-arguments-in-code-based-activities"></a>코드 기반 활동에서 변수 및 인수 사용  
 이전 예제에서는 워크플로 및 선언적 활동에서 인수와 변수를 사용하는 방법을 보여 줍니다. 인수와 변수는 코드 기반 활동에서도 사용됩니다. 개념상 사용법은 매우 유사합니다. 변수는 활동 내의 데이터 스토리지를 나타내고 인수는 활동 내부 및 외부로 흐르는 데이터 흐름을 나타내며 워크플로 작성자는 데이터가 흐르는 방향을 나타내는 워크플로의 다른 변수나 인수에 이를 바인딩합니다. 활동에서 변수 또는 인수의 값을 가져오거나 설정하려면 활동의 현재 실행 환경을 나타내는 활동 컨텍스트를 사용해야 합니다. 이 컨텍스트는 워크플로 런타임에서 활동의 <xref:System.Activities.CodeActivity%601.Execute%2A> 메서드에 전달됩니다. 이 예제에서는 `Add` 인수가 두 개 있는 사용자 지정 <xref:System.Activities.ArgumentDirection.In> 활동을 정의합니다. 인수의 값에 액세스하려면 <xref:System.Activities.Argument.Get%2A> 메서드를 사용하고 워크플로 런타임에서 전달된 컨텍스트를 사용합니다.  
  
```csharp  
public sealed class Add : CodeActivity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Operand1 { get; set; }  
  
    [RequiredArgument]  
    public InArgument<int> Operand2 { get; set; }  
  
    protected override int Execute(CodeActivityContext context)  
    {  
        return Operand1.Get(context) + Operand2.Get(context);  
    }  
}  
```  
  
 코드에서 인수, 변수 및 식을 사용 하는 방법에 대 한 자세한 내용은 명령적 코드 및 [필수 인수 및 오버 로드 그룹](required-arguments-and-overload-groups.md)을 [사용 하 여 워크플로, 활동 및 식 작성](authoring-workflows-activities-and-expressions-using-imperative-code.md) 을 참조 하세요.
