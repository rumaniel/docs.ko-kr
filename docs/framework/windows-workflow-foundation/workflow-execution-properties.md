---
title: 워크플로 실행 속성
ms.date: 03/30/2017
ms.assetid: a50e088e-3a45-4267-bd51-1a3e6c2d246d
ms.openlocfilehash: 87775ba6efb9ec26ed2445e1f9d0944c379ba04f
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70988592"
---
# <a name="workflow-execution-properties"></a>워크플로 실행 속성
CLR은 TLS(스레드 로컬 스토리지)를 통해 각 스레드의 실행 컨텍스트를 유지 관리합니다. 이 실행 컨텍스트는 스레드 ID, 앰비언트 트랜잭션 및 현재 권한 집합과 같은 잘 알려진 스레드 속성은 물론 명명된 슬롯과 같은 사용자 정의 스레드 속성을 제어합니다.  
  
 CLR을 직접 대상으로 하는 프로그램과 달리 워크플로 프로그램은 스레드를 알 수 없는 환경에서 실행되는 계층적 범위의 활동 트리입니다. 이는 표준 TLS 메커니즘을 직접 사용하여 제공된 작업 항목 범위에 있는 컨텍스트를 확인할 수 없음을 의미합니다. 예를 들어 두 개의 병렬 실행 분기는 서로 다른 트랜잭션을 사용할 수 있지만 스케줄러는 동일한 CLR 스레드에서 해당 실행을 인터리브할 수 있습니다.  
  
 워크플로 실행 속성은 활동 환경에 컨텍스트별 속성을 추가하는 메커니즘을 제공합니다. 이 실행 속성을 통해 활동에서 해당 하위 트리 범위의 속성을 선언할 수 있을 뿐 아니라 CLR 개체와의 적절한 상호 작용을 위해 TLS를 설정 및 중지하는 후크를 제공할 수 있습니다.  
  
## <a name="creating-and-using-workflow-execution-properties"></a>워크플로 실행 속성 만들기 및 사용  
 워크플로 실행 속성은 보통<xref:System.Activities.IExecutionProperty> 인터페이스를 구현하고, 메시징에 중점을 둔 속성을 통해 대신 <xref:System.ServiceModel.Activities.ISendMessageCallback> 및 <xref:System.ServiceModel.Activities.IReceiveMessageCallback>을 구현합니다. 워크플로 실행 속성을 만들려면 <xref:System.Activities.IExecutionProperty> 인터페이스를 구현하는 클래스를 만들고 멤버 <xref:System.Activities.IExecutionProperty.SetupWorkflowThread%2A> 및 <xref:System.Activities.IExecutionProperty.CleanupWorkflowThread%2A>를 구현합니다. 이 멤버는 자식 활동을 비롯하여 속성이 포함된 활동의 각 작업 펄스 중 스레드 로컬 저장소를 올바르게 설정하고 중지할 기회를 실행 속성에 제공합니다. 이 예제에서는 `ConsoleColorProperty`를 설정하는 `Console.ForegroundColor`를 만듭니다.  
  
```csharp  
class ConsoleColorProperty : IExecutionProperty  
{  
    public const string Name = "ConsoleColorProperty";  
  
    ConsoleColor original;  
    ConsoleColor color;  
  
    public ConsoleColorProperty(ConsoleColor color)  
    {  
        this.color = color;  
    }  
  
    void IExecutionProperty.SetupWorkflowThread()  
    {  
        original = Console.ForegroundColor;  
        Console.ForegroundColor = color;  
    }  
  
    void IExecutionProperty.CleanupWorkflowThread()  
    {  
        Console.ForegroundColor = original;  
    }  
}  
```  
  
 활동 작성자는 활동 실행 재정의에 이 속성을 등록하여 속성을 사용할 수 있습니다. 이 예제에서는 `ConsoleColorScope`를 현재 `ConsoleColorProperty`의 <xref:System.Activities.NativeActivityContext.Properties%2A> 컬렉션에 추가하여 등록하는 <xref:System.Activities.NativeActivityContext> 활동을 정의합니다.  
  
