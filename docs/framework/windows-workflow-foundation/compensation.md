---
title: 보정
ms.date: 03/30/2017
ms.assetid: 722e9766-48d7-456c-9496-d7c5c8f0fa76
ms.openlocfilehash: 147da26fd297d41876815cffcc70450ae905ba85
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69935424"
---
# <a name="compensation"></a>보정
WF (Windows Workflow Foundation)는 이후 오류가 발생할 때 응용 프로그램에서 정의 된 논리에 따라 이전에 완료 된 작업을 실행 취소 하거나 보정 하는 메커니즘입니다. 이 단원에서는 워크플로에서 보정을 사용하는 방법에 대해 설명합니다.  
  
## <a name="compensation-vs-transactions"></a>보정과 의  
 트랜잭션을 사용하여 여러 작업을 하나의 작업 단위로 결합할 수 있습니다. 트랜잭션을 사용하면 애플리케이션은 트랜잭션 처리의 어떠한 부분에서도 오류가 발생하지 않은 경우 트랜잭션 내부에서 실행된 모든 변경 내용을 취소(롤백)할 수 있습니다. 그러나 작업이 오래 실행되는 경우에는 트랜잭션을 사용하는 방법이 적합하지 않습니다. 예를 들어 여행 계획 애플리케이션은 워크플로로 구현됩니다. 이 워크플로의 각 단계는 항공권 예약, 관리자 승인 대기, 항공권 결제로 구성될 수 있습니다. 이 과정에 며칠이 걸릴 수도 있으므로 항공권 예약 및 결제 단계를 같은 트랜잭션으로 묶는 방법은 적절하지 않습니다. 이 시나리오에서는 보정을 사용하여 이후 처리 과정에서 오류가 발생하면 워크플로의 예약 단계를 취소할 수 있습니다.  
  
> [!NOTE]
> 이 항목에서는 워크플로의 보정에 대해 설명합니다. 워크플로의 트랜잭션에 대 한 자세한 내용은 [트랜잭션](workflow-transactions.md) 및 <xref:System.Activities.Statements.TransactionScope>을 참조 하십시오. 트랜잭션에 대 한 자세한 내용은 및 <xref:System.Transactions?displayProperty=nameWithType> <xref:System.Transactions.Transaction?displayProperty=nameWithType>을 참조 하십시오.  
  
