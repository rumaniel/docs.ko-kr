---
title: 상관 관계 개요
ms.date: 03/30/2017
ms.assetid: edcc0315-5d26-44d6-a36d-ea554c418e9f
ms.openlocfilehash: 7128ff531bb81fb6de526092513d5525ca138735
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61857335"
---
# <a name="correlation-overview"></a>상관 관계 개요
상관 관계는 워크플로 서비스 메시지를 서로 연결하거나 애플리케이션 상태와 연결하는 메커니즘입니다. 예를 들어 응답을 초기 요청과 연결하거나 특정 주문 ID를 주문 처리 워크플로의 지속된 상태와 연결할 수 있습니다. 이 항목에서는 상관 관계에 대해 간략하게 설명하고 이 단원의 다른 항목에서는 각 상관 관계 형식에 대해 자세히 설명합니다.  
  
## <a name="types-of-correlation"></a>상관 관계 형식  
 상관 관계는 프로토콜 기반 또는 내용 기반일 수 있습니다. 프로토콜 기반 상관 관계는 메시지 배달 인프라에서 제공하는 데이터를 사용하여 메시지 간의 매핑을 제공합니다. 프로토콜 기반 상관 관계를 사용하여 상호 관련된 메시지는 메모리에 있는 개체(예: <xref:System.ServiceModel.Channels.RequestContext>)를 사용하거나 전송 프로토콜에서 제공하는 토큰에 의해 서로 연결됩니다. 내용 기반 상관 관계는 애플리케이션에서 지정한 데이터를 사용하여 메시지를 서로 연결합니다. 내용 기반 상관 관계를 사용하여 상호 관련된 메시지는 해당 메시지에 있는 일부 애플리케이션 정의 데이터(예: 고객 번호)를 사용하여 서로 연결됩니다.  
  
 상관 관계에 참여하는 작업은 <xref:System.ServiceModel.Activities.CorrelationHandle>을 사용하여 메시징 작업을 서로 연결합니다. 예를 들어 서비스를 호출하는 데 사용되는 <xref:System.ServiceModel.Activities.Send>와 서비스로부터 콜백을 받은 데 사용되는 후속 <xref:System.ServiceModel.Activities.Receive>는 동일한 <xref:System.ServiceModel.Activities.CorrelationHandle>을 공유합니다. 이 기본 패턴은 내용 기반 상관 관계와 프로토콜 상관 관계에서 모두 사용됩니다. 즉, 각 작업에 상관 관계 핸들을 명시적으로 설정하거나 <xref:System.ServiceModel.Activities.CorrelationScope> 작업에 작업을 포함할 수 있습니다. <xref:System.ServiceModel.Activities.CorrelationScope>에 포함된 작업은 <xref:System.ServiceModel.Activities.CorrelationScope>를 통해 해당 상관 관계 핸들을 관리하기 때문에 <xref:System.ServiceModel.Activities.CorrelationHandle>을 명시적으로 설정할 필요가 없습니다. <xref:System.ServiceModel.Activities.CorrelationScope> 범위는 요청-회신 상관 관계 및 하나의 추가 상관 관계 형식에 <xref:System.ServiceModel.Activities.CorrelationHandle> 관리를 제공합니다. <xref:System.ServiceModel.Activities.WorkflowServiceHost>를 사용하여 호스트된 워크플로 서비스는 <xref:System.ServiceModel.Activities.CorrelationScope> 작업과 동일한 기본 상관 관계 관리를 사용합니다. 일반적으로 이 기본 상관 관계 관리는 두 개의 <xref:System.ServiceModel.Activities.CorrelationScope> 작업이 나란히 있거나 두 개의 <xref:System.ServiceModel.Activities.CorrelationHandle> 작업 뒤에 두 개의 <xref:System.ServiceModel.Activities.Receive> 작업이 있는 것과 같이 여러 메시징 작업이 나란히 있거나 겹치지 않는 한 대부분의 경우에 <xref:System.ServiceModel.Activities.Send> 또는 워크플로 서비스의 메시징 작업에 해당 <xref:System.ServiceModel.Activities.Receive> 집합이 필요 없음을 의미합니다. 기본 상관 관계는 이 단원에서 각 상관 관계 형식에 대해 설명하는 항목에서 자세히 설명합니다. 메시징 활동에 대 한 자세한 내용은 참조 하세요. [메시징 활동](../../../../docs/framework/wcf/feature-details/messaging-activities.md) 고 [방법: 메시징 활동에서 워크플로 서비스 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-with-messaging-activities.md)합니다.  
  
## <a name="protocol-based-correlation"></a>프로토콜 기반 상관 관계

프로토콜 기반 상관 관계는 전송 메커니즘을 사용하여 메시지를 서로 연결하거나 적절한 인스턴스와 연결합니다. 일부 시스템 제공 프로토콜 상관 관계에는 요청-회신 상관 관계와 컨텍스트 기반 상관 관계가 포함됩니다. 요청-회신 상관 관계는 <xref:System.ServiceModel.Activities.Send>와 쌍을 이루는 <xref:System.ServiceModel.Activities.ReceiveReply> 또는 <xref:System.ServiceModel.Activities.Receive>와 쌍을 이루는 <xref:System.ServiceModel.Activities.SendReply>처럼 한 쌍의 메시징 작업을 상호 연결하여 양방향 작업을 만드는 데 사용됩니다. Visual Studio Workflow Designer에는 또한 신속 하 게이 패턴을 구현 하려면 작업 템플릿 집합도 제공 합니다. 컨텍스트 기반 상관 관계에 설명 된 컨텍스트 교환 메커니즘을 기반으로 합니다 [.NET Context Exchange Protocol Specification](https://go.microsoft.com/fwlink/?LinkID=166059)합니다. 컨텍스트 상관 관계를 사용하려면 엔드포인트에서 <xref:System.ServiceModel.BasicHttpContextBinding>, <xref:System.ServiceModel.WSHttpContextBinding> 또는 <xref:System.ServiceModel.NetTcpContextBinding>을 사용해야 합니다.  
  
프로토콜 상관 관계에 대 한 자세한 내용은 참조 하세요. [영 속 이중](../../../../docs/framework/wcf/feature-details/durable-duplex-correlation.md) 하 고 [요청-회신](../../../../docs/framework/wcf/feature-details/request-reply-correlation.md)합니다. Visual Studio Workflow Designer 작업 템플릿을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [메시징 활동](../../../../docs/framework/wcf/feature-details/messaging-activities.md)합니다. 샘플 코드에 대 한 참조를 [NetContextExchangeCorrelation](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ee662963%28v%3dvs.100%29) 샘플입니다.  
  
## <a name="content-based-correlation"></a>내용 기반 상관 관계

내용 기반 상관 관계는 메시지에 있는 일부 정보를 사용하여 해당 메시지를 특정 인스턴스와 연결합니다. 프로토콜 기반 상관 관계와 달리 내용 기반 상관 관계는 애플리케이션 작성자가 연결된 각 메시지에서 이러한 데이터를 찾을 수 있는 위치를 명시적으로 지정해야 합니다. 내용 기반 상관 관계를 사용하는 작업은 <xref:System.ServiceModel.MessageQuerySet>을 사용하여 이 메시지 데이터를 지정합니다. 내용 기반 상관 관계는 <xref:System.ServiceModel.BasicHttpContextBinding>과 같은 컨텍스트 바인딩 중 하나를 사용하지 않는 서비스와 통신할 때 유용합니다.
  
## <a name="see-also"></a>참고자료

- [NetContextExchangeCorrelation](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ee662963%28v%3dvs.100%29)
