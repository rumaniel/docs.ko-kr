---
title: 선언적 제약 조건
ms.date: 03/30/2017
ms.assetid: 67001ed1-7f4d-4ada-ae57-a31176901a53
ms.openlocfilehash: e3ced8f6f88d698273ace5c8b74fe90b94fa9720
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945823"
---
# <a name="declarative-constraints"></a>선언적 제약 조건
선언적 제약 조건은 활동 및 활동과 다른 활동의 관계에 대한 강력한 유효성 검사 메서드를 제공합니다. 제약 조건이 제작 프로세스 중에 활동에 대해 구성되지만, 워크플로 호스트에서 추가 제약 조건을 지정할 수도 있습니다. 이 항목에서는 선언적 제약 조건을 사용하여 작업 유효성 검사를 제공하는 방법에 대해 간략하게 설명합니다.  
  
## <a name="using-declarative-constraints"></a>선언적 제약 조건 사용  
 제약 조건은 유효성 검사 논리를 포함하는 활동입니다. 이 제약 조건 작업을 코드 또는 XAML로 작성할 수 있습니다. 제약 조건 활동을 만든 후 작업 작성자는 유효성 검사를 수행할 작업의 <xref:System.Activities.Activity.Constraints%2A> 속성에 이 제약 조건을 추가합니다. 제약 조건을 사용하여 <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> 인스턴스의 <xref:System.Activities.Validation.ValidationSettings> 속성을 통해 추가 유효성 검사를 수행할 수도 있습니다. 유효성 검사 논리는 활동 메타데이터 유효성 검사와 같은 간단한 유효성 검사로 구성될 수도 있지만, 현재 활동과 부모, 자식 및 형제 활동 간의 관계를 고려하여 유효성 검사를 수행할 수도 있습니다. <xref:System.Activities.Validation.Constraint%601> 활동을 사용하여 제약 조건이 작성되며, 유효성 검사 오류 및 경고 생성을 지원하고 워크플로에서 관련 활동에 대한 정보를 제공하기 위한 여러 추가 유효성 검사 활동이 제공됩니다.  
  
### <a name="assertvalidation-and-addvalidationerror"></a>AssertValidation 및 AddValidationError  
 <xref:System.Activities.Validation.AssertValidation> 활동은 <xref:System.Activities.Validation.AssertValidation.Assertion%2A> 속성에서 참조되는 식을 평가합니다. 식이 `false`로 평가되면 유효성 검사 오류 또는 경고가 <xref:System.Activities.Validation.ValidationResults>에 추가됩니다. <xref:System.Activities.Validation.AssertValidation.Message%2A> 속성은 유효성 검사 오류에 대해 설명하고 <xref:System.Activities.Validation.AssertValidation.IsWarning%2A> 속성은 유효성 검사 실패가 오류인지 또는 경고인지를 나타냅니다. <xref:System.Activities.Validation.AssertValidation.IsWarning%2A>의 기본값은 `false`입니다.  
  
 다음 예제에서는 유효성 검사 중인 활동의 <xref:System.Activities.Activity.DisplayName%2A>이 2자 이하이면 유효성 검사 경고를 반환하는 제약 조건을 선언합니다. <xref:System.Activities.Validation.Constraint%601>에 대해 사용되는 제네릭 형식 매개 변수는 제약 조건에 따라 유효성이 검사되는 활동의 유형을 지정합니다. 이 제약 조건은 <xref:System.Activities.Activity>를 제네릭 형식으로 사용하며 모든 유형의 활동에 대해 유효성을 검사하는 데 이 제약 조건을 사용할 수 있습니다.  
  
```csharp  
public static Constraint ActivityDisplayNameIsNotSetWarning()  
{  
    DelegateInArgument<Activity> element = new DelegateInArgument<Activity>();  
  
    return new Constraint<Activity>  
    {  
        Body = new ActivityAction<Activity, ValidationContext>  
        {  
            Argument1 = element,  
            Handler = new AssertValidation  
            {  
                IsWarning = true,  
                Assertion = new InArgument<bool>(env => (element.Get(env).DisplayName.Length > 2)),  
                Message = new InArgument<string>("It is a best practice to have a DisplayName of more than 2 characters."),  
            }  
        }  
    };  
}  
```  
  
 활동에 대해 이 제약 조건을 지정하려면 다음 예제 코드처럼 제약 조건을 활동의 <xref:System.Activities.Activity.Constraints%2A>에 추가합니다.  
  
```csharp  
public sealed class SampleActivity : CodeActivity  
{  
    public SampleActivity()  
    {  
        base.Constraints.Add(ActivityDisplayNameIsNotSetWarning());  
    }  
  
    // Activity implementation omitted.  
}  
```  
  
 호스트에서 <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>를 사용하여 워크플로의 활동에 대해 이 제약 조건을 지정할 수도 있습니다. 이에 대해서는 다음 단원에서 설명합니다.  
  
 <xref:System.Activities.Validation.AddValidationError> 활동은 식을 평가하지 않고 유효성 검사 오류 또는 경고를 생성하는 데 사용됩니다. 이 활동의 속성은 <xref:System.Activities.Validation.AssertValidation>과 비슷하며 이 활동은 <xref:System.Activities.Statements.If> 활동과 같은 제약 조건 흐름 제어 활동과 함께 사용할 수 있습니다.
  
