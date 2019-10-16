---
title: '방법: ProtectionLevel 속성 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, security
- ProtectionLevel property
ms.assetid: 3d4e8f80-0f9e-4a26-9899-beb6584e78df
ms.openlocfilehash: 222fda180923cdc7b0d7b7ab413c151c69add259
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950975"
---
# <a name="how-to-set-the-protectionlevel-property"></a>방법: ProtectionLevel 속성 설정
적절한 특성을 적용하고 속성을 설정하여 보호 수준을 설정할 수 있습니다. 각 메시지의 모든 부분에 영향을 주도록 서비스 수준에서 보호를 설정하거나 메서드에서 메시지 부분으로 점차 세부적인 수준에서 보호를 설정할 수 있습니다. 에 대 한 자세한 내용은 합니다 `ProtectionLevel` 속성을 참조 하세요 [보호 수준 이해](../../../docs/framework/wcf/understanding-protection-level.md)합니다.  
  
> [!NOTE]
> 구성이 아닌 코드에서만 보호 수준을 설정할 수 있습니다.  
  
### <a name="to-sign-all-messages-for-a-service"></a>서비스의 모든 메시지를 서명하려면  
  
1. 서비스에 대한 인터페이스를 만듭니다.  
  
2. 다음 코드에 표시된 것처럼 <xref:System.ServiceModel.ServiceContractAttribute> 특성을 서비스에 적용하고 <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> 속성을 <xref:System.Net.Security.ProtectionLevel.Sign>으로 설정합니다. 기본 수준은 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>입니다.  
  
     [!code-csharp[C_ProtectionLevel#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#1)]
     [!code-vb[C_ProtectionLevel#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#1)]  
  
### <a name="to-sign-all-message-parts-for-an-operation"></a>작업에 대한 모든 메시지 부분을 서명하려면  
  
1. 서비스에 대한 인터페이스를 만들고 <xref:System.ServiceModel.ServiceContractAttribute> 특성을 인터페이스에 적용합니다.  
  
2. 메서드 선언을 인터페이스에 추가합니다.  
  
3. 다음 코드에 표시된 것처럼 <xref:System.ServiceModel.OperationContractAttribute> 특성을 메서드에 적용하고 <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> 속성을 <xref:System.Net.Security.ProtectionLevel.Sign>으로 설정합니다.  
  
     [!code-csharp[C_ProtectionLevel#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#2)]
     [!code-vb[C_ProtectionLevel#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#2)]  
  
## <a name="protecting-fault-messages"></a>오류 메시지 보호  
 서비스에서 throw된 예외는 클라이언트에 SOAP 오류로 전송될 수 있습니다. 강력한 형식의 오류를 만드는 방법에 대 한 자세한 내용은 [계약 및 서비스에서 오류 지정 및 처리](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md) 및 [방법: 서비스 계약](../../../docs/framework/wcf/how-to-declare-faults-in-service-contracts.md)에서 오류를 선언 합니다.  
  
#### <a name="to-protect-a-fault-message"></a>오류 메시지를 보호하려면  
  
1. 오류 메시지를 나타내는 형식을 만듭니다. 다음 예제에서는 두 개의 필드를 사용하여 `MathFault`라는 클래스를 만듭니다.  
  
2. 다음 코드에 표시된 것처럼 <xref:System.Runtime.Serialization.DataContractAttribute> 특성을 형식에 적용하고 <xref:System.Runtime.Serialization.DataMemberAttribute> 특성을 serialize해야 하는 각 필드에 적용합니다.  
  
     [!code-csharp[C_ProtectionLevel#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#3)]
     [!code-vb[C_ProtectionLevel#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#3)]  
  
3. 오류를 반환할 인터페이스에서 <xref:System.ServiceModel.FaultContractAttribute> 특성을 오류를 반환할 메서드에 적용하고 `detailType` 매개 변수를 오류 클래스 형식으로 설정합니다.  
  
4. 또한 다음 코드에 표시된 것처럼 생성자에서 <xref:System.ServiceModel.FaultContractAttribute.ProtectionLevel%2A> 속성을 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>으로 설정합니다.  
  
     [!code-csharp[C_ProtectionLevel#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#4)]
     [!code-vb[C_ProtectionLevel#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#4)]  
  
## <a name="protecting-message-parts"></a>메시지 부분 보호  
 메시지 계약을 사용하여 메시지의 일부분을 보호합니다. 메시지 계약에 대 한 자세한 내용은 [메시지 계약 사용](../../../docs/framework/wcf/feature-details/using-message-contracts.md)을 참조 하세요.  
  
#### <a name="to-protect-a-message-body"></a>메시지 본문을 보호하려면  
  
1. 메시지를 나타내는 형식을 만듭니다. 다음 예제에서는 `Company` 및 `CompanyName` 필드를 사용하여 `CompanyID`를 만듭니다.  
  
2. <xref:System.ServiceModel.MessageContractAttribute> 특성을 클래스에 적용하고 <xref:System.ServiceModel.MessageContractAttribute.ProtectionLevel%2A> 속성을 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>으로 설정합니다.  
  
3. <xref:System.ServiceModel.MessageHeaderAttribute> 특성을 메시지 헤더로 표시될 필드에 적용하고 `ProtectionLevel` 특성을 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign>으로 설정합니다.  
  
4. 다음 예제와 같이를 메시지 본문의 일부로 표시 될 필드 `ProtectionLevel` <xref:System.Net.Security.ProtectionLevel.EncryptAndSign> <xref:System.ServiceModel.MessageBodyMemberAttribute> 에 적용 하 고 속성을로 설정 합니다.  
  
     [!code-csharp[C_ProtectionLevel#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#5)]
     [!code-vb[C_ProtectionLevel#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#5)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 서비스의 다양한 위치에서 여러 특성 클래스의 `ProtectionLevel` 속성을 설정합니다.  
  
 [!code-csharp[C_ProtectionLevel#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#6)]
 [!code-vb[C_ProtectionLevel#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#6)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 다음 코드에서는 예제 코드를 컴파일하는 데 필요한 네임스페이스를 보여 줍니다.  
  
 [!code-csharp[C_ProtectionLevel#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#0)]
 [!code-vb[C_ProtectionLevel#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#0)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.ServiceModel.MessageContractAttribute>
- <xref:System.ServiceModel.MessageBodyMemberAttribute>
- [보호 수준 이해](../../../docs/framework/wcf/understanding-protection-level.md)
