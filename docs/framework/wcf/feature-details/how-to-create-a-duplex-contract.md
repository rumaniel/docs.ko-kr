---
title: '방법: 이중 계약 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- duplex contracts [WCF]
ms.assetid: 500a75b6-998a-47d5-8e3b-24e3aba2a434
ms.openlocfilehash: c603694bca82cfc5852c875946f18f9782209e48
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64638774"
---
# <a name="how-to-create-a-duplex-contract"></a>방법: 이중 계약 만들기
이 항목에서는 이중(양방향) 계약을 사용하는 메서드를 만드는 기본 단계를 보여 줍니다. 이중 계약을 사용하면 클라이언트와 서버가 각각 독립적으로 통신하므로 서로 호출을 시작할 수 있습니다. 이중 계약에는 Windows Communication Foundation (WCF) 서비스를 사용할 수 있는 세 가지 메시지 패턴 중 하나입니다. 다른 두 가지 메시지 패턴은 단방향과 요청-회신입니다. 이중 계약은 클라이언트와 서버 간 두 개의 단방향 계약으로 구성되며, 메서드 호출을 상호 관련시키지 않아도 됩니다. 서비스가 클라이언트에 세부 정보를 쿼리하거나 클라이언트에서 이벤트를 명시적으로 발생시킬 때 이러한 종류의 계약을 사용합니다. 이중 계약에 대 한 클라이언트 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 참조 하세요. [방법: 이중 계약을 사용 하 여 서비스에 액세스할](../../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)합니다. 작업 예제를 참조 하세요. 합니다 [이중](../../../../docs/framework/wcf/samples/duplex.md) 샘플입니다.  
  
### <a name="to-create-a-duplex-contract"></a>이중 계약을 만들려면  
  
1. 이중 계약의 서버 측을 구성하는 인터페이스를 만듭니다.  
  
2. 인터페이스에 <xref:System.ServiceModel.ServiceContractAttribute> 클래스를 적용합니다.  
  
     [!code-csharp[S_WS_DualHttp#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#3)]
     [!code-vb[S_WS_DualHttp#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#3)]  
  
3. 인터페이스에 메서드 서명을 선언합니다.  
  
4. 공용 계약의 일부여야 하는 각 메서드 서명에 <xref:System.ServiceModel.OperationContractAttribute> 클래스를 적용합니다.  
  
5. 서비스가 클라이언트에서 호출할 수 있는 작업 집합을 정의하는 콜백 인터페이스를 만듭니다.  
  
     [!code-csharp[S_WS_DualHttp#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#4)]
     [!code-vb[S_WS_DualHttp#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#4)]  
  
6. 콜백 인터페이스에 메서드 서명을 선언합니다.  
  
7. 공용 계약의 일부여야 하는 각 메서드 서명에 <xref:System.ServiceModel.OperationContractAttribute> 클래스를 적용합니다.  
  
8. 기본 인터페이스의 <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A> 속성을 콜백 인터페이스의 형식으로 설정하여 이중 계약에 두 개의 인터페이스를 연결합니다.  
  
### <a name="to-call-methods-on-the-client"></a>클라이언트에서 메서드를 호출하려면  
  
1. 기본 계약의 서비스 구현에서 콜백 인터페이스에 대한 변수를 선언합니다.  
  
2. 변수를 <xref:System.ServiceModel.OperationContext.GetCallbackChannel%2A> 클래스의 <xref:System.ServiceModel.OperationContext> 메서드에서 반환한 개체 참조로 설정합니다.  
  
     [!code-csharp[S_WS_DualHttp#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#1)]
     [!code-vb[S_WS_DualHttp#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#1)]  
  
     [!code-csharp[S_WS_DualHttp#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#2)]
     [!code-vb[S_WS_DualHttp#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#2)]  
  
3. 콜백 인터페이스에서 정의한 메서드를 호출합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 이중 통신을 수행하는 방법을 보여 줍니다. 서비스의 계약에는 앞뒤로 이동하기 위한 서비스 작업이 포함됩니다. 클라이언트의 계약에는 해당 위치를 보고하는 서비스 작업이 포함됩니다.  
  
 [!code-csharp[S_WS_DualHttp#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ws_dualhttp/cs/service.cs#5)]
 [!code-vb[S_WS_DualHttp#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_ws_dualhttp/vb/service.vb#5)]  
  
- <xref:System.ServiceModel.ServiceContractAttribute> 및 <xref:System.ServiceModel.OperationContractAttribute> 특성을 적용하면 WSDL(웹 서비스 기술 언어)에서 서비스 계약 정의를 자동으로 생성할 수 있습니다.  
  
- 사용 합니다 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) WSDL 문서 및 (선택 사항) 코드 및 클라이언트에 대 한 구성을 검색할 수 있습니다.  
  
- 이중 서비스를 노출하는 엔드포인트를 보호해야 합니다. 서비스가 이중 메시지를 받으면 들어오는 해당 메시지에서 ReplyTo를 확인하여 회신을 보낼 위치를 결정합니다. 채널이 보안되지 않으면 신뢰할 수 없는 클라이언트가 대상 컴퓨터의 ReplyTo를 사용하여 악의적인 메시지를 보낼 수 있으므로 해당 대상 컴퓨터의 서비스 거부가 발생할 수 있습니다. 정규 요청-회신 메시지를 사용하는 경우에는 ReplyTo가 무시되고 원래 메시지가 들어온 채널에서 응답이 보내지므로 이러한 문제가 생기지 않습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [방법: 이중 계약을와 함께 access Services](../../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)
- [이중](../../../../docs/framework/wcf/samples/duplex.md)
- [서비스 디자인 및 구현](../../../../docs/framework/wcf/designing-and-implementing-services.md)
- [방법: 서비스 계약 정의](../../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)
- [세션](../../../../docs/framework/wcf/samples/session.md)