### <a name="workflow-relationship-activities"></a>워크플로 관계 활동

유효성 검사 중인 활동을 기준으로 워크플로의 다른 활동에 대한 정보를 제공하는 여러 유효성 검사 활동을 사용할 수 있습니다. <xref:System.Activities.Validation.GetParentChain>은 현재 활동과 루트 활동 사이의 모든 활동을 포함하는 활동 컬렉션을 반환합니다. <xref:System.Activities.Validation.GetChildSubtree>는 재귀 패턴의 자식 활동을 포함하는 활동 컬렉션을 제공하고 <xref:System.Activities.Validation.GetWorkflowTree>는 워크플로의 모든 활동을 가져옵니다.  
  
다음 예제에서는 `CreateState` 활동을 정의합니다. `CreateState` 활동이 `CreateCountry` 활동에 포함되어야 하고, `GetParent` 메서드는 이 요구 사항을 적용하는 제약 조건을 반환합니다. `GetParent`는 <xref:System.Activities.Validation.GetParentChain> 활동을 <xref:System.Activities.Statements.ForEach%601> 활동과 함께 사용하여 `CreateState` 활동의 부모 활동을 조사하여 요구 사항이 충족되는지 확인합니다.  
  
```csharp  
public sealed class CreateState : CodeActivity  
{  
    public CreateState()  
    {  
        base.Constraints.Add(CheckParent());  
        this.Cities = new List<Activity>();              
    }  
  
    public List<Activity> Cities { get; set; }  
  
    public string Name { get; set; }    
  
    static Constraint CheckParent()  
    {  
        DelegateInArgument<CreateState> element = new DelegateInArgument<CreateState>();  
        DelegateInArgument<ValidationContext> context = new DelegateInArgument<ValidationContext>();                          
        Variable<bool> result = new Variable<bool>();  
        DelegateInArgument<Activity> parent = new DelegateInArgument<Activity>();  
  
        return new Constraint<CreateState>  
        {                                     
            Body = new ActivityAction<CreateState,ValidationContext>  
            {                      
                Argument1 = element,  
                Argument2 = context,  
                Handler = new Sequence  
                {  
                    Variables =  
                    {  
                        result   
                    },  
                    Activities =  
                    {  
                        new ForEach<Activity>  
                        {                                  
                            Values = new GetParentChain  
                            {  
                                ValidationContext = context                                      
                            },  
                            Body = new ActivityAction<Activity>  
                            {     
                                Argument = parent,   
                                Handler = new If()  
                                {                                            
                                    Condition = new InArgument<bool>((env) => object.Equals(parent.Get(env).GetType(),typeof(CreateCountry))),                                          
                                    Then = new Assign<bool>  
                                    {  
                                        Value = true,  
                                        To = result  
                                    }  
                                }  
                            }                                  
                        },  
                        new AssertValidation  
                        {  
                            Assertion = new InArgument<bool>(result),  
                            Message = new InArgument<string> ("CreateState has to be inside a CreateCountry activity"),                                                                  
                        }  
                    }  
                }  
            }  
        };  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // not needed for the sample  
    }  
}  
```
  
## <a name="additional-constraints"></a>추가 제약 조건  
 워크플로 호스트 작성자는 제약 조건을 만든 후 <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> 인스턴스의 <xref:System.Activities.Validation.ValidationSettings> 사전에 추가하여 워크플로의 활동에 대한 추가 유효성 검사 제약 조건을 지정할 수 있습니다. <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>의 각 항목에는 제약 조건이 적용되는 활동 유형과 해당 활동 유형에 대한 추가 제약 조건 목록이 포함됩니다. 워크플로에 대한 유효성 검사를 호출하면 파생 클래스를 포함하여 지정된 유형의 각 활동에서 제약 조건을 평가합니다. 이 예제에서는 이전 섹션의 `ActivityDisplayNameIsNotSetWarning` 제약 조건이 워크플로의 모든 작업에 적용됩니다.  
  
```csharp  
Activity wf = new Sequence  
{  
    // Workflow Details Omitted.  
};  
  
ValidationSettings settings = new ValidationSettings()  
{  
  
    AdditionalConstraints =  
    {  
        {typeof(Activity), new List<Constraint> {ActivityDisplayNameIsNotSetWarning()}},       
    }  
};  
  
// Validate the workflow.  
ValidationResults results = ActivityValidationServices.Validate(wf, settings);  
  
// Evaluate the results.  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error in " + error.Source.DisplayName + ": " + error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning in " + warning.Source.DisplayName + ": " + warning.Message);  
    }  
}  
```  
  
 <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A>의 <xref:System.Activities.Validation.ValidationSettings> 속성이 `true`인 경우 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>를 호출하여 유효성 검사를 호출하면 지정된 추가 제약 조건만 평가됩니다. 이 기능은 특정 유효성 검사 구성에 대한 워크플로를 검사할 때 유용합니다. 워크플로를 호출하면 워크플로에 구성된 유효성 검사 논리를 평가하여 통과해야 워크플로가 시작됩니다. 유효성 검사를 호출 하는 방법에 대 한 자세한 내용은 참조 하십시오 [활동 유효성 검사 호출](invoking-activity-validation.md)합니다.
