---
title: 활동 유효성 검사 호출
ms.date: 03/30/2017
ms.assetid: 22bef766-c505-4fd4-ac0f-7b363b238969
ms.openlocfilehash: b45840081f5fc142cf3ec88853dea984b204c9d0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69934975"
---
# <a name="invoking-activity-validation"></a>활동 유효성 검사 호출
활동 유효성 검사를 사용하면 활동을 실행하기 이전에 활동 구성 오류를 식별하여 보고할 수 있습니다. Workflow Designer에서 워크플로를 수정하면 유효성 검사가 수행되어 Workflow Designer에 유효성 검사 오류 또는 경고가 표시됩니다. 워크플로를 호출하면 런타임에도 유효성 검사가 수행되며 유효성 검사 오류가 발생할 경우 기본 유효성 검사 논리에 따라 <xref:System.Activities.InvalidWorkflowException>이 throw됩니다. WF (Windows Workflow Foundation)는 워크플로 <xref:System.Activities.Validation.ActivityValidationServices> 응용 프로그램 및 도구 개발자가 활동의 유효성을 명시적으로 검사 하는 데 사용할 수 있는 클래스를 제공 합니다. 이 항목에서는 <xref:System.Activities.Validation.ActivityValidationServices>를 사용하여 활동 유효성 검사를 수행하는 방법에 대해 설명합니다.  
  
## <a name="using-activityvalidationservices"></a>ActivityValidationServices 사용  
 <xref:System.Activities.Validation.ActivityValidationServices>에는 활동 유효성 검사 논리를 호출하는 데 사용되는 두 가지 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 오버로드가 있습니다. 첫 번째 오버로드에서는 루트 활동의 유효성 검사하고 유효성 검사 및 경고 컬렉션을 반환합니다. 다음 예제에서는 두 필수 인수를 가진 사용자 지정 `Add` 활동을 사용합니다.  
  
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
  
 다음 예제에 표시된 것처럼 `Add` 활동은 <xref:System.Activities.Statements.Sequence> 내에서 사용되지만 두 필수 인수가 바인딩되지 않습니다.  
  
```csharp  
Variable<int> Operand1 = new Variable<int>{ Default = 10 };  
Variable<int> Operand2 = new Variable<int>{ Default = 15 };  
Variable<int> Result = new Variable<int>();  
  
Activity wf = new Sequence  
{  
    Variables = { Operand1, Operand2, Result },  
    Activities =   
    {  
        new Add(),  
        new WriteLine  
        {  
            Text = new InArgument<string>(env => "The result is " + Result.Get(env))  
        }  
    }  
};  
```  
  
 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>를 호출하여 이 워크플로의 유효성을 검사할 수 있습니다. 다음 예에 표시된 것처럼 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>는 활동과 해당 자식에 포함된 유효성 검사 오류 또는 경고 컬렉션을 반환합니다.  
  
