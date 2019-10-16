---
title: 요청-회신 상관 관계
ms.date: 03/30/2017
ms.assetid: cf4379bf-2d08-43f3-9584-dfa30ffcb1f6
ms.openlocfilehash: c38854ad42ad4dddce5171482f3ddcfe5bd16b61
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61991135"
---
# <a name="request-reply-correlation"></a>요청-회신 상관 관계
요청-회신 상관 관계와 함께 사용 됩니다는 <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> 쌍 및 워크플로 서비스에서 양방향 작업을 구현 하는 <xref:System.ServiceModel.Activities.Send> / <xref:System.ServiceModel.Activities.ReceiveReply> 다른 웹에서 양방향 작업을 호출 하는 쌍 서비스입니다. WCF 서비스에서 양방향 작업을 호출 하는 경우, 서비스는 기존의 수 명령형 코드 기반 Windows Communication Foundation (WCF) 서비스 이거나 워크플로 서비스 일 수 있습니다. 요청-회신 상관 관계를 사용하려면 <xref:System.ServiceModel.BasicHttpBinding>과 같은 양방향 바인딩을 사용해야 합니다. 상관 관계 초기화 단계는 양방향 작업을 호출하는지 또는 양방향 작업을 구현하는지에 관계없이 비슷합니다. 이 단원에서는 이러한 상관 관계 초기화 단계에 대해 설명합니다.  
  
## <a name="using-correlation-in-a-two-way-operation-with-receivesendreply"></a>Receive/SendReply가 있는 양방향 작업에서 상관 관계 사용  
 A <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> 쌍은 워크플로 서비스에서 양방향 작업을 구현 하는 데 사용 됩니다. 런타임에서는 요청-회신 상관 관계를 사용하여 회신이 올바른 호출자에 디스패치되는지 확인합니다. 워크플로가 <xref:System.ServiceModel.Activities.WorkflowServiceHost>를 사용하여 호스트되는 경우, 즉 서비스가 워크플로 서비스인 경우 기본 상관 관계 초기화로 충분합니다. 이 시나리오에는 <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> 쌍이 워크플로 사용 하 고 특정 상관 관계 구성은 필요 하지 않습니다.  
  
```csharp  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder"  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
// Construct a workflow using StartOrder and ReplyToStartOrder.  
```  
  
### <a name="explicitly-initializing-request-reply-correlation"></a>명시적으로 요청-회신 상관 관계 초기화  
 여러 개의 양방향 작업이 나란히 있는 경우 상관 관계를 명시적으로 구성해야 합니다. 지정 하 여 수행할 수 있습니다이 <xref:System.ServiceModel.Activities.CorrelationHandle> 및 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer>, 또는 배치 하 여를 <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> 내에 <xref:System.ServiceModel.Activities.CorrelationScope>합니다. 이 예제에서는 요청-회신 상관 관계에 구성 되어는 <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> 쌍입니다.  
  
```csharp  
Variable<CorrelationHandle> RRHandle = new Variable<CorrelationHandle>();  
  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder",  
    CorrelationInitializers =  
    {  
        new RequestReplyCorrelationInitializer  
        {  
            CorrelationHandle = RRHandle  
        }  
    }  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
// Construct a workflow using StartOrder and ReplyToStartOrder.  
```  
  
 상관 관계를 명시적으로 구성하는 대신 <xref:System.ServiceModel.Activities.CorrelationScope> 작업을 사용할 수 있습니다. <xref:System.ServiceModel.Activities.CorrelationScope>는 해당 작업에 포함된 메시징 작업에 암시적 <xref:System.ServiceModel.Activities.CorrelationHandle>을 제공합니다. 이 예제는 <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> 쌍 내에 포함 되어는 <xref:System.ServiceModel.Activities.CorrelationScope>합니다. 명시적 상관 관계 구성은 필요 없습니다.  
  
```csharp  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder"  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
CorrelationScope s = new CorrelationScope  
{  
    Body = new Sequence  
    {  
        Activities =   
        {  
            StartOrder,  
            // Activities that create the reply.  
            ReplyToStartOrder  
        }  
    }  
};  
  
// Construct a workflow using the CorrelationScope.  
```  
  
 추가 상관 관계가 필요한 경우 원하는 <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> 형식을 사용하여 해당 메시징 작업의 `CorrelationInitializer` 속성을 통해 필요한 상관 관계를 구성할 수 있습니다.  
  
## <a name="using-correlation-in-a-two-way-operation-with-sendreceivereply"></a>Send/ReceiveReply가 있는 양방향 작업에서 상관 관계 사용  
 하는 동안를 <xref:System.ServiceModel.Activities.Receive> 작업에서 호스팅되는 워크플로 서비스에서 사용할 수 있습니다 <xref:System.ServiceModel.Activities.WorkflowServiceHost>, <xref:System.ServiceModel.Activities.Send> 및 <xref:System.ServiceModel.Activities.Send> / <xref:System.ServiceModel.Activities.ReceiveReply> 쌍을 웹 서비스에서 메서드를 호출 해야 하는 모든 워크플로에서 사용할 수 있습니다. 워크플로가 <xref:System.ServiceModel.Activities.WorkflowServiceHost>를 사용하여 호스트된 경우 이전 단원에서 설명한 기본 상관 관계가 적용됩니다. 그렇지 않은 경우 원하는 <xref:System.ServiceModel.Activities.CorrelationInitializer> 및 <xref:System.ServiceModel.Activities.CorrelationHandle>을 명시적으로 사용하거나 <xref:System.ServiceModel.Activities.CorrelationScope>의 암시적 핸들 관리를 사용하여 상관 관계를 구성해야 합니다.  
  
 사용 하는 경우 **서비스 참조 추가** 양방향 작업을 사용 하 여 서비스에 대해 작업이 생성 됩니다를 래핑하는 <xref:System.ServiceModel.Activities.Send> / <xref:System.ServiceModel.Activities.ReceiveReply> 쌍 요청/회신 상관 관계를 사용 하 여 내부적으로 작업을 명시적으로 지정 합니다.
