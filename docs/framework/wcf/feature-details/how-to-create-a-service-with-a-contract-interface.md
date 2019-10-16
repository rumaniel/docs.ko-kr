---
title: '방법: Contract 인터페이스를 사용하여 서비스 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7b6803f6-d6f9-4cc2-9f1b-6f4c920475d5
ms.openlocfilehash: 0aa5429d771aeda0b392b89ec4cc1a07de30973f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61787623"
---
# <a name="how-to-create-a-service-with-a-contract-interface"></a>방법: Contract 인터페이스를 사용하여 서비스 만들기
Windows Communication Foundation (WCF) 계약을 만들려면 인터페이스를 사용 하는 것이 좋습니다. 이 계약은 서비스에서 제공하는 작업에 액세스하는 데 필요한 메시지 컬렉션과 구조를 지정합니다. 이 인터페이스는 <xref:System.ServiceModel.ServiceContractAttribute> 클래스를 인터페이스에 적용하고 <xref:System.ServiceModel.OperationContractAttribute> 클래스를 노출할 메서드에 적용하여 입력 및 출력 형식을 정의합니다.  
  
 서비스 계약에 대 한 자세한 내용은 참조 하세요. [Designing Service Contracts](../../../../docs/framework/wcf/designing-service-contracts.md)합니다.  
  
### <a name="creating-a-wcf-contract-with-an-interface"></a>인터페이스로 WCF 계약 만들기  
  
1. Visual Basic을 사용 하 여 새 인터페이스를 만들 C#, 또는 기타 공용 언어 런타임 언어입니다.  
  
2. 인터페이스에 <xref:System.ServiceModel.ServiceContractAttribute> 클래스를 적용합니다.  
  
3. 인터페이스에 메서드를 정의합니다.  
  
4. 적용 된 <xref:System.ServiceModel.OperationContractAttribute> 고 공개 WCF 계약의 일부로 노출 해야 하는 각 메서드에 클래스입니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 서비스 계약을 정의하는 인터페이스를 보여 줍니다.  
  
 [!code-csharp[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createcontractwithinterface/cs/source.cs#1)]
 [!code-vb[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_createcontractwithinterface/vb/source.vb#1)]  
  
 <xref:System.ServiceModel.OperationContractAttribute> 클래스가 적용된 메서드는 기본적으로 요청-회신 메시지 패턴을 사용합니다. 이 메시지 패턴에 대 한 자세한 내용은 참조 하세요. [방법: 요청-회신 계약을 만들려면](../../../../docs/framework/wcf/feature-details/how-to-create-a-request-reply-contract.md)합니다. 특성의 속성을 설정하여 다른 메시지 패턴을 만들고 사용할 수도 있습니다. 추가 예제는 [방법: 단방향 계약을 만들려면](../../../../docs/framework/wcf/feature-details/how-to-create-a-one-way-contract.md) 고 [방법: 이중 계약 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