```csharp  
ValidationResults results = ActivityValidationServices.Validate(wf);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 이 샘플 워크플로에서 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>를 호출하면 두 유효성 검사 오류가 반환됩니다.  
  
 **오류: 필수 작업 인수 ' 99&operand2 '의 값이 제공 되지 않았습니다.**  
**오류: 필수 작업 인수 ' Operand1 '의 값이 제공 되지 않았습니다.**  이 워크플로를 호출하면 다음 예제처럼 <xref:System.Activities.InvalidWorkflowException>이 throw됩니다.  
  
```csharp  
try  
{  
    WorkflowInvoker.Invoke(wf);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
 **System.Activities.InvalidWorkflowException:**  
**워크플로 트리를 처리 하는 동안 다음 오류가 발생 했습니다.**    
**' 추가 ': 필수 작업 인수 ' 99&operand2 '의 값이 제공 되지 않았습니다.**    
**' 추가 ': 필수 작업 인수 ' Operand1 '의 값이 제공 되지 않았습니다.**  이 예제 워크플로가 유효하려면 `Add` 활동의 두 필수 인수가 바인딩되어야 합니다. 다음 예제에서는 두 필수 인수가 워크플로 변수에 결과 값과 함께 바인딩됩니다. 이 예제에서 <xref:System.Activities.Activity%601.Result%2A> 인수는 두 필수 인수와 함께 바인딩됩니다. <xref:System.Activities.Activity%601.Result%2A> 인수는 바인딩될 필요가 없으므로 바인딩되지 않더라도 유효성 검사 오류가 발생하지 않습니다. <xref:System.Activities.Activity%601.Result%2A> 인수의 값이 워크플로의 다른 위치에서 사용될 경우 워크플로 작성자가 이 인수를 바인딩해야 합니다.  
  
```csharp  
new Add  
{  
    Operand1 = Operand1,  
    Operand2 = Operand2,  
    Result = Result  
}  
```  
  
### <a name="validating-required-arguments-on-the-root-activity"></a>루트 활동의 필수 인수 유효성 검사  
 워크플로의 루트 활동에 인수가 있는 경우 워크플로를 호출하여 매개 변수가 워크플로에 전달될 때까지는 해당 인수가 바인딩되지 않습니다. 따라서 다음 예제처럼 필수 인수를 전달하지 않고 워크플로를 호출하면 다음 워크플로가 유효성을 통과하지만 예외가 throw됩니다.  
  
```csharp  
Activity wf = new Add();  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
// results has no errors or warnings, but when the workflow  
// is invoked, an InvalidWorkflowException is thrown.  
try  
{  
    WorkflowInvoker.Invoke(wf);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
 **System.ArgumentException: 루트 활동의 인수 설정이 올바르지 않습니다.**  
**워크플로 정의를 수정 하거나 입력 값을 제공 하 여 이러한 오류를 해결 하십시오.**    
**' 추가 ': 필수 작업 인수 ' 99&operand2 '의 값이 제공 되지 않았습니다.**    
**' 추가 ': 필수 작업 인수 ' Operand1 '의 값이 제공 되지 않았습니다.**  다음 예제처럼 올바른 인수가 전달되면 워크플로가 완료됩니다.  
  
```csharp  
Add wf = new Add();  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
// results has no errors or warnings, and the workflow completes  
// successfully because the required arguments were passed.  
try  
{  
    Dictionary<string, object> wfparams = new Dictionary<string, object>  
    {  
        { "Operand1", 10 },  
        { "Operand2", 15 }  
    };  
  
    int result = WorkflowInvoker.Invoke(wf, wfparams);  
    Console.WriteLine("Result: {0}", result);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
> [!NOTE]
> 이 예제에서는 이전 예제처럼 루트 활동을 `Add`로 선언하는 대신 `Activity`로 선언했습니다. 이렇게 하면 `WorkflowInvoker.Invoke` 메서드가 `Add` 인수 사전 대신 `out` 활동 결과를 나타내는 단일 정수를 반환할 수 있습니다. 변수 `wf`가 `Activity<int>`로 선언되었을 수도 있습니다.  
  
 루트 인수의 유효성을 검사할 때 호스트 애플리케이션에서는 워크플로를 호출할 때 모든 필수 인수가 전달되는지 확인해야 합니다.  
  
### <a name="invoking-imperative-code-based-validation"></a>명령 코드 기반 유효성 검사 호출

명령형 코드 기반 유효성 검사를 이용하면 활동 자체에서 활동 유효성 검사를 간단히 실행할 수 있으며 <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity> 및 <xref:System.Activities.NativeActivity>의 파생 활동에도 사용할 수 있습니다. 유효성 검사 오류 또는 경고를 판단하는 유효성 검사 코드가 활동에 추가됩니다. 활동에 유효성 검사가 호출되면 이러한 경고 또는 오류가 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 호출에서 반환된 컬렉션에 포함됩니다. 다음 예제에서는 `CreateProduct` 활동을 정의합니다. 다음 예에서 `Cost`가 `Price`보다 크면 <xref:System.Activities.CodeActivity.CacheMetadata%2A> 재정의 메타데이터에 유효성 검사 오류가 추가됩니다.  
  
```csharp  
public sealed class CreateProduct : CodeActivity  
{  
    public double Price { get; set; }  
    public double Cost { get; set; }  
  
    // [RequiredArgument] attribute will generate a validation error   
    // if the Description argument is not set.  
    [RequiredArgument]  
    public InArgument<string> Description { get; set; }  
  
    protected override void CacheMetadata(CodeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        // Determine when the activity has been configured in an invalid way.  
        if (this.Cost > this.Price)  
        {  
            // Add a validation error with a custom message.  
            metadata.AddValidationError("The Cost must be less than or equal to the Price.");  
        }  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // Not needed for the sample.  
    }  
}  
```  
  
 이 예제에서 워크플로는 `CreateProduct` 활동을 사용하여 구성됩니다. 이 워크플로에서 `Cost`는 `Price`보다 크고 필수 `Description` 인수는 설정되지 않습니다. 유효성 검사가 호출되면 다음 오류가 반환됩니다.  
  
```csharp  
Activity wf = new Sequence  
{  
    Activities =   
    {  
        new CreateProduct  
        {  
            Cost = 75.00,  
            Price = 55.00  
            // Cost > Price and required Description argument not set.  
        },  
        new WriteLine  
        {  
            Text = "Product added."  
        }  
    }  
};  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 **오류: 비용은 가격과 같거나 작아야 합니다.**  
**오류: 필수 작업 인수 ' Description '의 값이 제공 되지 않았습니다.**    
> [!NOTE]
> 사용자 지정 활동 작성자는 활동의 <xref:System.Activities.CodeActivity.CacheMetadata%2A> 재정의에서 유효성 검사 논리를 제공할 수 있습니다. <xref:System.Activities.CodeActivity.CacheMetadata%2A>에서 throw되는 모든 예외는 유효성 검사 오류로 처리되지 않습니다. 이러한 예외는 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>에 대한 호출에서 이스케이프되며 호출자가 처리해야 합니다.  
  
## <a name="using-validationsettings"></a>ValidationSettings 사용  
 <xref:System.Activities.Validation.ActivityValidationServices>에서 유효성 검사를 호출하면 기본적으로 활동 트리의 모든 활동이 평가됩니다. <xref:System.Activities.Validation.ValidationSettings> 을 사용하면 세 가지 속성을 구성하여 유효성 검사를 다양한 방법으로 사용자 지정할 수 있습니다. <xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A>은 유효성 검사기에서 전체 활동 트리를 검사해야 할지 또는 제공된 활동에만 유효성 검사 논리를 적용해야 할지 지정합니다. 기본값은 `false`입니다. <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>는 형식에서 제약 조건 목록으로 매핑하는 추가 제약 조건을 지정합니다. 유효성을 검사 중인 활동 트리에 있는 각 활동의 기본 형식에 대해 <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>를 조회합니다. 일치하는 제약 조건 목록이 있는 경우 활동에 대한 목록의 모든 제약 조건을 평가합니다. <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A>는 유효성 검사기에서 모든 제약 조건을 평가해야 할지 또는 <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>에 지정된 제약 조건만 평가해야 할지 지정합니다. 기본값은 `false`입니다. <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> 및 <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A>는 워크플로 호스트 작성자가 워크플로에 대한 유효성 검사(예: FxCop와 같은 도구에 대한 정책 제약 조건)를 추가하는 데 유용합니다 제약 조건에 대 한 자세한 내용은 [선언적 제약 조건](declarative-constraints.md)을 참조 하세요.  
  
 <xref:System.Activities.Validation.ValidationSettings>를 사용하려면 원하는 속성을 구성한 다음 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> 호출 시 전달합니다. 이 예제에서는 <xref:System.Activities.Statements.Sequence>와 사용자 지정 `Add` 활동으로 구성되는 워크플로의 유효성을 검사합니다. `Add` 활동에는 두 가지 필수 인수가 있습니다.  
  
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
  
 다음 `Add` 활동은 <xref:System.Activities.Statements.Sequence>에서 사용되지만 두 필수 인수는 바인딩되지 않습니다.  
  
```csharp  
Variable<int> Operand1 = new Variable<int> { Default = 10 };  
Variable<int> Operand2 = new Variable<int> { Default = 15 };  
Variable<int> Result = new Variable<int>();  
  
Activity wf = new Sequence  
{  
    Variables = { Operand1, Operand2, Result },  
    Activities =   
    {  
        new Add(),  
        new WriteLine  
        {  
            Text = new InArgument<string>(env => "The result is " + Result.Get(env))  
        }  
    }  
};  
```  
  
 다음 예제에서는 <xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A>을 `true`로 설정한 상태에서 유효성 검사를 수행하므로 루트 <xref:System.Activities.Statements.Sequence> 활동만 유효성을 검사합니다.  
  
```csharp  
ValidationSettings settings = new ValidationSettings  
{  
    SingleLevel = true  
};  
  
ValidationResults results = ActivityValidationServices.Validate(wf, settings);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 이 코드의 출력은 다음과 같습니다.  
  
 **경고 또는 오류 없음** 활동에 `Add` 바인딩되지 않은 필수 인수가 있지만 루트 활동만 평가 되기 때문에 유효성 검사가 성공 합니다. 이러한 유형의 유효성 검사는 활동 트리에서 특정 요소만 유효성을 검사(예: 디자이너의 단일 활동에 대한 속성 변경 유효성 검사)할 때 유용합니다. 이 워크플로를 호출하면 워크플로에 구성된 전체 유효성 검사가 수행되고 <xref:System.Activities.InvalidWorkflowException>이 throw됩니다. <xref:System.Activities.Validation.ActivityValidationServices> 및 <xref:System.Activities.Validation.ValidationSettings>는 호스트에서 명시적으로 호출되는 유효성 검사만 구성하고 워크플로를 호출할 때 발생하는 유효성 검사는 구성하지 않습니다.