```csharp  
public sealed class ConsoleColorScope : NativeActivity  
{  
    public ConsoleColorScope()  
        : base()  
    {  
    }  
  
    public ConsoleColor Color { get; set; }  
    public Activity Body { get; set; }  
  
    protected override void Execute(NativeActivityContext context)  
    {  
        context.Properties.Add(ConsoleColorProperty.Name, new ConsoleColorProperty(this.Color));  
  
        if (this.Body != null)  
        {  
            context.ScheduleActivity(this.Body);  
        }  
    }  
}  
```  
  
 활동 본문이 작업 펄스를 시작하면 속성의 <xref:System.Activities.IExecutionProperty.SetupWorkflowThread%2A> 메서드가 호출되고 작업 펄스가 완료되면 <xref:System.Activities.IExecutionProperty.CleanupWorkflowThread%2A>가 호출됩니다. 이 예제에서는 세 분기가 있는 <xref:System.Activities.Statements.Parallel> 활동을 사용하여 워크플로를 만듭니다. 처음 두 분기는 `ConsoleColorScope` 활동을 사용하고 세 번째 분기는 이 활동을 사용하지 않습니다. 세 분기에는 모두 <xref:System.Activities.Statements.WriteLine> 활동 두 개와 <xref:System.Activities.Statements.Delay> 활동 하나가 포함됩니다. <xref:System.Activities.Statements.Parallel> 활동이 실행되면 분기에 포함된 활동이 인터리브 방식으로 실행되지만, 각 자식 활동이 실행되면 `ConsoleColorProperty`에서 올바른 콘솔 색상이 적용됩니다.  
  
```csharp  
Activity wf = new Parallel  
{  
    Branches =   
    {  
        new ConsoleColorScope  
        {  
            Color = ConsoleColor.Blue,  
            Body = new Sequence  
            {  
                Activities =   
                {  
                    new WriteLine  
                    {  
                        Text = "Start blue text."  
                    },  
                    new Delay  
                    {  
                        Duration = TimeSpan.FromSeconds(1)  
                    },  
                    new WriteLine  
                    {  
                        Text = "End blue text."  
                    }  
                }  
            }  
        },  
        new ConsoleColorScope  
        {  
            Color = ConsoleColor.Red,  
            Body = new Sequence  
            {  
                Activities =   
                {  
                    new WriteLine  
                    {  
                        Text = "Start red text."  
                    },  
                    new Delay  
                    {  
                        Duration = TimeSpan.FromSeconds(1)  
                    },  
                    new WriteLine  
                    {  
                        Text = "End red text."  
                    }  
                }  
            }  
        },  
        new Sequence  
        {  
            Activities =   
            {  
                new WriteLine  
                {  
                    Text = "Start default text."  
                },  
                new Delay  
                {  
                    Duration = TimeSpan.FromSeconds(1)  
                },  
                new WriteLine  
                {  
                    Text = "End default text."  
                }  
            }  
        }  
    }  
};  
  
WorkflowInvoker.Invoke(wf);  
```  
  
 워크플로가 호출되면 다음 출력이 콘솔 창에 기록됩니다.  
  
```console  
Start blue text.  
Start red text.  
Start default text.  
End blue text.  
End red text.  
End default text.  
```  
  
> [!NOTE]
> 이전 출력에는 표시되지 않았지만 콘솔 창의 각 텍스트 행은 지정된 색상으로 표시됩니다.  
  
 워크플로 실행 속성은 사용자 지정 활동 작성자가 사용할 수 있으며, <xref:System.ServiceModel.Activities.CorrelationScope> 및 <xref:System.Activities.Statements.TransactionScope> 활동과 같은 활동의 처리 관리 메커니즘도 제공합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Activities.IExecutionProperty>
- <xref:System.Activities.IPropertyRegistrationCallback>
- <xref:System.Activities.RegistrationContext>
