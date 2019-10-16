---
title: '방법: 권한을 부여하는 동안 메타데이터 요청 허용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- allowing metadata requests while authorizing [WCF]
ms.assetid: 90cec34f-b619-452b-a056-8b1c0de49d05
ms.openlocfilehash: bea4f7e90df29678697fe6708bdc6a73145522db
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62047804"
---
# <a name="how-to-allow-metadata-requests-while-authorizing"></a>방법: 권한을 부여하는 동안 메타데이터 요청 허용
사용자 지정 인증을 수행하는 동안 메타데이터를 처리하도록 요청을 허용해야 할 수 있습니다. 다음 항목에서는 이러한 요청의 유효성을 검사하는 단계에 대해 설명합니다.  
  
 Windows Communication Foundation (WCF) 권한 부여에 대 한 자세한 내용은 참조 하세요. [권한 부여](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)합니다.  
  
### <a name="to-allow-metadata-requests-during-authorization"></a>권한을 부여하는 동안 메타데이터 요청을 허용하려면  
  
1. <xref:System.ServiceModel.ServiceAuthorizationManager> 클래스의 확장을 만듭니다.  
  
2. <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> 메서드를 재정의합니다. 메서드는 권한 부여가 허용되는지 여부에 따라 `true` 또는 `false`를 반환합니다. 현재 프로시저에 대한 정보는 매개 변수로서 메서드에 전달된 <xref:System.ServiceModel.OperationContext>에 있습니다.  
  
3. 재정의하는 동안 다음 예제에서처럼 계약 이름, 네임스페이스 및 작업을 확인합니다. 조건이 올바른 경우 `true.`가 반환됩니다.  
  
4. 확장성 지점을 사용하여 클래스를 채택합니다. 자세한 내용은 [방법: 서비스에 대 한 사용자 지정 권한 부여 관리자 만들기](../../../../docs/framework/wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md)합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> 메서드의 재정의를 보여 줍니다.  
  
 [!code-csharp[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/cs/source.cs#1)]
 [!code-vb[C_HowtoCheckForMexRequestsInAuthorization#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtocheckformexrequestsinauthorization/vb/source.vb#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.ServiceAuthorizationManager>
- [권한 부여](../../../../docs/framework/wcf/feature-details/authorization-in-wcf.md)
- [ID 모델을 사용하여 클레임 및 권한 부여 관리](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)
