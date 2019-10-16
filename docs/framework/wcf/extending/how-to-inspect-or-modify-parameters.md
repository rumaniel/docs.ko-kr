---
title: '방법: 매개 변수 검사 또는 수정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ab6c0ac7-aac4-45ba-93d6-a0e9afd1756f
ms.openlocfilehash: b4a673f97f06e8d489d9acc85d84e1ecea4656e4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795591"
---
# <a name="how-to-inspect-or-modify-parameters"></a>방법: 매개 변수 검사 또는 수정
인터페이스를 <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType> 구현 하 여 클라이언트 또는 서비스 런타임에 삽입 하 여 wcf (Windows Communication Foundation) 클라이언트 개체 또는 wcf 서비스에서 단일 작업에 대해 들어오거나 나가는 메시지를 검사 하거나 수정할 수 있습니다. 일반적으로 작업 동작을 사용하여 단일 작업에 매개 변수 검사자를 추가하지만, 다른 동작을 사용하여 더 넓은 범위의 런타임에 쉬운 액세스를 제공할 수도 있습니다. 자세한 내용은 [클라이언트 확장](extending-clients.md) 및 [디스패처 확장](extending-dispatchers.md)을 참조 하세요.  
  
### <a name="inspecting-or-modifying-parameters"></a>매개 변수 검사 또는 수정  
  
1. <xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=nameWithType> 인터페이스를 구현합니다.  
  
2. 필요한 범위에 따라 <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType>, <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType>, <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType>를 구현하여 매개 변수 검사자를 <xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.Dispatcher.DispatchOperation.ParameterInspectors%2A?displayProperty=nameWithType> 속성에 추가합니다.  
  
3. <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=nameWithType>에서 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> 또는 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> 메서드를 호출하기 전에 동작을 삽입합니다. 자세한 내용은 [동작을 사용 하 여 런타임 구성 및 확장](configuring-and-extending-the-runtime-with-behaviors.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 코드 예제는 아래 순서대로 나열되어 있습니다.  
  
- 매개 변수 검사자 구현.  
  
- <xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=nameWithType>, <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType> 및 <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=nameWithType>를 사용하여 매개 변수 검사자를 삽입하는 동작 구현.  
  
- 클라이언트 애플리케이션에서 엔드포인트 동작을 로드하고 실행하여 클라이언트에 매개 변수 검사자를 삽입하는 구성 파일.  
  
 [!code-csharp[Interceptors#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/interceptors.cs#4)]
 [!code-vb[Interceptors#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/interceptors.vb#4)]  
  
 [!code-csharp[Interceptors#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/insertingbehaviors.cs#5)]
 [!code-vb[Interceptors#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/insertingbehaviors.vb#5)]  
  
 [!code-xml[Interceptors#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/client.exe.config#3)]  
  
## <a name="see-also"></a>참고자료

- [동작을 사용하여 런타임 구성 및 확장](configuring-and-extending-the-runtime-with-behaviors.md)