## <a name="using-compensableactivity"></a>CompensableActivity 사용  
 <xref:System.Activities.Statements.CompensableActivity>는 [!INCLUDE[wf1](../../../includes/wf1-md.md)]의 핵심 보정 활동입니다. 보정이 필요할 수 있는 작업을 수행하는 활동은 <xref:System.Activities.Statements.CompensableActivity.Body%2A>의 <xref:System.Activities.Statements.CompensableActivity>에 배치됩니다. 이 예제에서는 항공권 구매 예약 단계가 <xref:System.Activities.Statements.CompensableActivity.Body%2A>의 <xref:System.Activities.Statements.CompensableActivity>에 배치되고 예약 취소가 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>에 배치됩니다. 워크플로의 <xref:System.Activities.Statements.CompensableActivity> 바로 다음에 관리자 승인을 대기하고 항공권 구매 단계를 완료하는 두 활동이 옵니다. <xref:System.Activities.Statements.CompensableActivity>를 완료한 이후에 오류 조건으로 인해 워크플로가 취소될 경우 <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A> 처리기의 활동이 예약되고 항공권이 취소됩니다.  
  
 [!code-csharp[CFX_CompensationExample#1](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#1)]  
  
 다음 예제는 XAML 형식의 워크플로입니다.  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken" />  
    </CompensableActivity.Result>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
    <c:ReserveFlight />  
  </CompensableActivity>  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
</Sequence>  
```  
  
 워크플로가 호출되면 다음 출력이 콘솔에 표시됩니다.  
  
 **ReserveFlight: 티켓이 예약 되어 있습니다.**  
**관리자 승인: 관리자 승인이 수신 되었습니다.**    
**PurchaseFlight: 티켓을 구매 합니다.**    
**워크플로가 완료 되었으나 상태: 닫히면.**    
> [!NOTE]
> 이 항목에서 `ReserveFlight`와 같은 샘플 활동은 이름과 목적을 콘솔에 표시하여 보정이 발생하는 경우 활동의 실행 순서를 보여 줄 수 있습니다.  
  
### <a name="default-workflow-compensation"></a>기본 워크플로 보정  
 기본적으로 워크플로가 취소되면 성공적으로 완료되었지만 아직 확인되거나 보정되지 않은 보정 가능한 활동에 대한 보정 논리가 실행됩니다.  
  
> [!NOTE]
> 이 확인 되 면 작업에 대 한 보정을 더 이상 호출할 수 없습니다. <xref:System.Activities.Statements.CompensableActivity> 확인 프로세스에 대해서는 이 단원의 뒷부분에서 설명합니다.  
  
 이 예제에서는 항공권을 예약한 이후에 관리자 승인 단계 이전에 예외가 throw됩니다.  
  
 [!code-csharp[CFX_CompensationExample#2](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#2)]  
  
 이 예제는 XAML 형식의 워크플로입니다.  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken" />  
    </CompensableActivity.Result>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
    <c:ReserveFlight />  
  </CompensableActivity>  
  <c:SimulatedErrorCondition />  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
</Sequence>  
```  
  
 [!code-csharp[CFX_CompensationExample#100](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#100)]  
  
 워크플로가 호출되면 <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>에서 호스트 애플리케이션이 시뮬레이션된 오류 조건 예외를 처리하고 워크플로가 취소되고 보정 논리가 호출됩니다.  
  
 **ReserveFlight: 티켓이 예약 되어 있습니다.**  
**SimulatedErrorCondition: ApplicationException을 throw 합니다.**    
**워크플로 처리 되지 않은 예외:**    
**System.ApplicationException: 워크플로의 시뮬레이션 된 오류 조건입니다.**    
**CancelFlight: 티켓이 취소 되었습니다.**    
**워크플로가 완료 되었으나 상태: 님.**    
### <a name="cancellation-and-compensableactivity"></a>취소 및 CompensableActivity  
 <xref:System.Activities.Statements.CompensableActivity.Body%2A>의 <xref:System.Activities.Statements.CompensableActivity>에 있는 활동이 완료되지 않은 상태에서 활동이 취소되면 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>의 활동이 실행됩니다.  
  
> [!NOTE]
> <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>는 <xref:System.Activities.Statements.CompensableActivity.Body%2A>의 <xref:System.Activities.Statements.CompensableActivity>에 있는 활동이 완료되지 않은 상태에서 활동이 취소되는 경우에만 호출됩니다. <xref:System.Activities.Statements.CompensableActivity.CompensationHandler%2A>는 <xref:System.Activities.Statements.CompensableActivity.Body%2A>의 <xref:System.Activities.Statements.CompensableActivity>에 있는 활동이 성공적으로 완료된 다음 활동에 대해 보정이 호출되는 경우에만 실행됩니다.  
  
 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>는 워크플로 작성자에게 적절한 취소 논리를 제공합니다. 다음 예제에서는 <xref:System.Activities.Statements.CompensableActivity.Body%2A>가 실행되는 동안 예외가 throw된 다음 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>가 호출됩니다.  
  
```csharp  
Activity wf = new Sequence()  
{  
    Activities =  
    {  
        new CompensableActivity  
        {  
            Body = new Sequence  
            {  
                Activities =   
                {  
                    new ChargeCreditCard(),  
                    new SimulatedErrorCondition(),  
                    new ReserveFlight()  
                }  
            },  
            CompensationHandler = new CancelFlight(),  
            CancellationHandler = new CancelCreditCard()  
        },  
        new ManagerApproval(),  
        new PurchaseFlight()  
    }  
};  
```  
  
 이 예제는 XAML 형식의 워크플로입니다.  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken" />  
    </CompensableActivity.Result>  
    <Sequence>  
      <c:ChargeCreditCard />  
      <c:SimulatedErrorCondition />  
      <c:ReserveFlight />  
    </Sequence>  
    <CompensableActivity.CancellationHandler>  
      <c:CancelCreditCard />  
    </CompensableActivity.CancellationHandler>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
  </CompensableActivity>  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
</Sequence>  
```  
  
 워크플로가 호출되면 <xref:System.Activities.WorkflowApplication.OnUnhandledException%2A>에서 호스트 애플리케이션이 시뮬레이션된 오류 조건 예외를 처리하고 워크플로가 취소되고 <xref:System.Activities.Statements.CompensableActivity>의 취소 논리가 호출됩니다. 이 예제에서는 보정 논리와 취소 논리가 다른 목표를 가지고 있습니다. <xref:System.Activities.Statements.CompensableActivity.Body%2A>가 성공적으로 완료되면 신용 카드가 청구되고 비행기가 예약되었으므로 보정은 두 단계 모두 실행 취소해야 합니다. 이 예제에서 비행기를 취소하면 자동으로 신용 카드 청구를 취소합니다. 하지만 <xref:System.Activities.Statements.CompensableActivity>가 취소되면 <xref:System.Activities.Statements.CompensableActivity.Body%2A>가 완료되지 않았으므로 취소를 가장 잘 처리하는 방법을 결정할 수 있도록 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>의 논리가 필요합니다. 이 예제에서 <xref:System.Activities.Statements.CompensableActivity.CancellationHandler%2A>가 신용 카드 청구를 취소하지만 `ReserveFlight`가 <xref:System.Activities.Statements.CompensableActivity.Body%2A>에서 마지막 활동이었으므로 비행기를 취소하려고 하지 않습니다. `ReserveFlight`가 <xref:System.Activities.Statements.CompensableActivity.Body%2A>에서 마지막 활동이었으므로 성공적으로 완료되었다면 <xref:System.Activities.Statements.CompensableActivity.Body%2A>가 완료되었으므로 가능한 취소도 없습니다.  
  
 **ChargeCreditCard: 비행 신용 카드로 청구 합니다.**  
**SimulatedErrorCondition: ApplicationException을 throw 합니다.**    
**워크플로 처리 되지 않은 예외:**    
**System.ApplicationException: 워크플로의 시뮬레이션 된 오류 조건입니다.**    
**CancelCreditCard: 신용 카드 요금을 취소 합니다.**    
**워크플로가 완료 되었으나 상태: 님.**  취소에 대 한 자세한 내용은 [취소](modeling-cancellation-behavior-in-workflows.md)를 참조 하세요.  
  
### <a name="explicit-compensation-using-the-compensate-activity"></a>보정 활동을 통한 명시적 보정  
 이전 단원에서는 암시적 보정에 대해 설명했습니다. 암시적 보정은 간단한 시나리오에 적합하지만, 보정 처리 일정에 대한 보다 명시적인 제어가 필요할 경우 <xref:System.Activities.Statements.Compensate> 활동을 사용할 수 있습니다. <xref:System.Activities.Statements.Compensate> 활동을 사용하여 보정 프로세스를 시작하려면 보정을 원하는 <xref:System.Activities.Statements.CompensationToken>의 <xref:System.Activities.Statements.CompensableActivity>이 사용됩니다. <xref:System.Activities.Statements.Compensate> 활동을 사용하면 완료되었지만 아직 확인되거나 보정되지 않은 <xref:System.Activities.Statements.CompensableActivity>에 대한 보정을 시작할 수 있습니다. 예를 들어 <xref:System.Activities.Statements.Compensate> 활동을 <xref:System.Activities.Statements.TryCatch.Catches%2A> 활동의 <xref:System.Activities.Statements.TryCatch> 섹션에서 또는 <xref:System.Activities.Statements.CompensableActivity>가 완료된 이후에 언제든지 사용할 수 있습니다. 이 예제에서는 <xref:System.Activities.Statements.Compensate> 활동의 <xref:System.Activities.Statements.TryCatch.Catches%2A> 섹션에서 <xref:System.Activities.Statements.TryCatch> 활동을 사용하여 <xref:System.Activities.Statements.CompensableActivity>의 동작을 되돌립니다.  
  
 [!code-csharp[CFX_CompensationExample#3](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#3)]  
  
 이 예제는 XAML 형식의 워크플로입니다.  
  
```xaml  
<TryCatch  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:s="clr-namespace:System;assembly=mscorlib"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <TryCatch.Variables>  
    <Variable  
       x:TypeArguments="CompensationToken"  
       x:Name="__ReferenceID0"  
       Name="token1" />  
  </TryCatch.Variables>  
  <TryCatch.Try>  
    <Sequence>  
      <CompensableActivity>  
        <CompensableActivity.Result>  
          <OutArgument  
             x:TypeArguments="CompensationToken">  
            <VariableReference  
               x:TypeArguments="CompensationToken"  
               Variable="{x:Reference __ReferenceID0}">  
              <VariableReference.Result>  
                <OutArgument  
                   x:TypeArguments="Location(CompensationToken)" />  
              </VariableReference.Result>  
            </VariableReference>  
          </OutArgument>  
        </CompensableActivity.Result>  
        <CompensableActivity.CompensationHandler>  
          <c:CancelFlight />  
        </CompensableActivity.CompensationHandler>  
        <CompensableActivity.ConfirmationHandler>  
          <c:ConfirmFlight />  
        </CompensableActivity.ConfirmationHandler>  
        <c:ReserveFlight />  
      </CompensableActivity>  
      <c:SimulatedErrorCondition />  
      <c:ManagerApproval />  
      <c:PurchaseFlight />  
    </Sequence>  
  </TryCatch.Try>  
  <TryCatch.Catches>  
    <Catch  
       x:TypeArguments="s:ApplicationException">  
      <ActivityAction  
         x:TypeArguments="s:ApplicationException">  
        <Compensate>  
          <Compensate.Target>  
            <InArgument  
               x:TypeArguments="CompensationToken">  
              <VariableValue  
                 x:TypeArguments="CompensationToken"  
                 Variable="{x:Reference __ReferenceID0}">  
                <VariableValue.Result>  
                  <OutArgument  
                     x:TypeArguments="CompensationToken" />  
                </VariableValue.Result>  
              </VariableValue>  
            </InArgument>  
          </Compensate.Target>  
        </Compensate>  
      </ActivityAction>  
    </Catch>  
  </TryCatch.Catches>  
</TryCatch>  
```  
  
 워크플로가 호출되면 다음 출력이 콘솔에 표시됩니다.  
  
 **ReserveFlight: 티켓이 예약 되어 있습니다.**  
**SimulatedErrorCondition: ApplicationException을 throw 합니다.**    
**CancelFlight: 티켓이 취소 되었습니다.**    
**워크플로가 완료 되었으나 상태: 닫히면.**    
### <a name="confirming-compensation"></a>보정 확인  
 기본적으로 보정 가능한 활동은 완료된 이후에 언제든지 보정할 수 있습니다. 일부 시나리오에서는 이 방법이 적합하지 않을 수 있습니다. 이전 예제에서는 예약을 취소하기 위해 티켓 예약에 대한 보정을 수행했습니다. 하지만 항공권이 완료된 이후에는 이 보정 단계는 더 이상 유효하지 않습니다. 보정 가능한 활동을 확인하면 <xref:System.Activities.Statements.CompensableActivity.ConfirmationHandler%2A>가 지정한 활동이 호출됩니다. 예를 들어 보정을 수행하는 데 필요한 리소스를 릴리스할 수 있습니다. 보정 가능한 활동이 확인된 이후에는 활동을 보정할 수 없습니다. 이 경우 보정을 시도하면 <xref:System.InvalidOperationException> 예외가 throw됩니다. 워크플로가 성공적으로 완료되면 완료되었지만 확인되거나 보정되지 않은 모든 보정 가능한 활동이 완료된 역순으로 확인됩니다. 이 예제에서는 항공권을 예약하고 구매한 후 완료하면 보정 가능한 활동이 확인됩니다. <xref:System.Activities.Statements.CompensableActivity>를 확인하려면 <xref:System.Activities.Statements.Confirm> 활동을 사용하고 확인할 <xref:System.Activities.Statements.CompensationToken>의 <xref:System.Activities.Statements.CompensableActivity>을 지정합니다.  
  
 [!code-csharp[CFX_CompensationExample#4](~/samples/snippets/csharp/VS_Snippets_CFX/CFX_CompensationExample/cs/Program.cs#4)]  
  
 이 예제는 XAML 형식의 워크플로입니다.  
  
```xaml  
<Sequence  
   xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"  
   xmlns:c="clr-namespace:CompensationExample;assembly=CompensationExample"  
   xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
  <Sequence.Variables>  
    <x:Reference>__ReferenceID0</x:Reference>  
  </Sequence.Variables>  
  <CompensableActivity>  
    <CompensableActivity.Result>  
      <OutArgument  
         x:TypeArguments="CompensationToken">  
        <VariableReference  
           x:TypeArguments="CompensationToken">  
          <VariableReference.Result>  
            <OutArgument  
               x:TypeArguments="Location(CompensationToken)" />  
          </VariableReference.Result>  
          <VariableReference.Variable>  
            <Variable  
               x:TypeArguments="CompensationToken"  
               x:Name="__ReferenceID0"  
               Name="token1" />  
          </VariableReference.Variable>  
        </VariableReference>  
      </OutArgument>  
    </CompensableActivity.Result>  
    <CompensableActivity.CompensationHandler>  
      <c:CancelFlight />  
    </CompensableActivity.CompensationHandler>  
    <CompensableActivity.ConfirmationHandler>  
      <c:ConfirmFlight />  
    </CompensableActivity.ConfirmationHandler>  
    <c:ReserveFlight />  
  </CompensableActivity>  
  <c:ManagerApproval />  
  <c:PurchaseFlight />  
  <c:TakeFlight />  
  <Confirm>  
    <Confirm.Target>  
      <InArgument  
         x:TypeArguments="CompensationToken">  
        <VariableValue  
           x:TypeArguments="CompensationToken"  
           Variable="{x:Reference __ReferenceID0}">  
          <VariableValue.Result>  
            <OutArgument  
               x:TypeArguments="CompensationToken" />  
          </VariableValue.Result>  
        </VariableValue>  
      </InArgument>  
    </Confirm.Target>  
  </Confirm>  
</Sequence>  
```  
  
워크플로가 호출되면 다음 출력이 콘솔에 표시됩니다.  
  
**ReserveFlight: 티켓이 예약 되어 있습니다.**  
**관리자 승인: 관리자 승인이 수신 되었습니다.**    
**PurchaseFlight: 티켓을 구매 합니다.**    
**TakeFlight: 비행이 완료 되었습니다.**    
**가 중 비행: 비행이 발생 했으며 보정을 수행할 수 없습니다.**    
**워크플로가 완료 되었으나 상태: 닫히면.**   

## <a name="nesting-compensation-activities"></a>보정 활동 중첩  

<xref:System.Activities.Statements.CompensableActivity>를 다른 <xref:System.Activities.Statements.CompensableActivity.Body%2A>의 <xref:System.Activities.Statements.CompensableActivity> 섹션에 배치할 수 있습니다. <xref:System.Activities.Statements.CompensableActivity>가 다른 <xref:System.Activities.Statements.CompensableActivity>의 처리기에 배치되지 않을 수도 있습니다. 이는 부모 <xref:System.Activities.Statements.CompensableActivity>의 책임입니다. 활동을 취소, 확인 또는 보정할 경우 성공적으로 완료되었지만 아직 확인 또는 보정되지 않은 보정 가능한 모든 자식 활동은 부모가 취소, 확인 또는 보정을 완료하기 전에 확인 또는 보정되어야 합니다. 이러한 내용이 명시적으로 모델링되지 않은 경우 부모가 취소 또는 보정 신호를 받으면 부모 <xref:System.Activities.Statements.CompensableActivity>는 보정 가능한 활동을 암시적으로 보정합니다. 부모가 확인 신호를 받으면 부모는 보정 가능한 자식 활동을 암시적으로 확인합니다. 취소, 확인 또는 보정을 처리하는 논리가 부모 <xref:System.Activities.Statements.CompensableActivity>의 처리기에 명시적으로 모델링되어 있을 경우 명시적으로 처리되지 않은 모든 자식은 암시적으로 확인됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Activities.Statements.CompensableActivity>
- <xref:System.Activities.Statements.Compensate>
- <xref:System.Activities.Statements.Confirm>
- <xref:System.Activities.Statements.CompensationToken>
