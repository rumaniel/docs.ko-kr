---
title: '방법: 서비스 인스턴스 만들기 제어'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e0b12b34-8004-443a-a46d-83a5c00f2601
ms.openlocfilehash: e8efbc5a3dec5f60dbefc8f6dc377d97b29b7653
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61699619"
---
# <a name="how-to-control-service-instancing"></a>방법: 서비스 인스턴스 만들기 제어
서비스의 인스턴스 모드를 설정하면 <xref:System.ServiceModel.InstanceContext?displayProperty=nameWithType>(및 연결된 사용자 정의 서비스 개체)가 만들어지는 시기를 지정할 수 있습니다. 가능한 모드에 대해서는 <xref:System.ServiceModel.InstanceContextMode> 열거형을 참조하세요. 동작에 대 한 자세한 내용은 참조 하세요. [구성 및 동작을 사용 하 여 런타임 확장](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)합니다. 작업 예제를 보려면 [동작](../../../../docs/framework/wcf/samples/behaviors.md)합니다.  
  
### <a name="to-control-the-service-instance-lifetime-using-code"></a>코드를 사용하여 서비스 인스턴스 수명을 제어하려면  
  
1. 서비스 클래스에 <xref:System.ServiceModel.ServiceBehaviorAttribute>를 적용합니다.  
  
2. <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 속성을 <xref:System.ServiceModel.InstanceContextMode.PerCall>, <xref:System.ServiceModel.InstanceContextMode.PerSession> 또는 <xref:System.ServiceModel.InstanceContextMode.Single> 값 중 하나로 설정합니다.  
  
     [!code-csharp[C_ControlServiceInstancing#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_controlserviceinstancing/cs/source.cs#1)]
     [!code-vb[C_ControlServiceInstancing#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_controlserviceinstancing/vb/source.vb#1)]  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 특성의 <xref:System.ServiceModel.ServiceBehaviorAttribute> 속성을 <xref:System.ServiceModel.InstanceContextMode.PerCall>로 설정합니다.  
  
 [!code-csharp[c_ControlServiceInstancing#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_controlserviceinstancing/cs/source.cs#2)]
 [!code-vb[c_ControlServiceInstancing#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_controlserviceinstancing/vb/source.vb#2)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.ServiceBehaviorAttribute>
- <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>
- <xref:System.ServiceModel.InstanceContextMode>
- [서비스: 동작 샘플](../samples/behaviors.md)
